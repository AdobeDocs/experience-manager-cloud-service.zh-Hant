---
title: 可編輯的範本
description: 瞭解在建立頁面、定義其初始內容、結構化內容、編寫原則和版面配置時，如何使用可編輯範本。
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 1%

---

# 可編輯的範本 {#editable-templates}

瞭解在建立頁面、定義其初始內容、結構化內容、編寫原則和版面配置時，如何使用可編輯範本。

## 概觀 {#overview}

建立頁面時，您需要選取範本。 頁面範本會用作新頁面的基礎。 範本可以定義結果頁面的結構、任何初始內容以及可以使用的元件（設計屬性）。

* 可編輯的範本可讓作者建立和使用範本。
* 可編輯的範本可用來建立可透過兩者編輯的頁面
   * [頁面編輯器](/help/sites-cloud/authoring/page-editor/templates.md)和
   * [通用編輯器](/help/sites-cloud/authoring/universal-editor/templates.md)

用來建立可透過通用編輯器編輯之頁面的頁面範本使用可編輯範本功能的有限子集。 因此，本檔案的其餘部分側重於用於建立可使用頁面編輯器編輯的頁面的可編輯範本。

## 使用頁面編輯器編輯的可編輯範本和頁面 {#page-editor}

建立範本以建立可使用「頁面編輯器」編輯的頁面時，通常會識別專門的作者。

* 這類特殊作者稱為&#x200B;**範本作者**
* 範本作者必須是`template-authors`群組的成員。
* 可編輯的範本會保留與任何建立頁面的動態連線。 這可確保對範本所做的任何變更都會反映在頁面本身中。
* 可編輯的範本讓頁面元件變得更通用，以便無需自訂即可使用核心頁面元件。

使用可編輯的範本，建立頁面的片段會隔離在元件中。 您可以在UI中設定必要的元件組合，因此不需要為每個頁面變數開發新的頁面元件。

本檔案：

* 提供建立可編輯範本的概觀
* 說明建立可編輯範本所需的管理員/開發人員工作
* 說明可編輯範本的技術基礎
* 說明AEM如何評估範本的可用性

>[!NOTE]
>
>本檔案假設您已熟悉建立和編輯範本。 請參閱編寫檔案[使用頁面編輯器建立可編輯頁面的範本](/help/sites-cloud/authoring/page-editor/templates.md)，其中詳細說明了範本作者所看到的可編輯範本功能。

>[!TIP]
>
>[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)會透過實作範例深入探討如何使用可編輯的範本，對於瞭解如何在新的專案中設定範本非常有用

## 建立新的可編輯範本 {#creating-a-new-template}

建立可編輯的範本主要是由範本作者使用[範本主控台和範本編輯器](/help/sites-cloud/authoring/page-editor/templates.md)完成。 本節提供此程式的概述，並接著說明在技術層級進行的工作。

建立可編輯的範本時，您可以：

1. 為範本[建立](#template-folders)資料夾。 這並不強制，但建議最佳實務。
1. 選取[範本型別](#template-type)。 這已複製以建立[範本定義](#template-definitions)。

   >[!NOTE]
   >
   >現成提供一系列範本型別。 如有必要，您也可以[建立您自己的網站特定範本型別](#creating-template-types)。

1. 設定新範本的結構、內容原則、初始內容和版面配置。

   **結構**

   * 結構可讓您定義範本的元件和內容。
   * 範本結構中定義的元件無法在產生的頁面上移動，也無法從任何產生的頁面中刪除。
   * 如果您希望頁面作者能夠新增和移除元件，請新增段落系統至範本。
   * 您可以解鎖元件，然後再將其鎖定，以便定義初始內容。

   如需範本作者如何定義結構的詳細資訊，請參閱[建立可使用頁面編輯器編輯的頁面的範本](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author)。

   如需結構的技術細節，請參閱本檔案中的[結構](#structure)。

   **原則**

   * 內容原則會定義元件的設計屬性。

      * 例如，可用的元件或最小/最大尺寸。

   * 這些適用於範本（以及使用範本建立的頁面）。

   如需範本作者如何定義原則的詳細資訊，請參閱[建立可使用頁面編輯器編輯的頁面的範本](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author)。

   如需原則的技術詳細資訊，請參閱本檔案中的[內容原則](#content-policies)。

   **初始內容**

   * 初始內容定義首次根據範本建立頁面時顯示的內容。
   * 然後，頁面作者可以編輯初始內容。

   如需範本作者如何定義結構的詳細資訊，請參閱[建立可使用頁面編輯器編輯的頁面的範本](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-initial-content-author)。

   如需初始內容的技術細節，請參閱本檔案中的[初始內容](#initial-content)。

   **配置**

   * 您可以為一系列裝置定義範本配置。
   * 範本的回應式版面運作方式與頁面製作相同。

   如需範本作者如何定義範本配置的詳細資訊，請參閱[建立可使用頁面編輯器編輯的頁面的範本](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-layout-template-author)。

   如需範本配置的技術詳細資訊，請參閱本檔案中的[配置](#layout)。

1. 啟用範本，然後允許用於特定內容樹。

   * 您可以啟用或停用範本，讓頁面作者可以使用或無法使用此範本。
   * 範本可以供某些頁面分支使用或無法使用。

   如需範本作者如何啟用範本的詳細資訊，請參閱[範本以建立可使用頁面編輯器編輯的頁面](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author)。

   如需啟用範本的技術詳細資訊，請參閱本檔案中的[啟用和允許我們使用範本](#enabling-and-allowing-a-template-for-use)e

1. 使用它來建立內容頁面。

   * 使用範本建立頁面時，靜態範本和可編輯範本之間沒有可見的差異和指示。
   * 對於頁面作者，程式是透明的。

   如需頁面作者如何使用範本建立頁面的詳細資訊，請參閱[建立及組織頁面](/help/sites-cloud/authoring/sites-console/organizing-pages.md#templates)。

   如需使用可編輯的範本建立頁面的技術詳細資訊，請參閱本檔案中的[結果內容頁面](#resultant-content-pages)。

>[!TIP]
>
>切勿在範本中輸入任何必須國際化的資訊。 基於內部化的目的，建議使用核心元件[的](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=zh-Hant)本地化功能。

>[!NOTE]
>
>範本是簡化頁面建立工作流程的強大工具。 然而，太多的範本會讓作者不知所措，並使頁面建立變得混亂。 一個好的經驗法則是將範本數保持在100以下。
>
>由於潛在的效能影響，Adobe不建議使用超過1000個範本。

>[!NOTE]
>
>編輯器使用者端程式庫假設內容頁面中存在`cq.shared`名稱空間，如果不存在，將導致JavaScript錯誤`Uncaught TypeError: Cannot read property 'shared' of undefined`。
>
>所有範例內容頁面都包含`cq.shared`，因此任何以這些頁面為基礎的內容都會自動包含`cq.shared`。 但是，如果您決定從頭開始建立自己的內容頁面，而不根據範例內容，則必須確定包括`cq.shared`名稱空間。
>
>如需進一步資訊，請參閱[使用使用者端資料庫](/help/implementing/developing/introduction/clientlibs.md)。

## 範本資料夾 {#template-folders}

若要組織您的範本，您可以使用下列資料夾：

* `global`
* 特定網站

>[!NOTE]
>
>即使您可以巢狀內嵌資料夾，當使用者在&#x200B;**範本**&#x200B;主控台中檢視資料夾時，資料夾會顯示為平面結構。

在標準AEM執行個體中，`global`資料夾已存在於範本主控台中。 此檔案會保留預設範本，並在目前資料夾中找不到原則及/或範本型別時，做為遞補內容。 您可以將預設範本新增至此資料夾或建立資料夾（建議）。

>[!NOTE]
>
>最佳實務是建立資料夾以存放自訂範本，而不是使用`global`資料夾。

>[!CAUTION]
>
>資料夾必須由具有`admin`許可權的使用者建立。

範本型別和原則會根據下列優先順序繼承至所有資料夾：

1. 目前的資料夾
1. 目前資料夾的父系
1. `/conf/global`
1. `/apps`
1. `/libs`

將會建立所有允許專案的清單。 如果任何設定重疊( `path`/ `label`)，則只會向使用者顯示最接近目前資料夾的執行個體。

若要建立資料夾，您可以執行下列任一操作：

* 以程式設計方式或使用CRXDE Lite
* 使用[設定瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## 使用 CRXDE Lite {#using-crxde-lite}

1. 可以程式設計方式或使用CRXDE Lite為您的執行個體建立新資料夾（在/conf下）。

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

   * 名稱：`jcr:title`
   * 類型：`String`
   * 值：您要在&#x200B;**範本**&#x200B;主控台中顯示的標題（資料夾）。

1. 除了標準撰寫許可權和許可權（例如`content-authors`）之外，您現在需要指派群組並定義作者所需的存取許可權(ACL)，才能在新資料夾中建立範本。

   `template-authors`群組是必須指派的預設群組。 如需詳細資訊，請參閱[ACL和群組](#acls-and-groups)一節。

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### 使用設定瀏覽器 {#using-the-configuration-browser}

1. 移至&#x200B;**全域導覽** > **工具** > [**設定瀏覽器**](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)。

   現有資料夾會列在左側，包括`global`資料夾。

1. 按一下「**建立**」。
1. 在&#x200B;**建立設定**&#x200B;對話方塊中，需要設定下列欄位：

   * **標題**：提供設定資料夾的標題
   * **可編輯的範本**：勾選以允許此資料夾中的可編輯範本

1. 按一下「**建立**」

>[!NOTE]
>
>在[組態瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)中，如果您想要在此資料夾中建立範本，可以編輯全域資料夾並啟動&#x200B;**可編輯的範本**&#x200B;選項，但這不是建議的最佳作法。

### ACL和群組 {#acls-and-groups}

建立範本資料夾（透過CRXDE或使用「設定瀏覽器」）後，必須為範本資料夾的適當群組定義ACL，以確保適當的安全性。

[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)的範本資料夾可作為範例使用。

#### 範本 — 作者群組 {#the-template-authors-group}

`template-authors`群組是用來管理範本存取權的群組，且隨附於AEM，但為空白。 必須將使用者新增至專案/網站的群組。

>[!CAUTION]
>
>`template-authors`群組僅適用於必須能夠建立新範本的使用者。
>
>編輯範本的功能非常強大，如果不適當地編輯範本，現有範本可能會失效。 因此，此角色應重點關注，且僅包含合格使用者。

下表詳細說明範本編輯的必要許可權。

<table>
 <tbody>
  <tr>
   <th>路徑</th>
   <th>角色/群組</th>
   <th>許可權<br /> </th>
   <th>說明</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>範本作者<br /> </td>
   <td>讀取、寫入、復寫</td>
   <td>在網站特定<code>/conf</code>空間中建立、讀取、更新、刪除和復寫範本的範本作者</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者在轉譯頁面時必須讀取範本</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>復寫</td>
   <td>replicate內容作者在啟用頁面時需要啟用頁面的範本</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>讀取、寫入、復寫</td>
   <td>在網站特定<code>/conf</code>空間中建立、讀取、更新、刪除和復寫範本的範本作者</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者在轉譯頁面時必須讀取原則</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>復寫</td>
   <td>內容作者在啟用頁面時需要啟用頁面範本的原則</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>範本作者</td>
   <td>讀取</td>
   <td>範本作者會根據預先定義的範本型別之一建立新範本。</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>無</td>
   <td>匿名Web使用者不得存取範本型別</td>
  </tr>
 </tbody>
</table>

此預設`template-authors`群組僅涵蓋專案設定，其中所有`template-authors`成員都可存取及編寫所有範本。 對於更複雜的設定，需要多個範本作者群組來分隔範本的存取許可權，則必須建立更多自訂範本作者群組。 不過，範本作者群組的許可權將仍相同。

## 範本型別 {#template-type}

建立範本時，您需要指定範本型別：

* 範本型別可有效提供範本的範本。 建立範本時，會使用所選範本型別的結構和初始內容來建立新範本。

   * 範本型別會複製以建立範本。
   * 複製一旦發生，範本和範本型別之間的唯一連線是靜態參考，以供參考。

* 範本型別可讓您定義：

   * 頁面元件的資源型別。
   * 根節點的原則，定義範本編輯器中允許的元件。
   * 建議為回應式格線定義中斷點，並在範本型別上設定行動模擬器。

* AEM提供少量現成可用的範本型別，例如HTML5頁面和調適型表單頁面。

   * 提供其他範例作為[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)的一部分。

* 範本型別通常由開發人員定義。

現成可用的範本型別儲存在下列位置：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>您不得變更`/libs`路徑中的任何專案。 這是因為`/libs`的內容可以隨時由AEM的更新覆寫。

您的網站特定範本型別應儲存在類似位置：

* `/apps/settings/wcm/template-types`

您自訂範本型別的定義應該儲存在使用者定義的資料夾中（建議使用），或是儲存在`global`中。 例如：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>範本型別必須遵循正確的資料夾結構（即`/settings/wcm/...`），否則將無法找到範本型別。

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating an editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

>[!CAUTION]
>
>The value of `cq:deviceGroups` must be set as a relative path such as `mobile/groups/responsive` and not as an absolute path such as `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>With static templates /help/sites-developing/page-templates-static.md, the value of `cq:deviceGroups` could be set at the root of the site.
>
>With editable templates, this value is now stored at the template level and is not supported at the page root level.
-->

### 建立範本型別 {#creating-template-types}

如果您已建立可作為其他範本基礎的範本，則可以複製此範本作為範本型別。

1. 建立範本，就像建立任何頁面範本一樣。 請參閱[範本，以建立可使用頁面編輯器](/help/sites-cloud/authoring/page-editor/templates.md#creating-a-new-template-template-author)編輯的頁面。 這會作為範本型別的基礎。
1. 使用CRXDE Lite將建立的範本從`templates`節點複製到`template-types`範本資料夾[下的](#template-folders)節點。
1. 從`templates`範本資料夾[下的](#template-folders)節點中刪除範本。
1. 在`template-types`節點下的範本復本中，從所有`cq:template`節點刪除所有`cq:templateType`和`jcr:content`屬性。

您也可以使用GitHub提供的範例可編輯範本，在此基礎上開發自己的範本型別。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-sites-example-custom-template-type專案](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 將專案下載為[ZIP檔](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 範本定義 {#template-definitions}

可編輯範本的定義會儲存在[使用者定義的資料夾](#template-folders) （建議使用）或`global`中。 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

範本的根節點屬於型別`cq:Template`，骨架結構為：

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

主要元素包括：

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

此節點會保留範本的屬性：

* **名稱**：`jcr:title`
* **名稱**：`status`
   * &#39;&#39;**型別**： `String`
   * **值**： `draft`、`enabled`或`disabled`

### 結構 {#structure}

定義結果頁面的結構：

* 在建立頁面時與初始內容( `/initial`)合併。
* 對結構所做的變更會反映在使用範本建立的任何頁面中。
* `root` (`structure/jcr:content/root`)節點會定義結果頁面中可用的元件清單。
   * 範本結構中定義的元件無法在任何結果頁面上移動或從中刪除。
   * 在元件解除鎖定後，`editable`屬性設定為`true`。
   * 解鎖已包含內容的元件後，此內容會移至`initial`分支。

* `cq:responsive`節點保留回應式配置的定義。

### 初始內容 {#initial-content}

定義建立新頁面時將具有的初始內容：

* 包含已複製到任何新頁面的`jcr:content`節點。
* 在建立頁面時與結構(`/structure`)合併。
* 如果在建立後變更初始內容，則不會更新任何現有頁面。
* `root`節點儲存元件清單，以定義結果頁面中可用的專案。
* 如果在結構模式下將內容新增到元件，且隨後解鎖該元件（或反之），則此內容會用作初始內容。

### 版面配置 {#layout}

當[編輯範本時，您可以定義配置](/help/sites-cloud/authoring/page-editor/templates.md)，這會使用[標準回應式配置](/help/sites-cloud/administering/responsive-layout.md)，內容作者可以在頁面上對其進行[設定](/help/sites-cloud/authoring/page-editor/responsive-layout.md)。

### 內容原則 {#content-policies}

內容原則會定義元件的設計屬性。 例如，可用的元件或最小/最大尺寸。 這些適用於範本（以及使用範本建立的頁面）。 可在範本編輯器中建立和選取內容原則。

* `cq:policy`節點上的屬性`root`
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
提供頁面段落系統內容原則的相對參照。

* 屬性`cq:policy`位於`root`下的元件明確節點上，提供個別元件原則的連結。

* 實際原則定義儲存在下列位置：
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>原則定義的路徑取決於元件的路徑。 `cq:policy`保留組態本身的相對參照。

### 頁面原則 {#page-policies}

頁面原則可讓您在範本或結果頁面中定義頁面（主要parsys）的[內容原則](#content-policies)。

### 啟用和允許使用範本 {#enabling-and-allowing-a-template-for-use}

1. **啟用範本**

   使用範本之前，必須透過以下任一方式啟用它：

   * [正在從](/help/sites-cloud/authoring/page-editor/templates.md)範本&#x200B;**主控台啟用範本**。

   * 正在設定`jcr:content`節點上的狀態屬性。

      * 例如，在：
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定義屬性：

         * 名稱：狀態
         * 型別：字串
         * 值： `enabled`

1. **允許的範本**

   * [在適當的頁面或子分支的根頁面的&#x200B;**頁面屬性**](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author)&#x200B;上定義允許的範本路徑。
   * 設定屬性：
     `cq:allowedTemplates`
在必要分支的`jcr:content`節點上。

   例如，使用值：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 產生的內容頁面 {#resultant-content-pages}

從可編輯的範本建立的頁面：

* 是以從範本中的`structure`和`initial`合併的子樹狀結構建立

* 具有範本和範本型別中資訊的參考。 這是透過具有下列屬性的`jcr:content`節點實現的：

   * `cq:template` — 提供實際範本的動態參考；讓範本的變更反映在實際頁面上。

   * `cq:templateType` — 提供範本型別的參考。

![範本、內容和元件如何相互關聯](assets/templates-content-components.png)

上圖顯示範本、內容和元件如何相互關聯：

* 控制器 — `/content/<my-site>/<my-page>` — 參考範本的結果頁面。 內容會控制整個流程。 根據定義，它會存取適當的範本和元件。
* 設定 — `/conf/<my-folder>/settings/wcm/templates/<my-template>` - [範本和相關內容原則](#template-definitions)定義頁面設定。
* 模型 — OSGi組合 — [OSGI組合](/help/implementing/deploying/configuring-osgi.md)實作該功能。
* 檢視 — `/apps/<my-site>/components` — 在製作和發佈環境中，內容都是由元件轉譯。

轉譯頁面時：

* **範本**：

   * 已參考其`cq:template`節點的`jcr:content`屬性，以存取對應於該頁面的範本。

* **元件**：

   * 頁面元件會將範本的`structure/jcr:content`樹狀結構與頁面的`jcr:content`樹狀結構合併。
      * 頁面元件將只允許作者編輯已標籤為可編輯的範本結構的節點（以及任何子系）。
      * 在頁面上呈現元件時，會從`jcr:content`節點取得該元件的相對路徑；接著會搜尋範本的`policies/jcr:content`節點下的相同路徑。
         * 此節點的`cq:policy`屬性指向實際內容原則（亦即，它儲存該元件的設計組態）。
            * 這可讓您擁有重複使用相同內容原則設定的多個範本。

### 範本可用性 {#template-availability}

在網站管理員介面中建立頁面時，可用範本清單會根據新頁面的位置及每個範本中指定的版位限制而定。

下列屬性決定是否允許範本`T`用於要放置為頁面`P`子項的新頁面。 這些屬性都是多值字串，其中包含零個或多個用於和路徑比對的規則運算式：

* `cq:allowedTemplates`的`jcr:content`子節點或`P`的上階的`P`屬性。

* `allowedPaths`的`T`屬性。

* `allowedParents`的`T`屬性。

* `allowedChildren`之範本的`P`屬性。

評估的運作方式如下：

* 以`cq:allowedTemplates`開頭的頁面階層遞增時，找到的第一個非空白`P`屬性與`T`的路徑相符。 如果沒有任何相符的值，則會拒絕`T`。

* 如果`T`具有非空白的`allowedPaths`屬性，但沒有符合`P`路徑的值，則會拒絕`T`。

* 如果上述兩個屬性都是空白或不存在，則會拒絕`T`，除非它與`P`屬於相同的應用程式。 當`T`路徑的第二層級名稱與`P`路徑的第二層級名稱相同時，`T`才屬於與`P`相同的應用程式。 例如，範本`/apps/wknd/templates/foo`與頁面`/content/wknd`屬於相同的應用程式。

* 如果`T`具有非空白的`allowedParents`屬性，但沒有符合`P`路徑的值，則會拒絕`T`。

* 如果`P`的範本有非空白的`allowedChildren`屬性，但沒有符合`T`路徑的值，則會拒絕`T`。

* 在所有其他情況下，都允許`T`。

下圖說明範本評估程式：

![範本評估程式](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM提供多個屬性，可控制&#x200B;**網站**&#x200B;下允許的範本。 不過，將它們合併可能會產生非常複雜的規則，而且難以追蹤和管理。
>
>因此，Adobe建議您先定義：
>
>* 僅`cq:allowedTemplates`屬性
>
>* 僅於網站根目錄上
>
>如需範例，請參閱[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)內容： `/content/wknd/jcr:content`
>
>屬性`allowedPaths`、`allowedParents`和`allowedChildren`也可以放在範本上，以定義更複雜的規則。 不過，如果可能的話，如果需要進一步限制允許的範本，在網站的子區段上定義其他&#x200B;*屬性會更簡單*&#x200B;許多`cq:allowedTemplates`。
>
>另一個優點是`cq:allowedTemplates`屬性可由作者在&#x200B;**頁面屬性**&#x200B;的&#x200B;**進階**&#x200B;索引標籤中更新。 無法使用（標準） UI更新其他範本屬性，因此需要開發人員維護規則和每次變更的程式碼部署。

#### 限制子頁面中使用的範本 {#limiting-templates-used-in-child-pages}

若要限制哪些範本可用於在指定頁面下建立子頁面，請使用頁面`cq:allowedTemplates`節點的`jcr:content`屬性，指定允許做為子頁面的範本清單。 清單中的每個值都必須是允許之子頁面的範本的絕對路徑，例如`/apps/wknd/templates/page-content`。

您可以在範本的`cq:allowedTemplates`節點上使用`jcr:content`屬性，將此組態套用至使用此範本的所有已建立頁面。

如果您想要新增更多限制，例如關於範本階層，您可以在範本上使用`allowedParents/allowedChildren`屬性。 然後，您可以明確指定從範本T建立的頁面必須是從範本T建立的頁面的父項/子項。
