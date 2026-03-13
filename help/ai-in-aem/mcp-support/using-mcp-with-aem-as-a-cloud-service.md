---
title: 搭配AEM as a Cloud Service使用MCP
description: 瞭解如何將模型上下文通訊協定與AEM as a Cloud Service搭配使用
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: ddb7fc8c-affc-4374-8e08-d45d96017109
source-git-commit: 6fccf4f197fbfd38aa6a84422dc347b02d03061d
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 0%

---

# 將MCP與AEM結合作為雲服務 {#using-mcp-with-aem-as-a-cloud-service}

## 簡介 {#introduction}

許多Adobe Experience Manager(AEM)團隊現在在整合開發環境(IDE)和基於聊天的應用程式(如Cursor、OpenAI ChatGPT、Thropic Claude和MicrosoftCopilot Studio)中工作。 這些應用支援模型上下文協定(MCP)，該協定允許應用以標準化方式向大型語言模型(LLM)公開後端工具。

透過AEM的MCP整合，不同的角色可以圍繞相同內容共同作業：

* **開發人員**&#x200B;可以從其IDE或聊天應用程式協調內容作業和工作流程
* **從業者**&#x200B;和內容架構師可以透過AI協助管理網站、內容片段和資產，同時留在AEM的現有許可權模式中。

>[!IMPORTANT]
>
> 對於修改或刪除內容的情境，從業人員應該使用AI助理介面，而不是直接叫用MCP工具。 AI Assistant所執行的AEM代理程式包含內建的防護措施。
>

本文說明AEM的MCP功能提供哪些功能、支援哪些MCP應用程式、如何設定，以及如何在實務中使用。

## 為什麼MCP對AEM客戶有用 {#why-mcp-is-useful-for-aem-customers}

現代IDE和聊天應用程式使用MCP作為LLM呼叫MCP伺服器後面公開工具的方式。 客戶可用自然語言描述其意圖，而非根據低階API規格撰寫程式碼。 例如，類似&#x200B;*「更新所有頁面上此行銷活動的主圖橫幅」*&#x200B;的提示可讓LLM叫用適當的MCP工具，然後與AEM的API互動。

主要優勢包括：

* **自然語言交互，而不是API管道**
MCP工具描述了哪些操作可用以及如何調用它們。 LLM使用這些架構來確定要調用哪些工具以及使用哪些參數。
* **跨應用程式的一致體驗**
同樣AEM的MCP工具可從多個與MCP相容的應用中使用，使團隊能夠在最高效的地方工作，同時調用相同的基礎AEM功能。
* **保留了安全性和治理**
對MCP工AEM具的請求在經過驗證的用戶身份下運行，並且每個工具都強制用戶的現有AEM權限。 AI輔助操作遵循的存取規則與AEM中的手動工作相同。

## MCP伺服器由提供AEM {#mcp-servers-provided-by-aem}

將AEMMCP伺服器作為HTTP終結點公開。 下面列出的端點相對於：

`https://mcp.adobeaemcloud.com/adobe/mcp/`

### MCP伺服器 {#mcp-servers}

| **MCP伺服器** | **終結點** | **說明** |
|---|---|----------------------------------------------------------------------------------------------------------------------|
| **內容** | `/content` | 所有低級內容操作，包括為頁面、片段和資產建立、讀取、更新和刪除(CRUD)。 |
| **內容（只讀）** | `/content-readonly` | 頁面、片段和資產的只讀內容操作（獲取、清單/搜索）。 |
| **Cloud Manager** | `/cloudmanager` | Manage Cloud Manager entities including programs, environments, repositories and pipelines, which can also be triggered. <br><br>*This MCP server is now in **beta**; to request access, email [aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com) with a description of your use case.* |

The specific tools exposed by each MCP server may evolve over time. In practice, you can ask your MCP-enabled application to discover tools via a prompt such as:

```
"List all AEM MCP tools available from this server and describe what they do."
```

The MCP client uses the MCP protocol to retrieve the tool list and schemas, which the LLM can then use.

請參考[Content MCP伺服器教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/ai/mcp-servers/accelerate-content-operations-with-aem-mcp-server)和[Cloud Manager MCP伺服器影片](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager)，瞭解其功能及使用方式的詳細資訊。

## 支援的MCP應用程式 {#supported-mcp-applications}

MCP服AEM務器設計為與一組定義的MCP相容應用程式配合工作。 每個應用程式都提供自己的配置體驗，但高級別步驟相似。

### 聊天應用程式（Web和案頭） {#chat-applications}

* 克洛德人
* OpenAI ChatGPT

### 開發人員工具（IDE擴充功能、案頭應用程式、CLI） {#developer-tools}

* Anthropic Claude程式碼（CLI、JetBrains、VS程式碼、游標）
* 增強程式碼（CLI、JetBrains、VS程式碼、游標）
* 增加縮排案頭應用程式
* Cline（JetBrains、VS代碼、游標）
* 游標
* GitHub Copilot (VS Code)
* Kiro (Desktop App, CLI)
* OpenAI Codex (Desktop App)
* OpenAI程式碼CLI
* Windsurf

### 企業平台 {#enterprise-platforms}

* Microsoft科皮洛特一室公寓

## 設定概述 {#setup-overview}

為配置MCPAEM涉及兩個主要部分：

1. **在每個MCP客戶端應用程式中配置**，以便應用程式知道如何連接到AEMMCP伺服器並執行OAuth登錄
1. **在開始提示之前選擇MCP伺服器**，以便MCP客戶端知道使用它。

### AEM設定 {#aem-configuration}

依預設，個別使用者在AEM中擁有的許可權可控制對AEM MCP伺服器的存取。 當使用者透過MCP使用者端應用程式進行驗證時，MCP工具會強制實施與AEM中手動操作相同的存取規則。 使用者只能執行他們已被授權執行的動作。

#### 允許的MCP使用者端應用程式 {#permitted-mcp-client-applications}

預設情況下允許以下MCP客戶端應用：

* 克洛德人
* 人類克洛德代碼
* 擴展代碼
* 增加縮排
* 斜面
* 游標
* GitHub Copilot
* 基郎
* Microsoft Copilot Studio
* OpenAI ChatGPT
* OpenAI程式碼
* OpenAI Codex CLI
* 風浪

#### 限制MCP伺服器 {#restricting-mcp-servers}

預設情況下允許列出所有MCP伺服器。 作為管理員，您可以選擇限制對組織、程式或環境級別的特定MCP伺服器的訪問。 此限制使您能夠精確控制組織中的用戶可以使用哪些MCP功能。

#### 管理MCP使用者端存取 {#managing-mcp-client-access}

如果組織的策略需要，管理員還可以禁用特定MCP客戶端應用程式的訪問。 如果希望Adobe啟用對其他MCP客戶端產品的支援，請發送到產品網站的連結。 如果需要允許列出自定義MCP客戶端，也請伸出手。

對於所有與MCP伺服器相關的請求，請隨時與我們聯繫，地址為&#x200B;**aemcs-mcp-feedback@adobe.com**

### MCP客戶端應用程式配置 {#mcp-client-application-configuration}

每個用戶都執行此步驟，或者MCP客戶端應用程式的管理員可以在支援的位置執行此步驟。 配置詳細資訊在應用程式之間略有不同。 MCP客戶端正在快速發展，對遠程MCP伺服器的支援正在積極發展。 您可能需要啟用開發人員模式才能訪問添加遠程伺服器的功能，但一般過程是：

1. 添加一個或多個AEMMCP伺服器URL
   * 從上表配置一個或多個MCP端點。 例如：`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. 觸發連接
   * 保存或激活配置，以便MCP客戶端應用程式嘗試連接到AEMMCP伺服器
1. Sign in with Adobe ID
   * When prompted, complete the Adobe login flow so the application can obtain OAuth tokens tied to your Adobe ID
1. Verify discovered tools
   * 驗證之後，應用程式就會從伺服器探索MCP工具。 You can then start prompting the LLM to perform AEM operations.

以下是支援的應用程式，其中一些會連結至逐步指南：

#### 聊天應用程式（Web和案頭） {#setup-chat-applications}

* [克洛德人](/help/ai-in-aem/mcp-support/setup-claude.md)
* [OpenAI ChatGPT](/help/ai-in-aem/mcp-support/setup-chatgpt.md)

#### 開發人員工具（IDE擴展、案頭應用、CLI） {#setup-developer-tools}

* 人體克洛德代碼（CLI、JetBrains、VS代碼、游標）
* 擴展代碼（CLI、JetBrains、VS代碼、游標）
* 擴展縮進案頭應用
* Cline（JetBrains、VS代碼、游標）
* [游標](/help/ai-in-aem/mcp-support/setup-cursor.md)
* GitHub Copilot（VS代碼）
* 基羅（案頭應用、CLI）
* OpenAI Codex (Desktop App)
* OpenAI程式碼CLI
* Windsurf

#### 企業平台 {#setup-enterprise-platforms}

* [Microsoft Copilot Studio](/help/ai-in-aem/mcp-support/setup-microsoft-copilot-studio.md)

## 驗證 {#authentication}

Adobe承載的MCP伺服器實現OAuth並與Adobe的身份系統整合。

* 當MCP客戶端應用程式連接到AEMMCP伺服器時，用戶將看到Adobe登錄對話框並向其&#x200B;**Adobe ID**&#x200B;進行身份驗證
* 成功登錄後，系統將驗證組織中是否允許MCP客戶端應用程式，以及是否允許請求的MCP伺服器。 如果其中一項檢查失敗，則顯示錯誤消息。

![MCP Client not permitted error](assets/MCP-Client-not-permitted.png)

* 驗證後，MCP伺服器會發行應用程式用於後續工具呼叫的權杖
* MCP工具會遵守使用者的AEM許可權。 只有有權在AEM中修改內容片段的使用者才能透過MCP修改它。

此方法可確保AI協助的作業符合您現有的AEM安全性與治理模式。

## 搭配AEM使用MCP {#using-mcp-with-aem}

配置AEMMCP客戶端應用程式後，您就可以在選擇的應用程式中工作並提示LLM執行AEM操作。 LLM讀取MCP工具模式，選擇要調用的工具，並根據需要對它們進行排序以滿足您的請求。

>[!IMPORTANT]
>
>包含多個步驟或針對不同內容類型的提示（如影像和文本）最適合使用思考模型。 在MCP客戶端中啟用思考模型或選擇Thinking選項，而不是依賴自動模式。

### 範例使用案例 {#example-usecases}

某些代表性的案例包括：

* **環境探索**
   * 列出環境和授權以決定執行工作流程的位置。

* **網站管理**
   * 列出網站
   * 建立、讀取、更新及刪除頁面和頁面內容。

* **內容片段管理**
   * 搜尋內容片段
   * 建立新片段
   * 在市場活動消息更改時更新現有片段。

* **資產管理**
   * 導入資產
   * 查找現有資產
   * 發佈資產。

### 示例工作流 {#example-workflows}

以下示例說明LLM如何將MCP工具鏈在一起。

1. **使用頁面引用的內容片段**
   * **獲取頁面內容** — 調用`get-aem-page-content`等工具以檢索頁面並查找`fragmentPath`屬性。
   * **解析片段路徑** — 使用`resolve_fragment_path`將路徑轉換為UUID。
   * **提取片段資料** — 調用`get_fragment`以檢索當前欄位。
   * **更新片段** — 調用`patch_fragment`以將更改應用於片段內容。
1. **根據模型建立新內容**
   * **探索模型** — 使用`list_models`檢視哪些內容片段模型可用。
   * **檢查模型** — 使用`get_model`瞭解模型的欄位結構描述。
   * **建立內容** — 使用`create_fragment`建立具有衍生自您提示之值的新片段。
1. **安全更新現有內容**
   * **讀取當前資料** — 使用`get_fragment`檢索現有資料和ETag。
   * **應用JSON修補程式** — 將`patch_fragment`與ETag和JSON修補程式文檔一起使用以更新片段，支援樂觀的併發。

從用戶的角度來看，可以使用以下提示啟動這些工作流：

```
"Create a new content fragment for the spring campaign based on our hero banner model and fill in its fields from this brief."
```

LLM自動選擇和協調所需的MCP工具。

## 期望管理 {#expectation-management}

在通過MCP處理LLM時，請牢記以下事項：

* **高度可能但不會出錯**
LLM可以完成複雜的任務，但偶爾會出錯。 同樣的提示可能產生稍微不同的結果或演示，沒有明顯的原因。 在對生產內容應用更改之前，請始終查看輸出。

* **正在演變的功能**
LLM模型正在不斷改進。 隨著時間的推移，他們越來越聰明地發現將MCP工具結合起來以實現你的目標的新方法。 今天需要多個提示的任務可能與明天的單個提示無縫協作。

* **人為監督至關重要：**
把LLM視為一個需要監督的知識淵博的助理。 它擁有廣泛的知識，可以設計出創造性的解決方案，但它得益於您的指導和審查。 驗證結果，尤其是關鍵操作的結果，並在輸出與您的預期不匹配時提供反饋。

* **在自動確認工具執行時要小心**
某些MCP客戶端應用程式（如Claude）提供了自動確認LLM請求的工具執行的選項。 雖然此選項可方便執行只讀操作（如搜索或檢索內容），但使用可更新或刪除內容的工具時要小心。 在確認修改環境的操作之前，請檢查每個工具執AEM行請求。

## 限制 {#limitations}

AEM currently supports configuring MCP servers in the applications listed under [Supported MCP Applications](#supported-mcp-applications).

If you would like to use a different MCP client application, feel free to reach out at **aemcs-mcp-feedback@adobe.com** to request support for additional clients or to allowlist a custom one.
