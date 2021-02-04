---
title: 在AEM中編輯外部SPA
description: 本檔案說明將獨立SPA上傳至AEM例項、新增可編輯的內容區段以及啟用編寫的建議步驟。
translation-type: tm+mt
source-git-commit: bb8ab907dbeb422db410328f9c559c6794c16a8f
workflow-type: tm+mt
source-wordcount: '2127'
ht-degree: 0%

---

# 在AEM {#editing-external-spa-within-aem}中編輯外部SPA

在決定您要在外部SPA和AEM之間使用何種整合等級[時，您通常需要能夠編輯並檢視AEM中的SPA。](/help/implementing/developing/headful-headless.md)

## 概覽 {#overview}

本檔案說明將獨立SPA上傳至AEM例項、新增可編輯的內容區段以及啟用編寫的建議步驟。

## 必備條件 {#prerequisites}

先決條件很簡單。

* 請確定AEM的例項是在本機執行。
* 使用[AEM Project Archetype建立基本AEM SPA專案。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)
   * 這將構成AEM專案的基礎，此專案將會更新以包含外部SPA。
   * 對於本文檔中的示例，我們使用[WKND SPA項目的起點。](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)
* 擁有您想要在手邊整合的正常外部React SPA。

## 將SPA上傳至AEM專案{#upload-spa-to-aem-project}

首先，您需要將外部SPA上傳至您的AEM專案。

1. 將`/ui.frontend`專案資料夾中的`src`取代為React應用程式的`src`資料夾。
1. 在應用程式的`package.json`檔案中，加入其他相依性。`/ui.frontend/package.json`
   * 確保SPA SDK相依性為[建議版本。](/help/implementing/developing/hybrid/getting-started-react.md#dependencies)
1. 在`/public`資料夾中加入任何自訂項目。
1. 在`/public/index.html`檔案中加入任何內嵌指令碼或樣式。

## 配置遠程SPA {#configure-remote-spa}

現在，外部SPA已包含在您的AEM專案中，因此必須在AEM中設定它。

### 包含Adobe SPA SDK套件{#include-spa-sdk-packages}

若要運用AEM SPA功能，請依賴下列三個套件。

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` 提供API，以初始化「模型管理員」並從AEM例項擷取模型。然後，此模型可用來使用`@adobe/aem-react-editable-components`和`@adobe/aem-spa-component-mapping`的API來轉換AEM元件。

#### 安裝{#installation}

運行以下npm命令以安裝所需的軟體包。

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManager初始化{#model-manager-initialization}

在應用程式轉譯之前，[`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)必須進行初始化，才能處理AEM `ModelStore`的建立作業。

這必須在應用程式的`src/index.js`檔案中，或在產生應用程式根目錄的任何地方完成。

對此，我們可以使用`ModelManager`提供的`initializationAsync` API。

以下螢幕擷取顯示如何在簡單的React應用程式中啟用初始化`ModelManager`。 唯一的限制是`initializationAsync`需要在`ReactDOM.render()`之前呼叫。

![初始化ModelManager](assets/external-spa-initialize-modelmanager.png)

在此示例中，初始化`ModelManager`並建立空`ModelStore`。

`initializationAsync` 可以選擇接受 `options` 對象作為參數：

* `path` -初始化時，將讀取定義路徑上的模型並將其儲存在中 `ModelStore`。如有需要，可使用此選項在初始化時讀取`rootModel`。
* `modelClient` -允許提供負責讀取模型的自定義客戶端。
* `model` -使用 `model` SSR時通常以參數形式傳遞 [的對象。](/help/implementing/developing/hybrid/ssr.md)

### AEM可授權葉元件{#authorable-leaf-components}

1. 建立／識別將為其建立可授權React元件的AEM元件。 在此示例中，我們使用WKND項目的文本元件。

   ![WKND文字元件](assets/external-spa-text-component.png)

1. 在SPA中建立簡單的React文字元件。 在此示例中，已使用以下內容建立了新檔案`Text.js`。

   ![Text.js](assets/external-spa-textjs.png)

1. 建立設定物件，以指定啟用AEM編輯所需的屬性。

   ![建立配置對象](assets/external-spa-config-object.png)

   * `resourceType` 必須將React元件對應至AEM元件，並在AEM編輯器中開啟時啟用編輯。

1. 使用包裝函式`withMappable`。

   ![與Mappable一起使用](assets/external-spa-withmappable.png)

   此包裝函式會將React元件對應至設定中指定的AEM `resourceType`，並在AEM編輯器中開啟時啟用編輯功能。 對於獨立元件，它還將獲取特定節點的模型內容。

   >[!NOTE]
   >
   >在此範例中，元件有個別版本：AEM包裝和解封React元件。 明確使用元件時，必須使用包裝版本。 當元件是頁面的一部分時，您可以繼續使用目前在SPA編輯器中完成的預設元件。

1. 在元件中演算內容。

   文字元件的JCR屬性在AEM中的顯示如下。

   ![文字元件屬性](assets/external-spa-text-properties.png)

   這些值會作為屬性傳遞給新建立的`AEMText` React元件，並可用來轉換內容。

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   這是當AEM設定完成時，元件的顯示方式。

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >在此範例中，我們進一步自訂演算的元件，以符合現有的文字元件。 但這與在AEM中編寫無關。

#### 將可授權元件新增至頁面{#add-authorable-component-to-page}

建立可授權的React元件後，我們就可以在整個應用程式中使用這些元件。

讓我們舉一個範例頁面，其中需要從WKND SPA專案新增文字。 在此範例中，我們要顯示文字&quot;Hello World!&quot; 於 `/content/wknd-spa-react/us/en/home.html`.

1. 確定要顯示的節點路徑。

   * `pagePath`:包含節點的頁面，在我們的範例中  `/content/wknd-spa-react/us/en/home`
   * `itemPath`:頁面內節點的路徑，在我們的範例中  `root/responsivegrid/text`
      * 這包括頁面上包含項目的名稱。

   ![節點的路徑](assets/external-spa-path.png)

1. 在頁面的必要位置新增元件。

   ![新增元件至頁面](assets/external-spa-add-component.png)

   `AEMText`元件可在頁面內的必要位置新增，其中`pagePath`和`itemPath`值設為屬性。 `pagePath` 是強制屬性。

#### 驗證在AEM {#verify-text-edit}上編輯文字內容

我們現在可以在執行中的AEM例項上測試元件。

1. 從`aem-guides-wknd-spa`目錄執行下列Maven命令，以建立專案並部署至AEM。

```shell
mvn clean install -PautoInstallSinglePackage
```

1. 在您的AEM例項上，導覽至`http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`。

![在AEM中編輯SPA](assets/external-spa-edit-aem.png)

`AEMText`元件現在可在AEM上授權。

### AEM可授權頁面{#aem-authorable-pages}

1. 識別要新增以在SPA中編寫的頁面。 此示例使用`/content/wknd-spa-react/us/en/home.html`。
1. 建立新檔案(例如`Page.js`)。 在這裡，我們可以重複使用`@adobe/cq-react-editable-components`中提供的頁面元件。
1. 在[AEM可授權葉片元件區段中重複步驟4。](#authorable-leaf-components) 在元件上使 `withMappable` 用wrapper函式。
1. 如先前所做，請套用`MapTo`至頁面內所有子元件的AEM資源類型。

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >在此示例中，我們使用未包裝的React文本元件，而不是先前建立的包裝的`AEMText`。 這是因為，當元件是頁面／容器的一部分，而非獨立時，容器將負責遞歸對應元件並啟用編寫功能，而且每個子系不需要額外的包裝函式。

1. 若要在SPA中新增可授權頁面，請依照[將可授權元件新增至頁面中相同的步驟進行。](#add-authorable-component-to-page) 不過，我們可以在此略過 `itemPath` 屬性。

#### 驗證AEM {#verify-page-content}上的頁面內容

若要確認頁面可以編輯，請依照[「驗證編輯AEM上的文字內容」一節中的相同步驟進行。](#verify-text-edit)

![在AEM中編輯頁面](assets/external-spa-edit-page.png)

頁面現在可在AEM上編輯，其中包含版面容器和子文字元件。

### 虛擬葉元件{#virtual-leaf-components}

在先前的範例中，我們新增元件至SPA並包含現有的AEM內容。 不過，有些情況下，內容尚未在AEM中建立，但需要由內容作者稍後新增。 為配合此需求，前端開發人員可在SPA的適當位置新增元件。 當在AEM的編輯器中開啟時，這些元件會顯示預留位置。 內容作者在這些預留位置中新增內容後，就會在JCR結構中建立節點，並保留內容。 建立的元件將允許與獨立葉元件相同的操作集。

在此示例中，我們重複使用以前建立的`AEMText`元件。 我們希望在WKND首頁的現有文本元件下添加新文本。 添加的組分與普通葉元件相同。 但是，`itemPath`可以更新為需要添加新元件的路徑。

由於新元件必須新增至`root/responsivegrid/text`的現有文字下方，因此新路徑應為`root/responsivegrid/{itemName}`。

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

添加虛擬元件後，`TestPage`元件如下所示。

![測試虛擬元件](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>確保`AEMText`元件在配置中設定了`resourceType`以啟用此功能。

您現在可以依照[「確認編輯AEM上的文字內容」一節中的步驟，將變更部署至AEM。](#verify-text-edit) 將顯示當前非現有節點的佔位符 `text_20` 。

![aem中的text_20節點](assets/external-spa-text20-aem.png)

當內容作者更新此元件時，會在`/content/wknd-spa-react/us/en/home`的`root/responsivegrid/text_20`中建立新的`text_20`節點。

![text20節點](assets/external-spa-text20-node.png)

#### 要求與限制{#limitations}

添加虛擬葉元件有許多要求，也有一些限制。

* `pagePath`屬性是建立虛擬元件的必備屬性。
* `pagePath`路徑中提供的頁面節點必須存在於AEM專案中。
* `itemPath`中必須提供要建立的節點的名稱。
* 可在任何級別建立元件。
   * 如果我們在上例中提供`itemPath='text_20'`，則新節點將直接在頁面(如`/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* 通過`itemPath`提供時，建立新節點的節點路徑必須有效。
   * 在此示例中，`root/responsivegrid`必須存在，以便在此處建立新節點`text_20`。
* 僅支援葉元件建立。 未來版本將支援虛擬容器和頁面。

## 其他自定義{#additional-customizations}

如果您遵循先前的範例，現在可在AEM中編輯您的外部SPA。 不過，您可進一步自訂外部SPA的其他方面。

### 根節點ID {#root-node-id}

依預設，我們假設React應用程式會呈現在元素ID `spa-root`的`div`中。 如有需要，可自訂此選項。

例如，假設我們有一個SPA，在該SPA中，應用程式會呈現在元素ID `root`的`div`內。 這必須反映在三個檔案中。

1. 在React應用程式的`index.js`中（或呼叫`ReactDOM.render()`的位置）

   ![index.js檔案中的ReactDOM.render()](assets/external-spa-root-index.png)

1. 在React應用程式的`index.html`中

   ![應用程式的index.html](assets/external-spa-index.png)

1. 在AEM應用程式的頁面元件內文中，透過兩個步驟：

   1. 為頁面元件建立新的`body.html`。

   ![建立新的body.html檔案](assets/external-spa-update-body.gif)

   1. 在新的`body.html`檔案中新增根元素。

   ![將根元素新增至body.html](assets/external-spa-add-root.png)

### 使用路由編輯React SPA {#editing-react-spa-with-routing}

如果外部React SPA應用程式具有多個頁，[它可以使用路由來確定要渲染的頁／元件。](/help/implementing/developing/hybrid/routing.md) 基本使用案例是將目前作用中的URL與路由提供的路徑相符。若要啟用此類可路由傳送的應用程式編輯，必須轉換要比對的路徑，以容納AEM特定的資訊。

在下列範例中，我們提供包含兩頁的簡單React應用程式。 要呈現的頁面是通過將提供給路由器的路徑與活動URL匹配來確定的。 例如，如果我們位於`mydomain.com/test`，則會呈現`TestPage`。

![外部SPA中的路由](assets/external-spa-routing.png)

若要在AEM中為此範例SPA啟用編輯，必須執行下列步驟。

1. 識別可做為AEM根目錄的層級。

   * 對於我們的樣本，我們考慮將wknd-spa-react/us/en作為SPA的根。 這表示該路徑之前的所有項目都只有AEM頁面／內容。

1. 在所需層級建立新頁面。

   * 在此範例中，要編輯的頁面為`mydomain.com/test`。 `test` 位於應用程式的根路徑中。在AEM中建立頁面時，也需要保留此項。 因此，我們可以在上一步驟中定義的根級別建立新頁面。
   * 建立的新頁面必須與要編輯的頁面具有相同的名稱。 在此示例中，對於`mydomain.com/test`，建立的新頁必須是`/path/to/aem/root/test`。

1. 在SPA路由中添加幫手。

   * 新建立的頁面尚未在AEM中呈現預期的內容。 這是因為路由器預期路徑為`/test` ，而AEM活動路徑為`/wknd-spa-react/us/en/test`。 為了容納URL的AEM特定部分，我們需要在SPA端新增一些協助工具。

   ![路由輔助工具](assets/external-spa-router-helper.png)

   * `@adobe/cq-spa-page-model-manager`提供的`toAEMPath`幫助程式可用於此。 當應用程式在AEM例項上開啟時，它會將提供的路由路由路徑變更為包含AEM特定部分。 它接受三個參數：
      * 路由所需的路徑
      * 編輯SPA之AEM例項的原始URL
      * AEM上的專案根（在第一個步驟中決定）
   * 這些值可設為環境變數，以提供更大的彈性。



1. 確認在AEM中編輯頁面。

   * 將專案部署至AEM，並導覽至新建立的`test`頁面。 現在會轉譯頁面內容，而且AEM元件是可編輯的。

## 其他資源 {#additional-resources}

下列參考資料可協助您瞭解AEM中的SPA。

* [AEM中的Headful和Headless](/help/implementing/developing/headful-headless.md)
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [WKND SPA專案](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [在AEM中使用React快速入門SPA](/help/implementing/developing/hybrid/getting-started-react.md)
* [SPA參考資料（API參考）](/help/implementing/developing/hybrid/reference-materials.md)
* [SPA Blueprint和PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [SPA模型路由](/help/implementing/developing/hybrid/routing.md)
* [SPA和伺服器端演算](/help/implementing/developing/hybrid/ssr.md)
