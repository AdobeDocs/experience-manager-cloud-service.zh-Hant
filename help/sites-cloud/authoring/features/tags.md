---
title: 使用標記
description: 標籤是快速且簡單的網站內容分類方法
exl-id: d2a9f578-fe0a-48ea-851c-2c84463661e0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 7%

---

# 使用標記 {#using-tags}

標籤是快速且簡單的網站內容分類方法。 標籤可以被視為可附加至頁面、資產或其他內容的關鍵字或標籤，以使搜索能夠找到該內容和相關內容。

* 請參閱管理標籤，以了解如何建立和管理標籤，以及套用了哪些內容標籤的資訊。<!-- See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.-->
* 請參閱[開發人員的標籤](/help/implementing/developing/introduction/tagging-framework.md) ，以取得關於標籤架構以及在自訂應用程式中包含和擴充標籤的資訊。

## 使用標籤{#ten-reasons-to-use-tagging}的十個理由

1. **組織內容**  — 標籤可讓作者更輕鬆，因為他們可以輕鬆快速地組織內容。
1. **組織標籤**  — 標籤組織內容時，階層分類/命名空間會組織標籤。
1. **組織嚴密的標籤**  — 透過建立標籤和子標籤的功能，便能表達整個分類系統，包括詞語、子詞語及其關係。這可以建立與官方層級平行的第二（或第三）個內容階層。
1. **控制標籤**  — 可借由對標籤和/或命名空間套用權限，以控制標籤的建立和應用程式。
1. **彈性的標籤**  — 標籤有許多名稱和面孔：標籤、分類術語、類別、標籤等。在內容模型和使用方式上，這些規則是有彈性的；例如，在概述目標人口統計資料時，將內容分類和評分，或建立次要內容階層。
1. **改進搜尋**  - AEM中的預設搜尋元件廣泛包含已建立的標籤和已套用的標籤，可套用篩選條件，將結果縮小至相關的標籤。
1. **SEO啟用**  — 以頁面屬性形式套用的標籤會自動顯示在頁面的中繼標籤中，讓搜尋引擎可見。
1. **簡單複雜**  — 只需使用字詞和按鈕的觸控功能，即可建立標籤。之後，可以新增標題、說明和無限標籤，為標籤提供更多語意。
1. **核心一致性**  — 標籤系統是AEM的核心元件，供所有AEM功能用來分類內容。此外，開發人員可使用標籤API來建立啟用標籤的應用程式，以存取相同的分類。
1. **結合結構與彈性**  — 由於頁面和路徑的巢狀，AEM是處理結構化資訊的理想選擇。由於內置的全文搜索功能，它在處理非結構化資訊時同樣具有強大的功能。 標籤結合了結構和彈性的優點。

設計網站的內容結構和資產的中繼資料結構時，請考慮提供的精簡且可存取的方法標籤。

## 套用標籤{#applying-tags}

在製作環境中，作者可以存取頁面屬性並在&#x200B;**標籤/關鍵字**&#x200B;欄位中輸入一或多個標籤，以套用標籤。

若要套用預先定義的標籤，請在「頁面屬 **性** 」視窗中使用「標籤 **」欄位和「選** 取標籤 **** 」視窗。「標 **準標籤** 」標籤是預設的命名空間，這表示分類 `namespace-string:` 沒有前置詞。<!-- To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window.-->

![選取多個標籤](/help/sites-cloud/authoring/assets/tags-select.png)

## 發佈標籤{#publishing-tags}

與發佈和取消發佈頁面的方式類似，您可以在標籤和命名空間上執行下列動作：

### 啟動 {#activate}

* 啟動個別標籤。

   就像頁面一樣，新建立的標籤必須先啟動，才能在發佈環境中使用。

>[!NOTE]
>
>當您啟動頁面時，會自動開啟對話方塊，讓您啟動屬於該頁面的未啟動標籤。

### 停用 {#deactivate}

* 停用選取的標籤。
