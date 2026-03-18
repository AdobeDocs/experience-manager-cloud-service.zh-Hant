---
title: 搭配AEM as a Cloud Service使用MCP
description: 瞭解如何將模型上下文通訊協定與AEM as a Cloud Service搭配使用
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: ddb7fc8c-affc-4374-8e08-d45d96017109
source-git-commit: 3b935114d543a0bf99f3c03a2840942862396216
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 0%

---

# 搭配AEM as a Cloud Service使用MCP {#using-mcp-with-aem-as-a-cloud-service}

## 簡介 {#introduction}

許多Adobe Experience Manager (AEM)團隊現在都在整合開發環境(IDE)和聊天型應用程式中工作，例如Cursor、OpenAI ChatGPT、Anthropic Claude和Microsoft Copilot Studio。 這些應用程式支援模型內容通訊協定(MCP)，可讓應用程式以標準化的方式將後端工具公開給大型語言模型(LLM)。

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

* **自然語言互動而非API管道**
MCP工具說明可以使用哪些作業以及如何呼叫它們。 LLM會使用這些結構來決定要叫用哪些工具以及使用哪些引數。
* **跨應用程式的一致體驗**
相同的AEM MCP工具可用於多個MCP相容應用程式，讓團隊可以在生產力最高的地方工作，同時呼叫相同的基礎AEM功能。
* **已保留安全性與治理**
對AEM MCP工具的請求會在已驗證的使用者身分下執行，而每個工具都會強制使用者現有的AEM許可權。 AI輔助操作遵循的存取規則與AEM中的手動工作相同。

## AEM提供的MCP伺服器 {#mcp-servers-provided-by-aem}

AEM會公開MCP伺服器作為HTTP端點。 以下所列的端點為相對於：

`https://mcp.adobeaemcloud.com/adobe/mcp/`

### MCP伺服器 {#mcp-servers}

| **MCP伺服器** | **端點** | **說明** |
|---|---|----------------------------------------------------------------------------------------------------------------------|
| **內容** | `/content` | 所有低階內容作業，包括頁面、片段和資產的建立、讀取、更新和刪除(CRUD)。 |
| **內容（唯讀）** | `/content-readonly` | 頁面、片段和資產的唯讀內容作業（取得、清單/搜尋）。 |
| **Cloud Manager** | `/cloudmanager` | 管理Cloud Manager實體，包括也可以觸發的方案、環境、存放庫和管道。 <br><br>*此MCP伺服器目前處於&#x200B;**測試版**；若要要求存取權，請傳送電子郵件至[aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com)，其中包含您使用案例的說明。* |

每個MCP伺服器公開的特定工具可能會隨著時間而改變。 實際上，您可以要求啟用MCP的應用程式透過提示來探索工具，例如：

```
"List all AEM MCP tools available from this server and describe what they do."
```

MCP使用者端會使用MCP通訊協定來擷取工具清單和結構描述，然後LLM就可以使用。

請參考[Content MCP伺服器教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/ai/mcp-servers/accelerate-content-operations-with-aem-mcp-server)和[Cloud Manager MCP伺服器影片](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager)，瞭解其功能及使用方式的詳細資訊。

## 支援的MCP應用程式 {#supported-mcp-applications}

AEM的MCP伺服器可搭配一組已定義的MCP相容應用程式運作。 每個應用程式都有各自的設定體驗，但高階步驟類似。

### 聊天應用程式（網頁與案頭） {#chat-applications}

* 合唱團克勞德
* OpenAI ChatGPT

### 開發人員工具（IDE擴充功能、案頭應用程式、CLI） {#developer-tools}

* Anthropic Claude程式碼（CLI、JetBrains、VS程式碼、游標）
* 增強程式碼（CLI、JetBrains、VS程式碼、游標）
* 增加縮排案頭應用程式
* Cline (JetBrains、VS Code、Cursor)
* 游標
* GitHub Copilot （VS程式碼）
* Kiro （案頭應用程式、CLI）
* OpenAI程式碼（案頭應用程式）
* OpenAI程式碼CLI
* Windsurf

### 企業平台 {#enterprise-platforms}

* Microsoft Copilot Studio

## 設定概述 {#setup-overview}

為AEM設定MCP涉及兩個主要部分：

1. **每個MCP使用者端應用程式中的設定**，讓應用程式知道如何連線至AEM MCP伺服器並執行OAuth登入
1. **在開始提示之前選取MCP伺服器**，讓MCP使用者端知道要使用它。

涵蓋兩個步驟的逐步指南適用於：

* [合唱團克勞德](/help/ai-in-aem/mcp-support/setup-claude.md)
* [OpenAI ChatGPT](/help/ai-in-aem/mcp-support/setup-chatgpt.md)
* [游標](/help/ai-in-aem/mcp-support/setup-cursor.md)
* [Microsoft Copilot Studio](/help/ai-in-aem/mcp-support/setup-microsoft-copilot-studio.md)

### AEM設定 {#aem-configuration}

依預設，個別使用者在AEM中擁有的許可權可控制對AEM MCP伺服器的存取。 當使用者透過MCP使用者端應用程式進行驗證時，MCP工具會強制實施與AEM中手動操作相同的存取規則。 使用者只能執行他們已被授權執行的動作。

#### 允許的MCP使用者端應用程式 {#permitted-mcp-client-applications}

依預設，允許列在[支援的MCP應用程式](#supported-mcp-applications)下的所有應用程式。

#### 限制MCP伺服器 {#restricting-mcp-servers}

所有MCP伺服器預設為允許清單。 作為管理員，您可以選擇在組織、方案或環境層級限制對特定MCP伺服器的存取。 此限制可讓您精細地控制組織內使用者可使用哪些MCP功能。

#### 管理MCP使用者端存取 {#managing-mcp-client-access}

如果貴組織的原則需要，管理員也可以停用特定MCP使用者端應用程式的存取權。 如果您希望Adobe啟用其他MCP使用者端產品的支援，請傳送產品網站的連結。 如果您需要允許列出自訂MCP使用者端，請連絡我們。

如需所有與MCP伺服器相關的要求，請隨時透過&#x200B;**aemcs-mcp-feedback@adobe.com**&#x200B;與我們連絡

### MCP使用者端應用程式組態 {#mcp-client-application-configuration}

每個使用者都會執行此步驟，或者MCP使用者端應用程式的管理員可以在支援時執行此步驟。 不同應用程式的設定詳細資料稍有不同。 MCP使用者端正在迅速成長，對遠端MCP伺服器的支援也正在積極開發中。 您可能需要啟用「開發人員模式」才能存取新增遠端伺服器的功能，但一般程式為：

1. 新增一或多個AEM MCP伺服器URL
   * 從上表設定一或多個MCP端點。 例如：`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. 觸發連線
   * 儲存或啟動設定，讓MCP使用者端應用程式嘗試連線至AEM MCP伺服器
1. 使用Adobe ID登入
   * 出現提示時，請完成Adobe登入流程，讓應用程式能夠取得與您的Adobe ID繫結的OAuth權杖
1. 驗證探索到的工具
   * 驗證之後，應用程式就會從伺服器探索MCP工具。 然後，您可以開始提示LLM執行AEM作業。

請參閱[支援的MCP應用程式](#supported-mcp-applications)，以取得支援的應用程式完整清單。

## 驗證 {#authentication}

Adobe代管的MCP伺服器會實作OAuth，並與Adobe的身分識別系統整合。

* 當MCP使用者端應用程式連線至AEM MCP伺服器時，使用者會看到Adobe登入對話方塊，並使用其&#x200B;**Adobe ID**&#x200B;進行驗證
* 成功登入後，系統會驗證貴組織是否允許MCP使用者端應用程式，以及是否允許請求的MCP伺服器。 如果任一檢查失敗，則會顯示錯誤訊息。

![不允許的MCP使用者端錯誤](assets/MCP-Client-not-permitted.png)

* 驗證後，MCP伺服器會發行應用程式用於後續工具呼叫的權杖
* MCP工具會遵守使用者的AEM許可權。 只有有權在AEM中修改內容片段的使用者才能透過MCP修改它。

此方法可確保AI協助的作業符合您現有的AEM安全性與治理模式。

## 搭配AEM使用MCP {#using-mcp-with-aem}

設定AEM和MCP使用者端應用程式後，您就可以使用您選擇的應用程式，並提示LLM執行AEM作業。 LLM會讀取MCP工具結構、選擇要呼叫的工具，並根據需要排序這些工具，以符合您的要求。

>[!IMPORTANT]
>
>包含多個步驟或針對不同內容型別（例如影像和文字）的提示，最適合用於思考模型。 啟用思考模型，或在您的MCP使用者端中選取「思考」選項，而非依賴「自動」模式。

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
   * 當行銷活動訊息變更時，更新現有片段。

* **Assets管理**
   * 以狀態檢查匯入資產

### 範例工作流程 {#example-workflows}

下列範例說明LLM如何將MCP工具鏈結在一起。

1. **使用頁面**&#x200B;所參考的內容片段
   * **取得頁面內容** — 呼叫`get-aem-page-content`之類的工具以擷取頁面，並找到`fragmentPath`屬性。
   * **解析片段路徑** — 使用`resolve_fragment_path`將路徑轉換為UUID。
   * **擷取片段資料** — 呼叫`get_fragment`以擷取目前的欄位。
   * **更新片段** — 呼叫`patch_fragment`將變更套用至片段內容。
1. **根據模型建立新內容**
   * **探索模型** — 使用`list_models`檢視哪些內容片段模型可用。
   * **檢查模型** — 使用`get_model`瞭解模型的欄位結構描述。
   * **建立內容** — 使用`create_fragment`建立具有衍生自您提示之值的新片段。
1. **安全更新現有內容**
   * **讀取目前的資料** — 使用`get_fragment`擷取現有的資料和ETag。
   * **套用JSON修補程式** — 使用`patch_fragment`搭配ETag和JSON修補程式檔案來更新片段，支援開放式並行。

從使用者的角度來看，這些工作流程可以使用提示來啟動，例如：

```
"Create a new content fragment for the spring campaign based on our hero banner model and fill in its fields from this brief."
```

LLM會自動選擇並協調必要的MCP工具。

## 期望管理 {#expectation-management}

透過MCP使用LLM時，請記住下列事項：

* **功能強大，但並非絕對可靠**
LLM可以完成複雜的工作，但容易偶爾發生錯誤。 相同的提示可能會產生稍微不同的結果或簡報，但並無明顯的原因。 將變更套用至生產內容之前，請務必檢閱輸出。

* **不斷發展的功能**
LLM模型不斷改進。 隨著時間推移，他們在發現結合MCP工具以實現您的目標的新方法方面變得更聰明。 今天需要多個提示的工作，明天可能會順暢地搭配單一提示運作。

* **人力監督是必要的：**
將LLM視為需要監督的知識淵博的助理。 它擁有廣泛的知識，可以設計創意解決方案，但受益於您的指導和審查。 驗證結果，特別是關鍵作業的結果，並在輸出不符合預期時提供意見回饋。

* **自動確認工具執行時請小心**
有些MCP使用者端應用程式（例如Claude）會提供LLM要求的自動認可工具執行的選項。 雖然此選項方便用於搜尋或擷取內容等唯讀操作，但請謹慎使用更新或刪除內容的工具。 在確認修改AEM環境的動作之前，請檢閱每個工具執行請求。

## 限制 {#limitations}

AEM目前支援在[支援的MCP應用程式](#supported-mcp-applications)下列出的應用程式中設定MCP伺服器。

如果您想要使用不同的MCP使用者端應用程式，請隨時與&#x200B;**aemcs-mcp-feedback@adobe.com**&#x200B;連絡，要求支援其他使用者端或允許列出自訂使用者端。
