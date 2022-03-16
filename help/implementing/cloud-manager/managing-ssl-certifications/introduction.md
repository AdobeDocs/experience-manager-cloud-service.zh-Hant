---
title: 簡介 — 管理SSL證書
description: 簡介 — 管理SSL證書
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: 09a2c24b848364954dc5621995d0d0dc24059011
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理SSL證書"
>abstract="Cloud Manager為客戶提供通過Cloud Manager UI安裝SSL證書的自助服務功能。 Cloud Manager使用平台TLS服務來管理客戶擁有的SSL證書和私鑰，通常從第三方認證機構獲得。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/view-update-replace-ssl-certificate.html" text="查看、更新和替換SSL證書"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/check-status-ssl-certificate.html" text="檢查SSL證書的狀態"


Cloud Manager為客戶提供通過Cloud Manager UI安裝SSL證書的自助服務功能。 Cloud Manager使用平台TLS服務管理客戶擁有的SSL證書和私鑰，通常從第三方認證機構獲得，例如， *讓我們加密*。

## 重要注意事項 {#important-considerations}

* 雲管理器不提供SSL證書或私鑰。 必須從第三方認證機構獲得。 請參閱 [獲取SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) 來瞭解更多資訊。

* 僅AEMas a Cloud Service `https` 站點。 具有多個自定義域的客戶在每次添加域時都不希望上載證書。 因此，此類客戶將受益於一個具有多個域的證書。

* AEMas a Cloud Service只接受符合OV（組織驗證）或EV（擴展驗證）策略的證書。 將不接受DV（域驗證）策略。 此外，任何證書都必須是來自受信任證書頒發機構(CA)的X.509 TLS證書，其中具有匹配的2048位RSA私鑰。

* AEMas a Cloud Service將接受域的通配符SSL證書。

* 在任何給定時間，Cloud Manager將允許最多50個SSL證書，這些證書可以與您程式中的一個或多個環境關聯，即使證書已過期。 但是，Cloud Manager UI將允許在此約束下在程式中安裝最多50個SSL證書。 通常，證書可以覆蓋多個域（最多100個SAN），因此請考慮將同一證書中的多個域分組以保持在此限制下。

Cloud Manager支援以下客戶SSL證書要求：

* SSL證書可供多個環境使用，即添加一次並使用多次。
* 每個Cloud Manager環境都可以使用多個證書。
* 私鑰可以頒發多個SSL證書。
* 每個證書通常包含多個域。
* 平台TLS服務根據用於終止的SSL證書和承載該域的CDN服務將請求路由到客戶的CDN服務。

使用「雲管理器UI SSL Certificates」頁，具有權限的用戶可以執行以下幾項任務來管理程式的SSL證書：

* [添加SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [查看、更新或替換SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >這些操作允許您查看詳細資訊或替換即將過期的證書。
* [刪除SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
