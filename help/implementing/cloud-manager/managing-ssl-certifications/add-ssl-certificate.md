---
title: 新增SSL憑證——管理SSL憑證
description: 新增SSL憑證——管理SSL憑證
translation-type: tm+mt
source-git-commit: 88ef9265b40f64f2229e37e5f8ca02959e8d9ce2
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 添加SSL證書{#adding-an-ssl-certificate}

>[!NOTE]
>AEM做為雲端服務將只接受OV（組織驗證）或EV（延伸驗證）憑證。 DV（網域驗證）憑證將不會被接受。

憑證布建需要數天，建議在數個月前布建憑證。 如需詳細資訊，請參閱[取得SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)。

## 證書格式{#certificate-format}

SSL檔案必須採用PEM格式，才能安裝在Cloud Manager上。 PEM格式內的常見副檔名包括`.pem,`。`crt`、 `.cer`和 `.cert`。

請依照下列步驟，將SSL檔案的格式轉換為PEM:

1. 將PFX轉換為PEM

`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

1. 將P7B轉換為PEM

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

1. 將DER轉換為PEM

`openssl x509 -inform der -in certificate.cer -out certificate.pem`

## 添加證書{#adding-certificate}

>[!NOTE]
>* 用戶必須是「業務擁有者」或「部署管理員」角色，才能在Cloud Manager中安裝SSL憑證。
>* Cloud Manager在任何指定時間內，最多可允許10個SSL憑證，這些憑證可與您方案中的一個或多個環境相關聯，即使憑證已過期亦然。 不過，Cloud Manager UI允許在此限制下，在程式中安裝最多50個SSL憑證。


請依照下列步驟新增憑證：

1. 登入Cloud Manager。
1. 從&#x200B;**概述**&#x200B;頁面導覽至&#x200B;**環境**&#x200B;畫面。
1. 從左側導覽功能表按一下「**SSL憑證**」。 此螢幕上將顯示一個包含任何現有SSL證書詳細資訊的表。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)
1. 選擇&#x200B;**添加證書**&#x200B;按鈕以開啟&#x200B;**添加SSL證書**&#x200B;對話框。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-2.png)
   1. 在&#x200B;**證書名稱**&#x200B;中輸入證書的名稱。 此名稱可協助您輕鬆參考憑證。
   1. 將&#x200B;**證書**、**私鑰**&#x200B;和&#x200B;**證書鏈**&#x200B;貼上到各自的欄位中。 使用輸入方塊右側的貼上圖示。

      >[!NOTE]
      >這三個欄位都不是選用欄位，必須加入。
1. 按一下&#x200B;**Save**&#x200B;以送出憑證。 您會在表格中看到它顯示為新列。
   >[!NOTE]
   >將顯示檢測到的任何錯誤。 您必須先解決所有錯誤，才能儲存憑證。 請參閱[Certificate Errors](#certificate-errors)以進一步瞭解如何解決常見錯誤。

## 證書錯誤{#certificate-errors}

### 正確的證書順序{#correct-certificate-order}

憑證部署失敗的最常見原因是中間或鏈式憑證順序不正確。 具體來說，中間證書檔案必須以最靠近根證書的根證書或證書結尾，並且從`main/server`證書到根證書的降序順序。

您可以使用以下命令確定中間檔案的順序：

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

您可以使用下列命令來驗證私鑰和`main/server`證書是否匹配：

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>這兩個命令的輸出必須完全相同。 如果您找不到與`main/server`憑證相符的私密金鑰，則必須產生新的CSR並／或向SSL廠商要求更新的憑證，以重新建立憑證的金鑰。

### 證書有效日期{#certificate-validity-dates}

Cloud Manager預計SSL憑證在未來至少90天內有效

檢查證書鏈的有效性。
