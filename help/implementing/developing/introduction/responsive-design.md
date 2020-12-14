---
title: 自適應設計
description: 透過互動式設計，以多種方向在多種裝置上有效顯示相同的體驗
translation-type: tm+mt
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# 自適應設計{#responsive-design}

設計您的體驗，以配合客戶的檢視區顯示。 透過多方互動設計，可以在多種裝置上以兩種方向有效顯示相同的頁面。 下列影像示範頁面回應檢視區大小變更的一些方式：

* 版面配置：對較小的視區使用單欄版面，對較大的視區使用多欄版面。
* 文字大小：在較大的檢視區中使用較大的文字大小（如適當時，例如標題）。
* 內容：在較小的裝置上顯示時，僅包含最重要的內容。
* 導覽：提供裝置專用工具以存取其他頁面。
* 影像：根據視窗尺寸，為客戶端視區提供適合的影像轉譯。

![自適應設計範例](assets/responsive-example.png)

開發Adobe Experience Manager(AEM)應用程式，以產生可適應多種視窗尺寸和方向的HTML5。 例如，下列視區寬度範圍與各種裝置類型和方向相對應

* 最大寬度為480像素（手機、縱向）
* 最大寬度為767像素（手機、橫向）
* 768像素和979像素之間的寬度（平板電腦、縱向）
* 寬度介於980像素和1199像素（平板電腦、橫向）
* 寬度為1200像素或更高（桌上型）

如需實作互動式設計行為的相關資訊，請參閱下列主題：

* [媒體查詢](#using-media-queries)
* [流體格線](#developing-a-fluid-grid)
* [最適化影像](#using-adaptive-images)

在設計時，使用&#x200B;**Emulator**&#x200B;工具列來預覽各種螢幕大小的頁面。

## 開發{#before-you-develop}之前

在您開發支援網頁的AEM應用程式之前，應先做幾項設計決策。 例如，您需要有下列資訊：

* 您要定位的裝置
* 目標視區大小
* 每個目標視區大小的頁面佈局

### 應用程式結構{#application-structure}

典型的AEM應用程式結構支援所有互動式設計實作：

* 頁面元件位於`/apps/<application_name>/components`下方
* 範本位於`/apps/<application_name>/templates`下方

## 使用媒體查詢{#using-media-queries}

媒體查詢可選擇性使用CSS樣式來轉換頁面。 AEM開發工具和功能可讓您在應用程式中有效且有效率地建置媒體查詢。

W3C群組提供描述此CSS3功能和語法的[媒體查詢](https://www.w3.org/TR/css3-mediaqueries/)建議。

### 建立CSS檔案{#creating-the-css-file}

在CSS檔案中，根據您所定位裝置的屬性來定義媒體查詢。 以下實施策略對於管理每個媒體查詢的樣式非常有效：

* 使用[Client Library資料夾](clientlibs.md)來定義呈現頁面時組合的CSS。
* 在個別的CSS檔案中定義每個媒體查詢和相關的樣式。 使用代表媒體查詢裝置功能的檔案名稱很實用。
* 在個別的CSS檔案中定義所有裝置通用的樣式。
* 在「用戶端程式庫」檔案夾的css.txt檔案中，依組合的CSS檔案中的要求來排序清單CSS檔案。

[WKND教學課程](develop-wknd-tutorial.md)使用此策略來定義網站設計中的樣式。 WKND使用的CSS檔案位於`/apps/wknd/clientlibs/clientlib-grid/less/grid.less`。
