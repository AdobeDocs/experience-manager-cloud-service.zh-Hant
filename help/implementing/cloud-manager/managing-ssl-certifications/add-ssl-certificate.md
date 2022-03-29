---
title: 添加SSL證書
description: 瞭解如何使用Cloud Manager的自助服務工具添加您自己的SSL證書。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 2c87d5fb33b83ca77b97391e4b0baaf38f8dd026
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# 添加SSL證書 {#adding-an-ssl-certificate}

瞭解如何使用Cloud Manager的自助服務工具添加您自己的SSL證書。

>[!TIP]
>
>證書可能需要幾天時間才能配置。 因此，Adobe建議提前預配證書。

## 證書格式 {#certificate-format}

SSL證書檔案必須採用PEM格式才能隨Cloud Manager一起安裝。 PEM格式的公共檔案擴展包括 `.pem,` 。`crt`。 `.cer`, `.cert`。

以下 `openssl` 命令可用於轉換非PEM證書。

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

## 添加證書 {#adding-a-cert}

按照以下步驟使用雲管理器添加證書。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **環境** 螢幕 **概述** 的子菜單。

1. 按一下 **SSL證書** 的下界。 主螢幕上將顯示一個包含任何現有SSL證書詳細資訊的表。

   ![添加SSL證書](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 按一下 **添加SSL證書** 開啟 **添加SSL證書** 對話框。

   * 在中輸入證書的名稱 **證書名稱**。
      * 這僅供參考，可以是任何有助於您輕鬆引用證書的名稱。
   * 貼上 **證書**。 **私鑰**, **證書鏈** 值。
      * 可以使用輸入框右側的貼上表徵圖。
      * 這三個欄位都是必填的。

   ![「添加SSL證書」對話框](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * 將顯示檢測到的任何錯誤。
      * 必須解決所有錯誤，才能保存證書。
      * 請參閱 [證書錯誤](#certificate-errors) 的子菜單。


1. 按一下 **保存** 保存證書。

保存後，您將在表中看到證書顯示為新行。

![已保存SSL證書](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>用戶必須是 **業務所有者** 或 **部署管理器** 角色，以便在雲管理器中安裝SSL證書。

## 證書錯誤 {#certificate-errors}

如果證書安裝不正確或滿足Cloud Manager的要求，可能會出現某些錯誤。

### 證書策略 {#certificate-policy}

如果您看到以下錯誤，請檢查證書的策略。

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

通常，證書策略由嵌入的OID值標識。 將證書輸出到文本並搜索OID將顯示證書的策略。

您可以使用以下示例作為指南將證書詳細資訊輸出為文本。

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

| 圖案 | 政策 | 在雲管理器中可接受 |
|---|---|---|
| `2.23.140.1.1` | EV | 是 |
| `2.23.140.1.2.2` | OV | 是 |
| `2.23.140.1.2.1` | DV | 否 |

按 `grep`對於輸出證書文本中的OID模式，您可以確認證書策略。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### 正確的證書訂單 {#correct-certificate-order}

證書部署失敗的最常見原因是中間或鏈證書的順序不正確。

中間證書檔案必須以根證書或最接近根證書的證書結尾。 它們必須按從 `main/server` 證書到根。

可以使用以下命令確定中間檔案的順序。

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

您可以驗證私鑰和 `main/server` 證書與以下命令匹配。

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>這兩個命令的輸出必須完全相同。 如果找不到您的 `main/server` 證書，您將需要通過生成新的CSR和/或向SSL供應商請求更新的證書來重新密鑰證書。

### 證書有效日期 {#certificate-validity-dates}

Cloud Manager要求SSL證書在當前日期起至少90天內有效。 您應檢查證書鏈的有效性。
