---
title: 新增SSL憑證——管理SSL憑證
description: 新增SSL憑證——管理SSL憑證
translation-type: tm+mt
source-git-commit: b6911f0b8674550713bd4ec1e34be5d0a14cc427
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# 添加SSL證書{#adding-an-ssl-certificate}

>[!NOTE]
>AEM做為雲端服務將只接受OV（組織驗證）或EV（延伸驗證）憑證。 DV（網域驗證）憑證將不會被接受。

憑證布建需要數天，建議在數個月前布建憑證。 如需詳細資訊，請參閱「取得SSL憑證」。

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
1. 從「概述」頁面導覽至「環境」畫面。
1. 從左側導覽功能表導覽至「SSL憑證」畫面。 此螢幕上將顯示一個包含任何現有SSL證書詳細資訊的表。
1. 選擇&#x200B;**添加證書**&#x200B;按鈕以啟動嚮導。
   1. 提供憑證的名稱。 此名稱可協助您輕鬆參考憑證。
   1. 將「憑證」、「私密金鑰」和「鎖鏈」內容貼入其各自的欄位。 使用輸入方塊右側的貼上圖示。

      >[!NOTE]
      >這三個欄位都不是選用欄位，必須加入。
1. 提交憑證後，您會在表格中看到它顯示為新列。


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
