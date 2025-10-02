---
title: 使用設定管道
description: 瞭解如何使用設定管道在AEM as a Cloud Service中部署不同的設定，例如記錄轉送設定、清除相關的維護任務和各種CDN設定。
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: 1d29700d8cbb9cd439ec909687c34db06a8090e4
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 3%

---

# 使用設定管道 {#config-pipelines}

瞭解如何使用設定管道在AEM as a Cloud Service中部署不同的設定，例如記錄轉送設定、清除相關的維護任務和各種CDN設定。

## 概觀 {#overview}

Cloud Manager設定管道將設定檔案（以YAML格式建立）部署到目標環境。 AEM as a Cloud Service中的許多功能可以這樣設定，包括記錄轉送、清除相關的維護任務和數個CDN功能。

對於&#x200B;**發佈傳遞**&#x200B;專案，可透過Cloud Manager將設定管道部署到開發、中繼和生產環境型別。 組態檔可以使用[命令列工具](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)部署至快速開發環境(RDE)。

也可以透過Cloud Manager為&#x200B;**Edge Delivery**&#x200B;專案部署設定管道。

本檔案的以下章節提供了有關如何使用設定管道以及如何為其構建配置的重要資訊的概述。 它說明在配置管道所支援的所有功能或功能子集之間共用的一般概念。

* [支援的組態](#configurations) — 可以使用組態管道部署的組態清單
* [建立和管理設定管道](#creating-and-managing) — 如何建立設定管道
* [通用語法](#common-syntax) — 跨組態共用的語法
* [資料夾結構](#folder-structure) — 說明組態預期的結構組態管道
* [秘密環境變數](#secret-env-vars) — 使用環境變數不洩露設定中的秘密的範例
* [秘密管道變數](#secret-pipeline-vars) — 在Edge Delivery Services專案前使用環境變數不要洩露設定中的秘密的範例

## 支援的設定 {#configurations}

下表提供這類設定的完整清單，以及描述其不同設定語法和其他資訊的專用檔案的連結。

| 類型 | YAML `kind`值 | 說明 | 發佈傳遞 | Edge Delivery |
|---|---|---|---|---|
| [流量篩選器規則，包括WAF](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | 宣告規則以封鎖惡意流量 | X | X |
| [要求轉換](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | 宣告規則以轉換流量請求的形狀 | X | X |
| [回應轉換](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | 宣告規則以轉換指定要求的回應形狀 | X | X |
| [伺服器端重新導向](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) | `CDN` | 宣告301/302樣式的伺服器端重新導向 | X | X |
| [來源選取器](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | 宣告將流量路由到不同後端的規則，包括非Adobe應用程式 | X | X |
| [CDN錯誤頁面](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | 如果無法連線AEM來源，並參考設定檔案中自行託管靜態內容的位置，則覆寫預設錯誤頁面 | X |  |
| [CDN清除](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | 宣告用來清除CDN的清除API金鑰 | X |  |
| [客戶管理的CDN HTTP權杖](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | 宣告從客戶CDN呼叫Adobe CDN所需的X-AEM-Edge-Key值 | X |  |
| [基本驗證](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | 為保護特定URL的基本驗證對話方塊宣告使用者名稱和密碼。 | X | X |
| [版本清除維護任務](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | 透過在應清除內容版本的時機周圍宣告規則來最佳化AEM存放庫 | X |  |
| [稽核記錄清除維護任務](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | 最佳化AEM稽核記錄，透過在應清除記錄的時間周圍宣告規則來提高效能 | X |  |
| [記錄檔轉送](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | 設定可將記錄轉送至不同目的地的端點和認證，包括Azure Blob Storage、Datadog、HTTPS、Elasticsearch、Splunk | X | X |
| [正在註冊使用者端ID](/help/implementing/developing/open-api-based-apis.md) | `API` | 註冊使用者端ID，將Adobe Developer Console API專案範圍設定為特定AEM環境。 使用需要驗證的OpenAPI型API時需要此專案 | X |  |

## 建立和管理設定管道 {#creating-and-managing}

有關如何建立和設定&#x200B;**發佈傳遞**&#x200B;設定管道的資訊，請參閱[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)。 在Cloud Manager中建立設定管道時，在設定管道時請務必選取&#x200B;**目標部署**，而不是&#x200B;**完整棧疊代碼**。 如前所述，RDE的組態是使用[命令列工具](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)部署，而非管道。

有關如何建立和設定&#x200B;**Edge Delivery**&#x200B;設定管道的資訊，請參閱[新增Edge Delivery管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)文章。

## 一般語法 {#common-syntax}

每個設定檔案都會以類似下列範常式式碼片段的屬性開頭：

```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
```

| 屬性 | 說明 | 預設 |
|---|---|---|
| `kind` | 字串；決定組態型別，如記錄轉送、流量篩選規則或要求轉換 | 必要，無預設值 |
| `version` | 代表結構描述版本的字串 | 必要，無預設值 |
| `envTypes` | 這個字串陣列是`metadata`節點的子屬性。 對於&#x200B;**發佈傳遞**，可能的值是dev、stage、prod或任何組合，它決定要處理組態的環境型別。 例如，如果陣列僅包含`dev`，則不會在Stage或Prod環境中載入組態，即使組態已部署於其中亦然。 對於&#x200B;**Edge Delivery**，只應使用`prod`的值 | 所有環境型別，也就是(dev、stage、prod)用於「發佈傳送」，或只是prod用於Edge Delivery |

您可以使用`yq`公用程式在本機驗證組態檔的YAML格式（例如，`yq cdn.yaml`）。

## 資料夾結構 {#folder-structure}

名稱為`/config`或類似的資料夾應位於樹狀結構頂端，其下方的樹狀結構中會有一個以上的YAML檔案。

例如：

```text
/config
  cdn.yaml
```

或

```text
/config
  /dev
    cdn.yaml
```

`/config`下的資料夾名稱和檔案名稱是任意的。 但是，YAML檔案必須包含有效的[`kind`屬性值](#configurations)。

通常，設定會部署到所有環境。 如果每個環境的所有屬性值都相同，則單個YAML檔案就足夠了。 不過，屬性值通常會在環境之間有所不同，例如在測試較低環境時。

以下各節將說明建構檔案的一些策略。

### 適用於所有環境的單一設定檔 {#single-file}

檔案結構將類似於以下內容：

```text
/config
  cdn.yaml
  logForwarding.yaml
```

當相同的設定足以滿足所有環境和所有型別的設定（CDN、記錄轉送等）時，請使用此結構。 在此案例中，`envTypes`陣列屬性將包含所有環境型別。

```yaml
   kind: "cdn"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

使用秘密型別的環境（或管道）變數，每個環境的[秘密屬性](#secret-env-vars)可能會有所不同，如`${{SPLUNK_TOKEN}}`參考所說明

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

### 每種環境型別有不同的檔案 {#file-per-env}

檔案結構將類似於以下內容：

```text
/config
  cdn-dev.yaml
  cdn-stage.yaml
  cdn-prod.yaml
  logForwarding-dev.yaml
  logForwarding-stage.yaml
  logForwarding-prod.yaml
```

屬性值可能有差異時，請使用此結構。 在檔案中，可以預期`envTypes`陣列值與尾碼相對應，例如
值為`cdn-dev.yaml`的`logForwarding-dev.yaml`和`["dev"]`、`cdn-stage.yaml`以及值為`logForwarding-stage.yaml`的`["stage"]`等。

### 每個環境的資料夾 {#folder-per-env}

在此策略中，每個環境有個別的`config`資料夾，在Cloud Manager中為每個環境宣告個別的管道。

如果您有多個開發環境，且每個環境都有獨特的屬性值，此方法會特別實用。

檔案結構將類似於以下內容：

```text
/config/dev1
  cdn.yaml
  logForwarding.yaml
/config/dev2
  cdn.yaml
  logForwarding.yaml
/config/prod  
  cdn.yaml
  logForwarding.yaml
```

此方法的不同之處在於為每個環境維護單獨的分支。

### Edge Delivery Services {#yamls-for-eds}

Edge Delivery設定管道沒有單獨的開發、測試和生產環境。 不同於「發佈傳遞」環境（其中的變更會通過開發、階段和生產層級進行），透過Edge Delivery設定管道部署的設定會直接套用至在Edge Delivery Site的Cloud Manager中註冊的所有網域對應。

因此，請部署簡單的檔案結構，例如：

```text
/config
  cdn.yaml
  logForwarding.yaml
```

如果每個Edge Delivery網站需要不同的規則，請使用&#x200B;*when*&#x200B;語法來區分規則。 例如，請注意網域符合下列程式碼片段中的dev.example.com ，這可以和網域www.example.com區別。

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
    # Block simple path
    - name: block-path
      when:
        allOf:
          - reqProperty: domain
            equals: "dev.example.com"
          - reqProperty: path
            equals: '/block/me'
      action: block
```

如果包含&#x200B;*envTypes*&#x200B;中繼資料欄位，則僅應使用值&#x200B;**prod** （省略envTypes中繼資料欄位也很好）。 對於&#x200B;*層* reqProperty，只應使用值&#x200B;**publish**。

## 秘密環境變數 {#secret-env-vars}

組態檔支援型別為&#x200B;**機密**&#x200B;的Cloud Manager環境變數，因此不需要將機密資訊儲存在原始檔控制中。 對於某些設定（包括記錄轉送），某些屬性會強制使用秘密環境變數。

請注意，秘密環境變數會用於發佈傳遞專案；請參閱Edge Delivery Services專案的「秘密管道變數」一節。

以下程式碼片段是如何在設定中使用機密環境變數`${{SPLUNK_TOKEN}}`的範例。

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

如需有關如何使用環境變數的詳細資訊，請參閱檔案[Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md)。

## 秘密管道變數 {#secret-pipeline-vars}

若為Edge Delivery Services專案，請使用&#x200B;**機密**&#x200B;型別的Cloud Manager管線變數，這樣敏感資訊就不需要儲存在原始檔控制中。 *套用的步驟*&#x200B;選取方塊應使用&#x200B;**部署**&#x200B;選項。

語法與上一節中顯示的程式碼片段相同。

如需如何使用管道變數的詳細資訊，請參閱檔案[Cloud Manager中的管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)。

