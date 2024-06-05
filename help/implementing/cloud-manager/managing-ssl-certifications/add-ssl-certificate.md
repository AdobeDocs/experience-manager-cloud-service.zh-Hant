---
title: 正在新增 SSL 憑證
description: 了解如何使用 Cloud Manager 的自助服務工具新增您自己的 SSL 憑證。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 80%

---

# 新增 SSL 憑證 {#adding-an-ssl-certificate}

了解如何使用 Cloud Manager 的自助服務工具新增您自己的 SSL 憑證。

>[!TIP]
>
>提供憑證可能需要幾天時間。因此，Adobe 建議提前準備好憑證。

## 憑證需求 {#certificate-requirements}

檢閱區段 **憑證需求** 檔案 [管理SSL憑證的簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) 以確保AEMas a Cloud Service支援您要新增的憑證。

## 正在新增憑證 {#adding-a-cert}

依照以下步驟使用 Cloud Manager 新增憑證。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**概觀**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 按一下 **SSL憑證** 從左側導覽面板。 包含任何現有 SSL 憑證詳細資訊的表格會顯示在主畫面上。

   ![新增 SSL 憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 按一下 **新增SSL憑證** 以開啟 **新增SSL憑證** 對話方塊。

   * 在&#x200B;**憑證名稱**&#x200B;中輸入憑證名稱。
      * 這僅供參考，可以是任何有助於您輕鬆引用憑證的名稱。
   * 在對應欄位中貼上&#x200B;**憑證**、**私人金鑰**&#x200B;和&#x200B;**憑證鏈**&#x200B;值。所有三個欄位都是必填項目。
   * 在某些情況下，終端使用者證書可能會包含在鏈中，並且必須在將鏈貼上到欄位之前將其清除。

   ![新增憑證對話方塊](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * 會顯示偵測到的任何錯誤。
      * 您必須先解決所有錯誤，然後才能保存您的憑證。
      * 請參閱[憑證錯誤](#certificate-errors)章節以了解有關解決常見錯誤的更多資訊。

1. 按一下&#x200B;**儲存**&#x200B;來儲存您的憑證。

儲存後，您會看到憑證在表格中顯示為新的一列。

![已儲存的 SSL 憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>使用者必須具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色，才能在 Cloud Manager 中安裝 SSL 憑證。

>[!NOTE]
>
>如果您收到類似以下的錯誤 `The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.`，您可能會將使用者端憑證納入憑證鏈中。 請確定該鏈結不包含使用者端憑證，然後再試一次。

## 憑證錯誤 {#certificate-errors}

如果憑證未正確安裝或未滿足 Cloud Manager 的要求，可能會出現某些錯誤。

### 憑證政策 {#certificate-policy}

如果您看到以下錯誤，請檢查您的憑證政策。

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

通常憑證策略由嵌入的 OID 值標識。將憑證輸出為文字並搜尋 OID 將顯示憑證的策略。

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

### 憑證有效期 {#certificate-validity-dates}

Cloud Manager 預計 SSL 憑證從當前日期起至少 90 天內有效。您應該檢查憑證鏈結的有效性。
