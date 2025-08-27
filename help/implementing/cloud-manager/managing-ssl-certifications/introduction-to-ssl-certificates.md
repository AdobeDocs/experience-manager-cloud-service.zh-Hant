---
title: SSL 憑證簡介
description: 瞭解Cloud Manager提供的自助服務工具，用於安裝和管理SSL憑證。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f1e9b76742c8d97f44ff974fb8686fdcb3d804e6
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 17%

---


# SSL 憑證簡介{#introduction}

瞭解Cloud Manager提供的自助服務工具，用於安裝和管理SSL （安全通訊端層）憑證。

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理 SSL 憑證"
>abstract="了解 Cloud Manager 如何利用自助服務工具來安裝和管理 SSL 憑證，協助您的使用者保護您的網站。Cloud Manager 使用平台 TLS 服務來管理客戶擁有並從第三方憑證授權單位獲得的 SSL 憑證和私密金鑰。"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/cicd-pipelines/manage-ssl-certificates/managing-certificates" text="檢視、更新和取代 SSL 憑證"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/cicd-pipelines/manage-ssl-certificates/managing-certificates" text="檢查 SSL 憑證狀態"

## 什麼是SSL憑證？ {#overview}

企業和組織使用SSL （安全通訊端層）憑證來保護他們的網站，並讓他們的客戶信任他們。 若要使用SSL通訊協定，Web伺服器需要SSL憑證。

當實體（例如組織或企業）向憑證授權單位(CA)要求憑證時，CA會完成驗證程式。 此程式的範圍包括從驗證網域名稱控制到收集公司註冊檔案和訂閱者協定。 在實體的資訊獲得驗證後，CA會使用CA的私密金鑰簽署其公開金鑰。 因為所有主要的憑證授權單位在Web瀏覽器中都有根憑證，實體的憑證會透過&#x200B;*信任鏈*&#x200B;連結，而且網頁瀏覽器會將其識別為受信任的憑證。

>[!IMPORTANT]
>
>Cloud Manager 不提供 SSL 憑證或私密金鑰。這些部分必須從憑證授權單位（受信任的第三方組織）取得。 某些知名的憑證授權單位包括&#x200B;*DigiCert*、*Let&#39;s Encrypt*、*GlobalSign*、*Entrust*&#x200B;和&#x200B;*Verisign*。

## 使用Cloud Manager管理憑證 {#cloud-manager}

Cloud Manager提供自助服務工具來安裝和管理SSL憑證，確保使用者的網站安全性。 Cloud Manager支援兩種管理憑證的模式。

| | 模型 | 說明 |
| --- | --- | --- |
| A | **[Adobe管理的SSL憑證(DV)](#adobe-managed)** | Cloud Manager可讓使用者設定Adobe所提供的DV （網域驗證）憑證，以進行快速網域設定。 |
| B | **[客戶管理的SSL憑證(OV/EV)](#customer-managed)** | Cloud Manager提供平台TLS （傳輸層安全性）服務，可讓您管理您所擁有的OV和EV SSL憑證，以及來自協力廠商憑證授權單位的私密金鑰，例如&#x200B;*Let&#39;s Encrypt*。 |

這兩種模式都提供下列管理憑證的一般功能：

* 每個 Cloud Manager 環境都可以使用多個憑證。
* 一個私密金鑰可以發行多個 SSL 憑證。
* 平台 TLS 服務根據用於終止的 SSL 憑證和託管該網域的 CDN 服務將要求路由到客戶的 CDN 服務。

>[!IMPORTANT]
>
>[若要新增自訂網域並與環境建立關聯](/help/implementing/cloud-manager/custom-domain-names/introduction.md)，您必須擁有涵蓋網域的有效SSL憑證。

### Adobe管理的(DV) SSL憑證 {#adobe-managed}

DV憑證是最基本的SSL憑證等級，通常用於測試目的或透過基本加密保護網站。 DV憑證可在[生產程式和沙箱程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)中使用。

建立DV憑證後，Adobe會每三個月自動更新一次，除非該憑證被刪除。

>[!IMPORTANT]
>
>如果您的環境使用(DV) SSL憑證進行CNAME型驗證，請注意，在自動憑證續約之前移除CNAME記錄可能會導致續約失敗。 移除可能會導致憑證過期和服務中斷。 若要避免此問題，請確定CNAME記錄在整個續約過程中保持不變。 續約程式需仰賴CNAME記錄的存在以進行網域擁有權驗證。

### 客戶管理的(OV/EV) SSL憑證 {#customer-managed}

OV和EV憑證提供CA驗證的資訊。 這類資訊可協助使用者評估網站所有者、電子郵件寄件者或程式碼或PDF檔案的數位簽署者是否值得信任。 DV 憑證不允許此類所有權驗證。

OV和EV另外在Cloud Manager中透過DV憑證提供這些功能。

* 多個環境可以使用OV/EV憑證。 也就是說，可以新增一次，但使用多次。
* 每個OV/EV憑證通常包含多個網域。
* Cloud Manager接受網域的萬用字元OV/EV憑證。

>[!TIP]
>
>如果您有多個自訂網域，則可能不希望每次新增網域時都上傳憑證。 在這種情況下，您可以透過取得涵蓋多個網域的單一憑證受益。

#### 客戶管理的OV/EV SSL憑證需求 {#requirements}

如果您選擇新增自己的客戶管理SSL憑證，該憑證必須符合下列更新要求：

* 不支援網域驗證(DV)憑證和自簽憑證。
* 憑證必須符合OV （組織驗證）或EV （擴展驗證）政策。
* 憑證必須是受信任的憑證授權單位(CA)所核發的X.509 TLS憑證。
* 支援的密碼編譯金鑰型別包括：

   * RSA 2048位元，標準支援。
目前不支援大於2048位元的RSA金鑰（例如3072位元或4096位元的RSA金鑰）。
   * 橢圓曲線(EC)索引鍵`prime256v1` (`secp256r1`)和`secp384r1`
   * 橢圓曲線數位簽章演演算法(ECDSA)憑證。 Adobe建議您使用這類憑證來取代RSA，以提升效能、安全性和效率。

* 憑證的格式必須正確才能通過驗證。 私密金鑰必須為`PKCS#8`格式。

>[!NOTE]
>如果您的組織需要使用3072位元RSA金鑰的規範遵循，Adobe建議的替代方法是使用ECDSA憑證（`secp256r1`或`secp384r1`）。


#### 憑證管理的最佳實務

* **避免憑證重疊：**

   * 若要確保順暢的憑證管理，請避免部署與相同網域相符的重疊憑證。 例如，搭配使用萬用字元憑證(*.example.com)和特定憑證(dev.example.com)可能會導致混淆。
   * TLS層會優先處理最近部署的特定憑證。

  案例範例：

   * 「開發憑證」涵蓋`dev.example.com`，並部署為`dev.example.com`的網域對應。
   * 「中繼憑證」涵蓋`stage.example.com`，並部署為`stage.example.com`的網域對應。
   * 如果「中繼憑證」在&#x200B;*「開發憑證」之後部署/更新*，它也會為`dev.example.com`提供要求。

     若要避免這類衝突，請確保將憑證的適用範圍仔細限定到其預期的網域。

* **萬用字元憑證：**

  雖然支援萬用字元憑證（例如`*.example.com`），但只有在必要時才應該使用。 在重疊的情況下，以更具體的憑證優先。 例如，特定憑證提供`dev.example.com`，而非萬用字元(`*.example.com`)。

* **驗證和疑難排解：**
嘗試使用Cloud Manager安裝憑證之前，Adobe建議您使用`openssl`等工具在本機驗證憑證的完整性。 例如，

  `openssl verify -untrusted intermediate.pem certificate.pem`


<!--
>[!NOTE]
>
>If two certificates cover the same domain are installed, the one that is more exact is applied.
>
>For example, if your domain is `dev.adobe.com` and you have one certificate for `*.adobe.com` and another for `dev.adobe.com`, the more specific one (`dev.adobe.com`) is used.
-->

#### 客戶管理的憑證格式 {#certificate-format}

SSL 憑證文件必須是 PEM 格式才能與 Cloud Manager 一起安裝。PEM格式的一般副檔名包括`.pem,`。 `crt`、`.cer` 和 `.cert`。

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

## 已安裝SSL憑證數量的限制 {#limitations}

在任何指定時間，Cloud Manager最多可支援50個已安裝的憑證。 這些憑證可以與您的計畫中的一個或多個環境相關聯，並且還包括任何過期的憑證。

如果您已達到限制，請檢視您的憑證並考慮刪除任何過期的憑證。 或者，將多個網域群組在同一個憑證中，因為一個憑證可以涵蓋多個網域（最多100個SAN）。

## 了解更多 {#learn-more}

具有必要權限的使用者可以使用 Cloud Manager 來管理計畫的 SSL 憑證。如需有關使用這些功能的更多詳細資訊，請參閱以下文件。

* [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

