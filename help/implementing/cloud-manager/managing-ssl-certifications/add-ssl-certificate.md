---
title: 新增SSL憑證
description: 瞭解如何使用Cloud Manager的自助服務工具新增您自己的SSL憑證或DV （網域驗證）憑證。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3aec9d13e2eb4bbc9a972e28195a6f43e92c1842
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 27%

---


# 新增SSL憑證

瞭解如何使用Cloud Manager的自助服務工具新增客戶管理的SSL憑證或Adobe產生和管理的DV （網域驗證）憑證。


## 新增SSL或DV憑證 {#adding-an-ssl-certificate}

提供憑證可能需要幾天時間。因此，Adobe建議在任何截止日期或上線日期之前提供憑證。

請務必在[管理SSL憑證簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements)中檢閱&#x200B;**憑證需求**，以確定AEM as a Cloud Service支援您要新增的憑證。

使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能完成此工作。

>[!NOTE]
>
>不允許客戶上傳DV （網域驗證）憑證。

**若要新增SSL或DV憑證：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從「**概觀**」頁面，瀏覽到「**環境**」畫面。

1. 從左側導覽面板的&#x200B;**服務**&#x200B;下，按一下&#x200B;**SSL憑證**。 如果您看不到下圖所示的左側導覽面板，您可能需要按一下左上角的漢堡圖示。

   ![正在新增SSL憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. 在頁面的右上角附近，按一下&#x200B;**新增SSL憑證**。

1. 在&#x200B;**新增SSL憑證**&#x200B;對話方塊中，根據[您的特定使用案例](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)，執行下列其中一項作業：

   | | 使用案例 | 步驟 |
   | --- | --- | --- |
   | 1 | **新增Adobe管理的憑證(DV)** | **若要新增Adobe管理的憑證(DV)：**<br> a。選取憑證型別&#x200B;**受管理的Adobe(DV)**。<br>![新增DV憑證](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b。在&#x200B;**選取網域**&#x200B;下拉式清單中，選取一或多個要與DV憑證關聯的網域。<br>沒有要選取的網域？ 若是如此，表示您必須新增自訂網域。 請參閱[新增自訂網域](#add-custom-domain)。 新增完自訂網域名稱后，請返回本主題並從步驟1重新開始。<br>天。繼續步驟7。 |
   | 2 | **新增客戶管理的憑證(OV/EV)** | **若要新增客戶管理的憑證(OV/EV)：**<br> a。選取憑證型別&#x200B;**客戶管理的(OV/EV)**。<br>b。在&#x200B;**憑證名稱**&#x200B;欄位中，輸入憑證的名稱。 此欄位僅供參考，可以是任何有助於您輕鬆引用憑證的名稱。<br>c。在&#x200B;**憑證**、**私密金鑰**&#x200B;和&#x200B;**憑證鏈**&#x200B;欄位中，將必要的值貼到各自的欄位中。<br>![新增SSL憑證對話方塊](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>顯示值中偵測到的任何錯誤。 您必須先解決所有錯誤，才能儲存憑證。 請參閱[憑證錯誤](#certificate-errors)，深入了解疑難排解常見錯誤。<br>天。繼續步驟7。 |

<!--
    **Add an SSL certificate:**
    1. Select the certificate type **Customer managed (OV/EV)**.
    1. In **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your certificate easily.
    1. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.

        ![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)
  
    Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate errors](#certificate-errors) to learn more about troubleshooting common errors.

    **Add a DV certificate:**
    1. Select the certificate type **Adobe managed (DV)**.

        ![Adding a DC certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

    1. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV certificate.

        No domains to select? If so, it means that you must add a custom domain. See [Add a custom domain](#add-custom-domain). When you are finished, resume the steps from the beginning again. -->

1. 在對話框右下角，按一下「**儲存**」。

   成功發行憑證後，會顯示綠色勾號，如上圖所示

   ![已核發的DV憑證](assets/issued-dv-certificate.png)

### 新增自訂網域 {#add-custom-domain}

您必須先新增自訂網域，才能新增Adobe產生並管理的網域驗證(DV)憑證。 此程式與[自訂網域名稱簡介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)和[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)中的詳細程式幾乎相同。 不過，此功能現在已稍微擴充，如下所述。

1. 新增自訂網域名稱時，請在&#x200B;**驗證網域**&#x200B;對話方塊中，選取&#x200B;**Adobe受管理憑證**。

   ![選擇Adobe管理](assets/verify-domain-dialog.png)

1. 在&#x200B;**驗證網域**&#x200B;對話方塊中，將CNAME驗證記錄新增至您的DNS。

   ![新增CNAME專案](assets/verify-domain-dialog-adobe-managed.png)

1. 建立網域後，按一下網域清單中的省略符號按鈕，然後選取&#x200B;**驗證**&#x200B;以驗證網域。

   ![驗證網域](assets/verify-domain.png)

1. 繼續執行工作[新增DV憑證](#adding-an-ssl-certificate)。

### 疑難排解憑證錯誤 {#certificate-errors}

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

## 後續步驟 {#next-steps}

您現在已為專案新增有效的SSL憑證。 此步驟通常是第一個設定自訂網域名稱的步驟。

* 若要設定自訂網域名稱，請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
* 若要瞭解如何在Cloud Manager中更新及管理SSL憑證，請參閱[管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)。
