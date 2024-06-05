---
title: 新增頁面註解
description: 使用註解模式，像使用註解一樣在頁面上留下註解和草圖，以協助您的內容檢閱程式
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# 新增頁面註解 {#adding-page-annotations}

為您的數位體驗建立內容通常需要在發佈前進行討論和提出意見。 為協助進行回饋意見程式，AEM可讓您將註解新增至內容。

註解會在頁面上放置簡單的草圖或註解（想象一下真實世界的註解）。 註解可讓您為其他作者和檢閱者留下評論或問題。

>[!TIP]
>
>別忘了 [評論](/help/sites-cloud/authoring/basic-handling.md#timeline) 也可在頁面上提供意見回饋。

一個特殊 [模式](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) 用於建立和檢視註解。

>[!TIP]
>
>您也可以根據您的需求，開發 [工作流程](/help/sites-cloud/authoring/workflows/overview.md) 以在新增、更新或刪除註解時傳送通知。

## 附註指示器 {#annotation-indicator}

註解不會在編輯模式中顯示，但工具列右上方的徽章會顯示目前頁面有多少注解。 徽章會取代預設的「註解」圖示，但仍可當作快速連結，切換至「註解」模式/從「註解」模式切換：

![附註指示器](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## 附註模式 {#annotate-mode}

註解僅在註解模式下可見。

1. 編輯頁面時，請使用工具列（右上方）中的圖示進入附註模式：

   ![註解按鈕](/help/sites-cloud/authoring/assets/annotations.png)

   您現在可以檢視任何現有的註解。

   ![附註範例](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 選取註釋以開啟註釋對話方塊並檢視其詳細資訊。

   ![附註詳細資料](/help/sites-cloud/authoring/assets/annotation-adding.png)

1. 若要退出「註釋」模式並返回先前使用的模式，請選取頂端工具列右側的x按鈕。

## 新增和編輯註解 {#annotating-a-component}

除了檢視註解之外，「註解」模式還允許您在內容上建立、編輯、移動或刪除註解

1. [啟動附註模式](#annotate-mode) 在頁面上。

1. 選取「加入註釋」(Add Annotation)圖示（工具列左側的加號）以開始加入註釋。

1. 選取所需的元件（可加上註解的元件會以藍色邊框反白顯示）以新增註解，並開啟對話方塊：

   ![新增註解](/help/sites-cloud/authoring/assets/annotation-adding.png)

   在這裡，您可以使用適當的欄位和/或圖示來：

   * 輸入註解文字。
   * 建立草圖（線條和形狀）以反白元件的某個區域。

     ![註釋草圖按鈕](/help/sites-cloud/authoring/assets/annotation-sketch.png)

     建立草繪時，游標會變成十字線。 您可以繪製多條不同的線條。 草繪線會反映註釋顏色，可以是箭頭、圓或橢圓形。

   * 選擇或變更顏色：

     ![附注色票按鈕](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. 您可以按一下或點選註釋對話方塊外部，以關閉該對話方塊。 隨即顯示截斷的註釋檢視及任何草圖：

   ![註釋草圖](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 編輯完特定註解後，您可以：

   * 選取文字標籤以開啟附註。 開啟後，即可檢視全文、進行變更，或 [刪除註解。](#deleting-annotations)
   * 重新定位文字標籤。
   * 選取草繪線以選取該草繪，並將其拖曳至所需位置。
   * 移動或複製元件
      * 也會移動或複製任何相關的註釋及其草圖，但它們相對於段落的位置將保持相同。


>[!NOTE]
>
>註解無法新增至已由其他使用者鎖定的頁面。

>[!NOTE]
>
>個別元件型別的定義決定是否可在該元件的例證上新增註釋。

## 刪除註釋和草繪 {#deleting-annotations}

可以刪除註釋及其關聯的草圖。

1. [啟動附註模式](#annotate-mode) 在頁面上。

1. 選取文字標籤以開啟附註。

1. 選取刪除圖示。

   ![刪除註解](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. 註釋及所有關聯的草繪都會被刪除。

>[!NOTE]
>
>刪除元件會刪除附加到該資源的所有註釋和草圖，無論這些註釋和草圖在整個頁面上的位置為何。

## 僅刪除草繪 {#deleting-sketches}

您只能刪除特定草繪，而非刪除具有所有關聯草繪的整個註釋。

1. [啟動附註模式](#annotate-mode) 在頁面上。

1. 選取草繪。 AEM會以較暗的藍色方塊反白顯示。

   ![選取要刪除的草圖](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. 按鍵盤上的Delete鍵。

1. 草繪即被刪除，但註釋仍會保留。

## 為其他資源加上註解 {#annotating-other-resources}

除了元件以外，您還可以為各種資源加上註解：

* 為資產加上註釋 [為資產加上註釋](/help/assets/manage-digital-assets.md#annotating)
* 為視訊資產加上註解 [為視訊資產加上註解](/help/assets/manage-video-assets.md#annotate-video-assets)
