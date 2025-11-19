---
title: 基於 OpenAPI 的 API
description: 瞭解AEM as a Cloud Service對OpenAPI型API的支援
feature: Developing
role: Admin, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: 3a46db9c98fe634bf2d4cffd74b54771de748515
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 1%

---

# 基於 OpenAPI 的 API {#openapi-based-apis}

較新的AEM as a Cloud Service API遵循OpenAPI規格，因此提供了一組一致且妥善記錄的API。

>[!NOTE]
>
> [端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)是建議的資源，可讓您瞭解如何設定和叫用以OpenAPI為基礎的AEM API。

對於需要驗證的端點，驗證方法會因端點而異，但可能使用OAuth伺服器對伺服器、OAuth網頁應用程式或OAuth單頁應用程式(SPA)。 認證是透過[Adobe Developer Console](https://developer.adobe.com/developer-console/)中的專案設定的。

常見API使用案例涉及與CRM或PIM等系統的整合，此情況下會叫用AEM API來擷取或保留資料。 作為整合實作的一部分，應用程式可能會訂閱[AEM發出的事件](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview)，這會觸發Adobe App Builder或其他基礎結構中的商業邏輯。

本檔案僅供概覽，以下頁面提供更深入的檔案：

* 來自[參考檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/)之OpenAPI型API區段的連結。 每個API的參考檔案也包含API遊樂場，這使得使用Adobe Developer Console產生的持有人權杖來試用端點變得容易。

* 提供資訊的[指南](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/)，包括[API概念和語法](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/)。

* 說明[驗證方法](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/overview#authentication-support)和其他概念的最上層教學課程。

* 此教學課程包含影片，重點說明[如何設定OpenAPI型API](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup)。

* [端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)，說明如何使用伺服器對伺服器驗證策略設定和叫用OpenAPI。 您也可以找到網頁應用程式和單頁應用程式驗證方法的類似教學課程。

## 設定API存取 {#configuring-api-access}

有些OpenAPI型AEM API需要驗證，這需要使用[Adobe Developer Console](https://developer.adobe.com/developer-console/)產生認證。 設定涉及以下步驟：

1. AEM as a Cloud Service環境的現代化。 如需詳細資訊，請參閱[AEM as a Cloud Service環境的現代化](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup?#modernization-of-aem-as-a-cloud-service-environment)教學課程步驟。
1. 使用產品設定檔啟用對AEM API的存取權。 產品設定檔與代表具有預先定義存取控制清單(ACL)之AEM使用者群組的服務相關聯。 雖然某些服務依預設會與特定產品設定檔建立關聯，但其他服務則需要明確建立關聯；例如，AEM Assets API Users Service未與任何[產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles)建立關聯，因此您必須啟用它才能使用AEM Assets API。 如需詳細資訊，請參閱[啟用AEM API存取](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access)教學課程步驟。
1. 若要新增伺服器對伺服器驗證，使用者設定整合必須是組織在Adobe Admin Console中的系統管理員，或新增為開發人員至與服務相關聯的產品設定檔。 如需詳細資訊，請參閱[啟用AEM API存取](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access)教學課程步驟。
1. 建立Adobe Developer Console (ADC)專案。
1. 設定ADC專案。 這可產生認證，稍後在叫用API時，這些認證將用於交換持有人權杖。
1. 設定AEM執行個體以啟用ADC專案通訊。 這涉及透過設定和部署YAML檔案來向環境註冊使用者端ID，如下面的[註冊使用者端ID](#registering-a-client-id)一節所述。

如需詳細的逐步指示，請參閱[設定OpenAPI型API教學課程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup)。

### 註冊使用者端ID {#registering-a-client-id}

使用者端ID會將Adobe Developer Console專案中的API範圍調整至特定的AEM環境。 可透過下列方式達成：

1. 使用如下列程式碼片段之類的設定，建立名為`api.yaml`或類似的檔案，包括所需的階層（作者、發佈、預覽）。 `Client_id`值應來自您的Adobe Developer Console API專案。

   `kind`、`version`和`metadata`屬性已在[設定管道](/help/operations/config-pipeline.md#common-syntax)文章中說明。 `kind`屬性值應該設定為&#x200B;*API*，而`version`屬性應該設定為&#x200B;*1*。

   ```
   kind: "API"
   version: "1"
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
