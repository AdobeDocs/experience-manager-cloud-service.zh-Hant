---
title: 頁面範本
description: 建立將用作新頁面基礎的頁面時，會使用「頁面範本」
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: f5aa9229ff06fdcff5474594269ebcf9daf09e41
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 1%

---

# 頁面範本 {#page-templates}

建立頁面時，您需要選取範本。 頁面範本是新頁面的基礎。 範本會定義產生的頁面、任何初始內容及可使用的元件（設計屬性）。 這有幾項優點：

* 頁面範本可讓專業作者 [建立和編輯範本](/help/sites-cloud/authoring/features/templates.md).
   * 這種專業作者被稱為 **範本作者**
   * 範本作者必須是 `template-authors` 群組。
* 「頁面範本」會保留動態連線至從這些範本建立的任何頁面。 這可確保對範本所做的任何變更都反映在頁面本身中。
* 頁面範本可讓頁面元件更為通用，讓核心頁面元件可供使用，而不需自訂。

使用「頁面範本」時，製作頁面的片段會獨立於元件中。 您可以在UI中設定必要的元件組合，因此不需要針對每個頁面變異開發新的頁面元件。

本文件:

* 提供建立頁面範本的概觀
* 說明建立可編輯的範本所需的管理員/開發人員工作
* 說明可編輯範本的技術基礎
* 說明AEM如何評估範本的可用性

>[!NOTE]
>
>本檔案假設您已熟悉建立和編輯範本。 請參閱編寫檔案 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md)，詳細說明可編輯範本的功能，這些範本作者可公開。

>[!TIP]
>
>[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 透過實作範例深入探討如何使用頁面範本，這對了解如何在新專案中設定範本非常有用

## 建立新範本 {#creating-a-new-template}

建立頁面範本主要是使用 [範本主控台和範本編輯器](/help/sites-cloud/authoring/features/templates.md) 由範本作者撰寫。 本節提供此程式的概觀，並隨後說明在技術層級發生的情況。

建立新的可編輯範本時，您可以：

1. 建立 [模板的資料夾](#template-folders). 這不是強制性的，而是建議的最佳實務。
1. 選取 [範本類型](#template-type). 這會複製到建立 [範本定義](#template-definitions).

   >[!NOTE]
   >
   >提供一系列範本類型的現成可用功能。 您也可以 [建立您自己的網站特定範本類型](#creating-template-types) （如果需要）。

1. 配置新模板的結構、內容策略、初始內容和佈局。

   **結構**

   * 結構可讓您定義範本的元件和內容。
   * 在範本結構中定義的元件無法在產生的頁面上移動，也無法從任何產生的頁面中刪除。
   * 如果您希望頁面作者能夠新增和移除元件，請在範本中新增段落系統。
   * 元件可以再次解除鎖定和鎖定，以便定義初始內容。

   如需範本作者如何定義結構的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   如需結構的技術詳細資訊，請參閱 [結構](#structure) 在此文檔中。

   **原則**

   * 內容策略定義元件的設計屬性。

      * 例如，可用元件或最小/最大尺寸。
   * 這些規則適用於範本（以及使用範本建立的頁面）。

   如需範本作者如何定義原則的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   如需原則的技術詳細資訊，請參閱 [內容原則](#content-policies) 在此文檔中。

   **初始內容**

   * 「初始內容」會定義根據範本首次建立頁面時所將顯示的內容。
   * 然後頁面作者就可以編輯初始內容。

   如需範本作者如何定義結構的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author).

   如需初始內容的技術詳細資訊，請參閱 [初始內容](#initial-content) 在此文檔中。

   **配置**

   * 您可以定義裝置範圍的範本配置。
   * 範本的回應式版面運作方式與頁面編寫相同。

   如需範本作者如何定義範本配置的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   如需範本配置的技術詳細資訊，請參閱 [版面](#layout) 在此文檔中。

1. 啟用範本，然後允許它建立特定內容樹。

   * 範本可以啟用或停用，讓頁面作者可使用或無法使用。
   * 範本可供某些頁面分支使用或無法使用。

   如需範本作者如何啟用範本的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   如需啟用範本的技術詳細資訊，請參閱 [為我們啟用和允許範本](#enabling-and-allowing-a-template-for-use)本檔案中的e

1. 使用它建立內容頁面。

   * 使用範本建立新頁面時，靜態和可編輯的範本之間沒有顯示差異，也沒有顯示任何指示。
   * 對於頁面作者而言，程式是透明的。

   如需頁面作者如何使用範本建立頁面的詳細資訊，請參閱 [建立及組織頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   有關使用可編輯的模板建立頁面的技術詳細資訊，請參閱 [產生的內容頁面](#resultant-content-pages) 在此文檔中。

>[!TIP]
>
>切勿輸入需要國際化到模板中的任何資訊。 為內部化目的， [核心元件的本地化功能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) 。

>[!NOTE]
>
>範本是功能強大的工具，可簡化頁面建立工作流程。 不過，太多範本可能會讓作者不堪重負，使頁面建立變得困惑。 經驗法則是將範本數量控制在100以下。
>
>Adobe不建議有超過1000個範本，因為可能會影響效能。

>[!NOTE]
>
>編輯器用戶端程式庫會假設 `cq.shared` 命名空間（若不存在JavaScript錯誤） `Uncaught TypeError: Cannot read property 'shared' of undefined` 會產生。
>
>所有範例內容頁面都包含 `cq.shared`，因此任何以其為基礎的內容都會自動包含 `cq.shared`. 不過，如果您決定從草稿開始建立自己的內容頁面，而不以範例內容為基礎，則必須確定包含 `cq.shared` 命名空間。
>
>請參閱 [使用用戶端程式庫](/help/implementing/developing/introduction/clientlibs.md) 以取得更多資訊。



## 範本資料夾 {#template-folders}

若要組織範本，您可以使用下列資料夾：

* `global`
* 網站特定

>[!NOTE]
>
>即使您可以巢狀內嵌資料夾，但當使用者在 **範本** 控制台顯示為平面結構。

在標準AEM例項中， `global` 模板控制台中已存在資料夾。 如果在當前資料夾中找不到策略和/或模板類型，則此選項將保留預設模板，並充當後援。 您可以將預設範本新增到此資料夾或建立新資料夾（建議）。

>[!NOTE]
>
>最佳實務是建立新資料夾以存放自訂的範本，而不要使用 `global` 檔案夾。

>[!CAUTION]
>
>資料夾必須由使用 `admin` 權限。

模板類型和策略根據以下優先順序繼承到所有資料夾：

1. 當前資料夾
1. 當前資料夾的父資料夾
1. `/conf/global`
1. `/apps`
1. `/libs`

將建立所有允許的條目的清單。 如果有任何設定重疊( `path`/ `label`)，則只會向使用者顯示最接近目前資料夾的例項。

若要建立新資料夾，您可以執行下列任一操作：

* 以程式設計方式或使用CRXDE Lite
* 使用 [配置瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## 使用 CRXDE Lite {#using-crxde-lite}

1. 可以以程式設計方式或使用CRXDE Lite為執行個體建立新資料夾（在/conf下）。

   必須使用下列結構：

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. 然後，您可以在資料夾根節點上定義下列屬性：

   `<your-folder-name> [sling:Folder]`

   * 名稱: `jcr:title`
   * 類型: `String`
   * 值：您要顯示在 **範本** 控制台。

1. 除了標準製作權限(例如 `content-authors`)您現在需要指派群組並定義必要的存取權限(ACL)，供作者在新資料夾中建立範本。

   此 `template-authors` 群組是需要指派的預設群組。 請參閱 [ACL和組](#acls-and-groups) 以取得詳細資訊。

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### 使用設定瀏覽器 {#using-the-configuration-browser}

1. 前往 **全域導覽** -> **工具** > [**配置瀏覽器**.](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

   現有資料夾會列在左側，包括 `global` 檔案夾。

1. 按一下&#x200B;**建立**。
1. 在 **建立配置** 對話方塊下列欄位需要設定：

   * **標題**:提供設定資料夾的標題
   * **可編輯的範本**:勾選以允許此資料夾內有可編輯的範本

1. 按一下 **建立**

>[!NOTE]
>
>在 [配置瀏覽器、](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 您可以編輯全域資料夾並啟用 **可編輯的範本** 選項，但建議不要使用此資料夾建立模板。

### ACL和組 {#acls-and-groups}

建立範本資料夾後（透過CRXDE或使用設定瀏覽器），必須為範本資料夾的適當群組定義ACL，以確保適當的安全性。

的範本資料夾 [WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 可做為範例。

#### 範本作者群組 {#the-template-authors-group}

此 `template-authors` 群組是用來管理範本存取權的群組，隨附AEM的標準，但空白。 必須將使用者新增至專案/網站的群組。

>[!CAUTION]
>
>此 `template-authors` 群組僅適用於必須能夠建立新範本的使用者。
>
>編輯範本功能強大，若未正確編輯，現有範本可能會損毀。 因此，此角色應該重點突出，並僅包括合格的使用者。

下表詳細說明了進行範本編輯所需的權限。

<table>
 <tbody>
  <tr>
   <th>路徑</th>
   <th>角色/群組</th>
   <th>權限<br /> </th>
   <th>說明</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>範本作者<br /> </td>
   <td>讀、寫、復寫</td>
   <td>在特定站點中建立、讀取、更新、刪除和複製模板的模板作者 <code>/conf</code> 空間</td>
  </tr>
  <tr>
   <td>匿名Web用戶</td>
   <td>讀取</td>
   <td>匿名Web用戶在呈現頁面時必須讀取模板</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>複製</td>
   <td>replicateContent作者在啟動頁面時需要啟動頁面的範本</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>讀、寫、復寫</td>
   <td>在特定站點中建立、讀取、更新、刪除和複製模板的模板作者 <code>/conf</code> 空間</td>
  </tr>
  <tr>
   <td>匿名Web用戶</td>
   <td>讀取</td>
   <td>匿名Web用戶在呈現頁面時必須讀取策略</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>複製</td>
   <td>啟用頁面時，內容作者需要啟用頁面範本的原則</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>範本作者</td>
   <td>讀取</td>
   <td>範本作者會根據其中一種預先定義的範本類型，建立新範本。</td>
  </tr>
  <tr>
   <td>匿名Web用戶</td>
   <td>無</td>
   <td>匿名Web用戶不能訪問模板類型</td>
  </tr>
 </tbody>
</table>

此預設值 `template-authors` 群組僅涵蓋專案設定，所有 `template-authors` 成員可以訪問和編寫所有模板。 若要進行更複雜的設定（需要多個範本作者群組來區隔範本的存取權），必須建立更多自訂範本作者群組。 不過，範本作者群組的權限仍會相同。

## 範本類型 {#template-type}

建立新範本時，您需要指定範本類型：

* 模板類型有效地為模板提供模板。 建立新模板時，將使用所選模板類型的結構和初始內容建立新模板。

   * 模板類型被複製以建立模板。
   * 複製發生後，範本和範本類型之間的唯一連線就是靜態參考，以供參考。

* 範本類型可讓您定義：

   * 頁面元件的資源類型。
   * 根節點的策略，定義模板編輯器中允許的元件。
   * 建議為回應式格線定義斷點，並在範本類型上設定行動模擬器。

* AEM提供一些現成的範本類型選項，例如「HTML5頁面」和「最適化表單頁面」。

   * 其他範例則隨附於 [WKND教學課程。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* 範本類型通常由開發人員定義。

現成可用的範本類型儲存在：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>您不得變更 `/libs` 路徑。 這是因為 `/libs` 可隨時由AEM的更新加以覆寫。

您的網站特定範本類型應儲存在以下可比位置：

* `/apps/settings/wcm/template-types`

自訂範本類型的定義應儲存在使用者定義的資料夾中（建議），或儲存在 `global`. 例如：

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

如果已建立可作為其他模板基礎的模板，則可以將此模板作為模板類型複製。

1. 建立範本的方式與任何頁面範本相同 [這裡記載的](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author)，這將作為範本類型的基礎。
1. 使用CRXDE Lite，從 `templates` 節點 `template-types` 節點 [範本資料夾](#template-folders).
1. 從 `templates` 節點 [範本資料夾](#template-folders).
1. 在位於 `template-types` 節點，全部刪除 `cq:template` 和 `cq:templateType` 全部屬性 `jcr:content` 節點。

您也可以使用可編輯範本範例來開發自己的範本類型，此範本可在GitHub上取得。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-sites-example-custom-template-type專案](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 範本定義 {#template-definitions}

可編輯範本的定義會儲存 [用戶定義的資料夾](#template-folders) （建議）或 `global`. 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

模板的根節點類型為 `cq:Template` 骨架結構為：

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

主要元素為：

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
   * &quot;**類型**: `String`
   * **值**: `draft`, `enabled` 或 `disabled`

### 結構 {#structure}

定義結果頁面的結構：

* 已與初始內容合併( `/initial`)。
* 對結構所做的變更將反映在使用範本建立的任何頁面中。
* 此 `root` ( `structure/jcr:content/root`)節點會定義產生頁面中可用的元件清單。
   * 在模板結構中定義的元件不能在任何結果頁面上移動或從中刪除。
   * 元件解除鎖定後， `editable` 屬性設為 `true`.
   * 一旦解除鎖定已包含內容的元件，此內容將移至 `initial` 分支。

* 此 `cq:responsive` 節點保留回應式配置的定義。

### 初始內容 {#initial-content}

定義新頁面建立時將擁有的初始內容：

* 包含 `jcr:content` 會複製到任何新頁面的節點。
* 與結構合併( `/structure`)。
* 如果初始內容在建立後變更，則任何現有頁面都不會更新。
* 此 `root` 節點包含元件清單，以定義產生頁面中可用的項目。
* 如果在結構模式中將內容添加到元件，並且該元件隨後被解鎖（反之亦然），則此內容用作初始內容。

### 配置 {#layout}

當 [編輯可定義佈局的模板](/help/sites-cloud/authoring/features/templates.md)，此用途 [標準回應式版面](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### 內容原則 {#content-policies}

內容策略定義元件的設計屬性。 例如，可用元件或最小/最大尺寸。 這些規則適用於範本（以及使用範本建立的頁面）。 可在範本編輯器中建立並選取內容原則。

* 屬性 `cq:policy`，在 `root` 節點
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
提供頁面段落系統的內容原則的相對參考。

* 屬性 `cq:policy`，位於 `root`，提供個別元件之原則的連結。

* 實際策略定義儲存在：
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>策略定義的路徑取決於元件的路徑。 `cq:policy` 保留對配置本身的相對引用。

### 頁面原則 {#page-policies}

頁面原則可讓您定義 [內容原則](#content-policies) 針對頁面(main parsys)，位於範本或產生的頁面中。

### 啟用和允許範本使用 {#enabling-and-allowing-a-template-for-use}

1. **啟用範本**

   必須先啟用範本，才能使用範本：

   * [啟用範本](/help/sites-cloud/authoring/features/templates.md) 從 **範本** 控制台。

   * 在 `jcr:content` 節點。

      * 例如，在：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定義屬性：

         * 名稱：狀態
         * 類型：字串
         * 值: `enabled`

1. **允許的範本**

   * [在 **頁面屬性**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) 的相應頁或根頁。
   * 設定屬性：
      `cq:allowedTemplates`
在 
`jcr:content` 所需分支的節點。
   例如，值為：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 產生的內容頁面 {#resultant-content-pages}

從可編輯的範本建立的頁面：

* 建立時使用合併自的子樹 `structure` 和 `initial` 在範本中

* 在模板和模板類型中保留對資訊的引用。 這是透過 `jcr:content` 節點（具有屬性）:

   * `cq:template`  — 提供實際模板的動態參考；可讓範本的變更反映在實際頁面上。

   * `cq:templateType`  — 提供範本類型的參考。

![範本、內容和元件之間的相互關係](assets/templates-content-components.png)

上圖顯示範本、內容和元件之間的關聯：

* 控制器 —  `/content/<my-site>/<my-page>`  — 參照模板的生成頁面。 內容可控制整個程式。 根據定義，它訪問相應的模板和元件。
* 配置 —  `/conf/<my-folder>/settings/wcm/templates/<my-template>` - [範本和相關內容原則](#template-definitions) 定義頁面設定。
* 模型 — OSGi套件組合 —  [OSGI套件組合](/help/implementing/deploying/configuring-osgi.md) 實作功能。
* 檢視 —  `/apps/<my-site>/components`  — 在製作和發佈環境中，內容會由元件呈現。

呈現頁面時：

* **範本**:

   * 此 `cq:template` 其屬性 `jcr:content` 會參考節點來存取與該頁面對應的範本。

* **元件**:

   * 頁面元件將合併 `structure/jcr:content` 模板的樹 `jcr:content` 頁面樹狀結構。
      * 頁面元件將僅允許作者編輯已標示為可編輯的範本結構節點（以及任何子項）。
      * 在頁面上呈現元件時，該元件的相對路徑將取自 `jcr:content` 節點；在 `policies/jcr:content` 然後會搜尋範本的節點。
         * 此 `cq:policy` 此節點的屬性指向實際內容策略（即它包含該元件的設計配置）。
            * 這允許您有多個模板重複使用相同的內容策略配置。

### 範本可用性 {#template-availability}

在網站管理員介面中建立新頁面時，可用範本清單會根據新頁面的位置，以及每個範本中指定的位置限制而定。

下列屬性決定範本是否為 `T` 可用於將新頁面放置為頁面子項 `P`. 這些屬性中的每個都是多值字串，包含零個或多個用於與路徑比對的規則運算式：

* 此 `cq:allowedTemplates` 屬性 `jcr:content` 子節點 `P` 或祖先 `P`.

* 此 `allowedPaths` 屬性 `T`.

* 此 `allowedParents` 屬性 `T`.

* 此 `allowedChildren` 模板的屬性 `P`.

評價工作如下：

* 第一個非空白 `cq:allowedTemplates` 遞增頁面階層時找到的屬性，開頭為 `P` 與 `T`. 如果沒有任何值相符， `T` 被拒絕。

* 若 `T` 非空白 `allowedPaths` 屬性，但沒有任何值符合 `P`, `T` 被拒絕。

* 如果上述兩個屬性均為空或不存在， `T` 拒絕，除非它屬於與 `P`. `T` 屬於與 `P` 如果且唯若路徑的第二層名稱 `T` 與路徑的第二層的名稱相同 `P`. 例如，範本 `/apps/wknd/templates/foo` 屬於與頁面相同的應用程式 `/content/wknd`.

* 若 `T` 具有非空白 `allowedParents` 屬性，但沒有任何值符合 `P`, `T` 被拒絕。

* 若範本為 `P` 非空白 `allowedChildren` 屬性，但沒有任何值符合 `T`, `T` 被拒絕。

* 在其他所有情況下， `T` 中指定的規則。

下圖描述了模板評估流程：

![模板評估過程](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM提供多個屬性，以控制 **網站**. 但是，結合這些規則可能會產生非常複雜的規則，且難以追蹤和管理。
>
>因此，Adobe建議您透過定義：
>
>* 只有 `cq:allowedTemplates` 屬性
>
>* 僅位於站點根
>
>如需範例，請參閱 [WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 內容： `/content/wknd/jcr:content`
>
>屬性 `allowedPaths`, `allowedParents`，和 `allowedChildren` 也可以放在範本上，以定義更複雜的規則。 但是，如果可能， *mod* 更簡單地定義 `cq:allowedTemplates` 屬性（如果需要進一步限制允許的範本）。
>
>另一個優點是 `cq:allowedTemplates` 屬性可由作者在 **進階** 的 **頁面屬性**. 無法使用（標準）UI更新其他範本屬性，因此需要開發人員來維護每次變更的規則和程式碼部署。

#### 限制子頁面中使用的模板 {#limiting-templates-used-in-child-pages}

若要限制哪些範本可用來建立指定頁面下的子頁面，請使用 `cq:allowedTemplates` 屬性 `jcr:content` 頁的節點，以指定允許作為子頁的模板清單。 例如，清單中的每個值必須是允許的子頁面範本的絕對路徑 `/apps/wknd/templates/page-content`.

您可以使用 `cq:allowedTemplates` 範本的屬性  `jcr:content` 節點，將此配置應用於使用此模板的所有新建立的頁面。

如果您想要新增更多限制（例如關於範本階層），可使用 `allowedParents/allowedChildren` 屬性。 然後，您可以明確指定從範本T建立的頁面必須是從範本T建立的頁面的父/子頁面。
