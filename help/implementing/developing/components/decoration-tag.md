---
title: 裝飾標記
description: 轉譯網頁中的元件時可產生 HTML 元素，將轉譯的元件圍在其中。對於開發人員來說，AEM 提供簡單清晰的邏輯，可控制圍住所含元件的裝飾標記。
exl-id: a90fd619-eff6-466f-9178-90374f988b5d
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 10%

---

# 裝飾標記 {#decoration-tag}

轉譯網頁中的元件時可產生 HTML 元素，將轉譯的元件圍在其中。這主要有兩個用途：

* 元件必須以HTML元素包住，才能加以編輯。
* 包裝元素用於套用提供以下內容的HTML類別：
   * 版面資訊
   * 樣式資訊

對於開發人員來說，AEM 提供簡單清晰的邏輯，可控制圍住所含元件的裝飾標記。裝飾標籤的呈現方式及是否由兩個因素的組合所定義，本頁將深入探討：

* 元件本身可以使用一組屬性來設定其裝飾標籤。
* 包含元件的指令碼可以使用包含參數來定義裝飾標籤的方面。

## 建議 {#recommendations}

以下是幾項一般建議，說明何時加入包裝函式元素，有助於避免遇到非預期的問題：

* 包裝器元素的存在在WCMMode（編輯或預覽模式）、例項（製作或發佈）或環境（測試或生產）之間不應有差異，因此頁面的CSS和JavaScripts在所有情況下都會相同。
* 應將包裝器元素新增至所有可編輯的元件，讓頁面編輯器能夠正確初始化和更新這些元件。
* 對於不可編輯的元件，如果包裝器元素不提供特定函式，則可以避免它，這樣產生的標籤就不會不必要的膨脹。

## 元件控制項{#component-controls}

下列屬性和節點可套用至元件，以控制其裝飾標籤的行為：

* **`cq:noDecoration {boolean}`:** 此屬性可新增至元件，若值為true，系統將強制AEM不在元件上產生任何包裝函式元素。
* **`cq:htmlTag`node :** 此節點可新增至元件下，且可具有下列屬性：
   * **`cq:tagName {String}`:** 這可用來指定要用來包裝元件的自訂HTML標籤，而非預設的DIV元素。
   * **`class {String}`:** 這可用來指定要新增至包裝函式的css類別名稱。
   * 其他屬性名稱將新增為HTML屬性，其字串值會與提供的值相同。

## 指令碼控制項{#script-controls}

一般而言，HTL中的包裝函式行為可總結如下：

* 預設不會轉譯包裝器DIV（只執行`data-sly-resource="foo"`時）。
* 所有wcm模式（停用、預覽、在製作和發佈上編輯）的呈現方式相同。

包裝函式的行為也可完全控制。

* HTL指令碼可完全控制包裝函式標籤的產生行為。
* 元件屬性（如`cq:noDecoration`和`cq:tagName`）也可以定義包裝函式標籤。

您可以完全控制HTL指令碼中包裝函式標籤的行為及其相關邏輯。

如需有關以HTL開發的詳細資訊，請參閱[ HTL檔案](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html)。

### 決策樹{#decision-tree}

此決策樹會總結決定包裝器標籤行為的邏輯。

![決策樹](assets/decoration-tag-decision-tree.png)

### 使用案例{#use-cases}

以下三個使用案例提供如何處理包裝函式標籤的範例，並說明控制包裝函式標籤的所需行為有多簡單。

下列所有範例假設有下列內容結構和元件：

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

#### 使用案例1:包含用於代碼重用的元件{#use-case-include-a-component-for-code-reuse}

最常見的使用案例是，由於程式碼重複使用的原因，元件包含其他元件。 在這種情況下，所包含的元件不想使用其自己的工具列和對話方塊進行編輯，因此不需要包裝函式，而元件的`cq:htmlTag`將會被忽略。 這可視為預設行為。

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

在`/content/test.html`上生成輸出：

**`Hello World!`**

例如，元件包括顯示影像的核心影像元件，在這種情況下，通常是使用合成資源，包括通過將表示元件將具有的所有屬性的映射對象傳遞到data-sly-resource來包括虛擬子元件。

#### 使用案例2:包含可編輯的元件{#use-case-include-an-editable-component}

另一個常見使用案例是容器元件包含可編輯的子元件時，例如「版面容器」。 在這種情況下，每個包含的子代都必須有一個包裝函式才能使編輯器工作（除非使用`cq:noDecoration`屬性顯式禁用）。

由於包含的元件在此情況下是獨立元件，因此它需要一個包裝元素才能讓編輯器工作，並定義要套用的版面和樣式。 若要觸發此行為，有`decoration=true`選項。

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

在`/content/test.html`上生成輸出：

**`<article class="component-two">Hello World!</article>`**

#### 使用案例3:自訂行為{#use-case-custom-behavior}

可能會有任何複雜的案例，而HTL可明確提供便於達成：

* **`decorationTagName='ELEMENT_NAME'`** 定義包裝函式的元素名稱。
* **`cssClassName='CLASS_NAME'`** 定義要在其上設定的CSS類名。

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

結果輸出`/content/test.html`:

**`<aside class="child">Hello World!</aside>`**
