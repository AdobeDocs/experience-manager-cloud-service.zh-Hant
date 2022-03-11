---
title: 編輯頁面屬性
description: 定義頁面的必需屬性
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: e51490a9422dab3cc4980eb1d2288d7c264343be
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 8%

---

# 編輯頁面屬性 {#editing-page-properties}

您可以定義頁面的必需屬性。 這些內容可能因頁面的性質而異。 例如，某些頁面可能已連接到即時拷貝，而其他頁面則未連接，並且即時拷貝資訊將根據需要可用。

## 頁面內容 {#page-properties}

屬性分佈在多個頁籤上。

### 基本 {#basic}

* **標題和標籤**

   * **標題**  — 頁面標題顯示在不同位置。 例如， **網站** 清單和 **站點** 卡/清單視圖。
      * 這是必要欄位。
   * **標籤**  — 在此，您可以通過更新選擇框中的清單來添加標籤，或從頁面中刪除標籤。
      * 選擇標籤後，它將列在選擇框下。 可以使用x從此清單中刪除標籤。
      * 可以通過在空選擇框中鍵入名稱來輸入完全新的標籤。
         * 當您按Enter時，將建立新標籤。
         * 然後，新標籤將在右側顯示，右側有一個小星號，表示它是新標籤。
      * 使用下拉功能，您可以從現有標籤中進行選擇。
      * 將滑鼠移到選擇框中的標籤條目上時，將顯示x，該標籤可用於刪除此頁的標籤。
      * 有關標籤的詳細資訊，請參見 [使用標籤](/help/sites-cloud/authoring/features/tags.md)。
   * **在導航中隱藏**  — 指示頁面是顯示還是隱藏在結果站點的頁面導航中。

* **品牌化**

   通過在每個頁面標題上附加一個品牌輔助資訊，跨頁面應用一致的品牌標識。 此功能需要使用2.14.0版或更高版本的頁面元件 [核心元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)

   * **覆蓋**  — 選中以定義此頁上的品牌輔助資訊。
      * 值將由任何子頁繼承，除非它們還有 **覆蓋** 值集。
   * **覆蓋值**  — 要附加到頁面標題的品牌輔助資訊的文本。
      * 該值將附加在管道字元（如「循環托斯卡納」）之後的頁標題中 |始終為WKND做好準備&quot;

* **HTML ID**

   * **ID**  — 要應用到元件的HTMLID。

* **更多標題和說明**

   * **頁面標題**  — 要在頁面上使用的標題。 通常由標題元件使用。 如果空 **標題** 的下界。
   * **導航標題**  — 可以指定一個單獨的標題以在導航中使用（例如，如果希望更簡潔一些）。 如果為空，則 **標題** 的下界。
   * **副標題**  — 用於頁面上的副標題。
   * **說明**  — 您對頁面、其用途或要添加的任何其他詳細資訊的說明。

* **開啟/關閉時間**

   >[!NOTE]
   >
   > 請參閱 [開啟和關閉時間 — 觸發器配置](/help/operations/replication.md#on-and-off-times-trigger-configuration) 有關如何配置相關自動複製的詳細資訊。

   >[!NOTE]
   >如果 **準時** 或 **關機時間** 過去，並且配置了自動複製，則將立即觸發相關操作。

   * **準時**  — 發佈環境上使發佈頁面可見（呈現）的日期和時間。 必須手動或通過預配置的自動複製發佈該頁。

      * 如果已 [已發佈（手動）](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) 此頁面將保持休眠（隱藏）狀態，直到在指定時間呈現。
      * 如果未發佈並配置為自動複製，則將在指定時間自動發佈並呈現該頁。
      * 如果未發佈，並且未配置為自動複製，則不會自動發佈該頁，因此當嘗試訪問該頁時，將看到404。
   * **關機時間**  — 類似於 **準時**，這定義發佈頁面在發佈環境中隱藏的時間。

   * 保留這些欄位(**準時** 和 **關機時間**)為空，用於要立即發佈的頁面，並且在發佈環境中可用，直到它們被停用（通常情況）。


* **虛名 URL**

   * 允許您為此頁面輸入虛榮URL，這可以使您具有更短和/或更豐富的URL。
   * 例如，如果Vanity URL設定為 `welcome` 到路徑標識的頁面 `/v1.0/startpage` 的 `http://example.com`，則 `http://example.com/welcome` 將是 `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虛名 URL:
   >
   >* 必須唯一，因此您應該注意該值尚未被其他頁面使用。
   >* 不支援regex模式。
   >* 不應設定為現有頁。


   * **添加**  — 點擊或按一下顯示欄位以定義頁面的虛榮URL。
      * 點擊或再次按一下以添加多個。
      * 點擊或按一下 **刪除** 表徵圖。
   * **重定向虛榮URL**  — 指示是否希望頁面使用虛榮URL。


### 進階 {#advanced}

* **設定**

   * **語言**  — 頁面語言
   * **語言根**  — 如果頁面是語言副本的根，則必須選中
   * **重定向**  — 指示此頁應自動重定向到的頁
   * **設計**  — 指示頁面是在生成站點的頁面導航中顯示還是隱藏
   * **別名**  — 指定要與此頁一起使用的別名
      * 例如，如果定義的別名 `private` 頁 `/content/wknd/us/en/magazine/members-only`，此頁也可通過 `/content/wknd/us/en/magazine/private`
      * 建立別名集 `sling:alias` 頁節點上的屬性，它只影響資源，而不影響儲存庫路徑。
      * 無法發佈編輯器中別名訪問的頁面。 [發佈選項](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) 編輯器中的頁面僅可用於通過實際路徑訪問的頁面。

   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

* **設定**

   * **雲配置**  — 配置路徑

* **模板設定**

   * **允許的模板** - [定義可用模板清單](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) 在這個支行內

* **驗證需求**

   * **啟用**  — 啟用身份驗證以訪問頁面

      >[!NOTE]
      >
      >在 **[權限](#permissions)** 頁籤。

   * **登錄頁**  — 用於登錄的頁面

* **匯出**

   * **導出配置**  — 指定導出配置

### 縮圖 {#thumbnail}

配置頁面縮略圖

* **生成預覽**  — 生成要用作縮略圖的頁面預覽
* **上載映像**  — 上載影像以用作縮略圖
* **選擇影像**  — 選擇要用作縮略圖的現有資產
* **還原**  — 更改縮略圖後，此選項將可用。 如果您不想保留更改，則可以在保存之前還原該更改。

### 社交媒體 {#social-media}

* **社交媒體分享**

   定義頁面上可用的共用選項。 顯示可供 [共用核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/sharing.html)。

   * **為Facebook啟用用戶共用**
   * **為Pinterest啟用用戶共用**
   * **偏好的 XF 變數**
      * 定義用於為頁生成元資料的經驗片段變體

### 雲端服務 {#cloud-services}

* **Cloud Service配置**  — 定義雲服務的屬性

   <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).
  -->

### 個性化 {#personalization}

* **ContextHub 組態**

   * **上下文中心路徑**  — 定義 [ContextHub配置](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **段路徑**  — 定義 [段路徑](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **定位組態**

   * **品牌**  — 定義 [要指定目標範圍的品牌](/help/sites-cloud/authoring/personalization/targeted-content.md)。
   >[!NOTE]
   >此選項要求用戶帳戶位於 `Target Administrators`組。

### 權限 {#permissions}

* **權限**

   * 新增權限
   * 編輯已關閉的使用者群組
   * 查看有效權限

   <!--[Add Permissions](/help/sites-administering/user-group-ac-admin.md) -->

   <!-- [Edit Closed User Group](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)-->

   <!-- View the [Effective Permissions](/help/sites-administering/user-group-ac-admin.md)-->

### Blueprint {#blueprint}

此頁籤僅對用作藍圖的頁面可見。 藍圖作為即時拷貝的基礎是 [多站點管理。](/help/sites-cloud/administering/msm/overview.md)

* **當前即時拷貝**  — 列出基於（即此藍圖的即時副本）此藍圖頁面的頁面

* **部署配置**  — 控制將修改傳播到即時副本的情況

### 即時副本 {#live-copy}

* **同步**  — 將即時拷貝與藍圖同步，保留本地修改
* **重置**  — 將即時拷貝重置為藍圖狀態，刪除本地修改
* **掛起**  — 通過進一步的部署修改暫停即時拷貝
* **分離**  — 從藍圖中分離即時副本

* **來源**

   * 顯示此即時副本的藍圖路徑

* **狀態**

   * 列出頁面的當前即時複製狀態

* **設定**

   * **即時複製繼承**  — 如果選中，則Live Copy配置對所有子項都有效
   * **從父代繼承部署配置**  — 如果選中，則從頁面的父級繼承展開配置
   * **選擇「推廣配置」**  — 定義修改將從藍圖傳播的情形，並且僅當 **從父代繼承部署配置** 未選擇

### 預覽 {#preview}

啟用預覽環境後，您將看到：

* 預覽URL — 用於訪問預覽環境中內容的URL

## 編輯頁面屬性 {#editing-page-properties-1}

* 從 **站點** 控制台：
   * [建立新頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) （屬性的子集）
   * 按一下或輕擊 **屬性**
      * 單頁
      * 對於多頁（僅屬性的子集可用於成批編輯）
* 從頁面編輯器：
   * 使用 **頁面資訊** (接著 **開啟屬性**)

### 從站點控制台 — 單頁 {#from-the-sites-console-single-page}

按一下或輕擊 **屬性** 要定義頁面屬性，請執行以下操作：

1. 使用 **站點** 控制台，導航到要查看和編輯其屬性的頁的位置。
1. 選擇 **屬性** 選項：
   * [快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * 頁面屬性將使用相應的頁籤顯示。
1. 根據需要查看或編輯屬性。
1. 然後使用 **保存** 保存更新，然後 **關閉** 返回控制台。

### 編輯頁面時 {#when-editing-a-page}

編輯頁面時，您可以使用 **頁面資訊** 要定義頁面屬性，請執行以下操作：

1. 開啟要編輯其屬性的頁面。
1. 選擇 **頁面資訊** 表徵圖以開啟選擇菜單：
1. 選擇 **開啟屬性** ，將開啟一個對話框，允許您按相應頁籤進行編輯。工具列右側也提供下列按鈕：
   * **取消**
   * **儲存並關閉**
1. 使用 **保存並關閉** 按鈕。

### 從站點控制台 — 多頁 {#from-the-sites-console-multiple-pages}

從Sites **** Console中，您可以選取數個頁面，然後使用 **View Properties**  (檢視屬性) 來檢視和/或編輯頁面屬性。這稱為頁面屬性的大量編輯。

>[!NOTE]
>
>對「資產」也可進行屬性的批量編輯。 它非常相似，但有幾點不同。 有關詳細資訊，請參閱編輯多個資產的屬性。
>
>還有批量編輯器，它允許您使用GQL(Google查詢語言)從多個頁面搜索內容，然後直接在批量編輯器中編輯內容，然後再將更改保存到原始頁面。

<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

可以通過各種方法選擇多個頁面進行批量編輯，包括：

* 瀏覽 **站點** 控制台
* 使用後 **搜索** 查找一組頁面

選取頁面，然後按一下或點選「屬 **性」選項**，就會顯示大量屬性：

![批量編輯頁面屬性](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

您只能批量編輯以下頁面：

* 共用相同的資源類型
* 不是livecopy的一部分
   * 如果其中任何頁面都在即時副本中，則開啟屬性時將顯示一條消息。

輸入「批量編輯」後，您可以：

* **檢視**

   * 受影響的頁面清單
      * 如果需要，可以選擇/取消選擇
      * 索引標籤
         * 與查看單頁的屬性一樣，屬性在頁籤下排序。
   * 屬性子集
      * 所有選定頁面上都可用且已明確定義為可用於批量編輯的屬性是可見的。
      * 如果將頁面選擇縮小為一頁，則所有屬性都可見。
   * 具有公用值的公用屬性
      * 在「視圖」模式下，只顯示具有公用值的屬性。
      * 當欄位為多值（例如「標籤」）時，僅在 *全部* 很常見。 如果只有一些是常見的，則只有在編輯時才顯示。
      * 如果不存在具有公用值的屬性，則顯示一條消息。

* **編輯**

   * 您可以更新可用欄位中的值。
      * 當您選擇時，新值將應用於所有選定的頁面 **完成**。
      * 當欄位為多值（例如「標籤」）時，可以追加新值或刪除公用值。
   * 通用但各頁具有不同值的欄位將用特殊值（如文本）來表示 `<Mixed Entries>`。 編輯此類欄位時應當注意防止資料丟失。

>[!NOTE]
>
>可以將頁面元件配置為指定可用於批量編輯的欄位。 請參閱配置頁面以批量編輯頁面屬性。

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
