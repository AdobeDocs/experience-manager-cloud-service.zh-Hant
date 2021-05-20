---
title: 新增頁面註解
description: 許多與內容直接相關的元件允許您添加註釋
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# 新增頁面註解 {#adding-page-annotations}

將內容新增至網站的頁面通常要經過實際發佈前的討論。 為此，許多與內容直接相關的元件（例如，與版面相對）允許您添加註釋。

註解會將彩色草繪或便箋放置在頁面上。 註解可讓您（或其他使用者）為其他作者/審核者留下意見和/或問題。

>[!NOTE]
>
>別忘了，[comments](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)也可用於在頁面上提供意見。

## 註解 {#annotations}

特殊的[mode](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)用於建立和查看注釋。

>[!CAUTION]
>
>刪除資源（例如元件）會刪除附加到該資源的所有注釋和草繪，而不管它們在整個頁面上的位置如何。

>[!NOTE]
>
>您也可以根據您的需求開發工作流程，以在新增、更新或刪除註解時傳送通知。

### 為元件{#annotating-a-component}加上註解

「注釋」模式可讓您在內容上建立、編輯、移動或刪除注釋：

1. 編輯頁面時，您可以使用工具列（右上）中的圖示，進入「注釋」模式：

   ![註解按鈕](/help/sites-cloud/authoring/assets/annotations.png)

   您現在可以檢視任何現有的註解。

   >[!NOTE]
   >
   >要退出「注釋」模式，請點選/按一下頂部工具欄右側的「注釋」表徵圖（x符號）。

1. 按一下/點選「新增附註」圖示（工具列左側的加號）以開始新增附註。

   >[!NOTE]
   >
   >若要停止新增註解（並返回檢視），請點選/按一下頂端工具列左側的「取消」圖示（白色圓圈中的x符號）。

1. 按一下/點選所需元件（可以注釋的元件將用藍色邊框突出顯示）以添加註釋並開啟對話框：

   ![添加註釋](/help/sites-cloud/authoring/assets/annotation-adding.png)

   在此，您可以使用適當的欄位和/或圖示來：

   * 輸入注釋文本。
   * 建立草繪（線和形狀）以加亮元件的區域。

      ![「注釋草繪」(Annotation Sketch)按鈕](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      建立草繪時，游標將更改為交叉軸。 可以繪製多條不同的線。 草繪線反映注釋顏色，可以是箭頭、圓或橢圓。

   * 選擇/變更顏色：

      ![批注色板按鈕](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

   * 刪除注釋。

      ![注釋刪除按鈕](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. 通過按一下/點選對話框外部，可以關閉注釋對話框。 注釋的截斷視圖（第一個字）和任何草繪一起顯示：

   ![注釋草繪](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 完成特定注釋的編輯後，可以：

   * 按一下/點選文字標籤以開啟註解。 開啟後，您可以查看全文，進行更改或刪除注釋。

      * 無法獨立於注釋刪除草繪。
   * 重新定位文本標籤。
   * 按一下/點選草繪線以選取該草繪，並將其拖動到所需位置。
   * 移動或複製元件

      * 所有相關注釋及其草繪也將被移動或複製，它們相對於段落的位置將保持不變。


1. 要退出「注釋」模式，並返回以前使用的模式，請點選/按一下頂部工具欄右側的「注釋」表徵圖（x符號）。

>[!NOTE]
>
>註解無法添加到已被其他用戶鎖定的頁面。

>[!NOTE]
>
>單個元件類型的定義確定是否可在該元件的實例上添加註釋。

## 注釋指示器{#annotation-indicator}

註解不會在「編輯」模式中顯示，但工具列右上角的徽章會顯示目前頁面有多少註解。 徽章會取代預設的「註解」圖示，但仍可作為快速連結，切換至「注釋」模式或從「注釋」模式切換：

![注釋指示器](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## 為其他資源{#annotating-other-resources}添加註釋

除了元件，您也可以為各種資源加上注釋：

* 為資產加上註解[為資產加上註解](/help/assets/manage-digital-assets.md#annotating)
* 為視訊資產加上註解[為視訊資產加上註解](/help/assets/manage-video-assets.md#annotate-video-assets)
