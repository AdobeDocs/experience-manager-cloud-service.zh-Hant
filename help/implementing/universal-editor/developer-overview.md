---
title: 適用於AEM開發人員的通用編輯器總覽
description: 如果您是AEM開發人員，且對Universal Editor的運作方式及如何在您的專案中使用它感興趣，本檔案將引導您檢測WKND專案以使用Universal Editor，為您提供端對端的簡介。
exl-id: d6f9ed78-f63f-445a-b354-f10ea37b0e9b
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '3139'
ht-degree: 1%

---


# 適用於AEM開發人員的通用編輯器總覽 {#developer-overview}

如果您是AEM開發人員，且對Universal Editor的運作方式及如何在您的專案中使用它感興趣，本檔案將引導您檢測WKND專案以使用Universal Editor，為您提供端對端的簡介。

## 用途 {#purpose}

本檔案將以開發人員的身分，介紹通用編輯器的運作方式，以及如何檢測您的應用程式如何搭配此編輯器運作。

其做法是透過大多數AEM開發人員熟悉的標準範例、核心元件和WKND網站，並裝備一些可使用通用編輯器編輯的範例元件。

>[!TIP]
>
>本檔案採取額外步驟說明通用編輯器的運作方式，旨在加深開發人員對編輯器的瞭解。 因此，它不會採取最直接的方式檢測應用程式，而是採用最能說明通用編輯器及其運作方式的方式。
>
>如果您想要儘快啟動並執行，請參閱AEM](/help/implementing/universal-editor/getting-started.md)中的[通用編輯器快速入門。

## 先決條件 {#prerequisites}

若要遵循本概述，您需要下列可用專案。

* [AEM as a Cloud Service的本機開發執行個體](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)
   * 您的本機開發執行個體必須在`localhost`.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html)上以HTTPS設定為開發目的[
   * [必須安裝WKND示範網站。](https://github.com/adobe/aem-guides-wknd)
* [存取通用編輯器](/help/implementing/universal-editor/getting-started.md#onboarding)
* [本機通用編輯器服務](/help/implementing/universal-editor/local-dev.md)正在執行以進行開發
   * 請確定將瀏覽器導向至[接受本機服務自我簽署憑證。](/help/implementing/universal-editor/local-dev.md#editing)

除了對Web開發的一般熟悉以外，本檔案假設您對AEM開發具有基本的熟悉。 如果您沒有使用AEM開發的經驗，請考慮先檢閱[WKND教學課程再繼續。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

## 啟動AEM並登入通用編輯器 {#sign-in}

如果您尚未安裝WKND，則必須安裝本機AEM開發執行個體，並啟用HTTPS作為[ （在先決條件中詳述）。](#prerequisites)此概觀假設您的執行個體在`https://localhost:8443`執行。

1. 在AEM編輯器中開啟WKND英文主版頁面。

   ```text
   https://localhost:8443/editor.html/content/wknd/language-masters/en.html
   ```

1. 在編輯器的&#x200B;**頁面資訊**&#x200B;功能表中，選取&#x200B;**以發佈的形式檢視**。 這會在停用AEM編輯器的新標籤中開啟相同頁面。

   ```text
   https://localhost:8443/content/wknd/language-masters/en.html?wcmmode=disabled
   ```

1. 複製此連結。

1. 現在請登入通用編輯器。

   ```text
   https://experience.adobe.com/#/aem/editor
   ```

1. 將您先前複製的WKND內容連結貼到Universal Editor的&#x200B;**網站URL**&#x200B;欄位，然後按一下&#x200B;**開啟**。

   ![在通用編輯器中開啟WKND頁面](assets/dev-ue-open.png)

## Universal Editor嘗試載入內容 {#sameorigin}

Universal Editor會載入要在框架中編輯的內容。 AEM的X-Frame選項預設設定可防止此情況，在瀏覽器中可清楚看到此錯誤，並在嘗試載入您的WKND本機副本時，在主控台輸出中詳細說明。

![由於SAMEORIGIN選項而發生瀏覽器錯誤](assets/dev-sameorigin.png)

X-Frame選項`sameorigin`可防止在框架中呈現AEM頁面。 您必須移除此標頭，才能讓頁面載入通用編輯器中。

1. 開啟Configuration Manager。

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. 編輯OSGi設定`org.apache.sling.engine.impl.SlingMainServlet`

   SAMEORIGIN的![OSGi屬性](assets/dev-sameorigin-osgi.png)

1. 刪除屬性&#x200B;**其他回應標題**&#x200B;的屬性`X-Frame-Options=SAMEORIGIN`。

1. 儲存變更。

現在，如果您重新載入通用編輯器，您會看到AEM頁面已載入。

>[!TIP]
>
>* 如需此OSGi設定的詳細資訊，請參閱檔案[AEM](/help/implementing/universal-editor/getting-started.md#sameorigin)中的Universal Editor快速入門。
>* 如需有關AEM中OSGi的詳細資訊，請參閱檔案[為Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md)設定OSGi。

## 處理相同網站Cookie {#samesite-cookies}

當通用編輯器載入您的頁面時，它會載入到AEM登入頁面，以確保您通過驗證可進行變更。

不過，您無法成功登入。 顯示瀏覽器主控台，您會看到瀏覽器已封鎖框架上的輸入

![輸入已封鎖](assets/dev-cross-origin.png)

登入權杖Cookie會作為協力廠商網域傳送給AEM。 因此，AEM中必須允許相同網站的Cookie。

1. 開啟Configuration Manager。

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. 編輯OSGi設定`com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`

   相同網站Cookie的![OSGi屬性](assets/dev-cross-origin-osgi.png)

1. 將登入權杖cookie **的屬性** SameSite屬性變更為`None`。

1. 儲存變更。

現在，如果您重新載入通用編輯器，您可以成功登入AEM並載入您的目標頁面。

>[!TIP]
>
>* 如需此OSGi設定的詳細資訊，請參閱檔案[AEM](/help/implementing/universal-editor/getting-started.md#samesite-cookies)中的Universal Editor快速入門。
>* 如需有關AEM中OSGi的詳細資訊，請參閱檔案[為Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md)設定OSGi。

## Universal Editor連線到遠端框架 {#ue-connect-remote-frame}

頁面載入通用編輯器並登入AEM後，通用編輯器會嘗試連線到遠端框架。 這是透過JavaScript程式庫完成，該程式庫必須載入遠端框架中。 如果JavaScript程式庫不存在，頁面最終會在主控台中建立逾時錯誤。

![逾時錯誤](assets/dev-timeout.png)

您必須將必要的JavaScript程式庫新增到WKND應用程式的頁面元件。

1. 開啟 CRXDE Lite。

   ```text
   https://localhost:8443/crx/de
   ```

1. 在`/apps/wknd/components/page`下，編輯檔案`customheaderlibs.html`。

   ![正在編輯customheaderlibs.html檔案](assets/dev-customheaderlibs.png)

1. 將JavaScript程式庫新增至檔案結尾。

   ```html
   <script src="https://universal-editor-service.experiencecloud.live/corslib/LATEST"></script>
   ```

1. 按一下&#x200B;**儲存全部**，然後重新載入通用編輯器。

頁面現在會使用適當的JavaScript程式庫載入，以允許Universal Editor連線至您的頁面，而逾時錯誤不再出現在主控台中。

>[!TIP]
>
>* 程式庫可載入頁首或頁尾。
>* `universal-editor-embedded.js`程式庫[可在NPM](https://www.npmjs.com/package/@adobe/universal-editor-cors)上使用，您可以視需要自行代管，或直接放入您的應用程式中。

## 定義連線以保留變更 {#connection}

WKND頁面現在會在Universal Editor中成功載入，且JavaScript程式庫會載入，以將編輯器連線至您的應用程式。

不過，您可能會注意到您無法與通用編輯器中的頁面互動。 通用編輯器無法實際編輯您的頁面。 為了讓Universal Editor能夠編輯您的內容，您需要定義連線，使其知道在哪裡寫入內容。 對於本機開發，您需要在`https://localhost:8443`回寫到您的本機AEM開發執行個體。

1. 開啟 CRXDE Lite。

   ```text
   https://localhost:8443/crx/de
   ```

1. 在`/apps/wknd/components/page`下，編輯檔案`customheaderlibs.html`。

   ![正在編輯customheaderlibs.html檔案](assets/dev-instrument-app.png)

1. 將連線至本機AEM執行個體的必要中繼資料新增至檔案結尾。

   ```html
   <meta name="urn:adobe:aue:system:aem" content="aem:https://localhost:8443">
   ```

   * 一律建議使用最新版本的程式庫。 如果您需要舊版，請參閱檔案[AEM中的通用編輯器快速入門。](/help/implementing/universal-editor/getting-started.md#alternative)

1. 將連線至本機Universal Editor服務的必要中繼資料新增至檔案結尾。

   ```html
   <meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
   ```

1. 按一下&#x200B;**儲存全部**，然後重新載入通用編輯器。

現在，Universal Editor不僅可以從您本機的AEM開發執行個體成功載入您的內容，而且會知道要將您使用本機的Universal Editor服務所做的任何變更儲存在何處。 這是測試應用程式以使用通用編輯器可編輯的第一步。

>[!TIP]
>
>* 如需有關連線中繼資料的詳細資訊，請參閱檔案[AEM中的通用編輯器快速入門](/help/implementing/universal-editor/getting-started.md#connection)。
>* 如需有關通用編輯器結構的詳細資訊，請參閱檔案[通用編輯器架構](/help/implementing/universal-editor/architecture.md#service)。
>* 如需有關如何連線到自行裝載的通用編輯器版本的詳細資訊，請參閱檔案[使用通用編輯器進行本機AEM開發](/help/implementing/universal-editor/local-dev.md)。

## 檢測元件 {#instrumenting-components}

不過，您可能會注意到您仍然可以對Universal Editor執行一些工作。 如果您嘗試按一下通用編輯器中WKND頁面頂端的Teaser，您實際上無法選取它（或頁面上的其他內容）。

您的元件也必須檢測為可使用通用編輯器進行編輯。 若要這麼做，您必須編輯Teaser元件。 因此，您需要覆蓋核心元件，因為核心元件位於`/libs`下方，而此為不可變專案。

1. 開啟 CRXDE Lite。

   ```text
   https://localhost:8443/crx/de
   ```

1. 選取節點`/libs/core/wcm/components`並按一下工具列上的&#x200B;**覆蓋節點**。

1. 選取`/apps/`做為&#x200B;**覆蓋位置**，按一下&#x200B;**確定**。

   ![覆蓋Teaser](assets/dev-overlay-teaser.png)

1. 選取`/libs/core/wcm/components`下的`teaser`節點，然後按一下工具列中的&#x200B;**複製**。

1. 選取位於`/apps/core/wcm/components`的重疊節點，然後按一下工具列中的&#x200B;**貼上**。

1. 連按兩下檔案`/apps/core/wcm/components/teaser/v2/teaser/teaser.html`以進行編輯。

   ![正在編輯Teaser.html檔案](assets/dev-edit-teaser.png)

1. 在第一個`div`的末尾（大約在第26行），新增元件的檢測詳細資料。

   ```text
   data-aue-resource="urn:aem:${resource.path}"
   data-aue-type="component"
   data-aue-label="Teaser"
   ```

1. 按一下工具列中的「儲存全部&#x200B;**」**，然後重新載入通用編輯器。

1. 在通用編輯器中，按一下頁面頂端的Teaser元件，檢視您現在可以選取它。

1. 如果您按一下通用編輯器屬性邊欄中的&#x200B;**內容樹狀結構**&#x200B;圖示，您會發現編輯器已辨識出頁面上所有的Teaser（您已偵測到它）。 您選取的Teaser是反白顯示的。

   ![選取檢測的Teaser元件](assets/dev-select-teaser.png)

>[!TIP]
>
>如需重疊節點的詳細資訊，請參閱檔案[在Adobe Experience Manager as a Cloud Service中使用Sling Resource Merger ](/help/implementing/developing/introduction/sling-resource-merger.md)。

## Teaser的儀器子元件 {#subcomponents}

您現在可以選取Teaser，但仍不可編輯。 這是因為Teaser是不同元件（例如影像和標題元件）的組合。 您必須檢測這些子元件才能進行編輯。

1. 開啟 CRXDE Lite。

   ```text
   https://localhost:8443/crx/de
   ```

1. 選取節點`/apps/core/wcm/components/teaser/v2/teaser/`並連按兩下`title.html`檔案。

   ![編輯title.html檔案](assets/dev-edit-title.png)

1. 在`h2`標籤的結尾處插入下列屬性（在第17行附近）。

   ```text
   data-aue-prop="jcr:title"
   data-aue-type="text"
   data-aue-label="Title"
   ```

1. 按一下工具列中的「儲存全部&#x200B;**」**，然後重新載入通用編輯器。

1. 按一下頁面頂端相同Teaser元件的標題，檢視您現在可以選取它。 內容樹狀結構也會將標題顯示為所選Teaser元件的一部分。

   ![在Teaser中選取標題](assets/dev-select-title.png)

您現在可以編輯Teaser元件的標題！

## 這是什麼意思？ {#what-does-it-mean}

現在您可以編輯Teaser的標題，讓我們花點時間檢閱您已完成的作業及操作方式。

您已透過檢測來向通用編輯器識別Teaser元件。

* `data-aue-resource`會識別AEM中正在編輯的資源。
* `data-aue-type`定義應將專案視為頁面元件（而不是容器）。
* `data-aue-label`會在所選Teaser的UI中顯示使用者易記標籤。

您也已在Teaser元件中檢測標題元件。

* `data-aue-prop`是寫入的JCR屬性。
* `data-aue-type`是應該如何編輯屬性。 在這種情況下，請使用文字編輯器，因為它是標題（相對於RTF編輯器）。

## 定義驗證標頭 {#auth-header}

現在您可以編輯Teaser內嵌的標題，且變更會保留在瀏覽器中。

![已編輯的Teaser標題](assets/dev-edited-title.png)

但是，如果您重新載入瀏覽器，則會重新載入前一個標題。 這是因為，雖然通用編輯器知道如何連線到您的AEM執行個體，但它無法驗證您的AEM執行個體以回寫對JCR的變更。

如果您顯示瀏覽器開發人員工具的網路索引標籤並搜尋`update`，您會發現嘗試編輯標題時發生401錯誤。

![嘗試編輯標題時發生錯誤](assets/dev-edit-error.png)

使用通用編輯器編輯您的生產AEM內容時，通用編輯器使用您用來登入編輯器的IMS權杖來驗證AEM，以方便回寫至JCR。

當您在本機開發時，無法使用AEM身分提供者，因為IMS權杖只會傳遞給Adobe擁有的網域。 您需要透過明確設定驗證標題來手動提供驗證方法。

1. 在Universal Editor介面中，按一下工具列中的&#x200B;**Authentication Headers**&#x200B;圖示。

1. 複製必要的驗證標頭以驗證您的本機AEM執行個體，然後按一下[儲存]。****

   ![正在設定驗證標頭](assets/dev-authentication-headers.png)

1. 重新載入通用編輯器，現在編輯Teaser的標題。

瀏覽器主控台中不再報告任何錯誤，且變更會保留回您的本機AEM開發執行個體。

如果您在瀏覽器開發人員工具中調查流量並尋找`update`事件，您可以檢視更新的詳細資料。

![已成功編輯Teaser標題](assets/dev-edit-title-successfully.png)

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "text",
    "prop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

* `connections`是您本機AEM執行個體的連線
* `target`是在JCR中更新的確切節點和屬性
* `value`是您所做的更新。

您可以在JCR中看到持續存在的變更。

在JCR](assets/dev-write-back-jcr.png)中更新![

>[!TIP]
>
>有許多線上工具可產生必要的驗證標頭，以用於您的測試和開發用途。
>
>基本驗證標頭範例`Basic YWRtaW46YWRtaW4=`適用於本機AEM開發中常見的`admin:admin`使用者/密碼組合。

## 為屬性邊欄檢測應用程式 {#properties-rail}

現在，您有一個應用程式，經檢測可以使用通用編輯器進行編輯！

編輯目前僅限於Teaser標題的內嵌編輯。 但是，在某些情況下，就地編輯並不足夠。 在鍵盤輸入所在的位置可以編輯Teaser標題等文字。 不過，更複雜的專案必須能夠顯示並允許編輯結構化資料，而不需將其呈現在瀏覽器中。 這是屬性邊欄的用途。

若要更新應用程式以使用屬性邊欄進行編輯，請返回應用程式頁面元件的標題檔案。 這是您已建立與本機AEM開發執行個體和本機Universal Editor服務之連線的位置。 您必須在此處定義可在應用程式中編輯的元件及其資料模型。

1. 開啟 CRXDE Lite。

   ```text
   https://localhost:8443/crx/de
   ```

1. 在`/apps/wknd/components/page`下，編輯檔案`customheaderlibs.html`。

   ![正在編輯customheaderlibs.html檔案](assets/dev-instrument-properties-rail.png)

1. 在檔案的結尾處新增定義元件所需的指令碼。

   ```html
   <script type="application/vnd.adobe.aue.component+json">
   {
     "groups": [
       {
         "title": "General Components",
         "id": "general",
         "components": [
           {
             "title": "Teaser",
             "id": "teaser",
             "plugins": {
               "aem": {
                 "page": {
                   "resourceType": "wknd/components/teaser"
                 }
               }
             }
           },
           {
             "title": "Title",
             "id": "title",
             "plugins": {
               "aem": {
                 "page": {
                   "resourceType": "wknd/components/title"
                 }
               }
             }
           }
         ]
       }
     ]
   }
   </script>
   ```

1. 在其下方，在檔案的結尾處新增定義模型所需的指令碼。

   ```html
   <script type="application/vnd.adobe.aue.model+json">
   [
     {
       "id": "teaser",
       "fields": [
         {
           "component": "text-input",
           "name": "jcr:title",
           "label": "Title",
           "valueType": "string"
         },
         {
           "component": "text-area",
           "name": "jcr:description",
           "label": "Description",
           "valueType": "string"
         }
       ]
     },
     {
       "id": "title",
       "fields": [
         {
           "component": "select",
           "name": "type",
           "value": "h1",
           "label": "Type",
           "valueType": "string",
           "options": [
             { "name": "h1", "value": "h1" },
             { "name": "h2", "value": "h2" },
             { "name": "h3", "value": "h3" },
             { "name": "h4", "value": "h4" },
             { "name": "h5", "value": "h5" },
             { "name": "h6", "value": "h6" }
           ]
         }
       ]
     }
   ]
   </script>
   ```

1. 按一下工具列中的「儲存全部&#x200B;****」。

## 這是什麼意思？ {#what-does-it-mean-2}

若要使用屬性邊欄進行編輯，必須將元件指派給`groups`，因此每個定義都會以包含元件的群組清單開始。

* `title`是群組的名稱。
* `id`是群組的唯一識別碼，在此案例中是組成頁面內容的一般元件，而不是頁面配置的進階元件。

然後每個群組都有一個`components`陣列。

* `title`是元件的名稱。
* `id`是元件的唯一識別碼，在此案例中是Teaser。

然後，每個元件都有外掛程式定義，可定義如何將元件對應至AEM。

* `aem`是處理編輯的外掛程式。 這可以視為處理元件的服務。
* `page`會定義其為哪種元件，在此案例中為標準頁面元件。
* `resourceType`是實際AEM元件的對應。

然後，每個元件都必須對應至`model`，以定義個別可編輯欄位。

* `id`是模型的唯一識別碼，必須符合元件的ID。
* `fields`是個別欄位的陣列。
* `component`是輸入型別，例如文字或文字區域。
* `name`是該欄位對應到的JCR中的欄位名稱。
* `label`是出現在編輯器UI中的欄位說明。
* `valueType`是資料型別。

## 為屬性邊欄檢測元件 {#properties-rail-component}

您還需要在元件層級定義元件應使用的模型。

1. 開啟 CRXDE Lite。

   ```text
   https://localhost:8443/crx/de
   ```

1. 連按兩下檔案`/apps/core/wcm/components/teaser/v2/teaser/teaser.html`以進行編輯。

   ![正在編輯Teaser.html檔案](assets/dev-edit-teaser.png)

1. 在第一個`div`的末尾（大約在第32行），在您先前新增的屬性之後，新增Teaser元件將使用的模型的檢測詳細資料。

   ```text
   data-aue-model="teaser"
   ```

1. 按一下工具列中的「儲存全部&#x200B;**」**，然後重新載入通用編輯器。

現在您已準備好測試針對元件所檢測的屬性邊欄。

1. 在通用編輯器中，按一下Teaser的標題以再次編輯。

1. 按一下屬性邊欄以顯示屬性標籤，並檢視您剛才檢測的欄位。

   ![檢測的屬性邊欄](assets/dev-properties-rail-instrumented.png)

您現在可以像之前一樣內嵌編輯Teaser標題，或在屬性邊欄中編輯。 在這兩種情況下，變更會保留回本機AEM開發執行個體。

## 新增其他欄位至屬性邊欄 {#add-fields}

使用已實作之元件的資料模型基本結構，可以依照相同模型新增其他欄位。

例如，您可以新增欄位來調整元件的樣式。

1. 開啟 CRXDE Lite。

   ```text
   https://localhost:8443/crx/de
   ```

1. 在`/apps/wknd/components/page`下，編輯檔案`customheaderlibs.html`。

   ![正在編輯customheaderlibs.html檔案](assets/dev-instrument-styles.png)

1. 在模型定義指令碼中，為樣式欄位新增其他專案至`fields`陣列。 插入新欄位之前，請記得在最後一個欄位後面加上逗號。

   ```json
   {
      "component": "select",
      "name": "cq:styleIds",
      "label": "Style",
      "valueType": "string",
        "multi": true,
      "options": [
        {"name": "hero", "value":"1555543212672"},
        {"name": "card", "value":"1605057868937"}
      ]
   }
   ```

1. 按一下工具列中的「儲存全部&#x200B;**」**，然後重新載入通用編輯器。

1. 按一下Teaser的標題可再次編輯。

1. 按一下「屬性」邊欄，檢視是否有新欄位可調整元件的樣式。

   ![具樣式欄位](assets/dev-style-instrumented.png)的檢測屬性邊欄

可透過此方式在Universal Editor中公開元件JCR中的任何欄位。

## 摘要 {#summary}

恭喜！現在您可以檢測自己的AEM應用程式，以便使用通用編輯器。

當您開始檢測自己的應用程式時，請牢記您在本範例中執行的基本步驟。

1. [您可以設定開發環境。](#prerequisites)
   * 在已安裝WKND的HTTPS上本機執行的AEM
   * 在HTTPS上本機執行的Universal Editor服務
1. 您已更新AEM OSGi設定，允許從遠端載入其內容。
   * [&#39;org.apache.sling.engine.impl.SlingMainServlet&#39;](#sameorigin)
   * [&#39;com.day.crx.security.token.impl.impl.TokenAuthenticationHandler&#39;](#samesite-cookies)
1. [您已新增 ](#ue-connect-remote-frame)
1. [您定義了一個連線，以將變更保留在 ](#connection)
   * 您已定義與本機AEM開發執行個體的連線。
   * 您也定義了與本機Universal Editor服務的連線。
1. [您已檢測Teaser元件。](#instrumenting-components)
1. [您檢測了Teaser的子元件。](#subcomponents)
1. [您定義了自訂驗證標頭，以便使用本機Universal Editor服務儲存變更。](#auth-header)
1. [您指示應用程式使用屬性邊欄。](#properties-rail)
1. [您檢測Teaser元件以使用屬性邊欄。](#properties-rail-component)

您可以依照這些相同步驟來檢測您自己的應用程式，以便與通用編輯器搭配使用。 JCR中的任何屬性都可以向通用編輯器公開。

## 其他資源 {#additional-resources}

請參閱下列檔案，瞭解通用編輯器功能的詳細資訊和詳細資訊。

* 如果您想要儘快啟動並執行，請參閱AEM](/help/implementing/universal-editor/getting-started.md)中的[通用編輯器快速入門。
* 如需有關必要OSGi設定的詳細資訊，請參閱檔案[AEM中的Universal Editor快速入門](/help/implementing/universal-editor/getting-started.md#sameorigin)。
* 如需有關連線中繼資料的詳細資訊，請參閱檔案[AEM中的通用編輯器快速入門](/help/implementing/universal-editor/getting-started.md#connection)。
* 如需有關通用編輯器結構的詳細資訊，請參閱檔案[通用編輯器架構](/help/implementing/universal-editor/architecture.md#service)。
* 如需有關如何連線到自行裝載的通用編輯器版本的詳細資訊，請參閱檔案[使用通用編輯器進行本機AEM開發](/help/implementing/universal-editor/local-dev.md)。
* 如需重疊節點的詳細資訊，請參閱檔案[在Adobe Experience Manager as a Cloud Service中使用Sling Resource Merger ](/help/implementing/developing/introduction/sling-resource-merger.md)。

