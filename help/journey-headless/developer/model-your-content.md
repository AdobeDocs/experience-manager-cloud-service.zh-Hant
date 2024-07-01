---
title: 如何建立內容模型
description: 在 Adobe Experience Manager (AEM) Headless 開發人員歷程的這一部分中，了解如何使用內容模型和內容片段模型及內容片段，建立您的內容模型用於 AEM Headless 傳遞。
exl-id: f052183d-18fd-4615-a81e-e45db5928fc1
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: ht
source-wordcount: '1814'
ht-degree: 100%

---

# 如何建立內容模型 {#model-your-content}

在 [AEM Headless 開發人員歷程](overview.md)的這一部分中，您會了解如何建立內容結構模型。然後使用內容片段模型和內容片段實現 Adobe Experience Manager (AEM) 的結構，以便跨管道重複使用。

## 到目前為止 {#story-so-far}

一開始，[了解 CMS Headless 開發](learn-about.md)介紹 Headless 內容傳遞以及使用它的原因。然後 [AEM Headless as a Cloud Service 快速入門](getting-started.md)以您自己的專案而言描述 AEM Headless 如何運作。

在 AEM Headless 歷程的上一個文件「[踏上首次使用 AEM Headless 之路](path-to-first-experience.md)」中，您接著了解實作第一個專案所需的步驟。閱讀後，您可以進行以下事項：

* 了解及解釋設計內容的重要規劃考量事項
* 了解及解釋實作 Headless 的步驟，根據您的整合層級要求來進行。
* 設定必要的工具和 AEM 設定。
* 了解最佳做法，以便您讓自己的 Headless 歷程順暢、持續高效產生內容，以及確保內容快速傳遞。

本文章以這些基本知識為基礎，以便您了解如何準備您自己的 AEM Headless 專案。

## 目標 {#objective}

* **對象**：初學者
* **目標**：了解如何建立內容結構模型，然後使用 AEM 內容片段模型和內容片段實現該結構：
   * 介紹與資料/內容模型相關的概念和術語。
   * 了解為什麼 Headless 內容傳遞需要建立內容模型。
   * 了解如何使用 AEM 內容片段模型實現此結構 (和使用內容片段編寫內容)。
   * 了解如何建立內容模型；基本範例的原則。

>[!NOTE]
>
>資料模型是一個廣大的領域，因為開發關聯式資料庫時會用到這類模型。有許多書籍和線上資訊來源可供您使用。
>
>在建立資料模型和 AEM Headless 搭配使用時，此歷程只會考慮感興趣的層面。

## 內容模型 {#content-modeling}

*外面的世界很大很糟糕*。

也許是，但也許不是。這肯定是一個&#x200B;***複雜***&#x200B;世界，資料模型用於定義一個非常 (極為) 小的子部分的簡化表示，使用特定目的所需的特定資訊。

>[!NOTE]
>
>由於 AEM 是處理內容方面，此歷程會將資料模型稱為內容模型。

例如：

有很多學校，但它們都有很多共同點：

* 位置
* 校長
* 許多老師
* 許多非教學人員
* 許多學生
* 許多前任老師
* 許多畢業校友
* 許多教室
* 許多 (很多) 書
* 許多 (很多) 設備
* 許多課外活動
* 以此類推....

即使在這麼小的例子中，此清單也似乎無止盡。但是，如果您只想讓您的應用程式執行一項簡單的任務，則要將資訊限制在最基本的範圍內。

例如，為該地區的所有學校宣傳特別活動：

* 學校名稱
* 學校位置
* 校長
* 活動類型
* 活動日期
* 組織活動的老師

### 概念 {#concepts}

您想要描述的內容稱為&#x200B;**實體** - 基本上是您要儲存關於其資訊的「東西」。

您想要儲存關於這些的資訊是&#x200B;**屬性**，例如老師的姓名和資格。

那麼實體之間就是各種&#x200B;**關係**。例如，通常一個學校只有一位校長，還有很多老師 (校長通常也是老師)。

分析和定義此資訊的流程以及彼此間的關係被稱之為&#x200B;**內容模型**。

### 基本資訊 {#basics}

通常，您必須先繪製描述實體及其關係的&#x200B;**概念性結構描述**。通常這是高層級的 (概念性)。

穩定後，您可以將模型轉譯成描述實體、屬性和關係的&#x200B;**邏輯結構描述**。在此層級，要仔細檢查定義以消除重複並最佳化您的設計。

>[!NOTE]
>
>有時這兩個步驟會合併，通常取決於您的情境複雜性。

例如，`Head Teacher` 和 `Teacher` 是否需要各自成為單獨的實體，或者只是 `Teacher` 模型的額外屬性？

### 確保資料完整性 {#data-integrity}

需要資料完整性來保證您的內容在其整個生命週期內的準確性和一致性。這包括確保內容作者可以輕鬆了解什麼儲存在哪裡 - 因此以下事項至關重要：

* 清楚的結構
* 結構盡可能簡潔 (在不犧牲準確性的情況下)
* 驗證個別欄位
* 在適當情況下，將特定欄位的內容限制在有意義的範圍內

### 消除資料冗餘 {#data-redundancy}

當內容結構中相同資料儲存兩次時，就會出現資料冗餘。應該避免這種情況，因為在建立內容時會造成困惑，查詢時會發生錯誤，更不用說濫用儲存空間了。

### 最佳化和效能 {#optimization-and-performance}

最佳化結構，您可以提高內容建立和查詢的效能。

一切都是一種平衡行為，但是建立過於複雜或層次過多的結構可能會讓生成內容的作者感到困惑。同時，如果查詢必須存取多個巢狀 (被參考的) 內容片段以擷取所需內容，這就會嚴重影響效能。

## AEM Headless 內容模型 {#content-modeling-for-aem-headless}

資料模型是一套既有的技術，通常在開發關聯式資料庫時使用，那麼內容模型對 AEM Headless 代表什麼？

### 原因為何？ {#why}

為確保您的應用程式能夠始終一致、有效率地從 AEM 要求和接收所需內容，這些內容必須結構化。

這表示您的應用程式預先知道回應採用的格式，因此知道如何處理回應。這比接收自由格式的內容要容易得多，自由格式的內容必須剖析以確定它包含什麼以及如何使用它。

### 運作方式簡介 {#how}

AEM 使用內容片段來提供將內容 Headless 傳遞到應用程式所需的結構。

您的內容模型結構：

* 是由您的內容片段模型的定義實現，
* 做為內容片段的基礎，內容片段用於產生內容。

>[!NOTE]
>
>內容片段模型也作為 AEM GraphQL 結構描述的基礎，用於擷取您的內容 - 在後面的課程會詳細介紹。

對內容的要求是使用 AEM GraphQL API 發出的，這是標準 GraphQL API 的自訂實作。AEM GraphQL API 可讓您對內容片段執行 (複雜) 查詢，每個查詢都根據特定的模型類型。

然後，您的應用程式可以使用傳回的內容。

## 使用內容片段模型建立架構 {#create-structure-content-fragment-models}

內容片段模型提供多種機制，允許您定義內容的結構。

內容片段模型描述一個實體。

>[!NOTE]
>您必須在設定瀏覽器中啟用內容片段功能，才能建立模型。

>[!TIP]
>
>應該命名模型，以便內容作者在建立內容片段時知道要選取哪個模型。

在模型中：

1. **資料類型**允許您定義個別屬性。
例如，將包含教師姓名的欄位定義為**文字** 並將他們的服務年限定義為&#x200B;**數字**。
1. 資料類型&#x200B;**內容參考**&#x200B;和&#x200B;**片段參考**&#x200B;允許您在 AEM 中建立與其他內容的關係。
1. **片段參考**&#x200B;資料類型可讓您將內容片段巢狀化 (根據模型類型)，以實現多層結構。這對建立內容模型很重要。

例如：
![使用內容片段建立內容模型](assets/headless-modeling-01.png "使用內容片段建立內容模型")

### 資料類型 {#data-types}

AEM 提供以下資料類型用於建立內容模型：

* 單行文字
* 多行文字
* 數字
* 布林值
* 日期和時間
* 列舉
* 標記
* 內容參考
* 片段參考
* JSON 物件

### 參考和巢狀內容 {#references-nested-content}

兩種資料類型允許您參考特定片段之外的內容：

* **內容參考**
這提供對任何類型之其他內容的簡單參考。
例如，您可以參考在指定之位置的影像。

* **片段參考**
這提供對其他內容片段的參考。
此類型的參考用於建立巢狀內容，引入建立內容模型時所需的關係。
可以設定此資料類型以允許片段作者：
   * 直接編輯參考的片段。
   * 根據適當的模型建立內容片段

### 建立內容片段模型 {#creating-content-fragment-models}

首先，您必須為您的網站啟用內容片段模型。這是在設定瀏覽器中完成，在「**工具** > **一般** > **設定瀏覽器**」下。您可以選擇設定全域項目，也可以建立設定。例如：

![定義設定](assets/cfm-configuration.png)

>[!NOTE]
>
>請參閱其他資源 - 設定瀏覽器中的內容片段

然後可以建立內容片段模型並定義結構。此操作可以在「**工具** >**一般** > **內容片段模型**」下完成。例如：

![內容片段模型](assets/cfm-model.png)

>[!NOTE]
>
>請參閱其他資源 - 內容片段模型。

## 使用模型以透過內容片段編寫內容 {#use-content-to-author-content}

內容片段一律以內容片段模型為基礎。模型提供結構，片段保存內容。

### 選擇適當的模型 {#select-model}

實際建立內容的第一步是建立內容片段。這是使用「建立 > 內容片段」在「資產 > 檔案」下的所需資料夾中完成的。精靈會引導您完成這些步驟。

內容片段基於特定的內容片段模型 (建立流程第一步時選取的)。

### 建立和編輯結構化內容 {#create-edit-structured-content}

建立片段後，您可以在內容片段編輯器中將其開啟。您可以在這裡進行以下作業︰

* 以正常或全螢幕模式編輯您的內容。
* 將您的內容格式化為全文、純文字或 Markdown。
* 建立和管理您內容的不同版本。
* 關聯內容。
* 編輯中繼資料。
* 顯示樹狀結構。
* 預覽 - JSON 表示。

### 建立內容片段 {#creating-content-fragments}

選擇適當的模型後，在內容片段編輯器中開啟一個內容片段進行編輯：

![內容片段編輯器](assets/cfm-editor.png)

>[!NOTE]
>
>請參閱其他資源 - 使用內容片段。

## 從一些範例開始 {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

如需基本結構範例，請參閱範例內容片段結構。

## 下一步 {#whats-next}

現在您已經了解如何為您的結構建立模型，並根據結構模型建立內容，下一步是[了解如何使用 GraphQL 查詢存取和擷取您的內容片段內容](access-your-content.md)。這會介紹和討論 GraphQL，然後查看一些範例查詢以了解實務運作。

## 其他資源 {#additional-resources}

* [使用內容片段](/help/sites-cloud/administering/content-fragments/overview.md) - 內容片段的引領頁面
   * [設定瀏覽器中的內容片段](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser) - 在設定瀏覽器中啟用內容片段功能
   * [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) - 建立及編輯新內容片段模型
   * [管理內容片段](/help/sites-cloud/administering/content-fragments/managing.md) - 建立和編寫內容片段，此頁面會引領您到其他詳細章節
* [AEM GraphQL 結構描述](access-your-content.md) - GraphQL 如何實現模型
* [範例內容片段結構](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)
* [AEM Headless 快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) - 此為簡短的教學影片系列，概述如何使用 AEM 的 Headless 功能，包括內容模型和 GraphQL
   * [GraphQL 模型基本概念](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/video-series/modeling-basics.html) - 了解如何在 Adobe Experience Manager (AEM) 中定義及使用內容片段以搭配 GraphQL 使用。
