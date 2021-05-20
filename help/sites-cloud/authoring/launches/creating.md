---
title: '建立啟動 '
description: 您可以建立啟動，以啟用更新新版本的現有網頁，以供日後啟用。
exl-id: 216ccb7a-1409-4f55-8be2-2b088f91a430
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 12%

---

# 建立啟動 {#creating-launches}

建立啟動，以啟用更新新版本的現有網頁，以供日後啟用。 建立Launch時，需指定標題和來源頁面：

* 標題會顯示在[參考](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)邊欄中，供作者存取，以便使用。
* 依預設，來源頁面的子頁面會包含在啟動中。 您只能視需要使用來源頁面。
* 依預設，當來源頁面變更時， [即時副本](/help/sites-cloud/administering/msm/overview.md)會自動更新啟動頁面。 您可以指定建立靜態副本以防止自動更改。

(可選) 您可以指定 **啟動日期**  (和時間)，以定義啟動頁面要升級和啟動的時間。不過，「 **啟動日期** 」只會搭配「生產就緒 **」旗標運作(請** 參閱編輯啟動設定 [](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration));要讓動作實際自動發生，必須同時設定。

>[!NOTE]
>
>當您建立啟動時，階層中上方的頁面不是來源頁面的復本。 它們是使用範本建立的預留位置：
>
>* `/libs/launches/templates/outofscope`
>
>
無法編輯這些頁面。 您會看到訊息：
>
>* **本頁面不屬於啟動。前往生產頁面**


## 建立啟動{#creating-a-launch}

您可以從Sites或Launches主控台建立啟動：

1. 開啟&#x200B;**Sites**&#x200B;或&#x200B;**Launches**&#x200B;主控台。

   >[!NOTE]
   >
   >使用&#x200B;**Sites**&#x200B;控制台時，通常導覽至來源頁面的位置，但這不是強制性操作，因為您在精靈中選取&#x200B;**啟動來源**&#x200B;時可以導覽。

1. 視您使用的主控台而定：
   * **啟動**:
      1. 從工具列選取&#x200B;**建立Launch**&#x200B;以開啟精靈。
   * **網站**:
      1. 從工具欄中選擇&#x200B;**建立**&#x200B;以開啟選擇框。
      1. 從中選擇&#x200B;**建立啟動**&#x200B;以開啟嚮導。

   >[!NOTE]
   >
   >在Sites **** Console中，您也可以使用選 [擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) ，在選擇「建立」之前選擇 **頁面**。
   >
   >這將使用所選頁面作為初始源頁面。

1. 在&#x200B;**選取來源**&#x200B;步驟中，您需要&#x200B;**新增頁面**。 您可以選取多個頁面，並指定每個頁面的路徑：
   * 導覽至所需位置。
   * 選擇源頁面並確認（複選標籤）。

   視需要重複。

   ![選擇啟動源](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >若要將頁面和/或分支新增至啟動，必須位於網站內；亦即位於通用頂層根底下。
   >
   >如果網站的頂層包含語言根目錄，則啟動的頁面和分支必須位於通用語言根目錄之下。

1. 您可以針對每個項目指定是否：

   * **包含子頁面**:

      * 指定您要使用或不使用子頁面建立啟動。  預設會包含此子頁面。

   繼續&#x200B;**Next**。

   ![選擇啟動源](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. 在精靈的&#x200B;**屬性**&#x200B;步驟中，您可以指定：

   * **啟動標題**:Launch的名稱。名稱對作者應有意義。
   * **搭配現有內容**:原始內容將用於建立啟動。
   * **使用新範本來取代頁面**:如需 [詳細資訊，請參](#create-launch-with-new-template) 閱使用新範本建立Launch 。
   * **繼承源頁面即時資料**:選取此選項，可在來源頁面變更時自動更新啟動頁面的內容。此選項會將啟動設為[即時副本](/help/sites-cloud/administering/msm/overview.md)來達成此目的。 預設情況下，此選項處於選中狀態。—>
   * **啟動日期**:啟動副本的啟動日期和時間(取決於「生產就緒」 **標** 幟；請 [參閱啟動 — 事件順序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events))。

   ![Launch屬性](/help/sites-cloud/authoring/assets/launches-properties.png)

1. 使用&#x200B;**Create**&#x200B;完成程式並建立新的啟動。 確認對話方塊會詢問您是否要立即開啟啟動。

   如果您傳回主控台（搭配&#x200B;**Done**），便可以從以下任一位置查看（並存取）您的啟動：

   * [**啟動**&#x200B;控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * **Sites**&#x200B;控制台](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)中的&#x200B;[**引用**

### 使用新範本建立Launch {#create-launch-with-new-template}

建立啟動時，您可以選取是否使用新範本：

>[!NOTE]
>
>只有在從&#x200B;**Sites**&#x200B;控制台建立啟動時，此選項才可用。 從&#x200B;**啟動**&#x200B;主控台建立啟動時無法使用。

![使用新範本建立啟動](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

選擇此項將：

* 更新其他可用選項，
* 納入可選取所需範本的新步驟。

![選取新範本](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>由於使用不同的範本，新頁面將會空白。 由於頁面結構不同，系統不會複製任何內容。
>
>此機制可用來變更[現有頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)的範本，但必須考量內容遺失。

### 建立巢狀啟動{#creating-a-nested-launch}

建立巢狀啟動（啟動內的啟動）可讓您從現有啟動建立啟動，讓作者可以利用已進行的變更，而不必對每次啟動多次進行相同的變更。

>[!NOTE]
>
>另請參閱[提升巢狀啟動](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch)。

#### 建立巢狀啟動 — 啟動主控台{#creating-a-nested-launch-launches-console}

從&#x200B;**啟動**&#x200B;控制台建立巢狀啟動基本上與建立任何其他啟動形式相同，但您需要導覽至啟動分支`/content/launches`的例外：

1. 在&#x200B;**啟動**&#x200B;控制台中，選擇&#x200B;**建立**。
1. 選取&#x200B;**新增頁面**，然後在&#x200B;**篩選器**&#x200B;邊欄中指定`/content/launches`，導覽至啟動分支。 選擇所需的啟動並使用「選擇 **」確認**:

   ![建立巢狀啟動](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. 繼續&#x200B;**Next**。

1. 如同任何其他啟動一樣完成&#x200B;**屬性**。

1. 完成&#x200B;**Create**。

#### 建立巢狀Launch — 網站主控台{#creating-a-nested-launch-sites-console}

若要從&#x200B;**Sites**&#x200B;主控台建立巢狀啟動，請根據現有啟動：

1. 存取[從參考啟動（網站控制台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)以顯示可用的動作。
1. 選 **擇「建立啟動** 」以開啟嚮導(由於已選擇源，因此它將跳過 **** 選擇源步驟)。
1. 輸入&#x200B;**啟動標題**&#x200B;和任何其他必要的詳細資訊（如同一般啟動）。
1. 使用&#x200B;**Create**&#x200B;完成程式並建立新的啟動。 確認對話方塊會詢問您是否要立即開啟啟動。

如果您選 **取「完成**」，則會返回至Sites ******** Console的「參考」邊欄，如果您選取適當的頁面，則會顯示您的新啟動。

### 刪除啟動{#deleting-a-launch}

您可以從[launches控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)刪除啟動：

* 點選/按一下縮圖，以選取啟動。
* 工具列隨即顯示 — 選取「刪除」。
* 確認動作。

>[!CAUTION]
>
>刪除啟動會移除啟動本身和所有子系巢狀啟動。
