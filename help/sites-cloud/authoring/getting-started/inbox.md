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

您可以從AEM的各個區域收到通知，包括工作流程和專案。 例如，您可能會收到以下通知：

* 任務：
   * 您也可以在AEM UI內的各個時間點建立這些項目，例如在&#x200B;**Projects**&#x200B;底下。
   * 這些可以是工作流「建立任務」 **或「建立****項目任務」步驟的產品** 。
* 工作流程:
   * 代表您需要在頁面內容上執行之動作的工作項目
      * 這些是工作流&#x200B;**參與者**&#x200B;步驟的產品。
   * 失敗項目，以允許管理員重試失敗的步驟

您會在自己的收件匣中收到這些通知，您可在此檢視並採取行動。

>[!NOTE]
>
>有關項目類型的詳細資訊，另請參閱：
>
>* [專案](/help/sites-cloud/authoring/projects/overview.md)
* [項目 — 使用任務](/help/sites-cloud/authoring/projects/tasks.md)
* [工作流程](/help/sites-cloud/authoring/workflows/overview.md)


## 標題{#inbox-in-the-header}中的收件箱

從任何主控台中，收件匣中目前的項目數會顯示在標題中。 也可以開啟指示器以提供對需要操作的頁面的快速訪問，或訪問收件箱：

![標頭中的收件匣概觀](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
某些動作也會顯示在適當資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)的[卡片檢視中。

## 開啟收件箱{#opening-the-inbox}

若要開啟AEM通知收件匣：

1. 按一下/點選工具列中的指示器。

1. 選擇「 **全部查看**」。「 **AEM收件匣** 」將會開啟。收件匣會顯示工作流程、專案和工作中的項目。
1. 預設視圖是「列 [表視圖](#inbox-list-view)」，但您也可以切換到「日 [歷視圖」](#inbox-calendar-view)。這是使用檢視選取器 (工具列，右上方) 完成。

   對於這兩個視圖，您也可以定義[View Settings](#inbox-view-settings)。 可用的選項取決於當前視圖。

   ![收件箱視圖設定](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
收件箱作為控制台運行，因此，在您完成 [後，使用全局導航](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)[](/help/sites-cloud/authoring/getting-started/search.md) 或搜索導航到其他位置。

### 收件箱 — 清單視圖{#inbox-list-view}

此檢視會列出所有項目，以及相關資訊：

![收件箱清單視圖](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### 收件箱 — 日曆視圖{#inbox-calendar-view}

此視圖會根據項目在日曆中的位置顯示項目：

![收件箱日曆視圖](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

您可以：

* 選擇特定視圖：**時間軸**, **列**, **清單**
* 指定要根據「計畫」顯示的 **任務**:所有 **計畫中**&#x200B;的， **進行中**, **即將到**，過 ******去的,**
* 深入鑽研，以了解有關項目的更詳細資訊
* 選取要聚焦檢視的日期範圍：

![收件匣日曆檢視日期範圍](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### 收件箱 — 查看設定{#inbox-view-settings}

對於兩個檢視（清單和日曆），您可以定義設定：

* **日曆檢視**

   對於&#x200B;**日曆視圖**，可以配置：

   * **分組依據**
   * **排程** 或無 ****
   * **卡片大小**

   ![收件箱日曆視圖設定](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **清單檢視**

   對於&#x200B;**清單視圖**，可以配置排序機制：

   * **排序**
   * **排序順序**

   ![收件箱清單視圖設定](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   您也可以將日曆委派給其他用途，以及請求其他使用者的委派及管理委派。

   ![收件箱清單視圖委派設定](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## 對項{#taking-action-on-an-item}執行操作

>[!NOTE]
雖然可以選取多個項目，但一次只能對一個項目執行動作。

1. 要對項目執行操作，請為相應項目選擇縮圖。 適用於該項目的動作圖示會顯示在工具列中：

   ![選擇收件箱項](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   這些動作適合項目，包括：

   * **** 完成動作
   * **** 刪除項目
   * **** 根據項目類型，此動作可以：

      * 顯示項目屬性
      * 開啟適當的控制面板或精靈以執行進一步動作
      * 開啟相關檔案
   * **退** 回上一步
   * 檢視工作流程的裝載
   * 從項目建立專案

   >[!NOTE]
   如需詳細資訊，請參閱：
   * 工作流程項目 — [參與工作流程](/help/sites-cloud/authoring/workflows/participating.md)


2. 會根據選取的項目啟動動作，例如：

   * 將開啟與該操作相應的對話框
   * 將啟動操作嚮導
   * 將會開啟檔案頁面

   例如， **Delegate**&#x200B;將開啟一個對話框：

   ![委派收件匣任務](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   根據是否開啟了對話框、嚮導和文檔頁，您可以：

   * 確認適當的動作，例如重新指派。
   * 取消動作
   * 選擇返回箭頭以返回收件箱，例如，如果操作嚮導或文檔頁已開啟，則可以返回收件箱。


## 建立任務{#creating-a-task}

從收件箱中，您可以建立任務：

1. 選擇&#x200B;**建立**，然後選擇&#x200B;**任務**。
1. 填寫「基本」和「進階 **」標籤中的必要欄位** (只有「 **標題****** 」是必填的，其他所有欄位都是選用的):

   * **基本**:

      * **標題**
      * **專案**
      * **被指定者**
      * **內容**（類似於裝載）是從任務到存放庫中某個位置的參考
      * **說明**
      * **任務優先順序**
      * **開始日期**
      * **到期日期**

   ![收件箱添加任務](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **進階**

      * **名稱**：這會用來形成URL，如果空白，則會以標題 **為基**。

   ![收件箱添加任務高級選項](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. 選擇&#x200B;**Submit**。

## 建立項目{#creating-a-project}

對於某些任務，您可以根據該任務建立[項目](/help/sites-cloud/authoring/projects/overview.md):

1. 點選/按一下縮圖，以選取適當的任務。

   >[!NOTE]
   只有使用&#x200B;**收件箱**&#x200B;的&#x200B;**建立**&#x200B;選項建立的任務才能用於建立項目。
   無法使用工作項（來自工作流）建立項目。

1. 從工 **具列選擇** 「建立專案」以開啟精靈。
1. 選取適當的範本，然後選取&#x200B;**Next**。
1. 指定所需的屬性：

   * **基本**

      * **標題**
      * **說明**
      * **開始日期**
      * **到期日期**
      * **** 使用者和角色
   * **進階**

      * **名稱**
   >[!NOTE]
   如需完整資訊，請參閱[建立專案](/help/sites-cloud/authoring/projects/managing.md#creating-a-project)。

1. 選擇&#x200B;**建立**&#x200B;以確認操作。

## 篩選AEM收件匣中的項目{#filtering-items-in-the-aem-inbox}

您可以篩選列出的項目：

1. 開啟&#x200B;**AEM收件匣**。

1. 開啟篩選選擇器：

   ![收件匣搜尋](/help/sites-cloud/authoring/assets/inbox-search.png)

1. 您可以根據一系列條件來篩選列出的項目，其中許多可以細化。 例如：

   ![收件箱搜索篩選器](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   使用[View Settings](#inbox-view-settings)，也可以在使用[List View](#inbox-list-view)時配置排序順序。
