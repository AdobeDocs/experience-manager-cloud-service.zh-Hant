---
title: 管理內容片段
description: 瞭解如何使用內容片段控制檯來管理您的AEM內容片段；用於頁面製作，或作為Headless內容的基礎。
feature: Content Fragments
role: User
exl-id: fc4497cb-85ac-4d2d-aca4-588541266f0b
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2051'
ht-degree: 2%

---

# 管理內容片段 {#managing-content-fragments}

瞭解如何使用 **內容片段** 主控台以管理您的AEM內容片段。 這些可用於頁面製作，或作為Headless內容的基礎。

定義您的 [內容片段模型](#creating-a-content-model) 您可以使用這些來 [建立您的內容片段](#creating-a-content-fragment).

此 [內容片段編輯器](#opening-the-fragment-editor) 提供各種 [模式](#modes-in-the-content-fragment-editor) 若要讓您：

* [編輯內容](#editing-the-content-of-your-fragment) 和 [管理變數](#creating-and-managing-variations-within-your-fragment)
* [為片段加上註釋](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [將內容與片段相關聯](#associating-content-with-your-fragment)
* [設定中繼資料](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [檢視結構樹](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md)
* [預覽JSON表示法](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>可以使用內容片段：
>
>* 編寫頁面時；請參閱 [使用內容片段編寫頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* 的 [搭配GraphQL使用內容片段的Headless內容傳送](/help/sites-cloud/administering/content-fragments/content-fragments-graphql.md).

>[!NOTE]
>
>內容片段儲存為 **資產**. 主要受下列專案管理： **內容片段** 主控台，但也可從 [資產](/help/assets/content-fragments/content-fragments-managing.md) 主控台。

## 內容片段主控台 {#content-fragments-console}

內容片段控制檯提供對片段和相關工作的直接存取。 如需進一步的詳細資訊，請參閱：

* [內容片段主控台的基本結構和處理](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#basic-structure-handling-content-fragments-console)

* [提供的有關您的內容片段的資訊](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#information-content-fragments)

* [內容片段控制檯中內容片段的動作](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#actions-selected-content-fragment)

* [自訂內容片段控制檯中可用的欄](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#select-available-columns)

* [在內容片段控制檯中搜尋和篩選](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#filtering-fragments)

## 建立內容片段 {#creating-content-fragments}

### 建立內容模型 {#creating-a-content-model}

[內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) 可以在使用結構化內容建立內容片段之前啟用和建立。

### 建立內容片段 {#creating-a-content-fragment}

若要建立內容片段：

1. 從 **內容片段** 主控台，選取 **建立** （右上方）。

   >[!NOTE]
   >
   >要預先定義新片段的位置，您可以導航到要建立片段的資料夾，也可以在建立過程中指定位置。

1. 此 **新內容片段** 對話方塊將會開啟，您可以從此處指定：

   * **位置**  — 使用目前位置自動完成，但您可以視需要選取其他位置
   * **內容片段模型**  — 從下拉式清單中選取要作為片段基礎的模式
   * **標題**
   * **名稱**  — 根據 **標題**，但如有需要，可加以編輯
   * **說明**

   ![新內容片段對話方塊](assets/cfm-managing-new-cf-01.png)

1. 選取 **建立**，或 **建立並開啟** 以保留您的定義。

## 內容片段的狀態 {#statuses-content-fragments}

內容片段在存在期間可以有數個狀態，如所示 [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)：

* **新增**
已建立新的內容片段，但從未在內容片段編輯器中編輯或開啟。
* **草稿**
有人在內容片段編輯器中編輯或開啟（新）內容片段 — 但尚未發佈。
* **已發佈**
內容片段已發佈。
* **已修改**
內容片段在發佈後（但在發佈修改之前）已進行編輯。
* **已取消發佈**
已取消發佈內容片段。

## 開啟片段編輯器 {#opening-the-fragment-editor}

若要開啟片段進行編輯：

>[!CAUTION]
>
>若要編輯內容片段，您需要 [適當的許可權](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 如果您遇到問題，請聯絡您的系統管理員。

1. 使用 **內容片段** 控制檯以導覽至您的內容片段位置。
1. 開啟片段進行編輯，方法是選取片段，然後 **開啟** 工具列中的。

1. 片段編輯器將會開啟。 視需要進行變更：

   ![片段編輯器](assets/cfm-managing-03.png)

1. 進行變更後，請使用 **儲存**， **儲存並關閉** 或 **關閉** 視需要。

   >[!NOTE]
   >
   >**儲存並關閉** 可透過 **儲存** 下拉式清單。

   >[!NOTE]
   >
   >兩者 **儲存並關閉** 和 **關閉** 將退出編輯器 — 請參閱 [儲存、關閉和版本](#save-close-and-versions) 以取得有關各種選項如何為內容片段運作的完整資訊。

## 內容片段編輯器中的模式和動作 {#modes-actions-content-fragment-editor}

內容片段編輯器提供各種模式和動作。

### 內容片段編輯器中的模式 {#modes-in-the-content-fragment-editor}

使用側面板中的圖示導覽各種模式：

* 變數： [編輯內容](#editing-the-content-of-your-fragment) 和 [管理您的變數](#creating-and-managing-variations-within-your-fragment)

* [註解](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [相關聯的內容](#associating-content-with-your-fragment)
* [中繼資料](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [樹狀結構](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md)
* [預覽](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)

![模式](assets/cfm-managing-04.png)

### 內容片段編輯器中的工具列動作 {#toolbar-actions-in-the-content-fragment-editor}

頂端工具列中的某些功能可以從多種模式使用：

![模式](assets/cfm-managing-top-toolbar.png)

* 當內容頁面上已參考片段時，會顯示訊息。 您可以 **關閉** 訊息。

* 您可以使用來隱藏/顯示側面板 **切換側面板** 圖示。

* 在片段名稱下方，您可以看到 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) 用於建立目前的片段：

   * 此名稱也是將開啟模型編輯器的連結。

* 檢視片段的狀態；例如，建立、修改或發佈時間的相關資訊。 狀態也以色彩標示：

   * **新增**：灰色
   * **草稿**：藍色
   * **已發佈**：綠色
   * **已修改**：橙色
   * **已停用**：紅色

* **儲存** 提供對的存取 **儲存並關閉** 選項。

* 三個點(**...**)下拉式清單提供其他動作的存取權：
   * **更新頁面參考**
      * 這會更新任何頁面引用。
   * **[快速發佈](/help/assets/manage-publication.md#quick-publish)**
   * **[管理發佈](/help/assets/manage-publication.md#manage-publication)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## 儲存、關閉和版本 {#save-close-and-versions}

>[!NOTE]
>
>版本也可為 [從時間軸建立、比較和還原](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

編輯器有各種選項：

* **儲存** 和 **儲存並關閉**

   * **儲存** 會儲存最新變更並保留在編輯器中。
   * **儲存並關閉** 將會儲存最新變更並退出編輯器。

  >[!CAUTION]
  >
  >若要編輯內容片段，您需要 [適當的許可權](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 如果您遇到問題，請聯絡您的系統管理員。

  >[!NOTE]
  >
  >在儲存之前，您可以保留在編輯器中進行一系列變更。

  >[!CAUTION]
  >
  >除了僅儲存您的變更，這些動作也會更新任何參考，並確保Dispatcher會依需求排清。 這些變更可能需要一些時間才能處理。 因此，大型/複雜/過載系統可能會受到效能影響。
  >
  >使用時，請記住此程式時間 **儲存並關閉**，然後快速重新輸入片段編輯器以進行並儲存進一步的變更。

* **關閉**

  將退出編輯器，而不儲存最新變更（即自上次更新以來進行的變更） **儲存**)。

在編輯您的內容片段時，AEM會自動建立版本，以確保如果您取消變更(使用 **關閉** 而不儲存)：

1. 開啟內容片段以編輯AEM時，會檢查是否存在Cookie型權杖並指出 *編輯工作階段* 存在：

   1. 如果找到Token，則會將片段視為現有編輯工作階段的一部分。
   2. 如果代號為 *非* 可使用且使用者開始編輯內容，接著會建立版本，並將此新編輯工作階段的Token傳送至使用者端，並儲存在Cookie中。

2. 當有 *主要* 編輯工作階段，正在編輯的內容每600秒自動儲存一次（預設）。

   >[!NOTE]
   >
   >自動儲存間隔可使用以下設定 `/conf` 機制。
   >
   >預設值，請參閱：
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果使用者取消編輯，則會還原在編輯工作階段開始時建立的版本，並移除Token以結束編輯工作階段。
4. 如果使用者選擇 **儲存** 會保留編輯、更新的元素/變數並移除Token以結束編輯工作階段。

## 編輯片段的內容 {#editing-the-content-of-your-fragment}

開啟片段後，您可以使用 [變數](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) 標籤以編寫您的內容。

## 建立和管理片段中的變數 {#creating-and-managing-variations-within-your-fragment}

建立主要內容後，您就可以建立和管理 [變數](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) 內容的。

## 將內容與片段建立關聯 {#associating-content-with-your-fragment}

您也可以 [關聯內容](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) 含片段。 這提供了連線，以便在將資產（即影像）新增到內容頁面時，可以（選擇性）與片段搭配使用。

## 檢視和編輯片段的中繼資料（屬性） {#viewing-and-editing-the-metadata-properties-of-your-fragment}

您可以使用檢視和編輯片段的屬性。 [中繼資料](/help/sites-cloud/administering/content-fragments/content-fragments-metadata.md) 標籤。

## 發佈和預覽片段 {#publishing-and-previewing-a-fragment}

您可以將內容片段發佈至：

* 此 **[發佈服務](/help/overview/architecture.md#runtime-architecture)**  — 完整公開存取

* 此 **[預覽服務](/help/overview/architecture.md#runtime-architecture)**  — 在完整可用之前預覽內容

  >[!CAUTION]
  >
  發佈內容片段至 **預覽服務** 只能從 [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)；使用 **發佈** 動作。

  >[!NOTE]
  >
  如需有關預覽環境的詳細資訊，請參閱：
  >
  * [管理環境](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)
  * [設定預覽階層的 OSGi 設定](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#configuring-osgi-settings-for-the-preview-tier)
  * [使用 Developer Console 偵錯預覽](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#debugging-preview-using-the-developer-console)

若要使用發佈您的內容片段 **發佈** 工具列中的選項 [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#actions-selected-content-fragment)：

>[!CAUTION]
>
如果您的片段以模型為基礎，則您應確保 [模型已發佈](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
如果您發佈的內容片段尚未發佈模型，選擇清單會指出這一點，模型會與片段一起發佈。

1. 從清單中選取一個或多個片段。

1. 從工具列中選取 **發佈** 然後執行下列任一項以開啟適當的對話方塊：

   * **現在**  — 選取 **發佈服務**，或 **預覽服務**；確認後，片段會立即發佈
   * **排程**  — 除了必要的服務之外，您還可以選擇片段發佈的日期和時間

   必要時，您必須指定要發佈的參照。 依預設，參考資料也會發佈到預覽服務，以確保內容中沒有中斷。
例如，對於已排程的發佈請求：
   ![發佈對話方塊](assets/cfm-publish-01.png)

1. 確認發佈動作。

您也可以發佈至 **發佈服務** 從 [內容片段編輯器](#toolbar-actions-in-the-content-fragment-editor) 使用：
* **快速發佈**
* **管理發佈**

>[!NOTE]
>
在您之後 [發佈使用片段的頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing)，片段會列在頁面參考中。

>[!CAUTION]
>
片段發佈、參考或兩者皆完成後，當作者再次開啟片段進行編輯時，AEM會顯示警告。 系統會警告作者，片段的變更也會影響參照的頁面。

## 取消發佈片段 {#unpublishing-a-fragment}

若要取消發佈內容片段，請選取一或多個片段，然後 **取消發佈** (在的 [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#actions-selected-content-fragment). 您可以選取 **現在** 或 **已排程**.

當相關對話方塊開啟時，您可以選取適當的服務：
![取消發佈對話方塊](assets/cfm-unpublish-01.png)

>[!NOTE]
>
此 **取消發佈** 動作僅在已發佈的片段可用時可見。

>[!CAUTION]
>
如果片段已從其他片段或頁面引用，您將看到警告訊息，並需要確認您要繼續。

## 刪除片段 {#deleting-a-fragment}

若要刪除片段：

1. 在 **內容片段** 主控台導覽至內容片段的位置。
2. 選取片段。

   >[!NOTE]
   >
   此 **刪除** 動作無法當作快速動作使用。

3. 選取 **刪除** 工具列中的。
4. 確認 **刪除** 動作。

   >[!CAUTION]
   >
   如果片段已從其他片段或頁面引用，您將看到警告訊息，並需要確認您要繼續進行 **強制刪除**. 片段及其內容片段元件會從任何內容頁面中刪除。

## 尋找片段的父參照 {#parent-references-fragment}

上層參考的詳細資訊可從以下網址存取： **引用** 的欄 [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#information-content-fragments).

## 尋找片段的語言副本 {#language-copies-fragment}

語言副本的詳細資訊可從 **語言** 的欄 [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#information-content-fragments).

## 內容片段的時間軸 {#timeline-for-content-fragments}

>[!NOTE]
>
此功能僅適用於 **資產** 主控台

除了標準選項外， [時間表](/help/assets/manage-digital-assets.md#timeline) 提供內容片段的特定資訊和動作：

* 檢視有關版本、註釋和註解的資訊
* 版本動作

   * **[還原為此版本](#reverting-to-a-version)** （選取現有片段，然後選取特定版本）

   * **[與目前專案比較](#comparing-fragment-versions)** （選取現有片段，然後選取特定版本）

   * 新增 **標籤** 和/或 **註解** （選取現有片段，然後選取特定版本）

   * **另存為版本** （選取現有片段，然後選取時間軸底部的向上箭頭）

* 註解動作

   * **刪除**

>[!NOTE]
>
註解包括：
>
* 所有資產的標準功能
* 在時間軸中製作
* 與片段資產相關
>
註解（適用於內容片段）包括：
>
* 在片段編輯器中輸入
* 特定於片段中選取的文字區段
>

例如：

![時間表](assets/cfm-managing-05.png)

## 比較片段版本 {#comparing-fragment-versions}

>[!NOTE]
>
此功能僅適用於 **資產** 主控台

此 **與目前專案比較** 動作可從 [時間表](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) 在您選取特定版本之後。

這將會開啟：

* 此 **目前** （最新）版本（左）

* 選取的版本 **v&lt;*x.y*>** （右）

它們會並排顯示，其中：

* 任何差異都會反白顯示

   * 刪除的文字 — 紅色
   * 插入的文字 — 綠色
   * 取代的文字 — 藍色

* 全熒幕圖示可讓您自行開啟任一版本，然後切換回平行檢視
* 您可以 **回覆** 至特定版本
* **完成** 將帶您返回主控台

>[!NOTE]
>
比較片段時無法編輯片段內容。

![比較](assets/cfm-managing-06.png)

## 回覆至某個版本  {#reverting-to-a-version}

>[!NOTE]
>
此功能僅適用於 **資產** 主控台

您可以還原到片段的特定版本：

* 直接從 [時間表](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

  選取所需的版本，然後 **還原為此版本** 動作。

* 當 [比較版本與目前版本](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#comparing-fragment-versions) 您可以 **回覆** 至選取的版本。
