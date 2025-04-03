---
title: 基於 OpenAPI 的 API
description: 瞭解AEM as a Cloud Service對OpenAPI型API的支援
feature: Developing
role: Admin, Architect, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: e735f7d2a39e3165907969d2e27565639499a636
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# 基於 OpenAPI 的 API {#openapi-based-apis}

>[!NOTE]
>
>OpenAPI屬於搶先存取計畫的一部分。 如果您有興趣存取這些檔案，建議您傳送電子郵件至[aem-apis@adobe.com](mailto:aem-apis@adobe.com)，並提供使用案例的說明。

較新的AEM as a Cloud Service API遵循OpenAPI規格，因此可產生一致、妥善記錄且方便使用的API。 下列頁面提供深入資訊：

* [端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)，說明如何使用伺服器對伺服器驗證，設定及叫用OpenAPI型AEM API。
* 提供資訊的[指南](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/)，包括[API概念和語法](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/)。
* API端點[參考檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/)，其中部分API是以OpenAPI為基礎，例如[此Sites API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)。 參考檔案也包含API遊樂場，這可讓您使用隨Adobe Developer Console產生的持有人權杖輕鬆試用端點。

常見的API使用案例涉及與CRM或PIM等系統的整合，此情況下會叫用AEM API來擷取或保留資料。 作為整合實作的一部分，應用程式可能會訂閱[AEM發出的事件](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview)，這會觸發Adobe App Builder或其他基礎結構中的商業邏輯。

支援的API驗證型別因端點而異，但可能是OAuth伺服器對伺服器、OAuth網頁應用程式和OAuth單頁應用程式(SPA)。

>[!NOTE]
>
> [端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)是建議的資源，可讓您瞭解如何設定和叫用以OpenAPI為基礎的AEM API。


## 設定API存取 {#configuring-api-access}

許多OpenAPI型AEM API需要驗證，這需要使用[Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/)產生認證。 設定涉及以下步驟：

1. 請確定您的AEM程式的[產品設定檔已更新](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles)，並已啟用適當的服務來存取所需的API。
1. 在Adobe Developer Console中建立新專案，並將所需的API新增至專案，同時選取適當的驗證型別。
1. 產生認證，稍後在叫用API時用來交換持有人權杖。
1. 透過設定YAML檔案來向環境註冊使用者端ID，該檔案是使用設定管道（或RDE的命令列）部署的。

如需逐步指示，請參閱[設定OpenAPI型API教學課程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/setup)。

## 註冊使用者端ID {#registering-a-client-id}

使用者端ID會將Adobe Developer Console專案中的APis範圍調整至特定AEM環境。 可透過下列方式達成：

1. 使用如下列程式碼片段之類的設定，建立名為`api.yaml`或類似的檔案，包括所需的階層（作者、發佈、預覽）。 `Client_id`值應來自您的Adobe Developer Console API專案。

   `kind`、`version`和`metadata`屬性已在[設定管道](/help/operations/config-pipeline.md#common-syntax)文章中說明。 `kind`屬性值應該設定為&#x200B;*API*，而`version`屬性應該設定為&#x200B;*1*。

   ```
   kind: "API"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     allowedClientIDs:
       author:
         - "<client_id>"
       publish:
         - "<client_id>"
       preview:
         - "<client_id>"
   ```

1. 將檔案放置在名為`config`或類似名稱的頂層資料夾之下，如[設定管道](/help/operations/config-pipeline.md#folder-structure)所述。
1. 針對RDE （使用命令列工具）以外的環境型別，在Cloud Manager中建立目標部署設定管道，如設定管道文章中的[此區段](/help/operations/config-pipeline.md#creating-and-managing)所參考。 請注意，完整棧疊管道和網頁層管道不會部署設定檔案。
1. 部署設定。
