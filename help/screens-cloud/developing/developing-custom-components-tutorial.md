---
title: 為螢幕開發自定義元件as a Cloud Service
description: 以下教程將介紹為AEM Screens建立自定義元件的步驟。 AEM Screens重新使用了許多現有的設計模式和其AEM它產品。 本教程著重介紹在為AEM Screens開發時的不同之處和特別考慮事項。
exl-id: fe8e7bf2-6828-4a5a-b650-fb3d9c172b97
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 2%

---

# 為AEM Screensas a Cloud Service開發定制元件{#developing-a-custom-component-for-aem-screens}

以下教程將介紹為AEM Screens建立自定義元件的步驟。 AEM Screens重新使用了許多現有的設計模式和其AEM它產品。 本教程著重介紹在為AEM Screens開發時的不同之處和特別考慮事項。

## 概覽 {#overview}

本教程適用於對AEM Screens不熟悉的開發人員。 在本教程中，為AEM Screens的Sequence頻道構建了簡單的「Hello World」元件。 對話框允許作者更新顯示的文本。


## 必備條件 {#prerequisites}

要完成本教程，需要執行以下操作：

1. 最新螢幕功能包

1. AEM Screens 播放器

1. 本機開發環境

使用 **CRXDE-Lite**。 IDE也可用於完成本教程。 有關使用IDE開發的詳細資訊 [的上AEM界。](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html#eclipse-ide)


## 項目設定 {#project-setup}

螢幕項目的原始碼通常作為多模組Maven項目進行管理。 為加快教程的完成，預生成的項目 [原型AEM13工程](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。 有關 [在此處可找到使用Maven項AEM目原型建立項目](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html#maven-multimodule)。

1. 使用 [CRX包管理器](http://localhost:4502/crx/packmgr/index.jsp):

[取得檔案](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)

   [取得檔案](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)
   **（可選）** 如果使用Eclipse或其他IDE，請下載以下源包。 使用Maven命令將項AEM目部署到本地實例：

   **`mvn -PautoInstallPackage clean install`**

   啟動HelloWorld SRC螢幕We.Retail運行項目

[取得檔案](/help/screens-cloud/developing/assets/src-screens-weretail-run.zip)

1. 在 [CRX包管理器](http://localhost:4502/crx/packmgr/index.jsp) 驗證是否安裝了以下兩個軟體包：

   1. **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**
   1. **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip**

   ![通過CRX包管理器安裝的We.Retail運行Ui.Apps和Ui.Content包的螢幕](assets/crx-packages.png)

   通過CRX包管理器安裝的We.Retail運行Ui.Apps和Ui.Content包的螢幕

1. 的 **screens-weretail-run.ui.apps** 軟體包安裝代碼 `/apps/weretail-run`。

   此包包含負責為項目呈現自定義元件的代碼。 此軟體包包括元件代碼和所需的任何JavaScript或CSS。 此包還嵌入 **screens-weretail-run.core-0.0.1-SNAPSHOT.jar** 包含項目所需的任何Java代碼。

   >[!NOTE]
   >
   >在本教程中，未編寫Java代碼。 如果需要更複雜的業務邏輯，可以使用核心Java捆綁包建立和部署後端Java。

   ![ui.apps代碼在CRXDE Lite中的表示](/help/screens-cloud/developing/assets/uipps-contents.png)

   ui.apps代碼在CRXDE Lite中的表示

   的 **螺旋世界** 元件當前只是一個佔位符。 在本教程中，將添加功能，使作者能夠更新元件顯示的消息。

1. 的 **screens-weretail-run.ui.co內容** 軟體包在下面安裝代碼：

   * `/conf/we-retail-run`
   * `/content/dam/we-retail-run`
   * `/content/screens/we-retail-run`

   此包包含項目所需的啟動內容和配置結構。 **`/conf/we-retail-run`** 包含We.Retail Run項目的所有配置。 **`/content/dam/we-retail-run`** 包括啟動項目的數字資產。 **`/content/screens/we-retail-run`** 包含螢幕內容結構。 所有這些路徑下的內容主要在中更新AEM。 為了提高環境（本地、開發、階段、產品）之間的一致性，通常在原始碼管理中保存基本內容結構。

1. **定位至「AEM Screens」>「We.Retail Run」項目：**

   從「開始」AEM菜單>按一下「螢幕」表徵圖。 驗證是否可以看到We.Retail Run項目。

   ![我們自主創業](/help/screens-cloud/developing/assets/we-retaiul-run-starter.png)

## 建立Hello World元件 {#hello-world-cmp}

Hello World元件是一個簡單元件，允許用戶輸入要在螢幕上顯示的消息。 元件基於 [AEM Screens元件模板：https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)。

AEM Screens有一些有趣的限制條件，這對於傳統的WCM站點元件不一定適用。

* 大多數螢幕元件需要在目標數字標牌設備上全屏運行
* 大多數螢幕元件需要嵌入序列通道中以生成幻燈片
* 創作應允許在序列通道中編輯單個元件，因此不需要將其全屏呈現

1. 在 **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp` （或選擇的IDE）導航到 `/apps/weretail-run/components/content/helloworld.`

   將以下屬性添加到 `helloworld` 元件：

   ```
       jcr:title="Hello World"
       sling:resourceSuperType="foundation/components/parbase"
       componentGroup="We.Retail Run - Content"
   ```

   ![/apps/weretail-run/components/content/helloworld的屬性](/help/screens-cloud/developing/assets/2018-04-28_at_4_23pm.png)

   /apps/weretail-run/components/content/helloworld的屬性

   的 **螺旋世界** 元件擴展 **基礎/元件/基礎** 這樣，它就可以在序列通道內正確使用。

1. 在下面建立檔案 `/apps/weretail-run/components/content/helloworld` 命名 `helloworld.html.`

   使用以下內容填充檔案：

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/helloworld.html
   
   */-->
   
   <!--/* production: preview authoring mode + unspecified mode (i.e. on publish) */-->
   <sly data-sly-test.production="${wcmmode.preview || wcmmode.disabled}" data-sly-include="production.html" />
   
   <!--/* edit: any other authoring mode, i.e. edit, design, scaffolding, etc. */-->
   <sly data-sly-test="${!production}" data-sly-include="edit.html" />
   ```

   螢幕元件需要兩種不同的渲染，具體取決於 [創作模式](https://helpx.adobe.com/experience-manager/6-4/sites/authoring/using/author-environment-tools.html#PageModes) 正在使用：

   1. **生產**:預覽或發佈模式（wcmmode=禁用）
   1. **編輯**:用於所有其他創作模式，如編輯、設計、腳手架、開發人員……

   `helloworld.html`充當交換機，檢查哪個創作模式當前處於活動狀態並重定向到另一個HTL指令碼。 螢幕元件使用的常見慣例是 `edit.html` 用於編輯模式的指令碼和 `production.html` 生產模式的指令碼。

1. 在下面建立檔案 `/apps/weretail-run/components/content/helloworld` 命名 `production.html.`

   使用以下內容填充檔案：

   ```xml
   <!--/*
    /apps/weretail-run/components/content/helloworld/production.html
   
   */-->
   
   <div data-duration="${properties.duration}" class="cmp-hello-world">
    <h1 class="cmp-hello-world__message">${properties.message}</h1>
   </div>
   ```

   以上是Hello World元件的生產標籤。 A `data-duration` 由於元件在序列通道上使用，因此包含屬性。 的 `data-duration` 序列通道使用屬性來瞭解序列項的顯示時間。

   元件呈現 `div` 和 `h1` 帶文本的標籤。 `${properties.message}` 是HTL指令碼的一部分，該指令碼將輸出名為JCR屬性的內容 `message`。 稍後將建立一個對話框，允許用戶為 `message` 屬性文本。

   另請注意，BEM（塊元素修飾符）表示法與元件一起使用。 BEM是一種CSS編碼約定，它使建立可重用元件變得更容易。 BEM是由 [核AEM心元件](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/wiki/CSS-coding-conventions)。 更多資訊可在以下網址找到： [https://getbem.com/](https://getbem.com/)

1. 在下面建立檔案 `/apps/weretail-run/components/content/helloworld` 命名 `edit.html.`

   使用以下內容填充檔案：

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/edit.html
   
   */-->
   
   <!--/* if message populated */-->
   <div
    data-sly-test.message="${properties.message}"
    class="aem-Screens-editWrapper cmp-hello-world">
    <p class="cmp-hello-world__message">${message}</p>
   </div>
   
   <!--/* empty place holder */-->
   <div data-sly-test="${!message}"
        class="aem-Screens-editWrapper cq-placeholder cmp-hello-world"
        data-emptytext="${'Hello World' @ i18n, locale=request.locale}">
   </div>
   ```

   上面是Hello World元件的編輯標籤。 如果已填充對話框消息，則第一個塊將顯示元件的編輯版本。

   如果未輸入對話消息，則呈現第二塊。 的 `cq-placeholder` 和 `data-emptytext` 呈現標籤 ***《你好世界》*** 在那個案子裡當持倉者。 標籤的字串可以使用i18n進行國際化，以支援在多個區域設定中進行創作。

1. **用於Hello World元件的「複製螢幕影像」對話框。**

   從現有對話框開始，然後進行修改是最容易的。

   1. 從以下位置複製對話框： `/libs/screens/core/components/content/image/cq:dialog`
   1. 將對話框貼上到下面 `/apps/weretail-run/components/content/helloworld`

   ![複製 — 映像 — 對話框](/help/screens-cloud/developing/assets/copy-image-dialog.gif)

1. **更新「Hello World」對話框以包含消息的頁籤。**

   更新對話框，使其與以下內容匹配。 下面以XML形式顯示了最終對話框的JCR節點結構：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
       jcr:primaryType="nt:unstructured"
       jcr:title="Hello World"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content
           jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/coral/foundation/tabs"
           size="L">
           <items jcr:primaryType="nt:unstructured">
               <message
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Message"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <message
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                   fieldDescription="Message for component to display"
                                   fieldLabel="Message"
                                   name="./message"/>
                           </items>
                       </column>
                   </items>
               </message>
               <sequence
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Sequence"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <duration
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield"
                                   defaultValue=""
                                   fieldDescription="Amount of time the image will be shown in the sequence, in milliseconds"
                                   fieldLabel="Duration (ms)"
                                   min="0"
                                   name="./duration"/>
                           </items>
                       </column>
                   </items>
               </sequence>
           </items>
       </content>
   </jcr:root>
   ```

   消息的文本欄位將保存到名為 `message` 並將持續時間的number欄位保存到名為 `duration`。 這兩個屬性都在中引用 `/apps/weretail-run/components/content/helloworld/production.html` 按HTL As `${properties.message}` 和 `${properties.duration}`。

   ![Hello World — 已完成對話](/help/screens-cloud/developing/assets/2018-04-29_at_5_21pm.png)

   Hello World — 已完成對話

## 建立客戶端庫 {#clientlibs}

客戶端庫提供一種機制，用於組織和管理實現所需的CSS和JavaScriptAEM檔案。

AEM Screens元件在「編輯」模式與「預覽/生產」模式下的呈現方式不同。 將建立兩個客戶端庫，一個用於編輯模式，另一個用於預覽/生產。

1. 為Hello World元件的客戶端庫建立資料夾。

   在下面 `/apps/weretail-run/components/content/helloworld`建立名為 `clientlibs`。

   ![2018-04-30_at_1046am](/help/screens-cloud/developing/assets/2018-04-30_at_1046am.png)

1. 在 `clientlibs` 資料夾建立名為 `shared` 類型 `cq:ClientLibraryFolder.`

   ![2018-04-30_at_1115am](/help/screens-cloud/developing/assets/2018-04-30_at_1115am.png)

1. 將以下屬性添加到共用客戶端庫：

   * `allowProxy` | 布林函數 | `true`

   * `categories`|字串[] | `cq.screens.components`

   ![/apps/weretail-run/components/content/helloworld/clientlibs/shared的屬性](/help/screens-cloud/developing/assets/2018-05-03_at_1026pm.png)

   /apps/weretail-run/components/content/helloworld/clientlibs/shared的屬性

   categories屬性是標識客戶端庫的字串。 cq.screens.componentscategory在「編輯」和「預覽/生產」模式下均使用。 因此，在sharedclientlib中定義的任何CSS/JS都會以所有模式載入。

   絕不直接向生產環境中的/app顯示任何路徑是最佳做法。 allowProxy屬性確保通過前置詞of/etc.clientlibs引用客戶端庫CSS和JS。

1. 建立名為 `css.txt` 下。

   使用以下內容填充檔案：

   ```
   #base=css
   
   styles.less
   ```

1. 建立名為 `css` 在下面 `shared` 的子菜單。 添加名為 `style.less` 在下面 `css` 的子菜單。 客戶端庫的結構現在應如下所示：

   ![2018-04-30_at_3_11pm](/help/screens-cloud/developing/assets/2018-04-30_at_3_11pm.png)

   本教程不直接編寫CSS，而是使用LESS。 [減](https://lesscss.org/) 是支援CSS變數、混合和函式的常用CSS預編譯器。 客AEM戶端庫本機支援LESS編譯。 可以使用Sass或其他預編譯器，但需要在外部編譯AEM。

1. 填充 `/apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less` 下面列出：

   ```css
   /**
       Shared Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less
   
   **/
   
   .cmp-hello-world {
       background-color: #fff;
   
    &__message {
     color: #000;
     font-family: Helvetica;
     text-align:center;
    }
   }
   ```

1. 複製並貼上 `shared` 客戶端庫資料夾，用於建立名為 `production`。

   ![複製共用客戶端庫以建立新的生產客戶端庫](/help/screens-cloud/developing/assets/copy-clientlib.gif)

   複製共用客戶端庫以建立新的生產客戶端庫

1. 更新 `categories` 要生產的客戶端庫的屬性 `cq.screens.components.production.`

   這確保只有在「預覽/生產」模式下才載入樣式。

   ![/apps/weretail-run/components/content/helloworld/clientlibs/production的屬性](/help/screens-cloud/developing/assets/2018-04-30_at_5_04pm.png)

   /apps/weretail-run/components/content/helloworld/clientlibs/production的屬性

1. 填充 `/apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less` 下面列出：

   ```css
   /**
       Production Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less
   
   **/
   .cmp-hello-world {
   
       height: 100%;
       width: 100%;
       position: fixed;
   
    &__message {
   
     position: relative;
     font-size: 5rem;
     top:25%;
    }
   }
   ```

   上述樣式將在螢幕中心顯示消息，但僅在生產模式下顯示。

第三個客戶端庫類別： `cq.screens.components.edit` 可用於向元件添加僅編輯特定樣式。

| 客戶端庫類別 | 使用狀況 |
|---|---|
| `cq.screens.components` | 在編輯和生產模式之間共用的樣式和指令碼 |
| `cq.screens.components.edit` | 僅在編輯模式中使用的樣式和指令碼 |
| `cq.screens.components.production` | 僅在生產模式中使用的樣式和指令碼 |

## 建立設計頁 {#design-page}

AEM Screens用途 [靜態頁模板](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/page-templates-static.html) 和 [設計配置](https://helpx.adobe.com/experience-manager/6-4/sites/authoring/using/default-components-designmode.html) 的子菜單。 設計配置經常用於為通道上的Parsys配置允許的元件。 最佳做法是以特定於應用的方式儲存這些配置。

在「We.Retail運行設計」頁面下，將儲存特定於We.Retail Run項目的所有配置。

1. 在 **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs` 導航 `/apps/settings/wcm/designs`
1. 在設計資料夾下建立新節點，名為 `we-retail-run` 具有 `cq:Page`。
1. 在 `we-retail-run` 頁，添加另一個名為 `jcr:content` 類型 `nt:unstructured`。 將以下屬性添加到 `jcr:content` 節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | jcr:title | 字串 | We.Retail Run |
   | sling:resourceType | 字串 | wcm/核心/元件/設計器 |
   | cq:doctype | 字串 | html_5 |

   ![設計頁面，位於/apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1219pm.png)

   設計頁面，位於/apps/settings/wcm/designs/we-retail-run

## 建立序列通道 {#create-sequence-channel}

Hello World元件用於序列通道。 要test元件，將建立新的「序列通道」。

1. 從「開始」AEM菜單導航到 **螢幕** > **We.Retail Ru** n >選擇 **頻道**。

1. 按一下 **建立** 按鈕

   1. 選擇 **建立實體**

   ![2018-04-30_at_5_18pm](/help/screens-cloud/developing/assets/2018-04-30_at_5_18pm.png)

1. 在「建立」嚮導中：

1. 模板步驟 — 選擇 **序列通道**

   1. 屬性步驟
   * 「基本」頁籤>標題= **空閒通道**
   * 「通道」頁籤>檢查 **使頻道聯機**

   ![空閒通道](/help/screens-cloud/developing/assets/idle-channel.gif)

1. 開啟空閒通道的頁面屬性。 更新「設計」欄位以指向 `/apps/settings/wcm/designs/we-retail-run,`在上一節中建立的設計頁面。

   ![設計配置/apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1240pm.png)

   指向/apps/settings/wcm/designs/we-retail-run的設計配置

1. 編輯新建立的空閒通道以將其開啟。

1. 將頁面模式切換到 **設計** 模式

   1. 按一下 **扳** 「參數」(Parsys)中的表徵圖，用於配置允許的元件

   1. 選擇 **螢幕** 本集團及 **We.Retail Run — 內容** 組。

   ![2018-04-30_at_5_43pm](assets/2018-04-30_at_5_43pm.png)

1. 將頁面模式切換到 **編輯**。 現在，Hello World元件可以添加到頁面，並與其他序列通道元件組合。

   ![2018-04-30_at_5_53pm](assets/2018-04-30_at_5_53pm.png)

1. 在 **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs/we-retail-run/jcr%3Acontent/sequencechannel/par` 導航 `/apps/settings/wcm/designs/we-retail-run/jcr:content/sequencechannel/par`。 注意 `components` 現在包括 `group:Screens`。 `group:We.Retail Run - Content`。

   ![在/apps/settings/wcm/designs/we-retail-run下進行設計配置](/help/screens-cloud/developing/assets/2018-05-07_at_1_14pm.png)

   在/apps/settings/wcm/designs/we-retail-run下進行設計配置

## 自定義處理程式模板 {#custom-handlers}

如果您的自定義元件使用外部資源(如資產（影像、視頻、字型、表徵圖等）、特定資產格式副本或客戶端庫（css、js等），則這些資源不會自動添加到離線配置中，因為預設情況下，我們只捆綁HTML標籤。

為了讓您自定義和優化下載到播放器的確切資產，我們為自定義元件提供了擴展機制，以在螢幕中顯示它們對離線快取邏輯的依賴性。

以下部分顯示了自定義離線資源處理程式的模板以及 `pom.xml` 為那個具體項目。

```java
package …;

import javax.annotation.Nonnull;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceUtil;
import org.apache.sling.api.resource.ValueMap;

import com.adobe.cq.screens.visitor.OfflineResourceHandler;

@Service(value = OfflineResourceHandler.class)
@Component(immediate = true)
public class MyCustomHandler extends AbstractResourceHandler {

 @Reference
 private …; // OSGi services injection

 /**
  * The resource types that are handled by the handler.
  * @return the handled resource types
  */
 @Nonnull
 @Override
 public String[] getSupportedResourceTypes() {
     return new String[] { … };
 }

 /**
  * Accept the provided resource, visit and traverse it as needed.
  * @param resource The resource to accept
  */
 @Override
 public void accept(@Nonnull Resource resource) {
     ValueMap properties = ResourceUtil.getValueMap(resource);
     
     /* You can directly add explicit paths for offline caching using the `visit`
        method of the visitor. */
     
     // retrieve a custom property from the component
     String myCustomRenditionUrl = properties.get("myCustomRenditionUrl", String.class);
     // adding that exact asset/rendition/path to the offline manifest
     this.visitor.visit(myCustomRenditionUrl);
     
     
     /* You can delegate handling for dependent resources so they are also added to
        the offline cache using the `accept` method of the visitor. */
     
     // retrieve a referenced dependent resource
     String referencedResourcePath = properties.get("myOtherResource", String.class);
     ResourceResolver resolver = resource.getResourceResolver();
     Resource referencedResource = resolver.getResource(referencedResourcePath);
     // let the handler for that resource handle it
     if (referencedResource != null) {
         this.visitor.accept(referencedResource);
     }
   }
}
```

以下代碼提供 `pom.xml` 針對該特定項目：

```css
   <dependencies>
        …
        <!-- Felix annotations -->
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.9.0</version>
            <scope>provided</scope>
        </dependency>

        <!-- Screens core bundle with OfflineResourceHandler/AbstractResourceHandler -->
        <dependency>
            <groupId>com.adobe.cq.screens</groupId>
            <artifactId>com.adobe.cq.screens</artifactId>
            <version>1.5.90</version>
            <scope>provided</scope>
        </dependency>
        …
      </dependencies>
```

## 把它們放在一起 {#putting-it-all-together}

以下視頻顯示了已完成的元件以及如何將其添加到序列通道。 然後，該頻道被添加到位置顯示器，並最終被分配給螢幕播放器。

>[!VIDEO](https://video.tv.adobe.com/v/22385?quaity=9)

## 已完成代碼 {#finished-code}

下面是本教程的完成代碼。 的 **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip** 和 **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip** 是已編譯的AEM包。 **SRC-screens-weretail-run-0.0.1.zip **是可使用Maven部署的未編譯原始碼。

[取得檔案](/help/screens-cloud/developing/assets/screens-weretail-runuiapps-001-snapshot.zip)

[取得檔案](/help/screens-cloud/developing/assets/screens-weretail-runuicontent-001-snapshot.zip)

[取得檔案](/help/screens-cloud/developing/assets/screens-weretail-run.zip)
