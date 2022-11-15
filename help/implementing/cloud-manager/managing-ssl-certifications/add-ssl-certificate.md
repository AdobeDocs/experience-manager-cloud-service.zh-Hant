---
title: 正在新增 SSL 憑證
description: 了解如何使用 Cloud Manager 的自助服務工具新增您自己的 SSL 憑證。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 14e0255b3ce2ca44579b9fc3de6c7b7f5d8f34b6
workflow-type: ht
source-wordcount: '579'
ht-degree: 100%

---

# 新增 SSL 憑證 {#adding-an-ssl-certificate}

了解如何使用 Cloud Manager 的自助服務工具新增您自己的 SSL 憑證。

>[!TIP]
>
>提供憑證可能需要幾天時間。因此，Adobe 建議提前準備好憑證。

## 憑證格式 {#certificate-format}

SSL 憑證文件必須是 PEM 格式才能與 Cloud Manager 一起安裝。PEM 格式的常見文件附檔名包括 `.pem,`。`crt`、`.cer` 和 `.cert`。

以下 `openssl` 命令可用於轉換非 PEM 憑證。

* 將 PFX 轉換為 PEM

   ```shell
   openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
   ```

* 將 P7B 轉換為 PEM

   ```shell
   openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
   ```

* 將 DER 轉換為 PEM

   ```shell
   openssl x509 -inform der -in certificate.cer -out certificate.pem
   ```

## 正在新增憑證 {#adding-a-cert}

依照以下步驟使用 Cloud Manager 新增憑證。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選擇適當的組織和計劃。

1. 從&#x200B;**概覽**&#x200B;頁面瀏覽&#x200B;**環境**&#x200B;畫面。

1. 從瀏覽面板點擊 **SSL 憑證**。包含任何現有 SSL 憑證詳細資訊的表格將顯示在主畫面上。

   ![新增 SSL 憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 點擊新增 **SSL 憑證**&#x200B;開啟&#x200B;**新增 SSL 憑證**&#x200B;對話方塊。

   * 在&#x200B;**憑證名稱**&#x200B;中輸入憑證名稱。
      * 這僅供參考，可以是任何有助於您輕鬆引用憑證的名稱。
   * 在對應欄位中貼上&#x200B;**憑證**、**私人金鑰**&#x200B;和&#x200B;**憑證鏈**&#x200B;值。所有三個欄位都是必填項目。

   ![新增憑證對話方塊](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * 將顯示偵測到的任何錯誤。
      * 您必須先解決所有錯誤，然後才能保存您的憑證。
      * 請參閱[憑證錯誤](#certificate-errors)部分以了解有關解決常見錯誤的更多資訊。


1. 點擊&#x200B;**儲存**&#x200B;來儲存您的憑證。

儲存後，您將看到您的憑證在資料表中顯示為新的資料列。

![已儲存的 SSL 憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>使用者必須是 **商務擁有者** 的成員或&#x200B;**部署管理員**&#x200B;職務，在 Cloud Manager 中安裝 SSL 憑證。

## 憑證錯誤 {#certificate-errors}

如果憑證未正確安裝或未滿足 Cloud Manager 的要求，可能會出現某些錯誤。

### 憑證政策 {#certificate-policy}

如果您看到以下錯誤，請檢查您的憑證的政策。

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
>這兩個命令的輸出必須完全相同。如果您找不到匹配的私鑰`main/server`憑證，您將需要透過生成新的 CSR 和/或向您的 SSL 供應商請求更新的憑證來重新加密憑證。

### 憑證有效期 {#certificate-validity-dates}

Cloud Manager 預計 SSL 憑證從當前日期起至少 90 天內有效。您應該檢查憑證鏈結的有效性。
