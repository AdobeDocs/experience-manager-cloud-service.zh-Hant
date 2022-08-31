---
title: 將體驗片段導出到Adobe Target
description: 將體驗片段導出到Adobe Target
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '2259'
ht-degree: 0%

---

# 將體驗片段導出到Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* 「AEM體驗片段」(Experience Fragments)將導出到Adobe Target的預設工作區。
>* 必AEM須按照Adobe Target [與Adobe Target整合](/help/sites-cloud/integrating/integrating-adobe-target.md)。


可以導出 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)，建立於Adobe Experience Manager as a Cloud Service(AEM)，建立至Adobe Target（目標）。 然後，它們可以用作目標活動中的優惠，以test和個性化規模體驗。

有三個選項可用於將體驗片段導出到Adobe Target:

* HTML（預設）:支援Web和混合內容交付
* JSON:支援無頭內容交付
* HTML 和 JSON

要準備將體驗片段AEM導出到Adobe Target的實例，您需要：

* [與Adobe Target整合](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [添加雲配置](#add-the-cloud-configuration)
* [添加舊配置](#add-the-legacy-configuration)

之後，您可以：

* [將經驗片段導出到Adobe Target](#exporting-an-experience-fragment-to-adobe-target)
* [使用您在Adobe Target的體驗片段](#using-your-experience-fragments-in-adobe-target)
* 還有 [刪除已導出到Adobe Target的體驗片段](#deleting-an-experience-fragment-already-exported-to-adobe-target)

「體驗片段」可導出到Adobe Target的預設工作區，或導出到Adobe Target的用戶定義的工作區。

>[!NOTE]
>
>Adobe Target工作區在Adobe Target本身不存在。 它們在Adobe IMS(Identity Management系統)中定義和管理，然後選擇在使用Adobe Developer控制台的解決方案中使用。

>[!NOTE]
>
>Adobe Target工作區可用於僅允許組織（組）的成員建立和管理此組織的聘用和活動；不允許其他用戶訪問。 例如，全球關注的具體國家組織。

>[!NOTE]
>
>有關詳細資訊，請參閱：
>
>* [Adobe Target開發](https://developers.adobetarget.com/)
>* [核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
>* [Adobe Target — 如何使用Adobe Experience Manager(AEM)體驗碎片？](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)
>* [6AEM.5 — 手動配置與Adobe Target的整合 — 建立目標雲配置](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-configuring.html#creating-a-target-cloud-configuration)


## 必備條件 {#prerequisites}

需要執行以下各種操作：

1. 你必須 [與AEMAdobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)。

1. 從作者實例導出AEM「體驗片段」，因此您需要 [配置鏈AEM接外部化程式](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) 在作者實例上，以確保將體驗片段中的任何引用外部化以用於Web傳遞。

   >[!NOTE]
   >
   >對於預設不覆蓋的連結重寫， [體驗片段連結重寫器提供程式](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) 的子菜單。 利用此功能，可以為實例開發自定義規則。

## 添加雲配置 {#add-the-cloud-configuration}

導出片段之前，需要添加 **雲配置** 為 **Adobe Target** 資料夾。 這還允許您：

* 指定要用於導出的格式選項
* 選擇目標工作區作為目標
* 選擇外部化程式域以重寫「體驗片段」中的引用（可選）

可在中選擇所需選項 **頁面屬性** 資料夾和/或片段；將根據需要繼承規範。

1. 導航到 **體驗片段** 控制台。

1. 開啟 **頁面屬性** 資料夾或檔案段。

   >[!NOTE]
   >
   >如果將雲配置添加到「體驗片段」父資料夾，則所有子資料夾都繼承該配置。
   >
   >如果將雲配置添加到體驗片段本身，則所有變數都會繼承該配置。

1. 選擇 **Cloud Services** 頁籤。

1. 下 **Cloud Service配置**&#x200B;選中 **Adobe Target** 從下拉清單中。

   >[!NOTE]
   >
   >可以自定義體驗片段提供的JSON格式。 要執行此操作，請定義客戶體驗片段元件，然後注釋如何在元件Sling模型中導出其屬性。
   >
   >請參閱核心元件： [核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

1. 下 **Adobe Target** 選擇：

   * 適當的配置
   * 所需格式選項
   * Adobe Target工作區
   * 如果需要 — 外部化程式域

   >[!CAUTION]
   >
   >外部化器域是可選的。
   >
   > 當希AEM望導出的內容指向特定內容時，將配置外部化器 *發佈* 。 有關詳細資訊，請參閱 [配置鏈AEM接外部化器](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer)。
   >
   > 另請注意，外部化程式域僅與發送到目標的體驗片段的內容相關，而不與元資料（如查看服務內容）相關。

   例如，對於資料夾：

   ![資料夾 — Cloud Services](assets/xf-target-integration-01.png "資料夾 — Cloud Services")

1. **儲存並關閉**.

## 添加舊配置 {#add-the-legacy-configuration}

<!-- This is effectively the Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target} section from 6.5 -->

>[!IMPORTANT]
>
>添加新的舊配置是僅支援導出經驗片段的特殊情況方案。

之後 [添加雲配置](#add-the-cloud-configuration) 要使用Launch by Adobe,AEM要最初與Adobe Target整合，您還需要使用舊式配置手動與Adobe Target整合。

### 建立目標雲配置 {#creating-a-target-cloud-configuration}

若要AEM與Adobe Target交互，請建立目標雲配置。 要建立配置，請提供Adobe Target客戶端代碼和用戶憑據。

您僅建立一次目標雲配置，因為您可以將配置與多個市場活動AEM關聯。 如果您有多個Adobe Target客戶端代碼，請為每個客戶端代碼建立一個配置。

您可以配置雲配置以同步來自Adobe Target的段。 如果啟用同步，則在保存雲配置後，會立即從後台的Target導入段。

請按下列步驟在中建立目標雲配AEM置：

1. 導航到 **舊Cloud Services** 通過 **AEM徽標** > **工具** > **Cloud Services** > **舊Cloud Services**。
例如：([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   的 **Adobe Experience Cloud** 的子菜單。

1. 在 **Adobe Target** ，按一下 **立即配置**。
1. 在 **建立配置** 對話框：

   1. 給配置 **標題**。
   1. 選擇 **Adobe Target配置** 的下界。
   1. 按一下&#x200B;**建立**。

現在可以選擇新配置進行編輯。

1. 編輯對話框開啟。

   ![配置 — 目標 — 設定 — 對話框](assets/config-target-settings-dialog.png)

   <!-- Can this still occur?

   >[!NOTE]
   >
   >When configuring A4T with AEM, you may see a Configuration reference missing entry. To be able to select the analytics framework, do the following:
   >
   >1. Navigate to **Tools** &gt; **General** &gt; **CRXDE Lite**.
   >1. Navigate to **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   >1. Set the property **disable** to **false**.
   >1. Tap or click **Save All**.

   -->

1. 在 **Adobe Target設定** 對話框，提供這些屬性的值。

   * **驗證**:這預設為IMS（不建議使用用戶憑據）

   * **客戶端代碼**:目標帳戶客戶端代碼

   * **租戶ID**:租戶ID

   * **IMS配置**:從下拉清單中選擇所需的配置

   * **API類型**:預設為REST（不建議使用XML）

   * **A4TAnalytics Cloud配置**:選擇用於目標活動目標和度量的分析雲配置。 如果在針對內容時使用Adobe Analytics作為報告源，則需要此選項。

      <!-- Is this needed?
     If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).
     -->

   * **使用準確的目標：** 預設情況下，此複選框處於選中狀態。 如果選中，則雲服務配置將在載入內容之前等待上下文載入。 請參閱下面的注釋。

   * **同步來自Adobe Target的段：** 選擇此選項可下載在目標中定義的段以在中使AEM用。 當API Type屬性為REST時，必須選擇此選項，因為不支援內聯段，並且您始終需要使用「目標」中的段。 (請注意，AEM「段」的術語等同於目標「受眾」。)

   * **客戶端庫：** 此預設值為AT.js（不建議使用mbox.js）

      >[!NOTE]
      >
      >目標庫檔案， [AT.JS](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html)，是為Adobe Target設計的一個新的實現庫，它既適用於典型的web實施，也適用於單頁應用程式。
      >
      >mbox.js已棄用，將在稍後階段刪除。
      >
      >Adobe建議將AT.js而不是mbox.js用作客戶端庫。
      >
      >AT.js對mbox.js庫提供了幾項改進：
      >
      >* 用於Web實現的改進的頁載入時間
      >* 提高安全性
      >* 針對單頁應用程式的更好實施選項
      >* AT.js包含target.js中包含的元件，因此不再調用target.js

      >
      >可以在 **客戶端庫** 的下界。

   * **使用Tag Management系統提供客戶端庫**  — 選擇此選項可使用Adobe啟動或其他標籤管理系統（或不建議使用的DTM）中的客戶端庫。

   * **自定義AT.js**:瀏覽以上載自定義AT.js。 留空以使用預設庫。

      >[!NOTE]
      >
      >預設情況下，當您選擇加入Adobe Target配置嚮導時，將啟用「準確定位」。
      >
      >準確定位意味著雲服務配置在載入內容之前等待上下文載入。 因此，從效能上看，準確的目標可能會在載入內容之前產生幾毫秒的延遲。
      >
      >始終在作者實例上啟用精確目標。 但是，在發佈實例上，您可以選擇在雲服務配置中清除「準確瞄準」旁邊的複選標籤，從而全局關閉準確瞄準(**http://localhost:4502/etc/cloudservices.html**)。 無論您在雲服務配置中的設定如何，您仍然可以針對各個元件開啟和關閉精確的目標。
      >
      >如果 ***已*** 建立了目標元件，並且您更改了此設定，您所做的更改不會影響這些元件。 必須直接對這些元件進行任何更改。

1. 按一下 **連接到Adobe Target** 初始化與目標的連接。 如果連接成功，則消息 **連接成功** 的上界。 按一下 **確定** 在留言上，然後 **確定** 對話框。

   如果無法連接到目標，請參閱 [故障排除](#troubleshooting-target-connection-problems) 的子菜單。

### 添加目標框架 {#adding-a-target-framework}

<!-- Is this section needed? -->

配置目標雲配置後，添加目標框架。 該框架標識從可用地址發送到Adobe Target的預設參數 [上下文中心](/help/implementing/developing/personalization/configuring-contexthub.md) 元件。 目標使用參數來確定應用於當前上下文的段。

可以為單個目標配置建立多個框架。 當您需要將一組不同的參數發送給網站不同部分的「目標」時，多個框架非常有用。 為需要發送的每組參數建立一個框架。 將網站的每個部分與相應的框架相關聯。 請注意，網頁一次只能使用一個框架。

1. 在「目標配置」頁上，按一下 **+** （加號）。

1. 在「建立框架」對話框中，指定 **標題**，選擇 **Adobe Target框架**，然後按一下 **建立**。

   <!-- ![config-target-framework-dialog](assets/config-target-framework-dialog.png) -->

   將開啟框架頁面。 Sidekick提供表示來自 [上下文中心](/help/implementing/developing/personalization/configuring-contexthub.md) 你可以畫地圖。

   <!-- ![chlimage_1-162](assets/chlimage_1-162.png) -->

1. 拖動表示要用於映射到放置目標的資料的客戶端上下文元件。 或者，拖動 **上下文中心儲存** 框架的元件。

   >[!NOTE]
   >
   >映射時，參數通過簡單字串傳遞到mbox。 不能從ContextHub映射陣列。

   例如，要使用 **配置檔案資料** 關於站點訪問者以控制目標市場活動，拖動 **配置檔案資料** 元件。 將顯示可用於映射到「目標」參數的配置檔案資料變數。

   <!-- ![chlimage_1-163](assets/chlimage_1-163.png) -->

1. 通過選擇要使Adobe Target系統可見的變數 **共用** 的子菜單。

   <!-- ![chlimage_1-164](assets/chlimage_1-164.png) -->

   >[!NOTE]
   >
   >同步參數只是一種方式 — 從AEM到Adobe Target。

已建立框架。 要將框架複製到發佈實例，請使用 **激活框架** 從旁邊踢出。

<!--
### Associating Activities With the Target Cloud Configuration  {#associating-activities-with-the-target-cloud-configuration}

Associate your [AEM activities](/help/sites-cloud/authoring/personalization/activities.md) with your Target cloud configuration so that you can mirror the activities in [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
>What types of activities are available is determined by the following:
>
>* If the **xt_only** option is enabled on the Adobe Target tenant (clientcode) used on the AEM side to connect to Adobe Target, then you can create **only** XT activities in AEM.
>
>* If the **xt_only** options is **not** enabled on the Adobe Target tenant (clientcode), then you can create **both** XT and A/B activities in AEM.
>
>**Additional note:** **xt_only** options is a setting applied on a certain Target tenant (clientcode) and can only be modified directly in Adobe Target. You cannot enable or disable this option in AEM.
-->

<!--
### Associating the Target Framework With Your Site {#associating-the-target-framework-with-your-site}

After you create a Target framework in AEM, associate your web pages with the framework. The targeted components on the pages send the framework-defined data to Adobe Target for tracking. (See [Content Targeting](/help/sites-cloud/authoring/personalization/targeted-content.md).)

When you associate a page with the framework, the child pages inherit the association.

1. In the **Sites** console, navigate to the site that you want to configure.
1. Using either [quick actions](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) or [selection mode](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources), select **View Properties.**
1. Select the **Cloud Services** tab.
1. Tap/click **Edit**.
1. Tap/click **Add Configuration** under **Cloud Service Configurations** and select **Adobe Target**.

  ![chlimage_1-165](assets/chlimage_1-165.png)

1. Select the framework you want under **Configuration Reference**.

   >[!NOTE]
   >
   >Make sure that you select the specific **framework** that you created and not the Target cloud configuration under which it was created.

1. Tap/click **Done**.
1. Activate the root page of the website to replicate it to the publish server. (See [How To Publish Pages](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).)

   >[!NOTE]
   >
   >If the framework you attached to the page was not activated yet, a wizard opens which allows you to publish it as well.
-->

<!--
### Troubleshooting Target Connection Problems {#troubleshooting-target-connection-problems}

Perform the following tasks to troubleshoot problems that occur when connecting to Target:

* Make sure that the user credentials that you provide are correct.
* Make sure that the AEM instance can connect to the Target server. For example, make sure that firewall rules are not blocking outbound AEM connections, or that AEM is configured to use necessary proxies.
* Look for helpful messages in the AEM error log. The error.log file is located in the **crx-quickstart/logs** directory where AEM is installed.
* When editing the activity in Adobe Target, the URL is pointing to localhost. Work around this by setting the AEM externalizer to the correct URL.
-->

## 將體驗片段輸出到Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>對於介質資產（如影像），只有引用會導出到目標。 資產本身仍保存在AEM Assets，並從發佈實例AEM交付。
>
>因此，在導出到目標之前，需要發佈包含所有相關資產的「體驗」片段。

要將體驗片段從導AEM出到目標（指定雲配置後）:

1. 導航到「體驗片段」控制台。
1. 選擇要導出到目標的體驗片段。

   >[!NOTE]
   >
   >它必須是體驗片段網頁變體。

1. 點擊/按一下 **對Adobe Target的出口**。

   >[!NOTE]
   >
   >如果已導出體驗片段，請選擇 **更新Adobe Target**。

1. 點擊/按一下 **導出而不發佈** 或 **發佈** 按需要。

   >[!NOTE]
   >
   >選擇 **發佈** 將立即發佈體驗片段並將其發送到目標。

1. 點擊/按一下 **確定** 的子菜單。

   您的體驗片段現在應位於目標中。

   >[!NOTE]
   >
   >[各種詳細資訊](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#details-of-your-experience-fragment) 可在 **清單視圖** 控制台和 **屬性**。

   >[!NOTE]
   >
   >在Adobe Target觀看體驗片段時， *上次修改* 可見的日期是上次修改片段的日期AEM，而不是上次將片段導出到Adobe Target的日期。

>[!NOTE]
>
>或者，也可以使用 [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 的子菜單。

## 用你在Adobe Target的經驗片段 {#using-your-experience-fragments-in-adobe-target}

執行上述任務後，體驗片段將顯示在「目標」中的「優惠」頁上。 請看 [特定目標文檔](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) 瞭解你能在那裡取得什麼成就。

>[!NOTE]
>
>在Adobe Target觀看體驗片段時， *上次修改* 可見的日期是上次修改片段的日期AEM，而不是上次將片段導出到Adobe Target的日期。

## 刪除已導出到Adobe Target的體驗片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

如果刪除已導出到目標的體驗片段，則如果該片段已在目標中的優惠中使用，則可能會導致問題。 如果刪除片段，則當片段內容由傳遞時，將導致提供不可用AEM。

為避免此類情況：

* 如果活動中當前未使用體驗片段，則AEM允許用戶刪除該片段而不顯示警告消息。
* 如果「目標」中的活動當前正在使用「體驗片段」，則會出現一條錯誤消息AEM，警告用戶刪除該片段可能對活動造成的後果。

   中的錯誤AEM消息不禁止用戶（強制）刪除體驗片段。 如果刪除了「體驗」片段：

   * 具有經驗片段的目AEM標產品可能顯示不期望的行為

      * 隨著將「體驗片段」HTML推到「目標」，此報價可能仍將呈現
      * 如果中也刪除了引用的資產，則「體驗」片段中的任何引用可能AEM無法正確工作。
   * 當然，對經驗片段的任何進一步修改都是不可能的，因為經驗片段在中已不存AEM在。
