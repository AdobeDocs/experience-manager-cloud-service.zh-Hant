---
title: 適用於  [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service] 的資產選擇器
description: 在應用程式內使用資產選擇器搜尋、查找和檢索資產的中繼資料和轉譯。
contentOwner: KK
role: Admin,User
exl-id: 5f962162-ad6f-4888-8b39-bf5632f4f298
source-git-commit: 2ce64892cd5bf414d328a9112c47092b762d3668
workflow-type: tm+mt
source-wordcount: '3908'
ht-degree: 45%

---

# 微前端資產選擇器 {#Overview}

微前端資產選擇器提供一個輕鬆整合 [!DNL Experience Manager Assets] 存放庫的使用者介面，讓您可以瀏覽或搜尋存放庫中的可用數位資產，並用於您的應用程式編寫體驗。

在您的應用程式體驗中可利用資產選擇器套件使用微前端使用者介面。套件的任何更新都會自動匯入，而最新部署的資產選擇器會自動載入到您的應用程式。

![概觀](assets/overview.png)

資產選擇器提供了許多優點，例如：

* 輕鬆與任何 [Adobe](#asset-selector-ims) 或 [非Adobe](#asset-selector-non-ims) 使用Vanilla JavaScript程式庫的應用程式。
* 容易維護，因為資產選擇器套件的更新會自動部署到您的應用程式可用的資產選擇器。您的應用程式無需更新即可載入最新的修改內容。
* 簡易的自訂功能，因為有可以控制應用程式中資產選擇器顯示的可用屬性。
* 全文搜尋、開箱即用和自訂篩選器，可快速找到要在編寫體驗中使用的資產。
* 能夠在 IMS 組織內切換存放庫以選擇資產。
* 能夠按名稱、維度和大小對資產進行排序，並以清單、網格、圖庫或瀑布視圖檢視。

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## 先決條件{#prereqs}

您必須確定下列通訊方法：

* 應用程式正在HTTPS上執行。
* 應用程式的URL位於IMS使用者端的允許重新導向URL清單中。
* IMS登入流程已設定完畢，並使用網頁瀏覽器上的快顯視窗呈現。 因此，目標瀏覽器上應該啟用或允許快顯視窗。

如果您需要Asset Selector的IMS驗證工作流程，請使用上述先決條件。 或者，如果您已通過IMS工作流程驗證，您可以改為新增IMS資訊。

>[!IMPORTANT]
>
> 此存放庫旨在作為補充檔案，說明整合資產選擇器的可用API和使用範例。 在嘗試安裝或使用「資產選擇器」之前，請確保貴組織已布建對「資產選擇器」的存取權，作為Experience Manager Assetsas a Cloud Service設定檔的一部分。 如果您尚未布建，則無法整合或使用這些元件。 若要請求布建，您的程式管理員應從Admin Console提出標示為P2的支援票證，並包含下列資訊：
>
>* 託管整合應用程式的網域名稱。
>* 布建後，您的組織將獲得 `imsClientId`， `imsScope`，和 `redirectUrl` 與要求的環境相對應，這對於設定資產選擇器至關重要。 如果沒有這些有效的屬性，您就無法執行安裝步驟。

## 安裝 {#installation}

資產選擇器可透過兩個ESM CDN使用(例如， [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/))和 [UMD](https://github.com/umdjs/umd) 版本。

在使用 **UMD 版** 的瀏覽器中 (建議)：

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

在具備 `import maps` 支援並使用 **ESM CDN 版**&#x200B;的瀏覽器中：

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

在使用 **ESM CDN 版**&#x200B;的 Deno/Webpack Module Federation 中：

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

## 使用 Vanilla JS 整合資產選擇器 {#integration-using-vanilla-js}

您可以整合 [!DNL Adobe] 或非Adobe應用程式，具有 [!DNL Experience Manager Assets] 存放庫中，並從應用程式中選取資產。 另請參閱 [Asset Selector與各種應用程式整合](#asset-selector-integration-with-apps).

匯入資產選擇器套件，並使用 Vanilla JavaScript 程式庫連接到 Assets as a Cloud Service，便完成了整合作業。編輯 `index.html` 或應用程式中任何適當的檔案：

* 定義身份驗證詳細資訊
* 存取 Assets as a Cloud Service 存放庫
* 設定資產選擇器顯示屬性

在以下情況下，您可以在不定義某些 IMS 屬性的情況下執行身份驗證：

* 在 [!DNL Adobe] [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=zh-Hant) 之上整合一個應用程式時。
* 您已經具有針對身份驗證產生的一個 IMS 語彙基元。

## 整合Asset Selector與各種應用程式 {#asset-selector-integration-with-apps}

您可以整合Asset Selector與各種應用程式，例如：

* [將資產選擇器與 [!DNL Adobe] 應用計畫](#adobe-app-integration-vanilla)
* [將資產選擇器與非Adobe應用程式整合](#adobe-non-app-integration)

>[!BEGINTABS]

<!--Integration with an Adobe application content starts here-->

>[!TAB 與Adobe應用程式整合]

### 先決條件{#prereqs-adobe-app}

如果您整合Asset Selector與 [!DNL Adobe] 應用程式

* [通訊方法](#prereqs)
* imsOrg
* imsToken
* apikey

### 將資產選擇器與 [!DNL Adobe] 應用計畫 {#adobe-app-integration-vanilla}

下列範例示範執行「 」時「資產選取器」的使用方式 [!DNL Adobe] Unified Shell下的應用程式，或當您已有 `imsToken` 產生以進行驗證。

使用以下專案在您的程式碼中加入Asset Selector套件： `script` 標籤，如所示 _第6-15行_ 範例的一部分。 在載入指令碼後，即可使用 `PureJSSelectors` 全域變數。定義資產選擇器 [屬性](#asset-selector-properties) 如所示 _第16-23行_. 此 `imsOrg` 和 `imsToken` 在Adobe應用程式中進行驗證時，屬性都是必要的。 `handleSelection` 屬性用於處理選取的資產。要轉譯資產選擇器，請呼叫 `renderAssetSelector` 函數，如&#x200B;_第 17 行_&#x200B;所述。資產選擇器顯示於 `<div>` 容器元素，如&#x200B;_第 21 和 22 行_&#x200B;所示。

按照以下步驟操作，您就可以將Asset Selector與 [!DNL Adobe] 應用程式。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
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

<!--For detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

+++**ImsAuthProps**
此 `ImsAuthProps` 屬性會定義Asset Selector用來取得 `imsToken`. 藉由設定這些屬性，您可以控制驗證流程應該如何行為並註冊各種驗證事件的接聽程式。

| 屬性名稱 | 說明 |
|---|---|
| `imsClientId` | 代表用於驗證目的之IMS使用者端ID的字串值。 此值由Adobe提供，且為您的AdobeAEM CS組織專用。 |
| `imsScope` | 說明用於驗證的範圍。 範圍會決定應用程式對貴組織資源的存取層級。 多個範圍可以用逗號分隔。 |
| `redirectUrl` | 代表驗證後重新導向使用者的URL。 此值通常設定為應用程式目前的URL。 如果 `redirectUrl` 未提供， `ImsAuthService` 使用用來註冊 `imsClientId` |
| `modalMode` | 表示驗證流程是否應該顯示在強制回應視窗（快顯視窗）中的布林值。 如果設為 `true`，驗證流程會以快顯視窗顯示。 如果設為 `false`，驗證流程會以完整頁面重新載入顯示。 _注意：_ 為了獲得更好的UX，您可以在使用者停用瀏覽器快顯視窗時動態控制此值。 |
| `onImsServiceInitialized` | Adobe IMS驗證服務初始化時呼叫的回呼函式。 此函式採用一個引數， `service`，此物件代表Adobe IMS服務。 另請參閱 [`ImsAuthService`](#imsauthservice-ims-auth-service) 以取得更多詳細資料。 |
| `onAccessTokenReceived` | 回呼函式，當 `imsToken` 從Adobe IMS驗證服務接收。 此函式採用一個引數， `imsToken`，此為代表存取Token的字串。 |
| `onAccessTokenExpired` | 當存取權杖過期時所呼叫的回呼函式。 此函式通常用於觸發新的驗證流程，以取得新的存取權杖。 |
| `onErrorReceived` | 驗證期間發生錯誤時所呼叫的回呼函式。 此函式採用兩個引數：錯誤型別和錯誤訊息。 錯誤型別是代表錯誤型別的字串，而錯誤訊息是代表錯誤訊息的字串。 |

+++

+++**ImsAuthService**
`ImsAuthService` 類別會處理Asset Selector的驗證流程。 其須負責取得 `imsToken` 來自Adobe IMS驗證服務。 此 `imsToken` 用於驗證使用者並授權對的存取權 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 資產存放庫。 ImsAuthService使用 `ImsAuthProps` 屬性來控制驗證流程並註冊各種驗證事件的接聽程式。 您可以使用方便的 [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) 函式以註冊 _ImsAuthService_ 使用資產選擇器的例項。 下列函式適用於 `ImsAuthService` 類別。 不過，如果您使用 _registerAssetsSelectorsAuthService_ 函式，您不需要直接呼叫這些函式。

| 函式名稱 | 說明 |
|---|---|
| `isSignedInUser` | 判斷使用者目前是否已登入服務並據此傳回布林值。 |
| `getImsToken` | 擷取驗證 `imsToken` 適用於目前登入的使用者，可用於驗證其他服務的請求，例如產生資產轉譯。 |
| `signIn` | 起始使用者的登入程式。 此函式使用 `ImsAuthProps` 在快顯視窗或整頁重新載入中顯示驗證 |
| `signOut` | 將使用者登出服務，讓其驗證Token失效，並要求他們再次登入以存取受保護的資源。 叫用此函式將會重新載入目前頁面。 |
| `refreshToken` | 重新整理目前登入使用者的驗證Token，避免其到期並確保受保護資源的存取不中斷。 傳回可用於後續請求的新驗證Token。 |

+++

+++**使用提供的IMS權杖進行驗證**

```
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected asset: ", selection);
    };
    function renderAssetSelectorInline() {
    console.log("initializing Asset Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('asset-selector-container');
    PureJSSelectors.renderAssetSelector(container, props);
    }
    $(document).ready(function() {
    renderAssetSelectorInline();
    });
</script>
```

+++

+++**向IMS服務註冊回呼**

```
// object `imsProps` to be defined as below 
let imsProps = {
    imsClientId: <IMS Client Id>,
        imsScope: "openid",
        redirectUrl: window.location.href,
        modalMode: true,
        adobeImsOptions: {
            modalSettings: {
            allowOrigin: window.location.origin,
},
        useLocalStorage: true,
},
onImsServiceInitialized: (service) => {
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
```

+++

<!--Integration with non-Adobe application content starts here-->

>[!TAB 與非Adobe應用程式整合]

<!--### Integrate Asset Selector with a [!DNL non-Adobe] application {#adobe-non-app-integration}-->

### 先決條件 {#prereqs-non-adobe-app}

如果您整合Asset Selector與非Adobe應用程式，請使用下列先決條件：

* [通訊方法](#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Asset Selector支援驗證 [!DNL Experience Manager Assets] 使用Identity Management系統(IMS)屬性的存放庫，例如 `imsScope` 或 `imsClientID` 將其與非Adobe應用程式整合時。

+++**設定非Adobe應用程式的資產選擇器**
若要為非Adobe應用程式設定「資產選擇器」，您必須先記錄布建的支援票證，然後進行整合步驟。

**記錄支援票證**
透過Admin Console記錄支援票證的步驟：

1. 新增 **具有AEM Assets的資產選擇器** 在票證的標題中。

1. 在說明中提供以下詳細資訊：

   * [!DNL Experience Manager Assets] as a [!DNL Cloud Service] URL （方案ID和環境ID）。
   * 託管非Adobe網頁應用程式的網域名稱。
+++

+++**整合步驟**
使用此範例 `index.html` 整合Asset Selector與非Adobe應用程式時用於驗證的檔案。

使用存取資產選擇器套件 `Script` 標籤，如所示 *第9行* 至 *第11行* 範例的 `index.html` 檔案。

*第14行* 至 *第38行* 的範例說明IMS流程屬性，例如 `imsClientId`， `imsScope`、和 `redirectURL`. 函式要求您至少定義 `imsClientId` 和 `imsScope` 屬性。 如果您未定義 `redirectURL`，則會使用使用者端ID的註冊重新導向URL。

因為您沒有 `imsToken` 已產生，請使用 `registerAssetsSelectorsAuthService` 和 `renderAssetSelectorWithAuthFlow` 函式，如範例的第40行至第50行所示 `index.html` 檔案。 使用 `registerAssetsSelectorsAuthService` 函式在前 `renderAssetSelectorWithAuthFlow` 註冊 `imsToken` 資產選擇器。 [!DNL Adobe] 建議呼叫 `registerAssetsSelectorsAuthService` 例項化元件時。

在中定義驗證和其他Assetsas a Cloud Service存取相關屬性 `const props` 部分，如所示 *第54行* 至 *第60行* 範例的 `index.html` 檔案。

此 `PureJSSelectors` 全域變數，提及於 *第65行*，用於轉譯網頁瀏覽器中的資產選擇器。

資產選擇器呈現於 `<div>` 容器元素，如中所述 *第74行* 至 *第81行*. 此範例使用對話方塊來顯示「資產選取器」。

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

+++

+++**無法存取傳遞存放庫**

>[!TIP]
>
>如果您已使用註冊登入工作流程整合資產選擇器，但仍無法存取傳遞存放庫，請確定已清理瀏覽器Cookie。 否則，您最終將獲得 `invalid_credentials All session cookies are empty` 主控台中的錯誤。

>[!ENDTABS]

## 資產選擇器屬性 {#asset-selector-properties}

您可以使用資產選擇器屬性自訂資產選擇器的呈現方式。下表列出可用於自訂和使用資產選擇器的屬性。

| 屬性 | 類型 | 必要 | 預設 | 說明 |
|---|---|---|---|---|
| *rail* | 布林值 | 否 | false | 若已標籤 `true`，資產選擇器會在左側邊欄檢視中轉譯。 若已標籤 `false`，資產選擇器會在模組檢視中呈現。 |
| *imsOrg* | 字串 | 是 | | Adobe Identity Management System (IMS) ID 是在為您的組織佈建 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 時所指派的。此 `imsOrg` 需要金鑰才能驗證您要存取的組織是否位於Adobe IMS之下。 |
| *imsToken* | 字串 | 否 | | 用於身份驗證的 IMS 持有人語彙基元。`imsToken` 若您使用 [!DNL Adobe] 整合的應用程式。 |
| *apiKey* | 字串 | 否 | | 用於存取 AEM Discovery 服務的 API 金鑰。`apiKey` 若您使用 [!DNL Adobe] 應用程式整合。 |
| *rootPath* | 字串 | 否 | /content/dam/ | 資產選擇器顯示資產的資料夾路徑。`rootPath` 也可以使用封裝形式。例如，假定路徑如下， `/content/dam/marketing/subfolder/`，Asset Selector不允許您周遊任何上層資料夾，只會顯示下層資料夾。 |
| *path* | 字串 | 否 | | 在呈現資產選擇器時，用於導覽到特定資產目錄的路徑。 |
| *filterSchema* | 陣列 | 否 | | 用於設定篩選器屬性的模式。這可用於想要限制資產選擇器中的特定篩選器選項時。 |
| *filterFormProps* | 物件 | 否 | | 指定用於調整搜尋所需的篩選器屬性。例如，MIME 類型 JPG、PNG、GIF。 |
| *selectedAssets* | 陣列 `<Object>` | 否 |                 | 呈現資產選擇器時指定選取的資產。需要包含資產的 id 屬性的物件陣列。例如，在目前的目錄中必須可以使用 `[{id: 'urn:234}, {id: 'urn:555'}]` 資產。如果您需要使用不同的目錄，請為該 `path` 屬性提供一個值。 |
| *acvConfig* | 物件 | 否 | | 包含要覆寫預設值之自訂設定的物件的資產集合檢視屬性。 此外，此屬性也用於 `rail` 屬性以啟用資產檢視器的邊欄檢視。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |                 | 如果OOTB翻譯無法滿足您的應用程式需求，您可以公開介面，讓您透過傳遞自己的自訂本地化值 `i18nSymbols` prop. 透過此介面傳遞值會覆寫所提供的預設翻譯，並改用您自己的翻譯。 若要執行覆寫，您必須傳遞一個有效的 [Message Descriptor](https://formatjs.io/docs/react-intl/api/#message-descriptor) 物件至您想要覆寫的 `i18nSymbols` 金鑰。 |
| *intl* | 物件 | 否 | | 資產選擇器提供預設的OOTB翻譯。 您可以透過 `intl.locale`prop 提供有效的語言環境字串，以選擇翻譯語言。例如：`intl={{ locale: "es-es" }}`</br></br>支援的語言環境字串遵循 [ISO 639 - 代碼](https://www.iso.org/iso-639-language-codes.html)來選擇代表語言標準名稱的代碼。</br></br>支援的語言環境清單：英文 - &#39;en-us&#39; (預設) 西班牙文 - &#39;es-es&#39; 德文 - &#39;de-de&#39; 法文 - &#39;fr-fr&#39; 義大利文 - &#39;it-it&#39; 日文 - &#39;ja-jp&#39;韓文 - &#39;ko-kr&#39; 葡萄牙文 - &#39;pt-br&#39; 中文 (繁體)- &#39;zh-cn&#39; 中文 (台灣) - &#39;zh-tw&#39; |
| *repositoryId* | 字串 | 否 | &#39;&#39; | 資產選擇器從中載入內容的存放庫。 |
| *additionalAemSolutions* | `Array<string>` | 否 | [ ] | 它可讓您新增其他AEM存放庫的清單。 如果此屬性未提供任何資訊，則僅考慮媒體資料庫或 AEM Assets 存放庫。 |
| *hideTreeNav* | 布林值 | 否 |  | 指定顯示或隱藏資產樹導覽側邊欄。那僅用於模組視圖，因此，此屬性在邊欄視圖中沒有影響。 |
| *onDrop* | 函數 | 否 | | 該屬性允許資產的放置功能。 |
| *dropOptions* | `{allowList?: Object}` | 否 | | 使用 &#39;allowList&#39; 設定放置選項。 |
| *colorScheme* | 字串 | 否 | | 為資產選擇器設定主題 (`light`或者`dark`)。 |
| *handleSelection* | 函數 | 否 | | 在選取資產並按一下`Select`模組上的按鈕時，叫用資產項目陣列。此函數僅在模組視圖中叫用。對於邊欄視圖，請使用 `handleAssetSelection`或`onDrop` 函數。範例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 查看[選取的資產類型](#selected-asset-type)以了解詳細資訊。 |
| *handleAssetSelection* | 函數 | 否 | | 在選擇或取消選擇資產時，以項目陣列叫用。當您想要在使用者選擇資產時進行監聽，這是十分實用的功能。範例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 查看[選取的資產類型](#selected-asset-type)以了解詳細資訊。 |
| *onClose* | 函數 | 否 | | 在按下`Close`模組視圖中的按鈕時叫用。這只在`modal`視圖中呼叫，而在`rail`視圖中忽略。 |
| *onFilterSubmit* | 函數 | 否 | | 當使用者變更不同的篩選條件時，以篩選項目叫用。 |
| *selectionType* | 字串 | 否 | single | 一次設定`single`或`multiple`資產選擇方式。 |
| *dragOptions.allowList* | 布林值 | 否 | | 屬性可用來允許或拒絕拖曳無法選取的資產。 |
| *aemTierType* | 字串 | 否 | | 它可讓您選取是否要顯示傳送層級、作者層級或兩者的資產。 <br><br> 語法： `aemTierType:[0: "author" 1: "delivery"` <br><br> 例如，如果兩者 `["author","delivery"]` 之後，存放庫切換器會同時顯示製作和傳送的選項。 |
| *handleNavigateToAsset* | 函數 | 否 | | 這是一個Callback函式，可處理資產的選取專案。 |
| *noWrap* | 布林值 | 否 | | 此 *noWrap* 屬性有助於在側邊欄面板中呈現「資產選擇器」。 如果未提及此屬性，則會轉譯 *對話方塊檢視* 依預設。 |
| *dialogsize* | 小型、中型、大型、全熒幕或全熒幕接管 | 字串 | 選用 | 您可以使用指定的選項指定版面大小，以控制版面。 |
| *colorScheme* | 淺色或深色 | 否 | | 此屬性用於設定Asset Selector應用程式的主題。 您可以選擇淺色或深色主題。 |
| *filterRepoList* | 函數 | 否 |  | 您可以使用 `filterRepoList` 呼叫Experience Manager存放庫並傳回已篩選的存放庫清單的回呼函式。 |

## 使用資產選擇器屬性的範例 {#usage-examples}

您可以定義 `index.html` 檔案裡的資產選擇器[屬性](#asset-selector-properties)，以便自訂在應用程式內的資產選擇器顯示。

### 範例 1：邊欄視圖中的資產選擇器

![rail-view-example](assets/rail-view-example-vanilla.png)

如果資產選擇器的值 `rail` 設為 `false` 或屬性中未提及，資產選擇器預設會顯示在模組檢視中。 此 `acvConfig` 屬性允許進行一些深入設定，例如拖放。 造訪 [啟用或停用拖放](#enable-disable-drag-and-drop) 瞭解的使用方式 `acvConfig` 屬性。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### 範例 2：中繼資料彈出視窗

使用各種屬性定義您要使用資訊圖示檢視的資產中繼資料。資訊彈出視窗提供有關資產或資料夾的資訊集合，包括資產的標題、尺寸、修改日期、位置和說明。在下面的範例中，各種屬性用於顯示資產的中繼資料，例如，`repo:path`屬性指定資產的位置<!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->。

![metadata-popover-example](assets/metadata-popover.png)

### 範例 3：邊欄視圖中的自訂篩選器屬性

除了多面向搜尋之外，Assets選擇器可讓您自訂各種屬性，以縮小您的搜尋範圍 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 應用程式。 新增下列程式碼，在您的應用程式中新增自訂的搜尋篩選器。 在下面的範例中，`Type Filter`在影像、文件或影片中篩選資產類型，或為搜尋新增篩選器類型的搜尋。

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

## 功能設定程式碼片段{#code-snippets}

在中定義先決條件 `index.html` 檔案或應用程式實作中的類似檔案，用於定義存取的驗證詳細資訊 [!DNL Experience Manager Assets] 存放庫。 完成後，您可以視需求新增程式碼片段。

### 自訂篩選器面板 {#customize-filter-panel}

您可以在中新增下列程式碼片段 `assetSelectorProps` 物件以自訂濾鏡面板：

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    }},
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

### 在強制回應檢視中自訂資訊 {#customize-info-in-modal-view}

您可以按一下「 」，自訂資產的詳細資料檢視 ![資訊圖示](assets/info-icon.svg) 圖示。 執行以下程式碼：

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path'
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

### 啟用或停用拖放模式 {#enable-disable-drag-and-drop}

將下列屬性新增至 `assetSelectorProp` 以啟用拖放模式。 若要停用拖放，請將 `true` 引數搭配 `false`.

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

### 選取資產 {#selection-of-assets}

選取的資產類型是一個物件陣列，包含使用 `handleSelection`、`handleAssetSelection` 和 `onDrop` 函數時的資產資訊。

執行以下步驟，設定選取單一或多個資產的選項：

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

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
        'https://ns.adobe.com/adobecloud/rel/rendition': Array<{
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

| 屬性 | 類型 | 說明 |
|---|---|---|
| *repo:repositoryId* | 字串 | 儲存資產之存放庫的唯一識別碼。 |
| *repo:id* | 字串 | 資產的唯一識別碼。 |
| *repo:assetClass* | 字串 | 資產的分類 (例如影像或影片、文件)。 |
| *repo:name* | 字串 | 資產的名稱，包括檔案副檔名。 |
| *repo:size* | 數字 | 資產的大小，以位元組計。 |
| *repo:path* | 字串 | 資產在存放庫中的位置。 |
| *repo:ancestors* | `Array<string>` | 存放庫中資產的上階項目陣列。 |
| *repo:state* | 字串 | 存放庫中資產的目前狀態（例如，作用中、已刪除等）。 |
| *repo:createdBy* | 字串 | 建立資產的使用者或系統。 |
| *repo:createDate* | 字串 | 建立資產的日期與時間。 |
| *repo:modifiedBy* | 字串 | 上次修改資產的使用者或系統。 |
| *repo:modifyDate* | 字串 | 上次修改資產的日期和時間。 |
| *dc:format* | 字串 | 資產的格式，例如檔案型別(例如JPEG、PNG等)。 |
| *tiff:imageWidth* | 數字 | 資產的寬度。 |
| *tiff:imageLength* | 數字 | 資產的高度。 |
| *computedMetadata* | `Record<string, any>` | 代表貯體的一個物件，可存放各種類型之所有資產中繼資料 (存放庫、應用程式或嵌入式中繼資料)。 |
| *_links* | `Record<string, any>` | 相關資產的超媒體連結。包括中繼資料和轉譯等資源的連結。 |
| *連結(_L)。<https://ns.adobe.com/adobecloud/rel/rendition>* | `Array<Object>` | 包含有關資產轉譯資訊的物件陣列。 |
| *連結(_L)。<https://ns.adobe.com/adobecloud/rel/rendition[].href>* | 字串 | 轉譯的 URI。 |
| *連結(_L)。<https://ns.adobe.com/adobecloud/rel/rendition[].type>* | 字串 | 轉譯的 MIME 類型。 |
| *連結(_L)。<https://ns.adobe.com/adobecloud/rel/rendition[].'repo:size>『* | 數字 | 轉譯的大小，以位元組計。 |
| *連結(_L)。<https://ns.adobe.com/adobecloud/rel/rendition[].width>* | 數字 | 轉譯的寬度。 |
| *連結(_L)。<https://ns.adobe.com/adobecloud/rel/rendition[].height>* | 數字 | 轉譯的高度。 |

如需完整的屬性清單和詳細範例，請造訪[資產選擇器代碼範例 ](https://github.com/adobe/aem-assets-selectors-mfe-examples)。

## 使用物件綱要處理資產選擇 {#handling-selection}

`handleSelection` 屬性用於處理資產選擇器中單個或多個資產選擇。下面的範例說明使用 `handleSelection` 的語法。

![handle-selection](assets/handling-selection.png)

## 停用資產的選擇 {#disable-selection}

「停用選取」可用來隱藏或停用資產或資料夾無法選取的功能。 它會隱藏卡片或資產中的「選取」核取方塊，使其無法選取。 若要使用此功能，您可以宣告要在陣列中停用的資產或資料夾位置。 例如，如果您要停用選取出現在第一個位置的資料夾，可以新增下列程式碼：
`disableSelection: [0]:folder`

您可以為陣列提供您想要停用的mime型別（例如影像、資料夾、檔案或其他mime型別，例如image/jpeg）清單。 您宣告的MIME型別會對應到 `data-card-type` 和 `data-card-mimetype` 資產的屬性。

此外，已停用選取範圍的資產是可拖曳的。 若要停用特定資產型別的拖放功能，您可使用 `dragOptions.allowList` 屬性。

停用選取的語法如下：

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> 若是資產，選取核取方塊會隱藏；若是資料夾，則資料夾無法選取，但提及資料夾的導覽仍會顯示。

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

Asset Selector也可讓您切換資產選取的存放庫。 您可以從左側面板中的下拉清單中選擇您要的存放庫。下拉清單中可用的存放庫選項是根據`repositoryId``index.html`檔案中定義的屬性。其基礎是登入使用者存取之所選IMS組織的環境。 消費者可以傳遞一個偏好的`repositoryID`，而且在該情況下，資產選擇器將停止呈現 repo 切換器，並僅從指定的存放庫呈現資產。
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

除了全文檢索搜尋之外，「資產選擇器」可讓您使用自訂搜尋功能來搜尋檔案中的資產。 您可以在模組視圖和邊欄視圖模式下，使用自訂搜尋篩選器。

![custom-search](assets/custom-search1.png)

您也可以建立預設的搜尋篩選器，以儲存您經常搜尋的欄位，以供之後使用。若要為資產建立自訂搜尋，您可以使用 `filterSchema` 屬性。

### 搜尋列 {#search-bar}

「資產選擇器」可讓您在選取的存放庫中執行資產的全文搜尋。 例如，如果您在搜尋列中鍵入關鍵字 `wave`，就會顯示中繼資料屬性中提及 `wave` 關鍵字的所有資產。

### 排序 {#sorting}

您可以按資產的名稱、維度或大小對資產選擇器中的資產進行排序。您可以依照遞增或遞減順序排序資產。

### 視圖的類型 {#types-of-view}

「資產選取器」可讓您以四種不同的檢視檢視檢視資產：

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
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It lets you control the display of various text or symbols as per your choice.
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
*   **Open in media library** Lets you open the asset in media library.
*   **Upload** Lets you upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector lets you know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->



<!--Best Practice-->
<!--
+++**Control default selection of the filter**
You can make the selection of filter default by implementing the following code snippet:

```
"defaultValue": [
    "image/*",
    "application/*"
],

{
    "label": "Documents",
    "value": "application/*"
}
```

+++
-->
