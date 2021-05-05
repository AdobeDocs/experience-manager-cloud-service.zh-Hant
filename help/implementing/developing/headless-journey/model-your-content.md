---
title: 如何建立內容模型
description: 在「無頭開發人AEM員歷程」的這部分，瞭解如何使用內容片段模型和內容片段的資料AEM模型來建立內容模型，以進行無頭髮傳送。
hide: true
hidefromtoc: true
index: false
exl-id: f872839b-2401-4ea4-9e09-e5dda18afd09
translation-type: tm+mt
source-git-commit: 3d5ea8df4cefdb8c2bebe26333002a4680fa9fd4
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 1%

---

# 如何建立內容的模型{#model-your-content}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[無頭開發人AEM員旅程](overview.md)的這部分，您可以學習如何對內容結構建模。 然後，瞭解Adobe Experience Manager(AEM)使用內容片段模型和內容片段的結構，以便跨通道重複使用。

## 到目前為止的故事{#story-so-far}

在[開始時，瞭解CMS無頭開發](learn-about.md)涵蓋了無頭內容傳送，以及使用它的原因。 然後，在您自己的專案中，將「開始使用AEM無頭」作為Cloud Service](getting-started.md)說AEM明為「無頭」[

在上一份無頭歷程的AEM檔案[使用無頭體驗的第AEM一次體驗路徑](/help/implementing/developing/headless-journey/path-to-first-experience.md)中，您接著瞭解實作第一個專案所需的步驟。 閱讀後，您應：

* 瞭解設計內容時的重要規劃考量
* 瞭解根據您的整合層級需求實作無頭的步驟。
* 設定必要的工具和AEM設定。
* 瞭解最佳實務，讓您的無頭體驗更順暢、讓內容製作更有效率，並確保內容能快速傳遞。

本文以這些基礎為基礎，讓您瞭解如何準備自己的無頭AEM專案。

## 目標 {#objective}

* **觀眾**:初學者
* **目標**:瞭解如何建立內容結構模型，然後使用內容片段模型和內AEM容片段來實現該結構：
   * 介紹與[資料建模](#data-modeling)相關的概念和術語。
   * 瞭解[為何無頭內容傳送需要建立資料模型](#data-modeling-for-aem-headless)。
   * 瞭解如何使用內容片段模型AEM（以及使用[內容片段](#use-content-to-author-content)製作內容）來實現此結構。[](#create-structure-content-fragment-models)
   * 瞭解[如何建立內容模型](#getting-started-examples);基本樣本的原則。

>[!NOTE]
>
>資料建模是一個非常大的領域，它在開發關係資料庫時使用。 有許多書籍和線上資訊來源可供使用。
>
>我們只會在建立資料模型以便與Headless搭配使用時，考慮相關的AEM方面。

## 資料建模{#data-modeling}

*外面的世界很糟*。

也許，也許不是，但是它確實是一個大的&#x200B;***複雜的***&#x200B;世界，資料模型被用來定義一個非常（非常）小的子區段的簡化表示，使用特定目的所需的特定資訊。

例如：

學校很多，但它們都有不同的共同點：

* 位置
* 校長
* 許多教師
* 許多非教職員
* 許多學生
* 許多前教師
* 許多前學生
* 許多教室
* 許多（多）本書
* 多（多）件設備
* 許多課外活動
* 等等…….

即使在如此小的例子中，這份清單也看起來無窮無盡。 但是，如果您只想讓應用程式執行簡單的工作，您就必須將資訊限制在基本功能。

例如，針對該地區所有學校宣傳特殊活動：

* 學校名稱
* 學校地點
* 校長
* 事件類型
* 事件日期
* 教師組織活動

### 概念{#concepts}

您要描述的內容稱為&#x200B;**Entities** —— 基本上是我們要儲存相關資訊的「內容」。

我們要儲存的相關資訊是&#x200B;**屬性**（屬性），例如教師的姓名和資格。

然後，實體之間有各種&#x200B;**關係**。 例如，一所學校通常只有一位校長，而許多教師（而校長通常也是一位教師）。

分析和定義此資訊以及它們之間的關係的過程稱為&#x200B;**資料建模**。

### 基本資訊 {#basics}

通常，您需要首先繪製&#x200B;**描述實體及其關係的概念方案**。 這通常是高階（概念性）。

穩定後，可以將模型轉換為描述實體、屬性和關係的&#x200B;**邏輯架構**。 在此層級，您應仔細檢查定義，以消除重複並最佳化您的設計。

>[!NOTE]
>
>有時，這兩個步驟會合併，通常視您的藍本複雜性而定。

例如，您需要`Head Teacher`和`Teacher`的個別實體，還是只需要`Teacher`模型上的其他屬性？

### 確保資料完整性{#data-integrity}

您需要具備資料完整性，以確保內容在整個生命週期中的準確性與一致性。 這包括確保內容作者可輕鬆瞭解儲存內容的位置——因此以下內容至關重要：

* 清晰的結構
* 盡可能簡潔的結構（而不犧牲精確性）
* 驗證個別欄位
* 視情況，將特定欄位的內容限制為有意義的

### 消除資料冗餘{#data-redundancy}

當相同的資訊在內容結構中儲存兩次時，就會發生資料冗餘。 這應避免，因為在建立內容時可能會造成混淆，而在查詢時會產生錯誤；更別提誤用儲存空間了。

### 優化和效能{#optimization-and-performance}

透過最佳化結構，您可以改善內容建立和查詢的效能。

一切都是一種平衡行為，但創造一種過於複雜或層次過多的結構，可以：

* 讓產生內容的作者感到困惑。

* 如果查詢必須存取多個巢狀（參考）內容片段以擷取所需內容，就會嚴重影響效能。

## 無頭&lt;AEMa0/>的資料建模{#data-modeling-for-aem-headless}

資料建模是一組既有的技術，在開發關係資料庫時經常使用，對於Headless來說，它意味著什AEM麼？

### 為什麼？{#why}

為確保您的應用程式能夠一致且有效率地要求及接收所需內容，AEM此內容必須結構化。

這表示您的應用程式會事先知道回應的形式，因此也知道如何處理。 這比接收自由格式內容要容易得多，因為必須對其進行剖析，以確定其中包含的內容，並因此確定其使用方式。

### How簡介？{#how}

使AEM用內容片段來提供將內容無頭傳送至應用程式所需的結構。

您的資料模型結構為：

* 內容片段模型的定義，
* 做為內容產生所用內容片段的基礎。

>[!NOTE]
>
>內容片段模型也用作GraphQL架構的基礎AEM，用於檢索內容——在以後的會話中有更多內容。

您會使用GraphQL API(標準GraphQL API的自訂實AEM作)來要求內容。 GraphQL AEM API允許您對內容片段執行（複雜）查詢，每個查詢都根據特定的模型類型。

然後，您的應用程式就可以使用傳回的內容。

## 使用內容片段模型建立結構{#create-structure-content-fragment-models}

內容片段模型提供多種機制，可讓您定義內容結構。

內容片段模型描述實體。

>[!NOTE]
>您必須在「設定瀏覽器」中啟用「內容片段」功能，才能建立新模型。

>[!TIP]
>
>模型應命名，以便內容作者知道在建立內容片段時要選取的模型。

模型內：

1. **「資** 料類型」可讓您定義個別屬性。例如，將教師姓名的欄位定義為&#x200B;**Text**，其服務年限定為&#x200B;**Number**。
1. 資料類型&#x200B;**內容參考**&#x200B;和&#x200B;**片段參考**&#x200B;可讓您建立與內容中其他內容的關係AEM。
1. **片段參考**&#x200B;資料類型可讓您巢狀化內容片段（根據模型類型），以實現多層結構。 這對您的資料模型至關重要。

例如：
![使用內容片段建立內容模型](assets/headless-modeling-01.png "使用內容片段建立內容模型")

### 資料類型 {#data-types}

提AEM供下列資料類型，供您建立內容模型：

* 單行文字
* 多行文字
* 數量
* 布林值 (Boolean)
* 日期時間
* 列舉
* 標記
* 內容參考資料
* 片段引用
* JSON 物件

### 參考與巢狀內容{#references-nested-content}

兩種資料類型提供特定片段以外內容的參考：

* **內容**
參考這可提供任何類型其他內容的簡單參考。例如，您可以在指定位置參考影像。

* **片段**
參考這可提供其他內容片段的參考。此類參考可用來建立巢狀內容，並引入建立內容模型所需的關係。
可以配置資料類型以允許片段作者：
   * 直接編輯參考的片段。
   * 根據適當的模型建立新的內容片段

## 使用模型製作內容片段{#use-content-to-author-content}

內容片段一律以內容片段模型為基礎。 模型提供結構，片段保存內容。

### 選擇適當的型號{#select-model}

實際建立內容的第一步是建立內容片段。 這是以特定的內容片段模型為基礎，您會選取該模型作為建立程式的第一步。

### 建立和編輯結構化內容{#create-edit-structured-content}

一旦您的片段建立後，您就可以在內容片段編輯器中開啟它。 您可以：

* 以一般或全螢幕模式編輯您的內容。
* 將您的內容格式化為「全文」、「純文字」或「標籤」。
* 建立並管理您內容的變數。
* 關聯內容.
* 編輯中繼資料。
* 顯示樹結構。
* 預覽JSON表示法。

## 開始使用某些範例{#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

如需範例的基本結構，請參閱範例內容片段結構。

## 下一個{#whats-next}

現在您已學習如何建立結構模型並建立相關內容，接下來的步驟是[瞭解如何使用GraphQL查詢來存取和擷取您的內容片段內容](access-your-content.md)。 這將介紹並討論GraphQL，然後查看一些示例查詢，以瞭解實際操作的方式。

## 其他資源 {#additional-resources}

* [使用內容片段](/help/assets/content-fragments/content-fragments.md) -內容片段的引入頁面
   * [配置瀏覽器中的內容片段](/help/assets/content-fragments/content-fragments-configuration-browser.md) -在配置瀏覽器中啟用內容片段功能
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md) -建立和編輯內容片段模型
   * [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md) -建立和製作內容片段；此頁面將引導您進入其他詳細章節
* [AEM GraphQL方案](/help/implementing/developing/headless-journey/access-your-content.md) - GraphQL如何實現模型
* [範例內容片段結構](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [開始使用無AEM頭](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) -簡短的教學課程系列影片，概述如何使用無頭功AEM能，包括資料建模和GraphQL
