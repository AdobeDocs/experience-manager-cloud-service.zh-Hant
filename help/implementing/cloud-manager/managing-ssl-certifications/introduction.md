---
title: 管理SSL憑證簡介
description: 了解Cloud Manager如何提供自助工具來安裝SSL憑證。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: f69a26c6156c1f9038d612a00b16cac0e51e17ca
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# 管理SSL憑證簡介{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理SSL憑證"
>abstract="了解Cloud Manager如何提供自助工具，協助您安裝及管理SSL憑證，為使用者保護您的網站。 Cloud Manager使用平台TLS服務來管理客戶擁有且自第三方認證機構取得的SSL憑證和私密金鑰。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="檢視、更新和取代SSL憑證"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="檢查SSL憑證的狀態"

Cloud Manager提供自助服務工具，可安裝及管理SSL憑證，為使用者保護您的網站。 Cloud Manager使用平台TLS服務來管理客戶擁有且從第三方認證機構（例如Let&#39;s Encrypt）取得的SSL憑證和私密金鑰。

## 憑證簡介 {#certificates}

企業使用SSL憑證來保護其網站的安全，並讓客戶信任他們。 若要使用SSL通訊協定，Web伺服器需要使用SSL憑證。

當實體向證書頒發機構請求證書時，CA將完成驗證過程。 從驗證域名控制到收集公司註冊文檔和訂閱者協定，都可以。 一旦實體的資訊被驗證後，CA將使用CA的私鑰簽署其公鑰。 因為所有主要憑證授權單位在Web瀏覽器中都有根憑證，因此實體的憑證會透過 *信任鏈* 網頁瀏覽器會將其辨識為信任的憑證。

>[!IMPORTANT]
>
>Cloud Manager不提供SSL憑證或私密金鑰。 必須向認證機構(CA)取得。

## Cloud Manager SSL管理功能 {#features}

Cloud Manager支援下列客戶SSL憑證使用選項。

* SSL憑證可供多個環境使用。 即可新增一次，並多次使用。
* 每個Cloud Manager環境都可使用多個憑證。
* 私密金鑰可發行多個SSL憑證。
* 每個憑證通常包含多個網域。
* 平台TLS服務會根據用來終止的SSL憑證，以及托管該網域的CDN服務，將要求路由至客戶的CDN服務。
* AEMas a Cloud Service接受網域的萬用字元SSL憑證。

## 建議 {#recommendations}

AEMas a Cloud Service僅支援secure `https` 網站。

* 具有多個自訂網域的客戶不想在每次新增網域時上傳憑證。
* 此類客戶將受益於一個具有多個網域的憑證。

## 需求 {#requirements}

* AEMas a Cloud Service僅接受符合OV（組織驗證）或EV（延伸驗證）原則的憑證。
* 任何憑證都必須是來自信任認證機構(CA)的X.509 TLS憑證，且具有相符的2048位元RSA私密金鑰。
* 不接受DV（域驗證）策略。
* 不接受自簽名證書。

OV和EV證書為用戶提供了經過CA驗證的額外資訊，這些資訊可用於判斷網站的所有者、電子郵件的發送者，或可執行代碼或PDF檔案的數字簽名者是否值得信賴。 DV證書不允許進行此類所有權驗證。

## 限制 {#limitations}

Cloud Manager可在任何指定時間最多安裝50個SSL憑證。 這些環境可與您程式中的一或多個環境相關聯，也包含任何過期的憑證。

如果您已達到限制，請檢閱您的憑證，並考慮：

* 刪除任何過期的憑證。
* 將多個網域分組到相同憑證中，因為憑證可涵蓋多個網域（最多100個SAN）。

## 了解更多 {#learn-more}

擁有必要權限的使用者可以使用Cloud Manager管理方案的SSL憑證。 有關使用這些功能的詳細資訊，請參閱以下文檔。

* [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [檢視、更新或更換SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [刪除SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
