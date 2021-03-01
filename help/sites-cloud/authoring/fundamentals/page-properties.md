---
title: 編輯頁面屬性
description: 定義頁面的必要屬性
translation-type: tm+mt
source-git-commit: 66b2fb19cbc4c8aa480f1ace31a7f973dc7fb0f7
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 8%

---


# 編輯頁面屬性{#editing-page-properties}

您可以定義頁面的必要屬性。 這些視頁面性質而定。 例如，有些頁面可能會連線至即時副本，而其他頁面則未連線，且即時副本資訊會視需要提供。

## 頁面內容 {#page-properties}

屬性分佈在多個頁籤上。

### 基本 {#basic}

* **標題與標籤**

   * **Title**  —— 頁面標題會顯示在不同位置。例如，**Websites**&#x200B;標籤清單和&#x200B;**Sites**&#x200B;卡片／清單檢視。
      * 這是必要欄位。
   * **標籤** -您可以在這裡新增標籤，或透過更新選取方塊中的清單，從頁面中移除標籤。
      * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
      * 您可以在空的選取方塊中輸入名稱，以輸入全新的標籤。
         * 當您按Enter時，將會建立新標籤。
         * 然後，新標籤會在右側顯示，並加上一個小星號，表示它是新標籤。
      * 透過下拉式功能，您可從現有標籤中選取。
      * 當您將滑鼠移至選取方塊中的標籤項目上時，會顯示x，可用來移除此頁面的標籤。
      * 如需標籤的詳細資訊，請參閱[使用標籤](/help/sites-cloud/authoring/features/tags.md)。
   * **在導覽中隱藏** -指出在產生的網站的頁面導覽中是否顯示或隱藏頁面。

* **品牌化**

   將品牌邊界附加至每個頁面標題，以跨頁套用一致的品牌識別。 此功能需要使用[核心元件2.14.0版或更新版本的頁面元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)

   * **覆寫** -勾選以定義此頁面上的品牌印刷邊界。
      * 任何子頁面都將繼承該值，除非它們也設定了&#x200B;**Override**&#x200B;值。
   * **覆寫值** -要附加至頁面標題的品牌印刷邊界文字。
      * 該值會附加在垂直號字元（例如「循環圖表」）後的頁面標題中 |隨時為WKND做好準備&quot;

* **HTML ID**

   * **ID**  —— 套用至元件的HTML ID。

* **更多標題和說明**

   * **頁面標題** -用於頁面上的標題。通常由標題元件使用。 如果空白，則會使用&#x200B;**Title**。
   * **導覽標題** -您可以指定個別的標題，以用於導覽（例如，如果您想要更簡潔的內容）。如果為空，則使用&#x200B;**Title**。
   * **副標題** -頁面上使用的副標題。
   * **說明** -您對頁面、其用途或您要新增的任何其他詳細資訊的說明。

* **開啟/關閉時間**

   * **On Time**  —— 發佈環境上顯示（轉譯）發佈頁面的日期和時間。必須手動或預先設定的自動複製來發佈頁面。

      >[!NOTE]
      >
      > 有關如何配置相關自動複製的詳細資訊，請參見[開啟和關閉時間——觸發器配置](/help/operations/replication.md#on-and-off-times-trigger-configuration)。

      * 如果[已發佈（手動）](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)，則此頁面將保持休眠（隱藏），直到在指定時間顯示。
      * 如果未發佈，且已針對自動複製設定，則頁面會在指定的時間自動發佈，然後轉譯。
      * 如果未發佈，且未針對自動複製進行設定，則不會自動發佈頁面，因此當嘗試存取頁面時，會看到404。
   * **關閉時間** -與「開啟時間」類似，並常與「開啟時間 ****」搭配使用，這會定義發佈頁面在發佈環境中隱藏的時間。

   * 對於您要立即發佈的頁面，請將這些欄位（**On Time**&#x200B;和&#x200B;**Off Time**）留空，並在發佈環境中使用，直到它們停用（一般情形）為止。


* **虛名 URL**

   * 可讓您輸入此頁面的虛名URL，讓您擁有更短和／或更具表現力的URL。
   * 例如，如果虛名URL設定為`welcome`至網站`http://example.com`的路徑`/v1.0/startpage`所識別的頁面，則`http://example.com/welcome`會是`http://example.com/content/v1.0/startpage`的虛名URL

   >[!CAUTION]
   >
   >虛名 URL:
   >
   >* 必須是唯一的，因此您應該注意該值尚未被其他頁面使用。
   >* 不支援regex圖樣。
   >* 不應設為現有頁面。


   * **新增** -點選或按一下以顯示欄位，以定義頁面的虛名URL。
      * 點選或再按一下以新增多個。
      * 點選或按一下「移除&#x200B;****」圖示，以刪除虛名URL。
   * **重新導向虛名URL** -指出您是否希望頁面使用虛名URL。




### 進階 {#advanced}

* **設定**

   * **語言** -頁面語言
   * **語言根目錄** -如果頁面是語言副本的根目錄，則必須勾選
   * **重新導向** -指出此頁面應自動重新導向至的頁面
   * **Design**  —— 指出在產生的網站的頁面導覽中是否顯示或隱藏頁面
   * **別名** -指定要與此頁一起使用的別名

   >[!NOTE]
   >
   >別名設定`sling:alias`屬性以定義資源的別名（這僅影響資源，不影響路徑）。
   >
   >例如：如果為節點`/content/we-retail/spanish`節點定義了`latin-lang`別名，則可通過`/content/we-retail/latin-language`訪問此頁
   >
   >如需詳細資訊，請參閱「SEO與URL管理最佳實務」下的「本地化頁面名稱」。

   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

* **設定**

   * **雲端設定** -設定的路徑

* **範本設定**

   * **允許的模板** - [定義此子分支中](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) 可用的模板清單

* **驗證需求**

   * **啟用** -啟用驗證以存取頁面

      >[!NOTE]
      >
      >頁面的已關閉使用者群組是在&#x200B;**[Permissions](#permissions)**&#x200B;標籤上定義。

   * **登錄頁** -用於登錄的頁

* **匯出**

   * **導出配置** -指定導出配置

### 縮圖 {#thumbnail}

設定頁面縮圖

* **產生預覽** -產生要當做縮圖使用的頁面預覽
* **上傳影像** -上傳影像以當做縮圖
* **選取影像** -選取現有的資產做為縮圖
* **回復** -對縮圖進行更改後，此選項將變為可用。如果您不想保留變更，可以在儲存前回復該變更。

### 社交媒體 {#social-media}

* **社交媒體分享**

   定義頁面上可用的共用選項。 顯示[共用核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/sharing.html)可用的選項。

   * **啟用Facebook的使用者共用**
   * **啟用Pinterest的使用者共用功能**
   * **偏好的 XF 變數**
      * 定義用於產生頁面中繼資料的體驗片段變數

### 雲端服務 {#cloud-services}

* **Cloud Service配置** -定義雲端服務的屬性

   <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).
  -->

### 個性化 {#personalization}

* **ContextHub 組態**

   * **ContextHub路徑** -定義 [ContextHub組態](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **區段路徑** -定義區段 [路徑](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **定位組態**

   * **品牌** -定義品 [牌以指定定位範圍](/help/sites-cloud/authoring/personalization/targeted-content.md)。
   >[!NOTE]
   >此選項要求使用者帳戶位於`Target Administrators`群組中。

### 權限 {#permissions}

* **權限**

   * 新增權限
   * 編輯已關閉的使用者群組
   * 檢視有效權限

   <!--[Add Permissions](/help/sites-administering/user-group-ac-admin.md) -->

   <!-- [Edit Closed User Group](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)-->

   <!-- View the [Effective Permissions](/help/sites-administering/user-group-ac-admin.md)-->

### Blueprint {#blueprint}

此頁籤僅對用作藍圖的頁面可見。 「Blueprints」（藍圖）作為「Live Copies」（即時副本）的基礎是「[多站點管理」的一部分。](/help/sites-cloud/administering/msm/overview.md)

* **目前的即時副本** -列出以此藍圖頁面為基礎（亦即，即即時副本）的頁面

* **轉出設定** -控制修改傳播至即時副本的情況

### 即時副本 {#live-copy}

* **同步** -將即時副本與Blueprint同步，保留本機修改
* **重設** -將即時副本重設為Blueprint的狀態，移除本機修改
* **暫停** -暫停即時副本以進一步轉出修改
* **分離** -從Blueprint中分離即時副本

* **來源**

   * 顯示此即時副本的Blueprint路徑

* **狀態**

   * 列出頁面的目前即時副本狀態

* **設定**

   * **即時副本繼承** -如果勾選此選項，即時副本配置對所有子項都有效
   * **從父代繼承轉出配置** -如果選中，轉出配置將繼承自頁面的父代
   * **選擇轉出配置** -定義在何種情況下，修改將從Blueprint傳播，並且僅當未選擇從Parentis中繼出配置 **時才可** 用。

## 編輯頁面屬性{#editing-page-properties-1}

* 從&#x200B;**Sites**&#x200B;控制台：
   * [建立新頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) （屬性的子集）
   * 按一下或點選&#x200B;**屬性**
      * 適用於單一頁面
      * 對於多個頁面（只有屬性的子集可供整體編輯）
* 從頁面編輯器：
   * 使用 **頁面資訊** (接著 **開啟屬性**)

### 從站點控制台——單頁{#from-the-sites-console-single-page}

按一下或點選&#x200B;**屬性**&#x200B;以定義頁面屬性：

1. 使用&#x200B;**Sites**&#x200B;控制台，瀏覽至您要檢視和編輯屬性之頁面的位置。
1. 使用下列任一項，為所需頁面選擇&#x200B;**屬性**&#x200B;選項：
   * [快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * 頁面屬性將使用適當的標籤顯示。
1. 視需要檢視或編輯屬性。
1. 然後使用&#x200B;**Save**&#x200B;儲存更新，接著使用&#x200B;**Close**&#x200B;返回主控台。

### 編輯頁面{#when-editing-a-page}時

編輯頁面時，可以使用&#x200B;**頁面資訊**&#x200B;定義頁面屬性：

1. 開啟您要編輯其屬性的頁面。
1. 選擇&#x200B;**頁面資訊**&#x200B;圖示以開啟選擇功能表：
1. 選擇 **開啟屬性** ，將開啟一個對話框，允許您按相應頁籤進行編輯。工具列右側也提供下列按鈕：
   * **取消**
   * **儲存並關閉**
1. 使用&#x200B;**儲存並關閉**&#x200B;按鈕儲存變更。

### 從站點控制台——多頁{#from-the-sites-console-multiple-pages}

從Sites **** Console中，您可以選取數個頁面，然後使用 **View Properties**  (檢視屬性) 來檢視和/或編輯頁面屬性。這稱為頁面屬性的大量編輯。

>[!NOTE]
>
>Assets也提供大量屬性編輯功能。 很相似，但有幾點不同。 如需詳細資訊，請參閱編輯多個資產的屬性。
>
>此外還有「批量編輯器」，可讓您使用GQL（Google查詢語言）從多個頁面搜尋內容，然後在將變更儲存至原始頁面之前，直接在批量編輯器中編輯內容。

<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

您可以選取多個頁面，以透過各種方法進行大量編輯，包括：

* 瀏覽&#x200B;**Sites**&#x200B;控制台時
* 使用&#x200B;**Search**&#x200B;找到一組頁面

選取頁面，然後按一下或點選「屬 **性」選項**，就會顯示大量屬性：

![大量編輯頁面屬性](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

您只能大量編輯下列頁面：

* 共用相同的資源類型
* 不屬於livecopy
   * 如果任何頁面位於即時副本中，則開啟屬性時會顯示訊息。

輸入「批量編輯」後，您可以：

* **檢視**

   * 受影響頁面的清單
      * 您可以視需要選取／取消選取
      * 索引標籤
         * 如同檢視單一頁面的屬性，屬性會排在標籤下。
   * 屬性子集
      * 所有選定頁面上都可用且已明確定義為可用於批量編輯的屬性都可見。
      * 如果您將頁面選擇範圍縮小為一個頁面，則所有屬性都會顯示。
   * 具有公用值的公用屬性
      * 只有具有公用值的屬性才會顯示在「視圖」模式中。
      * 當欄位為多值（例如「標籤」）時，只有&#x200B;*all*&#x200B;是公用的值才會顯示。 如果只有某些是常見的，則只有在編輯時才會顯示。
      * 當不存在具有公用值的屬性時，將顯示一條消息。

* **編輯**

   * 您可以更新可用欄位中的值。
      * 當您選取&#x200B;**Done**&#x200B;時，新值將會套用至所有選取的頁面。
      * 當欄位為多值（例如「標籤」）時，您可以附加新值或移除公用值。
   * 在各個頁面上共有但值不同的欄位，會以特殊值（例如文字`<Mixed Entries>`）來標示。 編輯此類欄位時應格外小心，以避免資料遺失。

>[!NOTE]
>
>頁面元件可設定為指定可進行大量編輯的欄位。 請參閱設定您的頁面以大量編輯頁面屬性。

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
