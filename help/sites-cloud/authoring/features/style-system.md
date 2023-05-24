---
title: 樣式系統
description: 樣式系統可讓範本作者在元件的內容原則中定義樣式類別，讓內容作者在編輯頁面上的元件時能夠選取這些類別。 這些樣式可作為元件的替代視覺變體，使其更靈活。
exl-id: 224928dd-e365-4f3e-91af-4d8d9f47efdd
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 2%

---

# 樣式系統{#style-system}

樣式系統可讓範本作者在元件的內容原則中定義樣式類別，讓內容作者在編輯頁面上的元件時能夠選取這些類別。 這些樣式可作為元件的替代視覺變體，讓元件更具彈性。

如此一來，您就不需要為每種樣式開發自訂元件，或是自訂元件對話方塊以啟用此類樣式功能。 它帶來更多可重複使用的元件，這些元件可以快速輕鬆地適應內容作者的需求，而無需任何AEM後端開發。

## 使用案例 {#use-case}

範本作者不僅需要為內容作者設定元件運作方式的能力，還需要設定元件的許多替代視覺變體。

同樣地，內容作者不僅需要建構和排列其內容的能力，還需要選取其視覺呈現方式。

樣式系統針對範本作者與內容作者的需求，提供統一的解決方案：

* 範本作者可以在元件的內容原則中定義樣式類別。
* 內容作者接著可在編輯頁面上的元件時，從下拉式清單中選取這些類別，以套用對應的樣式。

然後，樣式類別會插入至元件的裝飾包裝函式元素上，如此一來，元件開發人員就不需要在提供CSS規則以外的方式處理樣式。

## 概觀 {#overview}

通常，使用「樣式系統」會採用下列形式。

1. 網頁設計工具會建立元件的不同視覺變體。

1. 向HTML開發人員提供元件的HTML輸出以及要實施的所需視覺變化。

1. HTML開發人員會定義與每個視覺變數相對應的CSS類別，並插入在包裝元件的元素上。

1. HTML開發人員會針對每個視覺變數實作對應的CSS程式碼（以及選用的JS程式碼），使其看起來像已定義。

1. AEM開發人員將提供的CSS （和選用的JS）放在 [使用者端資源庫](/help/implementing/developing/introduction/clientlibs.md) 並進行部署。

1. AEM開發人員或範本作者會設定頁面範本，並編輯每個已設定樣式的元件的原則、新增定義的CSS類別、為每種樣式提供好記的名稱，以及指出哪些樣式可以合併。

1. AEM頁面作者隨後可以透過元件工具列的樣式選單，在頁面編輯器中選擇設計的樣式。

請注意，在AEM中實際執行的只有最後三個步驟。 這表示所有必要的CSS和Javascript開發都可以在不使用AEM的情況下完成。

實際實作樣式只需要在AEM上部署，並在所需範本的元件中選取。

下圖說明樣式系統的架構。

![aem-style-system](/help/sites-cloud/authoring/assets/style-system-architecture.png)

## 使用 {#use}

為了示範此功能，我們將使用 [WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)核心元件的實作 [標題元件](https://www.adobe.com/go/aem_cmp_title_v2) 例如。

下列章節 [作為內容作者](#as-a-content-author) 和 [作為範本作者](#as-a-template-author) 說明如何使用WKND的樣式系統來測試樣式系統的功能。

如果您想要對自己的元件使用「樣式系統」，請執行下列動作：

1. 將CSS安裝為使用者端程式庫，如區段所述 [概觀](#overview).
1. 依照一節中的說明，設定您想要可供內容作者使用的CSS類別 [作為範本作者](#as-a-template-author).
1. 然後，內容作者就可以使用區段中所述的樣式 [作為內容作者](#as-a-content-author).

### 作為內容作者 {#as-a-content-author}

1. 安裝WKND專案後，請導覽至WKND的英文主版首頁： `http://<host>:<port>/sites.html/content/wknd/language-masters/en` 並編輯頁面。
1. 選取 **標題** 頁面下方元件

   ![作者的樣式系統](/help/sites-cloud/authoring/assets/style-system-author1.png)

1. 點選或按一下 **樣式** 的工具列上的按鈕 **清單** 元件來開啟樣式選單並變更元件的外觀。

   ![選取樣式](/help/sites-cloud/authoring/assets/style-system-author2.png)

   >[!NOTE]
   >
   >在此範例中， **顏色** 樣式(**黑色**， **白色**、和 **灰色**)互斥，而 **樣式** 選項(**加底線**， **靠右對齊**、和 **最小間距**)可合併。 這可在范 [本中設定為範本作者](#as-a-template-author)。

### 作為範本作者 {#as-a-template-author}

1. 編輯WKND的英文主版首頁時 `http://<host>:<port>/sites.html/content/wknd/language-masters/en`，編輯頁面的範本，透過 **頁面資訊 — >編輯範本**.

   ![編輯範本](/help/sites-cloud/authoring/assets/style-system-edit-template.png)

1. 編輯的原則 **標題** 點選或按一下 **原則** 元件的按鈕。

   ![編輯原則](/help/sites-cloud/authoring/assets/style-system-edit-policy.png)

1. 在屬性的「樣式」標籤上，您可以看到樣式的設定方式。

   ![編輯屬性](/help/sites-cloud/authoring/assets/style-system-properties.png)

   * **群組名稱：** 樣式可在樣式選單中分組，內容作者在設定元件樣式時會看到該選單。
   * **樣式可以合併：** 允許同時選取該群組中的多個樣式。
   * **樣式名稱：** 設定元件樣式時，內容作者會看到的樣式說明。
   * **CSS類別：** 與樣式關聯的CSS類別的實際名稱。

   使用拖曳操作框來排列群組的順序以及群組內的樣式。 使用新增或刪除圖示來新增或移除群組內的群組或樣式。

>[!CAUTION]
>
>設定為元件原則的樣式屬性的CSS類別（以及任何必要的Javascript）必須部署為 [使用者端資料庫](/help/implementing/developing/introduction/clientlibs.md) 才能順利運作。

## 設定 {#setup}

核心元件2版及更新版本已完全啟用，以充分利用樣式系統，且不需要額外設定。

只有為您自己的自訂元件啟用樣式系統，或執行以下步驟時，才需要執行下列步驟 [在「編輯」對話方塊中啟用選用的樣式索引標籤。](#enable-styles-tab-edit)

### 在「設計」對話方塊中啟用「樣式」標籤 {#enable-styles-tab-design}

若要讓元件與AEM樣式系統搭配使用並在其「設計」對話方塊中顯示「樣式」索引標籤，元件開發人員必須在元件上使用下列設定來包含「樣式」索引標籤：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>此使用 [覆蓋](/help/implementing/developing/introduction/overlays.md)，透過 [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md).

設定好元件後，AEM會自動將頁面作者設定的樣式插入裝飾元素上，AEM會自動將該裝飾元素包裝在每個可編輯的元件周圍。 元件本身不需執行任何其他動作，即可讓此情況發生。

### 在「編輯」對話方塊中啟用樣式索引標籤 {#enable-styles-tab-edit}

「編輯」對話方塊中也有選用的樣式索引標籤。 與「設計」對話方塊標籤不同，「編輯」對話方塊中的標籤並非樣式系統正常運作的必要專案，而是可供內容作者設定樣式的選擇性替代介面。

編輯對話方塊索引標籤可以類似設計對話方塊索引標籤的方式加入：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>此使用 [覆蓋](/help/implementing/developing/introduction/overlays.md)，透過 [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md).

>[!NOTE]
>
>依預設，「編輯」對話方塊上的「樣式」索引標籤未啟用。

### 具有元素名稱的樣式 {#styles-with-element-names}

開發人員也可以使用為元件上的樣式設定允許的元素名稱清單 `cq:styleElements` 字串陣列屬性。 然後在「設計」對話方塊中原則的「樣式」標籤中，範本作者也可以選擇要為每個樣式設定的元素名稱。 這會設定包裝函式元素的元素名稱。

此屬性設定於 `cq:Component` 節點。 例如：

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>請避免為可組合的樣式定義元素名稱。 定義多個元素名稱時，優先順序為：
>
>1. HTL優先於所有內容： `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. 然後，在多個作用中樣式中，會採用元件原則中設定的樣式清單中的第一個樣式。
>1. 最後，元件的 `cq:htmlTag`/ `cq:tagName` 將被視為遞補值。

>


這種定義樣式名稱的功能對於非常一般的元件（例如佈局容器或內容片段元件）非常有用，可為它們提供額外的含義。

例如，這可讓版面配置容器獲得如下的語意 `<main>`， `<aside>`， `<nav>`等。
