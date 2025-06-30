---
title: 整合資產選擇器與非Adobe或第三方應用程式
description: 整合資產選擇器與各種Adobe、非Adobe及協力廠商應用程式。
role: Admin, User
exl-id: 55848de0-aff2-42a0-b959-c771235d9425
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 9%

---

# 與非Adobe應用程式整合 {#integrate-asset-selector-non-adobe-app}

Asset Selector可讓您使用各種非Adobe或協力廠商應用程式進行整合，好讓他們順暢地共同作業。

## 先決條件 {#prereqs-non-adobe-app}

如果您整合Asset Selector與非Adobe應用程式，請使用下列先決條件：

* [通訊方法](/help/assets/overview-asset-selector.md#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Asset Selector支援使用Identity Management System (IMS)屬性（例如`imsScope`或`imsClientID`）驗證[!DNL Experience Manager Assets]存放庫(當您將其與非Adobe應用程式整合時)。

## 設定非Adobe應用程式的資產選擇器 {#configure-non-adobe-app}

若要為非Adobe應用程式設定Asset Selector，您必須先記錄布建的支援票證，然後進行整合步驟。

### 記錄支援票證 {#log-a-support-ticket}

透過 Admin Console 記錄支援服務單的步驟：

1. 在票證標題中新增具有AEM Assets **的**&#x200B;資產選擇器。

1. 在說明中提供以下詳細資訊：

   * [!DNL Experience Manager Assets]作為[!DNL Cloud Service] URL （方案ID和環境ID）。
   * 託管非Adobe Web應用程式的網域名稱。

## 整合步驟 {#non-adobe-app-integration-steps}

將Asset Selector與非Adobe應用程式整合時，請使用這個範例`index.html`檔案進行驗證。

使用`Script`標籤存取Asset Selector套件，如範例`index.html`檔案的&#x200B;*第9*&#x200B;行到&#x200B;*第11*&#x200B;行所示。

範例的&#x200B;*第14*&#x200B;行到&#x200B;*第38*&#x200B;行說明IMS流程屬性，例如`imsClientId`、`imsScope`和`redirectURL`。 函式要求您至少定義`imsClientId`和`imsScope`屬性之一。 如果您未定義`redirectURL`的值，則會使用使用者端ID的註冊重新導向URL。

由於您尚未產生`imsToken`，請使用`registerAssetsSelectorsAuthService`和`renderAssetSelectorWithAuthFlow`函式，如範例`index.html`檔案的第40行至第50行所示。 使用`renderAssetSelectorWithAuthFlow`之前的`registerAssetsSelectorsAuthService`函式，以透過資產選擇器註冊`imsToken`。 [!DNL Adobe]建議您在具現化元件時呼叫`registerAssetsSelectorsAuthService`。

在`const props`區段中定義驗證和其他Assets as a Cloud Service存取相關屬性，如範例`index.html`檔案的&#x200B;*行54*&#x200B;到&#x200B;*行60*&#x200B;所示。

在&#x200B;*第65*&#x200B;行中提到的`PureJSSelectors`全域變數是用來在網頁瀏覽器中轉譯Asset Selector。

資產選擇器已在`<div>`容器元素上呈現，如&#x200B;*第74*&#x200B;行到&#x200B;*第81*&#x200B;行中所述。 此範例使用對話方塊來顯示「資產選取器」。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8">
    <title>Asset Selectors</title>
    <link rel="stylesheet" href="index.css">
    <script id="asset-selector"
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
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
            PureJSSelectors.renderAssetSelectorWithAuthFlow(container, assetSelectorProps, () =>
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

## 無法存取傳遞存放庫 {#unable-to-access-delivery-repository}

>[!TIP]
>
>如果您已使用註冊登入工作流程整合資產選擇器，但仍無法存取傳遞存放庫，請確定已清理瀏覽器Cookie。 否則，您會在主控台中收到`invalid_credentials All session cookies are empty`錯誤。

>[!MORELIKETHIS]
>
>* [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
>* [整合資產選擇器與具備 OpenAPI 功能的 Dynamic Media](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [資產選擇器自訂](/help/assets/asset-selector-customization.md)
