---
title: 響應性設計
description: 通過響應性設計，可以在多個設備上以多個方向有效地顯示相同的體驗
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# 響應性設計 {#responsive-design}

設計您的體驗，使其適應顯示這些體驗的客戶端視圖。 通過響應設計，在兩個方向上的多個設備上可以有效地顯示相同的頁面。 下圖演示了頁面響應視區大小變化的一些方法：

* 佈局：對較小的視區使用單列佈局，對較大的視區使用多列佈局。
* 文本大小：在較大的視區中使用較大的文本大小（如適當時，如標題）。
* 內容：在較小的設備上顯示時，僅包括最重要的內容。
* 導航：提供了用於訪問其它頁面的設備特定工具。
* 影像：根據窗口尺寸提供適合客戶端視區的影像格式副本。

![響應性設計示例](assets/responsive-example.png)

開發Adobe Experience Manager(AEM)應用程式，生成適應多個窗口大小和方向的HTML5。 例如，以下視區寬度範圍對應於各種設備類型和方向

* 最大寬度為480像素（電話、縱向）
* 最大寬度為767像素（電話、橫向）
* 768像素和979像素之間的寬度（平板、縱向）
* 寬度介於980像素和1199像素之間（平板、橫向）
* 寬度為1200px或更高（台式機）

有關實施響應性設計行為的資訊，請參閱以下主題：

* [媒體查詢](#using-media-queries)
* [流體網格](#developing-a-fluid-grid)
* [自適應影像](#using-adaptive-images)

在設計時，使用 **模擬器** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

## 在開發之前 {#before-you-develop}

在開發支AEM持網頁的應用程式之前，應作出若干設計決定。 例如，您需要具有以下資訊：

* 您的目標設備
* 目標視區大小
* 每個目標視區大小的頁面佈局

### 應用程式結構 {#application-structure}

典型的應AEM用程式結構支援所有響應性設計實現：

* 頁面元件位於下面 `/apps/<application_name>/components`
* 模板位於下方 `/apps/<application_name>/templates`

## 使用媒體查詢 {#using-media-queries}

媒體查詢允許選擇性使用CSS樣式進行頁面呈現。 開發工AEM具和功能使您能夠高效地在應用程式中實施介質查詢。

W3C組提供 [媒體查詢](https://www.w3.org/TR/css3-mediaqueries/) 描述此CSS3功能和語法的建議。

### 建立CSS檔案 {#creating-the-css-file}

在CSS檔案中，根據所針對設備的屬性定義媒體查詢。 以下實施策略對於管理每個媒體查詢的樣式是有效的：

* 使用 [客戶端庫資料夾](clientlibs.md) 定義呈現頁面時組裝的CSS。
* 在單獨的CSS檔案中定義每個媒體查詢和關聯樣式。 使用表示媒體查詢的設備功能的檔案名非常有用。
* 在單獨的CSS檔案中定義所有設備通用的樣式。
* 在「客戶端庫」資料夾的css.txt檔案中，按裝配的CSS檔案中的要求對清單CSS檔案進行排序。

的 [WKND教程](develop-wknd-tutorial.md) 使用此策略在站點設計中定義樣式。 WKND使用的CSS檔案位於 `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`。
