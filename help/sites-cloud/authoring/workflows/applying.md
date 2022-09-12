---
title: 將工作流程套用至頁面
description: 編寫時，您可以叫用工作流程以在頁面上執行動作；也可以套用多個工作流程。
exl-id: 86e71f0e-e53e-40bc-901d-2a1ab347bd0a
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 15%

---

# 將工作流程套用至頁面 {#applying-workflows-to-pages}

編寫時，您可以叫用工作流程以在頁面上執行動作；您也可以套用多個工作流程。

套用工作流程時，需指定下列資訊：

* 要套用的工作流程。
   * 您可以套用您有權存取的任何工作流程 (由AEM管理員指派)。
* （可選）幫助標識用戶收件箱中工作流實例的標題。
* 工作流程裝載；這可以是一或多個頁面。

工作流程可從以下位置開始：

* [網站主控台](#starting-a-workflow-from-the-sites-console).
* [編輯頁面時，從頁面資訊](#starting-a-workflow-from-the-page-editor).

>[!NOTE]
>
>另請參閱:
>
>* 如何將工作流程套用至DAM資產。
>* [使用專案工作流程](/help/sites-cloud/authoring/projects/workflows.md).


<!-- 
>* [How to apply workflows to DAM assets](/help/assets/assets-workflow.md).
>* [Working with Project Workflows](/help/sites-cloud/authoring/projects/workflows.md).
-->

>[!NOTE]
>
>AEM管理員可使用其他數種方法開始工作流程。

<!-- 
>AEM administrators can [start workflows using several other methods](/help/sites-administering/workflows-starting.md).
-->

## 從Sites Console啟動工作流程 {#starting-a-workflow-from-the-sites-console}

您可以從以下任一位置啟動工作流程：

* [Sites工具欄的「建立」選項](#starting-a-workflow-from-the-sites-toolbar).
* [Sites控制台的時間軸邊欄](#starting-a-workflow-from-the-timeline).

在這兩種情況下，您需要：

* [在「建立工作流嚮導」中指定「工作流詳細資訊」](#specifying-workflow-details-in-the-create-workflow-wizard).

### 從網站工具列啟動工作流程 {#starting-a-workflow-from-the-sites-toolbar}

您可以從 **網站** 主控台：

1. 導覽至並選取所需頁面。

1. 從 **建立** 選項，您現在可以選取 **工作流程**.

   ![從工具列建立工作流程](/help/sites-cloud/authoring/assets/workflows-create-from-toolbar.png)

1. 此 **建立工作流程** 嚮導將幫助 [指定工作流詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard).

### 從時間軸啟動工作流程 {#starting-a-workflow-from-the-timeline}

從 **時間表** 您可以啟動要套用至所選資源的工作流程。

1. [選取資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 開啟 [時間表](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) （或開啟時間軸，然後選取資源）。
1. 注釋欄位旁的箭頭可用來顯示 **開始工作流程**:

   ![從時間軸建立工作流程](/help/sites-cloud/authoring/assets/workflows-create-from-timeline.png)

1. 此 **建立工作流程** 嚮導將幫助 [指定工作流詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard).

### 在建立工作流嚮導中指定工作流詳細資訊 {#specifying-workflow-details-in-the-create-workflow-wizard}

此 **建立工作流程** 精靈將協助您選取工作流程並指定所需的詳細資訊。

開啟 **建立工作流程** 嚮導，從以下任一項：

* [Sites工具欄的「建立」選項](#starting-a-workflow-from-the-sites-toolbar).
* [Sites控制台的時間軸邊欄](#starting-a-workflow-from-the-timeline).

您可以指定詳細資訊：

1. 在 **屬性** 步驟中，會定義工作流程的基本選項：

   * **工作流程模型**
   * **工作流程標題**

      * 您可以指定此例項的標題，以協助您在稍後階段進行識別。

   根據工作流模型，也提供下列選項。 這可讓工作流程完成後，保留建立為裝載的套件。

   * **保留工作流程封裝**
   * **封裝標題**

      * 您可以指定套件的標題，以協助識別。
   >[!NOTE]
   >
   >當為「 **** 多資源支援」配置了工作流且已選擇多個資源時，「保留工作流包」選項可用。

   <!--
   >The **Keep workflow package** option is available when the workflow has been configured for [Multi Resource Support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) and multiple resources have been selected.
   -->

   完成時，請使用 **下一個** 繼續。

   ![指定工作流屬性](/help/sites-cloud/authoring/assets/workflows-properties.png)

1. 在 **範圍** 步驟：

   * **新增內容** 開啟 [路徑瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) 並選擇其他資源；在瀏覽器中時，按一下/點選 **選擇** 將內容新增至工作流程例項。

   * 可查看其他動作的現有資源：

      * **包括子項** 指定將該資源的子項包含在工作流中。
將會開啟一個對話框，允許您根據以下內容優化選擇：

         * 僅包含直接子項.
         * 僅包含修改過的頁面.
         * 僅包含已發佈的頁面.

         指定的任何子項將添加到將應用工作流的資源清單中。

      * **移除選取項目** 從工作流中刪除該資源。

   ![定義工作流範圍](/help/sites-cloud/authoring/assets/workflows-scope.png)

   >[!NOTE]
   >
   >如果添加其他資源，則可以使用「上 **一步** 」( **Back** )在「屬性」(Properties)步驟中調整「保留工作流程包 **」(Keep workflow package** )的設定。

1. 使用 **建立** 關閉嚮導並建立工作流實例。 通知會顯示在Sites主控台中。

## 從頁面編輯器啟動工作流程 {#starting-a-workflow-from-the-page-editor}

編輯頁面時，您可以選取 **頁面資訊** 的上界。 下拉式功能表中有選項 **在工作流程中開始**. 這會開啟一個對話方塊，您可在其中指定所需的工作流程，並視需要加上標題：

![從頁面編輯器啟動工作流程](/help/sites-cloud/authoring/assets/workflows-create-page-editor.png)
