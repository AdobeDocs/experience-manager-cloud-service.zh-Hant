---
title: 整合內容片段選擇器與非Adobe或第三方應用程式
description: 整合內容片段選擇器與各種Adobe、非Adobe和第三方應用程式。
role: Admin, User, Developer
source-git-commit: 3af1a89489af96bf9c9908aea7fb20883956517b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# 與非Adobe應用程式整合 {#integration-with-non-adobe-application}

內容片段選擇器可讓您整合各種非Adobe或協力廠商的應用程式，好讓他們順暢地共同作業。

## 先決條件 {#prerequisites}

如果您要將內容片段選擇器與非Adobe應用程式整合，請使用下列先決條件：

* [先決條件](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

當您將其與非Adobe應用程式整合時，內容片段選擇器支援使用Identity Management System (IMS)屬性（例如`imsScope`或`imsClientID`）來驗證Adobe Experience Manager (AEM) as a Cloud Service存放庫。

## 設定非Adobe應用程式的內容片段選擇器 {#configure-content-fragment-selector-for-a-non-adobe-application}

若要為非Adobe應用程式設定內容片段選擇器，您必須先記錄布建的支援票證，才能繼續整合步驟。

### 記錄支援票證 {#logging-a-support-ticket}

透過 Admin Console 記錄支援服務單的步驟：

1. 在票證標題中新增具有AEM片段&#x200B;**的**&#x200B;內容片段選擇器。

1. 在說明中提供以下詳細資訊：

   * Experience Manager as a Cloud Service URL （方案ID和環境ID）。
   * 託管非Adobe Web應用程式的網域名稱。

## 整合步驟 {#integration-steps}

將內容片段選擇器與非Adobe應用程式整合時，請使用下列範例`index.html`檔案進行驗證：

* 使用`Script`標籤存取內容片段選擇器套件。

* 定義IMS流程屬性，例如`imsClientId`、`imsScope`和`redirectURL`。

   * 函式要求您至少定義`imsClientId`和`imsScope`屬性之一。
   * 如果您未定義`redirectURL`的值，則會使用使用者端ID的註冊重新導向URL。

* 由於範例未產生`imsToken`，請使用`registerFragmentsSelectorsAuthService`和`renderFragmentSelectorWithAuthFlow`函式。

   * 使用`registerFragmentsSelectorsAuthService`之前的`renderFragmentSelectorWithAuthFlow`函式，以內容片段選取器註冊`imsToken`。
   * Adobe建議您在具現化元件時呼叫`registerFragmentsSelectorsAuthService`。

* 在`const props`區段中定義驗證和其他片段as a Cloud Service存取相關屬性。
* `PureJSContentFragmentSelectors`全域變數可用來轉譯網頁瀏覽器中的內容片段選取器。
* 內容片段選擇器在`<div>`容器元素上呈現。 此範例使用對話方塊來顯示內容片段選擇器。

**範例`ìndex.html`**

```html {line-numbers="true"}
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <link rel="icon" type="image/svg+xml" href="/vite.svg" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>testing-cf-mfe-integration-with-3rd-party-app</title>
        <script
            id="content-fragments-selector"
            src="https://experience.adobe.com/solutions/CQ-sites-content-fragment-selector/static-assets/resources/content-fragment-selector.js"
        ></script>
        <script>
            const imsProps = {
                imsClientId: '<IMS_CLIENT_ID>',
                imsScope:
                    'additional_info.projectedProductContext, AdobeID, openid, read_organizations',
                redirectUrl: window.location.href,
                onImsServiceInitialized: (service) => {
                    // invoked when the ims service is initialized and is ready
                    console.log('onImsServiceInitialized', service);
                },
                onAccessTokenReceived: (token) => {
                    console.log('onAccessTokenReceived', token);
                },
                onAccessTokenExpired: () => {
                    console.log('onAccessTokenError');
                    // re-trigger sign-in flow
                },
                onErrorReceived: (type, msg) => {
                    console.log('onErrorReceived', type, msg);
                },
            };

            function load() {
                const registeredTokenService =
                    PureJSContentFragmentSelectors.registerContentFragmentSelectorAuthService(
                        imsProps
                    );
                imsInstance = registeredTokenService;
            }

            // initialize the IMS flow before attempting to render the content fragment selector
            load();

            // function that will render the content fragment selector
            function renderContentFragmentSelectorWithAuthFlow() {
                const contentFragmentSelectorDialog = document.getElementById(
                    'content-fragment-selector-dialog'
                );

                const contentFragmentSelectorProps = {
                    inventoryViewToggleEnabled: true,
                    isOpen: true,
                    noWrap: false,
                    orgId: 'YOUR_ORG_ID@AdobeOrg',
                    // repoId: "author-p12345-e67890.adobeaemcloud.com", // if wanted to restrict to a specific repo
                    runningInUnifiedShell: false,
                    onDismiss: () => contentFragmentSelectorDialog.close(),
                    onSubmit: ({ contentFragments }) => {
                        const selectedContentFragment = contentFragments[0];
                        alert(selectedContentFragment.path);
                    },
                };
                // container element on which you want to render the ContentFragmentSelector component
                const container = document.getElementById('content-fragment-selector');

                /// Use the PureJSContentFragmentSelectors in globals to render the ContentFragmentSelector component
                PureJSContentFragmentSelectors.renderContentFragmentSelectorWithAuthFlow(
                    container,
                    contentFragmentSelectorProps,
                    () => contentFragmentSelectorDialog.showModal()
                );
            }
        </script>
    </head>
    <body>
        <div>
            <button onclick="renderContentFragmentSelectorWithAuthFlow()">
                Content Fragment Selector - Select Content Fragments with Ims Flow
            </button>
        </div>
        <dialog id="content-fragment-selector-dialog">
            <div
                id="content-fragment-selector"
                style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px"
            ></div>
        </dialog>
    </body>
</html>
```

## 無法存取傳遞存放庫 {#unable-to-access-delivery-repository}

如果您已使用註冊登入工作流程整合內容片段選擇器，但仍無法存取傳遞存放庫，請確定瀏覽器Cookie已清除。

否則，您可能會在主控台中看到`invalid_credentials All session cookies are empty`錯誤。
