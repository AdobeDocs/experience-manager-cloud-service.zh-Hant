---
title: AEMas a Cloud Service的目的地選擇器
description: 使用AEM目的地選擇器來顯示和選取您可以用來作為原始資產副本的資產。
contentOwner: Adobe
feature: destination selector
role: Admin,User
source-git-commit: fc156b95ebbdb0546f9fb334b0cb6f599f5f2692
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 37%

---


# 微前端目的地選擇器 {#Overview}

Micro-Frontend Destination Selector在您的應用程式中提供使用者介面，可輕鬆與 [!DNL Experience Manager Assets as a Cloud Service] 存放庫。 您可以搜尋或瀏覽至內的適當資料夾。 [!DNL Experience Manager Assets as a Cloud Service] 存放庫並從您的應用程式上傳資產。

Micro-Frontend使用者介面可在您的應用程式體驗中使用Destination Selector套件。 套件的任何更新都會自動匯入，而最新部署的目標選擇器會在您的應用程式中自動載入。

![概觀](assets/overview-destination-selector.png)

目的地選擇器提供許多好處，例如：

* 使用 Vanilla JavaScript 程式庫輕鬆整合任何 Adobe 或非 Adobe 應用程式。
* 可輕鬆維護，因為目的地選擇器套件的更新會自動部署至您的應用程式可用的目的地選擇器。 您的應用程式無需更新即可載入最新的修改內容。
* 易於自訂，因為有可用屬性可控制目的地選擇器顯示在應用程式中。
* 全文搜尋可快速導覽至資料夾，以從您的應用程式上傳資產。
* 能夠建立資料夾、以遞增或遞減順序排序資料夾，以及在「清單」、「格線」、「相簿」或「瀑布」檢視中檢視資料夾。

本文的範圍是示範如何使用目的地選擇器搭配 [!DNL Adobe] Unified Shell下的應用程式，或您已針對驗證產生imsToken時。 這些工作流程在本文中稱為非 SUSI 流程。

執行以下工作，將「目的地選擇器」與您的整合和使用 [!DNL Experience Manager Assets as a Cloud Service] 存放庫：

* [使用Vanilla JS整合目的地選擇器](#integration-with-vanilla-js)
* [定義目的地選擇器顯示屬性](#destination-selector-properties)
* [使用目的地選擇器](#using-destination-selector)

## 使用Vanilla JS整合目的地選擇器 {#integration-with-vanilla-js}

您可以整合任何 [!DNL Adobe] 或非 Adobe 應用程式與 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 存放庫，並從應用程式之中選擇資產。

整合是透過匯入Destination Selector套件並使用Vanilla JavaScript程式庫連線至Assets as a Cloud Service來完成。 您必須編輯 `index.html` 或任何應用程式內的適當檔案，以 — 
* 定義身份驗證詳細資訊
* 存取 Assets as a Cloud Service 存放庫
* 設定目的地選擇器顯示屬性

在以下情況下，您可以在不定義某些 IMS 屬性的情況下執行身份驗證：

* 在 [!DNL Adobe] [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=zh-Hant) 之上整合一個應用程式時。
* 您已經具有針對身份驗證產生的一個 IMS 語彙基元。

## 必備條件 {#prerequisites}

在應用程式實作之內定義 `index.html` 檔案或類似檔案的必備條件，以定義存取 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 存放庫的身分驗證資料。必備條件包括：
* imsOrg
* imsToken
* apikey

## 安裝 {#installation}

目的地選擇器可透過兩個ESM CDN使用(例如， [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/))和 [UMD](https://github.com/umdjs/umd) 版本。

在使用 **UMD 版** 的瀏覽器中 (建議)：

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderDestinationSelector } = PureJSSelectors;
</script>
```

在具備 `import maps` 支援並使用 **ESM CDN 版**&#x200B;的瀏覽器中：

```
<script type="module">
  import { DestinationSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

在使用 **ESM CDN 版**&#x200B;的 Deno/Webpack Module Federation 中：

```
import { DestinationSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### 選取的目的地 {#selected-destination}

目的地選擇器會從接收回呼 `onItemSelect`， `onTreeToggleItem`，或 `onTreeSelectionChange` 與包含物件（目錄、影像等）的所選目錄。

**綱要語法**

```
interface SelectedDestination {
  id: string;
  children: SelectedDestination[];
  'repo:repositoryId': string;
  'dc:format': string;
  'repo:assetClass': string;
  'storage:directoryType': string;
  'storage:region': string;
  'repo:name': string;
  'repo:path': string;
  'repo:ancestors': string[];
  'repo:createDate': string;
  'storage:assignee':

  { type: string; id: string; }
  ;
  'repo:assetId': string;
  'aem:published': boolean;
  'repo:createdBy': string;
  'repo:state': string;
  'repo:id': string;
  'repo:modifyDate': string;
  _page:

  { orderBy: string; count: number; };
}
```

下表說明所選目的地的一些重要特性。

| 屬性 | 類型 | 解釋 |
|---|---|---|
| *repo:repositoryId* | 字串 | 儲存資產之存放庫的唯一識別碼。 |
| *repo:id* | 字串 | 資產的唯一識別碼。 |
| *repo:assetClass* | 字串 | 資產的分類 (例如影像或影片、文件)。 |
| *repo:name* | 字串 | 資產的名稱，包括檔案副檔名。 |
| *repo:size* | 數字 | 資產的大小，以位元組計。 |
| *repo:path* | 字串 | 資產在存放庫中的位置。 |
| *repo:ancestors* | `Array<string>` | 存放庫中資產的上階項目陣列。 |
| *repo:state* | 字串 | 存放庫中資產的目前狀態 (例如使用中、已刪除等)。 |
| *repo:createdBy* | 字串 | 建立資產的使用者或系統。 |
| *repo:createDate* | 字串 | 建立資產的日期與時間。 |
| *repo:modifiedBy* | 字串 | 上次修改資產的使用者或系統。 |
| *repo:modifyDate* | 字串 | 上次修改資產的日期和時間。 |
| *dc:format* | 字串 | 資產的格式。 |
| *_頁面* | orderBy： string； count： number； | 包含檔案的頁碼。 |

如需屬性的完整清單和詳細範例，請造訪 [目的地選擇器程式碼範例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

### 非 SUSI 流程的範例 {#non-ims-vanilla}

此範例示範如何在執行時搭配非SUSI流程使用目的地選擇器。 [!DNL Adobe] Unified Shell下的應用程式，或當您已 `imsToken` 產生以進行驗證。

使用以下專案在您的程式碼中加入Destination Selector套件 `script` 標籤，如所示 _第6行至第15行_ 範例中的。 在載入指令碼後，即可使用 `PureJSSelectors` 全域變數。定義目的地選擇器 [屬性](#destination-selector-properties) 如所示 _第16到23行_. 在非 SUSI 流程執行身份驗證需要 `imsOrg` 和 `imsToken` 屬性。`handleSelection` 屬性用於處理選取的資產。若要轉譯目的地選擇器，請呼叫 `renderDestinationSelector` 中提及的函式 _第17行_. 目的地選擇器會顯示在 `<div>` 容器元素，如所示 _第21行和第22行_.

按照以下步驟操作，您可以在中使用非SUSI流程的目標選擇器 [!DNL Adobe] 應用程式。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Destination Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the DestinationSelector component
        const container = document.getElementById('destination-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
        const destinationSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderDestinationSelector` available in PureJSSelectors globals to render DestinationSelector
        PureJSSelectors.renderDestinationSelector(container, destinationselectorprops);
    </script>
</head>

<body>
    <div id="destination-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

如需詳細資訊，請造訪 [目的地選擇器程式碼範例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

## 使用目的地選擇器屬性 {#destination-selector-properties}

您可以使用「目的地選擇器」屬性來自訂「目的地選擇器」的呈現方式。 下表列出您可以用來自訂及使用「目的地選擇器」的屬性：

| 屬性 | 類型 | 必要 | 預設 | 說明 |
|---|---|---|---|---|
| *imsOrg* | 字串 | 是 |  | Adobe Identity Management System (IMS) ID 是在為您的組織佈建 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 時所指派的。不管您所存取的組織是否在 Adobe IMS 之下，都需要 `imsOrg` 金鑰進行身分驗證。 |
| *imsToken* | 字串 | 否 |  | 用於身份驗證的 IMS 持有人語彙基元。`imsToken` 如果您使用SUSI流程，則不需要使用。 不過，如果您使用非SUSI流程，則需要使用。 |
| *apiKey* | 字串 | 否 |  | 用於存取 AEM Discovery 服務的 API 金鑰。`apiKey` 如果您使用SUSI流程，則不需要使用。 但是，在非SUSI流程中需要它。 |
| *rootPath* | 字串 | 否 | /content/dam/ | 目的地選擇器顯示資產的資料夾路徑。 `rootPath` 也可以使用封裝形式。例如，假定路徑如下， `/content/dam/marketing/subfolder/`，目的地選擇器不允許您周遊任何父資料夾，但只會顯示子資料夾。 |
| *hasMore* | 布林值 | 否 |  | 當應用程式有更多可顯示的內容時，您可以使用此屬性來新增載入內容的載入器，使內容在應用程式中可見。 這是指出正在載入內容的指標。 |
| *orgName* | 布林值 | 否 |  | 這是與AEM相關聯之組織（可能是orgID）的名稱 |
| *initRepoID* | 字串 | 否 |  | 這是您要在預設初始檢視中使用的資產存放庫的路徑 |
| *onCreateFolder* | 字串 | 否 |  | 此 `onCreateFolder` 屬性可讓您新增圖示，在應用程式中新增資料夾。 |
| *onConfirm* | 字串 | 否 |  | 這是您按下「確認」按鈕時的回呼。 |
| *confirmDisabled* | 字串 | 否 |  | 此屬性可控制確認按鈕的切換。 |
| *viewType* | 字串 | 否 |  | 此 `viewType` 屬性用於指定用來顯示資產的檢視。 |
| *viewTypeOptions* | 字串 | 否 |  | 此屬性與 `viewType` 屬性。 您可以指定一或多個檢視來顯示資產。 可用的viewTypeOptions包括：「清單」檢視、「格點」檢視、「庫」檢視、「瀑布」檢視和「樹」檢視。 |
| *itemNameFormatter* | 字串 | 否 |  | 此屬性可讓您格式化專案名稱 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |  | 如果 OOTB 翻譯不足以滿足應用程式的需求，您可以公開一個介面，並透過 `i18nSymbols`prop 傳遞您自訂的本地化數值。透過此介面傳遞的值會覆寫已提供的預設翻譯，並改為使用您自己的翻譯。若要執行覆寫，您必須傳遞一個有效的 [Message Descriptor](https://formatjs.io/docs/react-intl/api/#message-descriptor) 物件至您想要覆寫的 `i18nSymbols` 金鑰。 |
| *inlineAlertSetup* | 字串 | 否 |  | 它會新增您要在應用程式中傳遞的警示訊息。 例如，新增您無權存取此資料夾的警示訊息。 |
| *intl* | 物件 | 否 |  | 目的地選擇器提供預設的OOTB翻譯。 您可以透過 `intl.locale`prop 提供有效的語言環境字串，以選擇翻譯語言。例如：`intl={{ locale: "es-es" }}`</br></br>支援的語言環境字串遵循 [ISO 639 - 代碼](https://www.iso.org/iso-639-language-codes.html)來選擇代表語言標準名稱的代碼。</br></br>支援的語言環境清單：英文 - &#39;en-us&#39; (預設) 西班牙文 - &#39;es-es&#39; 德文 - &#39;de-de&#39; 法文 - &#39;fr-fr&#39; 義大利文 - &#39;it-it&#39; 日文 - &#39;ja-jp&#39;韓文 - &#39;ko-kr&#39; 葡萄牙文 - &#39;pt-br&#39; 中文 (繁體)- &#39;zh-cn&#39; 中文 (台灣) - &#39;zh-tw&#39; |

## 使用目的地選擇器屬性的範例 {#usage-examples}

您可以定義目的地選擇器 [屬性](#destination-selector-properties) 在 `index.html` 檔案以自訂目的地選擇器在您應用程式中的顯示。

### 範例1：在目的地選擇器中建立資料夾

目的地選擇器可讓您建立新資料夾，以上傳、移動或複製特定位置的資產。

![create-folder-destination-selector](assets/create-folder-destination-selector.png)

### 範例2：指定目的地選擇器的檢視型別

「目的地選擇器」會以四種不同的檢視顯示廣泛的資產陣列，包括清單檢視、格線檢視、相簿檢視和瀑布檢視。 若要指定預設檢視型別，您可以使用 `viewType` 屬性。 此 `viewTypeOptions` 屬性會與 `viewType` 屬性來指定其他檢視型別，以便其他檢視型別選項可顯示在下拉式清單中。 如果您只想顯示一個選項，可以使用單一引數。

![viewtype-destination-selector](assets/viewtype-destination-selector.png)

### 範例3：初始化資產資料夾的路徑

使用 `path` 屬性，定義在轉譯目的地選擇器時自動顯示的資料夾名稱。

![initialize-folder-path](assets/initialize-folder-path.png)

## 使用目的地選擇器 {#using-destination-selector}

在設定目的地選擇器並驗證您同意搭配使用目的地選擇器後， [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 應用程式，您可以選取資產或執行各種其他操作，以在存放庫中搜尋您的資產。

![using-destination-selector](assets/using-destination-selector.png)

* **A**： [搜尋列](#search-bar)
* **B**： [排序](#sorting)
* **C**：[資產](#assets-repo)
* **D**： [新增字尾或首碼](#add-suffix-or-prefix)
* **E**： [建立新資料夾](#create-new-folder)
* **F**： [檢視](#types-of-view)
* **G**： [資訊](#info)
* **H**： [選取資料夾](#select-folder)

### 搜尋列 {#search-bar}

目的地選擇器可讓您對所選存放庫內的資產執行全文搜尋。 例如，如果您在搜尋列中鍵入關鍵字 `wave`，就會顯示中繼資料屬性中提及 `wave` 關鍵字的所有資產。

### 排序 {#sorting}

您可以在「目的地選擇器」中依資產名稱、維度或大小來排序資產。 您可以依照遞增或遞減順序排序資產。

### 資產存放庫 {#assets-repo}

目的地選擇器也可讓您檢視AEM應用程式中選擇的存放庫資料。 您可以使用 `repositoryID` 屬性，初始化您要在「目的地選取器」的第一個執行個體檢視的目的地資料夾路徑。

### 新增字尾或首碼 {#add-suffix-or-prefix}

以下範例說明 `optionsFormSetup` 屬性。 您可以使用它來確認選取範圍，它傳遞至 `onConfirm` 事件。

### 建立新資料夾 {#create-new-folder}

它可讓您在的目的地資料夾中建立新資料夾 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].

### 視圖的類型 {#types-of-view}

目的地選擇器可讓您以四種不同的檢視檢視資產：

* **![清單檢視](assets/do-not-localize/list-view.png)[!UICONTROL 清單檢視]**：清單檢視在單一欄中顯示可捲動的檔案和資料夾。
* **![網格檢視](assets/do-not-localize/grid-view.png)[!UICONTROL 網格檢視]**：網格檢視圖在列與欄的網格中顯示可捲動的檔案和資料夾。
* **![圖庫檢視](assets/do-not-localize/gallery-view.png)[!UICONTROL 圖庫檢視]**：圖庫檢視在居中鎖定的水平清單中顯示檔案或資料夾。
* **![瀑布檢視](assets/do-not-localize/waterfall-view.png)[!UICONTROL 瀑布檢視]**：瀑布檢視以 Bridge 的形式顯示檔案或資料夾。

### 資訊 {#info}

資訊或資訊圖示可讓您檢視所選資產的中繼資料。 其中包含各種細節，例如維度、大小、說明、路徑、修改日期和建立日期。 中繼資料資訊是在上傳、複製或建立新資產時提供。

### 選取檔案夾 {#select-folder}

「選取資料夾」按鈕可讓您選取資產，以執行與相關的各種操作 [屬性](#destination-selector-properties) 在目的地選擇器上。