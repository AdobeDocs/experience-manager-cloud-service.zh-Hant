---
title: 使用AI工具進行本機開發
description: 瞭解如何使用專案內容、代理程式技能和MCP伺服器來設定AI編碼工具，以加速AEM as a Cloud Service開發。
feature: Developing
role: Developer
source-git-commit: 0bc00b6e14be6ba111ac26ce69f07e138ca400e4
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 0%

---


# 使用AI工具進行本機開發 {#local-development-with-ai-tools}

>[!IMPORTANT]
>
>本文所述功能為&#x200B;**beta**。 客戶與合作夥伴可以提早存取Adobe正在開發的功能，並提供意見回饋（透過傳送電子郵件至[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)）並決定產品開發。 此外，也能協助客戶在功能全面推出前做好採用新功能的準備。
>
>Beta發行版本可能包含瑕疵，並依「現況」提供，並無任何保固。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援（透過Adobe支援服務或其他方式）測試版。 Adobe建議客戶謹慎行事，不要依賴Beta版正確運作或效能，或依賴任何隨附的檔案或資料。 Beta版中的功能和API可能會有所變更，恕不另行通知。 因此，使用測試版完全由客戶自行承擔風險。

>[!NOTE]
>
>本文主要介紹使用AI工具進行&#x200B;**AEM Java棧疊開發**&#x200B;的本機開發。 若為Edge Delivery Services，請參閱[使用AI工具開發](https://www.aem.live/developer/ai-coding-agents)。

AI編碼代理程式（Claude Code、Cursor、GitHub Copilot和類似工具）對AEM的基礎技術(Java、OSGi、Sling、JCR、HTL)有廣泛的瞭解，但不一定知道產生程式碼和設定的最佳實務，或如何偵錯常見的AEM開發問題。

有四個補充元件可解決此問題：

| 元件 | 用途 |
|---|---|
| **代理程式.md** | 特定專案的內容檔案，可在每個工作階段的AEM Cloud Service專案中建立AI |
| **代理程式技能** | 可重複使用的指令集用於週期性開發任務，例如元件建立和Dispatcher設定 |
| **AEM Quickstart本機MCP伺服器** | 公開本機AEM SDK執行個體的即時執行階段資料，以支援疑難排解 |
| **Dispatcher本機MCP伺服器** | 啟用本機Dispatcher執行個體的執行階段驗證和檢查 |

>[!NOTE]
>
> AEM雲端服務的遠端MCP伺服器對於本機開發也很有用，但本文未予說明。 在[搭配使用MCP與Cloud Service文章](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)中進一步瞭解這些功能。

## AGENTS.md {#agentsmd}

`AGENTS.md`是位於AEM專案根目錄的Markdown檔案，AI編碼工具會在每個工作階段開始時自動載入，以便以基本的AEM Cloud Service Java棧疊網域專業知識為基礎（而不是其他AEM解決方案，例如AEM 6.5或Edge Delivery Services）。

`AGENTS.md`不是您複製的靜態檔案 — 它是由下一節中說明的`ensure-agents-md`技能產生的。 此技能會讀取您的`pom.xml`來解析專案名稱、探索模組，以及偵測已安裝的附加元件，產生針對您特定專案量身打造的檔案。

>[!NOTE]
>
>一旦`AGENTS.md`存在於專案根目錄中，`ensure-agents-md`技能便不再執行。 如果您的專案結構變更，請直接編輯檔案。

## 代理程式技能 {#agent-skills}

技能是編碼多步驟開發工作流程的指示集。 經叫用時，AI會遵循技能的程式，而非僅依賴一般知識，以產生一致、符合慣例的結果。

Adobe已在&#x200B;**[分支上的](https://github.com/adobe/skills/tree/beta/skills/aem/cloud-service/skills)adobe/skills**`beta`存放庫中發佈AEM as a Cloud Service技能，因為此功能尚未普遍可用：

| 技能 | 用途 |
|---|---|
| `ensure-agents-md` | 啟動程式`AGENTS.md`和`CLAUDE.md`根據專案的實際模組結構量身打造 |
| `create-component` | 支架完整的AEM元件：元件定義、對話方塊XML、HTL範本、Sling模型、單元測試和clientlibs |
| `dispatcher` | AI支援的Dispatcher和Apache HTTPD設定小幫手，涵蓋設定編寫、技術諮詢、事件回應、效能調整和安全性強化 |
| `workflow` | 所有AEM as a Cloud Service工作流程技能的單一進入點。 涵蓋工作流程模型設計、自訂流程步驟和參與者選擇器開發、啟動器設定、工作流程觸發和生產支援，包括偵錯停滯/失敗的工作流程、透過Cloud Manager記錄擷取事件、執行緒集區分析，以及Granite工作流程引擎的Sling作業診斷。 |

### 安裝技能 {#install-skills}

選擇與您的AI編碼工具相符的方法。 一旦安裝技能，即可供該電腦上的所有專案使用。

#### 克勞德程式碼 {#claude-code}

```bash
# Add the Adobe Skills marketplace (one-time setup)
/plugin marketplace add adobe/skills#beta

# Install all available skills
/plugin install aem-cloud-service@adobe-skills
```

#### Npx技能 {#npx-skills}

```bash
# Install all available skills
npx skills add https://github.com/adobe/skills/tree/beta/skills/aem/cloud-service --all
```

#### 提升技能（GitHub CLI擴充功能） {#upskill-github-cli-extension}

```bash
# Install the gh-upskill extension (one-time setup)
gh extension install trieloff/gh-upskill

# Install all available skills
gh upskill adobe/skills --branch beta --path skills/aem/cloud-service --all
```

### 使用secure-agents-md技能 {#use-the-ensure-agents-md-skill}

安裝技能後，在尚未有`AGENTS.md`的任何AEM Cloud Service專案中開啟您的AI助理。 此技能會在處理您的第一個要求之前自動執行，在專案根目錄建立兩個檔案時不需要明確叫用。

### 使用建立元件技能 {#use-the-create-component-skill}

第一次使用時，技能會自動從`project`和現有元件中偵測`package`、`group`和`pom.xml`，要求您確認偵測到的值，然後在專案根目錄中建立`.aem-skills-config.yaml`。 首次使用前不需要手動設定。

如果您偏好預先建立檔案，請將`.aem-skills-config.yaml`置於專案根目錄，其結構如下：

```yaml
configured: true

project: "wknd"                                    # Check /apps/{project}/ or pom.xml
package: "com.adobe.aem.guides.wknd.core"          # Check core/pom.xml
group: "WKND Components"                           # Check existing component .content.xml files
```

檔案位在技能目錄之外，在技能更新時永遠不會覆寫。

在AI聊天室中說明元件：

```
Create an AEM component called "Hero Banner"

Dialog specification:
Title (title) - Textfield, mandatory
Subtitle (subtitle) - Textfield
Background Image (backgroundImage) - Fileupload
CTA Text (ctaText) - Textfield
CTA Link (ctaLink) - Pathfield
```

代理程式會回應欄位規格以進行確認，然後產生所有元件檔案。 支援的模式包括含有複合巢狀專案的多欄位、條件式顯示/隱藏邏輯、透過Sling Resource Merger的核心元件擴充功能，以及使用AEM Mocks的JUnit 5測試。

### 使用Dispatcher技能 {#use-the-dispatcher-skill}

叫用任何Dispatcher或Apache HTTPD設定工作的Dispatcher技能。 此技能會根據請求的性質，將請求路由到六個專業子技能中的一個：

| 子技能 | 用途 |
|---|---|
| `workflow-orchestrator` | 端對端工作橫跨設計、組態變更、驗證及後續追蹤 |
| `config-authoring` | 具體設定變更：篩選器、快取規則、重新寫入、主機、標題和陣列 |
| `technical-advisory` | 概念指引、原則說明和引文支援的建議 |
| `incident-response` | 執行階段失敗、快取異常和回歸 |
| `performance-tuning` | 快取效率、延遲和輸送量最佳化 |
| `security-hardening` | 曝光檢閱與生產強化 |

若是廣泛或首次要求，請從`workflow-orchestrator`子技能開始。 針對鎖定目標工作，請向適當的專員說明特定的關注事項和技能路線。

Dispatcher技能可處理協調和建議指導。 Dispatcher MCP伺服器（如下所述）提供技能在需要本機證據時所使用的七項驗證和執行階段工具。

## AEM快速入門MCP伺服器 {#aem-quickstart-mcp-server}

模型上下文通訊協定(MCP)是一種開放標準，允許AI編碼工具連線到外部資料來源和服務。 AEM Quickstart MCP伺服器是一個內容套件，一旦安裝在本機AEM SDK執行個體中，就會將執行階段資料直接公開給連線的AI工具，讓代理程式能夠擷取記錄、診斷OSGi失敗並在不離開IDE的情況下檢查請求處理。

### 安裝內容封裝 {#install-the-content-package}

從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Abeta)下載內容封裝，並在`com.adobe.aem:com.adobe.aem.mcp-server-contribs-content`使用封裝管理員將`/crx/packmgr`安裝至您的本機Quickstart。

**相容性：**&#x200B;已透過AEM SDK `2026.2.24678.20260226T154829Z-260200`和更新版本驗證。

### 可用工具 {#available-tools}

| 工具 | 說明 |
|---|---|
| `aem-logs` | 擷取AEM和OSGi記錄專案，可依規則運算式模式、記錄層級和專案計數篩選 |
| `diagnose-osgi-bundle` | 診斷套件組合或DS元件未啟動的原因；報告缺少套件、未滿足的參照和組態問題 |
| `recent-requests` | 傳回具有Sling完整內部處理追蹤（資源解析、指令碼解析、篩選鏈）的最新HTTP請求，可依路徑規則運算式篩選 |

### 設定IDE {#configure-your-ide}

#### 游標 {#cursor}

在「游標設定」中，新增自訂MCP伺服器：

```json
"aem-cs-sdk": {
  "type": "streamable-http",
  "url": "http://localhost:4502/bin/mcp",
  "headers": {
    "Authorization": "Basic YWRtaW46YWRtaW4="
  }
}
```

#### GitHub Copilot與IntelliJ IDEA {#github-copilot-with-ihtellij-idea}

導覽至&#x200B;**工具> GitHub Copilot >模型內容通訊協定(MCP)**，然後按一下&#x200B;**設定**。 新增：

```json
"aem-cs-sdk": {
  "url": "http://localhost:4502/bin/mcp",
  "requestInit": {
    "headers": {
      "Authorization": "Basic YWRtaW46YWRtaW4="
    }
  }
}
```

#### 其他IDE {#other-ides}

任何MCP使用者端都可以指向帶有`http://localhost:4502/bin/mcp`標頭的`Authorization: Basic YWRtaW46YWRtaW4=`來連線。 使用IDE的MCP設定來設定自訂標頭。

>[!NOTE]
>
>值`Basic YWRtaW46YWRtaW4=`是本機Quickstart的預設認證`admin:admin`的Base64編碼。 請勿在非本機環境中使用它。

## Dispatcher MCP伺服器 {#dispatcher-mcp-server}

Dispatcher MCP伺服器與AEM Dispatcher SDK搭配。 它可讓AI工具驗證Dispatcher和Apache HTTPD設定、追蹤請求處理，以及針對Docker中本機執行的Dispatcher執行個體檢查快取行為。

不像Dispatcher技能，Dispatcher MCP伺服器只會公開工具：七個MCP工具，沒有提示或資源。

### 先決條件 {#prerequisites}

- Docker Desktop 4.x或更高版本，已安裝並執行
- 從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Abeta)下載的AEM Dispatcher SDK

>[!NOTE]
>
>如果您看見`client version 1.43 is too new`，請在殼層或`DOCKER_API_VERSION=1.41`中設定`mcp.json`。

### 安裝Dispatcher SDK {#install-the-dispatcher-sdk}

**macOS和Linux：**

```bash
chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
./aem-sdk-dispatcher-tools-<version>-unix.sh
cd dispatcher-sdk-<version>
chmod +x ./bin/docker_run_mcp.sh
./bin/docker_run_mcp.sh test
```

**Windows：**

```powershell
Expand-Archive aem-sdk-dispatcher-tools-<version>-windows.zip
```

執行`./bin/docker_run_mcp.sh help`以擷取複製貼上IDE組態，並執行`./bin/docker_run_mcp.sh version`以確認套件式MCP和SDK版本。 使用`./bin/docker_run_mcp.sh diagnose`調查連線問題。

### 設定游標 {#configure-cursor}

新增`aem-dispatcher-mcp`專案至`~/.cursor/mcp.json`：

```json
{
  "mcpServers": {
    "aem-dispatcher-mcp": {
      "command": "<path_to_dispatcher_sdk>/bin/docker_run_mcp.sh",
      "env": {
        "DOCKER_API_VERSION": "1.43",
        "AEM_DEPLOYMENT_MODE": "cloud",
        "MCP_LOG_LEVEL": "trace",
        "MCP_LOG_FILE": "/tmp/dispatcher-mcp.log",
        "DISPATCHER_CONFIG_PATH": "<path_to_dispatcher_src>"
      }
    }
  }
}
```

以擷取的Dispatcher SDK位置取代`<path_to_dispatcher_sdk>`，並以專案的Dispatcher `<path_to_dispatcher_src>`目錄取代`src`。 將`DISPATCHER_CONFIG_PATH`設為包含已定義`/docroot`之檔案的設定根目錄。 `MCP_LOG_LEVEL`和`MCP_LOG_FILE`是選擇性偵錯設定。 如果您看見`client version 1.43 is too new`，請將`DOCKER_API_VERSION`設為`1.41`。 如果已設定其他MCP伺服器，請新增`aem-dispatcher-mcp`專案而不取代它們。 儲存後重新啟動游標。

其他IDE也可以以類似的方式進行設定。 SDK的`docs/DispatcherMCP.md`包含Claude Desktop和VS Code的完整範例。

### 可用工具 {#available-tools-dispatcher}

| 工具 | 說明 |
|---|---|
| `validate` | 驗證Dispatcher和Apache HTTPD設定 |
| `lint` | 執行模式感知靜態檢查和最佳實務分析 |
| `sdk` | 執行Dispatcher SDK工作流程： `validate`、`validate-full`、`three-phase-validate`、`docker-test`、`check-files`、`diff-baseline` |
| `trace_request` | 使用執行階段證據追蹤要求行為 |
| `inspect_cache` | 檢查目標URL的快取和docroot行為 |
| `monitor_metrics` | 從Dispatcher和HTTPD記錄檔讀取執行階段量度 |
| `tail_logs` | 提供相關Dispatcher和HTTPD執行階段記錄檔的詳細資料 |

MCP表面僅會刻意公開這七種工具；提示和資源會保留在技能層中。 擷取的Dispatcher SDK內的`docs/DispatcherMCP.md`中有完整的參考檔案。
