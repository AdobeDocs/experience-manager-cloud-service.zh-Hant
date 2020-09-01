---
title: 使用頁面版本
description: 建立、比較和還原頁面版本
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 5%

---


# 使用頁面版本 {#working-with-page-versions}

版本修訂會在特定時間點建立頁面的「快照」。 使用版本控制，您可以執行下列動作：

* 建立頁面版本。
* 將一個或多個頁面的先前版本恢復為：
   * 還原對頁面所做的變更。
   * 還原已刪除的頁面。
   * 恢復樹（在指定的日期和時間）。
* 預覽版本。
* 比較頁面的目前版本與舊版。
   * 文字和影像的差異會反白顯示。
* 時間彎曲會使用頁面版本來判斷發佈環境的狀態。

## 建立新版本 {#creating-a-new-version}

您可以從以下網址建立資源版本：

* 時間 [軸邊欄](#creating-a-new-version-timeline)
* 「創 [建](#creating-a-new-version-create-with-a-selected-resource) 」選項（當選擇資源時）

### 建立新版本——時間軸 {#creating-a-new-version-timeline}

1. 導覽以顯示您要建立版本的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟時 **間軸** 邊欄。
1. 按一下／點選注釋欄位上的省略號，以顯示選項：

   ![時間軸邊欄中的版本](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. 選擇「 **另存為版本**」。
1. 如果需要， **請輸入** 「標 **簽」和「注釋** 」。

   ![新增版本標籤](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. 使用「建立」確認新 **版本**。

   時間軸中的資訊將會更新，以指出新版本。

### 建立新版本——使用選定資源建立 {#creating-a-new-version-create-with-a-selected-resource}

1. 導覽以顯示您要建立版本的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
1. 從工具 **列中選** 取「建立」選項。
1. 將會開啟相同的對話方塊。 如有需要，您可 **以輸入** 「標籤」 **和「注釋** 」。
1. 使用「建立」確認新 **版本**。

時間軸將會開啟，並更新資訊以指出新版本。

## 恢復版本 {#reinstating-versions}

在您建立頁面版本後，有多種方法可重新安裝舊版：

* 「時 **間軸」邊欄中** 「回復為 [此版本](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) 」

   重新建立舊版選取頁面。

* 頂部操 **作工具欄** 中的「恢復 [」選項](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * **還原版本**

      恢復當前選定資料夾中指定頁面的版本；這也可以包括還原先前已刪除的頁面。

   * **還原樹狀結構**

      在指定日期和時間恢復整個樹的版本；這可包含先前已刪除的頁面。

>[!NOTE]
>
>當恢復頁面時，所建立的版本將是新分支的一部分。
>
>要說明：
>
>1. 建立任何頁面的版本。
>1. 初始標籤和版本節點名稱為1.0、1.1、1.2等。
>1. 恢復第一個版本；即1.0。
>1. 再次建立新版本。
>1. 產生的標籤和節點名稱現在會是1.0.0、1.0.1、1.0.2等。


### 還原為版本 {#revert-to-a-version}

要將 **選定頁** 恢復為舊版，請執行以下操作：

1. 導覽以顯示您要回復為舊版的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。將列出所選頁面的頁面版本。
1. 選擇要回復的版本。 可能的選項將顯示：

   ![還原為此版本](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Select **Revert to this Version**. 將還原所選版本，並更新時間軸中的資訊。

### 還原版本 {#restore-version}

此方法可用於恢復當前資料夾中指定頁面的版本；這也可以包括還原先前已刪除的頁面：

1. 導覽至所需的 [資料夾](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)，並加以選取。

1. 從頂 **部操作工具**&#x200B;欄中，依次選 **擇「恢復版本** 」和「 [恢復版本](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)」。

   >[!NOTE]
   >
   >如果，則：
   >* 您選擇了單一頁面，而且沒有子頁面，
   >* 或者資料夾中的任何頁面都沒有版本，

   >
   >然後，由於沒有適用的版本，顯示將會是空的。

1. 將列出可用版本：

   ![還原版本——資料夾中所有頁的清單](/help/sites-cloud/authoring/assets/versions-restore-version-01.png)

1. 對於特定頁面，請使用「還原為版本 **** 」下方的下拉式選取器來選取該頁面的必要版本。

   ![還原版本——選擇版本](/help/sites-cloud/authoring/assets/versions-restore-version-02.png)

1. 在主顯示中，選擇要還原的所需頁面：

   ![「恢復版本——選擇」頁](/help/sites-cloud/authoring/assets/versions-restore-version-03.png)

1. 為要 **** 還原為當前版本的選定頁面選擇「還原」。

>[!NOTE]
>
>您選擇所需頁面和相關版本的順序是可互換的。

### 還原樹狀結構 {#restore-tree}

此方法可用於在指定的日期和時間恢復樹的版本；這可包含先前已刪除的頁面：

1. 導覽至所需的 [資料夾](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)，並加以選取。

1. 從頂 **部操作工具**&#x200B;欄中，依次選 **擇「恢復樹** 」和「 [恢復樹](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)」。 將顯示樹的最新版本：

   ![還原樹狀結構](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. 使用日期和時間選擇器 **的「日期的最新版本** 」(Latest Versions at Date)來選擇樹的另一個版本，即要還原的版本。

1. 根據需要設 **置「保留的非版本化頁** 」標籤：

   * 如果是作用中（選取），則任何非版本化頁面都將保留，且不會受到還原的影響。

   * 如果非活動（未選定），則任何非版本化頁面都將被移除，因為版本化樹中不存在這些頁面。

1. 為要 **還原的樹的選定版本選擇「還原」(Restore** )作為當前 *版本* 。

## 預覽版本 {#previewing-a-version}

您可以預覽特定版本：

1. 導覽以顯示您要比較的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。
1. 將列出頁面版本。 選擇您要預覽的版本：

   ![預覽版本](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 選擇「 **預覽**」。 頁面將顯示在新標籤中。

   >[!CAUTION]
   >
   >如果頁面已移動，您無法再對移動前進行的任何版本執行預覽。
   >
   >如果您在預覽時遇到問題，請檢查頁 [面的時間軸](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) ，以查看頁面是否已移動。

## 比較版本與目前頁面 {#comparing-a-version-with-current-page}

若要比較舊版與目前頁面：

1. 導覽以顯示您要比較的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。
1. 將列出頁面版本。 選擇要比較的版本：

   ![比較版本](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 選擇 **與目前比較**。 頁 [面差異](/help/sites-cloud/authoring/features/page-diff.md) ，會開啟並顯示差異。

## Timewarp {#timewarp}

時間彎曲是一種功能，可模 *擬過去* 特定時間頁面的發佈狀態。

由於內容建立是持續的協作程式，因此「時間彎曲」的目的是讓作者能夠隨時追蹤發佈的網站，以便瞭解內容的變更。 此功能使用頁面版本來判斷發佈環境的狀態。

要執行此操作：

* 系統會尋找在選取時間作用中的頁面版本。
* 這表示在「時間彎曲」中選取的時 *間點之前* ，已建立／啟動顯示的版本。
* 導航到已刪除的頁面時，也會呈現該頁面——只要該頁面的舊版本仍然在儲存庫中可用。
* 如果找不到發佈版本，則「時間彎曲」會回復為作者環境上頁面的目前狀態（這是為了防止發生錯誤/404頁面，這會防止瀏覽）。

### 使用時間彎曲 {#using-timewarp}

時間彎曲是頁 [面編輯](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 器的一種模式。 若要啟動它，只需像切換任何其他模式一樣來切換它。

1. 啟動您要啟動「時間彎曲」頁面的編輯器，然後在模式選 **擇中選擇** 「時間彎曲」。

   ![時間彎曲模式](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. 在對話方塊中設定目標日期和時間，然後按一下或點選「設 **定日期」**。如果您未選取時間，則預設為目前時間。

   ![時間彎曲目標日期](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. 頁面會根據日期集顯示。 時間彎曲模式會透過視窗頂端的藍色狀態列來指示。 使用狀態列中的連結來選取新的目標日期或退出時間彎曲模式。

   ![在「時間彎曲」模式中](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### 時間彎曲限制 {#timewarp-limitations}

時間彎曲會盡力在選取的時間點重制頁面。 不過，由於AEM中持續製作內容十分複雜，因此並非總能做到。 當您使用Timewarp時，應牢記這些限制。

* **時間彎曲會根據已發佈的頁面運作** -只有在您先前已發佈頁面時，時間彎曲才會完全運作。 如果不是，時間彎曲會顯示作者環境中的目前頁面。
* **時間彎曲使用頁面版本** -如果您導覽至已從儲存庫中移除／刪除的頁面，如果舊版頁面仍在儲存庫中，則會正確呈現該頁面。
* **刪除的版本會影響「時間彎曲** 」 —— 如果從儲存庫中刪除版本，則「時間彎曲」無法顯示正確的視圖。
* **時間彎曲為唯讀** -您無法編輯舊版頁面。 僅供檢視。 如果要恢復舊版，則必須使用恢復手動執行 [操作](#revert-to-a-version)。
* **時間彎曲僅基於頁面內容** -如果轉換網站的元素（例如程式碼、css、資產／影像等）已變更，檢視會與原本的檢視不同，因為這些項目未在儲存庫中版本化。

>[!CAUTION]
>
>時間彎曲功能是設計為工具，可協助作者瞭解並建立其內容。 它不是作為審計日誌或用於法律目的。
