---
title: 將體驗片段匯出至Adobe Target
description: 將體驗片段匯出至Adobe Target
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '2259'
ht-degree: 0%

---

# 將體驗片段匯出至Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* AEM體驗片段會匯出至Adobe Target的預設工作區。
>* AEM必鬚根據 [與Adobe Target整合](/help/sites-cloud/integrating/integrating-adobe-target.md).


您可以匯出 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)，在Adobe Experience Manager as a Cloud Service(AEM)中建立，到Adobe Target(Target)。 然後可在Target活動中作為選件，以大規模測試並個人化體驗。

有三個選項可用來匯出體驗片段至Adobe Target:

* HTML（預設）:支援網頁和混合式內容傳送
* JSON:支援無頭內容傳送
* HTML 和 JSON

若要準備您的執行個體以將AEM體驗片段匯出至Adobe Target，您必須：

* [整合Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [新增雲端設定](#add-the-cloud-configuration)
* [新增舊組態](#add-the-legacy-configuration)

之後，您可以：

* [將體驗片段匯出至Adobe Target](#exporting-an-experience-fragment-to-adobe-target)
* [在Adobe Target中使用您的體驗片段](#using-your-experience-fragments-in-adobe-target)
* 還有 [刪除已匯出至Adobe Target的體驗片段](#deleting-an-experience-fragment-already-exported-to-adobe-target)

體驗片段可匯出至Adobe Target中的預設工作區，或匯出至Adobe Target的使用者定義工作區。

>[!NOTE]
>
>Adobe Target工作區不存在於Adobe Target本身。 這些範本會在Adobe IMS(Identity Management系統)中定義和管理，然後選取此選項，以便在使用Adobe Developer Console的各解決方案中使用。

>[!NOTE]
>
>Adobe Target工作區可用來允許組織（群組）的成員僅建立和管理此組織的選件和活動；而不授予其他使用者存取權。 例如，全球關注的特定國家組織。

>[!NOTE]
>
>如需詳細資訊，另請參閱：
>
>* [Adobe Target開發](https://developers.adobetarget.com/)
>* [核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
>* [Adobe Target — 如何使用Adobe Experience Manager(AEM)體驗片段？](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)
>* [AEM 6.5 — 手動設定與Adobe Target的整合 — 建立Target雲端設定](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-configuring.html#creating-a-target-cloud-configuration)


## 必備條件 {#prerequisites}

需要執行各種動作：

1. 你必須 [將AEM與Adobe Target整合](/help/sites-cloud/integrating/integrating-adobe-target.md).

1. 體驗片段會從AEM製作例項匯出，因此您需要 [設定AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) 在製作例項上，以確保體驗片段內的任何參考會外部化以進行網頁傳送。

   >[!NOTE]
   >
   >對於預設未涵蓋的連結重寫， [體驗片段連結重寫器提供者](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) 的URL區段。 借此，您可針對執行個體開發自訂規則。

## 新增雲端設定 {#add-the-cloud-configuration}

匯出片段之前，您需要新增 **雲端設定** for **Adobe Target** 至片段或資料夾。 這也可讓您：

* 指定要用於匯出的格式選項
* 選擇目標工作區作為目標
* 選取外部化程式網域，以重新寫入體驗片段中的參考（選用）

您可以在 **頁面屬性** 所需資料夾和/或片段；將視需要繼承規範。

1. 導覽至 **體驗片段** 控制台。

1. 開啟 **頁面屬性** ，以取得適當的資料夾或片段。

   >[!NOTE]
   >
   >如果您將雲端設定新增至體驗片段上層資料夾，設定會由所有子項繼承。
   >
   >如果您將雲端設定新增至體驗片段本身，則設定會由所有變數繼承。

1. 選取 **Cloud Services** 標籤。

1. 在 **Cloud Service配置**，選取 **Adobe Target** 從下拉式清單中。

   >[!NOTE]
   >
   >體驗片段選件的JSON格式可自訂。 若要這麼做，請定義客戶體驗片段元件，然後註解如何在元件Sling模型中匯出其屬性。
   >
   >請參閱核心元件： [核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

1. 在 **Adobe Target** 選擇：

   * 適當的配置
   * 所需格式選項
   * Adobe Target工作區
   * 如有必要 — externalizer域

   >[!CAUTION]
   >
   >外部化程式域是可選的。
   >
   > 當您希望匯出的內容指向特定 *發佈* 網域。 如需更多詳細資訊，請參閱 [設定AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer).
   >
   > 另請注意，外部化程式網域僅與傳送至Target的體驗片段內容相關，而與檢視選件內容等中繼資料無關。

   例如，對於資料夾：

   ![資料夾 — Cloud Services](assets/xf-target-integration-01.png "資料夾 — Cloud Services")

1. **儲存並關閉**.

## 新增舊組態 {#add-the-legacy-configuration}

<!-- This is effectively the Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target} section from 6.5 -->

>[!IMPORTANT]
>
>新增新舊組態是特殊案例，僅支援匯出體驗片段。

之後 [添加雲配置](#add-the-cloud-configuration) 若要使用Launch by Adobe，若要最初將AEM與Adobe Target整合，您還需要使用舊版設定手動與Adobe Target整合。

### 建立Target雲端設定 {#creating-a-target-cloud-configuration}

若要讓AEM與Adobe Target互動，請建立Target雲端設定。 若要建立設定，請提供Adobe Target用戶端代碼和使用者憑證。

您只需建立Target雲端設定一次，因為您可以將設定與多個AEM促銷活動建立關聯。 如果您有數個Adobe Target用戶端代碼，請為每個用戶端代碼建立一個設定。

您可以設定雲端設定，以從Adobe Target同步區段。 如果啟用同步，當儲存雲端設定時，就會立即從背景的Target匯入區段。

請依照下列步驟，在AEM中建立Target雲端設定：

1. 導覽至 **舊版Cloud Services** 透過 **AEM標誌** > **工具** > **Cloud Services** > **舊版Cloud Services**.
例如：([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   此 **Adobe Experience Cloud** 概覽頁面隨即開啟。

1. 在 **Adobe Target** ，按一下 **立即配置**.
1. 在 **建立配置** 對話框：

   1. 為設定指定 **標題**.
   1. 選取 **Adobe Target設定** 範本。
   1. 按一下&#x200B;**建立**。

您現在可以選取要編輯的新設定。

1. 編輯對話方塊隨即開啟。

   ![config-target-settings-dialog](assets/config-target-settings-dialog.png)

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

1. 在 **Adobe Target設定** 對話框，請為這些屬性提供值。

   * **驗證**:這預設為IMS（不建議使用使用者憑證）

   * **用戶端代碼**:目標帳戶客戶端代碼

   * **租用戶ID**:租用戶ID

   * **IMS設定**:從下拉式清單中選取所需的設定

   * **API類型**:預設為REST（不支援XML）

   * **A4T Analytics Cloud設定**:選取用於目標活動目標和量度的Analytics雲端設定。 如果您在鎖定目標內容時使用Adobe Analytics作為報表來源，則需要此功能。

      <!-- Is this needed?
     If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).
     -->

   * **使用準確的定位：** 依預設，此核取方塊會選取。 如果選取此選項，雲端服務設定會在載入內容之前等待內容載入。 請參閱以下備注。

   * **從Adobe Target同步區段：** 選取此選項可下載Target中定義的區段，以便在AEM中使用。 當API類型屬性為REST時，您必須選取此選項，因為不支援內嵌區段，且您一律需要使用Target中的區段。 (請注意，「區段」的AEM詞語等同於Target「對象」。)

   * **客戶端庫：** 這預設為AT.js（已棄用mbox.js）

      >[!NOTE]
      >
      >目標庫檔案， [AT.JS](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html)，是新的Adobe Target實作程式庫，專為典型Web實作和單頁應用程式而設計。
      >
      >mbox.js已遭取代，將在稍後階段移除。
      >
      >Adobe建議您使用AT.js（而非mbox.js）作為用戶端程式庫。
      >
      >AT.js提供幾項優於mbox.js資料庫的改善：
      >
      >* 改善Web實作的頁面載入時間
      >* 提高安全性
      >* 更適合單頁應用程式的實作選項
      >* AT.js包含target.js中包含的元件，因此不再需要呼叫target.js

      >
      >您可以在 **用戶端程式庫** 下拉式功能表。

   * **使用Tag Management系統來傳送用戶端程式庫**  — 選取此選項，使用AdobeLaunch或其他標籤管理系統（或已廢止的DTM）中的用戶端程式庫。

   * **自訂AT.js**:瀏覽以上傳自訂AT.js。 保留空白以使用預設程式庫。

      >[!NOTE]
      >
      >依預設，當您選擇加入Adobe Target設定精靈時，會啟用「精確鎖定目標」。
      >
      >準確鎖定目標表示雲端服務設定會在載入內容前等待內容載入。 因此，就效能而言，精確鎖定目標可能會在載入內容前造成毫秒的延遲。
      >
      >一律會在製作例項上啟用正確鎖定目標。 不過，在發佈執行個體上，您可以在雲端服務設定中清除「精確鎖定目標」旁的勾號，選擇全域關閉精確鎖定目標(**http://localhost:4502/etc/cloudservices.html**)。 無論您在雲端服務設定中進行什麼設定，您仍可開啟或關閉個別元件的精確鎖定目標。
      >
      >若您有 ***已*** 已建立目標元件，而您變更此設定時，您所做的變更不會影響這些元件。 您必須直接對這些元件進行任何變更。

1. 按一下 **連線至Adobe Target** 初始化與Target的連線。 如果連線成功，則會顯示訊息 **連接成功** 的下界。 按一下 **確定** 在消息上，然後 **確定** 對話框。

   如果您無法連線至Target，請參閱 [疑難排解](#troubleshooting-target-connection-problems) 區段。

### 新增Target架構 {#adding-a-target-framework}

<!-- Is this section needed? -->

設定Target雲端設定後，新增Target架構。 此架構可識別從可用 [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) 元件。 Target使用參數來判斷要套用至目前內容的區段。

您可以為單一Target設定建立多個架構。 當您需要針對網站的不同區段傳送不同的一組參數至Target時，多個架構就十分實用。 為您需要傳送的每組參數建立架構。 將網站的每個區段與適當的架構建立關聯。 請注意，網頁一次只能使用一個架構。

1. 在您的Target設定頁面上，按一下 **+** （加號）。

1. 在「建立框架」對話框中，指定 **標題**，請選取 **Adobe Target架構**，然後按一下 **建立**.

   <!-- ![config-target-framework-dialog](assets/config-target-framework-dialog.png) -->

   框架頁面隨即開啟。 Sidekick提供代表 [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) 你可以映射的。

   <!-- ![chlimage_1-162](assets/chlimage_1-162.png) -->

1. 拖曳代表您要用於對應至放置目標的資料的用戶端內容元件。 或者，拖曳 **ContextHub存放區** 構成部分。

   >[!NOTE]
   >
   >映射時，參數會透過簡單字串傳遞至mbox。 無法從ContextHub映射陣列。

   例如，若要使用 **設定檔資料** 關於網站訪客以控制Target促銷活動，請拖曳 **設定檔資料** 元件。 此時會顯示可用於對應至Target參數的設定檔資料變數。

   <!-- ![chlimage_1-163](assets/chlimage_1-163.png) -->

1. 選取要讓Adobe Target系統可見的變數，方法是選取 **共用** 核取方塊。

   <!-- ![chlimage_1-164](assets/chlimage_1-164.png) -->

   >[!NOTE]
   >
   >同步參數只是一種方式 — 從AEM到Adobe Target。

已建立您的架構。 若要將架構複製到發佈執行個體，請使用 **啟動框架** 選項。

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

## 將體驗片段匯出至Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>若為媒體資產（例如影像），則只會將參考匯出至Target。 資產本身會保存在AEM Assets中，並從AEM發佈例項傳送。
>
>因此，匯出至Target之前，必須先發佈體驗片段及所有相關資產。

若要將體驗片段從AEM匯出至Target（指定雲端設定後）:

1. 導覽至體驗片段主控台。
1. 選取您要匯出至目標的體驗片段。

   >[!NOTE]
   >
   >必須是體驗片段Web變數。

1. 點選/按一下 **匯出至Adobe Target**.

   >[!NOTE]
   >
   >如果體驗片段已匯出，請選取 **Adobe Target中的更新**.

1. 點選/按一下 **不發佈即可匯出** 或 **發佈** 視需要。

   >[!NOTE]
   >
   >選取 **發佈** 會立即發佈體驗片段並傳送至Target。

1. 點選/按一下 **確定** 在確認對話方塊中。

   您的體驗片段現在應位於Target中。

   >[!NOTE]
   >
   >[各種詳細資訊](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#details-of-your-experience-fragment) 的 **清單檢視** 控制台和 **屬性**.

   >[!NOTE]
   >
   >在Adobe Target中檢視體驗片段時， *上次修改* 顯示的日期是片段上次在AEM中修改的日期，而非片段上次匯出至Adobe Target的日期。

>[!NOTE]
>
>或者，您也可以使用 [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 功能表。

## 在Adobe Target中使用您的體驗片段 {#using-your-experience-fragments-in-adobe-target}

執行先前的工作後，體驗片段會顯示在Target的「選件」頁面上。 請看 [特定Target檔案](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) 了解你能在那裡實現什麼。

>[!NOTE]
>
>在Adobe Target中檢視體驗片段時， *上次修改* 顯示的日期是片段上次在AEM中修改的日期，而非片段上次匯出至Adobe Target的日期。

## 刪除已匯出至Adobe Target的體驗片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

刪除已匯出至Target的體驗片段，如果該片段已用於Target中的選件，則可能會造成問題。 刪除片段會導致選件無法使用，因為AEM正在傳送片段內容。

要避免這種情況：

* 如果活動中目前未使用體驗片段，AEM可讓使用者刪除片段，而不含警告訊息。
* 如果Target中的活動目前正在使用體驗片段，則會出現錯誤訊息，警告AEM使用者刪除片段對活動可能造成的後果。

   AEM中的錯誤訊息並未禁止使用者（強制）刪除體驗片段。 如果刪除體驗片段：

   * 具有AEM體驗片段的Target選件可能會顯示不適當的行為

      * 由於體驗片段HTML推送至Target，選件可能仍會呈現
      * 如果參考的資產也在AEM中刪除，體驗片段中的任何參考可能也無法正常運作。
   * 當然，由於體驗片段已不存在，因此無法對體驗片段進行任何進一步修改。
