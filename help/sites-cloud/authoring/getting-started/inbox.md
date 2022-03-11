---
title: 您的收件匣
description: 使用收件箱管理任務
exl-id: 37d0cf43-192f-4a50-b174-42d7dced3b63
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 17%

---

# 您的收件匣 {#your-inbox}

您可以從各個領域(包括工作流和AEM項目)接收通知。 例如，您可能會收到有關以下內容的通知：

* 任務：
   * 也可在UI內的各個點建立AEM，例如，在 **項目**。
   * 這些可以是工作流「建立任務」 **或「建立****項目任務」步驟的產品** 。
* 工作流程:
   * 表示需要對頁面內容執行的操作的工作項
      * 這些是工作流的產品 **參與者** 的子菜單。
   * 失敗項，允許管理員重試失敗的步驟

您可以在自己的收件箱中接收這些通知，您可以在此查看這些通知並採取行動。

>[!NOTE]
>
>有關項目類型的詳細資訊，另請參閱：
>
>* [專案](/help/sites-cloud/authoring/projects/overview.md)
>* [項目 — 使用任務](/help/sites-cloud/authoring/projects/tasks.md)
>* [工作流程](/help/sites-cloud/authoring/workflows/overview.md)


## 標題中的收件箱 {#inbox-in-the-header}

在任何控制台中，收件箱中的當前項目數都顯示在標題中。 還可以開啟指示器，以便快速訪問需要操作的頁面或訪問收件箱：

![標題中的收件箱概述](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>某些操作也將顯示在 [相應資源的卡視圖](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)。

## 開啟收件箱 {#opening-the-inbox}

要開啟通知收AEM件箱：

1. 按一下/點擊工具欄中的指示器。

1. 選擇「 **全部查看**」。「 **AEM收件匣** 」將會開啟。收件匣會顯示工作流程、專案和工作中的項目。
1. 預設視圖是「列 [表視圖](#inbox-list-view)」，但您也可以切換到「日 [歷視圖」](#inbox-calendar-view)。這是使用檢視選取器 (工具列，右上方) 完成。

   對於這兩個視圖，您還可以定義 [查看設定](#inbox-view-settings)。 可用選項取決於當前視圖。

   ![收件箱視圖設定](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>收件箱作為控制台運行，因此，在您完成 [後，使用全局導航](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)[](/help/sites-cloud/authoring/getting-started/search.md) 或搜索導航到其他位置。

### 收件箱 — 清單視圖 {#inbox-list-view}

此視圖列出所有項目及相關資訊：

![收件箱清單視圖](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### 收件箱 — 日曆視圖 {#inbox-calendar-view}

此視圖根據項目在日曆中的位置顯示項目：

![收件箱日曆視圖](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

您可以：

* 選擇特定視圖： **時間軸**。 **列**。 **清單**
* 指定要根據「計畫」顯示的 **任務**:所有 **計畫中**&#x200B;的， **進行中**, **即將到**，過 ******去的,**
* 深入查看有關物料的詳細資訊
* 選擇日期範圍以聚焦視圖：

![收件箱日曆視圖日期範圍](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### 收件箱 — 查看設定 {#inbox-view-settings}

對於兩個視圖（「清單」和「日曆」），可以定義設定：

* **日曆檢視**

   對於 **日曆視圖** 您可以配置：

   * **分組依據**
   * **排程** 或無 ****
   * **卡大小**

   ![收件箱日曆視圖設定](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **清單檢視**

   對於 **清單視圖** 可以配置排序機制：

   * **排序**
   * **排序順序**

   ![收件箱清單視圖設定](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   您還可以將日曆委託給其他用途，以及從其他用戶請求委託並管理委託。

   ![收件箱清單視圖委派設定](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## 對物料執行操作 {#taking-action-on-an-item}

>[!NOTE]
>
>雖然可以選擇多個項，但一次只能對一個項執行操作。

1. 要對項目執行操作，請為相應項目選擇縮略圖。 適用於該項目的操作的表徵圖將顯示在工具欄中：

   ![選擇收件箱項](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   這些操作適用於項目，包括：

   * **完成** 動作
   * **委託** 物料
   * **開啟** 項，根據項類型，此操作可以：

      * 顯示項屬性
      * 開啟適當的儀表板或嚮導以執行進一步操作
      * 開啟相關文檔
   * **後退** 到上一步
   * 查看工作流的負載
   * 從物料建立項目

   >[!NOTE]
   >
   >有關詳細資訊，請參閱：
   >
   >* 工作流項 —  [參與工作流](/help/sites-cloud/authoring/workflows/participating.md)


2. 將根據選定的項啟動操作，例如：

   * 將開啟與操作相適應的對話框
   * 將啟動操作嚮導
   * 將開啟文檔頁面

   比如說， **委託** 將開啟對話框：

   ![委派收件箱任務](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   根據是否開啟了對話框、嚮導和文檔頁，您可以：

   * 確認相應的操作，例如重新分配。
   * 取消操作
   * 選擇後箭頭以返回到收件箱，例如，如果操作嚮導或文檔頁面已開啟，則可以返回到收件箱。


## 建立任務 {#creating-a-task}

在收件箱中，您可以建立任務：

1. 選擇 **建立**，則 **任務**。
1. 填寫「基本」和「進階 **」標籤中的必要欄位** (只有「 **標題****** 」是必填的，其他所有欄位都是選用的):

   * **基本**:

      * **標題**
      * **專案**
      * **被指定者**
      * **內容**&#x200B;與負載類似，這是從任務到儲存庫中某個位置的引用
      * **說明**
      * **任務優先順序**
      * **開始日期**
      * **到期日期**

   ![收件箱添加任務](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **進階**

      * **名稱**：這將用於形成URL，如果為空，則基於 **標題**。

   ![收件箱添加任務高級選項](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. 選擇 **提交**。

## 建立項目 {#creating-a-project}

對於某些任務，您可以建立 [項目](/help/sites-cloud/authoring/projects/overview.md) 基於該任務：

1. 按一下/按一下縮略圖，選擇相應的任務。

   >[!NOTE]
   >
   >僅使用 **建立** 選項 **收件箱** 可用於建立項目。
   >
   >無法使用工作流中的工作項建立項目。

1. 從工 **具列選擇** 「建立專案」以開啟精靈。
1. 選擇相應模板，然後 **下一個**。
1. 指定所需的屬性：

   * **基本**

      * **標題**
      * **說明**
      * **開始日期**
      * **到期日期**
      * **用戶** 角色
   * **進階**

      * **名稱**
   >[!NOTE]
   >
   >請參閱 [建立項目](/help/sites-cloud/authoring/projects/managing.md#creating-a-project) 的雙曲餘切值。

1. 選擇 **建立** 確認操作。

## 篩選收件箱中的AEM項 {#filtering-items-in-the-aem-inbox}

您可以篩選列出的項：

1. 開啟 **收件箱AEM**。

1. 開啟篩選器選擇器：

   ![收件箱搜索](/help/sites-cloud/authoring/assets/inbox-search.png)

1. 您可以根據一系列標準篩選列出的項目，其中許多可以細化。 例如：

   ![收件箱搜索篩選器](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >與 [查看設定](#inbox-view-settings) 也可以在使用 [清單視圖](#inbox-list-view)。
