---
title: 新增SSL憑證
description: 了解如何使用 Cloud Manager 的自助服務工具新增您自己的 SSL 憑證。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 64aa010c3d840adad9e1ab6040a6d80c07cd8455
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 50%

---


# 新增SSL憑證 {#adding-an-ssl-certificate}

了解如何使用 Cloud Manager 的自助服務工具新增您自己的 SSL 憑證。

>[!TIP]
>
>提供憑證可能需要幾天時間。因此，Adobe建議在任何期限或上線日期之前提供憑證。

## 憑證需求 {#certificate-requirements}

檢閱[管理SSL憑證簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements)中的&#x200B;**憑證需求**，以確定AEM as a Cloud Service支援您要新增的憑證。

## 新增憑證 {#adding-a-cert}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**概觀**&#x200B;頁面，瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 從左側導覽面板的&#x200B;**服務**&#x200B;下，按一下&#x200B;**SSL憑證**。 (如有必要，您可能需要按一下左上角的漢堡圖示，以使用導覽面板。 隨即顯示一個表格，其中包含任何現有SSL憑證的詳細資訊。

   ![新增SSL憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 按一下&#x200B;**新增SSL憑證**&#x200B;以開啟&#x200B;**新增SSL憑證**&#x200B;對話方塊。

   * 在&#x200B;**憑證名稱**&#x200B;中輸入憑證名稱。 此欄位僅供參考，可以是任何有助於您輕鬆引用憑證的名稱。
   * 在對應欄位中貼上&#x200B;**憑證**、**私人金鑰**&#x200B;和&#x200B;**憑證鏈**&#x200B;值。這三個欄位都是必填欄位。

   ![新增SSL憑證對話方塊](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * 將顯示值中偵測到的任何錯誤。 您必須先解決所有錯誤，才能儲存憑證。
請參閱[憑證錯誤](#certificate-errors)，深入瞭解如何解決常見錯誤。

1. 按一下「**儲存**」。

![已儲存的SSL憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)您的憑證現在會在表格中顯示為新列，類似於上圖。

>[!NOTE]
>
>使用者必須具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色，才能在 Cloud Manager 中安裝 SSL 憑證。

## 憑證錯誤 {#certificate-errors}

如果憑證未正確安裝或未滿足 Cloud Manager 的要求，可能會出現某些錯誤。

### 正確的憑證順序 {#correct-certificate-order}

憑證部署失敗的最常見原因是中間憑證或鏈憑證的順序不正確。

中間憑證文件必須以根憑證或最接近根的憑證結尾。它們必須按降序排列`main/server`憑證到根。

您可以使用以下命令確定中間文件的順序。

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

您可以驗證私鑰和`main/server`使用以下命令進行憑證匹配。

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>這兩個命令的輸出必須完全相同。如果您無法為您的 `main/server` 憑證找到相符的私密金鑰，您需要透過產生新的 CSR 和/或向您的 SSL 供應商請求更新的憑證來重新加密憑證。

### 移除使用者端憑證 {#client-certificates}

新增憑證時，如果您收到類似下列的錯誤：

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

您可能在憑證鏈結中包含使用者端憑證。 請確定該鏈結不包含使用者端憑證，然後再試一次。

### 憑證原則 {#certificate-policy}

如果您看到以下錯誤，請檢查您的憑證政策。

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

嵌入的OID值通常會識別憑證策略。 將憑證輸出為文字並搜尋OID會顯示憑證的策略。

您可以使用以下範例作為指南將您的憑證詳細資訊輸出為文字。

```text
openssl x509 -in 9178c0f58cb8fccc.pem -text
certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            91:78:c0:f5:8c:b8:fc:cc
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, ST = Arizona, L = Scottsdale, O = "GoDaddy.com, Inc.", OU = http://certs.godaddy.com/repository/, CN = Go Daddy Secure Certificate Authority - G2
        Validity
            Not Before: Nov 10 22:55:36 2021 GMT
            Not After : Dec  6 15:35:06 2022 GMT
        Subject: C = US, ST = Colorado, L = Denver, O = Alexandra Alwin, CN = adobedigitalimpact.com
        Subject Public Key Info:
...
```

文字中的 OID 模式定義了憑證的策略類型。

| 模式 | 政策 | Cloud Manager 中的已接受內容 |
|---|---|---|
| `2.23.140.1.1` | EV | 是 |
| `2.23.140.1.2.2` | OV | 是 |
| `2.23.140.1.2.1` | DV | 否 |

透過`grep`ping 輸出憑證文字中的 OID 模式，您可以確認您的憑證策略。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### 憑證有效日期 {#certificate-validity-dates}

Cloud Manager 預計 SSL 憑證從當前日期起至少 90 天內有效。檢查憑證鏈結的有效性。

## 後續步驟 {#next-steps}

恭喜！您現在擁有專案的有效的SSL憑證。 此步驟通常是第一個設定自訂網域名稱的步驟。

* 若要設定自訂網域名稱，請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
* 若要瞭解如何在Cloud Manager中更新及管理SSL憑證，請參閱[管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)。
