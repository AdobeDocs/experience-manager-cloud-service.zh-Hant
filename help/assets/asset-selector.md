---
title: 適用於 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: 使用資產選擇器在您的應用程式中搜尋、尋找及擷取資產的中繼資料和轉譯。
contentOwner: Adobe
role: Admin,User
source-git-commit: 22d2a2235c8696fce76369d3ffe369bcbaa3f6f2
workflow-type: tm+mt
source-wordcount: '2355'
ht-degree: 3%

---


# 微額資產選擇器 {#Overview}

Micro-Frontend Asset Selector提供可輕鬆與 [!DNL Experience Manager Assets as a Cloud Service] 存放庫，以便您能夠瀏覽或搜尋存放庫中可用的數位資產，並在應用程式編寫體驗中使用這些資產。

您可使用資產選取器套件，在應用程式體驗中使用Micro-Frontend使用者介面。 套件的任何更新都會自動匯入，而最新部署的資產選擇器會自動在您的應用程式中載入。

![概觀](assets/overview.png)

資產選擇器提供許多優點，例如：

* 使用Vanilla JavaScript程式庫，輕鬆與任何Adobe或非Adobe應用程式整合。
* 易於維護，因為資產選擇器套件的更新會自動部署至您應用程式可用的資產選擇器。 您的應用程式內不需要更新即可載入最新修改。
* 由於有可控制「資產選擇器」的屬性可用，因此可輕鬆自訂。

* 全文搜尋、現成可用和自訂的篩選器，可快速導覽至創作體驗中使用的資產。

* 可切換IMS組織內的存放庫以選擇資產。

* 能夠依名稱、維度和大小排序資產，並在「清單」、「網格」、「圖庫」或「瀑布圖」檢視中檢視資產。

執行下列工作，將Asset Selector與您的 [!DNL Experience Manager Assets as a Cloud Service] 存放庫：

* [使用Vanilla JS整合資產選取器](#integration-with-vanilla-js)
* [定義資產選擇器顯示屬性](#asset-selector-properties)
* [使用資產選擇器](#using-asset-selector)

## 使用Vanilla JS整合資產選取器 {#integration-with-vanilla-js}

您可以整合任何 [!DNL Adobe] 或非Adobe應用程式 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 存放庫，然後從應用程式內選取資產。

整合的方式為匯入「資產選取器」套件，並使用Vanilla JavaScript程式庫連線至as a Cloud Service資產。 您需要編輯 `index.html` 或應用程式中任何適當的檔案，
* 定義驗證詳細資訊
* 存取Assetsas a Cloud Service存放庫
* 設定資產選擇器顯示屬性

<!--
Asset Selector supports authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS) properties such as `imsScope` or `imsClientID`. Authentication using these IMS properties is referred to as SUSI (Sign Up Sign In) flow in this article.

You can perform authentication without defining some of the IMS properties, such as `imsScope` or `imsClientID`, if:

*   You are integrating an [!DNL Adobe] application on [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
*   You already have an IMS token generated for authentication.

Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining `imsScope` or `imsClientID` IMS properties is referred to as a non-SUSI flow in this article.
-->

若符合下列條件，您就可以不定義部分IMS屬性而執行驗證：

* 您正在整合 [!DNL Adobe] 應用程式 [統一殼層](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
* 您已為驗證產生IMS代號。

## 必備條件 {#prerequisites}

<!--
If your application requires user based authentication, out-of-the-box Asset Selector also supports a flow for authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS.)

You can use properties such as `imsScope` or `imsClientID` to retrieve `imsToken` automatically. You can use SUSI (Sign Up Sign In) flow and IMS properties. Also, you can obtain your own imsToken and pass it to Asset Selector by integrating within [!DNL Adobe] application on Unified Shell or if you already have an imsToken obtained via other methods (for example, using technical account). Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining IMS properties (For example, `imsScope` and `imsClientID`) is referred to as a non-SUSI flow.
-->

在 `index.html` 檔案或應用程式實作中的類似檔案，以定義驗證詳細資料以存取 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 存放庫。 先決條件包括：
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

可透過兩個ESM CDN使用資產選取器(例如 [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/))和 [UMD](https://github.com/umdjs/umd) 版本。

在使用 **UMD版本** （建議）:

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

在具有 `import maps` 支援使用 **ESM CDN版本**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

在Deno/Webpack模組聯合中，使用 **ESM CDN版本**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### 所選資產類型 {#selected-asset-type}

所選資產類型是一組物件，當使用 `handleSelection`, `handleAssetSelection`，和 `onDrop` 函式。

**結構語法**

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

下表說明所選資產物件的一些重要屬性。

| 屬性 | 類型 | 解釋 |
|---|---|---|
| *repo:repositoryId* | 字串 | 儲存資產的存放庫的唯一識別碼。 |
| *repo.id* | 字串 | 資產的唯一識別碼。 |
| *repo:assetClass* | 字串 | 資產的分類（例如影像或視訊、檔案）。 |
| *repo.name* | 字串 | 資產的名稱，包括副檔名。 |
| *repo:size* | 數字 | 資產位元組的大小。 |
| *repo.path* | 字串 | 資產在存放庫內的位置。 |
| *repo:ancestors* | `Array<string>` | 存放庫中資產的上階項目陣列。 |
| *repo.state* | 字串 | 存放庫中資產的目前狀態（例如使用中、已刪除等）。 |
| *repo:createdBy* | 字串 | 建立資產的使用者或系統。 |
| *repo:createDate* | 字串 | 資產建立的日期和時間。 |
| *repo:modifiedBy* | 字串 | 上次修改資產的使用者或系統。 |
| *repo:modifyDate* | 字串 | 上次修改資產的日期和時間。 |
| *dc:format* | 字串 | 資產的格式，例如檔案類型(例如JPEG、PNG等)。 |
| *tiff:imageWidth* | 數字 | 資產的寬度。 |
| *tiff:imageLength* | 數字 | 資產的高度。 |
| *computedMetadata* | `Record<string, any>` | 物件，代表所有資產中繼資料（存放庫、應用程式或內嵌中繼資料）的貯體。 |
| *_links* | `Record<string, any>` | 相關資產的超媒體連結。 包括中繼資料和轉譯等資源的連結。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition* | `Array<Object>` | 包含資產轉譯資訊的物件陣列。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].href* | 字串 | 格式副本的URI。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].type* | 字串 | 轉譯的MIME類型。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].&#39;repo:size&#39;* | 數字 | 格式副本的大小（以位元組為單位）。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].width* | 數字 | 轉譯的寬度。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].height* | 數字 | 轉譯的高度。 |

如需屬性的完整清單和詳細範例，請造訪 [資產選擇器程式碼範例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

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

### 非SUSI流的範例 {#non-susi-vanilla}

此範例示範如何在執行 [!DNL Adobe] 應用程式（位於「統一殼層」下）或 `imsToken` 為驗證而產生。

在程式碼中加入資產選取器套件，使用 `script` 標籤，如 _行6至15_ 以下範例。 指令碼載入後， `PureJSSelectors` 全域變數可供使用。 定義資產選取器 [屬性](#asset-selector-properties) 如所示 _行16 - 23_. 此 `imsOrg` 和 `imsToken` 屬性在非SUSI流中均是驗證必需的。 此 `handleSelection` 屬性可用來處理選取的資產。 若要呈現「資產選取器」，請呼叫 `renderAssetSelector` 函式，於 _17號線_. 「資產選取器」會顯示在 `<div>` 容器元素，如 _行21和22_.

依照下列步驟操作，您可以將「資產選取器」與「非SUSI」流程搭配使用 [!DNL Adobe] 應用程式。

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

如需詳細範例，請造訪 [資產選擇器程式碼範例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

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

您可以使用「資產選擇器」屬性來自訂資產選擇器的呈現方式。 下表列出您可用來自訂和使用「資產選取器」的屬性。

| 屬性 | 類型 | 必要 | 預設 | 說明 |
|---|---|---|---|---|
| *邊欄* | 布林值 | 否 | false | 如果已標籤 `true`，資產選擇器會以左側邊欄檢視呈現。 如果已標籤 `false`，資產選取器會以強制回應檢視呈現。 |
| *imsOrg* | 字串 | 是 |  | Adobe布建時指派的Identity Management系統(IMS)ID [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 貴組織。 此 `imsOrg` 驗證您存取的組織是否位於Adobe IMS之下時，需要金鑰。 |
| *imsToken* | 字串 | 否 |  | 用於驗證的IMS承載權杖。 `imsToken` 如果您使用SUSI流，則不需要。 不過，如果您使用非SUSI流，則此為必要項目。 |
| *apiKey* | 字串 | 否 |  | 用於存取AEM Discovery服務的API金鑰。 `apiKey` 如果您使用SUSI流，則不需要。 但是，它在非SUSI流中是必需的。 |
| *rootPath* | 字串 | 否 | /content/dam/ | 「資產選擇器」顯示資產的資料夾路徑。 `rootPath` 也可以以封裝的形式使用。 例如，在下列路徑中， `/content/dam/marketing/subfolder/`，資產選取器不允許您周遊任何父資料夾，但只會顯示子資料夾。 |
| *路徑* | 字串 | 否 |  | 呈現資產選擇器時用於導覽至特定資產目錄的路徑。 |
| *filterSchema* | 陣列 | 否 |  | 用於配置篩選器屬性的模型。 如果您想要限制「資產選擇器」中的特定篩選選項，此功能會相當實用。 |
| *filterFormProps* | 物件 | 否 |  | 指定您需要用來調整搜尋的篩選屬性。 例如MIME類型JPG、PNG、GIF。 |
| *selectedAssets* | 陣列 `<Object>` | 否 |  | 在轉譯「資產選擇器」時指定選取的資產。 需要包含資產ID屬性的物件陣列。 例如， `[{id: 'urn:234}, {id: 'urn:555'}]` 目前目錄中必須有資產可用。 如果您需要使用不同目錄，請為 `path` 屬性。 |
| *acvConfig* | 物件 | 否 |  | 包含包含自訂設定的物件以覆寫預設值的資產集合檢視屬性。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |  | 如果OOTB翻譯不足以滿足您的應用程式的需求，您可以公開一個介面，透過該介面，您可以透過 `i18nSymbols` prop。 透過此介面傳遞值會覆寫提供的預設翻譯，而改用您自己的翻譯。  若要執行覆寫，您必須傳遞有效的 [消息描述符](https://formatjs.io/docs/react-intl/api/#message-descriptor) 物件至的鍵 `i18nSymbols` 你想置換的。 |
| *intl* | 物件 | 否 |  | 「資產選擇器」提供預設的OOTB翻譯。 通過提供有效的語言環境字串，可以選擇翻譯語言 `intl.locale` prop。 例如： `intl={{ locale: "es-es" }}` </br></br> 支援的地區設定字串遵循 [ISO 639 — 代碼](https://www.iso.org/iso-639-language-codes.html) 代表語言標準。 </br></br> 支援的地區設定清單：英文 — &#39;en-us&#39;（預設）西班牙文 — &#39;es&#39;德文 — &#39;de-de&#39;法文 — &#39;fr-fr&#39;義大利文 — &#39;it-it&#39;日文 — &#39;ja-jp&#39;韓文 — &#39;ko-kr&#39;葡萄牙文 — &#39;pt-br&#39;中文（繁體） — &#39;zh-cn&#39;中文（台灣） — &#39;zh-tw&#39; |
| *repositoryId* | 字串 | 否 | &quot; | 資產選擇器載入內容的存放庫。 |
| *additionalAemSolutions* | `Array<string>` | 否 | [ ] | 它可讓您新增其他AEM存放庫的清單。 若此屬性中未提供任何資訊，則只會考慮媒體程式庫或AEM Assets存放庫。 |
| *hideTreeNav* | 布林值 | 否 |  | 指定是顯示還是隱藏資產樹導航側欄。 此屬性僅用於強制回應檢視，因此在邊欄檢視中不會有此屬性的影響。 |
| *onDrop* | 函數 | 否 |  | 屬性可讓資產的拖放功能。 |
| *dropOptions* | `{allowList?: Object}` | 否 |  | 使用&#39;allowList&#39;配置刪除選項。 |
| *colorScheme* | 字串 | 否 |  | 配置主題(`light` 或 `dark`)（適用於資產選取器）。 |
| *handleSelection* | 函數 | 否 |  | 選取資產時，透過資產項目陣列叫用，且 `Select` 按鈕。 此函式只會在強制回應視圖中叫用。 若為邊欄檢視，請使用 `handleAssetSelection` 或 `onDrop` 函式。 範例: <pre>handleSelection=(assets:資產[])=> {..}</pre> 請參閱 [所選資產類型](#selected-asset-type) 以取得詳細資訊。 |
| *handleAssetSelection* | 函數 | 否 |  | 在選取或取消選取資產時，以項目陣列叫用。 當您想要在使用者選取資產時監聽資產，這個功能會很實用。 範例: <pre>handleSelection=(assets:資產[])=> {..}</pre> 請參閱 [所選資產類型](#selected-asset-type) 以取得詳細資訊。 |
| *onClose* | 函數 | 否 |  | 在 `Close` 按鈕。 這只會呼叫 `modal` 在 `rail` 檢視。 |
| *onFilterSubmit* | 函數 | 否 |  | 當使用者變更不同的篩選條件時，叫用篩選項目。 |
| *selectionType* | 字串 | 否 | 單一 | 配置 `single` 或 `multiple` 一次選取資產。 |

## 使用資產選擇器屬性的範例 {#usage-examples}

您可以定義資產選擇器 [屬性](#asset-selector-properties) 在 `index.html` 檔案來自訂「資產選取器」在您的應用程式內顯示。

### 範例1:邊欄檢視中的資產選取器

![邊欄檢視範例](assets/rail-view-example-vanilla.png)

如果AssetSelector的值 `rail` 設為 `false` 或屬性中未提及，則預設情況下，資產選擇器會顯示在強制回應視窗中。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### 範例2:中繼資料彈出視窗

使用各種屬性，以使用資訊圖示來定義您要檢視之資產的中繼資料。 資訊彈出式視窗提供資產或資料夾的相關資訊收集，包括資產的標題、維度、修改日期、位置和說明。 在下列範例中，各種屬性用於顯示資產的中繼資料，例如 `repo:path` 屬性會指定資產的位置。 <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)


### 範例3:邊欄檢視中的自訂篩選器屬性

除了多面搜尋外，「資產選擇器」還可讓您自訂各種屬性，以從 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 應用程式。 您必須新增下列程式碼，才能在您的應用程式中新增自訂搜尋篩選器。 在以下範例中， `Type Filter` 搜尋可篩選影像、檔案或影片中的資產類型，或您為搜尋新增的篩選類型。

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

## 使用物件結構處理資產的選取 {#handling-selection}

此 `handleSelection` 屬性可用於處理資產選擇器中的單一或多個資產選取項目。 以下範例說明的使用語法 `handleSelection`.

![句柄選擇](assets/handling-selection.png)

## 使用資產選擇器 {#using-asset-selector}

設定資產選擇器後，您即通過驗證，可搭配您的 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 應用程式中，您可以選取資產或執行各種其他作業，以在存放庫內搜尋您的資產。

![using-asset-selector](assets/using-asset-selector.png)

* **A**: [隱藏/顯示面板](#hide-show-panel)
* **B**: [存放庫切換器](#repository-switcher)
* **C**: [資產](#repository)
* **D**: [篩選器](#filters)
* **E**: [搜尋列](#search-bar)
* **F**: [排序](#sorting)
* **G**: [依遞增或遞減順序排序](#sorting)
* **H**: [檢視](#types-of-view)

### 隱藏/顯示面板 {#hide-show-panel}

若要隱藏左側導覽中的資料夾，請按一下 **[!UICONTROL 隱藏資料夾]** 表徵圖。 若要還原變更，請按一下 **[!UICONTROL 隱藏資料夾]** 圖示。

### 存放庫切換器 {#repository-switcher}

「資產選擇器」也可讓您切換資產選擇的存放庫。 您可以從左側面板的下拉式清單中選取您選擇的存放庫。 下拉式清單中可用的存放庫選項會以 `repositoryId` 在中定義的屬性 `index.html` 檔案。 它以登入使用者存取之所選IMS組織中的環境為基礎。 消費者可以傳遞 `repositoryID` 在此情況下，資產選擇器會停止轉譯存放庫切換器，並只從指定存放庫轉譯資產。
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### 資產存放庫

這是資產資料夾的集合，您可以用來執行操作。

### 現成可用的篩選器 {#filters}

「資產選擇器」也提供現成可用的篩選選項，以調整搜尋結果。 可使用下列篩選：

* `File type`:包括資料夾、檔案、影像、文檔或視頻
* `MIME type`:包括JPG、GIF、PPTX、PNG、MP4、DOCX、TIFF、PDF、XLSX
* `Image Size`:包括最小/最大寬度、最小/最大影像高度

![邊欄檢視範例](assets/filters-asset-selector.png)

### 自訂搜尋

除了全文搜尋外，「資產選擇器」還可讓您使用自訂搜尋功能，在檔案內搜尋資產。 您可以在強制回應視圖和邊欄檢視模式中使用自訂搜尋篩選器。

![自訂搜尋](assets/custom-search.png)

您也可以建立預設搜尋篩選器，以儲存您經常搜尋的欄位，並稍後使用。 若要建立資產的自訂搜尋，您可以使用 `filterSchema` 屬性。

### 搜尋列 {#search-bar}

「資產選取器」可讓您對選取存放庫內的資產執行全文搜尋。 例如，如果您輸入關鍵字 `wave` 在搜尋列中， `wave` 任何中繼資料屬性中提及的關鍵字都會顯示。

### 排序 {#sorting}

您可以在「資產選擇器」中依資產名稱、維度或大小來排序資產。 您也可以依遞增或遞減順序來排序資產。

### 檢視類型 {#types-of-view}

「資產選擇器」可讓您以四種不同檢視來檢視資產：

* **![清單檢視](assets/do-not-localize/list-view.png) [!UICONTROL 清單檢視]**:清單視圖在單個列中顯示可捲動的檔案和資料夾。
* **![網格視圖](assets/do-not-localize/grid-view.png) [!UICONTROL 網格視圖]**:網格視圖以行和列的網格顯示可滾動的檔案和資料夾。
* **![圖庫檢視](assets/do-not-localize/gallery-view.png) [!UICONTROL 圖庫視圖]**:圖庫視圖在中心鎖定的水準清單中顯示檔案或資料夾。
* **![瀑布視圖](assets/do-not-localize/waterfall-view.png) [!UICONTROL 瀑布視圖]**:瀑布視圖以橋的形式顯示檔案或資料夾。

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