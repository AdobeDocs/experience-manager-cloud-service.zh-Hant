---
title: SPA 中的複合元件
description: 瞭解如何建立您自己的複合元件，也就是由AEM單頁應用程式(SPA)編輯器運作的其他元件所組成的元件。
exl-id: fa1ab1dd-9e8e-4e2c-aa9a-5b46ed8a02cb
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---


# SPA 中的複合元件 {#composite-components-in-spas}

複合元件可藉由將多個基本元件結合為單一元件，來使用AEM元件的模組化特性。 常見的複合元件使用案例是卡片元件，由影像和文字元件的組合所組成。

當在AEM單頁應用程式(SPA)編輯器架構中正確實作複合元件時，內容作者可以拖放此類元件（就像拖放任何其他元件一樣），但還是可以個別編輯組成複合元件的每個元件。

本文示範如何將複合元件新增至單頁應用程式，以便順暢地與AEM SPA Editor搭配運作。

{{ue-over-spa}}

## 使用案例 {#use-case}

本文將以典型卡片元件作為範例使用案例。 卡片是許多數位體驗的通用UI元素，通常由影像和相關文字或標題組成。 作者想要能夠拖放整個卡片，但可以個別編輯卡片的影像和自訂關聯文字。

## 先決條件 {#prerequisites}

下列支援複合元件使用案例的模型需要下列先決條件。

* 您的AEM開發執行個體正在連線埠4502上本機執行，並有一個範例專案。
* 您已啟用有效的外部React應用程式[，以便在AEM](editing-external-spa.md)中編輯。
* React應用程式已使用RemotePage元件](remote-page.md)載入AEM編輯器[中。

## 將複合元件新增至SPA {#adding-composite-components}

實作複合元件有三種不同的模型，取決於AEM中的SPA實作。

* [您的AEM專案中不存在該元件](#component-does-not-exist)。
* [元件存在於您的AEM專案中，但它的必要內容不是](#content-does-not-exist)。
* [元件及其必要內容都存在於您的AEM專案中](#both-exist)。

以下各節會以卡片元件為例，提供實施每個案例的範例。

### 您的AEM專案中不存在該元件。 {#component-does-not-exist}

首先，建立構成複合元件的元件，也就是影像及其文字的元件。

1. 在您的AEM專案中建立文字元件。
1. 從元件的`editConfig`節點中的專案新增對應的`resourceType`。

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. 使用`withMappable`協助程式來啟用元件的編輯。

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

文字元件類似於以下內容。

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

如果您以類似方式建立影像元件，可以將其與`AEMText`元件結合為新的卡片元件，並使用影像和文字元件作為子系。

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

如此產生的複合元件現在可置於應用程式中的任何位置，且將在SPA編輯器中為文字和影像元件新增預留位置。 在以下範例中，卡片元件會新增到標題下方的首頁元件。

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

這會在編輯器中顯示文字和影像的空白預留位置。 使用編輯器輸入這些專案的值時，它們會儲存在指定的頁面路徑中，亦即`/content/wknd-spa/home`，位於根層級，且名稱在`itemPath`中指定。

編輯器中的![複合卡元件](assets/composite-card.png)

### 元件存在於您的AEM專案中，但它的必要內容不存在。 {#content-does-not-exist}

在此案例中，卡片元件已在包含標題和影像節點的AEM專案中建立。 子節點（文字和影像）具有對應的資源型別。

卡片元件的![節點結構](assets/composite-node-structure.png)

接著，您可以將它新增至SPA並擷取其內容。

1. 在SPA中為此建立對應的元件。 確保子元件對應至SPA專案中其對應的AEM資源型別。 在此範例中，我們使用與先前案例](#component-does-not-exist)中詳細[相同的`AEMText`和`AEMImage`元件。

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. 由於`imagecard`元件沒有內容，請將卡片新增至頁面。 在SPA中加入AEM的現有容器。
   * 如果AEM專案中已有容器，我們可以改為將此容器加入SPA，並改為從AEM將元件新增至容器。
   * 確認卡片元件已對應至SPA中對應的資源型別。

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. 將已建立的`wknd-spa/components/imagecard`元件新增至頁面範本](/help/sites-cloud/authoring/page-editor/templates.md)中容器元件[的允許元件。

現在可以直接將`imagecard`元件新增到AEM編輯器中的容器。

編輯器中的![複合卡片](assets/composite-card.gif)

### 元件及其必要內容都存在於您的AEM專案中。 {#both-exist}

如果內容存在於AEM中，可提供內容的路徑直接包含在SPA中。

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![節點結構中的複合路徑](assets/composite-path.png)

`AEMCard`元件與先前使用案例](#content-does-not-exist)中定義的[相同。 此處，上述位置在AEM專案中定義的內容包含在SPA中。
