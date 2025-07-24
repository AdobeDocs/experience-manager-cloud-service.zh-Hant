---
title: 為 Screens as a Cloud Service 開發自訂元件
description: 下列教學課程將逐步說明為AEM Screens建立自訂元件的步驟。 AEM Screens會重複使用其他AEM產品的許多現有設計模式與技術。 本教學課程著重說明針對AEM Screens進行開發時的差異和特殊考量事項。
exl-id: fe8e7bf2-6828-4a5a-b650-fb3d9c172b97
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: 1179e45f6e75a8a4f5e5e76903243f64d9f406ae
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 2%

---

# 為AEM Screens as a Cloud Service開發自訂元件{#developing-a-custom-component-for-aem-screens}

下列教學課程將逐步說明為AEM Screens建立自訂元件的步驟。 AEM Screens會重複使用其他AEM產品的許多現有設計模式與技術。 本教學課程著重說明針對AEM Screens進行開發時的差異和特殊考量事項。

## 概觀 {#overview}

本教學課程適用於AEM Screens的新手開發人員。 在本教學課程中，我們會為AEM Screens中的順序頻道建置簡單的「Hello World」元件。 對話方塊可讓作者更新顯示的文字。


## 先決條件 {#prerequisites}

若要完成本教學課程，您需要完成下列事項：

1. 最新Screens Feature Pack

1. AEM Screens 播放器

1. 本機開發環境

教學課程步驟和熒幕擷取畫面使用&#x200B;**CRXDE Lite**&#x200B;執行。 您也可以使用IDE來完成本教學課程。 有關使用IDE來開發[與AEM的詳細資訊，請參閱此處](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html)。


## 專案設定 {#project-setup}

Screens專案的原始程式碼通常會作為多模組Maven專案來管理。 為了加快教學課程，已使用[AEM專案原型13](https://github.com/adobe/aem-project-archetype)預先產生專案。 如需使用Maven AEM專案原型建立專案的詳細資訊，請參閱[專案設定](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html)。

1. 使用[CRX Package Manager](http://localhost:4502/crx/packmgr/index.jsp)下載並安裝下列套件：

[取得檔案](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)

   [取得檔案](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)
   **選擇性** （如果使用Eclipse或其他IDE下載下列來源套件）。 使用Maven命令將專案部署到本機AEM執行個體：

   **`mvn -PautoInstallPackage clean install`**

   啟動HelloWorld SRC Screens We.Retail執行專案

[取得檔案](/help/screens-cloud/developing/assets/src-screens-weretail-run.zip)

1. 在[CRX Package Manager](http://localhost:4502/crx/packmgr/index.jsp)中，確認已安裝下列兩個套件：

   1. **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**
   1. **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip**

   ![Screens We.Retail執行透過CRX Package Manager安裝的Ui.Apps和Ui.Content套件](assets/crx-packages.png)

   Screens We.Retail執行透過CRX封裝管理員安裝的Ui.Apps和Ui.Content套件

1. **screens-weretail-run.ui.apps**&#x200B;套件會在`/apps/weretail-run`下方安裝程式碼。

   此套件包含負責呈現專案自訂元件的程式碼。 此套件包含元件程式碼及任何所需的JavaScript或CSS。 此套件也內嵌&#x200B;**screens-weretail-run.core-0.0.1-SNAPSHOT.jar**，其中包含專案所需的任何Java™程式碼。

   >[!NOTE]
   >
   >在本教學課程中，不會撰寫任何Java™程式碼。 如果需要更複雜的商業邏輯，可以使用核心Java™套件組合來建立及部署後端Java™。

   ![在CRXDE Lite中呈現ui.apps程式碼](/help/screens-cloud/developing/assets/uipps-contents.png)

   CRXDE Lite中ui.apps程式碼的表示法

   **`helloworld`**&#x200B;元件只是預留位置。 在教學課程中新增功能，讓作者可更新元件顯示的訊息。

1. **screens-weretail-run.ui.content**&#x200B;套件會在下方安裝程式碼：

   * `/conf/we-retail-run`
   * `/content/dam/we-retail-run`
   * `/content/screens/we-retail-run`

   此套件包含專案所需的起始內容和設定結構。 **`/conf/we-retail-run`**&#x200B;包含We.Retail Run專案的所有設定。 **`/content/dam/we-retail-run`**&#x200B;包括專案的開始數位資產。 **`/content/screens/we-retail-run`**&#x200B;包含Screens內容結構。 這些路徑下的內容主要是在AEM中更新。 為了提高環境（本機、開發、舞台、生產）之間的一致性，通常會將基本內容結構儲存在原始檔控制中。

1. **導覽至AEM Screens > We.Retail Run專案：**

   從AEM全域導覽>按一下Screens圖示。 確認可以看到We.Retail執行專案。

   ![we-retaiul-run-starter](/help/screens-cloud/developing/assets/we-retaiul-run-starter.png)

## 建立Hello World元件 {#hello-world-cmp}

Hello World元件是簡單的元件，可讓使用者輸入要在熒幕顯示的訊息。 元件是以[AEM Screens元件範本為基礎： https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)。

AEM Screens有一些有趣的限制，不適用於傳統WCM Sites元件。

* 大部分的Screens元件都必須在目標數位看板裝置上以全熒幕執行
* 大部分的Screens元件都必須內嵌在順序色版中，才能產生投影片
* 製作時應允許編輯循序頻道中的個別元件，因此不可能以全熒幕呈現這些元件

1. 在&#x200B;**CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp` （或選擇的IDE）中，導覽至`/apps/weretail-run/components/content/helloworld.`

   將下列屬性新增至`helloworld`元件：

   ```
       jcr:title="Hello World"
       sling:resourceSuperType="foundation/components/parbase"
       componentGroup="We.Retail Run - Content"
   ```

   /apps/weretail-run/components/content/helloworld![的](/help/screens-cloud/developing/assets/2018-04-28_at_4_23pm.png)屬性

   /apps/weretail-run/components/content/helloworld的屬性

   **`helloworld`**&#x200B;元件會擴充&#x200B;**foundation/components/parbase**&#x200B;元件，使其可在序列通道內正確使用。

1. 在`/apps/weretail-run/components/content/helloworld`下建立名為`helloworld.html.`的檔案

   將下列專案填入檔案中：

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/helloworld.html
   
   */-->
   
   <!--/* production: preview authoring mode + unspecified mode (that is, on publish) */-->
   <sly data-sly-test.production="${wcmmode.preview || wcmmode.disabled}" data-sly-include="production.html" />
   
   <!--/* edit: any other authoring mode, that is, edit, design, scaffolding, and so on. */-->
   <sly data-sly-test="${!production}" data-sly-include="edit.html" />
   ```

   根據目前使用的[編寫模式](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/authoring/author-environment-tools.html#page-modes)，Screens元件需要兩種不同的轉譯：

   1. **生產**：預覽或發佈模式(wcmmode=disabled)
   1. **編輯**：用於所有其他編寫模式，也就是編輯、設計、支架、開發人員……

   `helloworld.html`充當切換器，檢查哪一個編寫模式作用中，並重新導向到另一個HTL指令碼。 Screens元件使用的常見慣例是，擁有用於編輯模式的`edit.html`指令碼和用於生產模式的`production.html`指令碼。

1. 在`/apps/weretail-run/components/content/helloworld`下建立名為`production.html.`的檔案

   將下列專案填入檔案中：

   ```xml
   <!--/*
    /apps/weretail-run/components/content/helloworld/production.html
   
   */-->
   
   <div data-duration="${properties.duration}" class="cmp-hello-world">
    <h1 class="cmp-hello-world__message">${properties.message}</h1>
   </div>
   ```

   上述生產標籤適用於Hello World元件。 由於元件用於序列頻道，因此包含`data-duration`屬性。 順序頻道使用`data-duration`屬性來瞭解順序專案要顯示多久。

   元件會呈現包含文字的`div`和`h1`標籤。 `${properties.message}`是HTL指令碼的一部分，它輸出名為`message`的JCR屬性內容。 稍後會建立對話方塊，讓使用者可以輸入`message`屬性文字的值。

   另請注意，元件會使用BEM （區塊元素修飾元）記號。 BEM是CSS編碼慣例，可讓您更輕鬆地建立可重複使用的元件。 BEM是[AEM的核心元件](https://github.com/adobe/aem-core-wcm-components/wiki/CSS-coding-conventions)所使用的記號。<!-- WEBSITE WAS NOT ACCESSIBLE AS OF SEPTEMBER 1, 2022 More info can be found at: [https://getbem.com/](https://getbem.com/) -->

1. 在`/apps/weretail-run/components/content/helloworld`下建立名為`edit.html.`的檔案

   將下列專案填入檔案中：

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

   上述編輯標籤適用於Hello World元件。 如果已填入對話方塊訊息，第一個區塊會顯示元件的編輯版本。

   如果沒有輸入對話方塊訊息，則會轉譯第二個區塊。 `cq-placeholder`和`data-emptytext`將標籤&#x200B;***Hello World***&#x200B;呈現為該案例中的預留位置。 可使用i18n將標籤的字串國際化，以支援在多個語言環境中撰寫。

1. **複製Screens影像對話方塊以用於Hello World元件。**

   最簡單的方式是從現有的對話方塊開始，然後進行修改。

   1. 複製對話方塊來源： `/libs/screens/core/components/content/image/cq:dialog`
   1. 在`/apps/weretail-run/components/content/helloworld`下方貼上對話方塊

   ![複製 — 影像 — 對話](/help/screens-cloud/developing/assets/copy-image-dialog.gif)

1. **更新Hello World對話方塊以包含訊息的索引標籤。**

   更新對話方塊，使其符合下列內容。 最後對話方塊的JCR節點結構以XML形式顯示如下：

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
                                   fieldDescription="Amount of time the image is shown in the sequence, in milliseconds"
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

   訊息的`textfield`已儲存至名為`message`的屬性，而Duration的`numberfield`已儲存至名為`duration`的屬性。 這兩個屬性都由HTL在`/apps/weretail-run/components/content/helloworld/production.html`中參照為`${properties.message}`和`${properties.duration}`。

   ![Hello World — 已完成對話方塊](/help/screens-cloud/developing/assets/2018-04-29_at_5_21pm.png)

   Hello World — 已完成對話方塊

## 建立使用者端程式庫 {#clientlibs}

使用者端資料庫提供一種機制，可整理和管理AEM實作所需的CSS和JavaScript檔案。

AEM Screens元件在編輯模式與預覽/生產模式中的轉譯方式不同。 已建立兩個使用者端程式庫：一個用於編輯模式，另一個用於預覽/生產。

1. 為Hello World元件的使用者端資料庫建立資料夾。

   在`/apps/weretail-run/components/content/helloworld`下方，建立名為`clientlibs`的資料夾。

   ![2018-04-30_at_1046am](/help/screens-cloud/developing/assets/2018-04-30_at_1046am.png)

1. 在`clientlibs`資料夾下，建立名稱為`shared`且型別為`cq:ClientLibraryFolder.`的節點

   ![2018-04-30_at_1115am](/help/screens-cloud/developing/assets/2018-04-30_at_1115am.png)

1. 將下列屬性新增至共用使用者端程式庫：

   * `allowProxy` | 布林值 | `true`

   * `categories`| 字串[] | `cq.screens.components`

   /apps/weretail-run/components/content/helloworld/clientlibs/shared![的](/help/screens-cloud/developing/assets/2018-05-03_at_1026pm.png)屬性

   /apps/weretail-run/components/content/helloworld/clientlibs/shared的屬性

   categories屬性是識別使用者端程式庫的字串。 cq.screens.componentscategory會用於編輯和預覽/生產模式。 因此，在sharedclientlib中定義的任何CSS/JS都會以所有模式載入。

   最佳實務是絕對不要在生產環境中直接向/apps公開任何路徑。 allowProxy屬性可確保透過前置詞of/etc.clientlibs來參考使用者端程式庫CSS和JS。

1. 在共用資料夾下建立名為`css.txt`的檔案。

   將下列專案填入檔案中：

   ```
   #base=css
   
   styles.less
   ```

1. 在`css`資料夾下建立名為`shared`的資料夾。 在`style.less`資料夾下新增名為`css`的檔案。 使用者端程式庫的結構現在看起來應該像這樣：

   ![2018-04-30_at_3_11pm](/help/screens-cloud/developing/assets/2018-04-30_at_3_11pm.png)

   本教學課程不直接撰寫CSS，而是使用LESS。 [LESS](https://lesscss.org/)是一種常用的CSS預先編譯器，支援CSS變數、mixin和函式。 AEM使用者端程式庫原生支援LESS編譯。 可以使用Sass或其他預先編譯程式，但必須在AEM之外編譯。

1. 以下列專案填入`/apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less`：

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

1. 複製並貼上`shared`使用者端資料庫資料夾，以建立名為`production`的使用者端資料庫。

   ![複製共用使用者端資料庫以建立生產使用者端資料庫](/help/screens-cloud/developing/assets/copy-clientlib.gif)

   複製共用使用者端程式庫以建立生產使用者端程式庫。

1. 將生產clientlibrary的`categories`屬性更新為`cq.screens.components.production.`

   這麼做可確保只在「預覽/生產」模式中載入樣式。

   ![ /apps/weretail-run/components/content/helloworld/clientlibs/production的屬性](/help/screens-cloud/developing/assets/2018-04-30_at_5_04pm.png)

   /apps/weretail-run/components/content/helloworld/clientlibs/production的屬性

1. 以下列專案填入`/apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less`：

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

   上述樣式會在畫面中央顯示訊息，但僅限於生產模式。

第三個clientlibrary類別： `cq.screens.components.edit`可用來將Edit-only特定樣式新增至元件。

| Clientlib類別 | 使用情況 |
|---|---|
| `cq.screens.components` | 在編輯和生產模式之間共用的樣式和指令碼 |
| `cq.screens.components.edit` | 僅用於編輯模式的樣式和指令碼 |
| `cq.screens.components.production` | 僅用於生產模式的樣式和指令碼 |

## 建立設計頁面 {#design-page}

AEM Screens使用[靜態頁面範本](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-static.html)和[設計設定](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/siteandpage/default-components-designmode.html)進行全域變更。 設計設定常用於設定通道上Parsys的允許元件。 最佳實務是以應用程式專屬的方式儲存這些設定。

We.Retail Run設計頁面會建立於下方，用於儲存We.Retail Run專案的所有特定設定。

1. 在&#x200B;**CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs`中，瀏覽至`/apps/settings/wcm/designs`
1. 在設計資料夾底下建立名為`we-retail-run`且型別為`cq:Page`的節點。
1. 在`we-retail-run`頁面下方，新增另一個名稱為`jcr:content`且型別為`nt:unstructured`的節點。 將下列屬性新增至`jcr:content`節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | jcr:title | 字串 | We.Retail執行 |
   | sling:resourceType | 字串 | wcm/core/components/designer |
   | cq:doctype | 字串 | html_5 |

   ![設計頁面，位於/apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1219pm.png)

   位於/apps/settings/wcm/designs/we-retail-run的設計頁面

## 建立順序頻道 {#create-sequence-channel}

Hello World元件適用於序列頻道。 若要測試元件，則會建立新的「順序頻道」。

1. 在AEM全域導覽中，導覽至&#x200B;**Screens** > **We.Retail Ru** n >並選取&#x200B;**管道**。

1. 按一下&#x200B;**建立**&#x200B;按鈕

   1. 選擇&#x200B;**建立實體**

   ![2018-04-30_at_5_18pm](/help/screens-cloud/developing/assets/2018-04-30_at_5_18pm.png)

1. 在建立精靈中：

1. 範本步驟 — 選擇&#x200B;**順序頻道**

   1. 屬性步驟

   * 基本索引標籤>標題= **閒置頻道**
   * 頻道標籤>檢查&#x200B;**讓頻道上線**

   ![閒置頻道](/help/screens-cloud/developing/assets/idle-channel.gif)

1. 開啟「閒置頻道」的頁面屬性。 更新[設計]欄位，使其指向`/apps/settings/wcm/designs/we-retail-run,`在前一節中建立的設計頁面。

   ![設計設定/apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1240pm.png)

   指向/apps/settings/wcm/designs/we-retail-run的設計設定

1. 編輯已建立的「閒置頻道」，以將其開啟。

1. 將頁面模式切換為&#x200B;**設計**&#x200B;模式。

   1. 按一下Parsys中的&#x200B;**扳手**&#x200B;圖示，即可設定允許的元件。

   1. 選取&#x200B;**Screens**&#x200B;群組和&#x200B;**We.Retail Run - Content**&#x200B;群組。

   ![2018-04-30_at_5_43pm](assets/2018-04-30_at_5_43pm.png)

1. 將頁面模式切換為&#x200B;**編輯**。 現在可將Hello World元件新增至頁面，並與其他序列頻道元件結合。

   ![2018-04-30_at_5_53pm](assets/2018-04-30_at_5_53pm.png)

1. 在&#x200B;**CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs/we-retail-run/jcr%3Acontent/sequencechannel/par`中，導覽至`/apps/settings/wcm/designs/we-retail-run/jcr:content/sequencechannel/par`。 請注意，`components`屬性現在包含`group:Screens`、`group:We.Retail Run - Content`。

   ![在/apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1_14pm.png)下的設計組態

   在/apps/settings/wcm/designs/we-retail-run下的設計設定

## 自訂處理常式的範本 {#custom-handlers}

如果您的自訂元件使用外部資源，例如資產（影像、影片、字型和圖示）、特定資產轉譯或使用者端資料庫（css和js），這些資源不會自動新增到離線設定。 這是因為Adobe預設只會整合HTML標籤。

為了讓您自訂並最佳化下載至播放器的確切資產，Adobe為自訂元件提供擴充機制，向Screens中的離線快取邏輯公開其相依性。

下節將展示自訂離線資源處理常式的範本，以及該特定專案在`pom.xml`中的最低需求。

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

下列程式碼提供該特定專案在`pom.xml`中的最低需求：

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

## 整合所有內容 {#putting-it-all-together}

以下影片說明完成的元件，以及如何將其新增到序列頻道。 該管道隨後會新增至位置顯示，並最終指派給Screens播放器。

>[!VIDEO](https://video.tv.adobe.com/v/22385?quaity=9)

## 完成的程式碼 {#finished-code}

以下是教學課程中完成的程式碼。 **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip**&#x200B;和&#x200B;**screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**&#x200B;是編譯的AEM套件。 **SRC-screens-weretail-run-0.0.1.zip &#x200B;** 是可以使用Maven部署的未編譯原始程式碼。

[取得檔案](/help/screens-cloud/developing/assets/screens-weretail-runuiapps-001-snapshot.zip)

[取得檔案](/help/screens-cloud/developing/assets/screens-weretail-runuicontent-001-snapshot.zip)

[取得檔案](/help/screens-cloud/developing/assets/screens-weretail-run.zip)
