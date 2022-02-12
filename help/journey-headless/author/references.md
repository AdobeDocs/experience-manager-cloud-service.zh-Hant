---
title: 瞭解在內容片段中使用引用
description: 瞭解如何在內容片段、內容、其他片段和其他資產（媒體）中使用引用。 介紹無頭CMS創作中嵌套片段的必要性和機制。
exl-id: a65e8a5a-954b-4307-8027-ca8bac5f4261
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---

# 瞭解在內容片段中使用引用 {#author-headless-references}

## 到目前為止的故事 {#story-so-far}

在 [無AEM頭內容作者之旅](overview.md) 這樣 [導言](introduction.md) 介紹了與無頭創作相關的基本概念和術語。

您已學習了無頭CMS創作的基礎知識，並介紹了使用AEMaaCS進行創作，特別是創作內容片段。

本文基於這些內容，以便您瞭解如何使用引用來為您的無頭項目創作AEM您自己的內容。

## 目標 {#objective}

* **觀眾**:高級
* **目標**:介紹對無頭CMS創作的引用的使用。 可用的參考類型及其目的：

   * 內容參考資料
   * 資產/介質引用
   * 片段引用
   * 來自文本塊內的即席引用

## 什麼是引用 {#what-are-references}

引用只是連接資源的一種機制，無論是其他內容、資產（如影像中）還是其他片段。 雖然非常相似，但還是有一些不同。

某些引用具有專用的資料類型（例如，內容引用和片段引用），而其他引用則只是作為文本塊（資產引用和即席引用）中的引用而添加。

![內容片段 — 引用](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## 內容參考資料 {#content-references}

「內容引用」只是這樣做 — 它們允許您引用任何其他內容。 這將開啟一個瀏覽器，允許您選擇內容項。

## 資產/介質引用 {#assets-media-references}

使用 **插入資產** 的雙曲餘切值。 這將開啟一個瀏覽器，允許您選擇資產。

![內容片段 — 插入資產](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## 片段引用 {#fragment-references}

再次，片段引用只是執行此操作 — 它們允許您引用另一個片段。 為什麼這很重要，需要多一點解釋。

例如，您可能定義了以下內容片段模型：

* 城市
* 公司
* 人員
* 獎項

看起來很簡單，但公司當然有CEO和員工……。這些都是人，每個人都被定義為人。

一個人可以獲得一個獎（或者兩個獎）。

* 我的公司 — 公司
   * CEO — 人員
   * 員工 — 人員
      * 個人獎 — 獎

這只是開始。 根據複雜性，獎項可能是公司特定的，或公司可能在特定的城市擁有其主要辦事處。

使用片段引用可以表示這些相互關係，因為您（作者）和無頭應用程式都瞭解這些關係。

作為作者，您不負責定義這些關係（建立內容片段模型時由內容架構師完成），但您需要知道如何識別和編輯引用。

<!--
![Content Modeling with Content Fragments](/help/journey-headless/developer/assets/headless-modeling-01.png "Content Modeling with Content Fragments")
-->

### 如何生成嵌套片段 {#author-nested-fragment}

創作片段引用相當簡單(儘管通常不會將欄位標籤為 **片段引用**)。 您可以直接鍵入引用，或者（更可能）選擇資料夾表徵圖以開啟瀏覽器，該瀏覽器允許您導航並選擇所需的片段。

![內容片段 — 引用](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

內容片段模型的定義控制：

* 是否可以選擇添加多個參照
* 可選擇的內容片段的模型類型；內容片段模型定義了允許用於引用的片段模型，AEM因此僅根據這些模型顯示片段。

### 如何導航嵌套片段 {#navigate-nested-fragment}

使用 **結構樹** 在內容片段編輯器的頁籤中，您可以瀏覽片段引用的片段，然後瀏覽它們可能包含的任何引用。 選取參照會開啟該片段進行編輯。

>[!NOTE]
>
>使用主面板中的麵包屑，您可以導航回起始點。

![內容片段結構樹](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## 即席引用 {#adhoc-references}

Ad hoc引用可以作為文本塊中的簡單連結添加：

![內容片段 — 即席引用](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 下一步是什麼 {#whats-next}

現在，您已經瞭解了「內容片段」中的引用和結構，下一步是 [瞭解元資料和標籤](metadata-tagging.md)。 這將介紹並討論如何定義內容片段的元資料和標籤。

## 其他資源 {#additional-resources}

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)

   * [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)

      * [將配置應用到您的資產資料夾](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [建立內容片段](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [變體 — 創作內容片段](/help/assets/content-fragments/content-fragments-variations.md)

   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [內容片段模型 — 資料類型](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [內容片段模型 — 屬性](/help/assets/content-fragments/content-fragments-models.md#properties)


* 入門指南
   * [建立資產資料夾 — 無頭設定](/help/headless/setup/create-assets-folder.md)

* 無AEM頭內容架構師旅程

* 無AEM頭翻譯之旅
