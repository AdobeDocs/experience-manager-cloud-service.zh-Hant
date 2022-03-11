---
title: 將工作流程套用至頁面
description: 創作時，可以調用工作流對頁面執行操作；也可以應用多個工作流……
exl-id: 86e71f0e-e53e-40bc-901d-2a1ab347bd0a
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 15%

---

# 將工作流程套用至頁面 {#applying-workflows-to-pages}

創作時，可以調用工作流對頁面執行操作；還可以應用多個工作流。

應用工作流時，可指定以下資訊：

* 要套用的工作流程。
   * 您可以套用您有權存取的任何工作流程 (由AEM管理員指派)。
* （可選）幫助標識用戶收件箱中工作流實例的標題。
* 工作流負載；這可以是一個或多個頁面。

可以從以下位置啟動工作流：

* [站點控制台](#starting-a-workflow-from-the-sites-console)。
* [編輯頁面時，從頁面資訊](#starting-a-workflow-from-the-page-editor)。

>[!NOTE]
>
>另請參閱:
>
>* 如何將工作流應用於DAM資產。
>* [使用專案工作流程](/help/sites-cloud/authoring/projects/workflows.md).


<!-- 
>* [How to apply workflows to DAM assets](/help/assets/assets-workflow.md).
>* [Working with Project Workflows](/help/sites-cloud/authoring/projects/workflows.md).
-->

>[!NOTE]
>
>管AEM理員可以使用其他幾種方法啟動工作流。

<!-- 
>AEM administrators can [start workflows using several other methods](/help/sites-administering/workflows-starting.md).
-->

## 從站點控制台啟動工作流 {#starting-a-workflow-from-the-sites-console}

您可以從以下任一位置啟動工作流：

* [「站點」工具欄的「建立」選項](#starting-a-workflow-from-the-sites-toolbar)。
* [站點控制台的時間軸軌道](#starting-a-workflow-from-the-timeline)。

在這兩種情況下，您都需要：

* [在建立工作流嚮導中指定工作流詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 從站點工具欄啟動工作流 {#starting-a-workflow-from-the-sites-toolbar}

可從 **站點** 控制台：

1. 導航到所需頁面並選擇。

1. 從 **建立** 選項 **工作流**。

   ![從工具欄建立工作流](/help/sites-cloud/authoring/assets/workflows-create-from-toolbar.png)

1. 的 **建立工作流** 嚮導將幫助 [指定工作流詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 從時間軸啟動工作流 {#starting-a-workflow-from-the-timeline}

從 **時間軸** 您可以啟動要應用於所選資源的工作流。

1. [選擇資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 開啟 [時間軸](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) （或開啟時間軸，然後選擇資源）。
1. 注釋欄位的箭頭可用於顯示 **啟動工作流**:

   ![從時間線建立工作流](/help/sites-cloud/authoring/assets/workflows-create-from-timeline.png)

1. 的 **建立工作流** 嚮導將幫助 [指定工作流詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 在建立工作流嚮導中指定工作流詳細資訊 {#specifying-workflow-details-in-the-create-workflow-wizard}

的 **建立工作流** 嚮導將幫助您選擇工作流並指定所需的詳細資訊。

開啟 **建立工作流** 嚮導：

* [「站點」工具欄的「建立」選項](#starting-a-workflow-from-the-sites-toolbar)。
* [站點控制台的時間軸軌道](#starting-a-workflow-from-the-timeline)。

您可以指定詳細資訊：

1. 在 **屬性** 步驟，定義工作流的基本選項：

   * **工作流程模型**
   * **工作流程標題**

      * 您可以為此實例指定標題，以幫助您在以後階段識別它。

   根據工作流模型，還可以使用以下選項。 這允許在工作流完成後保留建立為負載的包。

   * **保留工作流程封裝**
   * **封裝標題**

      * 您可以為包指定標題，以幫助標識。
   >[!NOTE]
   >
   >當為「 **** 多資源支援」配置了工作流且已選擇多個資源時，「保留工作流包」選項可用。

   <!--
   >The **Keep workflow package** option is available when the workflow has been configured for [Multi Resource Support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) and multiple resources have been selected.
   -->

   完成後，使用 **下一個** 繼續。

   ![指定工作流屬性](/help/sites-cloud/authoring/assets/workflows-properties.png)

1. 在 **範圍** 步驟：

   * **添加內容** 開啟 [路徑瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) 並選擇其他資源；在瀏覽器中按一下/點擊 **選擇** 中設定網格顏色。

   * 要查看附加操作的現有資源：

      * **包括子項** 指定該資源的子項將包含在工作流中。
將開啟一個對話框，允許您根據以下內容細化選擇：

         * 僅包含直接子項.
         * 僅包含修改過的頁面.
         * 僅包含已發佈的頁面.

         指定的任何子級都將添加到工作流將應用到的資源清單中。

      * **刪除所選內容** 從工作流中刪除該資源。

   ![定義工作流範圍](/help/sites-cloud/authoring/assets/workflows-scope.png)

   >[!NOTE]
   >
   >如果添加其他資源，則可以使用「上 **一步** 」( **Back** )在「屬性」(Properties)步驟中調整「保留工作流程包 **」(Keep workflow package** )的設定。

1. 使用 **建立** 關閉嚮導並建立工作流實例。 在「站點」控制台中顯示通知。

## 從頁面編輯器啟動工作流 {#starting-a-workflow-from-the-page-editor}

編輯頁面時，可以選擇 **頁面資訊** 的子菜單。 下拉菜單具有選項 **在工作流中啟動**。 這將開啟一個對話框，您可以在其中指定所需的工作流以及標題（如果需要）:

![從頁面編輯器啟動工作流](/help/sites-cloud/authoring/assets/workflows-create-page-editor.png)
