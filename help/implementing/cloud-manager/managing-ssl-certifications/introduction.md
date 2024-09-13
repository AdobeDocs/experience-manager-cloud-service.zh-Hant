---
title: SSL憑證簡介
description: 了解 Cloud Manager 如何提供自助服務工具以安裝 SSL 憑證。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d2f05915c0bf0af073db7f070b83f13aeae55252
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 34%

---


# SSL憑證簡介{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理 SSL 憑證"
>abstract="了解 Cloud Manager 如何提供自助服務工具來安裝和管理 SSL 憑證，為您的使用者保護您的網站。Cloud Manager 使用平台 TLS 服務來管理客戶擁有並從第三方憑證授權單位獲得的 SSL 憑證和私密金鑰。"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="檢視、更新和取代 SSL 憑證"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="檢查 SSL 憑證狀態"


Cloud Manager提供自助服務工具來安裝和管理SSL （安全通訊端層）憑證，確保使用者的網站安全性。 支援以下兩個使用案例：

<!-- CQDOC-21758, #1 -->

| | 使用案例 | 說明 |
| --- | --- | --- |
| 1 | **Adobe受管理憑證(DV)** | Cloud Manager可讓使用者設定來自Adobe的DV （網域驗證）憑證，以進行快速網域設定。 DV憑證是最基本的SSL憑證等級，通常用於測試目的或透過基本加密保護網站。 DV憑證可在[生產程式和沙箱程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)中使用。 建立DV憑證後，Adobe每三個月會自動更新一次，除非憑證被刪除。 |
| 2 | **客戶管理的憑證(OV/EV)** | Cloud Manager使用平台TLS （傳輸層安全性）服務來管理客戶擁有的SSL憑證，以及來自協力廠商憑證授權單位（例如&#x200B;*Let&#39;s Encrypt*）的私密金鑰。 |

>[!NOTE]
>
>不允許客戶上傳DV （網域驗證）憑證。


## SSL憑證簡介 {#certificates}

企業和組織使用SSL憑證來保護他們的網站，並允許他們的客戶信任他們。 為了使用 SSL 協議，Web 伺服器需要使用 SSL 憑證。

當實體（例如組織或企業）向憑證授權單位(CA)要求憑證時，CA會完成驗證程式。 此程式的範圍包括從驗證網域名稱控制到收集公司註冊檔案和訂閱者協定。 在實體的資訊獲得驗證後，CA會使用CA的私密金鑰簽署其公開金鑰。 因為所有主要的憑證授權單位在Web瀏覽器中都有根憑證，實體的憑證會透過&#x200B;*信任鏈*&#x200B;連結，而且網頁瀏覽器會將其識別為受信任的憑證。

>[!IMPORTANT]
>
>Cloud Manager 不提供 SSL 憑證或私密金鑰。這些必須從憑證授權單位（受信任的第三方組織）取得。 某些知名的憑證授權單位包括&#x200B;*DigiCert*、*Let&#39;s Encrypt*、*GlobalSign*、*Entrust*&#x200B;和&#x200B;*Verisign*。

Cloud Manager 支援以下客戶 SSL 憑證使用選項。

* 多個環境可以使用SSL憑證。 也就是說，可以新增一次，但使用多次。
* 每個 Cloud Manager 環境都可以使用多個憑證。
* 一個私密金鑰可以發行多個 SSL 憑證。
* 一個憑證通常包含多個網域。
* 平台 TLS 服務根據用於終止的 SSL 憑證和託管該網域的 CDN 服務將要求路由到客戶的 CDN 服務。
* AEM as a Cloud Service 接受網域的萬用字元 SSL 憑證。

AEM as a Cloud Service僅支援安全的`https`網站。 擁有多個自訂網域的客戶不希望每次新增網域時都上傳憑證。 這類客戶能因獲得具有多個網域的憑證而受益。

## SSL憑證需求 {#requirements}

* AEM as a Cloud Service接受符合OV （組織驗證）、EV （擴展驗證）或DV （網域驗證）原則的憑證。<!-- CQDOC-21758, #2 -->
* 任何憑證都必須是來自受信任憑證授權單位的X.509 TLS憑證，並具有相符的2048位元RSA私密金鑰。
* 不接受自我簽署憑證。

OV和EV憑證提供CA驗證的資訊。 這類資訊可協助使用者評估網站所有者、電子郵件寄件者或程式碼或PDF檔案的數位簽署者是否可信。 DV 憑證不允許此類所有權驗證。

### 客戶管理的SSL憑證格式 {#certificate-format}

<!-- CQDOC-21758, #3 -->

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

在任何指定時間，Cloud Manager允許最多安裝50個SSL憑證。 這些憑證可以與您的計畫中的一個或多個環境相關聯，並且還包括任何過期的憑證。

如果您已達到限制，請檢視您的憑證並考慮刪除任何過期的憑證。 或者，將多個網域群組在同一個憑證中，因為一個憑證可以涵蓋多個網域（最多100個SAN）。

## 了解更多 {#learn-more}

具有必要權限的使用者可以使用 Cloud Manager 來管理計畫的 SSL 憑證。如需有關使用這些功能的更多詳細資訊，請參閱以下文件。

* [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

