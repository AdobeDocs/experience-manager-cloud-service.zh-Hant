---
title: 新增頁面註解
description: 使用注釋模式將注釋和草繪保留在頁面上，就像使用便箋來幫助內容審閱過程一樣
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: 64d801b108229866394e993811a67f983be5df6c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 新增頁面註解 {#adding-page-annotations}

為您的數字型驗建立內容通常需要在發佈前進行討論和反饋。 為幫助此反饋過程，AEM允許您向內容添加註釋。

注釋將簡單的草繪或注釋（想想現實世界的便箋）放在頁面上。 注釋允許您為其他作者和審閱者留下注釋或問題。

>[!TIP]
>
>別忘了 [評論](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) 也可用於在頁面上提供反饋。

特殊 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 用於建立和查看注釋。

>[!TIP]
>
>根據您的要求，您還可以開發 [工作流](/help/sites-cloud/authoring/workflows/overview.md) 在添加、更新或刪除注釋時發送通知。

## 注釋指示器 {#annotation-indicator}

注釋不會在「編輯」模式下顯示，但工具欄右上角的標籤顯示當前頁面存在多少注釋。 標籤將替換預設的「注釋」表徵圖，但仍作為快速連結使用，可切換到/從「注釋」模式：

![注釋指示器](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## 注釋模式 {#annotate-mode}

批注僅在「批注」模式下可見。

1. 編輯頁面時，使用工具欄（右上）中的表徵圖進入「注釋」模式：

   ![「注釋」按鈕](/help/sites-cloud/authoring/assets/annotations.png)

   現在，您可以查看任何現有批注。

   ![注釋示例](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 按一下或點擊注釋以開啟注釋對話框並查看其詳細資訊。

   ![注釋詳細資訊](/help/sites-cloud/authoring/assets/annotation-adding.png)

1. 要退出「注釋」模式並返回到先前使用的模式，請點擊/按一下頂部工具欄右側的x按鈕。

## 添加和編輯注釋 {#annotating-a-component}

除了查看注釋外，「注釋」模式還允許您在內容上建立、編輯、移動或刪除注釋

1. [啟動注釋模式](#annotate-mode) 的下一頁。

1. 按一下或按一下「添加註釋」表徵圖（工具欄左側的加號）開始添加註釋。

1. 按一下或點擊所需元件（可注釋的元件將用藍色邊框加亮）以添加註釋並開啟對話框：

   ![添加註釋](/help/sites-cloud/authoring/assets/annotation-adding.png)

   在此，您可以使用相應的欄位和/或表徵圖：

   * 輸入注釋文本。
   * 建立草繪（線和形狀）以加亮元件的區域。

      ![「注釋草繪」按鈕](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      建立草繪時，游標將變為十字線。 可以繪製多條不同的線條。 草繪線反映注釋顏色，可以是箭頭、圓或橢圓。

   * 選擇或更改顏色：

      ![「注釋顏色樣本」按鈕](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. 可通過按一下或在對話框外部點擊來關閉注釋對話框。 注釋的截斷視圖以及任何草繪顯示如下：

   ![注釋草繪](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 編輯完特定注釋後，可以：

   * 按一下或點擊文本標籤以開啟注釋。 開啟後，您可以查看全文、進行更改或 [刪除注釋。](#deleting-annotations)
   * 重新定位文本標籤。
   * 按一下或點擊草繪線以選取該草繪並將其拖動到所需位置。
   * 移動或複製元件
      * 所有相關注釋及其草圖也將被移動或複製，但它們相對於段落的位置將保持不變。


>[!NOTE]
>
>無法將批注添加到已由其他用戶鎖定的頁面。

>[!NOTE]
>
>單個元件類型的定義確定是否可能（或否）在該元件實例上添加註釋。

## 刪除注釋和草繪 {#deleting-annotations}

可以刪除注釋及其相關的草繪。

1. [啟動注釋模式](#annotate-mode) 的下一頁。

1. 按一下/點擊文本標籤以開啟注釋。

1. 按一下或點擊「刪除」表徵圖。

   ![刪除注釋](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. 注釋和所有相關草繪均被刪除。

>[!NOTE]
>
>刪除元件將刪除附加到該資源的所有注釋和草繪，而不考慮它們在整個頁面上的位置。

## 僅刪除草繪 {#deleting-sketches}

只能刪除特定草繪，而不能刪除所有相關草繪的整個注釋。

1. [啟動注釋模式](#annotate-mode) 的下一頁。

1. 按一下或點擊草繪。 用深AEM藍色的盒子加亮。

   ![選取要刪除的草繪](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. 按鍵盤上的「Delete（刪除）」鍵。

1. 草繪被刪除，但注釋仍保留。

## 注釋其他資源 {#annotating-other-resources}

除了元件外，還可以注釋各種資源：

* 注釋資產 [注釋資產](/help/assets/manage-digital-assets.md#annotating)
* 注釋視頻資產 [注釋視頻資產](/help/assets/manage-video-assets.md#annotate-video-assets)
