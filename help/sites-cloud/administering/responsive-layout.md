---
title: 設定配置容器和配置模式
description: 瞭解如何設定版面容器和版面模式，以便為內容作者啟用回應式版面。
exl-id: 469e8151-8231-4ccc-b7f6-855545f87440
solution: Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# 設定配置容器和配置模式 {#configuring-layout-container-and-layout-mode}

[回應式佈局](/help/sites-cloud/authoring/page-editor/responsive-layout.md)是一種實現[回應式網頁設計的機制。](https://en.wikipedia.org/wiki/Responsive_web_design)這可讓內容作者建立網頁，這些網頁的版面配置和維度與其使用者使用的裝置有關。

AEM使用一組機製為頁面實現回應式佈局：

* **[配置容器](/help/sites-cloud/authoring/page-editor/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)** — 此元件提供格線段落系統，可讓您在回應式格線中新增及放置元件。
   * 它可作為您頁面的預設Parsys使用，和/或在元件瀏覽器中可供作者使用。
   * 預設&#x200B;**配置容器**&#x200B;元件定義在`/libs/wcm/foundation/components/responsivegrid`下。
   * 您可以定義配置容器：
      * 作為使用者可新增至頁面的元件。
      * 做為頁面的預設parsys。
      * 作為元件和預設parsys。
         * 您可以將版面容器設為頁面的標準版面容器，同時允許使用者在此容器中新增更多版面容器；例如，實現欄控制。
* **[佈局模式](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)** — 一旦佈局容器放置到您的頁面上，您就可以使用&#x200B;**佈局**&#x200B;模式在回應式格線內放置內容。
* **[模擬器](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate)** — 這可讓您建立並編輯回應式網站，這些網站會根據裝置/視窗大小，以互動方式調整元件大小，重新排列版面。 之後，使用者可以使用模擬器檢視內容的呈現方式。

利用這些回應式格點機制，您可以：

* 使用中斷點（表示裝置分組）可依據裝置配置定義不同的內容行為。
* 根據裝置群組隱藏元件（定義元件將隱藏在哪個中斷點）。
* 使用水準貼齊格點（將元件放入格點，視需要調整大小，定義它們何時應該摺疊/重排成並排或上下對齊）。
* 實現欄控制。

>[!NOTE]
>
>從[專案原型](#addlink)或從[標準網站範本](#addlink)建立網站時，通常會設定回應式配置。 否則，您必須為頁面[啟動配置容器元件](#enable-the-layout-container-component-for-page)。

## 啟用模擬器 {#enabling-emulator}

[專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)和[標準網站範本](/help/sites-cloud/administering/site-creation/site-templates.md#standard-site-template)已經啟用，可以使用模擬器。 如果您不是根據核心元件或原型開發自己的內容，請參閱檔案[回應式設計](/help/implementing/developing/introduction/responsive-design.md)，瞭解如何利用這些功能開發元件的詳細資訊。

## 啟用網站的佈局模式 {#activate-layout-mode-for-your-site}

**配置**&#x200B;模式允許您使用模擬器來調整不同裝置的內容配置。 WKND範例網站已針對&#x200B;**配置**&#x200B;模式啟用。 請依照下列步驟啟用您自己的網站。

### 設定中斷點 {#configure-breakpoints}

中斷點對於回應式設計而言至關重要，而且可定義將內容調整至目標裝置的方法和時機。 不過，請務必小心，因為您引進的每個中斷點都會為作者產生額外的工作，以便容納內容。 很多時候，兩個中斷點就足夠了，包括永遠存在的預設中斷點。 Adobe建議不要建立超過三個中斷點，包括預設值，亦即在`cq:responsive/breakpoint`下不超過兩個節點。

* 中斷點具有標題和寬度：
   * 標題說明一般裝置群組，並視需要提供方向。
      * 例如，`phone`， `tablet`
   * 寬度會定義該一般裝置群組的最大寬度（畫素）。
      * 例如，如果中斷點電話的寬度為768，那麼就會是電話裝置所使用的配置寬度上限。
* 可以定義中斷點：
   * 在頁面範本上，設定會從中複製到使用該範本建立的任何頁面。
   * 在頁面節點上，任何子頁面會從中繼承設定。
* 使用模擬器時，中斷點會在頁面編輯器頂端顯示為標籤。
* 中斷點繼承自父節點階層，並可隨意覆寫。
* 有一個預設（現成）中斷點，其涵蓋了上次設定的中斷點以上所有內容。
* 可以使用CRXDE Lite或XML定義中斷點。

新專案和現有專案都應該考量中斷點。

* 如果您要設定新專案，則應將中斷點新增至範本。
* 如果您要移轉現有專案（包含現有內容），您必須：
   * 將中斷點新增至範本。
   * 將相同的中斷點新增至現有頁面。

由於繼承關係，您只需對內容的根頁面執行此動作。

#### 使用CRXDE Lite設定中斷點 {#configuring-breakpoints-using-crxde-lite}

1. 使用CRXDE Lite，導覽至：

   * 您的範本定義。
   * 您頁面的`jcr:content`節點。

1. 在`jcr:content`下建立節點：

   * 名稱：`cq:responsive`
   * 類型：`nt:unstructured`

1. 在此之下建立節點：

   * 名稱：`breakpoints`
   * 類型：`nt:unstructured`

1. 在中斷點節點下，您可以建立任意數目的中斷點。 每個定義都是具有下列屬性的單一節點：

   * 名稱：`<descriptive name>`
   * 類型：`nt:unstructured`
   * 標題： `String <descriptive title seen in Emulator>`
   * 寬度： `Decimal <value of breakpoint>`

#### 使用XML設定中斷點 {#configuring-breakpoints-using-xml}

中斷點位於`.context.html`的`<jcr:content>`區段內，在適當的範本（或內容）資料夾下。

範例定義：

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

## 啟用頁面元件大小調整 {#enable-component-resizing-for-the-page}

在&#x200B;**配置**&#x200B;模式中調整元件大小是回應式設計的重要部分，可以在WKND範例網站中使用。 請依照下列步驟啟用您自己的網站。

### 將配置容器設定為主要Parsys {#set-layout-container-as-main-parsys}

若要將頁面的主要parsys設定為配置容器，請將parsys定義為：

`wcm/foundation/components/responsivegrid`

在：

* 頁面元件
* 頁面範本（供日後使用）

以下兩個範例說明定義：

* **HTL：**

  ```xml
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP：**

  ```xml
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### 包含回應式CSS {#include-the-responsive-css}

#### 使用LESS的中斷點CSS {#css-for-breakpoints-using-less}

AEM使用LESS來產生必要CSS的部分，這些需要包含在您的專案中。

您必須建立[使用者端程式庫](/help/implementing/developing/introduction/clientlibs.md)，以提供額外的設定和函式呼叫。 以下LESS擷取是您必須新增至專案的最小值範例：

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

基底格點定義可在下列位置找到：

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 樣式考量事項 {#styling-considerations}

保持在回應式容器中的元件會根據回應式格線大小調整大小(連同其各自的HTMLDOM元素)。 因此，在這些情況下，建議避免（或更新）固定寬度（包含） DOM元素的定義。

例如：

* 之前：

   * `width=100px`

* 之後：

   * `max-width=100px`

#### 調整大小和調整影像法規遵循 {#resizing-and-adaptive-image-compliance}

在格線內調整元件大小的任何動作，都會視情況觸發下列接聽程式：

* `beforeedit`
* `beforechildedit`
* `afteredit`
* `afterchildedit`

若要正確調整回應式格線中所包含的最適化影像內容大小並加以更新，您必須將設為`REFRESH_PAGE`的`afterEdit`接聽程式新增至每個所包含元件的`EditConfig`檔案。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

可透過指令碼使用最適化影像機制，該指令碼控制選擇符合目前視窗大小的正確影像。 在DOM準備就緒或收到專用事件時，它會啟動。 目前必須重新整理頁面，才能正確反映使用者動作的結果。

>[!CAUTION]
>
>自訂樣式表clientlibs必須載入為標頭的一部分，才能在製作及發佈上正確運作。

## 啟用頁面的配置容器元件 {#enable-the-layout-container-component-for-page}

為了達到有效的回應式佈局，內容作者必須能夠將「佈局容器」元件的例項拖曳到頁面上。 WKND範例網站已啟用此功能。 請依照下列步驟啟用您自己的網站。

### 啟用配置容器元件以進行頁面編輯 {#enable-the-layout-container-component-for-page-editing}

若要讓作者更能回應式地新增網格至內容頁面，您必須啟用頁面的「配置容器」元件。 您可以透過以下其中一種方式來達成此目的：

* **透過作者環境** - [編輯您的頁面範本](/help/sites-cloud/authoring/sites-console/templates.md)以啟用頁面的配置容器。
* **元件定義** — 在定義元件時使用`allowedComponent`或靜態包含。

### 設定配置容器的格線 {#configure-the-grid-of-the-layout-container}

您可以編輯您的頁面範本，設定配置容器[的每個特定執行個體可用的欄數。](/help/sites-cloud/authoring/sites-console/templates.md)
