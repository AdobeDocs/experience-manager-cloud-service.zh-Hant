---
title: 頁面差異
description: 頁面差異功能可方便並排比較兩個頁面，並反白顯示其差異。
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 1%

---

# 頁面差異 {#page-diff}

## 簡介 {#introduction}

內容建立是一個反複的過程。 以效率撰寫需要能夠檢視反複專案之間有何變更。 檢視一個頁面版本然後檢視另一個頁面版本會效率低下，並容易出錯。 作者希望能夠輕鬆地將目前頁面與另一個版本並排比較。

頁面差異功能可方便並排比較兩個頁面，並反白顯示其差異。

>[!NOTE]
>
>使用者必須具備 **修改/建立/刪除** 節點的許可權 `/content/versionhistory` 以使用功能。
>
>另請參閱 [開發和頁面差異](/help/implementing/developing/introduction/page-diff.md#operation-details) 以取得此功能的詳細技術資訊。

## 使用 {#use}

並排的差異可以比較：

* [版本](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page)  — 具有目前狀態的舊版頁面
* [即時副本](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page)  — 即時副本與其Blueprint
* [啟動](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page)  — 以其來源啟動
* [語言副本](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies)  — 翻譯之前和翻譯之後（重新翻譯）的頁面

請參閱相關主題，瞭解如何在這些內容中開始差異化。

### 差異的表示 {#presentation-of-differences}

無論比較的內容為何，差異的顯示方式會維持不變。

* 開始差異時選取的內容會顯示在左側（差異進入點）。
* 比較對象內容會顯示在右側（所選內容會與之比較）。

例如，如果比較版本，目前版本會顯示在左側，而先前版本會顯示在右側。

兩個頁面的來源會清楚顯示在瀏覽器視窗頂端的標頭列中。

![版本並排檢視](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

差異會偵測元件和HTML層級的變更。 已變更的專案會以不同的顏色反白。

**元件變更**

* 淡綠色 — 已新增元件
* 粉紅色 — 元件已移除

**HTML變更**

* 深綠色 — 新增HTML
* 紅色 — 已移除HTML

>[!NOTE]
>
>比較語言副本時，反白顯示會停用，因為在翻譯中，所有變更和反白顯示都沒有好處。

### 全熒幕和正在退出 {#fullscreen-and-exiting}

若要聚焦於特定內容，您可以按一下並排差異的任一「邊」的全熒幕圖示，將其放大至整個瀏覽器視窗。

![全熒幕按鈕](/help/sites-cloud/authoring/assets/versions-full-screen.png)

選取的一側會填滿整個視窗，但橫條會保留在頂端，讓您在兩個頁面之間切換。

![全熒幕模式](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>如果瀏覽器寬度無法同時容納全熒幕檢視中的兩個頁面名稱，則只會顯示所顯示頁面的名稱，而另一個名稱則會顯示在省略符號後面。

您也可以選擇按一下退出全熒幕圖示來關閉全熒幕檢視。

![退出全螢幕模式](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

您可以隨時按一下標頭中的「關閉」按鈕來結束並排比較。

## 限制 {#limitations}

在某些情況下，頁面差異可能不會如預期偵測到差異。

* 不同版本和啟動時，差異不會將階層連結、選單、產品清單或標誌（依賴網站結構來呈現其內容的元件）等動態元件列入考量。
* 對於版本，差異不會重新建立存取控制原則和即時副本關係。
* 如果頁面已移動，您將無法再執行與移動前所做的任何版本之間的差異。
   * 如果您遇到差異問題，請檢查 [時間表](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) ，以檢視頁面是否已移動。

>[!NOTE]
>
>版本無法相互比較。 只有目前版本可以和頁面的其他版本比較。 目前版本永遠是反白顯示變更的版本。

>[!NOTE]
>
>如需有關頁面差異機制的操作以及可能影響頁面差異的限制的詳細資訊，請參閱 [開發人員檔案](/help/implementing/developing/introduction/page-diff.md) 此功能的功能。
