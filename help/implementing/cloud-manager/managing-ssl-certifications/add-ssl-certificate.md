---
title: 新增SSL憑證 — 管理SSL憑證
description: 新增SSL憑證 — 管理SSL憑證
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# 新增SSL憑證 {#adding-an-ssl-certificate}

>[!NOTE]
>AEMas a Cloud Service僅接受符合OV（組織驗證）或EV（延伸驗證）原則的憑證。 不接受DV（域驗證）策略。 此外，任何證書都必須是來自受信任認證機構(CA)的X.509 TLS證書，且具有相符的2048位RSA私鑰。 AEMas a Cloud Service會接受網域的萬用字元SSL憑證。

憑證布建需要數天的時間，建議您提前數個月布建憑證。 請參閱 [取得SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) 以取得更多詳細資訊。

## 憑證格式 {#certificate-format}

SSL檔案必須為PEM格式，才能安裝在Cloud Manager上。 PEM格式內的常見副檔名包括 `.pem,` .`crt`, `.cer`，和 `.cert`.

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
1. 導覽至 **環境** 螢幕 **概述** 頁面。
1. 按一下 **SSL憑證** 的上界。 此畫面會顯示包含任何現有SSL憑證詳細資訊的表格。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 按一下 **新增SSL憑證** 開啟 **新增SSL憑證** 對話框。

   * 在 **憑證名稱**. 這可以是任何可協助您輕鬆參考憑證的名稱。
   * 貼上 **憑證**, **私密金鑰** 和 **憑證鏈** 進入各自的欄位。 使用輸入方塊右側的貼上圖示。
這三個欄位均非選用欄位，且必須包含。

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >將顯示檢測到的任何錯誤。 您必須先解決所有錯誤，才能儲存憑證。 請參閱 [憑證錯誤](#certificate-errors) 以進一步了解如何處理常見錯誤。

1. 按一下 **儲存** 來提交憑證。 您會在表格中看到它顯示為新列。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## 憑證錯誤 {#certificate-errors}

### 證書策略 {#certificate-policy}

如果您看到錯誤「證書策略必須符合EV或OV，而不是DV策略。」，請檢查證書的策略。

通常，證書類型由嵌入在策略中的OID值標識。 這些OID是唯一的，因此將證書轉換為文本形式，搜索OID將確認證書具有匹配項。

您可以依下列方式檢視憑證詳細資料。

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

本表提供識別模式。

| 圖樣 | 憑證類型 | 可接受 |
|---|---|---|
| `2.23.140.1.2.1` | DV | 否 |
| `2.23.140.1.2.2` | OV | 是 |
| `2.23.140.1.2.3`與`TLS Web Server Authentication` | IV證書，允許使用https | 是 |

`grep`對於模式，您可以確認憑證類型。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### 正確的證書順序 {#correct-certificate-order}

憑證部署失敗的最常見原因，是中間或鏈式憑證的順序不正確。 具體而言，中間憑證檔案的結尾必須是根憑證或憑證最接近根憑證，且必須以從 `main/server` 憑證至根。

您可以使用下列命令來判斷中間檔案的順序：

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

您可以確認私密金鑰和 `main/server` 證書與以下命令匹配：

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>這兩個命令的輸出必須完全相同。 如果您找不到相符的私密金鑰，請 `main/server` 憑證時，您必須產生新CSR及/或向SSL廠商要求更新的憑證，以重新輸入憑證。

### 證書有效日期 {#certificate-validity-dates}

Cloud Manager預期SSL憑證在未來至少90天內有效。 您應該檢查憑證鏈的有效性。
