---
title: Governance Agent概述
description: 瞭解AEM Governance Agent如何跨AEM保障品牌完整性和合規性
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 9b26cd1f30ad6fa23e28c9f36fe48091e069962e
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Governance Agent概述 {#governance-agent}

**治理代理程式**&#x200B;是專為在Adobe Experience Manager中保護品牌完整性和合規性而設計的解決方案。 它會執行安全性、法規及品牌政策，以確保每次互動與啟用都遵循既定的標準。 Governance Agent已完全整合在AI Assistant中，且設計成可利用&#x200B;**A2A (Agent-to-Agent)**&#x200B;及&#x200B;**MCP （模型控制通訊協定）**&#x200B;工具，在企業環境中順暢運作。 這些整合可讓代理程式與進階AI協調者（例如ChatGPT、Claude和其他外部AI系統）連線，以確保跨平台的靈活且可擴充的智慧。

主要功能包括：

* **品牌治理：**&#x200B;藉由自動執行跨內容和資產的品牌檢查，維持品牌一致性並減少手動檢閱
* **許可權與Digital Rights Management (DRM)：**&#x200B;藉由控制數位資產的許可權與使用許可權，確保安全且合規的協同合作。

結合這些功能，治理代理程式就能降低風險，並實現快速、安全且大規模的品牌上交付。

>[!IMPORTANT]
>
>AI產生的回應可能不準確或誤導。 請務必仔細檢查建議的修正和回應。
>
>另請參閱[Adobe Experience Cloud Generative AI使用者指南](https://www.adobe.com/tw/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

## AEM Governance Agent技能 {#skills-in-aem-governance-agent}

### 品牌控管 {#brand-governance}

治理代理程式可以根據品牌指引驗證內容，以確保所有數位體驗的一致性。 它會使用預先擷取的品牌規則，例如色調、宣告、標誌使用、印刷樣式和影像。 它在Experience Hub的聊天、編輯和批次模式下即時運作，因此非常適合用於AI產生的內容、網站移轉和以簡短為基礎的網站建立。

![品牌治理總覽](/help/ai-in-aem/agents/governance/assets/brand-governance.png)

**提示範例：**

* *此頁面是否符合我的品牌？`https://www.website/en.html`*
* *此`https://www.website/en.html`是否遵循品牌訊息指南？*
* *檢查`https://www.website/homepage`是否遵循品牌方針*
* *顯示我的品牌指南*

### 許可權與Digital Rights Management {#permission-and-digital-rights-management}

#### Content Hub中的許可權管理 {#permission-management-in-content-hub}

在Content Hub中，治理代理程式可確保只有合適的人在合適的時間存取合適的資產。 藉由套用精細的、以屬性為基礎的控制項和使用許可權，它可以保護敏感內容，同時啟用安全的共同作業。 這表示降低法規遵循風險、加強品牌誠信度，以及加快工作流程，讓團隊可以放心地共用及重複使用資產，不必擔心未經授權的存取或濫用。 在安全性與彈性之間取得平衡，可提升營運效率，並提升整個組織的信任度。

![許可權管理概觀](/help/ai-in-aem/agents/governance/assets/permission-management.png)

**提示範例：**

* *顯示所有現有的Content Hub ABAC規則。*
* *建立可讓「行銷」群組存取所有資產的規則。*
* *授予Sales群組存取行銷:segment等於EMEA之資產的許可權。*
* *刪除所有可存取外部代理的規則*
* *什麼是Content Hub中的ABAC，您可以協助我做什麼？*

#### Assets Digital Rights Management {#assets-digital-rights-management}

使用代理程式，您可以在內容生態系統中管理您的Assets數位版權。 它會在精細的層級控制許可權和使用許可權，確保僅在定義的合規性範圍記憶體取和使用資產。 這讓您完全安心、保護智慧財產、降低法規風險，以及維持品牌完整性。 透過自動化許可權強制執行，團隊可以安全且自信地共同作業，加速內容發佈，而不會影響安全性或合規性。

![DRM管理總覽](/help/ai-in-aem/agents/governance/assets/drm-management.png)

**提示範例：**

* *我的任何資產是否即將到期？*
* *尋找上個月過期的所有腳踏車資產。*
* *哪些資產最近過期？*
* *尋找沒有到期日期的資產*
* *顯示/content/dam/products中將在未來14天到期的所有資產*

