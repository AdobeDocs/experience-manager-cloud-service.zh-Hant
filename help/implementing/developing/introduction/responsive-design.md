---
title: 回應式設計
description: 透過回應式設計，以多個方向在多個裝置上有效顯示相同的體驗
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# 回應式設計 {#responsive-design}

設計您的體驗，使其能適應其顯示所在的用戶端檢視區。 透過回應式設計，相同的頁面可以兩種方向有效地顯示在多個裝置上。 下列影像示範頁面可以透過哪些方式回應檢視區大小的變更：

* 配置：對較小的視區使用單列佈局，對較大的視區使用多列佈局。
* 文本大小：在較大的檢視區中使用較大的文字大小（如適當，例如標題）。
* 內容：在較小的裝置上顯示時，僅包含最重要的內容。
* 導覽：提供裝置專用工具，供存取其他頁面。
* 影像：根據視窗尺寸提供適合用戶端檢視區的影像轉譯。

![回應式設計範例](assets/responsive-example.png)

開發Adobe Experience Manager(AEM)應用程式，產生可適應多種視窗大小和方向的HTML5。 例如，下列檢視區寬度範圍對應於各種裝置類型和方向

* 最大寬度為480像素（手機、縱向）
* 最大寬度為767像素（手機、橫向）
* 寬度介於768像素和979像素（平板電腦、縱向）之間
* 寬度介於980像素和1199像素（平板電腦、橫向）之間
* 寬度為1200px或更高（台式機）

如需實作回應式設計行為的相關資訊，請參閱下列主題：

* [媒體查詢](#using-media-queries)
* [流體網格](#developing-a-fluid-grid)
* [最適化影像](#using-adaptive-images)

在設計時，請使用 **模擬器** 工具列來預覽不同螢幕大小的頁面。

## 開發之前 {#before-you-develop}

在開發支援您網頁的AEM應用程式之前，應先做出幾項設計決策。 例如，您需要下列資訊：

* 您正在定位的裝置
* 目標檢視區大小
* 每個目標檢視區大小的頁面配置

### 應用程式結構 {#application-structure}

典型的AEM應用程式結構支援所有回應式設計實施：

* 頁面元件位於下方 `/apps/<application_name>/components`
* 範本位於下方 `/apps/<application_name>/templates`

## 使用媒體查詢 {#using-media-queries}

媒體查詢可讓您選擇性使用CSS樣式來呈現頁面。 AEM開發工具和功能可讓您有效且有效地在應用程式中實施媒體查詢。

W3C群組提供 [媒體查詢](https://www.w3.org/TR/css3-mediaqueries/) 說明此CSS3功能和語法的建議。

### 建立CSS檔案 {#creating-the-css-file}

在您的CSS檔案中，根據您所定位裝置的屬性定義媒體查詢。 下列實施策略對於管理每個媒體查詢的樣式是有效的：

* 使用 [客戶端庫資料夾](clientlibs.md) 定義呈現頁面時組合的CSS。
* 在個別CSS檔案中定義每個媒體查詢及相關的樣式。 使用代表媒體查詢之裝置功能的檔案名稱會很實用。
* 定義個別CSS檔案中所有裝置通用的樣式。
* 在「客戶端庫」資料夾的css.txt檔案中，按照組合的CSS檔案中的需要對清單CSS檔案進行排序。

此 [WKND教學課程](develop-wknd-tutorial.md) 使用此策略來定義網站設計中的樣式。 WKND使用的CSS檔案位於 `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
