---
title: 編輯頁面屬性
description: 定義頁面的必要屬性
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: 34247d8de3dc1a243eaac152b1d2036f9c237303
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 8%

---

# 編輯頁面屬性 {#editing-page-properties}

您可以定義頁面的必要屬性。 這些項目可能會因頁面性質而異。 例如，某些頁面可能連線至即時副本，而其他頁面則未連線，且即時副本資訊將可視情況提供。

## 頁面內容 {#page-properties}

屬性分佈在多個索引標籤之間。

### 基本 {#basic}

* **標題與標籤**

   * **標題**  — 頁面標題會顯示在不同位置。例如， **Websites**&#x200B;索引標籤清單和&#x200B;**Sites**&#x200B;卡片/清單檢視。
      * 這是必要欄位。
   * **標籤**  — 您可以在此更新選取方塊中的清單，以從頁面新增或移除標籤。
      * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
      * 您可以在空白的選取方塊中輸入名稱，以輸入全新的標籤。
         * 當您點擊Enter時，將會建立新標籤。
         * 接著，新標籤會在右側以小星號顯示，指出為新標籤。
      * 透過下拉式功能，您可以從現有標籤中選取。
      * 將滑鼠移至選取方塊中的標籤項目上時，會顯示x，可用來移除此頁面的標籤。
      * 如需標籤的詳細資訊，請參閱[使用標籤](/help/sites-cloud/authoring/features/tags.md)。
   * **在導覽中隱藏**  — 指出頁面在所產生網站的頁面導覽中是否顯示或隱藏。

* **品牌化**

   在每個頁面標題附加品牌概要資訊，借此在頁面間套用一致的品牌識別。 若要使用此功能，需使用2.14.0版或更新版本的[核心元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)

   * **覆寫**  — 勾選以定義此頁面上的品牌概要資訊。
      * 值將由任何子頁繼承，除非它們也設定了其&#x200B;**Override**&#x200B;值。
   * **覆寫值**  — 要附加至頁面標題的品牌概要文字。
      * 此值會附加在垂直號字元（如「循環托斯卡納」）之後的頁面標題 |始終為WKND做好準備&quot;

* **HTML ID**

   * **ID**  — 套用至元件的HTML ID。

* **更多標題和說明**

   * **頁面標題**  — 用於頁面的標題。通常用於標題元件。 如果空白，則將使用&#x200B;**Title**。
   * **導覽標題**  — 您可以指定個別標題以用於導覽（例如，如果您想要更精簡的標題）。如果空白，則將使用&#x200B;**Title**。
   * **副標題**  — 用於頁面上的副標題。
   * **說明**  — 您對頁面、其用途或您要新增的任何其他詳細資訊的說明。

* **開啟/關閉時間**

   >[!NOTE]
   >
   > 有關如何配置相關自動複製的詳細資訊，請參閱[開啟和關閉時間 — 觸發配置](/help/operations/replication.md#on-and-off-times-trigger-configuration)。

   >[!NOTE]
   >如果&#x200B;**On Time**&#x200B;或&#x200B;**Off Time**&#x200B;過去，且已設定自動復寫，則會立即觸發相關動作。

   * **時間**  — 在發佈環境中顯示（轉譯）已發佈頁面的日期和時間。必須手動或預先設定的自動復寫來發佈頁面。

      * 如果已發佈[（手動）](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)此頁面將保持休眠（隱藏），直到在指定時間呈現為止。
      * 如果未發佈並已針對自動復寫進行設定，則頁面將在指定時間自動發佈並呈現。
      * 如果未發佈且未針對自動復寫進行設定，則不會自動發佈頁面，因此在嘗試存取頁面時，會看到404。
   * **關閉時間**  — 此選項與經常搭配使用的 **開啟時間**&#x200B;類似，可定義發佈頁面在發佈環境中隱藏的時間。

   * 對於您要立即發佈的頁面，請將這些欄位（**On Time**&#x200B;和&#x200B;**Off Time**）保留空白，並在發佈環境中可用，直到停用為止（一般情況）。


* **虛名 URL**

   * 可讓您輸入此頁面的虛名URL，以便您擁有較短和/或更具表達力的URL。
   * 例如，如果虛名URL設為`/v1.0/startpage`，且以網站`http://example.com`的路徑`welcome`所識別的頁面，則`http://example.com/welcome`會是`http://example.com/content/v1.0/startpage`的虛名URL

   >[!CAUTION]
   >
   >虛名 URL:
   >
   >* 必須是唯一的，因此您應注意，值尚未被其他頁面使用。
   >* 不支援規則運算式模式。
   >* 不應設為現有頁面。


   * **新增**  — 點選或按一下以顯示欄位，以定義頁面的虛名URL。
      * 點選或再按一下以新增多個。
      * 點選或按一下&#x200B;**移除**&#x200B;圖示以刪除虛名URL。
   * **重新導向虛名URL**  — 指出您是否希望頁面使用虛名URL。


### 進階 {#advanced}

* **設定**

   * **語言**  — 頁面語言
   * **語言根**  — 如果頁面是語言副本的根，則必須勾選
   * **重新導向**  — 指出此頁面應自動重新導向的頁面
   * **設計**  — 指出頁面在所產生網站的頁面導覽中是否顯示或隱藏
   * **別名**  — 指定要與此頁一起使用的別名

   >[!NOTE]
   >
   >別名設定`sling:alias`屬性以定義資源的別名（這只會影響資源，而非路徑）。
   >
   >例如：如果為節點`/content/we-retail/spanish`定義別名`latin-lang`，則可通過`/content/we-retail/latin-language`訪問此頁
   >
   >如需詳細資訊，請參閱SEO和URL管理最佳實務底下的本地化頁面名稱。

   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

* **設定**

   * **雲端設定**  — 設定的路徑

* **範本設定**

   * **允許的範本**  -  [定義此子分支](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) 中可用的範本清單

* **驗證需求**

   * **啟用**  — 啟用驗證以存取頁面

      >[!NOTE]
      >
      >頁面的封閉使用者群組是在&#x200B;**[Permissions](#permissions)**&#x200B;標籤上定義。

   * **登入頁面**  — 用於登入的頁面

* **匯出**

   * **導出配置**  — 指定導出配置

### 縮圖 {#thumbnail}

設定頁面縮圖

* **產生預覽**  — 產生頁面預覽以作為縮圖
* **上傳影像**  — 上傳影像以作為縮圖
* **選取影像**  — 選取現有資產作為縮圖
* **回復**  — 在您對縮圖進行變更後，即可使用此選項。如果您不想保留變更，可以在儲存前還原該變更。

### 社交媒體 {#social-media}

* **社交媒體分享**

   定義頁面上可用的共用選項。 顯示[共用核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/sharing.html)的可用選項。

   * **啟用Facebook的使用者共用**
   * **啟用Pinterest的使用者共用**
   * **偏好的 XF 變數**
      * 定義用於產生頁面中繼資料的體驗片段變數

### 雲端服務 {#cloud-services}

* **Cloud Service設定**  — 定義雲端服務的屬性

   <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).
  -->

### 個性化 {#personalization}

* **ContextHub 組態**

   * **ContextHub路徑**  — 定義ContextHub [設定](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **區段路徑**  — 定義區 [段路徑](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **定位組態**

   * **品牌**  — 定義 [品牌以指定目標定位範圍](/help/sites-cloud/authoring/personalization/targeted-content.md)。
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

此頁簽僅對用作藍圖的頁面可見。 Blueprint作為Live Copy的基礎是[多站點管理的一部分。](/help/sites-cloud/administering/msm/overview.md)

* **目前的即時** 副本 — 列出以此Blueprint頁面為基礎（即為的即時副本）的頁面

* **轉出設定**  — 控制修改將傳播至即時副本的情況

### 即時副本 {#live-copy}

* **同步**  — 將Live Copy與Blueprint同步，保留本機修改
* **重設**  — 將即時副本重設為Blueprint的狀態，移除本機修改
* **暫停**  — 暫停即時副本以進一步轉出修改
* **分離**  — 從Blueprint分離即時副本

* **來源**

   * 顯示此即時副本的Blueprint路徑

* **狀態**

   * 列出頁面的目前即時副本狀態

* **設定**

   * **即時副本繼承**  — 如果勾選此選項，即時副本設定對所有子項都有效
   * **從父項繼承轉出設定**  — 如果勾選此選項，則轉出設定繼承自頁面的父項
   * **選擇轉出設定**  — 定義將從Blueprint傳播修改的情況，且僅當未選取從Parentis繼承轉出 **設定時** 可用

### 預覽 {#preview}

「預覽」環境啟用後，您會看到：

* 預覽URL — 用於存取預覽環境中內容的URL

## 編輯頁面屬性 {#editing-page-properties-1}

* 從&#x200B;**Sites**&#x200B;控制台：
   * [建立新頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) （屬性的子集）
   * 按一下或點選&#x200B;**屬性**
      * 針對單一頁面
      * 對於多個頁面（只有屬性的子集可供集體編輯）
* 從頁面編輯器：
   * 使用 **頁面資訊** (接著 **開啟屬性**)

### 從Sites Console — 單頁 {#from-the-sites-console-single-page}

按一下或點選&#x200B;**屬性**&#x200B;以定義頁面屬性：

1. 使用&#x200B;**Sites**&#x200B;控制台，導覽至您要檢視及編輯屬性之頁面的位置。
1. 使用下列任一項，為所需頁面選取&#x200B;**屬性**&#x200B;選項：
   * [快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * 頁面屬性將會使用適當的標籤來顯示。
1. 視需要檢視或編輯屬性。
1. 然後使用&#x200B;**Save**&#x200B;保存更新，然後使用&#x200B;**Close**&#x200B;返回控制台。

### 編輯頁面時 {#when-editing-a-page}

編輯頁面時，您可以使用&#x200B;**頁面資訊**&#x200B;來定義頁面屬性：

1. 開啟要編輯其屬性的頁面。
1. 選擇&#x200B;**頁面資訊**&#x200B;表徵圖以開啟選擇菜單：
1. 選擇 **開啟屬性** ，將開啟一個對話框，允許您按相應頁籤進行編輯。工具列右側也提供下列按鈕：
   * **取消**
   * **儲存並關閉**
1. 使用&#x200B;**儲存並關閉**&#x200B;按鈕來儲存變更。

### 從Sites Console — 多個頁面 {#from-the-sites-console-multiple-pages}

從Sites **** Console中，您可以選取數個頁面，然後使用 **View Properties**  (檢視屬性) 來檢視和/或編輯頁面屬性。這稱為頁面屬性的大量編輯。

>[!NOTE]
>
>資產也提供大量屬性編輯功能。 這非常相似，但有幾點不同。 如需詳細資訊，請參閱編輯多個資產的屬性。
>
>還有批量編輯器，它允許您使用GQL（Google查詢語言）從多個頁面搜索內容，然後直接在批量編輯器中編輯內容，然後將更改保存到原始頁面。

<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

您可以選取多個頁面，以透過各種方法進行大量編輯，包括：

* 瀏覽&#x200B;**Sites**&#x200B;主控台時
* 使用&#x200B;**Search**&#x200B;找出一組頁面後

選取頁面，然後按一下或點選「屬 **性」選項**，就會顯示大量屬性：

![大量編輯頁面屬性](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

您只能批量編輯以下頁面：

* 共用相同的資源類型
* 不屬於LiveCopy
   * 如果任何頁面位於即時副本中，則在開啟屬性時會顯示訊息。

輸入「大量編輯」後，您可以：

* **檢視**

   * 受影響頁面的清單
      * 您可以視需要選取/取消選取
      * 索引標籤
         * 如同檢視單一頁面的屬性時，屬性會依索引標籤排序。
   * 屬性的子集
      * 所有選取頁面上皆可使用，且明確定義為可用於大量編輯的屬性，則會顯示。
      * 如果您將頁面選取範圍縮小為一個頁面，則所有屬性都會顯示。
   * 具有公用值的公用屬性
      * 「視圖」模式中只顯示具有公共值的屬性。
      * 當欄位為多值時（例如「標籤」），只有&#x200B;*all*&#x200B;為共同值時才會顯示值。 如果只有部分是常見的，則只會在編輯時顯示。
      * 當不存在具有公用值的屬性時，將顯示一條消息。

* **編輯**

   * 您可以更新可用欄位中的值。
      * 當您選取&#x200B;**Done**&#x200B;時，新值將套用至所有選取的頁面。
      * 當欄位為多值時（例如「標籤」），您可以附加新值或移除通用值。
   * 在不同頁面上共有但值不同的欄位，將會以特殊值（例如文字`<Mixed Entries>`）表示。 編輯此類欄位時應謹慎處理，以防止資料遺失。

>[!NOTE]
>
>頁面元件可設定為指定可用於大量編輯的欄位。 請參閱設定頁面以大量編輯頁面屬性。

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
