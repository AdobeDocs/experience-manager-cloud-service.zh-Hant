---
title: '建立啟動 '
description: 您可以建立啟動來更新現有網頁的新版本，以供日後啟動。
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 14%

---


# 建立啟動 {#creating-launches}

建立啟動以更新現有網頁的新版本，以供日後啟動。 當您建立啟動時，您會指定標題和來源頁面：

* 標題會出現在「參 [考」邊欄](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) ，作者可從中存取這些標題以處理它們。
* 依預設，來源頁面的子頁面會包含在啟動中。 視需要，您只能使用來源頁面。
* 依預設，即時副本會隨著來源頁面的變更自動更新啟動頁面。 您可以指定建立靜態副本以防止自動更改。 <!--By default, [Live Copy](/help/sites-administering/msm.md) automatically updates the launch pages as the source pages change. You can specify that a static copy is created to prevent automatic changes.-->

(可選) 您可以指定 **啟動日期**  (和時間)，以定義啟動頁面要升級和啟動的時間。不過，「 **啟動日期** 」只會搭配「生產就緒 **」旗標運作(請** 參閱編輯啟動設定 [](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration));要讓動作實際自動發生，必須同時設定。

## 建立啟動 {#creating-a-launch}

您可以從「網站」或「啟動」主控台建立啟動：

1. 開啟「 **Sites** 」或「 **Launches** 」主控台。

   >[!NOTE]
   >
   >使用 **Sites** Console時，通常導覽至來源頁面的位置，但這並非強制性，因為您在精靈中選取 **Launch Source** 時可導覽。

1. 根據您使用的控制台：
   * **啟動**:
      1. Select **Create Launch** from the toolbar to open the wizard.
   * **網站**:
      1. 從工 **具列選擇** 「建立」(Create)以開啟選擇框。
      1. 在此選擇「 **建立啟動** 」以開啟嚮導。

   >[!NOTE]
   >
   >在Sites **** Console中，您也可以使用選 [擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) ，在選擇「建立」之前選擇 **頁面**。
   >
   >這會將選取的頁面當做初始來源頁面。

1. 在「選 **取來源** 」步驟中，您需要 **新增頁面**。 您可以選取多個頁面，並指定每個頁面的路徑：
   * 導覽至所需位置。
   * 選擇源頁面並確認（複選標籤）。

   視需要重複。

   ![選擇啟動源](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >若要新增頁面和／或分支至啟動，它們必須位於網站中； 例如，在一般頂層根目錄下。
   >
   >如果網站的語言根目錄位於最上層，則啟動的頁面和分支必須位於共同語言根目錄下。

1. 您可以針對每個項目指定是否：

   * **包含子頁面**:

      * 指定您要建立包含子頁面或不包含子頁面的啟動。  依預設，會包含此子頁面。

   繼續「下 **一步**」。

   ![選擇啟動源](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. 在嚮導 **的** 「屬性」步驟中，您可以指定：

   * **啟動標題**: 啟動的名稱。 名稱對作者應有意義。
   * **使用現有內容**: 原始內容將用來建立啟動。
   * **使用新範本來取代頁面**: 如需詳 [細資訊，請參閱「使用新範本建立啟動](#create-launch-with-new-template) 」。
   * **繼承來源頁面即時資料**: 選取此選項，可在來源頁面變更時自動更新啟動頁面的內容。 此選項可讓啟動成為即時副本，以達成此目的。 預設會選取此選項。 <!--Select this option to automatically update the content of launch pages when the source pages change. This option achieves this by making the launch a [live copy](/help/sites-administering/msm.md). By default, this option is selected.-->
   * **啟動日期**: 啟動副本要啟動的日期和時間(取決於「生產就緒」 **標誌** ; 請 [參閱啟動——事件順序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events))。

   ![啟動屬性](/help/sites-cloud/authoring/assets/launches-properties.png)

1. 使用 **Create** （建立）完成程式並建立新的啟動。 確認對話框將詢問您是否要立即開啟啟動。

   如果您傳回主控台(使 **用Done**)，您可從下列任一位置查看（並存取）您的啟動：

   * 啟動 [**控制台&#x200B;**](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * Sites控 [**制台&#x200B;**中的**&#x200B;參考&#x200B;**](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### 使用新範本建立啟動 {#create-launch-with-new-template}

建立啟動時，您可以選擇是否使用新範本：

>[!NOTE]
>
>只有在從Sites主控台建立啟動時，才能使用 **此選項** 。 當從啟動控制台建立啟動時， **它不** 可用。

![使用新範本建立啟動](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

選擇此選項將：

* 更新其他可用選項，
* 加入新步驟，您可在其中選取所需範本。

![選取新範本](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>當使用不同的範本時，新頁面會是空的。 由於頁面結構不同，不會複製任何內容。
>
>此機制可用來變更現有頁面的范 [本](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) -不過必須考慮內容遺失。

### 建立巢狀啟動 {#creating-a-nested-launch}

建立巢狀啟動（在啟動中啟動）可讓您從現有啟動建立啟動，讓作者可以利用已做的變更，而不必對每次啟動進行多次相同的變更。

>[!NOTE]
>
>另請參閱 [提升巢狀啟動](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch)。

#### 建立巢狀啟動——啟動主控台 {#creating-a-nested-launch-launches-console}

從 **Launches** console建立巢狀啟動基本上與建立任何其他啟動形式相同，但您必須導覽至啟動分支 `/content/launches`:

1. 在啟動控 **制台** ，選擇 **建立**。
1. 選取「 **新增頁面**」，然後在篩選條件中指定以導覽至啟 `/content/launches` 動分支。選擇所需的啟動並使用「選擇 **」確認**:

   ![建立巢狀啟動](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. 繼續「下 **一步** 」，並像啟動其 **他產品一樣完成「屬性** 」。

   ![選取巢狀啟動的來源](/help/sites-cloud/authoring/assets/launches-create-nested-select.png)

#### 建立巢狀啟動——網站主控台 {#creating-a-nested-launch-sites-console}

若要從 **Sites** Console建立巢狀啟動，請根據現有啟動：

1. 存取「 [從參考啟動（網站主控台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 」以顯示可用動作。
1. 選 **擇「建立啟動** 」以開啟嚮導(由於已選擇源，因此它將跳過 **** 選擇源步驟)。
1. 輸入「 **啟動標題** 」和任何其他必要的詳細資訊（如同一般啟動）。
1. 使用 **Create** （建立）完成程式並建立新的啟動。 確認對話框將詢問您是否要立即開啟啟動。

如果您選 **取「完成**」，則會返回至Sites ******** Console的「參考」邊欄，如果您選取適當的頁面，則會顯示您的新啟動。

### 刪除啟動 {#deleting-a-launch}

您可以從啟動控制台刪 [除啟動](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* 點選／按一下縮圖，以選取啟動。
* 工具欄將出現——選擇刪除。
* 確認動作。

>[!CAUTION]
>
>刪除啟動會移除啟動本身和所有子系巢狀啟動。
