---
title: 資產選擇器 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service]
description: 使用「資產」選擇器搜索、查找和檢索應用程式中資產的元資料和格式副本。
contentOwner: Adobe
role: Admin,User
source-git-commit: af36101d8fecd7fab2300f93d40bba4c92f8eafe
workflow-type: tm+mt
source-wordcount: '2378'
ht-degree: 3%

---


# 微型前端資產選擇器 {#Overview}

Micro-Frontend Asset Selector提供一個用戶介面，可輕鬆與 [!DNL Experience Manager Assets as a Cloud Service] 儲存庫，以便您可以瀏覽或搜索儲存庫中可用的數字資產，並在應用程式創作體驗中使用它們。

使用「資產選擇器」包，在您的應用程式體驗中可使用Micro-Frontend用戶介面。 自動導入包的任何更新，並在應用程式中自動載入最新部署的資產選擇器。

![概觀](assets/overview.png)

資產選擇器提供許多好處，例如：

* 易於使用Vanilla JavaScript庫與任何Adobe或非Adobe應用程式整合。
* 易於維護，因為資產選擇器包的更新將自動部署到適用於您的應用程式的資產選擇器。 您的應用程式中不需要更新來載入最新的修改。
* 易於自定義，因為應用程式中有可控制資產選擇器顯示的屬性。

* 全文搜索、現成功能和自定義篩選器，以快速導航到資產，供創作體驗使用。

* 能夠切換IMS組織內的儲存庫以進行資產選擇。

* 能夠按名稱、維和大小對資產進行排序，並在「清單」、「網格」、「庫」或「瀑布」視圖中查看這些資產。

本文的範圍是演示如何將Asset Selector與 [!DNL Adobe] 在Unified Shell下或已生成imsToken進行身份驗證時生成。 這些工作流在本文中稱為非SUSI流。

執行以下任務，將資產選擇器與 [!DNL Experience Manager Assets as a Cloud Service] 儲存庫：

* [使用Vanilla JS整合資產選擇器](#integration-with-vanilla-js)
* [定義資產選擇器顯示屬性](#asset-selector-properties)
* [使用資產選擇器](#using-asset-selector)

## 使用Vanilla JS整合資產選擇器 {#integration-with-vanilla-js}

可以整合任何 [!DNL Adobe] 或非Adobe應用程式 [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] 儲存庫，並從應用程式中選擇資產。

通過導入Asset Selector軟體包並使用Vanilla JavaScript庫連接到Assetsas a Cloud Service，完成整合。 您需要編輯 `index.html` 或應用程式中的任何適當檔案。
* 定義驗證詳細資訊
* 訪問Assetsas a Cloud Service儲存庫
* 配置資產選擇器顯示屬性

<!--
Asset Selector supports authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS) properties such as `imsScope` or `imsClientID`. Authentication using these IMS properties is referred to as SUSI (Sign Up Sign In) flow in this article.

You can perform authentication without defining some of the IMS properties, such as `imsScope` or `imsClientID`, if:

*   You are integrating an [!DNL Adobe] application on [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
*   You already have an IMS token generated for authentication.

Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining `imsScope` or `imsClientID` IMS properties is referred to as a non-SUSI flow in this article.
-->

在以下情況下，無需定義某些IMS屬性即可執行身份驗證：

* 您正在整合 [!DNL Adobe] 應用程式 [統一外殼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en)。
* 您已經生成了用於驗證的IMS令牌。

## 必備條件 {#prerequisites}

<!--
If your application requires user based authentication, out-of-the-box Asset Selector also supports a flow for authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS.)

You can use properties such as `imsScope` or `imsClientID` to retrieve `imsToken` automatically. You can use SUSI (Sign Up Sign In) flow and IMS properties. Also, you can obtain your own imsToken and pass it to Asset Selector by integrating within [!DNL Adobe] application on Unified Shell or if you already have an imsToken obtained via other methods (for example, using technical account). Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining IMS properties (For example, `imsScope` and `imsClientID`) is referred to as a non-SUSI flow.
-->

定義中的先決條件 `index.html` 檔案或應用程式實現中的類似檔案，以定義訪問 [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] 儲存庫。 先決條件包括：
* imsOrg
* ims令牌
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

資產選擇器可通過兩個ESM CDN(例如， [esm.sh](https://esm.sh/)/[天窗](https://www.skypack.dev/)) [UMD](https://github.com/umdjs/umd) 。

在瀏覽器中使用 **UMD版本** （推薦）:

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

在瀏覽器中 `import maps` 支援使用 **ESM CDN版本**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

在Deno/Webpack模組聯合中使用 **ESM CDN版本**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### 所選資產類型 {#selected-asset-type}

選定資產類型是使用 `handleSelection`。 `handleAssetSelection`, `onDrop` 的子菜單。

**架構語法**

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

下表介紹了選定資產對象的某些重要屬性。

| 屬性 | 類型 | 解釋 |
|---|---|---|
| *repo:repositoryId* | 字串 | 儲存資產的儲存庫的唯一標識符。 |
| *回購：id* | 字串 | 資產的唯一標識符。 |
| *repo:assetClass* | 字串 | 資產的分類（例如，影像或視頻、文檔）。 |
| *repo：名稱* | 字串 | 資產的名稱，包括檔案副檔名。 |
| *回購：大小* | 數字 | 資產位元組的大小。 |
| *回購：路徑* | 字串 | 資產在儲存庫中的位置。 |
| *repo：祖先* | `Array<string>` | 儲存庫中資產的祖先項的陣列。 |
| *回購：狀態* | 字串 | 儲存庫中資產的當前狀態（例如，活動、已刪除等）。 |
| *repo：建立者* | 字串 | 建立資產的用戶或系統。 |
| *repo:createDate* | 字串 | 建立資產的日期和時間。 |
| *repo:modifiedBy* | 字串 | 上次修改資產的用戶或系統。 |
| *repo:modifyDate* | 字串 | 上次修改資產的日期和時間。 |
| *dc:format* | 字串 | 資產的格式，如檔案類型(例如，JPEG、PNG等)。 |
| *tiff：影像寬度* | 數字 | 資產的寬度。 |
| *tiff：影像長度* | 數字 | 資產的高度。 |
| *計算元資料* | `Record<string, any>` | 一個對象，它代表所有類型（儲存庫、應用程式或嵌入元資料）的資產的元資料的儲存桶。 |
| *連結* | `Record<string, any>` | 關聯資產的超級媒體連結。 包括元資料和格式副本等資源的連結。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition* | `Array<Object>` | 包含有關資產格式副本資訊的對象陣列。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].href* | 字串 | 格式副本的URI。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].類型* | 字串 | 格式副本的MIME類型。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[]&#39;repo：大小* | 數字 | 格式副本的大小（以位元組為單位）。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].寬度* | 數字 | 格式副本的寬度。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].高度* | 數字 | 格式副本的高度。 |

有關屬性和詳細示例的完整清單，請訪問 [資產選擇器代碼示例](https://github.com/adobe/aem-assets-selectors-mfe-examples)。

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

### 非SUSI流示例 {#non-susi-vanilla}

此示例說明在運行 [!DNL Adobe] 應用程式，或當您已 `imsToken` 為驗證生成。

使用 `script` 標籤，如所示 _6至15行_ 下例。 載入指令碼後， `PureJSSelectors` 全局變數可用。 定義資產選擇器 [屬性](#asset-selector-properties) 如所示 _線路16至23_。 的 `imsOrg` 和 `imsToken` 屬性在非SUSI流中都是身份驗證所必需的。 的 `handleSelection` 屬性用於處理選定的資產。 要呈現資產選擇器，請調用 `renderAssetSelector` 函式，如 _17號線_。 「資產選擇器」顯示在 `<div>` 容器元素，如所示 _行21和22_。

通過執行這些步驟，您可以將資產選擇器與非SUSI流一起使用 [!DNL Adobe] 的子菜單。

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

有關詳細示例，請訪問 [資產選擇器代碼示例](https://github.com/adobe/aem-assets-selectors-mfe-examples)。

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

您可以使用「資產選擇器」屬性來自定義「資產選擇器」的呈現方式。 下表列出了可用於自定義和使用資產選擇器的屬性。

| 屬性 | 類型 | 必要 | 預設 | 說明 |
|---|---|---|---|---|
| *軌* | 布林值 | 否 | false | 如果已標籤 `true`，資產選擇器將在左欄視圖中呈現。 如果已標籤 `false`，將在模式視圖中呈現「資產選擇器」。 |
| *imsOrg* | 字串 | 是 |  | AdobeIdentity Management系統(IMS)ID，該ID在設定時分配 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 為您的組織。 的 `imsOrg` 驗證您訪問的組織是否在Adobe IMS下需要密鑰。 |
| *ims令牌* | 字串 | 否 |  | 用於驗證的IMS持有者令牌。 `imsToken` 使用非SUSI流時為必填項。 |
| *api密鑰* | 字串 | 否 |  | 用於訪問Discovery服務AEM的API密鑰。 `apiKey` 使用非SUSI流時為必填項。 |
| *根路徑* | 字串 | 否 | /content/dam/ | 資產選擇器從中顯示資產的資料夾路徑。 `rootPath` 也可以以封裝形式使用。 例如，給定以下路徑， `/content/dam/marketing/subfolder/`，資產選擇器不允許您遍歷任何父資料夾，但只顯示子資料夾。 |
| *路徑* | 字串 | 否 |  | 在呈現資產選擇器時用於導航到資產特定目錄的路徑。 |
| *filterSchema* | 陣列 | 否 |  | 用於配置篩選器屬性的模型。 當要限制資產選擇器中的某些篩選器選項時，此選項非常有用。 |
| *filterFormProps* | 物件 | 否 |  | 指定需要用於細化搜索的篩選器屬性。 例如，MIME類型JPG、PNG、GIF。 |
| *選定資產* | 陣列 `<Object>` | 否 |  | 在呈現資產選擇器時指定選定的資產。 需要包含資產id屬性的對象陣列。 比如說， `[{id: 'urn:234}, {id: 'urn:555'}]` 當前目錄中必須有資產可用。 如果需要使用其他目錄，請為 `path` 還有財產。 |
| *acv配置* | 物件 | 否 |  | 包含包含要覆蓋預設值的自定義配置的對象的「資產收集視圖」屬性。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |  | 如果OOTB翻譯不能滿足您的應用程式的需要，則您可以公開一個介面，通過該介面，您可以通過 `i18nSymbols` 道具。 通過此介面傳遞值將覆蓋提供的預設轉換，而使用您自己的轉換。  要執行覆蓋，必須傳遞有效 [消息描述符](https://formatjs.io/docs/react-intl/api/#message-descriptor) 對象到的鍵 `i18nSymbols` 你想推翻的。 |
| *超* | 物件 | 否 |  | 資產選擇器提供預設的OOTB轉換。 通過提供有效的區域設定字串，可以選擇翻譯語言 `intl.locale` 道具。 例如： `intl={{ locale: "es-es" }}` </br></br> 支援的區域設定字串 [ISO 639 — 代碼](https://www.iso.org/iso-639-language-codes.html) 語言名稱標準的表示。 </br></br> 支援的區域設定清單：英語 — &#39;en-us&#39;（預設）西班牙語 — &#39;es-es&#39;德語 — &#39;de-de&#39;法語 — &#39;fr-fr&#39;義大利語 — &#39;it-it&#39;日語 — &#39;ja-jp&#39;韓語 — &#39;ko-kr&#39;葡萄牙語 — &#39;pt-br&#39;中文（繁體） — &#39;zh-cn&#39;中文（台灣） — &#39;zh-tw&#39; |
| *資料庫ID* | 字串 | 否 | &quot; | 資產選擇器從中載入內容的儲存庫。 |
| *其他AemSolutions* | `Array<string>` | 否 | [ ] | 它允許您添加其他儲存庫AEM清單。 如果此屬性中未提供任何資訊，則只考慮介質庫或AEM Assets儲存庫。 |
| *隱藏樹導航* | 布林值 | 否 |  | 指定是顯示還是隱藏資產樹導航邊欄。 它僅用於模態視圖，因此在軌道視圖中不會影響該屬性。 |
| *離線* | 函數 | 否 |  | 該屬性允許資產的刪除功能。 |
| *刪除選項* | `{allowList?: Object}` | 否 |  | 使用「allowList」配置刪除選項。 |
| *配色方案* | 字串 | 否 |  | 配置主題(`light` 或 `dark`)。 |
| *句柄選擇* | 函數 | 否 |  | 在選擇資產和 `Select` 按鈕 此函式僅在模式視圖中調用。 對於鐵路視圖，使用 `handleAssetSelection` 或 `onDrop` 的子菜單。 範例: <pre>handleSelection=(資產：資產[])=> {...</pre> 請參閱 [所選資產類型](#selected-asset-type) 的雙曲餘切值。 |
| *句柄資產選擇* | 函數 | 否 |  | 在選擇或取消選擇資產時，使用項陣列調用。 當用戶選擇資產時，當您要偵聽這些資產時，此功能非常有用。 範例: <pre>handleSelection=(資產：資產[])=> {...</pre> 請參閱 [所選資產類型](#selected-asset-type) 的雙曲餘切值。 |
| *關閉* | 函數 | 否 |  | 在 `Close` 按鈕。 僅調用 `modal` 查看和忽略 `rail` 的子菜單。 |
| *onFilterSubmit* | 函數 | 否 |  | 當用戶更改不同的篩選條件時，使用篩選器項調用。 |
| *選擇類型* | 字串 | 否 | 單一 | 配置 `single` 或 `multiple` 一次選擇資產。 |

## 使用資產選擇器屬性的示例 {#usage-examples}

您可以定義資產選擇器 [屬性](#asset-selector-properties) 的 `index.html` 檔案，以自定義應用程式中的「資產選擇器」顯示。

### 示例1:鐵路視圖中的資產選擇器

![軌道視圖示例](assets/rail-view-example-vanilla.png)

如果AssetSelector的值 `rail` 設定為 `false` 或在屬性中未提及，則預設情況下，「資產選擇器」(Asset Selector)將顯示在「模式」視圖中。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### 示例2:元資料跨距

使用各種屬性來定義要使用資訊表徵圖查看的資產的元資料。 資訊跨距提供有關資產或資料夾的資訊的集合，包括資產的標題、尺寸、修改日期、位置和說明。 在以下示例中，使用各種屬性來顯示資產的元資料，例如， `repo:path` 屬性指定資產的位置。 <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![元資料跨距示例](assets/metadata-popover.png)


### 示例3:軌道視圖中的自定義篩選器屬性

除了多面搜索外，「資產選擇器」還允許您自定義各種屬性以從 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 的子菜單。 您需要添加以下代碼以在應用程式中添加自定義搜索篩選器。 在下面的示例中， `Type Filter` 用於篩選「影像」、「文檔」或「視頻」中的資產類型或您為搜索添加的篩選器類型的搜索。

![定制過濾器示例香草](assets/custom-filter-example-vanilla.png)

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

## 使用對象架構處理資產選擇 {#handling-selection}

的 `handleSelection` 屬性用於處理在Assets Selector中選擇的單個或多個資產。 以下示例說明了 `handleSelection`。

![句柄選擇](assets/handling-selection.png)

## 使用資產選擇器 {#using-asset-selector}

設定資產選擇器後，您將通過身份驗證與 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 應用程式，您可以選擇資產或執行各種其他操作以在儲存庫中搜索資產。

![使用資產選擇器](assets/using-asset-selector.png)

* **A**: [隱藏/顯示面板](#hide-show-panel)
* **B**: [儲存庫切換器](#repository-switcher)
* **C**: [資產](#repository)
* **D**: [篩選器](#filters)
* **E**: [搜索欄](#search-bar)
* **F**: [排序](#sorting)
* **G**: [按升序或降序排序](#sorting)
* **H**: [視圖](#types-of-view)

### 隱藏/顯示面板 {#hide-show-panel}

要隱藏左導航中的資料夾，請按一下 **[!UICONTROL 隱藏資料夾]** 表徵圖 要撤消更改，請按一下 **[!UICONTROL 隱藏資料夾]** 的子菜單。

### 儲存庫切換器 {#repository-switcher}

資產選擇器還允許您切換儲存庫以進行資產選擇。 您可以從左側面板中的下拉菜單中選擇您選擇的儲存庫。 下拉清單中可用的儲存庫選項基於 `repositoryId` 在 `index.html` 的子菜單。 它基於登錄用戶訪問的所選IMS組織中的環境。 消費者可以通過首選 `repositoryID` 在這種情況下，資產選擇器停止呈現回購交換機，並僅從給定的儲存庫呈現資產。
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### 資產儲存庫

它是可用於執行操作的資產資料夾的集合。

### 現成過濾器 {#filters}

資產選擇器還提供現成過濾器選項來優化搜索結果。 以下篩選器可用：

* `File type`:包括資料夾、檔案、影像、文檔或視頻
* `MIME type`:包括JPG、GIF、PPTX、PNG、MP4、DOCX、TIFF、PDF、XLSX
* `Image Size`:包括最小/最大寬度、最小/最大影像高度

![軌道視圖示例](assets/filters-asset-selector.png)

### 自定義搜索

除了全文搜索外，「資產選擇器」還允許您使用自定義搜索在檔案內搜索資產。 可以在「模式」視圖和「軌道」視圖模式中使用自定義搜索過濾器。

![自定義搜索](assets/custom-search.png)

您還可以建立預設搜索篩選器，以保存您經常搜索的欄位，並稍後使用這些欄位。 要為資產建立自定義搜索，您可以使用 `filterSchema` 屬性。

### 搜索欄 {#search-bar}

資產選擇器允許您對選定儲存庫中的資產執行全文搜索。 例如，如果鍵入關鍵字 `wave` 在搜索欄中，所有 `wave` 將顯示任何元資料屬性中提及的關鍵字。

### 排序 {#sorting}

您可以按資產的名稱、維或大小對「資產選擇器」中的資產進行排序。 您還可以按升序或降序對資產進行排序。

### 視圖類型 {#types-of-view}

資產選擇器允許您以四個不同的視圖查看資產：

* **![清單視圖](assets/do-not-localize/list-view.png) [!UICONTROL 清單視圖]**:清單視圖在單個列中顯示可滾動的檔案和資料夾。
* **![網格視圖](assets/do-not-localize/grid-view.png) [!UICONTROL 網格視圖]**:網格視圖在行和列的網格中顯示可滾動的檔案和資料夾。
* **![庫視圖](assets/do-not-localize/gallery-view.png) [!UICONTROL 庫視圖]**:庫視圖在中心鎖定的水準清單中顯示檔案或資料夾。
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