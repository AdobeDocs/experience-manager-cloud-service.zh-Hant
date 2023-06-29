---
title: 在 AEM 中編輯外部 SPA
description: 本檔案說明將獨立SPA上傳至AEM執行個體、新增可編輯的內容區段及啟用編寫的建議步驟。
exl-id: 7978208d-4a6e-4b3a-9f51-56d159ead385
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2421'
ht-degree: 1%

---

# 在 AEM 中編輯外部 SPA {#editing-external-spa-within-aem}

決定時 [哪一個層級的整合](/help/implementing/developing/headful-headless.md) 您想要在外部SPA和AEM之間切換，請考量您通常必須能夠在AEM內編輯和檢視SPA。

## 概觀 {#overview}

本檔案說明將獨立SPA上傳至AEM執行個體、新增可編輯的內容區段及啟用編寫的建議步驟。

## 必備條件 {#prerequisites}

先決條件很簡單。

* 確定AEM的執行個體正在本機執行。
* 建立基礎AEM SPA專案，使用 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties).
   * Forms是AEM專案的基礎，已更新以包含外部SPA。
   * 對於本檔案中的範例，Adobe是使用 [WKND SPA專案](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor).
* 準備好您想要整合的可使用的外部React SPA。

## 上傳SPA至AEM專案 {#upload-spa-to-aem-project}

首先，您必須將外部SPA上傳至您的AEM專案。

1. Replace `src` 在 `/ui.frontend` 含有您React應用程式的專案資料夾 `src` 資料夾。
1. 在應用程式的 `package.json` 在 `/ui.frontend/package.json` 檔案。
   * 確保SPA SDK相依性屬於 [建議版本](/help/implementing/developing/hybrid/getting-started-react.md#dependencies).
1. 將任何自訂專案納入 `/public` 資料夾。
1. 包含任何新增至中的任何內嵌指令碼或樣式 `/public/index.html` 檔案。

## 設定遠端SPA {#configure-remote-spa}

現在，外部SPA已成為AEM專案的一部分，因此必須在AEM中進行設定。

### 包含AdobeSPA SDK套件 {#include-spa-sdk-packages}

若要利用AEM SPA功能，需依賴下列三個套件。

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/login?next=/package/@adobe/aem-spa-model-manager)

此 `@adobe/aem-spa-page-model-manager` 套件提供初始化模型管理員和從AEM執行個體擷取模型的API。 然後，此模型可用於使用來自的API轉譯AEM元件 `@adobe/aem-react-editable-components` 和 `@adobe/aem-spa-component-mapping`.

#### 安裝 {#installation}

執行以下命令 `npm` 命令，讓您安裝所需的套裝軟體。

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManager初始化 {#model-manager-initialization}

在應用程式轉譯之前， [`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager) 必須初始化才能處理AEM的建立 `ModelStore`.

此初始化必須在 `src/index.js` 應用程式的檔案，或是呈現應用程式根目錄的位置。

若要進行此初始化，您可以使用 `initializationAsync` API由 `ModelManager`.

下列熒幕擷圖顯示如何啟用 `ModelManager` 在簡單的React應用程式中。 唯一的限制是 `initializationAsync` 必須在之前呼叫 `ReactDOM.render()`.

![初始化ModelManager](assets/external-spa-initialize-modelmanager.png)

在此範例中， `ModelManager` 已初始化且為空白 `ModelStore` 「 」已建立。

此 `initializationAsync` 可選擇接受 `options` 物件作為引數：

* `path`  — 初始化時，會擷取定義路徑處的模型並儲存在 `ModelStore`. 此路徑可用來擷取 `rootModel` 初始化時（如有需要）。
* `modelClient`  — 允許提供負責擷取模型的自訂使用者端。
* `model` - A `model` 作為引數傳遞的物件通常在 [使用SSR](/help/implementing/developing/hybrid/ssr.md).

### AEM可授權分葉元件 {#authorable-leaf-components}

1. 建立/識別已為其建立可授權的React元件的AEM元件。 在此範例中，它使用WKND專案的文字元件。

   ![WKND文字元件](assets/external-spa-text-component.png)

1. 在SPA中建立簡單的React文字元件。 在此範例中，新檔案 `Text.js` 已使用下列內容建立。

   ![Text.js](assets/external-spa-textjs.png)

1. 建立組態物件，讓您指定啟用AEM編輯所需的屬性。

   ![建立設定物件](assets/external-spa-config-object.png)

   * `resourceType` 在AEM編輯器中開啟時，必須將React元件對應至AEM元件並啟用編輯功能。

1. 使用包裝函式 `withMappable`.

   ![使用withMappable](assets/external-spa-withmappable.png)

   此包裝函式將React元件對應至AEM `resourceType` 在config中指定，並在AEM編輯器中開啟時啟用編輯功能。 對於獨立元件，它也會擷取特定節點的模型內容。

   >[!NOTE]
   >
   >在此範例中，有不同版本的元件： AEM包裝和未包裝的React元件。 明確使用元件時，必須使用包裝的版本。 當元件是頁面的一部分時，您可以繼續使用預設元件，就像目前在SPA編輯器中完成的一樣。

1. 呈現元件中的內容。

   文字元件的JCR屬性在AEM中會顯示如下。

   ![文字元件屬性](assets/external-spa-text-properties.png)

   這些值會以屬性形式傳遞至新建立的 `AEMText` React元件，且可用於呈現內容。

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

   以下是AEM設定完成時元件的顯示方式。

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
   >在此範例中，已對轉譯的元件進行進一步自訂，以符合現有的文字元件。 這與AEM中的撰寫無關。

#### 將可編寫的元件新增至頁面 {#add-authorable-component-to-page}

建立可授權的React元件後，即可在整個應用程式中使用這些元件。

讓我們舉一個您必須從WKND SPA專案新增文字的範例頁面。 在此範例中，您想要顯示文字「Hello World！」 於 `/content/wknd-spa-react/us/en/home.html`.

1. 決定要顯示的節點路徑。

   * `pagePath`：此範例中包含節點的頁面 `/content/wknd-spa-react/us/en/home`
   * `itemPath`：此範例中頁面內節點的路徑 `root/responsivegrid/text`
      * 由頁面上包含專案的名稱組成。

   ![節點的路徑](assets/external-spa-path.png)

1. 在頁面的所需位置新增元件。

   ![將元件新增至頁面](assets/external-spa-add-component.png)

   此 `AEMText` 元件可新增至頁面內的所需位置，並具有 `pagePath` 和 `itemPath` 設定為屬性的值。 `pagePath` 是強制屬性。

#### 驗證在AEM上編輯文字內容 {#verify-text-edit}

現在請在執行中的AEM例項上測試元件。

1. 從以下位置執行以下Maven命令： `aem-guides-wknd-spa` 目錄，讓您可以建置專案並將其部署到AEM。

```shell
mvn clean install -PautoInstallSinglePackage
```

1. 在您的AEM執行個體上，導覽至 `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![在AEM中編輯SPA](assets/external-spa-edit-aem.png)

此 `AEMText` 元件現在可在AEM上編寫。

### AEM可編寫頁面 {#aem-authorable-pages}

1. 識別要新增以在SPA中編寫的頁面。 此範例使用 `/content/wknd-spa-react/us/en/home.html`.
1. 建立檔案(例如， `Page.js`)時，不會顯示任何文字。 使用中提供的頁面元件 `@adobe/cq-react-editable-components`.
1. 在區段中重複步驟4 [AEM可授權分葉元件](#authorable-leaf-components). 使用包裝函式 `withMappable` 在元件上。
1. 如同先前一樣，套用 `MapTo` 至頁面中所有子元件的AEM資源型別。

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >在此範例中，會使用未包裝的React文字元件，而非包裝的 `AEMText` 先前建立。 原因是因為當元件是頁面/容器的一部分而不是獨立時，容器會負責遞回對應元件。 此外，每個子項也不需要啟用編寫功能和其他包裝函式。

1. 若要在SPA中新增可授權頁面，請遵循區段中的相同步驟 [將可編寫的元件新增至頁面](#add-authorable-component-to-page). 在這裡，您可以略過 `itemPath` 屬性。

#### 驗證AEM上的頁面內容 {#verify-page-content}

若要驗證頁面是否可以編輯，請遵循區段中的相同步驟 [驗證在AEM上編輯文字內容](#verify-text-edit).

![在AEM中編輯頁面](assets/external-spa-edit-page.png)

頁面現在可以在具有版面容器和子文字元件的AEM上編輯。

### 虛擬分葉元件 {#virtual-leaf-components}

在前述範例中，您使用現有AEM內容將元件新增至SPA。 但是，在某些情況下，內容尚未在AEM中建立，但必須由內容作者稍後新增。 為因應這種情況，前端開發人員可以在SPA內的適當位置新增元件。 在AEM的編輯器中開啟這些元件時，會顯示預留位置。 內容作者將內容新增到這些預留位置後，會在JCR結構中建立節點，並持續保留內容。 建立的元件允許與獨立葉元件相同的操作集。

在此範例中，您會重複使用 `AEMText` 先前建立的元件。 您想要在WKND首頁上的現有文字元件下方新增文字。 新增的元件與一般葉元件相同。 不過， `itemPath` 可更新至必須新增新元件的路徑。

因為新元件必須新增到現有文字下方 `root/responsivegrid/text`，新路徑為 `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

此 `TestPage` 新增虛擬元件後，元件如下所示。

![測試虛擬元件](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>確保 `AEMText` 元件有其 `resourceType` 在設定中設定，以便您可以啟用此功能。

您現在可以依照一節中的步驟將變更部署至AEM [驗證在AEM上編輯文字內容](#verify-text-edit). 此時會顯示目前不存在的預留位置 `text_20` 節點。

![aem中的text_20節點](assets/external-spa-text20-aem.png)

內容作者更新此元件時，會新增一個 `text_20` 節點建立於 `root/responsivegrid/text_20` 在 `/content/wknd-spa-react/us/en/home`.

![text20節點](assets/external-spa-text20-node.png)

#### 要求和限制 {#limitations}

新增虛擬分葉元件有幾項需求和幾項限制。

* 此 `pagePath` 屬性是建立虛擬元件的必要專案。
* 中的路徑所提供的頁面節點 `pagePath` 必須在AEM專案中。
* 要建立的節點名稱必須提供在 `itemPath`.
* 可在任何層級建立元件。
   * 如果您提供 `itemPath='text_20'` 在上一個範例中，新節點會直接建立於頁面下方，即 `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* 透過提供時，建立新節點所在節點的路徑必須有效 `itemPath`.
   * 在此範例中， `root/responsivegrid` 必須存在，才能使用新節點 `text_20` 可以在那裡建立。
* 僅支援建立分葉元件。 未來版本將支援虛擬容器和頁面。

### 虛擬容器 {#virtual-containers}

即使尚未在AEM中建立對應的容器，也支援新增容器的功能。 概念和方法類似於 [虛擬分葉元件](#virtual-leaf-components).

前端開發人員可以在AEM內的適當位置新增容器元件，這些元件在SPA的編輯器中開啟時會顯示預留位置。 然後，作者可以將元件及其內容新增到容器中，容器會在JCR結構中建立所需的節點。

例如，如果容器存在於 `/root/responsivegrid`，而開發人員想要新增子容器：

![容器位置](assets/container-location.png)

此 `newContainer` 尚未存在於AEM中。

在AEM中編輯包含此元件的頁面時，會顯示空的容器預留位置，作者可在此位置新增內容。

![容器預留位置](assets/container-placeholder.png)

![JCR中的容器位置](assets/container-jcr-structure.png)

一旦作者將子元件新增至容器後，新容器節點就會以JCR結構中的對應名稱建立。

![包含內容的容器](assets/container-with-content.png)

![包含JCR中內容的容器](assets/container-with-content-jcr.png)

現在可以根據作者的需要將更多元件和內容新增到容器中，且變更會持續存在。

#### 要求和限制 {#container-limitations}

新增虛擬容器有幾項需求和幾項限制。

* 判斷可新增哪些元件的原則繼承自父容器。
* 要建立的容器的直接父系必須存在於AEM中。
   * 如果容器 `root/responsivegrid` 存在於AEM容器中，則可提供路徑以建立新容器 `root/responsivegrid/newContainer`.
   * 但是 `root/responsivegrid/newContainer/secondNewContainer` 是不可能的。
* 一次只能建立一個新層級的元件。

## 其他自訂 {#additional-customizations}

如果您依照前面的範例進行，您現在可以在AEM內編輯外部SPA。 不過，您外部SPA還有其他方面可以進一步自訂。

### 根節點ID {#root-node-id}

依預設，您可以假設React應用程式呈現在內部 `div` 元素ID的 `spa-root`. 如有需要，可自訂此語法。

例如，假設您有SPA，應用程式會呈現在內部 `div` 元素ID的 `root`. 此語法必須反映在三個檔案中。

1. 在 `index.js` React應用程式的(或 `ReactDOM.render()` 稱為)

   ![index.js檔案中的ReactDOM.render()](assets/external-spa-root-index.png)

1. 在 `index.html` React應用程式的

   ![應用程式的index.html](assets/external-spa-index.png)

1. 在AEM應用程式的頁面元件內文中，透過兩個步驟：

   1. 建立 `body.html` （頁面元件）。

   ![建立body.html檔案](assets/external-spa-update-body.gif)

   1. 在新的中新增根元素 `body.html` 檔案。

   ![將根元素新增至body.html](assets/external-spa-add-root.png)

### 編輯React SPA與路由 {#editing-react-spa-with-routing}

如果外部React SPA應用程式有多個頁面， [它可使用路由來決定要轉譯的頁面/元件](/help/implementing/developing/hybrid/routing.md). 基本的使用案例是將目前作用中的URL與為路由提供的路徑進行比對。 若要在啟用路由的應用程式上啟用編輯，必須轉換要比對的路徑以容納AEM的特定資訊。

在以下範例中，您有一個包含兩個頁面的簡單React應用程式。 要呈現的頁面是根據提供給路由器的路徑與作用中URL相符來決定。 例如，如果您在 `mydomain.com/test`， `TestPage` 已呈現。

![外部SPA中的路由](assets/external-spa-routing.png)

若要在AEM中啟用此範例SPA的編輯功能，需要下列步驟。

1. 識別將當作AEM根的層級。

   * 對於您的範例，將wknd-spa-react/us/en視為SPA的根。 此根目錄表示該路徑之前的所有內容都只有AEM頁面/內容。

1. 在所需層級建立頁面。

   * 在此範例中，要編輯的頁面為 `mydomain.com/test`. `test` 在應用程式的根路徑中。 在AEM中建立頁面時，也必須保留此根路徑。 因此，您可以在先前步驟中定義的根層級建立頁面。
   * 建立的新頁面必須與要編輯的頁面同名。 在此範例中，針對 `mydomain.com/test`，建立的新頁面必須 `/path/to/aem/root/test`.

1. 在SPA路由中新增協助程式。

   * 新建立的頁面尚無法在AEM中轉譯預期的內容。 原因是因為路由器預期路徑為 `/test` 而AEM作用中路徑是 `/wknd-spa-react/us/en/test`. 若要適應AEM特定的URL部分，您必須在SPA端新增一些協助程式。

   ![路由協助程式](assets/external-spa-router-helper.png)

   * 此 `toAEMPath` 協助程式提供者： `@adobe/cq-spa-page-model-manager` 可使用。 它會轉換為路由提供的路徑，以便在AEM例項上開啟應用程式時包含AEM的特定部分。 它接受三個引數：
      * 路由所需的路徑
      * 編輯SPA的AEM執行個體的來源URL
      * AEM上的專案根目錄，如第一個步驟所決定

   * 這些值可以設定為環境變數，以獲得更多彈性。

1. 驗證是否在AEM中編輯頁面。

   * 將專案部署到AEM並導覽至新建立的 `test` 頁面。 頁面內容現已呈現，且AEM元件可供編輯。

## 框架限制 {#framework-limitations}

RemotePage元件預期實作會提供如下的資產資訊清單 [可在此處找到](https://github.com/shellscape/webpack-manifest-plugin). 不過，RemotePage元件僅經過測試，可用於React架構（以及透過remote-page-next元件的Next.js），因此不支援從其他架構(例如Angular)遠端載入應用程式。

## 其他資源 {#additional-resources}

下列參考資料可能有助於瞭解AEM內容中的SPA。

* [AEM Headful 和 Headless 技術](/help/implementing/developing/headful-headless.md)
* [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [WKND SPA專案](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [開始在 AEM 中使用 React 建立 SPA](/help/implementing/developing/hybrid/getting-started-react.md)
* [SPA參考資料（API參考）](/help/implementing/developing/hybrid/reference-materials.md)
* [SPA Blueprint和PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [SPA模型製程](/help/implementing/developing/hybrid/routing.md)
* [SPA和伺服器端轉譯](/help/implementing/developing/hybrid/ssr.md)
