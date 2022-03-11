---
title: 管理產品目錄頁和模板
description: 瞭解如何管理產品目錄頁和模板
exl-id: 0d795d85-c865-40d5-941e-e02ee96fdd11
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# 管理產品目錄頁和模板 {#product-catalog}

瞭解如何管理產品目錄頁面和模板。

## 到目前為止的故事 {#story-so-far}

在「內容和商AEM業」創作過程的上一文檔中， [CIF創作基礎AEM知識入門](getting-started.md)你學了CIF創作的基礎。

本文基於這些基本原理。

## 目標 {#objective}

本文檔可幫助您瞭解如何管理產品目錄頁面和模板。 閱讀完後，您應：

* 瞭解目錄模板的概念
* 一般模板如何工作
* 已建立單個模板

## 基本概念 {#basic-concept}

Venia店面提供典型的產品目錄體驗，包括導航、登陸、類別(PLP)和產品詳細資訊頁面(PDP)。

使用CIF目錄模板和即時產品資料動態生成AEM目錄頁，該即時產品資料在需要時從商業端點提取。 每個目錄都有一個產品頁和類別頁的通用模板。
![目錄結構](assets/catalog-structure.png)

導航元件顯示內容和目錄頁。 可以在導航中顯示目錄登錄頁或第一級類別。 懸停在類別上將顯示第二級類別作為第二行。
![目錄導航](assets/catalog-navigation.png)

按一下某個類別將開啟該類別頁（或產品清單頁）。

![PLP](assets/catalog-plp.png)

按一下產品將開啟產品詳細資訊頁面。

![PLP](assets/catalog-pdp.png)

## 模板 {#templates}

### 通用模板 {#generic}

通用Venia目錄模板使用「產品清單核心元件」。 此元件顯示類別影像（如果可用）和類別中的產品。
![類別模板](assets/category-template.png)

通用Venia產品模板使用「產品詳細資訊核心元件」。 此元件顯示各種產品類型的產品資訊和添加到購物車操作。
![產品模板](assets/product-template.png)

### 編輯模板 {#edit-templates}

可以通過直接開啟模板頁面或在瀏覽產品目錄頁面時切換到編輯模式來編輯模板。 請記住，更改頁面將更改模板，而不僅是產品/類別的特定頁面。

### 類別或產品特定模板 {#specific}

CIF只需按一下幾下即可支援多個模板。 要建立另一個模板，請從相應類別中選擇通用模板，然後使用 **建立** 操作。

![建立模板頁](assets/create-template-page.png)

選擇相應的產品或類別模板。

![建立模板選擇](assets/create-template-select.png)

輸入標題並建立頁面。

![建立模板輸入](assets/create-template-enter.png)

請注意，現在在通用模板下有一個特定模板。

![建立模板層次](assets/create-template-hierachry.png)

開啟模板。 它與一般類別模板完全相似。

![新建模板](assets/create-template-new.png)

在頁面頂部添加任何影像。

![建立模板更新](assets/create-template-update.png)

可以使用任何類別/產品預覽模板。 開啟 **頁面資訊** ，然後選擇 **查看類別/產品**。 從選取器中選擇產品/類別以獲取此產品/類別的預覽。 選擇 **購買外觀** 的子菜單。

![建立模板 ](assets/create-template-picker.png)

現在，我們必須將此模板分配給特定類別。 在 **頁面資訊** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。 按一下資料夾表徵圖以選擇 **購買外觀** 的下界。 可以通過啟用複選框將多個類別分配給模板，還可以包括子類別。

![建立模板關聯](assets/create-template-associate.png)

返回主首頁，然後按一下 **購買外觀** 的子菜單。 所有其他類別仍使用通用模板。

![建立模板結果](assets/create-template-result.png)

可以應用相同的工作流來建立單個產品模板。

## 下一步是什麼 {#what-is-next}

現在，您已完成了此部分的旅程，您應：

* 瞭解目錄模板的概念
* 一般模板如何工作
* 已建立單個模板

在此知識基礎上構建並通過下一步查看文檔繼續您的旅程 [管理分階段產品目錄體驗](staged-catalog.md)中，您將學習如何處理已轉移的產品資料和啟動AEM。

## 其他資源 {#additional-resources}

雖然建議您通過查看文檔來繼續下一段旅程 [管理分階段產品目錄體驗](staged-catalog.md)，下面是一些附加的可選資源，可對本文檔中提到的一些概念進行更深入的分析，但不需要繼續無頭之旅：

* [建立多個類別和產品頁](/help/commerce-cloud/authoring/multi-template-usage.md)
* [遷移指南Experience Manager Cloud Service](/help/commerce-cloud/migration.md)  — 如何從舊版AEM本遷移到Commerce Integration Framework(CIF)附加程式
