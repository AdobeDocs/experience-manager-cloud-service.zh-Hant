---
title: 使用標記
description: 標籤是對網站內的內容進行分類的快速而簡便的方法
exl-id: d2a9f578-fe0a-48ea-851c-2c84463661e0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 7%

---

# 使用標記 {#using-tags}

標籤是對網站內的內容進行分類的一種快速而簡便的方法。 標籤可以被視為關鍵字或標籤，可以附加到頁面、資產或其他內容，以使搜索能夠查找該內容和相關內容。

* 有關建立和管理標籤以及已應用哪些內容標籤的資訊，請參閱管理標籤。 <!-- See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.-->
* 請參閱 [為開發人員添加標籤](/help/implementing/developing/introduction/tagging-framework.md) 有關標籤框架以及在自定義應用程式中包括和擴展標籤的資訊。

## 使用標籤的十個理由 {#ten-reasons-to-use-tagging}

1. **組織內容**  — 標籤使作者的生活更輕鬆，因為他們可以用很少的精力快速組織內容。
1. **組織標籤**  — 當標籤組織內容時，分層分類/命名空間組織標籤。
1. **組織嚴密的標籤**  — 由於能夠建立標籤和子標籤，因此可以表示整個分類系統，包括術語、子術語及其關係。 這允許建立與正式內容級別平行的第二（或第三）內容等級。
1. **受控標籤**  — 可以通過對標籤和/或命名空間應用權限來控制標籤的建立和應用。
1. **靈活標籤**  — 標籤有許多名稱和面：標籤、分類術語、類別、標籤等。 在內容模型和使用方式上是靈活的；例如，在概述目標人口統計資訊、對內容進行分類和評級或建立輔助內容層次結構時。
1. **改進搜索**  — 廣義上的預設搜索組AEM件包括建立的標籤和應用的標籤，篩選器可應用到這些標籤，以將結果縮小到相關的標籤。
1. **SEO啟用**  — 作為頁面屬性應用的標籤將自動顯示在頁面的元標籤中，使搜索引擎可見。
1. **簡單複雜**  — 只需用單詞和按鈕即可建立標籤。 然後，可以添加標題、描述和無限制的標籤，以向標籤提供更多語義。
1. **核心一致性**  — 標籤系統是內容的核心元件AEM，並被所有功AEM能用於分類內容。 此外，標籤API可供開發人員用於建立具有對相同分類的訪問權限的標籤啟用的應用程式。
1. **結合結構和靈活性** -AEM由於頁面和路徑的嵌套，非常適合處理結構化資訊。 由於內置了全文搜索功能，在處理非結構化資訊時，它同樣具有強大的功能。 標籤結合了結構和靈活性的優點。

在為站點設計內容結構和為資產設計元資料架構時，請考慮提供的輕量級且易於訪問的方法標籤。

## 應用標籤 {#applying-tags}

在作者環境中，作者可以通過訪問頁面屬性並在 **標籤/關鍵字** 的子菜單。

若要套用預先定義的標籤，請在「頁面屬 **性** 」視窗中使用「標籤 **」欄位和「選** 取標籤 **** 」視窗。「標 **準標籤** 」標籤是預設的命名空間，這表示分類 `namespace-string:` 沒有前置詞。<!-- To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window.-->

![選擇多個標籤](/help/sites-cloud/authoring/assets/tags-select.png)

## 發佈標籤 {#publishing-tags}

與發佈和取消發佈頁面的方式類似，您可以在標籤和命名空間上執行以下操作：

### 啟動 {#activate}

* 激活單個標籤。

   與頁面一樣，新建立的標籤在發佈環境中可用之前需要激活。

>[!NOTE]
>
>激活頁面時，會自動開啟一個對話框，使您能夠激活屬於頁面的未激活標籤。

### 停用 {#deactivate}

* 停用所選標籤。
