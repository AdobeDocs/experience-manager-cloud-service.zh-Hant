---
title: 簡介 — 管理SSL憑證
description: 簡介 — 管理SSL憑證
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: d457d76d56a729a2e6eb729ad91a6e7877fd6a0c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理SSL憑證"
>abstract="Cloud Manager可讓客戶透過Cloud Manager UI自行安裝SSL憑證。 Cloud Manager使用Platform TLS服務來管理客戶擁有且通常從第三方認證機構取得的SSL憑證和私密金鑰。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/view-update-replace-ssl-certificate.html" text="檢視、更新和取代SSL憑證"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/check-status-ssl-certificate.html" text="檢查SSL憑證的狀態"


Cloud Manager可讓客戶透過Cloud Manager UI自行安裝SSL憑證。 Cloud Manager使用Platform TLS服務來管理客戶擁有的SSL憑證和私密金鑰，且通常從協力廠商認證機構取得，例如&#x200B;*我們加密*。

## 重要考量 {#important-considerations}

* Cloud Manager不提供SSL憑證或私密金鑰。 這些認證必須從第三方認證機構獲得。 請參閱[取得SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)以深入了解。

* AEM as aCloud Service僅支援安全的`https`網站。 具有多個自訂網域的客戶不想在每次新增網域時上傳憑證。 因此，此類客戶將受益於一個具有多個網域的憑證。

* AEM as aCloud Service只會接受OV（組織驗證）或EV（延伸驗證）憑證。 不接受DV（域驗證）證書。 此外，任何證書都必須是來自受信任認證機構(CA)的X.509 TLS證書，且具有相符的2048位RSA私鑰。

* AEM as aCloud Service會接受網域的萬用字元SSL憑證。

* 在任何指定時間，Cloud Manager最多可允許20個SSL憑證，此憑證可與您方案中的一或多個環境建立關聯，即使憑證已過期亦然。 不過，在具有此限制的程式中，Cloud Manager UI將允許安裝最多50個SSL憑證。 通常，證書可以覆蓋多個域（最多100個SAN），因此，請考慮將同一證書中的多個域分組以保持在此限制下。

Cloud Manager支援下列客戶SSL憑證需求：

* SSL憑證可供多個環境使用，即只需新增一次，便可多次使用。
* 每個Cloud Manager環境都可使用多個憑證。
* 私密金鑰可發行多個SSL憑證。
* 每個憑證通常會包含多個網域。
* Platform TLS服務會根據用來終止的SSL憑證，以及托管該網域的CDN服務，將要求路由至客戶的CDN服務。

擁有權限的使用者可使用Cloud Manager UI SSL Certificates頁面，執行數項工作以管理方案的SSL憑證：

* [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [檢視、更新或更換SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >這些動作可讓您檢視詳細資訊或取代即將過期的憑證。
* [刪除SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
