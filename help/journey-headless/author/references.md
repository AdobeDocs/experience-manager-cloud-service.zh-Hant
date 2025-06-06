---
title: 了解如何在內容片段中使用參考
description: 了解如何在內容片段中使用內容、其他片段和其他資產 (媒體) 的參考。介紹巢狀片段對 Headless CMS 製作的必要性和機制。
exl-id: a65e8a5a-954b-4307-8027-ca8bac5f4261
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 2c74a3a42dd21e2eaf71c1922931d5fa5149f7c5
workflow-type: ht
source-wordcount: '791'
ht-degree: 100%

---

# 了解如何在內容片段中使用參考 {#author-headless-references}

## 目前進度 {#story-so-far}

在[AEM Headless 內容作者歷程](overview.md)的一開始，[簡介](introduction.md)部分介紹了和 Headless 內容製作相關的基本概念和術語。

您已經了解 Headless CMS 製作的基本知識，包含如何使用 AEMaaCS 製作內容，尤其是製作內容片段。

本文以這些概念為基礎，以便您了解如何使用參考為您的 AEM Headless 專案製作您自己的內容。

## 目標 {#objective}

* **客群**：進階
* **目標**：介紹如何如何使用 Headless CMS 製作的參考。有哪些類型參考可用，它們的作用為何：

   * 內容參考
   * 資產/媒體參考
   * 片段參考
   * 文字區塊內的臨時參考

## 什麼是參考 {#what-are-references}

參考只是一種連接資源 (無論是其他內容、資產 (如影像) 還是其他片段) 的機制。雖然非常相似，但還是有一些不同。

一些參考有專用資料類型 (例如內容參考和片段參考)，而其他參考只是新增至文字區塊內的參考 (資產參考和臨時參考)。

![內容片段 - 參考](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-overview.png)

## 內容參考 {#content-references}

內容參考的作用就是可讓您參考任何其他內容。這會開啟讓您選取內容項目的瀏覽器。

有兩種類型：

* **內容參考**
   * 指定所參考資源的路徑
* **內容參考 (UUID)**
   * 在編輯器中，參考會指定所參考資源的路徑；在內部，參考被視為參考資源的通用唯識別碼 (UUID)。

## 資產/媒體參考 {#assets-media-references}

可以使用&#x200B;**插入資產**&#x200B;選項，讓資產 (例如影像或媒體) 可在文字區塊內被參考。這會開啟讓您選取資產的瀏覽器。

![內容片段 - 插入資產](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## 片段參考 {#fragment-references}

同樣地，片段參考的作用就是可讓您參考另一個片段。為什麼這很重要需要進一步說明。

例如，您可能定義了以下內容片段模型：

* 城市
* 公司
* 人員
* 獎項

看起來很簡單，但一家公司既有執行長也有員工...這些都是人，每一個都被定義為人員。

人員可以獲得一個獎項 (或兩個)。

* 我的公司 - 公司
   * CEO - 人員
   * 員工 - 人員
      * 人員獎項 - 獎項

這只是供初學者了解。根據複雜程度，獎項可以是特定於公司的，或者公司可以在特定城市設有主要辦公室。

可以使用片段參考來表示這些相互關係，因為您 (作者) 和 Headless 應用程式都可理解。

作為作者，您不負責定義這些關係 (由內容架構師在建立內容片段模型時定義)，但您需要知道如何識別和編輯參考。

有兩種類別：

* **片段參考**
   * 指定所參考資源的路徑
* **片段參考 (UUID)**
   * 在編輯器中，參考會指定所參考資源的路徑；在內部，參考被視為參考資源的通用唯識別碼 (UUID)。

<!--
![Content Modeling with Content Fragments](/help/journey-headless/developer/assets/headless-modeling-01.png "Content Modeling with Content Fragments")
-->

### 如何製作巢狀片段 {#author-nested-fragment}

製作片段參考非常簡單 (儘管欄位通常不會被標記為&#x200B;**片段參考**)。您可以直接輸入參考，或者 (更有可能) 選取資料夾圖示以開啟瀏覽器，讓您可瀏覽和選取所需片段。

![內容片段 - 參考](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

內容片段模型定義在控制：

* 是否可以選擇新增多個參考
* 您可以選取的內容片段模型類型；內容片段模型定義允許參考的片段模型，因此 AEM 僅根據這些模型顯示片段。

### 如何導覽巢狀片段 {#navigate-nested-fragment}

使用內容片段編輯器的&#x200B;**樹狀結構**&#x200B;索引標籤，您可以瀏覽片段參考的片段，然後瀏覽該片段包含的任何參考。選取一個參考會開啟該片段供您編輯。

![內容片段樹狀結構](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-structure-tree.png)

## 臨時參考 {#adhoc-references}

臨時參考可以簡單連結的形式新增到文字區塊內：

![內容片段 - 臨時參考](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 下一步 {#whats-next}

現在您已經了解了內容片段中的參考和結構，下一步是[了解中繼資料和標記](metadata-tagging.md)。將介紹和討論如何定義內容片段的中繼資料和標記。

## 其他資源 {#additional-resources}

* [使用內容片段](/help/sites-cloud/administering/content-fragments/overview.md)

   * [管理內容片段](/help/sites-cloud/administering/content-fragments/managing.md)

      * [套用設定到資產資料夾](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)

      * [建立內容片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)

   * [製作內容片段](/help/sites-cloud/administering/content-fragments/authoring.md)

   * [內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [內容片段模型 - 資料類型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)

      * [內容片段模型 - 屬性](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)

* 快速入門指南
   * [建立資產資料夾 - Headless 設定](/help/headless/setup/create-assets-folder.md)

* AEM Headless 內容架構師歷程

* AEM Headless 翻譯歷程
