---
title: 新增SSL憑證
description: 了解如何使用Cloud Manager的自助服務工具新增您自己的SSL憑證。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 14e0255b3ce2ca44579b9fc3de6c7b7f5d8f34b6
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# 新增SSL憑證 {#adding-an-ssl-certificate}

了解如何使用Cloud Manager的自助服務工具新增您自己的SSL憑證。

>[!TIP]
>
>憑證可能需要數天時間才能布建。 因此，Adobe建議事先布建憑證。

## 憑證格式 {#certificate-format}

SSL憑證檔案必須採用PEM格式才能與Cloud Manager一起安裝。 PEM格式的常見副檔名包括 `.pem,` .`crt`, `.cer`, 和 `.cert`.

以下 `openssl` 命令來轉換非PEM憑證。

* 將PFX轉換為PEM

   ```shell
   openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
   ```

* 將P7B轉換為PEM

   ```shell
   openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
   ```

* 將DER轉換為PEM

   ```shell
   openssl x509 -inform der -in certificate.cer -out certificate.pem
   ```

## 新增憑證 {#adding-a-cert}

請依照下列步驟，使用Cloud Manager新增憑證。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **環境** 螢幕 **概述** 頁面。

1. 按一下 **SSL憑證** 從左側導覽面板。 主畫面上會顯示包含任何現有SSL憑證詳細資訊的表格。

   ![新增SSL憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 按一下 **新增SSL憑證** 開啟 **新增SSL憑證** 對話框。

   * 在 **憑證名稱**.
      * 這僅供參考，可以是任何可協助您輕鬆參考憑證的名稱。
   * 貼上 **憑證**, **私密金鑰**，和 **憑證鏈** 值填入其各自的欄位中。 這三個欄位都是必填欄位。

   ![「添加SSL證書」對話框](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * 將顯示檢測到的任何錯誤。
      * 您必須先解決所有錯誤，才能儲存憑證。
      * 請參閱 [憑證錯誤](#certificate-errors) 一節，以進一步了解如何處理常見錯誤。


1. 按一下 **儲存** 來儲存憑證。

儲存後，您會在表格中看到憑證顯示為新列。

![已儲存SSL憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>使用者必須是 **業務負責人** 或 **部署管理員** 角色，以在Cloud Manager中安裝SSL憑證。

## 憑證錯誤 {#certificate-errors}

若未正確安裝憑證或符合Cloud Manager的要求，便可能會產生某些錯誤。

### 證書策略 {#certificate-policy}

如果您看到下列錯誤，請檢查憑證的原則。

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

通常，證書策略由嵌入的OID值標識。 將證書輸出為文本並搜索OID將顯示證書的策略。

您可以使用下列範例作為指南，將憑證詳細資料輸出為文字。

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

文本中的OID模式定義證書的策略類型。

| 圖樣 | 政策 | Cloud Manager可接受 |
|---|---|---|
| `2.23.140.1.1` | EV | 是 |
| `2.23.140.1.2.2` | OV | 是 |
| `2.23.140.1.2.1` | DV | 否 |

依據 `grep`在輸出證書文本中對OID模式執行ping操作，可以確認證書策略。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### 正確的證書順序 {#correct-certificate-order}

憑證部署失敗的最常見原因，是中間或鏈式憑證的順序不正確。

中間憑證檔案的結尾必須是根憑證，或最接近根憑證的憑證。 它們必須以 `main/server` 憑證至根。

您可以使用下列命令來判斷中間檔案的順序。

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

您可以確認私密金鑰和 `main/server` 證書使用以下命令匹配。

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>這兩個命令的輸出必須完全相同。 如果您找不到 `main/server` 憑證時，您必須產生新CSR及/或向SSL廠商要求更新的憑證，以重新輸入憑證。

### 證書有效日期 {#certificate-validity-dates}

Cloud Manager預期SSL憑證自目前日期起至少90天內有效。 您應該檢查憑證鏈的有效性。
