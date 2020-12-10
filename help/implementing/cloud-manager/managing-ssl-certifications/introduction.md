---
title: 簡介——管理SSL憑證
description: 簡介——管理SSL憑證
translation-type: tm+mt
source-git-commit: 4ab944ad15390f9399138672a024aa30cf4aede8
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# 簡介 {#introduction}

Cloud Manager為客戶提供自助功能，可透過Cloud Manager UI安裝SSL憑證。 Cloud Manager使用Platform TLS服務來管理客戶擁有的SSL憑證和私密金鑰，通常是從第三方認證機構取得，例如&#x200B;*讓Encrypt*。

## 重要注意事項{#important-considerations}


* Cloud Manager不提供SSL憑證或私密金鑰。 您必須向第三方認證機構取得這些授權。 請參閱[取得SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)以瞭解詳細資訊。

* AEM作為雲端服務僅支援安全的`https`網站。 擁有多個自訂網域的客戶在每次新增網域時，都不想上傳憑證。 因此，此類客戶將受益於一個具有多個域的證書。

Cloud Manager支援下列客戶SSL憑證需求：

* SSL憑證可供多個環境使用，即新增一次，然後多次使用。
* 每個Cloud Manager環境都可以使用多個證書。
* 私密金鑰可能會發出多個SSL憑證。
* 每個憑證通常會包含多個網域。
* 平台TLS服務會根據用來終止的SSL憑證和代管該網域的CDN服務，將要求路由至客戶的CDN服務。

使用「Cloud Manager UI SSL憑證」頁面，擁有權限的使用者可以執行數項工作來管理程式的SSL憑證：

* [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [查看、更新或替換SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >這些動作可讓您檢視詳細資訊或取代即將到期的憑證。
* [刪除SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)