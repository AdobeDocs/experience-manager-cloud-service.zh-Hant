---
title: 頁面範本
description: 在建立將用作新頁面基礎的頁面時使用頁面模板
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '3296'
ht-degree: 1%

---

# 頁面範本 {#page-templates}

建立頁面時，需要選擇模板。 頁面模板用作新頁面的基礎。 模板定義結果頁面的結構、任何初始內容以及可使用的元件（設計屬性）。 這有幾個優點：

* 頁面模板允許專業作者 [建立和編輯模板](/help/sites-cloud/authoring/features/templates.md)。
   * 這類專業作者被稱為 **模板作者**
   * 模板作者必須是 `template-authors` 組。
* 頁面模板保留與從它們建立的任何頁面的動態連接。 這可確保對模板所做的任何更改都反映在頁面本身中。
* 頁面模板使頁面元件更為通用，因此無需自定義即可使用核心頁面元件。

使用「頁面模板」，生成頁面的部分會在元件中隔離。 您可以在UI中配置元件的必要組合，從而消除了為每個頁面變體開發新頁面元件的需要。

此文檔：

* 概述了建立頁面模板
* 描述建立可編輯模板所需的管理員/開發人員任務
* 描述可編輯模板的技術基礎
* 介紹如AEM何評估模板的可用性

>[!NOTE]
>
>本文檔假定您已經熟悉建立和編輯模板。 請參閱創作文檔 [建立頁面模板](/help/sites-cloud/authoring/features/templates.md)，其中詳細說明了模板作者所公開的可編輯模板的功能。

>[!TIP]
>
>[WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 通過實施示例深入瞭解如何使用頁面模板，對於瞭解如何在新項目中設定模板非常有用

## 建立新模板 {#creating-a-new-template}

建立頁面模板主要使用 [模板控制台和模板編輯器](/help/sites-cloud/authoring/features/templates.md) 模板作者。 本節概述了此過程，並隨後介紹了在技術級別發生的情況。

建立新可編輯模板時，您：

1. 建立 [模板的資料夾](#template-folders)。 這不是強制性的，但建議採用最佳做法。
1. 選擇 [模板類型](#template-type)。 複製此項以建立 [模板定義](#template-definitions)。

   >[!NOTE]
   >
   >現成提供了模板類型的選擇。 您也可以 [建立您自己的站點特定模板類型](#creating-template-types) 的子菜單。

1. 配置新模板的結構、內容策略、初始內容和佈局。

   **結構**

   * 該結構允許您為模板定義元件和內容。
   * 在模板結構中定義的元件不能移動到結果頁面上，也不能從任何結果頁面中刪除。
   * 如果希望頁面作者能夠添加和刪除元件，請向模板中添加段落系統。
   * 可以解鎖和重新鎖定元件，以允許您定義初始內容。

   有關模板作者如何定義結構的詳細資訊，請參見 [建立頁面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)。

   有關結構的技術詳細資訊，請參見 [結構](#structure) 的子菜單。

   **原則**

   * 內容策略定義元件的設計屬性。

      * 例如，可用元件或最小/最大尺寸。
   * 這些模板（以及使用模板建立的頁面）適用。

   有關模板作者如何定義策略的詳細資訊，請參見 [建立頁面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)。

   有關策略的技術詳細資訊，請參見 [內容策略](#content-policies) 的子菜單。

   **初始內容**

   * 初始內容定義在首次基於模板建立頁面時將顯示的內容。
   * 然後，頁面作者可以編輯初始內容。

   有關模板作者如何定義結構的詳細資訊，請參見 [建立頁面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author)。

   有關初始內容的技術詳細資訊，請參見 [初始內容](#initial-content) 的子菜單。

   **配置**

   * 可以為一系列設備定義模板佈局。
   * 模板的響應佈局與頁面創作的佈局一樣。

   有關模板作者如何定義模板佈局的詳細資訊，請參閱 [建立頁面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author)。

   有關模板佈局的技術詳細資訊，請參閱 [佈局](#layout) 的子菜單。

1. 啟用模板，然後允許它用於特定內容樹。

   * 可以啟用或禁用模板，使其對頁面作者可用或不可用。
   * 模板可用於某些頁面分支或不可用。

   有關模板作者如何啟用模板的詳細資訊，請參見 [建立頁面模板](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author)。

   有關啟用模板的技術詳細資訊，請參見 [為我們啟用和允許模板](#enabling-and-allowing-a-template-for-use)本文檔

1. 使用它建立內容頁。

   * 使用模板建立新頁面時，靜態模板和可編輯模板之間沒有可見的差異和指示。
   * 對於頁面作者，該過程是透明的。

   有關頁面作者如何使用模板建立頁面的詳細資訊，請參閱 [建立和組織頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates)。

   有關使用可編輯模板建立頁面的技術詳細資訊，請參閱 [結果內容頁](#resultant-content-pages) 的子菜單。

>[!TIP]
>
>切勿輸入需要國際化到模板中的任何資訊。 就內部化而言， [核心元件的本地化功能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) 。

>[!NOTE]
>
>模板是優化頁面建立工作流的強大工具。 然而，過多的模板可能會使作者不堪重負，使頁面建立變得混亂。 一個很好的經驗法則是將模板數量保持在100以下。
>
>Adobe建議不要有1000個以上的模板，因為可能會影響效能。

>[!NOTE]
>
>編輯器客戶端庫假定 `cq.shared` 內容頁中的命名空間，如果不存在JavaScript錯誤 `Uncaught TypeError: Cannot read property 'shared' of undefined` 將產生結果。
>
>所有示例內容頁包含 `cq.shared`，因此基於它們的任何內容都自動包括 `cq.shared`。 但是，如果您決定從頭開始建立自己的內容頁面而不根據示例內容進行建立，則必須確保包括 `cq.shared` 命名空間。
>
>請參閱 [使用客戶端庫](/help/implementing/developing/introduction/clientlibs.md) 的上界。



## 模板資料夾 {#template-folders}

為了組織模板，您可以使用以下資料夾：

* `global`
* 特定於站點

>[!NOTE]
>
>即使您可以嵌套資料夾，當用戶在 **模板** 控制台呈扁平結構。

在標準AEM實例中 `global` 模板控制台中已存在資料夾。 如果在當前資料夾中未找到策略和/或模板類型，則保留預設模板並充當回退。 您可以將預設模板添加到此資料夾或建立新資料夾（推薦）。

>[!NOTE]
>
>最好建立一個新資料夾來保存您的自定義模板，而不要使用 `global` 的子菜單。

>[!CAUTION]
>
>資料夾必須由用戶建立 `admin` 。

模板類型和策略按以下優先順序繼承到所有資料夾：

1. 當前資料夾
1. 當前資料夾的父級
1. `/conf/global`
1. `/apps`
1. `/libs`

將建立所有允許條目的清單。 如果任何配置重疊( `path`/ `label`)，只向用戶顯示最接近當前資料夾的實例。

要建立新資料夾，您可以執行以下操作：

* 以寫程式方式或使用CRXDE Lite
* 使用 [配置瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## 使用CRXDE Lite {#using-crxde-lite}

1. 可以以寫程式方式或使用CRXDE Lite為實例建立新資料夾（在/conf下）。

   必須使用以下結構：

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
   * 值：要顯示在 **模板** 控制台。

1. 除了標準的創作權限和權限(例如 `content-authors`)現在需要分配組並定義所需的訪問權限(ACL)，以便作者能夠在新資料夾中建立模板。

   的 `template-authors` group是需要分配的預設組。 請參閱一節 [ACL和組](#acls-and-groups) 的雙曲餘切值。

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### 使用配置瀏覽器 {#using-the-configuration-browser}

1. 轉到 **全局導航** -> **工具** > [**配置瀏覽器**。](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

   現有資料夾將列在左側，包括 `global` 的子菜單。

1. 按一下&#x200B;**建立**。
1. 在 **建立配置** 對話框需要配置以下欄位：

   * **標題**:提供配置資料夾的標題
   * **可編輯模板**:勾選以允許此資料夾中的可編輯模板

1. 按一下 **建立**

>[!NOTE]
>
>在 [配置瀏覽器，](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 可以編輯全局資料夾並激活 **可編輯模板** 的子菜單。

### ACL和組 {#acls-and-groups}

建立模板資料夾（通過CRXDE或使用配置瀏覽器）後，必須為模板資料夾的相應組定義ACL，以確保適當的安全性。

的模板資料夾 [WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 可以作為一個例子。

#### 模板作者組 {#the-template-authors-group}

的 `template-authors` group是用於管理對模板的訪問的組，它是標準的，AEM但為空。 必須將用戶添加到項目/站點的組。

>[!CAUTION]
>
>的 `template-authors` 組僅用於必須能夠建立新模板的用戶。
>
>編輯模板功能強大，如果不正確編輯，現有模板將被破壞。 因此，此角色應重點突出，並僅包括合格用戶。

下表詳細說明了模板編輯所需的權限。

<table>
 <tbody>
  <tr>
   <th>路徑</th>
   <th>角色/組</th>
   <th>權限<br /> </th>
   <th>說明</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>模板作者<br /> </td>
   <td>讀、寫、複製</td>
   <td>在特定站點中建立、讀取、更新、刪除和複製模板的模板作者 <code>/conf</code> 空間</td>
  </tr>
  <tr>
   <td>匿名Web用戶</td>
   <td>讀</td>
   <td>匿名Web用戶在呈現頁面時必須讀取模板</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>複製</td>
   <td>replicateContent作者在激活頁面時需要激活頁面的模板</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>讀、寫、複製</td>
   <td>在特定站點中建立、讀取、更新、刪除和複製模板的模板作者 <code>/conf</code> 空間</td>
  </tr>
  <tr>
   <td>匿名Web用戶</td>
   <td>讀</td>
   <td>匿名Web用戶在呈現頁面時必須讀取策略</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>複製</td>
   <td>激活頁面時，內容作者需要激活頁面模板的策略</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>模板作者</td>
   <td>讀</td>
   <td>模板作者基於預定義模板類型之一建立新模板。</td>
  </tr>
  <tr>
   <td>匿名Web用戶</td>
   <td>無</td>
   <td>匿名Web用戶不得訪問模板類型</td>
  </tr>
 </tbody>
</table>

此預設值 `template-authors` 組僅涵蓋項目設定，其中 `template-authors` 允許成員訪問和建立所有模板。 對於更複雜的設定，需要多個模板作者組才能分開訪問模板，必須建立更多自定義模板作者組。 但是，模板作者組的權限仍然相同。

## 模板類型 {#template-type}

建立新模板時，需要指定模板類型：

* 模板類型有效地為模板提供模板。 建立新模板時，所選模板類型的結構和初始內容將用於建立新模板。

   * 複製模板類型以建立模板。
   * 複製完成後，模板與模板類型之間的唯一連接就是靜態引用，以供參考。

* 模板類型允許您定義：

   * 頁面元件的資源類型。
   * 根節點的策略，它定義模板編輯器中允許的元件。
   * 建議在模板類型上定義響應網格的斷點和移動模擬器的設定。

* 提AEM供了一些現成的模板類型選擇，如「HTML5頁」和「自適應表單頁」。

   * 作為Windows Server的一部分，提供了其他示例 [WKND教程。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* 模板類型通常由開發人員定義。

現成模板類型儲存在以下位置：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>您不能更改 `/libs` 路徑。 這是因為 `/libs` 可隨時被更新覆蓋AEM。

您的站點特定模板類型應儲存在以下可比位置：

* `/apps/settings/wcm/template-types`

自定義模板類型的定義應儲存在用戶定義的資料夾中（建議），或儲存在 `global`。 例如：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>模板類型必須尊重正確的資料夾結構(即 `/settings/wcm/...`)，否則找不到模板類型。

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

### 建立模板類型 {#creating-template-types}

如果已建立可作為其他模板基礎的模板，則可以將此模板複製為模板類型。

1. 像建立任何頁面模板一樣建立模板 [此處記錄](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author)，將作為模板類型的基礎。
1. 使用CRXDE Lite，從 `templates` 節點到 `template-types` 節點 [模板資料夾](#template-folders)。
1. 從 `templates` 節點 [模板資料夾](#template-folders)。
1. 在位於 `template-types` 節點，刪除所有 `cq:template` 和 `cq:templateType` `jcr:content` 屬性。

您還可以使用GitHub上提供的示例可編輯模板作為基礎來開發自己的模板類型。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟aem-sites-example-custom-template-type項目](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 模板定義 {#template-definitions}

儲存可編輯模板的定義 [用戶定義的資料夾](#template-folders) （推薦）或 `global`。 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

模板的根節點的類型 `cq:Template` 骨架結構為：

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

主要內容有：

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr：內容 {#jcr-content}

此節點保存模板的屬性：

* **名稱**: `jcr:title`
* **名稱**: `status`
   * &quot;**類型**: `String`
   * **值**: `draft`。 `enabled` 或 `disabled`

### 結構 {#structure}

定義結果頁的結構：

* 與初始內容合併( `/initial`)。
* 對結構所做的更改將反映在使用模板建立的任何頁面中。
* 的 `root` ( `structure/jcr:content/root`)節點定義將在生成頁面中可用的元件清單。
   * 在模板結構中定義的元件不能移動或從任何結果頁面中刪除。
   * 一旦元件解鎖， `editable` 屬性設定為 `true`。
   * 一旦解除鎖定已包含內容的元件，此內容將移動到 `initial` 分支。

* 的 `cq:responsive` 節點保存響應佈局的定義。

### 初始內容 {#initial-content}

定義新頁面在建立時將具有的初始內容：

* 包含 `jcr:content` 複製到任何新頁面的節點。
* 與結構合併( `/structure`)。
* 如果初始內容在建立後發生更改，則不會更新任何現有頁面。
* 的 `root` 節點包含元件清單，以定義生成頁中可用的元件。
* 如果內容以結構模式添加到元件中，並且該元件隨後被解鎖（反之亦然），則此內容將用作初始內容。

### 配置 {#layout}

當 [編輯可定義佈局的模板](/help/sites-cloud/authoring/features/templates.md)，使用 [標準響應佈局](/help/sites-cloud/authoring/features/responsive-layout.md)。

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### 內容策略 {#content-policies}

內容策略定義元件的設計屬性。 例如，可用元件或最小/最大尺寸。 這些模板（以及使用模板建立的頁面）適用。 可以在模板編輯器中建立和選擇內容策略。

* 屬性 `cq:policy`的 `root` 節點
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
為頁面的段落系統提供對內容策略的相對引用。

* 屬性 `cq:policy`，在下的元件顯式節點上 `root`，提供指向各個元件的策略的連結。

* 實際策略定義儲存在：
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>策略定義的路徑取決於元件的路徑。 `cq:policy` 保存對配置本身的相對引用。

### 頁面原則 {#page-policies}

頁面策略允許您定義 [內容策略](#content-policies) 在模板或結果頁中。

### 啟用和允許使用模板 {#enabling-and-allowing-a-template-for-use}

1. **啟用模板**

   必須通過以下任一方法啟用模板，才能使用模板：

   * [啟用模板](/help/sites-cloud/authoring/features/templates.md) 從 **模板** 控制台。

   * 在 `jcr:content` 的下界。

      * 例如，在：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定義屬性：

         * 名稱：狀態
         * 類型：字串
         * 值: `enabled`

1. **允許的範本**

   * [在上定義允許的模板路徑 **頁面屬性**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) 子分支的相應頁面或根頁面。
   * 設定屬性：
      `cq:allowedTemplates`
在 
`jcr:content` 所需分支的節點。
   例如，值為：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 結果內容頁 {#resultant-content-pages}

根據可編輯模板建立的頁面：

* 使用合併自的子樹建立 `structure` 和 `initial` 中

* 對模板和模板類型中保存的資訊有引用。 這是通過 `jcr:content` 具有以下屬性的節點：

   * `cq:template`  — 提供對實際模板的動態引用；允許對模板的更改反映在實際頁面上。

   * `cq:templateType`  — 提供對模板類型的引用。

![模板、內容和元件如何相互關聯](assets/templates-content-components.png)

上圖顯示了模板、內容和元件如何相互關聯：

* 控制器 —  `/content/<my-site>/<my-page>`  — 引用模板的結果頁。 內容控制整個過程。 根據定義，它訪問相應的模板和元件。
* 配置 —  `/conf/<my-folder>/settings/wcm/templates/<my-template>` - [模板和相關內容策略](#template-definitions) 定義頁面配置。
* 型號 — OSGi捆綁包 —  [OSGI捆綁](/help/implementing/deploying/configuring-osgi.md) 實現功能。
* 視圖 —  `/apps/<my-site>/components`  — 在作者和發佈環境中，內容都由元件呈現。

呈現頁面時：

* **範本**:

   * 的 `cq:template` 其財產 `jcr:content` 將引用節點以訪問與該頁對應的模板。

* **元件**:

   * 頁面元件將合併 `structure/jcr:content` 模板樹 `jcr:content` 樹。
      * 頁面元件將僅允許作者編輯已標籤為可編輯的模板結構的節點（以及任何子級）。
      * 在頁面上呈現元件時，該元件的相對路徑將從 `jcr:content` 節點；同一條路 `policies/jcr:content` 然後將搜索模板的節點。
         * 的 `cq:policy` 此節點的屬性指向實際內容策略（即它包含該元件的設計配置）。
            * 這樣，您就可以擁有多個模板，這些模板可以重新使用相同的內容策略配置。

### 範本可用性 {#template-availability}

在站點管理介面中建立新頁面時，可用模板清單取決於新頁面的位置以及在每個模板中指定的放置限制。

以下屬性確定模板 `T` 允許將新頁面用作頁面的子頁面 `P`。 每個屬性都是一個多值字串，包含零個或多個用於與路徑匹配的規則運算式：

* 的 `cq:allowedTemplates` 屬性 `jcr:content` 子節點 `P` 或是 `P`。

* 的 `allowedPaths` 物業 `T`。

* 的 `allowedParents` 物業 `T`。

* 的 `allowedChildren` 模板的屬性 `P`。

評價工作如下：

* 第一個非空 `cq:allowedTemplates` 升序頁層次結構時找到的屬性 `P` 與 `T`。 如果所有值都不匹配， `T` 已拒絕。

* 如果 `T` 具有非空 `allowedPaths` 屬性，但所有值均與 `P`。 `T` 已拒絕。

* 如果上述兩個屬性都為空或不存在， `T` 除非它屬於與 `P`。 `T` 屬於與 `P` 如果且僅當路徑的第二級的名稱 `T` 與路徑的第二級的名稱相同 `P`。 例如，模板 `/apps/wknd/templates/foo` 屬於與頁面相同的應用程式 `/content/wknd`。

* 如果 `T` 具有非空 `allowedParents` 屬性，但所有值均與 `P`。 `T` 已拒絕。

* 如果的模板 `P` 具有非空 `allowedChildren` 屬性，但所有值均與 `T`。 `T` 已拒絕。

* 在其他情況下， `T` 的子菜單。

下圖描述了模板評估流程：

![模板評估流程](assets/template-evaluation.png)

>[!CAUTION]
>
>提供AEM多個屬性，以控制在 **站點**。 但是，將它們組合起來會導致非常複雜的規則，難以跟蹤和管理。
>
>因此，Adobe建議您通過定義：
>
>* 只有 `cq:allowedTemplates` 屬性
>
>* 僅在站點根目錄上
>
>有關示例，請參見 [WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 內容： `/content/wknd/jcr:content`
>
>屬性 `allowedPaths`。 `allowedParents`, `allowedChildren` 也可以放在模板上以定義更複雜的規則。 但是，如果可能的話 *多* 更簡單地定義 `cq:allowedTemplates` 如果需要進一步限制允許的模板，則在站點的子節上顯示屬性。
>
>另外一個優勢是 `cq:allowedTemplates` 屬性可由作者在 **高級** 頁籤 **頁面屬性**。 其他模板屬性無法使用（標準）UI更新，因此需要開發人員來維護每次更改的規則和代碼部署。

#### 限制子頁中使用的模板 {#limiting-templates-used-in-child-pages}

要限制可用於在給定頁面下建立子頁面的模板，請使用 `cq:allowedTemplates` 物業 `jcr:content` 的子頁。 清單中的每個值必須是允許的子頁模板的絕對路徑，例如 `/apps/wknd/templates/page-content`。

您可以使用 `cq:allowedTemplates` 模板的  `jcr:content` 節點，以將此配置應用於使用此模板的所有新建立的頁面。

如果要添加更多約束（例如有關模板層次結構），可以使用 `allowedParents/allowedChildren` 屬性。 然後，可以明確指定從模板T建立的頁面必須是從模板T建立的頁面的父/子。
