---
title: 編輯啟動
description: 為您的頁面（或一組頁面）建立啟動後，您可以在頁面的啟動副本中編輯內容。
exl-id: d3cd3383-e0a0-4019-9f97-8baa3be99e6e
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 18%

---

# 編輯啟動 {#editing-launches}

## 編輯啟動頁面 {#editing-launch-pages}

為某個頁面（或一組頁面）建立啟動後，您可以在頁面的啟動副本中編輯內容。

1. 存取 [從「引用」（網站主控台）啟動](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 以顯示可用的動作。
1. 選取 **前往頁面** 以開啟頁面進行編輯。

編輯頁面時，您可以在頂端工具列中看到指示，以及 **離開** 和 **導覽** 選項：

![從頁面編輯器離開並導覽啟動項](/help/sites-cloud/authoring/assets/launches-edit-01.png)

>[!NOTE]
>
>您不能在啟動項中移動頁面。 嘗試此動作將觸發警告訊息：
>
>* 警告：此頁面是啟動項的來源。 不允許移動頁面。

### 編輯以即時副本為主題的啟動頁面 {#editing-launch-pages-subject-to-a-live-copy}

如果您的啟動是根據 [即時副本](/help/sites-cloud/administering/msm/overview.md) 然後您會：

* 編輯元件（內容和/或屬性）時，請參閱鎖定符號（小掛鎖）。
* 請參閱 **即時副本** 定位於 **頁面屬性**

livecopy可用來將來源 *分支的內容*** 同步到啟動分支 (以便讓啟動與來源中所做的變更保持最新)。

您可以使用與編輯標準即時副本相同的方式進行變更；例如：

* 按一下已關閉的掛鎖會中斷此同步作業，並允許您對啟動項中的內容進行新的更新。 解除鎖定（開啟掛鎖）後，在來源分支內的相同位置所做的任何變更都不會覆寫您的變更。
* **暫停** (和 **繼續**)特定頁面的繼承。

另請參閱 [變更即時副本內容](/help/sites-cloud/administering/msm/creating-live-copies.md) 以取得進一步資訊。

## 比較啟動頁面與其來源頁面 {#comparing-a-launch-page-to-its-source-page}

若要追蹤您所做的變更，您可以在「參考」中檢視啟動 **** ，並比較啟動頁面與其來源頁面：

1. 在 **網站** 主控台， [導覽至啟動項的來源頁面，並選取一個來源頁面](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. 開啟 **[引用](/help/sites-cloud/authoring/basic-handling.md#references)** 面板並選取 **啟動**.
1. 選取您的特定啟動，然後 **與來源比較**：

   ![比較啟動項和來源](/help/sites-cloud/authoring/assets/launches-compare.png)

1. 兩個頁面（啟動項和來源）會並排開啟。

   如需有關使用此功能的完整資訊，請參閱 [頁面差異](/help/sites-cloud/authoring/sites-console/page-diff.md).

## 變更使用的來源頁面 {#changing-the-source-pages-used}

您隨時可以在啟動項的來源頁面範圍中，新增或移除頁面：

1. 從下列任一位置存取並選取啟動：
   * 此 [啟動主控台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)：
      * 選取&#x200B;**編輯**。
   * [引用（網站主控台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 顯示可用的動作：
      * 選取 **編輯啟動項**.
      * 此時會顯示來源頁面。
1. 進行必要的變更，然後使用「儲存」 **確認**。

>[!NOTE]
>
>若要將頁面新增至啟動，這些頁面必須位於共同語言根目錄下；也就是說，在單一網站內。

## 編輯啟動設定 {#editing-a-launch-configuration}

您隨時可以編輯啟動項的屬性：

1. 從下列任一位置存取並選取啟動：
   * 此 [啟動主控台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)：
      * 選取 **屬性**.
   * [引用（網站主控台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 顯示可用的動作：
      * 選取 **編輯屬性**.
      * 詳細資訊隨即顯示。
1. 進行必要的變更，然後使用「儲存」 **確認**。
   * 如需 [「啟動日期」和「生產就緒」欄位的用途和互動相關資訊，請參閱「啟動——事件順序」](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) (Launches - Order of Events ******** )。

## 探索頁面的啟動狀態 {#discovering-the-launch-status-of-a-page}

當您從「引用」標籤中選取特定啟動時，會顯示狀態(請參閱 [引用（網站主控台）中的啟動](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console))。

![探索啟動項狀態](/help/sites-cloud/authoring/assets/launches-status.png)
