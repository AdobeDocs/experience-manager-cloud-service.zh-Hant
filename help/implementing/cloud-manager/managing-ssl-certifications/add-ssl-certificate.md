---
title: 添加SSL證書 — 管理SSL證書
description: 添加SSL證書 — 管理SSL證書
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# 添加SSL證書 {#adding-an-ssl-certificate}

>[!NOTE]
>AEMas a Cloud Service只接受符合OV（組織驗證）或EV（擴展驗證）策略的證書。 將不接受DV（域驗證）策略。 此外，任何證書都必須是來自受信任證書頒發機構(CA)的X.509 TLS證書，其中具有匹配的2048位RSA私鑰。 AEMas a Cloud Service將接受域的通配符SSL證書。

配置證書需要幾天時間，建議提前數月配置證書。 請參閱 [獲取SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) 的子菜單。

## 證書格式 {#certificate-format}

SSL檔案必須採用PEM格式才能安裝在Cloud Manager上。 PEM格式內的常用檔案副檔名包括 `.pem,` 。`crt`。 `.cer`, `.cert`。

按照以下步驟將SSL檔案的格式轉換為PEM:

* 將PFX轉換為PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* 將P7B轉換為PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* 將DER轉換為PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## 重要注意事項 {#important-considerations}

* 用戶必須處於「業務所有者」或「部署管理器」角色中，才能在雲管理器中安裝SSL證書。

* 在任何給定時間，Cloud Manager都允許最多10個SSL證書，這些證書可以與您程式中的一個或多個環境關聯，即使證書已過期。 但是，Cloud Manager UI將允許在此約束下在程式中安裝最多50個SSL證書。 通常，證書可以覆蓋多個域（最多100個SAN），因此請考慮將同一證書中的多個域分組，以保持在此限制內。


## 添加證書 {#adding-a-cert}

按照以下步驟添加證書：

1. 登錄到雲管理器。
1. 導航到 **環境** 螢幕 **概述** 的子菜單。
1. 按一下 **SSL證書** 的下界。 此螢幕上將顯示一個包含任何現有SSL證書詳細資訊的表。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 按一下 **添加SSL證書** 開啟 **添加SSL證書** 對話框。

   * 在中輸入證書的名稱 **證書名稱**。 這可以是任何有助於您輕鬆引用證書的名稱。
   * 貼上 **證書**。 **私鑰** 和 **證書鏈** 進入各自的領域。 使用輸入框右側的貼上表徵圖。
這三個欄位都不是可選的，必須包括在內。

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >將顯示檢測到的任何錯誤。 必須解決所有錯誤，才能保存證書。 請參閱 [證書錯誤](#certificate-errors) 瞭解有關解決常見錯誤的詳細資訊。

1. 按一下 **保存** 提交證書。 您將在表中看到它顯示為新行。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## 證書錯誤 {#certificate-errors}

### 證書策略 {#certificate-policy}

如果您看到錯誤「證書策略必須符合EV或OV，而不符合DV策略。」，請檢查證書策略。

通常，證書類型由策略中嵌入的OID值標識。 這些OID是唯一的，因此將證書轉換為文本表單並搜索OID將確認證書具有匹配項。

您可以按如下方式查看證書詳細資訊。

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

此表提供標識模式。

| 圖案 | 證書類型 | 可接受 |
|---|---|---|
| `2.23.140.1.2.1` | DV | 否 |
| `2.23.140.1.2.2` | OV | 是 |
| `2.23.140.1.2.3`與`TLS Web Server Authentication` | 具有用於https權限的IV證書 | 是 |

`grep`對於模式，您可以確認證書類型。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### 正確的證書訂單 {#correct-certificate-order}

證書部署失敗的最常見原因是中間或鏈證書的順序不正確。 具體來說，中間證書檔案必須以根證書或最接近根證書的證書結尾，並且從根證書開始按降序排列 `main/server` 證書到根。

可以使用以下命令確定中間檔案的順序：

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

您可以驗證私鑰和 `main/server` 證書匹配：

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>這兩個命令的輸出必須完全相同。 如果找不到與您的 `main/server` 證書，您將需要通過生成新的CSR和/或向SSL供應商請求更新的證書來重新密鑰證書。

### 證書有效日期 {#certificate-validity-dates}

Cloud Manager希望SSL證書在將來至少90天內有效。 您應檢查證書鏈的有效性。
