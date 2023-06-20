---
title: 適用於  [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service] 的資產選擇器
description: 在應用程式內使用資產選擇器搜尋、查找和檢索資產的中繼資料和轉譯。
contentOwner: Adobe
role: Admin,User
exl-id: b968f63d-99df-4ec6-a9c9-ddb77610e258
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2376'
ht-degree: 99%

---

# 微前端資產選擇器 {#Overview}

微前端資產選擇器提供一個輕鬆整合 [!DNL Experience Manager Assets as a Cloud Service] 存放庫的使用者介面，讓您可以瀏覽或搜尋存放庫中的可用數位資產，並用於您的應用程式編寫體驗。

在您的應用程式體驗中可利用資產選擇器套件使用微前端使用者介面。套件的任何更新都會自動匯入，而最新部署的資產選擇器會自動載入到您的應用程式。

![概觀](assets/overview.png)

資產選擇器提供了許多優點，例如：

* 使用 Vanilla JavaScript 程式庫輕鬆整合任何 Adobe 或非 Adobe 應用程式。
* 容易維護，因為資產選擇器套件的更新會自動部署到您的應用程式可用的資產選擇器。您的應用程式無需更新即可載入最新的修改內容。
* 簡易的自訂功能，因為有可以控制應用程式中資產選擇器顯示的可用屬性。

* 全文搜尋、開箱即用和自訂篩選器，可快速找到要在編寫體驗中使用的資產。

* 能夠在 IMS 組織內切換存放庫以選擇資產。

* 能夠按名稱、維度和大小對資產進行排序，並以清單、網格、圖庫或瀑布視圖檢視。

本文的範圍是示範在 Unified Shell 之下有 [!DNL Adobe] 應用程式或者已經產生用於身份驗證的 imsToken 的情況下，如何使用資產選擇器。這些工作流程在本文中稱為非 SUSI 流程。

執行以下任務，以便搭配 [!DNL Experience Manager Assets as a Cloud Service] 存放庫來整合與使用資產選擇器：

* [使用 Vanilla JS 整合資產選擇器](#integration-with-vanilla-js)
* [定義資產選擇器顯示屬性](#asset-selector-properties)
* [使用資產選擇器](#using-asset-selector)

## 使用 Vanilla JS 整合資產選擇器 {#integration-with-vanilla-js}

您可以整合任何 [!DNL Adobe] 或非 Adobe 應用程式與 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 存放庫，並從應用程式之中選擇資產。

匯入資產選擇器套件，並使用 Vanilla JavaScript 程式庫連接到 Assets as a Cloud Service，便完成了整合作業。您必須在應用程式內編輯一個 `index.html` 或任何適當的文件，以利 -
* 定義身份驗證詳細資訊
* 存取 Assets as a Cloud Service 存放庫
* 設定資產選擇器顯示屬性

<!--
Asset Selector supports authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS) properties such as `imsScope` or `imsClientID`. Authentication using these IMS properties is referred to as SUSI (Sign Up Sign In) flow in this article.

You can perform authentication without defining some of the IMS properties, such as `imsScope` or `imsClientID`, if:

*   You are integrating an [!DNL Adobe] application on [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
*   You already have an IMS token generated for authentication.

Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining `imsScope` or `imsClientID` IMS properties is referred to as a non-SUSI flow in this article.
-->

在以下情況下，您可以在不定義某些 IMS 屬性的情況下執行身份驗證：

* 在 [!DNL Adobe] [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=zh-Hant) 之上整合一個應用程式時。
* 您已經具有針對身份驗證產生的一個 IMS 語彙基元。

## 必備條件 {#prerequisites}

<!--
If your application requires user based authentication, out-of-the-box Asset Selector also supports a flow for authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS.)

You can use properties such as `imsScope` or `imsClientID` to retrieve `imsToken` automatically. You can use SUSI (Sign Up Sign In) flow and IMS properties. Also, you can obtain your own imsToken and pass it to Asset Selector by integrating within [!DNL Adobe] application on Unified Shell or if you already have an imsToken obtained via other methods (for example, using technical account). Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining IMS properties (For example, `imsScope` and `imsClientID`) is referred to as a non-SUSI flow.
-->

在應用程式實作之內定義 `index.html` 檔案或類似檔案的必備條件，以定義存取 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 存放庫的身分驗證資料。必備條件包括：
* imsOrg
* imsToken
* apikey
<!--
The prerequisites vary if you are authenticating using a SUSI flow or a non-SUSI flow.

**Non-SUSI flow**

*   imsOrg
*   imsToken
*   apikey

For more information on these properties, refer to [Asset Selector Properties](#asset-selector-properties).

**SUSI flow**

*   imsClientId
*   imsScope
*   redirectUrl
*   imsOrg
*   apikey

For more information on these properties, refer to [Example for the SUSI flow](#susi-vanilla) and [Asset Selector Properties](#asset-selector-properties).
-->

## 安裝 {#installation}

ESM CDN (例如，[esm.sh](https://esm.sh/) /[skypack](https://www.skypack.dev/)) 和 [UMD](https://github.com/umdjs/umd) 版本均可使用資產選擇器。

在使用 **UMD 版** 的瀏覽器中 (建議)：

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

在具備 `import maps` 支援並使用 **ESM CDN 版**&#x200B;的瀏覽器中：

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

在使用 **ESM CDN 版**&#x200B;的 Deno/Webpack Module Federation 中：

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### 選取的資產類型 {#selected-asset-type}

選取的資產類型是一個物件陣列，包含使用 `handleSelection`、`handleAssetSelection` 和 `onDrop` 函數時的資產資訊。

**綱要語法**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

下表說明選取之資產物件的一些重要屬性。

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
| *dc:format* | 字串 | 資產的格式，例如檔案類型 (例如 JPEG、PNG 等)。 |
| *tiff:imageWidth* | 數字 | 資產的寬度。 |
| *tiff:imageLength* | 數字 | 資產的高度。 |
| *computedMetadata* | `Record<string, any>` | 代表貯體的一個物件，可存放各種類型之所有資產中繼資料 (存放庫、應用程式或嵌入式中繼資料)。 |
| *_links* | `Record<string, any>` | 相關資產的超媒體連結。包括中繼資料和轉譯等資源的連結。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition* | `Array<Object>` | 包含有關資產轉譯資訊的物件陣列。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].href* | 字串 | 轉譯的 URI。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].type* | 字串 | 轉譯的 MIME 類型。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].&#39;repo:size&#39;* | 數字 | 轉譯的大小，以位元組計。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].width* | 數字 | 轉譯的寬度。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].height* | 數字 | 轉譯的高度。 |

如需完整的屬性清單和詳細範例，請造訪[資產選擇器代碼範例 ](https://github.com/adobe/aem-assets-selectors-mfe-examples)。

<!--
### ImsAuthProps {#ims-auth-props}

The `ImsAuthProps` properties define the authentication information and flow that the Asset Selector uses to obtain an `imsToken`. By setting these properties, you can control how the authentication flow should behave and register listeners for various authentication events.

| Property Name | Description|
|---|---|
| `imsClientId`| A string value representing the IMS client ID used for authentication purposes. This value is provided by Adobe and is specific to your Adobe AEM CS organization.|
| `imsScope`| Describes the scopes used in authentication. The scopes determine the level of access that the application has to your organization resources. Multiple scopes can be separated by commas.|
| `redirectUrl` | Represents the URL where the user is redirected after authentication. This value is typically set to the current URL of the application. If a `redirectUrl` is not supplied, `ImsAuthService` will use the redirectUrl used to register the `imsClientId`|
| `modalMode`| A boolean indicating whether the authentication flow should be displayed in a modal (pop-up) or not. If set to `true`, the authentication flow is displayed in a pop-up. If set to `false`, the authentication flow is displayed in a full page reload. _Note:_ for better UX, you can dynamically control this value if the user has browser pop-up disabled. |
| `onImsServiceInitialized`| A callback function that is called when the Adobe IMS authentication service is initialized. This function takes one parameter, `service`, which is an object representing the Adobe IMS service. See [`ImsAuthService`](#imsauthservice-ims-auth-service) for more details.|
| `onAccessTokenReceived`| A callback function that is called when an `imsToken` is received from the Adobe IMS authentication service. This function takes one parameter, `imsToken`, which is a string representing the access token. |
| `onAccessTokenExpired`| A callback function that is called when an access token has expired. This function is typically used to trigger a new authentication flow to obtain a new access token. |
| `onErrorReceived`| A callback function that is called when an error occurs during authentication. This function takes two parameters: the error type and error message. The error type is a string representing the type of error and the error message is a string representing the error message. |

### ImsAuthService {#ims-auth-service}

`ImsAuthService` class handles the authentication flow for the Asset Selector. It is responsible for obtaining an `imsToken` from the Adobe IMS authentication service. The `imsToken` is used to authenticate the user and authorize access to the Adobe Experience Manager (AEM) CS Assets repository. ImsAuthService uses the `ImsAuthProps` properties to control the authentication flow and register listeners for various authentication events. You can use the convenient [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) function to register the _ImsAuthService_ instance with the Asset Selector. The following functions are available on the `ImsAuthService` class. However, if you're using the _registerAssetsSelectorsAuthService_ function, you do not need to call these functions directly.

| Function Name | Description |
|---|---|
| `isSignedInUser` | Determines whether the user is currently signed in to the service and returns a boolean value accordingly.|
| `getImsToken`    | Retrieves the authentication `imsToken` for the currently signed-in user, which can be used to authenticate requests to other services such as generating asset _rendition.|
| `signIn`| Initiates the sign-in process for the user. This function uses the `ImsAuthProps` to show authentication in either a pop-up or a full page reload |
| `signOut`| Signs the user out of the service, invalidating their authentication token and requiring them to sign in again to access protected resources. Invoking this function will reload the current page.|
| `refreshToken`| Refreshes the authentication token for the currently signed-in user, preventing it from expiring and ensuring uninterrupted access to protected resources. Returns a new authentication token that can be used for subsequent requests. |
-->

### 非 SUSI 流程的範例 {#non-susi-vanilla}

本範例示範在 Unified Shell 之下執行 [!DNL Adobe] 應用程式時，或者在已經產生用於身份驗證的 `imsToken` 時，如何搭配非 SUSI 流程使用資產選擇器。

使用`script`標記在代碼中納入資產選擇器套件，如以下範例的 _第 6 至 15 行_ 所示。在載入指令碼後，即可使用 `PureJSSelectors` 全域變數。定義資產選擇器[屬性](#asset-selector-properties)，如 _第 16 至 23 行_ 所示。在非 SUSI 流程執行身份驗證需要 `imsOrg` 和 `imsToken` 屬性。`handleSelection` 屬性用於處理選取的資產。要轉譯資產選擇器，請呼叫 `renderAssetSelector` 函數，如&#x200B;_第 17 行_&#x200B;所述。資產選擇器顯示於 `<div>` 容器元素，如&#x200B;_第 21 和 22 行_&#x200B;所示。

透過執行這些步驟，您可以在您的 [!DNL Adobe] 應用程式中，以非 SUSI 流程使用資產選擇器。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
        const assetSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderAssetSelector` available in PureJSSelectors globals to render AssetSelector
        PureJSSelectors.renderAssetSelector(container, assetSelectorProps);
    </script>
</head>

<body>
    <div id="asset-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

有關詳細的範例，請造訪[資產選擇器代碼範例 ](https://github.com/adobe/aem-assets-selectors-mfe-examples)。

<!--
### Example for the SUSI flow {#susi-vanilla}

Use this example `index.html` file for authentication if you are integrating your application using SUSI flow.

Access the Asset Selector package using the `Script` Tag, as shown in *line 9* to *line 11* of the example `index.html` file.

*Line 14* to *line 38* of the example describes the IMS flow properties, such as `imsClientId`, `imsScope`, and `redirectURL`. The function requires that you define at least one of the `imsClientId` and `imsScope` properties. If you do not define a value for `redirectURL`, the registered redirect URL for the client ID is used.

As you do not have an `imsToken` generated, use the `registerAssetsSelectorsAuthService` and `renderAssetSelectorWithAuthFlow` functions, as shown in line 40 to line 50 of the example `index.html` file. Use the `registerAssetsSelectorsAuthService` function before `renderAssetSelectorWithAuthFlow` to register the `imsToken` with the Asset Selector. [!DNL Adobe] recommends to call `registerAssetsSelectorsAuthService` when you instantiate the component.

Define the authentication and other Assets as a Cloud Service access-related properties in the `const props` section, as shown in *line 54* to *line 60* of the example `index.html` file.

The `PureJSSelectors` global variable, mentioned in *line 65*, is used to render the Asset Selector in the web browser.

Asset Selector is rendered on the `<div>` container element, as mentioned in *line 74* to *line 81*. The example uses a dialog to display the Asset Selector.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8">
    <title>Asset Selectors</title>
    <link rel="stylesheet" href="index.css">
    <script id="asset-selector"
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/asset-selectors.js"></script>
    <script>

        const imsProps = {
            imsClientId: "<obtained from IMS team>",
            imsScope: "openid, <other scopes>",
            redirectUrl: window.location.href,
            modalMode: true, // false to open in a full page reload flow
            onImsServiceInitialized: (service) => {
                // invoked when the ims service is initialized and is ready
                console.log("onImsServiceInitialized", service);
            },
            onAccessTokenReceived: (token) => {
                console.log("onAccessTokenReceived", token);
            },
            onAccessTokenExpired: () => {
                console.log("onAccessTokenError");
                // re-trigger sign-in flow
            },
            onErrorReceived: (type, msg) => {
                console.log("onErrorReceived", type, msg);
            },
        }

        function load() {
            const registeredTokenService = PureJSSelectors.registerAssetsSelectorsAuthService(imsProps);
            imsInstance = registeredTokenService;
        };

        // initialize the IMS flow before attempting to render the asset selector
        load();
        

        //function that will render the asset selector
            const otherProps = {
            // any other props supported by asset selector
            }
            const assetSelectorProps = {
                "imsOrg": "imsorg",
                ...otherProps
            }
             // container element on which you want to render the AssetSelector/DestinationSelector component
            const container = document.getElementById('asset-selector');

            /// Use the PureJSSelectors in globals to render the AssetSelector/DestinationSelector component
            PureJSSelectors.renderAssetSelectorWithAuthFlow(container, assetSelectorProps, () => {
                const assetSelectorDialog = document.getElementById('asset-selector-dialog');
                assetSelectorDialog.showModal();
            });
        }
    </script>

</head>
<body class="asset-selectors">
    <div>
        <button onclick="renderAssetSelectorWithAuthFlowFlow()">Asset Selector - Select Assets with Ims Flow</button>
    </div>
        <dialog id="asset-selector-dialog">
            <div id="asset-selector" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
            </div>
        </dialog>
    </div>
</body>

</html>

```
-->

## 使用資產選擇器屬性 {#asset-selector-properties}

您可以使用資產選擇器屬性自訂資產選擇器的呈現方式。下表列出可用於自訂和使用資產選擇器的屬性。

| 屬性 | 類型 | 必要 | 預設 | 說明 |
|---|---|---|---|---|
| *rail* | 布林值 | 否 | false | 若已標籤 `true`，資產選擇器會呈現在左側欄檢視中。 如果已標示 `false`，資產選擇器會在強制回應檢視中呈現。 |
| *imsOrg* | 字串 | 是 | | Adobe Identity Management System (IMS) ID 是在為您的組織佈建 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 時所指派的。不管您所存取的組織是否在 Adobe IMS 之下，都需要 `imsOrg` 金鑰進行身分驗證。 |
| *imsToken* | 字串 | 否 | | 用於身份驗證的 IMS 持有人語彙基元。如果您使用的是非 SUSI 流程，則需要 `imsToken`。 |
| *apiKey* | 字串 | 否 | | 用於存取 AEM Discovery 服務的 API 金鑰。如果您使用的是非 SUSI 流程，則需要 `apiKey`。 |
| *rootPath* | 字串 | 否 | /content/dam/ | 資產選擇器顯示資產的資料夾路徑。`rootPath` 也可以使用封裝形式。例如指定以下路徑，`/content/dam/marketing/subfolder/`，資產管理器不允許您穿越任何父系資料夾，而只顯示子系資料夾。 |
| *path* | 字串 | 否 | | 在呈現資產選擇器時，用於導覽到特定資產目錄的路徑。 |
| *filterSchema* | 陣列 | 否 | | 用於設定篩選器屬性的模式。這可用於想要限制資產選擇器中的特定篩選器選項時。 |
| *filterFormProps* | 物件 | 否 | | 指定用於調整搜尋所需的篩選器屬性。例如，MIME 類型 JPG、PNG、GIF。 |
| *selectedAssets* | 陣列 `<Object>` | 否 |                 | 呈現資產選擇器時指定選取的資產。需要包含資產的 id 屬性的物件陣列。例如，在目前的目錄中必須可以使用 `[{id: 'urn:234}, {id: 'urn:555'}]` 資產。如果您需要使用不同的目錄，請為該 `path` 屬性提供一個值。 |
| *acvConfig* | 物件 | 否 | | 資產集合視圖屬性包含的物件含有用於覆寫預設值的自訂設定。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |                 | 如果 OOTB 翻譯不足以滿足應用程式的需求，您可以公開一個介面，並透過 `i18nSymbols`prop 傳遞您自訂的本地化數值。透過此介面傳遞的值會覆寫已提供的預設翻譯，並改為使用您自己的翻譯。若要執行覆寫，您必須傳遞一個有效的 [Message Descriptor](https://formatjs.io/docs/react-intl/api/#message-descriptor) 物件至您想要覆寫的 `i18nSymbols` 金鑰。 |
| *intl* | 物件 | 否 | | 資產選擇器提供預設的 OOTB 翻譯。您可以透過 `intl.locale`prop 提供有效的語言環境字串，以選擇翻譯語言。例如：`intl={{ locale: "es-es" }}`</br></br>支援的語言環境字串遵循 [ISO 639 - 代碼](https://www.iso.org/iso-639-language-codes.html)來選擇代表語言標準名稱的代碼。</br></br>支援的語言環境清單：英文 - &#39;en-us&#39; (預設) 西班牙文 - &#39;es-es&#39; 德文 - &#39;de-de&#39; 法文 - &#39;fr-fr&#39; 義大利文 - &#39;it-it&#39; 日文 - &#39;ja-jp&#39;韓文 - &#39;ko-kr&#39; 葡萄牙文 - &#39;pt-br&#39; 中文 (繁體)- &#39;zh-cn&#39; 中文 (台灣) - &#39;zh-tw&#39; |
| *repositoryId* | 字串 | 否 | &#39;&#39; | 資產選擇器從中載入內容的存放庫。 |
| *additionalAemSolutions* | `Array<string>` | 否 | [ ] | 允許您新增其他的 AEM 存放庫清單。如果此屬性未提供任何資訊，則僅考慮媒體資料庫或 AEM Assets 存放庫。 |
| *hideTreeNav* | 布林值 | 否 |  | 指定顯示或隱藏資產樹導覽側邊欄。那僅用於模組視圖，因此，此屬性在邊欄視圖中沒有影響。 |
| *onDrop* | 函數 | 否 | | 該屬性允許資產的放置功能。 |
| *dropOptions* | `{allowList?: Object}` | 否 | | 使用 &#39;allowList&#39; 設定放置選項。 |
| *colorScheme* | 字串 | 否 | | 為資產選擇器設定主題 (`light`或者`dark`)。 |
| *handleSelection* | 函數 | 否 | | 在選取資產並按一下`Select`模組上的按鈕時，叫用資產項目陣列。此函數僅在模組視圖中叫用。對於邊欄視圖，請使用 `handleAssetSelection`或`onDrop` 函數。範例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 查看[選取的資產類型](#selected-asset-type)以了解詳細資訊。 |
| *handleAssetSelection* | 函數 | 否 | | 在選擇或取消選擇資產時，以項目陣列叫用。當您想要在使用者選擇資產時進行監聽，這是十分實用的功能。範例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 查看[選取的資產類型](#selected-asset-type)以了解詳細資訊。 |
| *onClose* | 函數 | 否 | | 在按下`Close`模組視圖中的按鈕時叫用。這只在`modal`視圖中呼叫，而在`rail`視圖中忽略。 |
| *onFilterSubmit* | 函數 | 否 | | 當使用者變更不同的篩選條件時，以篩選項目叫用。 |
| *selectionType* | 字串 | 否 | single | 一次設定`single`或`multiple`資產選擇方式。 |

## 使用資產選擇器屬性的範例 {#usage-examples}

您可以定義 `index.html` 檔案裡的資產選擇器[屬性](#asset-selector-properties)，以便自訂在應用程式內的資產選擇器顯示。

### 範例 1：邊欄視圖中的資產選擇器

![rail-view-example](assets/rail-view-example-vanilla.png)

如果 AssetSelector 的值 `rail` 設定為 `false` 或屬性中未提及，資產選擇器依預設顯示於模組視圖中。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### 範例 2：中繼資料彈出視窗

使用各種屬性定義您要使用資訊圖示檢視的資產中繼資料。資訊彈出視窗提供有關資產或資料夾的資訊集合，包括資產的標題、尺寸、修改日期、位置和說明。在下面的範例中，各種屬性用於顯示資產的中繼資料，例如，`repo:path`屬性指定資產的位置<!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->。

![metadata-popover-example](assets/metadata-popover.png)


### 範例 3：邊欄視圖中的自訂篩選器屬性

除了多面搜尋，資產選擇器讓您自訂各種屬性，讓您在 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 應用程式的搜尋更精準。您必須新增以下代碼，以便在應用程式中新增自訂搜尋篩選器。在下面的範例中，`Type Filter`在影像、文件或影片中篩選資產類型，或為搜尋新增篩選器類型的搜尋。

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

<!-- Property details to be added here. Referred the ticket https://jira.corp.adobe.com/browse/ASSETS-19023-->

<!--
## Asset Selector Object Schema {#object-schema}

Schema describes the object properties associated with an asset selected using Asset Selector. It uses the combination of data types and their values to validate the object describing the selected Asset using an Asset Selector.

**Schema Syntax**
````
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
````

**Query Parameters**

| Parameter | Type | Description |
|---|---|---|
| repo:id | string | ID of an Asset |
| repo:name | string | The name of an Asset |
| repo:path | string | The path of an Asset |
| repo:size | number | Size of an Asset (in bytes) |
| repo:createdBy | string | ID of a user who created an Asset |
| repo: createdDate | string | The timestamp when an asset was created |
| repo:modifiedBy | string | ID of a user who modified the asset recently |
| repo:modifyDate | string | The timestamp when the asset was last modified |
| dc:format | string | MIME type of an Asset |
| tiff:imageWidth | number | The width of an image type of Asset |
| tiff:imageLength | number | The height of an image type of Asset |
| repo:state | string | The `Approved`, `Rejected`, or `Expired`state of an Asset |
| computedMetadata | string | It is an object that represents a bucket for all the Asset's metadata of all kinds (repository, application or embedded metadata) |
| _links | string | It represents the collection of links used in the Asset Selector. The links are represented in the form of an array. The parameters of an array include: `href`, `type`, `repo:size`, `width`, `height`, etc.  |

For the detailed example of Object Schema, click 
-->

## 使用物件綱要處理資產選擇 {#handling-selection}

`handleSelection` 屬性用於處理資產選擇器中單個或多個資產選擇。下面的範例說明使用 `handleSelection` 的語法。

![handle-selection](assets/handling-selection.png)

## 使用資產選擇器 {#using-asset-selector}

在資產選擇器設定完成後，且您以 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 應用程式使用資產選擇器完成身分驗證，則您可以選擇資產或執行各種其他操作，以便在存放庫中搜尋您的資產。

![using-asset-selector](assets/using-asset-selector.png)

* **A**：[隱藏/顯示面板](#hide-show-panel)
* **B**：[存放庫切換器](#repository-switcher)
* **C**：[資產](#repository)
* **D**：[篩選器](#filters)
* **E**：[搜尋列](#search-bar)
* **F**：[排序](#sorting)
* **G**：[按遞增或遞減順序排序](#sorting)
* **H**：[視圖](#types-of-view)

### 隱藏/顯示面板 {#hide-show-panel}

若要將資料夾隱藏在左側導覽中，請按一下&#x200B;**[!UICONTROL 隱藏資料夾]**&#x200B;圖示。要還原變更，請再按一下&#x200B;**[!UICONTROL 隱藏資料夾]**&#x200B;圖示。

### 存放庫切換器 {#repository-switcher}

資產選擇器讓您可以切換存放庫，以進行資產選擇。您可以從左側面板中的下拉清單中選擇您要的存放庫。下拉清單中可用的存放庫選項是根據`repositoryId``index.html`檔案中定義的屬性。那是根據於登入的使用者從選取的 IMS org 所存取的環境。消費者可以傳遞一個偏好的`repositoryID`，而且在該情況下，資產選擇器將停止呈現 repo 切換器，並僅從指定的存放庫呈現資產。
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### 資產存放庫

那是可用於執行操作的資產資料夾集合。

### 現成可用篩選器 {#filters}

資產選擇器也提供現成可用的篩選器選項，以調整您的搜尋結果。您可以使用以下篩選器：

* `File type`：包括資料夾、檔案、影像、文件或影片
* `MIME type`：包括 JPG、GIF、PPTX、PNG、MP4、DOCX、TIFF、PDF、XLSX
* `Image Size`：包括影像的最小/最大寬度，最小/最大高度

![rail-view-example](assets/filters-asset-selector.png)

### 自訂搜尋

除了全文搜尋外，資產選擇器也讓您使用自訂搜尋以搜尋檔案中的資產。您可以在模組視圖和邊欄視圖模式下，使用自訂搜尋篩選器。

![custom-search](assets/custom-search.png)

您也可以建立預設的搜尋篩選器，以儲存您經常搜尋的欄位，以供之後使用。若要為資產建立自訂搜尋，您可以使用 `filterSchema` 屬性。

### 搜尋列 {#search-bar}

資產選擇器讓您可以在選取的存放庫中執行資產的全文搜尋。例如，如果您在搜尋列中鍵入關鍵字 `wave`，就會顯示中繼資料屬性中提及 `wave` 關鍵字的所有資產。

### 排序 {#sorting}

您可以按資產的名稱、維度或大小對資產選擇器中的資產進行排序。您可以依照遞增或遞減順序排序資產。

### 視圖的類型 {#types-of-view}

資產選擇器讓您在四種不同的視圖中檢視資產：

* **![清單檢視](assets/do-not-localize/list-view.png)[!UICONTROL 清單檢視]**：清單檢視在單一欄中顯示可捲動的檔案和資料夾。
* **![格線檢視](assets/do-not-localize/grid-view.png)[!UICONTROL 格線檢視]**：格線檢視在列與欄的格線中顯示可捲動的檔案和資料夾。
* **![圖庫檢視](assets/do-not-localize/gallery-view.png)[!UICONTROL 圖庫檢視]**：圖庫檢視在居中鎖定的水平清單中顯示檔案或資料夾。
* **![瀑布檢視](assets/do-not-localize/waterfall-view.png)[!UICONTROL 瀑布檢視]**：瀑布檢視以 Bridge 的形式顯示檔案或資料夾。

<!--
### Modes to view Asset Selector

Asset Selector supports two types of out of the box views:

**  Modal view or Inline view:** The modal view or inline view is the default view of Asset Selector that represents Assets folders in the front area. The modal view allows users to view assets in a full screen to ease the selection of multiple assets for import. Use `<AssetSelector rail={false}>` to enable modal view.

    ![modal-view](assets/modal-view.png)

**  Rail view:** The rail view represents Assets folders in a left panel. The drag and drop of assets can be performed in this view. Use `<AssetSelector rail={true}>` to enable rail view.

    ![rail-view](assets/rail-view.png)
-->
<!--

### Application Integration

Asset Selector is flexible and can be integrated within your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application. It is accessible and localized to add, search, and select assets in your application. With Asset Selector you can:
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It allows you to control the display of various text or symbols as per your choice.
*   **Perfect fit** Asset selector easily fits in your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application and choose the way you want to view. The mode of view can be inline, rail, or modal view.
*   **Accessible** With Asset Selector, you can reach the desired asset in an easy manner.
*   **Localize** Assets can be availed for the various locales available as per Adobe's localization standards.
-->
<!--

### Support for multiple instances

The micro front-end design supports the display of multiple instances of Asset Selector on a single screen.

![multiple-instance](assets/multiple-instance.png)
-->

<!--

### Controlled selection with multi-select

You can make default multi-selection of assets by specifying the assets to the component using `selectedAssets` property. You should specify an array of asset IDs. For example, `[{id: 'urn:234}, {id: 'urn:555'}].`
-->
<!--

### Action buttons

When you customize your application with Asset Selector based on ReactJS, you are provided with the following action buttons to perform various actions:
*   **Open in media library** Allows you to open the asset in media library.
*   **Upload** Allows you to upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector allows you to know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->
