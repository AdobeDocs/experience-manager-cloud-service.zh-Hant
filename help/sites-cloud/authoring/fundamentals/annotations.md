---
title: 新增頁面註解
description: 使用批注模式在頁面上保留批注和草繪，就像使用註解幫助內容審閱過程一樣
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: 5d533354a29237aeafc00e5570ede3ab00b721fd
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 0%

---

# 新增頁面註解 {#adding-page-annotations}

為您的數位體驗建立內容通常需要在發佈前進行討論和提供意見。 為協助進行此意見反應程式，AEM可讓您將註解新增至內容。

附註會將簡單的草圖或附註（想想真實世界的便箋）放在頁面上。 註解可讓您為其他作者和審核者留下意見或問題。

>[!TIP]
>
>別忘了，[comments](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)也可用於在頁面上提供意見。

特殊的[mode](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)用於建立和查看注釋。

>[!TIP]
>
>根據您的需求，您也可以開發[workflow](/help/sites-cloud/authoring/workflows/overview.md)以在新增、更新或刪除註解時傳送通知。

## 注釋指示器{#annotation-indicator}

註解不會在「編輯」模式中顯示，但工具列右上角的徽章會顯示目前頁面有多少註解。 徽章會取代預設的「註解」圖示，但仍可作為快速連結，切換至「注釋」模式或從「注釋」模式切換：

![注釋指示器](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## 注釋模式{#annotate-mode}

注釋僅在「注釋」模式中可見。

1. 編輯頁面時，您可使用工具列（右上）中的圖示進入「注釋」模式：

   ![註解按鈕](/help/sites-cloud/authoring/assets/annotations.png)

   您現在可以檢視任何現有的註解。

   ![註解範例](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 按一下或點選注釋以開啟注釋對話框並查看其詳細資訊。

   ![註解詳細資訊](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 若要退出「注釋」模式，並返回先前使用的模式，請點選/按一下頂端工具列右側的x按鈕。

## 添加和編輯注釋{#annotating-a-component}

除了檢視註解外，「注釋」模式還可讓您在內容上建立、編輯、移動或刪除註解

1. [在頁面上](#annotate-mode) 開始注釋模型。

1. 按一下或點選「添加註釋」表徵圖（工具欄左側的加號）以開始添加註釋。

1. 按一下或點選所需元件（可以注釋的元件將用藍色邊框突出顯示）以添加註釋並開啟對話框：

   ![添加註釋](/help/sites-cloud/authoring/assets/annotation-adding.png)

   在此，您可以使用適當的欄位和/或圖示來：

   * 輸入注釋文本。
   * 建立草繪（線和形狀）以加亮元件的區域。

      ![「注釋草繪」(Annotation Sketch)按鈕](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      建立草繪時，游標將更改為交叉軸。 可以繪製多條不同的線。 草繪線反映注釋顏色，可以是箭頭、圓或橢圓。

   * 選擇或更改顏色：

      ![批注色板按鈕](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. 通過按一下或點選對話框外部，可以關閉注釋對話框。 將顯示注釋的截斷視圖以及任何草繪：

   ![注釋草繪](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 完成特定注釋的編輯後，可以：

   * 按一下或點選文字標籤以開啟註解。 開啟後，您可以查看全文、進行更改，或刪除注釋。](#deleting-annotations)[
   * 重新定位文本標籤。
   * 按一下或點選草繪線以選取該草繪，並將其拖動到所需位置。
   * 移動或複製元件
      * 所有相關注釋及其草圖也將被移動或複製，但它們相對於段落的位置將保持不變。


>[!NOTE]
>
>註解無法添加到已被其他用戶鎖定的頁面。

>[!NOTE]
>
>單個元件類型的定義確定是否可在該元件的實例上添加註釋。

## 刪除注釋和草繪{#deleting-annotations}

可刪除注釋及其相關草繪。

1. [在頁面上](#annotate-mode) 開始注釋模型。

1. 按一下/點選文字標籤以開啟註解。

1. 按一下或點選「刪除」圖示。

   ![刪除注釋](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. 將刪除注釋和所有相關草繪。

>[!NOTE]
>
>刪除元件會刪除附加到該資源的所有注釋和草繪，而不考慮它們在整個頁面上的位置。

## 僅刪除草繪{#deleting-sketches}

只能刪除特定草繪，而不能刪除包含所有關聯草繪的整個注釋。

1. [在頁面上](#annotate-mode) 開始注釋模型。

1. 按一下或點選草繪。 AEM會以較深的藍色方塊醒目顯示。

   ![選取要刪除的草繪](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. 按鍵盤上的Delete鍵。

1. 草繪被刪除，但注釋仍然保留。

## 為其他資源{#annotating-other-resources}添加註釋

除了元件，您也可以為各種資源加上注釋：

* 為資產加上註解[為資產加上註解](/help/assets/manage-digital-assets.md#annotating)
* 為視訊資產加上註解[為視訊資產加上註解](/help/assets/manage-video-assets.md#annotate-video-assets)
