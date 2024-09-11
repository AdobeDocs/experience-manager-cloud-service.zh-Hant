---
title: 疑難排解SSL憑證錯誤
description: 瞭解如何識別常見原因以疑難排解SSL憑證錯誤，進而維護安全連線。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9ffec422ec4b5a45962f07142c49a466e8892754
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 63%

---


# 疑難排解SSL憑證錯誤 {#certificate-errors}

如果憑證未正確安裝或不符合Cloud Manager的要求，可能會出現某些錯誤。

+++**正確的憑證順序**

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

+++

+++**移除使用者端憑證**

新增憑證時，如果您收到類似下列的錯誤：

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

您可能在憑證鏈結中包含使用者端憑證。 請確定該鏈結不包含使用者端憑證，然後再試一次。

+++

+++**憑證原則**

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

+++

+++**憑證有效日期**

Cloud Manager 預計 SSL 憑證從當前日期起至少 90 天內有效。檢查憑證鏈結的有效性。

+++