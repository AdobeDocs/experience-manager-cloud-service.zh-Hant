---
title: 搭配AEM as a Cloud Service使用MCP
description: 瞭解如何將模型上下文通訊協定與AEM as a Cloud Service搭配使用
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 96ce03c86d0406320223f3fae87beed3552d479f
workflow-type: tm+mt
source-wordcount: '2003'
ht-degree: 0%

---


# 搭配AEM as a Cloud Service使用MCP {#using-mcp-with-aem-as-a-cloud-service}

## 簡介 {#introduction}

許多AEM團隊現在都使用IDE和聊天式應用程式，例如Cursor、ChatGPT、Anthropic Claude和Microsoft Copilot Studio。 這些應用程式支援模型內容通訊協定(MCP)，可讓應用程式以標準化的方式將後端工具公開給大型語言模型(LLM)。

透過AEM的MCP整合，不同的角色可以圍繞相同內容共同作業：

* **開發人員**&#x200B;可以從其IDE或聊天應用程式協調內容作業和工作流程
* **從業者**&#x200B;和內容架構師可以透過AI協助管理網站、內容片段和資產，同時留在AEM的現有許可權模式中。

本文說明AEM的MCP功能提供哪些功能、支援哪些MCP應用程式、如何設定，以及如何在實務中使用。

## 為什麼MCP對AEM客戶有用 {#why-mcp-is-useful-for-aem-customers}

現代IDE和聊天應用程式使用MCP作為LLM呼叫MCP伺服器後面公開工具的方式。 客戶可以自然語言描述其意圖（將&#x200B;*「在所有頁面上更新此行銷活動的主圖橫幅」*），而非「根據低階API規格撰寫程式碼」，並讓LLM叫用適當的MCP工具，進而與AEM的API互動。

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

每個MCP伺服器公開的特定工具可能會隨著時間而改變。 實際上，您可以要求啟用MCP的應用程式透過提示來探索工具，例如：

*「列出此伺服器可用的所有AEM MCP工具，並說明其用途。」*

MCP使用者端將使用MCP通訊協定來擷取工具清單和結構描述，然後LLM可以使用。

## 支援的MCP應用程式 {#supported-mcp-applications}

AEM的MCP伺服器可搭配一組已定義的MCP相容應用程式運作。 支援下列應用程式：

* 合唱團克勞德
* 游標
* OpenAI ChatGPT
* Microsoft Copilot Studio

每個應用程式都有各自的設定體驗，但高階步驟類似。

## 設定概述 {#setup-overview}

為AEM設定MCP涉及三個主要部分：

1. **管理員在AEM中執行一次性設定**，允許特定MCP使用者端應用程式存取AEM的MCP伺服器
1. **每個MCP使用者端應用程式中的設定**，讓應用程式知道如何連線至AEM MCP伺服器並執行OAuth登入
1. **在開始提示之前選取MCP伺服器**，讓MCP使用者端知道要使用它。

### AEM設定 {#aem-configuration}

依預設，對AEM MCP伺服器的存取權由個別使用者在AEM中擁有的許可權控制。 當使用者透過MCP使用者端應用程式進行驗證時，MCP工具會強制實施與AEM中手動操作相同的存取規則。 使用者只能執行他們已被授權執行的動作。

#### 允許的MCP使用者端應用程式 {#permitted-mcp-client-applications}

預設允許下列MCP使用者端應用程式：

* ChatGPT
* 克勞德
* MS Copilot Studio
* 游標

#### 限制MCP伺服器 {#restricting-mcp-servers}

所有MCP伺服器預設為允許清單。 作為管理員，您可以選擇在組織、方案或環境層級限制對特定MCP伺服器的存取。 這可讓您精細地控制貴組織內使用者可使用哪些MCP功能。

#### 管理MCP使用者端存取 {#managing-mcp-client-access}

如果貴組織的原則需要，管理員也可以停用特定MCP使用者端應用程式的存取權。 如果您希望Adobe啟用其他MCP使用者端產品的支援，請傳送產品網站的連結。 如果您需要允許列出自訂MCP使用者端，請連絡我們。

如需所有與MCP伺服器相關的要求，請隨時透過&#x200B;**aemcs-mcp-feedback@adobe.com**&#x200B;與我們連絡

### MCP使用者端應用程式組態 {#mcp-client-application-configuration}

此步驟由每個使用者(或由MCP使用者端應用程式的管理員（如果支援）執行。 不同應用程式的設定詳細資料稍有不同。 MCP使用者端正在迅速成長，對遠端MCP伺服器的支援也正在積極開發中。 您可能需要啟用「開發人員模式」才能存取新增遠端伺服器的功能，但一般程式為：

1. 新增AEM MCP伺服器URL
   * 從上表設定MCP端點。 例如：`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. 觸發連線
   * 儲存或啟動設定，讓MCP使用者端應用程式嘗試連線至AEM MCP伺服器
1. 使用Adobe ID登入
   * 出現提示時，請完成Adobe登入流程，讓應用程式能夠取得與您的Adobe ID繫結的OAuth權杖
1. 驗證探索到的工具
   * 驗證後，應用程式將從伺服器探索MCP工具。 然後，您可以開始提示LLM執行AEM作業。

以下範例說明這在各支援應用程式中的概觀。

**ChatGPT**

![設定ChatGPT步驟1](assets/chatgpt-1.png)

![設定ChatGPT步驟2](assets/chatgpt-2.png)

![設定ChatGPT步驟3](assets/chatgpt-3.png)

![設定ChatGPT步驟4](assets/chatgpt-4.png)

![設定ChatGPT步驟5](assets/chatgpt-5.png)

![設定ChatGPT步驟6](assets/chatgpt-6.png)

![設定ChatGPT步驟7](assets/chatgpt-7.png)

* 在設定MCP連線或工具的區域中新增AEM MCP伺服器URL
* 在重新導向時，觸發連線並使用您的Adobe ID登入
* 在聊天中，在提示中參考已設定的AEM工具，例如：

  *&quot;使用已設定的AEM MCP工具，列出作者環境中的所有網站。&quot;*

**克勞德**

![設定克勞德步驟1](assets/claude-1.png)

![設定克勞德步驟2](assets/claude-2.png)

![設定克勞德步驟3](assets/claude-3.png)

![設定克勞德步驟4](assets/claude-4.png)

![設定克勞德步驟5](assets/claude-5.png)

![設定克勞德步驟6](assets/claude-6.png)

![設定克勞德步驟7](assets/claude-7.png)

* 在Claude的MCP設定中，註冊AEM MCP伺服器URL
* 完成Adobe登入流程
* 可選擇在設定區域中啟用特定工具的自動確認。 建議將此用於搜尋或唯讀作業。
* 在開始交談之前，請確定已選取MCP伺服器
* 要求Claude執行AEM相關工作；Claude會根據您的提示選取MCP伺服器公開的AEM工具。

**游標**

![設定游標步驟1](assets/cursor-1.png)

![設定游標步驟2](assets/cursor-2.png)

![設定游標步驟3](assets/cursor-3.png)

![設定游標步驟4](assets/cursor-4.png)

![設定游標步驟5](assets/cursor-5.png)

* 在Cursor的MCP設定中，使用AEM MCP URL建立新的MCP伺服器專案
* 出現提示時，使用您的Adobe ID進行驗證
* 或者，按一下工具名稱來啟用或停用個別工具。 預設會啟用所有工具。
* 使用游標的編輯器或聊天叫用AEM工具，作為開發或內容工作流程的一部分。

**Microsoft Copilot Studio**

![設定Copilot步驟1](assets/copilot-1.png)

![設定Copilot步驟2](assets/copilot-2.png)

![設定Copilot步驟3](assets/copilot-3.png)

![設定Copilot步驟4](assets/copilot-4.png)

![設定Copilot步驟5](assets/copilot-5.png)

![設定Copilot步驟6](assets/copilot-6.png)

![設定Copilot步驟7](assets/copilot-7.png)

![設定Copilot步驟8](assets/copilot-8.png)

![設定Copilot步驟9](assets/copilot-9.png)

![設定Copilot步驟10](assets/copilot-10.png)

* 建立新的代理程式
* 瀏覽至工具區段，然後按一下&#x200B;**新增工具**
* 選取現有工具或建立新工具
* 設定指向AEM MCP伺服器URL的新MCP工具
* 建立可在代理程式之間共用或專用的連線
* 當重新導向時，使用您的Adobe ID登入
* 可選擇啟用自動確認模式，或要求使用者對所有工具互動進行確認
* 測試代理程式時，請先開啟連線管理員以指派連線給工作階段，然後按&#x200B;**重試**。

## 驗證 {#authentication}

Adobe代管的MCP伺服器會實作OAuth，並與Adobe的身分識別系統整合。

* 當MCP使用者端應用程式連線至AEM MCP伺服器時，使用者會看到Adobe登入對話方塊，並使用其&#x200B;**Adobe ID**&#x200B;進行驗證
* 成功登入後，系統會驗證貴組織是否允許MCP使用者端應用程式，以及是否允許請求的MCP伺服器。 如果任一檢查失敗，則會顯示錯誤訊息。

![不允許的MCP使用者端錯誤](assets/MCP-Client-not-permitted.png)

* 驗證後，MCP伺服器會發行應用程式用於後續工具呼叫的權杖
* MCP工具會遵守使用者的AEM許可權。 無權在AEM中修改內容片段的使用者也無法透過MCP修改它。

這可確保AI協助的作業符合您現有的AEM安全性和治理模型。

## 搭配AEM使用MCP {#using-mcp-with-aem}

設定AEM和MCP使用者端應用程式後，您就可以使用您選擇的應用程式，並提示LLM執行AEM作業。 LLM會讀取MCP工具結構、選擇要呼叫的工具，並根據需要排序這些工具，以符合您的要求。

>[!IMPORTANT]
>
>為獲得最佳結果，尤其是當提示包含多個步驟或鎖定不同的內容型別（例如影像和文字）時，請在MCP使用者端中啟用思考模式或選取「思考」選項，而不是依賴「自動」模式。

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
   * 匯入資產
   * 尋找現有資產
   * 發佈資產。

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

*「根據我們的主圖橫幅模式，為春季行銷活動建立新的內容片段，並從此簡介填寫其欄位。」*

LLM會自動選擇並協調必要的MCP工具。

## 期望管理 {#expectation-management}

透過MCP使用LLM時，請記住下列事項：

* **功能強大，但並非絕對可靠**
LLM可以完成複雜的工作，但容易偶爾發生錯誤。 相同的提示可能會產生稍微不同的結果或簡報，但並無明顯的原因。 將變更套用至生產內容之前，請務必檢閱輸出。

* **不斷發展的功能**
LLM模型不斷改進。 隨著時間推移，他們在發現結合MCP工具以實現您的目標的新方法方面變得更聰明。 今天需要多個提示的工作，明天可能會順暢地搭配單一提示運作。

* **人力監督是必要的**
將LLM視為需要監督的知識淵博的助理。 它擁有廣泛的知識，可以設計創意解決方案，但受益於您的指導和審查。 驗證結果，特別是關鍵作業的結果，並在輸出不符合預期時提供意見回饋。

* **自動確認工具執行時請小心**
有些MCP使用者端應用程式（例如Claude）會提供LLM要求的自動認可工具執行的選項。 雖然這樣便於搜尋或擷取內容等唯讀操作，但請謹慎使用更新或刪除內容的工具。 在確認修改AEM環境的動作之前，請檢閱每個工具執行請求。

## 限制 {#limitations}

AEM的MCP伺服器目前預計在ChatGPT、Claude、Cursor和Microsoft Copilot Studio中進行設定。

如果您想要使用不同的MCP使用者端應用程式，請隨時與&#x200B;**aemcs-mcp-feedback@adobe.com**&#x200B;連絡，要求支援其他使用者端或允許列出自訂使用者端。
