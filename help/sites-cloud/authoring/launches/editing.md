---
title: 編輯啟動
description: '為頁面（或一組頁面）建立啟動後，您可以編輯頁面啟動副本中的內容。 '
translation-type: tm+mt
source-git-commit: ba7a8f5027b71ebdee7c84ed35d374fe22645a5a
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 17%

---


# 編輯啟動 {#editing-launches}

## 編輯啟動頁面{#editing-launch-pages}

為頁面（或一組頁面）建立啟動後，您可以編輯頁面啟動副本中的內容。

1. 存取[從參考啟動（網站主控台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)以顯示可用動作。
1. 選擇&#x200B;**移至頁面**&#x200B;以開啟頁面進行編輯。

編輯頁面時，您會在頂端工具列中看到指示，以及&#x200B;**Leave**&#x200B;和&#x200B;**Navigate**&#x200B;選項：

![離開頁面編輯器並導覽啟動](/help/sites-cloud/authoring/assets/launches-edit-01.png)

>[!NOTE]
>
>您不允許在啟動中移動頁面。 嘗試此動作將觸發警告訊息：
>
>* 警告：此頁面是啟動的來源。 不允許移動頁面。


### 編輯受即時副本約束的啟動頁面{#editing-launch-pages-subject-to-a-live-copy}

如果您的啟動是以[即時副本](/help/sites-cloud/administering/msm/overview.md)為基礎，則您會：

* 當您編輯元件（內容和／或屬性）時，請參閱鎖定符號（小掛鎖）。
* 請參閱&#x200B;**頁面屬性**&#x200B;中的&#x200B;**即時副本**&#x200B;標籤

livecopy可用來將來源 *分支的內容*** 同步到啟動分支 (以便讓啟動與來源中所做的變更保持最新)。

您可以編輯標準即時副本的方式進行變更；例如：

* 按一下已關閉的掛鎖將中斷此同步，並允許您在啟動中對內容進行新更新。 解鎖（開啟掛鎖）後，源分支中同一位置所做的任何更改將不會覆蓋您的更改。
* **暫停** (和 **繼續**)特定頁面的繼承。

如需詳細資訊，請參閱[變更即時副本內容](/help/sites-cloud/administering/msm/creating-live-copies.md)。

## 將啟動頁與其源頁比較{#comparing-a-launch-page-to-its-source-page}

若要追蹤您所做的變更，您可以在「參考」中檢視啟動 **** ，並比較啟動頁面與其來源頁面：

1. 在&#x200B;**Sites**&#x200B;主控台中，[導覽至啟動的來源頁面，並選取一個](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟&#x200B;**[References](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**&#x200B;面板，然後選擇&#x200B;**Launches**。
1. 選擇您的特定啟動，然後選擇&#x200B;**與源比較**:

   ![比較啟動與來源](/help/sites-cloud/authoring/assets/launches-compare.png)

1. 兩個頁面（啟動和來源）將並排開啟。

   有關使用此功能的完整資訊，請參見[頁面差異](/help/sites-cloud/authoring/features/page-diff.md)。

## 更改使用的源頁{#changing-the-source-pages-used}

您隨時可以在啟動的來源頁面範圍中新增或移除頁面：

1. 存取並選取啟動：
   * [啟動控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * 選擇&#x200B;**編輯**。
   * [參考（Sites控制台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 以顯示可用動作：
      * 選擇&#x200B;**編輯啟動**。
      * 將顯示源頁面。
1. 進行必要的變更，然後使用「儲存」 **確認**。

>[!NOTE]
>
>若要將頁面新增至啟動，頁面必須位於通用語言根目錄下；即在單一網站中。

## 編輯啟動配置{#editing-a-launch-configuration}

您可以隨時編輯啟動的屬性：

1. 存取並選取啟動：
   * [啟動控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * 選擇&#x200B;**屬性**。
   * [參考（Sites控制台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 以顯示可用動作：
      * 選擇&#x200B;**編輯屬性**。
      * 將顯示詳細資訊。
1. 進行必要的變更，然後使用「儲存」 **確認**。
   * 如需 [「啟動日期」和「生產就緒」欄位的用途和互動相關資訊，請參閱「啟動——事件順序」](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) (Launches - Order of Events ******** )。

## 發現頁面{#discovering-the-launch-status-of-a-page}的啟動狀態

當您從「參考」標籤中選擇特定啟動時，會顯示狀態(請參閱[在參考中啟動(Sites Console)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console))。

![發現啟動狀態](/help/sites-cloud/authoring/assets/launches-status.png)
