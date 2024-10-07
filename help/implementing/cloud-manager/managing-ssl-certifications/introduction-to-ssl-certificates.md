---
title: SSL 憑證簡介
description: 瞭解Cloud Manager提供的自助服務工具，用於安裝和管理SSL憑證。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 912e63b2ff11e24392fc7509945f352ab07c60cc
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 22%

---


# SSL 憑證簡介{#introduction}

瞭解Cloud Manager提供的自助服務工具，用於安裝和管理SSL （安全通訊端層）憑證。

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理 SSL 憑證"
>abstract="了解 Cloud Manager 如何提供自助服務工具來安裝和管理 SSL 憑證，為您的使用者保護您的網站。Cloud Manager 使用平台 TLS 服務來管理客戶擁有並從第三方憑證授權單位獲得的 SSL 憑證和私密金鑰。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="檢視、更新和取代 SSL 憑證"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="檢查 SSL 憑證狀態"

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
| A | **[Adobe受管理憑證(DV)](#adobe-managed)** | Cloud Manager可讓使用者設定Adobe所提供的DV （網域驗證）憑證，以進行快速網域設定。 |
| B | **[客戶管理的憑證(OV/EV)](#customer-managed)** | Cloud Manager提供平台TLS （傳輸層安全性）服務，可讓您管理您所擁有的OV和EV SSL憑證，以及來自協力廠商憑證授權單位的私密金鑰，例如&#x200B;*Let&#39;s Encrypt*。 |

這兩種模式都提供下列管理憑證的一般功能：

* 每個 Cloud Manager 環境都可以使用多個憑證。
* 一個私密金鑰可以發行多個 SSL 憑證。
* 平台 TLS 服務根據用於終止的 SSL 憑證和託管該網域的 CDN 服務將要求路由到客戶的 CDN 服務。

>[!IMPORTANT]
>
>[若要新增自訂網域並與環境建立關聯](/help/implementing/cloud-manager/custom-domain-names/introduction.md)，您必須擁有涵蓋網域的有效SSL憑證。

### AdobeManaged憑證 {#adobe-managed}

DV憑證是最基本的SSL憑證等級，通常用於測試目的或透過基本加密保護網站。 DV憑證可在[生產程式和沙箱程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)中使用。

建立DV憑證後，Adobe每三個月會自動更新一次，除非憑證被刪除。

### 客戶管理的憑證 {#customer-managed}

OV和EV憑證提供CA驗證的資訊。 這類資訊可協助使用者評估網站所有者、電子郵件寄件者或程式碼或PDF檔案的數位簽署者是否可信。 DV 憑證不允許此類所有權驗證。

OV和EV另外在Cloud Manager中透過DV憑證提供這些功能。

* 多個環境可以使用OV/EV憑證。
   * 也就是說，可以新增一次，但使用多次。
* 每個OV/EV憑證通常包含多個網域。
* Cloud Manager接受網域的萬用字元OV/EV憑證。

>[!TIP]
>
>如果您有多個自訂網域，則可能不希望每次新增網域時都上傳憑證。 在這種情況下，您可以透過取得涵蓋多個網域的單一憑證受益。

>[!NOTE]
>
>如果已安裝兩個涵蓋相同網域的憑證，則會套用更精確的憑證。
>
>例如，如果您的網域是`dev.adobe.com`，而您有`*.adobe.com`的一個憑證和`dev.adobe.com`的另一個憑證，則會使用更具體的憑證(`dev.adobe.com`)。

#### 客戶管理憑證的需求 {#requirements}

如果您選擇上傳自己的EV/OV憑證，該憑證必須符合以下要求：

* AEM as a Cloud Service接受符合OV （組織驗證）或EV （擴展驗證）原則的憑證。
   * Cloud Manager不支援上傳您自己的DV （網域驗證）憑證。
* 任何憑證都必須是來自受信任憑證授權單位的X.509 TLS憑證，並具有相符的2048位元RSA私密金鑰。
* 不接受自我簽署憑證。

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

>[!TIP]
>
>Adobe建議您先使用`openssl verify -untrusted intermediate.pem certificate.pem`之類的工具在本機驗證憑證的完整性，然後再嘗試使用Cloud Manager進行安裝。

## 已安裝SSL憑證數量的限制 {#limitations}

在任何指定時間，Cloud Manager允許最多安裝50個SSL憑證。 這些憑證可以與您的計畫中的一個或多個環境相關聯，並且還包括任何過期的憑證。

如果您已達到限制，請檢視您的憑證並考慮刪除任何過期的憑證。 或者，將多個網域群組在同一個憑證中，因為一個憑證可以涵蓋多個網域（最多100個SAN）。

## 了解更多 {#learn-more}

具有必要權限的使用者可以使用 Cloud Manager 來管理計畫的 SSL 憑證。如需有關使用這些功能的更多詳細資訊，請參閱以下文件。

* [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

