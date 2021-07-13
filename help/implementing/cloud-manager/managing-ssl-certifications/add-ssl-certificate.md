---
title: 新增SSL憑證 — 管理SSL憑證
description: 新增SSL憑證 — 管理SSL憑證
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 3b4a9d7c04a5f4feecad0f34c27a894c187152e7
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 新增SSL憑證 {#adding-an-ssl-certificate}

>[!NOTE]
>AEM as aCloud Service只會接受OV（組織驗證）或EV（延伸驗證）憑證。 不接受DV（域驗證）證書。 此外，任何證書都必須是來自受信任認證機構(CA)的X.509 TLS證書，且具有相符的2048位RSA私鑰。 AEM as aCloud Service會接受網域的萬用字元SSL憑證。

憑證布建需要數天的時間，建議您提前數個月布建憑證。 如需詳細資訊，請參閱[取得SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) 。

## 憑證格式 {#certificate-format}

SSL檔案必須為PEM格式，才能安裝在Cloud Manager上。 PEM格式內的常見副檔名包括`.pem,` 。`crt`、  `.cer`和 `.cert`。

請依照下列步驟，將SSL檔案的格式轉換為PEM:

* 將PFX轉換為PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* 將P7B轉換為PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* 將DER轉換為PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## 重要考量 {#important-considerations}

* 使用者必須處於業務擁有者或部署管理員角色中，才能在Cloud Manager中安裝SSL憑證。

* 在任何指定時間，Cloud Manager最多可允許10個SSL憑證，此憑證可與您方案中的一或多個環境建立關聯，即使憑證已過期亦然。 不過，在具有此限制的程式中，Cloud Manager UI將允許安裝最多50個SSL憑證。 通常，證書可以覆蓋多個域（最多100個SAN），因此請考慮將同一證書中的多個域分組，以便保持在此限制內。


## 新增憑證 {#adding-a-cert}

請依照下列步驟新增憑證：

1. 登入Cloud Manager。
1. 從&#x200B;**概述**&#x200B;頁面導覽至&#x200B;**環境**&#x200B;畫面。
1. 按一下左側導覽功能表中的&#x200B;**SSL憑證**。 此畫面會顯示包含任何現有SSL憑證詳細資訊的表格。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 按一下&#x200B;**添加SSL證書**&#x200B;以開啟&#x200B;**添加SSL證書**&#x200B;對話框。

   * 在&#x200B;**證書名稱**&#x200B;中輸入證書的名稱。 這可以是任何可協助您輕鬆參考憑證的名稱。
   * 將&#x200B;**憑證**、**私密金鑰**&#x200B;和&#x200B;**憑證鏈**貼到其各自的欄位。 使用輸入方塊右側的貼上圖示。
這三個欄位均非選用欄位，且必須包含。

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >將顯示檢測到的任何錯誤。 您必須先解決所有錯誤，才能儲存憑證。 請參閱[憑證錯誤](#certificate-errors)以深入了解如何解決常見錯誤。

1. 按一下&#x200B;**Save**&#x200B;以提交證書。 您會在表格中看到它顯示為新列。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## 憑證錯誤 {#certificate-errors}

### 正確的證書順序 {#correct-certificate-order}

憑證部署失敗的最常見原因，是中間或鏈式憑證的順序不正確。 具體而言，中間證書檔案的結尾必須是根證書或證書最接近根，並且從`main/server`證書到根證書的降序順序。

您可以使用下列命令來判斷中間檔案的順序：

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

您可以使用以下命令驗證私鑰和`main/server`證書是否匹配：

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>這兩個命令的輸出必須完全相同。 如果您找不到與`main/server`憑證相符的私密金鑰，則需要透過產生新CSR及/或向SSL廠商要求更新的憑證，來重新輸入憑證。

### 證書有效日期 {#certificate-validity-dates}

Cloud Manager預期SSL憑證在未來至少90天內有效。 您應該檢查憑證鏈的有效性。
