---
title: 您的收件匣
description: 使用收件箱管理任務
translation-type: tm+mt
source-git-commit: 672f1483c017d791365173c91b0bee5c44c33535
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 17%

---


# 您的收件匣 {#your-inbox}

您可以從AEM的各個區域收到通知，包括工作流程和專案。 例如，您可能會收到有關以下內容的通知：

* 任務：
   * 您也可以在AEM UI的不同點建立這些項目，例如在「專案」 **下**。
   * 這些可以是工作流「建立任務」 **或「建立****項目任務」步驟的產品** 。
* 工作流程:
   * 代表您需要對頁面內容執行之動作的工作項目
      * 這些是工作流參與者步 **驟的產** 品。
   * 失敗項目，允許管理員重試失敗的步驟

您會在自己的收件箱中收到這些通知，您可以在其中查看通知並採取措施。

>[!NOTE]
>
>有關項目類型的詳細資訊，另請參閱：
>
>* [專案](/help/sites-cloud/authoring/projects/overview.md)
>* [項目——使用任務](/help/sites-cloud/authoring/projects/tasks.md)
>* [工作流程](/help/sites-cloud/authoring/workflows/overview.md)


## 頁首中的收件箱 {#inbox-in-the-header}

在任何控制台中，收件匣中的目前項目數會顯示在標題中。 也可以開啟指示器，以提供對需要執行操作的頁面的快速訪問或對收件箱的訪問：

![標題中的收件匣概述](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>某些動作也會顯示在適 [當資源的卡片檢視中](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)。

## 開啟收件箱 {#opening-the-inbox}

若要開啟AEM通知收件匣：

1. 按一下／點選工具列中的指標。

1. 選擇「 **全部查看**」。「 **AEM收件匣** 」將會開啟。收件匣會顯示工作流程、專案和工作中的項目。
1. 預設視圖是「列 [表視圖](#inbox-list-view)」，但您也可以切換到「日 [歷視圖」](#inbox-calendar-view)。這是使用檢視選取器 (工具列，右上方) 完成。

   您也可以針對這兩種檢視定義「檢 [視設定」](#inbox-view-settings)。 可用的選項取決於當前視圖。

   ![收件箱視圖設定](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>收件箱作為控制台運行，因此，在您完成 [後，使用全局導航](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)[](/help/sites-cloud/authoring/getting-started/search.md) 或搜索導航到其他位置。

### 收件箱——清單視圖 {#inbox-list-view}

此視圖列出了所有項目，以及相關資訊：

![收件箱清單視圖](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### Inbox - Calendar View {#inbox-calendar-view}

此視圖根據項目在日曆中的位置顯示項目：

![收件匣日曆檢視](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

您可以：

* 選擇特定視圖： **時間軸**、 **欄**、清 **單**
* 指定要根據「計畫」顯示的 **任務**:所有 **計畫中**&#x200B;的， **進行中**, **即將到**，過 ******去的,**
* 深入查看項目的詳細資訊
* 選擇日期範圍以集中檢視：

![收件匣日曆檢視日期範圍](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### 收件箱——查看設定 {#inbox-view-settings}

您可以針對兩種檢視（清單和日曆）定義設定：

* **日曆檢視**

   對於 **日曆視圖** ，您可以配置：

   * **分組依據**
   * **排程** 或無 ****
   * **卡片大小**

   ![收件匣行事歷檢視設定](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **清單檢視**

   對於 **清單視圖** ，您可以配置排序機制：

   * **排序方式**
   * **排序順序**

   ![收件箱清單視圖設定](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   您也可以將日曆委派給其他用途，以及要求其他使用者委派並管理您的委派。

   ![收件箱清單視圖委派設定](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## 對項目採取操作 {#taking-action-on-an-item}

>[!NOTE]
>
>雖然可以選取多個項目，但一次只能對一個項目採取動作。

1. 若要對項目採取動作，請選取適當項目的縮圖。 適用於該項目的動作圖示會顯示在工具列中：

   ![選擇收件箱項目](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   這些操作適合項目，包括：

   * **完整動作** (Complete action)
   * **委派** 項目
   * **開啟項目** ，視項目類型而定，此動作可以：

      * 顯示項目屬性
      * 開啟適當的控制面板或精靈以執行進一步動作
      * 開啟相關檔案
   * **退回** 至上一步
   * 檢視工作流程的裝載
   * 從項目建立專案

   >[!NOTE]
   >
   >如需詳細資訊，請參閱：
   >
   >* 工作流程項目- [參與工作流程](/help/sites-cloud/authoring/workflows/participating.md)


2. 根據所選項目，將啟動一個操作，例如：

   * 將開啟與操作相適應的對話框
   * 將啟動操作嚮導
   * 將會開啟檔案頁面

   例如， **Delegate** 將開啟一個對話框：

   ![委派收件箱任務](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   視對話方塊、精靈和檔案頁面是否已開啟而定，您可以：

   * 確認適當的動作，例如重新指派。
   * 取消動作
   * 選擇返回收件箱的後箭頭，例如，如果操作嚮導或文檔頁面已開啟，則可以返回收件箱。


## 建立任務 {#creating-a-task}

您可以從收件箱建立任務：

1. 依次選擇 **建立**、 **任務**。
1. 填寫「基本」和「進階 **」標籤中的必要欄位** (只有「 **標題****** 」是必填的，其他所有欄位都是選用的):

   * **基本**:

      * **標題**
      * **專案**
      * **被指定者**
      * **內容**（類似於裝載）是從任務到儲存庫中某個位置的引用
      * **說明**
      * **任務優先順序**
      * **開始日期**
      * **到期日期**

   ![收件箱添加任務](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **進階**

      * **名稱**：這將用來形成URL，如果空白則會以標題為 **基礎**。

   ![收件箱添加任務高級選項](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. 選擇 **提交**。

## 建立專案 {#creating-a-project}

對於某些任務，您可以基 [於該任務](/help/sites-cloud/authoring/projects/overview.md) 建立項目：

1. 點選／按一下縮圖，以選取適當的工作。

   >[!NOTE]
   >
   >只有使用「收件匣」 **的「建立** 」選項建立的 **任務** ，才能用於建立專案。
   >
   >工作項目（來自工作流）不能用於建立項目。

1. 從工 **具列選擇** 「建立專案」以開啟精靈。
1. Select the appropriate template, then **Next**.
1. 指定所需的屬性：

   * **基本**

      * **標題**
      * **說明**
      * **開始日期**
      * **到期日期**
      * **使用者** 和角色
   * **進階**

      * **名稱**
   >[!NOTE]
   >
   >如需 [完整資訊，請參閱](/help/sites-cloud/authoring/projects/managing.md#creating-a-project) 「建立專案」。

1. 選擇 **建立** ，確認操作。

## 篩選AEM收件匣中的項目 {#filtering-items-in-the-aem-inbox}

您可以篩選列出的項目：

1. 開啟 **AEM收件匣**。

1. 開啟篩選選擇器：

   ![收件箱搜索](/help/sites-cloud/authoring/assets/inbox-search.png)

1. 您可以依據一系列標準來篩選列出的項目，其中許多標準可加以調整。 例如：

   ![收件箱搜索篩選器](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >使用 [「檢視設定](#inbox-view-settings) 」 [，您也可以在使用「清單檢視」時設定排序](#inbox-list-view)順序。
