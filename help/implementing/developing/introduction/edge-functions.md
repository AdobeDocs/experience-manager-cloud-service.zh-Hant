---
title: AEM Edge功能
description: 瞭解如何使用AEM Edge功能在CDN層執行JavaScript，以接近使用者的個人化、安全性和動態體驗。
feature: Developing, Edge Delivery Services
role: Developer
source-git-commit: f8000bef01d6b72fb3ac2ae81be9fc19ed1a67d1
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 3%

---


# AEM Edge功能 {#aem-edge-functions}

>[!IMPORTANT]
>
>AEM Edge功能是&#x200B;**測試版**&#x200B;功能。 功能和檔案可能會有所變更，恕不另行通知。 若要加入搶先體驗計畫並提供意見回饋，請寄電子郵件至[aemcs-edge-functions-feedback@adobe.com](mailto:aemcs-edge-functions-feedback@adobe.com)。

AEM Edge功能可讓您在CDN層執行JavaScript，讓資料處理更接近於一般使用者。 這能縮短延遲時間，並提供快速回應、動態的體驗，無需往返至您的來源。

常見使用案例包含：

- 根據地理位置、裝置型別或使用者屬性等資訊製作個人化內容
- 做為 CDN 和您來源之間的中介軟體
- 在第三方API到達瀏覽器之前重新格式化或彙總回應
- 使用從多個後端拼接的內容，在邊緣構成和服務伺服器轉譯的HTML

AEM Edge函式與Edge Delivery Services和AEM雲端服務Java棧疊相容。

## 主要優點 {#key-benefits}

| 優點 | 說明 |
|---|---|
| **效能** | 透過邊緣SSR快速TTFB傳回完全轉譯的HTML。 透過平行擷取和最佳化的網路躍點進行的低延遲API呼叫。 |
| **SEO /地理** | 伺服器HTML在首次抓取時編列索引。 完全演算的內容已可供AI爬蟲使用。 |
| **安全性** | 在伺服器端保留API認證，在使用者端JavaScript中隱藏。 向身分提供者進行驗證並限制內容存取。 |
| **個人化** | 根據地理和裝置訊號在頁面載入之前個人化內容。 在邊緣執行對象查詢，以取得目標傳送。 |

## 先決條件 {#prerequisites}

- AEM as a Cloud Service環境
- 您的AEM環境製作執行個體上的Cloud Service管理員產品設定檔，**或** Edge Delivery Services網站的Admin Console中的Cloud Manager部署管理員角色
- [Node.js和npm](https://nodejs.org/)

## 設定 {#setup}

### 安裝Adobe CLI {#install-adobe-cli}

安裝Adobe Developer CLI (`aio`)：

```bash
npm install -g @adobe/aio-cli
```

安裝AEM Edge函式外掛程式：

```bash
aio plugins install @adobe/aio-cli-plugin-aem-edge-functions
```

驗證並設定您環境的外掛程式：

```bash
aio login
aio aem edge-functions setup
```

setup指令會提示您登入，然後選取您要使用AEM Edge函式的AEM環境。

### 原地複製樣板 {#boilerplate}

將[aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate)複製到您自己的存放庫，然後安裝相依性：

```bash
npm install
```

## 建立您的第一個函式 {#create-your-function}

AEM Edge功能服務在YAML設定檔案中宣告，並透過Cloud Manager設定管道部署。

### 1.設定設定管道 {#configuration-pipeline}

在建立邊緣函式之前，請確定Cloud Manager中有您環境的設定管道。 如果沒有，請先建立[設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

>[!NOTE]
>
>如果您使用快速開發環境(RDE)，您可以直接使用`aio aem rde:install -t env-config ./config`部署設定，而不是透過設定管道。

### 2.宣告您的Edge功能服務 {#declare-services}

在組態目錄中建立名為`edgeFunctions.yaml`的檔案：

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  services:
    - name: first-function
    - name: second-function
    # Uncomment to enable secrets
    # secrets:
    #   - key: API_TOKEN
    #     value: ${{ API_TOKEN_SECRET }}
```

此設定支援最多三個服務。 最上層索引鍵為：

| 索引鍵 | 說明 |
|---|---|
| `services` | 邊緣函式服務清單，每個服務都以`name`識別。 |
| `configs` | 公開（作為環境變數）給所有邊緣函式服務的索引鍵/值組。 |
| `secrets` | 參考Cloud Manager密碼的金鑰/值組已公開至所有邊緣函式服務。 |

### 3.新增CDN來源選擇器規則 {#cdn-routing}

透過透過原始選擇器規則將CDN流量路由到它們來叫用Edge函式。 將下列專案新增至您的`cdn.yaml`設定檔（如果不存在則建立一個）：

```yaml
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-to-first-function
        when: { reqProperty: path, equals: "/weather" }
        action:
          type: selectAemOrigin
          originName: edgefunction-first-function
      - name: route-to-second-function
        when: { reqProperty: path, equals: "/hello-world" }
        action:
          type: selectAemOrigin
          originName: edgefunction-second-function
```

原始選擇器規則可讓您根據CDN規則引擎提供的任何條件（例如特定路徑、網域或請求標題），將流量路由至邊緣函式。 如需完整的規則語法，請參閱[來源選取器](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors)。

### 4.部署設定 {#deploy-configuration}

將`edgeFunctions.yaml`和`cdn.yaml`認可到您的Cloud Manager Git存放庫並觸發設定管道。 管道成功完成後，您的邊緣函式端點可在以下位置使用：

- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/weather`
- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/hello-world`

其中`pXXXXX-eYYYYY`為您的環境座標。 如果已設定自訂網域，則也可以在這些網域路徑（例如，`example.com/weather`）存取函式。

## 建置和部署AEM Edge函式程式碼 {#build-deploy}

### 建置 {#build}

封裝您的邊緣函式程式碼以進行部署：

```bash
aio aem edge-functions build
```

### 部署 {#deploy}

將內建套件部署至已命名的邊緣函式服務。 `function-name`引數必須符合`name`中的`edgeFunctions.yaml`值：

```bash
aio aem edge-functions deploy <function-name>
```

## 本機開發 {#local-development}

### 本機執行 {#local-run}

在`http://127.0.0.1:7676`啟動本機開發伺服器：

```bash
aio aem edge-functions serve
```

請參閱此[計算JavaScript檔案](https://www.fastly.com/documentation/guides/compute/javascript/)，瞭解本機執行階段支援的詳細資訊。

### 測試 {#test}

使用[Mocha](https://mochajs.org/)執行測試套裝：

```bash
npm run test
```

### 遠端偵錯 {#remote-debugging}

Adobe Managed CDN不會公開遠端偵錯工具，但會公開記錄串流。 追蹤已部署功能的記錄，以直接在終端機接收`console.log`輸出：

```bash
aio aem edge-functions tail-logs <function-name>
```

## 設定引用 {#configuration-reference}

### 來源 {#origins}

預設情況下，邊緣函式可從任何來源擷取。 若要將函式限製為定義的來源集合，請在`origins`中的`edgeFunctions.yaml`下宣告它們：

```yaml
origins:
  - name: my-origin-name
    domain: example.com
```

使用`backend`擷取選項，在函式程式碼中參考具名來源：

```js
const request = new Request("https://example.com/test");
const response = await fetch(request, { backend: "my-origin-name" });
```

### 服務設定 {#service-configuration}

在`configs`中使用`edgeFunctions.yaml`索引鍵向函式公開環境變數。 值儲存在名為`config_default`的設定存放區：

```yaml
configs:
  - key: LOG_LEVEL
    value: DEBUG
```

讀取函式程式碼中的設定值：

```js
import { ConfigStore } from "fastly:config-store";

const config = new ConfigStore('config_default');
const logLevel = config.get('LOG_LEVEL') || 'info';
```

>[!NOTE]
>
>- 設定存放區一律名為`config_default`。
>- 金鑰名稱區分大小寫。
>- 此設定存放區會在相同環境中的所有邊緣函式服務之間共用。

### 服務密碼 {#service-secrets}

在`edgeFunctions.yaml`中參考未儲存的秘密。 `value`欄位必須使用`${{SECRET_REFERENCE}}`語法指向Cloud Manager機密。 先在Cloud Manager中定義基礎機密 — 請參閱[Cloud Manager機密變數](/help/implementing/cloud-manager/environment-variables.md)。

```yaml
secrets:
  - key: API_TOKEN
    value: ${{ API_TOKEN_SECRET }}
```

使用範本中的`SecretStoreManager`協助程式擷取函式程式碼中的秘密：

```js
import { SecretStoreManager } from "./lib/config";

const apiToken = await SecretStoreManager.getSecret('API_TOKEN');
```

>[!NOTE]
>
>- 秘密存放區一律名為`secret_default`。
>- 金鑰名稱區分大小寫。
>- 秘密一旦建立就不可改變。
>- 機密存放區會在相同環境中的所有邊緣功能服務之間共用。

### 記錄 {#logging}

AEM Edge功能與[AEM記錄轉送](/help/implementing/developing/introduction/log-forwarding.md)功能整合。 在您的`logForwarding.yaml`旁邊建立`edgeFunctions.yaml`檔案：

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["rde", "dev", "stage", "prod"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

使用函式程式碼中的記錄器來寫入結構化記錄專案：

```js
import { Logger } from "fastly:logger";

const logger = new Logger("customerSplunk");
logger.log(JSON.stringify({
  method: event.request.method,
  url: event.request.url
}));
```

>[!NOTE]
>
>CDN記錄（包括AEM Edge函式記錄專案）可從Java棧疊環境的Cloud Manager下載，但無法用於Edge Delivery Services網站。
>
