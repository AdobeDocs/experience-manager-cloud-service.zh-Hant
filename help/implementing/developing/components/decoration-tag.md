---
title: 裝飾標記
description: 轉譯網頁中的元件時可產生 HTML 元素，將轉譯的元件圍在其中。對於開發人員來說，AEM 提供簡單清晰的邏輯，可控制圍住所含元件的裝飾標記。
exl-id: a90fd619-eff6-466f-9178-90374f988b5d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 8%

---

# 裝飾標記 {#decoration-tag}

轉譯網頁中的元件時可產生 HTML 元素，將轉譯的元件圍在其中。這主要有兩個用途：

* 元件必須以HTML元素包住，才能進行編輯。
* 包裝元素是用來套用HTML類別，提供：
   * 配置資訊
   * 樣式資訊

對於開發人員而言，AEM提供簡單清晰的邏輯，可控制包住所含元件的裝飾標籤。 裝飾標籤是否及如何呈現取決於兩個因素的組合，此頁面將深入研究這兩個因素：

* 元件本身可使用一組屬性來設定其裝飾標籤。
* 包含元件的指令碼可使用包含引數來定義裝飾標籤的各個層面。

## 建議 {#recommendations}

以下是何時納入包裝函式元素的一些一般建議，有助於避免發生非預期的問題：

* WCMModes （編輯或預覽模式）、例項（製作或發佈）或環境（測試或生產）之間不存在包裝函式元素，因此頁面的CSS和JavaScripts在所有情況下都運作相同。
* 應將包裝函式元素新增至所有可編輯的元件，讓頁面編輯器可以正確初始化及更新這些元件。
* 對於不可編輯的元件，如果包裝函式元素沒有提供特定功能，則可以避免使用，這樣產生的標籤就不會不必要地膨脹。

## 元件控制項 {#component-controls}

下列屬性和節點可套用至元件，以控制其裝飾標籤的行為：

* **`cq:noDecoration {boolean}`：**&#x200B;此屬性可以新增至元件，而true值會強制AEM在元件上不產生任何包裝函式元素。
* **`cq:htmlTag`節點：**&#x200B;此節點可以新增到元件下，並且可以具有以下屬性：
   * **`cq:tagName {String}`：**&#x200B;這可用來指定用於包住元件的自訂HTML標籤，而非預設DIV元素。
   * **`class {String}`：**&#x200B;這可用來指定要新增至包裝函式的CSS類別名稱。
   * 其他屬性名稱會新增為HTML屬性，其字串值與提供的值相同。

## 指令碼控制項 {#script-controls}

一般而言，HTL中的包裝函式行為可歸納如下：

* 預設不會轉譯任何包裝函式DIV （僅執行`data-sly-resource="foo"`時）。
* 所有wcm-modes （已停用、預覽、編輯作者和發佈）的轉譯方式相同。

您也可以完全控制包裝函式的行為。

* HTL指令碼可完全控制包裝函式標籤的結果行為。
* 元件屬性（例如`cq:noDecoration`和`cq:tagName`）也可以定義包裝函式標籤。

您可以透過HTL指令碼及其相關邏輯，完全控制包裝函式標籤的行為。

如需使用HTL開發的詳細資訊，請參閱[HTL檔案](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hant)。

### 決策樹 {#decision-tree}

此決策樹會摘要判斷包裝函式標籤行為的邏輯。

![決策樹](assets/decoration-tag-decision-tree.png)

### 使用案例 {#use-cases}

以下三個使用案例提供如何處理包裝函式標籤的範例，並說明控制包裝函式標籤所需行為的簡易程度。

以下所有範例均假設下列內容結構和元件：

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### 使用案例1：包含重複使用程式碼的元件 {#use-case-include-a-component-for-code-reuse}

最典型的使用案例是當一個元件包含另一個元件來重複使用程式碼時。 在這種情況下，包含的元件不需要使用其本身的工具列和對話方塊進行編輯，因此不需要包裝函式，且元件的`cq:htmlTag`會被忽略。 可將此視為預設行為。

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

在`/content/test.html`上產生的輸出：

**`Hello World!`**

例如，包含核心影像元件的元件會顯示影像，且通常會使用合成資源來顯示，此情況下包含虛擬子元件，透過將代表元件具備之所有屬性的Map物件傳遞至data-sly-resource來包含虛擬子元件。

#### 使用案例2：包含可編輯的元件 {#use-case-include-an-editable-component}

另一個常見的使用案例是容器元件包含可編輯的子元件，例如配置容器。 在這種情況下，每個包含的子項都需要包裝函式才能讓編輯器運作（除非使用`cq:noDecoration`屬性明確停用）。

由於包含的元件在此情況下是獨立元件，因此它需要包裝函式元素才能讓編輯器運作，並定義其要套用的版面和樣式。 若要觸發此行為，有`decoration=true`選項。

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

在`/content/test.html`上產生的輸出：

**`<article class="component-two">Hello World!</article>`**

#### 使用案例3：自訂行為 {#use-case-custom-behavior}

您可以透過使用HTL明確提供以下內容的方式，輕鬆處理任意數量的複雜案例：

* **`decorationTagName='ELEMENT_NAME'`**&#x200B;定義包裝函式的元素名稱。
* **`cssClassName='CLASS_NAME'`**&#x200B;定義要在其中設定的CSS類別名稱。

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

產生的輸出`/content/test.html`：

**`<aside class="child">Hello World!</aside>`**
