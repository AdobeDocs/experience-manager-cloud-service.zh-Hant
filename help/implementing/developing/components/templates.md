---
title: 頁面範本
description: 建立將用作新頁面基礎的頁面時，會使用頁面範本
translation-type: tm+mt
source-git-commit: 69756d6831678151b0e8eb73db81113d49f17447
workflow-type: tm+mt
source-wordcount: '3228'
ht-degree: 0%

---


# 頁面範本 {#page-templates}

建立頁面時，您需要選取範本。 頁面範本是新頁面的基礎。 範本會定義結果頁面的結構、任何初始內容以及可使用的元件（設計屬性）。 這有幾項優點：

* 頁面範本可讓專業作者 [建立和編輯範本](/help/sites-cloud/authoring/features/templates.md)。
   * 這些專業作者稱為范 **本作者**
   * 範本作者必須是群組的成 `template-authors` 員。
* 頁面範本會保留動態連線至從其建立的任何頁面。 如此可確保範本的任何變更都反映在頁面本身。
* 頁面範本可讓頁面元件更為通用，讓核心頁面元件不需自訂即可使用。

使用「頁面範本」，會在元件中隔離製作頁面的片段。 您可以在UI中設定必要的元件組合，因此不需要針對每個頁面變化開發新的頁面元件。

本檔案：

* 提供建立頁面範本的概觀
* 說明建立可編輯範本所需的管理員／開發人員工作
* 說明可編輯範本的技術基礎
* 說明AEM如何評估範本的可用性

>[!NOTE]
>
>本檔案假設您已熟悉建立和編輯範本。 請參閱編寫文 [件「建立頁面範本](/help/sites-cloud/authoring/features/templates.md)」，其中詳細說明範本作者可公開的可編輯範本功能。

>[!TIP]
>
>[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ，透過實作範例深入探討如何使用頁面範本，對於瞭解如何在新專案中設定範本非常有用

## Creating a New Template {#creating-a-new-template}

「建立頁面範本」主要由範本作 [者使用範本主控台](/help/sites-cloud/authoring/features/templates.md) 和範本編輯器完成。 本節概述此程式，並說明在技術層級發生的情況。

建立新的可編輯範本時：

1. 為模板 [建立資料夾](#template-folders)。 這不是強制性的，而是建議的最佳做法。
1. 選取范 [本類型](#template-type)。 複製此項以建立范 [本定義](#template-definitions)。

   >[!NOTE]
   >
   >提供了一系列現成的模板類型。 您也可以 [視需要建立自己的網站特定範本類型](#creating-template-types) 。

1. 設定新範本的結構、內容原則、初始內容和版面配置。

   **結構**

   * 此結構可讓您定義範本的元件和內容。
   * 在範本結構中定義的元件無法在產生的頁面上移動，也無法從任何產生的頁面刪除。
   * 如果您希望頁面作者能夠新增和移除元件，請將段落系統新增至範本。
   * 元件可以解除鎖定並再次鎖定，以便您定義初始內容。

   如需範本作者如何定義結構的詳細資訊，請參 [閱建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)。

   有關結構的技術詳細資訊，請參 [閱本文](#structure) 中的結構。

   **原則**

   * 內容策略定義元件的設計屬性。

      * 例如，可用元件或最小／最大尺寸。
   * 這些範本（和使用範本建立的頁面）適用。

   如需範本作者如何定義原則的詳細資訊，請參 [閱建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)。

   如需政策的技術詳細資訊，請參 [閱本檔案中的](#content-policies) 「內容政策」。

   **初始內容**

   * 「初始內容」會定義首次根據範本建立頁面時將出現的內容。
   * 然後頁面作者就可以編輯初始內容。

   如需範本作者如何定義結構的詳細資訊，請參 [閱建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author)。

   如需初始內容的技術詳細資訊，請參 [閱本檔案中的](#initial-content) 「初始內容」。

   **配置**

   * 您可以為各種裝置定義範本版面。
   * 範本的互動式版面功能與網頁製作功能相同。

   如需範本作者如何定義範本版面的詳細資訊，請參閱「建立頁 [面範本」](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author)。

   如需範本版面的技術詳細資訊，請參 [閱本檔案中的](#layout) 「版面」。

1. 啟用範本，然後允許範本用於特定內容樹狀結構。

   * 範本可以啟用或停用，讓頁面作者可使用或無法使用。
   * 範本可供某些頁面分支使用或無法使用。

   如需範本作者如何啟用範本的詳細資訊，請參閱建 [立頁面範本](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author)。

   如需啟用範本的技術詳細資訊，請參 [閱本檔案中的啟用和允](#enabling-and-allowing-a-template-for-use)許範本使用

1. 使用它建立內容頁面。

   * 使用範本建立新頁面時，靜態和可編輯範本之間沒有明顯的差異，也沒有任何指示。
   * 對於頁面作者，此程式是透明的。

   如需頁面作者如何使用範本建立頁面的詳細資訊，請參閱「建立 [和組織頁面」](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates)。

   如需有關使用可編輯範本建立頁面的技術詳細資訊，請參 [閱本檔案中的「產生內容頁面](#resultant-content-pages) 」。

>[!NOTE]
>
>編輯器用戶端程式庫會假設內容頁面 `cq.shared` 中存在命名空間，如果它不存在，則會產生JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` 錯誤。
>
>所有範例內容頁面都 `cq.shared`包含，因此任何以它們為基礎的內容都會自動包含 `cq.shared`。 不過，如果您決定從頭開始建立您自己的內容頁面，而不以範例內容為基礎，則必須確定包含命名空間 `cq.shared` 。
>
>如需 [詳細資訊，請參閱使用用戶端程式庫](/help/implementing/developing/introduction/clientlibs.md) 。

>[!CAUTION]
>
>切勿將任何需要國際化的資訊輸入到模板中。

## 範本資料夾 {#template-folders}

若要組織範本，您可以使用下列資料夾：

* `global`
* 特定網站

>[!NOTE]
>
>即使您可以巢狀內嵌資料夾，當使用者在 **Templates** Console中檢視資料夾時，資料夾會顯示為平面結構。

在標準AEM例項中， `global` 範本主控台中已有資料夾。 如果當前資料夾中未找到策略和／或模板類型，則此選項將保留預設模板並充當備援。 您可以將預設範本新增至此檔案夾，或建立新檔案夾（建議使用）。

>[!NOTE]
>
>建立新資料夾以存放您的自訂範本，而不使用資料夾，是最佳的作 `global` 法。

>[!CAUTION]
>
>資料夾必須由具有權限的用戶 `admin` 建立。

模板類型和策略會根據以下優先順序繼承到所有資料夾：

1. 當前資料夾
1. 當前資料夾的父項
1. `/conf/global`
1. `/apps`
1. `/libs`

將建立所有允許條目的清單。 如果任何配置重疊( `path`/ `label`)，則僅向用戶顯示最接近當前資料夾的實例。

若要建立新資料夾，您可以執行下列任一動作：

* 以程式設計或使用CRXDE Lite
* 使用配 [置瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## 使用CRXDE Lite {#using-crxde-lite}

1. 您可以以程式設計方式或使用CRXDE Lite，為您的例項建立新資料夾（在/conf下）。

   必須使用下列結構：

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. 然後，可以在資料夾根節點上定義以下屬性：

   `<your-folder-name> [sling:Folder]`

   * 名稱: `jcr:title`
   * 類型: `String`
   * 值：您要顯示在「範本」控制台中的標題(資料 **夾** )。

1. 除了標準的製作權限和權限外(例如 `content-authors`)，您現在需要指派群組，並定義作者在新資料夾中建立範本所需的存取權限(ACL)。

   群 `template-authors` 組是需要指派的預設群組。 有關詳細資訊， [請參閱ACL和](#acls-and-groups) Groups一節。

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### 使用配置瀏覽器 {#using-the-configuration-browser}

1. 前往全 **域導覽** ->工 **具** >設 [**定瀏覽器**。](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

   現有資料夾列在左側，包括該文 `global` 件夾。

1. 按一下&#x200B;**建立**。
1. 在「創 **建配置** 」對話框中，需要配置以下欄位：

   * **標題**:提供配置資料夾的標題
   * **可編輯的範本**:勾選以允許在此資料夾內編輯範本

1. Click **Create**

>[!NOTE]
>
>在「配 [置瀏覽器」中](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) ，如果您想在此資料夾中建立模板，可以編輯全局資料夾並激活「可編輯模板 **** 」選項，但建議您不要這樣做。

### ACL和組 {#acls-and-groups}

建立模板資料夾後（通過CRXDE或使用配置瀏覽器），必須為模板資料夾的相應組定義ACL，以確保正確的安全性。

WKND教學課程的范 [本資料夾](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ，可做為範例。

#### 範本作者群組 {#the-template-authors-group}

群 `template-authors` 組是用來管理範本存取權的群組，是AEM的標準群組，但是是空的。 必須將用戶添加到項目／站點的組。

>[!CAUTION]
>
>群 `template-authors` 組僅適用於必須能夠建立新範本的使用者。
>
>編輯範本功能十分強大，如果未正確完成，現有範本就會中斷。 因此，此角色應該有重點，並僅包括合格用戶。

下表詳細說明範本編輯的必要權限。

<table>
 <tbody>
  <tr>
   <th>路徑</th>
   <th>角色／群組</th>
   <th>權限<br /> </th>
   <th>說明</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>範本作者<br /> </td>
   <td>讀、寫、複製</td>
   <td>在網站特定空間中建立、讀取、更新、刪除和複製範本的範本作 <code>/conf</code> 者</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者必須在轉譯頁面時讀取範本</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>複製</td>
   <td>replicateContent作者在啟動頁面時，需要啟動頁面的範本</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>讀、寫、複製</td>
   <td>在網站特定空間中建立、讀取、更新、刪除和複製範本的範本作 <code>/conf</code> 者</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者必須在轉譯頁面時讀取原則</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>複製</td>
   <td>內容作者在啟動頁面時，需要啟動頁面範本的原則</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>範本作者</td>
   <td>讀取</td>
   <td>範本作者會根據其中一種預先定義的範本類型，建立新範本。</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>無</td>
   <td>匿名Web用戶不能訪問模板類型</td>
  </tr>
 </tbody>
</table>

此預設 `template-authors` 群組僅涵蓋專案設定，所有成 `template-authors` 員皆可存取及編寫所有範本。 對於更複雜的設定，當需要多個範本作者群組才能區隔範本的存取權時，必須建立更多自訂範本作者群組。 不過，範本作者群組的權限仍會相同。

## Template Type {#template-type}

建立新範本時，您需要指定範本類型：

* 範本類型可有效提供範本的範本。 建立新模板時，將使用所選模板類型的結構和初始內容建立新模板。

   * 模板類型將被複製以建立模板。
   * 複製完成後，範本和範本類型之間的唯一連接，就是供參考之用的靜態參考。

* 範本類型可讓您定義：

   * 頁元件的資源類型。
   * 根節點的策略，它定義了模板編輯器中允許的元件。
   * 建議您在範本類型上定義回應式格點和行動模擬器設定的中斷點。

* AEM提供一些現成可用的範本類型選擇，例如HTML5頁面和最適化表單頁面。

   * 在 [WKND教學課程中提供其他範例。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* 範本類型通常由開發人員定義。

現成可用的範本類型儲存在：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>您不得變更路徑中的任 `/libs` 何項目。 這是因為AEM的更新 `/libs` 可隨時覆寫的內容。

您的網站特定範本類型應儲存在下列可比位置：

* `/apps/settings/wcm/template-types`

您自訂範本類型的定義應儲存在使用者定義的資料夾（建議）中，或儲存在中 `global`。 例如：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>範本類型必須遵循正確的資料夾結構(即 `/settings/wcm/...`)，否則將找不到範本類型。

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating a new editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

>[!CAUTION]
>
>The value of `cq:deviceGroups` must be set as a relative path such as `mobile/groups/responsive` and not as an absolute path such as `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>With static templates /help/sites-developing/page-templates-static.md, the value of `cq:deviceGroups` could be set at the root of the site.
>
>With editable templates, this value is now stored at the template level and is not supported at the page root level.
-->

### 建立範本類型 {#creating-template-types}

如果您已建立可做為其他範本基礎的範本，您可以將此範本複製為範本類型。

1. 建立範本，就像此處所述的任 [何頁面範本](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author)，這將做為範本類型的基礎。
1. 使用CRXDE Lite，將新建立的範本從節點複製 `templates` 到範本資 `template-types` 料夾下的 [節點](#template-folders)。
1. 從範本資料夾下 `templates` 的節點刪 [除範本](#template-folders)。
1. 在節點下的模板副本中，刪 `template-types` 除所有 `cq:template` 和 `cq:templateType` 屬 `jcr:content` 性。

您也可以使用範例可編輯的範本（可在GitHub上使用）來開發您自己的範本類型。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-sites-example-custom-template-type專案](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 範本定義 {#template-definitions}

可編輯範本的定義會儲存 [在使用者定義的資料夾](#template-folders) （建議使用），或儲存在 `global`中。 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

模板的根節點類型為： `cq:Template` 骨架結構：

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

主要元素有：

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

此節點包含模板的屬性：

* **名稱**: `jcr:title`
* **名稱**: `status`
   * ``**Type**: `String`
   * **值**: `draft`、 `enabled` or或 `disabled`

### 結構 {#structure}

定義結果頁的結構：

* 會在建立新頁面時與 `/initial`初始內容()合併。
* 對結構所做的變更將反映在使用範本建立的任何頁面中。
* ( `root` )節 `structure/jcr:content/root`點定義將在結果頁面中提供的元件清單。
   * 在模板結構中定義的元件不能在任何結果頁面上移動或刪除。
   * 一旦元件解除鎖定後， `editable` 屬性就會設為 `true`。
   * 當已包含內容的元件解除鎖定後，此內容就會移至分 `initial` 支。

* 節 `cq:responsive` 點保存響應式佈局的定義。

### 初始內容 {#initial-content}

定義建立新頁面時將包含的初始內容：

* 包含復 `jcr:content` 制到任何新頁面的節點。
* 在建立新頁面時 `/structure`與結構()合併。
* 如果初始內容在建立後變更，則不會更新任何現有的頁面。
* 節 `root` 點包含一個元件清單，用於定義在結果頁中可用的元件。
* 如果以結構模式將內容新增至元件，且該元件隨後已解除鎖定（反之亦然），則此內容會用作初始內容。

### 配置 {#layout}

在編 [輯範本時，您可以定義版面](/help/sites-cloud/authoring/features/templates.md)，這會使用標 [準的互動版面](/help/sites-cloud/authoring/features/responsive-layout.md)。

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Content Policies {#content-policies}

內容策略定義元件的設計屬性。 例如，可用元件或最小／最大尺寸。 這些範本（和使用範本建立的頁面）適用。 可在範本編輯器中建立和選取內容原則。

* 屬性 `cq:policy`，在節 `root` 點
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
提供頁面段落系統內容原則的相對參考。

* 屬性 `cq:policy`位於元件顯式節點下， `root`提供各元件策略的連結。

* 實際策略定義儲存在以下位置：
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>策略定義的路徑取決於元件的路徑。 `cq:policy` 保存配置本身的相對引用。

### 頁面原則 {#page-policies}

頁面原則可讓您在范 [本或結果頁面中](#content-policies) ，定義頁面的內容原則（主參數）。

### 啟用和允許範本使用 {#enabling-and-allowing-a-template-for-use}

1. **啟用範本**

   範本必須先由下列其中一項啟用，才能使用：

   * [從範本主控台](/help/sites-cloud/authoring/features/templates.md) 啟用 **範本** 。

   * 在節點上設定狀態 `jcr:content` 屬性。

      * 例如，在：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定義屬性：

         * 名稱：狀態
         * 類型：字串
         * 值: `enabled`

1. **允許的範本**

   * [在子分支的適當頁面或根頁 **面的**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) 「頁面屬性」上定義允許的範本路徑。
   * 設定屬性：
      `cq:allowedTemplates`
在 
`jcr:content` 的節點。
   例如，值為：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 產生的內容頁面 {#resultant-content-pages}

從可編輯範本建立的頁面：

* 是使用從和模板中合併的子 `structure` 樹 `initial` 建立的

* 對範本和範本類型中保存的資訊有引用。 這是通過具有以下 `jcr:content` 屬性的節點實現的：

   * `cq:template` -提供實際範本的動態參考；可讓範本的變更反映在實際頁面上。

   * `cq:templateType` -提供範本類型的參考。

![範本、內容和元件如何互動](assets/templates-content-components.png)

上圖顯示範本、內容和元件如何相互關聯：

* 控制器- `/content/<my-site>/<my-page>` -參照模板的結果頁。 內容控制整個程式。 根據定義，它訪問適當的模板和元件。
* 配置- `/conf/<my-folder>/settings/wcm/templates/<my-template>` -模 [板和相關內容策略](#template-definitions) ，定義頁面配置。
* Model - OSGi bundles - [OSGI bundles](/help/implementing/deploying/configuring-osgi.md) implement the functionality.
* 檢視- `/apps/<my-site>/components` -在作者和發佈環境中，內容都由元件呈現。

呈現頁面時：

* **範本**:

   * 其節 `cq:template` 點的屬性 `jcr:content` 將被引用，以訪問與該頁對應的模板。

* **元件**:

   * 頁面元件將合併模 `structure/jcr:content` 板的樹和頁 `jcr:content` 面的樹。
      * 頁面元件僅允許作者編輯已標幟為可編輯的範本結構節點（以及任何子系）。
      * 在頁面上呈現元件時，該元件的相對路徑會從節點中取 `jcr:content` 得；然後，將搜索模 `policies/jcr:content` 板節點下的相同路徑。
         * 此節 `cq:policy` 點的屬性指向實際內容策略（即它包含該元件的設計配置）。
            * 這可讓您擁有多個範本，可重複使用相同的內容原則設定。

### 範本可用性 {#template-availability}

在網站管理介面中建立新頁面時，可用範本的清單會視新頁面的位置以及每個範本中指定的位置限制而定。

下列屬性可決定是否允 `T` 許範本用於新頁面，以做為頁面的子頁面 `P`。 這些屬性中的每個屬性都是一個多值字串，其中包含0或多個規則運算式，用於與路徑進行比對：

* 子 `cq:allowedTemplates` 節點或 `jcr:content` 祖先的 `P` 屬性 `P`。

* 屬 `allowedPaths` 性 `T`。

* 屬 `allowedParents` 性 `T`。

* 的 `allowedChildren` 模板屬性 `P`。

評價工作如下：

* 遞增頁面階層時找 `cq:allowedTemplates` 到的第一個非空白屬性(以開頭為 `P` 單位)與路徑相符 `T`。 如果沒有任何值符合，則 `T` 會拒絕。

* 如 `T` 果具有非空 `allowedPaths` 白屬性，但沒有任何值與路徑相符 `P`，則 `T` 拒絕。

* 如果上述兩個屬性皆為空白或不存在，則 `T` 會拒絕，除非屬於與相同的應用程式 `P`。 `T` 僅當路徑的第二 `P` 級名稱與路徑的第二級名稱相同 `T` 時，才屬於相同的應用程式 `P`。 例如，範本屬 `/apps/geometrixx/templates/foo` 於與頁面相同的應用程式 `/content/geometrixx`。

* 如 `T` 果具有非空 `allowedParents` 白屬性，但沒有任何值與路徑相符 `P`，則 `T` 拒絕。

* 如果的模板 `P` 具有非空 `allowedChildren` 屬性，但沒有任何值與路徑匹配 `T`，則 `T` 拒絕。

* 在其他所有情況下， `T` 都允許。

下圖描述了模板評估流程：

![範本評估程式](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM提供多個屬性，以控制「網站」下允許的 **範本**。 但是，結合這些規則可能會產生非常複雜的規則，而且難以追蹤和管理。
>
>因此，Adobe建議您從定義：
>
>* 只有屬 `cq:allowedTemplates` 性
   >
   >
* 僅位於站點根目錄
>
>
例如，請參閱 [WKND教學課程內容](/help/implementing/developing/introduction/develop-wknd-tutorial.md) : `/content/wknd/jcr:content`
>
>屬性 `allowedPaths`、 `allowedParents`和 `allowedChildren` 也可放在範本上，以定義更複雜的規則。 不過，如果有必要 *進一步限制* ，在網站 `cq:allowedTemplates` 的子區段上定義更多屬性會更簡單。
>
>另一個好處是， `cq:allowedTemplates` 「頁面屬性」的「進階」索引標籤中的作者 **可更新** 屬性 ****。 其他範本屬性無法使用（標準）UI進行更新，因此需要開發人員來維護規則和程式碼部署以進行每項變更。

#### 限制子頁面中使用的範本 {#limiting-templates-used-in-child-pages}

若要限制在指定頁面下可用來建立子頁面的範本，請使用頁面 `cq:allowedTemplates` 節 `jcr:content` 點的屬性來指定範本清單，以允許做為子頁面。 例如，清單中的每個值都必須是允許子頁面範本的絕對路徑 `/apps/wknd/templates/page-content`。

您可以使用范 `cq:allowedTemplates` 本節點上的屬性，將 `jcr:content` 此組態套用至使用此範本的所有新建立頁面。

如果要添加更多約束（例如，關於模板層次），可以使用模 `allowedParents/allowedChildren` 板上的屬性。 然後，您可以明確指定從範本T建立的頁面必須是從範本T建立的頁面的父項／子項。
