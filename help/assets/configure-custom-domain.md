---
title: 設定Publish層的自訂網域
description: 瞭解如何在AdobeCloud Manager中為發佈層設定自訂網域。
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 11%

---

# 設定發佈層的自訂網域{#configure-custom-domain}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Dynamic Media搭配OpenAPI功能指南現在提供PDF格式。 下載整份指南，並使用Adobe Acrobat AI Assistant回答您的疑問。
>
>[!BADGE 具有OpenAPI功能的Dynamic Media指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

在AdobeCloud Manager中，您可以新增自訂網域，讓您的網站脫穎而出。 雖然AEM as a Cloud Service隨附預設網域，但您可以視需求加以自訂。

## 開始之前

* 您必須擁有多個SAN （主體替代名稱） TLS或SSL憑證。
* SSL憑證應該有針對相同網域內發佈層對應之憑證的不同SAN。
* 憑證原則必須符合擴展驗證(EV)或組織驗證(OV)，而不是網域驗證(DV)原則。


## 設定發佈層的自訂網域

1. 移至&#x200B;**[!UICONTROL AdobeCloud Manager]** > **[!UICONTROL 計畫總覽]** > **[!UICONTROL SSL憑證]**，然後新增您的SSL憑證。
   ![影像](/help/assets/assets/ssl-certificate.png)
瞭解如何在AdobeCloud Manager中新增[SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

1. 新增SSL憑證後，請新增自訂網域。 按一下「**[!UICONTROL 網域設定]**」，並針對「**[!UICONTROL Publish服務]**」選項指定自訂網域。
深入瞭解[自訂網域](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

1. 在對應發佈網域的DNS記錄中新增兩個[CNAME記錄](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
由於 DNS 傳播延遲，DNS 驗證可能需要幾個小時才能完成。

1. 記錄支援案例以協助設定自訂網域，確保將其導向傳送階層。

>[!NOTE]
>
新增自訂網域至允許的重新導向URL清單。 此清單位於資產選擇器的IMS使用者端中。<br>提供自訂網域字串，與個別Adobe團隊協調以執行此工作。
