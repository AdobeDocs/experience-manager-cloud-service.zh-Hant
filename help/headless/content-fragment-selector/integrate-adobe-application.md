---
title: 整合內容片段選擇器與Adobe應用程式
description: 整合內容片段選擇器與各種Adobe應用程式。
role: Admin, User, Developer
source-git-commit: a16d9e9fa6483a89283c595372abcc437d1d962e
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# 整合內容片段選擇器與Adobe應用程式 {#integrate-content-fragment-selector-with-adobe-application}

內容片段選擇器可讓您整合各種Adobe應用程式，讓這些應用程式緊密合作。

## 先決條件 {#prerequisites}

如果您整合內容片段選擇器與Adobe應用程式，請使用下列先決條件：

* [先決條件](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsOrg
* imsToken
* apikey

## 整合內容片段選擇器與Adobe應用程式 {#integrate-content-fragment-selector-with-an-adobe-application}

下列範例示範如何在Unified Shell下執行Adobe應用程式時，或您已針對驗證產生`imsToken`時，使用內容片段選擇器。

使用`script`標籤在您的程式碼中包含內容片段選擇器套件，如下列範例所示。

* 載入指令碼後，`PureJSContentFragmentSelectors`全域變數即可使用。
* 定義內容片段選擇器[屬性](/help/headless/content-fragment-selector/properties.md)：

   * 在Adobe應用程式中驗證時需要`imsOrg`和`imsToken`屬性
   * `handleSelection`屬性用於處理選取的片段。

* 若要呈現內容片段選擇器，請呼叫`renderFragmentSelector`函式。
* 內容片段選擇器會顯示在`<div>`容器元素中。

依照這些步驟，您可以在Adobe應用程式中使用內容片段選擇器。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Fragment Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-fragmentss-selectors/static-fragments/resources/fragments-selectors.js"></script>
    <script>
        // get the container element in which we want to render the FragmentSelector component
        const container = document.getElementById('fragment-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const fragmentSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (fragmentss: SelectedFragmentType[]) => {},
        };
        // Call the `renderFragmentSelector` available in PureJSContentFragmentSelectors globals to render FragmenttSelector
        PureJSContentFragmentSelectors.renderFragmentSelector(container, fragmentSelectorProps);
    </script>
</head>

<body>
    <div id="fragment-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

### ImsAuthProps {#imsauthprops}

`ImsAuthProps`屬性定義內容片段選擇器用來取得`imsToken`的驗證資訊和流程。 透過設定這些屬性，您可以控制驗證流程的行為方式，並為各種驗證事件註冊接聽程式。

如需屬性詳細資料，請參閱[ImsAuthProps屬性](/help/headless/content-fragment-selector/properties.md#imsauthprops-properties)

### ImsAuthService {#imsauthservice}

`ImsAuthService`類別會處理片段選擇器的驗證流程。 其負責從Adobe IMS驗證服務取得`imsToken`。 `imsToken`用於驗證使用者並授權存取AEM as a Cloud Service存放庫。 `ImsAuthService`使用`ImsAuthProps`屬性來控制驗證流程並註冊各種驗證事件的接聽程式。 您可以使用`registerFragmentsSelectorsAuthService`函式向片段選擇器註冊`ImsAuthService`執行個體。 `ImsAuthService`類別上有以下可用函式。 不過，如果您使用`registerFragmentsSelectorsAuthService`函式，則不需要直接呼叫這些函式。

如需屬性詳細資料，請參閱[ImsAuthService屬性](/help/headless/content-fragment-selector/properties.md#imsauthservice-properties)

### 使用提供的IMS權杖進行驗證 {#validation-with-provided-ims-token}

```javascript
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected fragment: ", selection);
    };
    function renderFragmentSelectorInline() {
    console.log("initializing Fragment Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('fragment-selector-container');
    PureJSContentFragmentSelectors.renderFragmentSelector(container, props);
    }
    $(document).ready(function() {
    renderFragmentSelectorInline();
    });
</script>
```

### 向IMS服務註冊回呼 {#register-callbacks-to-ims-service}

```java
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
