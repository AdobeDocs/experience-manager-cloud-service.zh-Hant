---
title: 將體驗片段匯出到 Adobe Target
description: 瞭解如何將您的體驗片段匯出至Adobe Target，以測試並個人化體驗。
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 1%

---

# 將體驗片段匯出到 Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* AEM體驗片段會匯出至Adobe Target的預設工作區。
>* AEM必須依照下的指示與Adobe Target整合 [與Adobe Target整合](/help/sites-cloud/integrating/integrating-adobe-target.md).

您可以匯出 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)，在Adobe Experience Manager as a Cloud Service (AEM)中建立並移至Adobe Target (Target)。 然後，它們可以當作Target活動中的選件，以大規模測試並個人化體驗。

有三個選項可用來將體驗片段匯出至Adobe Target：

* HTML（預設）：支援網頁和混合式內容傳遞
* JSON：支援Headless內容傳送
* HTML 和 JSON

若要準備您的執行個體以將AEM體驗片段匯出至Adobe Target，您需要：

* [整合Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [新增雲端設定](#add-the-cloud-configuration)
* [新增舊組態](#add-the-legacy-configuration)

之後，您可以：

* [將體驗片段匯出至Adobe Target](#exporting-an-experience-fragment-to-adobe-target)
* [在Adobe Target中使用您的體驗片段](#using-your-experience-fragments-in-adobe-target)
* 以及 [刪除已匯出至Adobe Target的體驗片段](#deleting-an-experience-fragment-already-exported-to-adobe-target)

體驗片段可以匯出至Adobe Target中的預設工作區，或匯出至Adobe Target的使用者定義工作區。

>[!NOTE]
>
>Adobe Target本身並不存在Adobe Target工作區。 可透過Adobe IMS (Identity Management系統)進行定義和管理，接著使用Adobe Developer Console選取跨解決方案使用的虛擬報表套裝。

>[!NOTE]
>
>Adobe Target工作區可用來允許組織（群組）的成員僅針對此組織建立和管理優惠方案及活動，不將存取權授予其他使用者。 例如，全球關注的國家/地區特定組織。

>[!NOTE]
>
>如需詳細資訊，請參閱下列內容：
>
>* [Adobe Target開發](https://developers.adobetarget.com/)
>* [核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
>* [Adobe Target — 如何使用Adobe Experience Manager (AEM)體驗片段？](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)
>* [AEM 6.5 — 手動設定與Adobe Target的整合 — 建立Target雲端設定](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-configuring.html#creating-a-target-cloud-configuration)

## 先決條件 {#prerequisites}

需要執行各種動作：

1. 您必須 [將AEM與Adobe Target整合](/help/sites-cloud/integrating/integrating-adobe-target.md).

1. 體驗片段會從AEM編寫執行個體匯出，因此您需要 [設定AEM連結外部器](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) 在作者執行個體上，以確保體驗片段中的任何參考資料都會外部化，以利網頁傳送。

   >[!NOTE]
   >
   >對於預設未涵蓋的連結重寫， [體驗片段連結重寫器提供者](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) 可用。 如此一來，您就可以針對執行個體開發自訂規則。

## 新增雲端設定 {#add-the-cloud-configuration}

在匯出片段之前，您需要新增 **雲端設定** 的 **Adobe Target** 至片段或資料夾。 這也可讓您：

* 指定要用於匯出的格式選項
* 選取Target工作區作為目的地
* 選取外部化器網域，以重寫體驗片段中的參照（選用）

您可在以下位置選取所需選項： **頁面屬性** 所需資料夾或/和片段的；會視需要繼承規格。

1. 導覽至 **體驗片段** 主控台。

1. 開啟 **頁面屬性** 用於適當的資料夾或片段。

   >[!NOTE]
   >
   >如果您將雲端設定新增至體驗片段父資料夾，設定將由所有子系繼承。
   >
   >如果您將雲端設定新增至體驗片段本身，該設定會由所有變體繼承。

1. 選取 **Cloud Service** 標籤。

1. 在 **Cloud Service設定**，選取 **Adobe Target** 下拉式清單中的。

   >[!NOTE]
   >
   >可自訂體驗片段選件的JSON格式。 若要這麼做，請定義客戶體驗片段元件，然後註明如何在元件Sling模型中匯出其屬性。
   >
   >請參閱核心元件： [核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

1. 在 **Adobe Target** 選取：

   * 適當的設定
   * 所需的格式選項
   * Adobe Target工作區
   * 如有必要 — 外部化器網域

   >[!CAUTION]
   >
   >外部化器網域是選用的。
   >
   > 當您想要匯出的內容指向特定時，就會設定AEM外部器 *發佈* 網域。 如需詳細資訊，請參閱 [設定AEM連結外部器](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer).
   >
   > 另請注意，外部化器網域僅與傳送至Target的體驗片段內容相關，與檢視選件內容之類的中繼資料無關。

   例如，針對資料夾：

   ![資料夾 — Cloud Service](assets/xf-target-integration-01.png "資料夾 — Cloud Service")

1. **儲存並關閉**.

## 新增舊組態 {#add-the-legacy-configuration}

<!-- This is effectively the Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target} section from 6.5 -->

>[!IMPORTANT]
>
>新增舊版設定是一種特殊情況，僅支援匯出體驗片段。

晚於 [新增雲端設定](#add-the-cloud-configuration) 若要使用Launch by Adobe，若要將AEM與Adobe Target整合，您還需要使用舊版設定手動與Adobe Target整合。

### 建立Target雲端設定 {#creating-a-target-cloud-configuration}

若要讓AEM與Adobe Target互動，請建立Target雲端設定。 若要建立設定，您必須提供Adobe Target使用者端代碼和使用者認證。

您只會建立一次Target雲端設定，因為您可以將此設定與多個AEM行銷活動建立關聯。 如果您有多個Adobe Target使用者端代碼，請為每個使用者端代碼建立一個設定。

您可以設定雲端設定，以從Adobe Target同步區段。 如果您啟用同步，儲存雲端設定後，會立即在背景從Target匯入區段。

使用以下程式，在AEM中建立Target雲端設定：

1. 瀏覽至 **舊版Cloud Service** 透過 **AEM標誌** > **工具** > **Cloud Service** > **舊版Cloud Service**.
例如：([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   此 **Adobe Experience Cloud** 概觀頁面隨即開啟。

1. 在 **Adobe Target** 區段，按一下 **立即設定**.
1. 在 **建立設定** 對話方塊：

   1. 為設定提供 **標題**.
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
   >1. Select **Save All**.

   -->

1. 在 **Adobe Target設定** 對話方塊，提供這些屬性的值。

   * **驗證**：此專案預設為IMS （已棄用使用者憑證）

   * **使用者端代碼**：Target帳戶使用者端代碼

   * **租使用者ID**：租使用者ID

   * **IMS設定**：從下拉式清單中選取所需的設定

   * **API型別**：預設為REST （已棄用XML）

   * **A4T Analytics Cloud設定**：選取用於鎖定活動目標和量度的Analytics雲端設定。 如果您在鎖定目標內容時使用Adobe Analytics作為報表來源，則需要此專案。

     <!-- Is this needed?
     If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).
     -->

   * **使用準確定位：** 依預設，會選取此核取方塊。 如果選取，雲端服務設定將等待內容載入後再載入內容。 請參閱下列備註。

   * **從Adobe Target同步區段：** 選取此選項可下載Target中定義的區段，以便在AEM中使用。 當「API型別」屬性為REST時，選取此選項，因為內嵌區段不受支援，而且您一律需要使用來自Target的區段。 ( AEM術語「區段」等同於Target「對象」。)

   * **使用者端資源庫：** 此預設為AT.js （已棄用mbox.js）

     >[!NOTE]
     >
     >Target程式庫檔案， [AT.JS](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/at-js/how-atjs-works.html)是新的Adobe Target實作程式庫，專為典型Web實作和單頁應用程式而設計。
     >
     >mbox.js已過時，並將在稍後階段移除。
     >
     >Adobe建議您使用AT.js而非mbox.js作為使用者端資料庫。
     >
     >AT.js對mbox.js資料庫提供數項改善專案：
     >
     >* 改善Web實施的頁面載入時間
     >* 提升安全性
     >* 單頁應用程式的更佳實作選項
     >* AT.js包含target.js所包含的元件，因此不再需要呼叫target.js
     >
     >您可以選取「 」中的AT.js或mbox.js **客戶庫** 下拉式功能表。

   * **使用Tag Management系統提供使用者端資源庫**  — 選取此選項，以使用AdobeLaunch或其他標籤管理系統（或DTM，已棄用）的使用者端程式庫。

   * **自訂AT.js**：瀏覽以上傳您的自訂AT.js。 留空將使用預設程式庫。

     >[!NOTE]
     >
     >依預設，當您選擇加入Adobe Target設定精靈時，會啟用「準確定位」 。
     >
     >準確定位表示雲端服務設定會等待內容載入後再載入內容。 因此，就效能而言，準確定位可能會在載入內容前造成幾毫秒的延遲。
     >
     >作者例項上一律會啟用「準確定位」 。 不過在發佈執行個體上，您可以清除雲端服務設定中「準確定位」旁的核取記號，來選擇全域關閉準確定位(**http://localhost:4502/etc/cloudservices.html**)。 無論您在雲端服務設定中的設定為何，您仍可開啟和關閉個別元件的準確定位。
     >
     >如果您有 ***已經*** 已建立目標元件，而您變更此設定，您的變更不會影響這些元件。 您必須直接對這些元件進行任何變更。

1. 按一下 **連線至Adobe Target** 以初始化與Target的連線。 如果連線成功，則訊息會顯示 **連線成功** 隨即顯示。 按一下 **確定** 在訊息上，然後 **確定** 在對話方塊上。

### 新增Target框架 {#adding-a-target-framework}

<!-- Is this section needed? -->

設定Target雲端設定後，請新增Target框架。 此架構會識別從可用傳送至Adobe Target的預設引數 [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) 元件。 Target會使用引數來決定套用至目前內容的區段。

您可以為單一Target設定建立多個架構。 如果您需要針對網站的不同區段傳送一組不同的引數至Target，則多個架構會很有用。 為您需要傳送的每組引數建立框架。 將網站的每個區段與適當的架構建立關聯。 請注意，一個網頁一次只能使用一個架構。

1. 在Target設定頁面上，按一下 **+** （加號）並列於「可用設定」旁。

1. 在「建立架構」對話方塊中，指定 **標題**，選取 **Adobe Target框架**，然後按一下 **建立**.

   <!-- ![config-target-framework-dialog](assets/config-target-framework-dialog.png) -->

   框架頁面隨即開啟。 Sidekick提供的元件代表來自 [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) 可以對映的專案。

   <!-- ![Framework](assets/chlimage_1-162.png) -->

1. 將代表您要用來對應之資料的「從屬端內容」元件拖曳至放置目標。 或者，拖曳 **ContextHub存放區** 元件至框架。

   >[!NOTE]
   >
   >對應時，引數會透過簡單字串傳遞至mbox。 您無法從ContextHub對應陣列。

   例如，若要使用 **設定檔資料** 關於您的網站訪客以控制Target促銷活動，請拖曳 **設定檔資料** 元件至頁面。 可用於對應至Target引數的設定檔資料變數隨即顯示。

   <!-- ![Profile Data](assets/chlimage_1-163.png) -->

1. 選取您要對Adobe Target系統可見的變數，方法是選取 **共用** 核取方塊。

   <!-- ![Share](assets/chlimage_1-164.png) -->

   >[!NOTE]
   >
   >同步引數是唯一方式 — 從AEM到Adobe Target。

您的框架隨即建立。 若要將框架復寫至發佈執行個體，請使用 **啟動框架** Sidekick中的選項。

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
1. Select **Edit**.
1. Select **Add Configuration** under **Cloud Service Configurations** and select **Adobe Target**.

  ![Cloud Service Configuration](assets/chlimage_1-165.png)

1. Select the framework you want under **Configuration Reference**.

   >[!NOTE]
   >
   >Make sure that you select the specific **framework** that you created and not the Target cloud configuration under which it was created.

1. Select **Done**.
1. Activate the root page of the website to replicate it to the publish server. (See [How To Publish Pages](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).)

   >[!NOTE]
   >
   >If the framework you attached to the page was not activated yet, a wizard opens which lets you publish it as well.
-->

## 將體驗片段匯出至Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>對於媒體資產（例如影像），只會將參考匯出至Target。 資產本身仍會儲存在AEM Assets中，並從AEM發佈例項傳送。
>
>因此，在匯出至Target之前，必須發佈包含所有相關資產的體驗片段。

若要將體驗片段從AEM匯出至Target （在指定雲端設定後）：

1. 導覽至體驗片段主控台。
1. 選取您要匯出至Target的體驗片段。

   >[!NOTE]
   >
   >它必須是體驗片段Web變數。

1. 選取 **匯出至Adobe Target**.

   >[!NOTE]
   >
   >如果體驗片段已匯出，請選取「 」 **Adobe Target中的更新**.

1. 選取 **不發佈即匯出** 或 **發佈** 視需要。

   >[!NOTE]
   >
   >選取 **發佈** 將立即發佈體驗片段並將其傳送到Target。

1. 選取 **確定** 在確認對話方塊中。

   您的體驗片段現在應該在Target中。

   >[!NOTE]
   >
   >[各種詳細資訊](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#details-of-your-experience-fragment) 匯出的檔案可在下列位置檢視： **清單檢視** 主控台和 **屬性**.

   >[!NOTE]
   >
   >在Adobe Target中檢視體驗片段時， *上次修改時間* 看到的日期是上次在AEM中修改片段的日期，而不是上次將片段匯出至Adobe Target的日期。

>[!NOTE]
>
>或者，您也可以使用下列檔案中的類似命令，從頁面編輯器執行匯出 [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 功能表。

## 在Adobe Target中使用您的體驗片段 {#using-your-experience-fragments-in-adobe-target}

執行先前的工作後，體驗片段會顯示在Target的「選件」頁面中。 另請參閱 [特定Target檔案](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) 以瞭解您能達成的目標。

>[!NOTE]
>
>在Adobe Target中檢視體驗片段時， *上次修改時間* 看到的日期是上次在AEM中修改片段的日期，而不是上次將片段匯出至Adobe Target的日期。

## 刪除已匯出至Adobe Target的體驗片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

刪除已匯出至Target的體驗片段，如果片段已用於Target的選件中，可能會造成問題。 刪除片段會導致選件無法使用，因為AEM正在傳遞片段內容。

若要避免此類情況：

* 如果體驗片段目前未用於活動中，AEM可讓使用者刪除片段而不顯示警告訊息。
* 如果Target中的活動目前正在使用體驗片段，則會出現錯誤訊息，警告AEM使用者刪除片段可能會對活動造成的後果。

  AEM中的錯誤訊息不會禁止使用者（強制）刪除體驗片段。 如果刪除體驗片段：

   * 具有AEM體驗片段的Target選件可能會顯示不良行為

      * 由於體驗片段HTML已推送至Target，因此該選件很可能仍會呈現
      * 如果也在AEM中刪除了參照的資產，體驗片段中的任何參照都無法正常運作。

   * 當然，由於體驗片段在AEM中不再存在，因此無法對體驗片段進行任何進一步的修改。
