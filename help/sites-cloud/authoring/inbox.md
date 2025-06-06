---
title: 您的收件匣
description: 瞭解如何使用到達收件匣的通知來管理您的工作。
exl-id: 37d0cf43-192f-4a50-b174-42d7dced3b63
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 15%

---

# 您的收件匣 {#your-inbox}

您可以從AEM的各種區域接收通知，包括工作流程和專案。 例如，您可能會收到下列相關通知：

* 任務：
   * 這些也可以在AEM UI中的不同位置建立，例如&#x200B;**專案**&#x200B;下。
   * 這些可以是工作流「建立任務」 **或「建立**&#x200B;**項目任務」步驟的產品** 。
* 工作流程：
   * 代表您需要對頁面內容執行之動作的工作專案
      * 這些是工作流程&#x200B;**參與者**&#x200B;步驟的產品。
   * 失敗專案，可讓管理員重試失敗的步驟

您會在自己的收件匣中收到這些通知，您可以在其中檢視通知並採取行動。

>[!NOTE]
>
>如需有關專案型別的詳細資訊，請參閱下列內容：
>
>* [個專案](/help/sites-cloud/authoring/projects/overview.md)
>* [專案 — 處理任務](/help/sites-cloud/authoring/projects/tasks.md)
>* [工作流程](/help/sites-cloud/authoring/workflows/overview.md)

## 標題中的收件匣 {#inbox-in-the-header}

在任一控制檯中，收件匣中目前的專案數量會顯示在標題中。 指標也可以開啟，以提供對需要動作的頁面的快速存取或收件匣的存取權：

標題![&#128279;](/help/sites-cloud/authoring/assets/inbox-header.png)中的收件匣概觀

>[!NOTE]
>
>某些動作也會顯示在適當資源[&#128279;](/help/sites-cloud/authoring/basic-handling.md#card-view)的卡片檢視中。

## 開啟收件匣 {#opening-the-inbox}

若要開啟AEM通知收件匣：

1. 選取工具列中的指示器。

1. 選擇「 **全部查看**」。**AEM收件匣**&#x200B;開啟。 收件匣會顯示工作流程、專案和工作中的項目。
1. 預設視圖是「列 [表視圖](#inbox-list-view)」，但您也可以切換到「日 [歷視圖」](#inbox-calendar-view)。這是使用檢視選取器 (工具列，右上方) 完成。

   對於這兩個檢視，您也可以定義[檢視設定](#inbox-view-settings)。 可用的選項取決於目前檢視。

   ![收件匣檢視設定](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>收件箱作為控制台運行，因此，在您完成 [後，使用全局導航](/help/sites-cloud/authoring/basic-handling.md#global-navigation) [&#128279;](/help/sites-cloud/authoring/search.md) 或搜索導航到其他位置。

### 收件匣 — 清單檢視 {#inbox-list-view}

此檢視會列出所有專案，以及相關資訊：

![收件匣清單檢視](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### 收件匣 — 行事曆檢視 {#inbox-calendar-view}

此檢視會根據專案在行事曆中的位置顯示專案：

![收件匣行事曆檢視](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

您可以：

* 選取特定檢視： **時間表**，**欄**，**清單**
* 指定要根據「計畫」顯示的 **任務**:所有 **計畫中**&#x200B;的， **進行中**, **即將到**，過 **&#x200B;**&#x200B;**去的,**
* 向下展開以取得專案的詳細資訊
* 選取日期範圍以集中檢視：

![收件匣行事曆檢視日期範圍](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### 收件匣 — 檢視設定 {#inbox-view-settings}

對於這兩個檢視（「清單」和「行事曆」），您可以定義設定：

* **日曆檢視**

  您可以針對&#x200B;**行事曆檢視**&#x200B;設定：

   * **群組依據**
   * **排程** 或無 **&#x200B;**
   * **卡片大小**

  ![收件匣行事曆檢視設定](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **清單檢視**

  您可以為&#x200B;**清單檢視**&#x200B;設定排序機制：

   * **排序於**
   * **排序順序**

  ![收件匣清單檢視設定](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

  您也可以將行事曆委派給其他使用者、請求其他使用者的委派以及管理您的委派。

  ![收件匣清單檢視委派設定](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## 對專案執行動作 {#taking-action-on-an-item}

>[!NOTE]
>
>雖然可以選取多個專案，但一次只能對一個專案執行動作。

1. 若要對專案執行動作，請選取適當專案的縮圖。 適用於該專案的動作圖示會顯示在工具列中：

   ![選取收件匣專案](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   這些動作適用於該專案，包括：

   * **完成**&#x200B;動作
   * **委派**&#x200B;專案
   * **開啟**&#x200B;專案，視專案型別而定，此動作可以：

      * 顯示專案屬性
      * 開啟適當的儀表板或精靈以進一步動作
      * 開啟相關檔案

   * **後退**&#x200B;至上一步
   * 檢視工作流程的裝載
   * 從專案建立專案

   >[!NOTE]
   >
   >如需詳細資訊，請參閱下列內容：
   >
   >* 工作流程專案 — [參與工作流程](/help/sites-cloud/authoring/workflows/participating.md)

2. 視選取的專案而定，會啟動動作，例如：

   * 隨即開啟適用於此動作的對話方塊
   * 已啟動動作精靈
   * 檔案頁面已開啟

   例如，**代理人**&#x200B;會開啟一個對話方塊：

   ![委派收件匣任務](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   視是否已開啟對話方塊、精靈、檔案頁面而定，您可以：

   * 確認適當的動作，例如，重新指派。
   * 取消動作
   * 選取「上一步」箭頭可返回收件匣，例如，如果動作精靈或檔案頁面已開啟，則可返回「收件匣」。

## 建立任務 {#creating-a-task}

您可以從收件匣建立任務：

1. 選取&#x200B;**建立**，然後選取&#x200B;**工作**。
1. 填寫「基本」和「進階 **」標籤中的必要欄位** (只有「 **標題**&#x200B;**&#x200B;** 」是必填的，其他所有欄位都是選用的):

   * **基本**：

      * **標題**
      * **專案**
      * **被指定者**
      * **內容**，類似承載，這是從任務到存放庫中的位置的參考
      * **說明**
      * **任務優先順序**
      * **開始日期**
      * **到期日期**

   ![收件匣新增任務](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **進階**

      * **名稱**：用來組成URL，如果空白，則以&#x200B;**標題**&#x200B;為基礎。

   ![收件匣新增工作進階選項](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. 選取&#x200B;**提交**。

## 建立專案 {#creating-a-project}

您可以針對特定任務根據該任務建立[專案](/help/sites-cloud/authoring/projects/overview.md)：

1. 點選/按一下縮圖，選取適當的工作。

   >[!NOTE]
   >
   >只有使用&#x200B;**收件匣**&#x200B;的&#x200B;**建立**&#x200B;選項建立的任務才能用來建立專案。
   >
   >工作專案（來自工作流程）無法用於建立專案。

1. 從工 **具列選擇** 「建立專案」以開啟精靈。
1. 選取適當的範本，然後按&#x200B;**下一步**。
1. 指定必要的屬性：

   * **基本**

      * **標題**
      * **說明**
      * **開始日期**
      * **到期日期**
      * **使用者**&#x200B;和角色

   * **進階**

      * **名稱**

   >[!NOTE]
   >
   >如需完整資訊，請參閱[建立專案](/help/sites-cloud/authoring/projects/managing.md#creating-a-project)。

1. 選取&#x200B;**建立**&#x200B;以確認動作。

## 篩選AEM收件匣中的專案 {#filtering-items-in-the-aem-inbox}

您可以篩選列出的專案：

1. 開啟&#x200B;**AEM收件匣**。

1. 開啟篩選選擇器：

   ![收件匣搜尋](/help/sites-cloud/authoring/assets/inbox-search.png)

1. 您可以根據一系列條件篩選列出的專案，其中許多條件可以細化。 例如：

   ![收件匣搜尋篩選器](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >透過[檢視設定](#inbox-view-settings)，您也可以在使用[清單檢視](#inbox-list-view)時設定排序順序。
