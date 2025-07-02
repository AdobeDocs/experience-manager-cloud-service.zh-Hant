---
title: Content Credentials整合
description: Content Credentials已整合至AEM Assets並在Assets檢視中提供，可提供資產歷史記錄的上下文，包括資產的製作方式以及參與建立資產的對象。 就像數位內容的營養標籤一樣，Content Credentials可以協助提高透明度並與受眾建立信任。
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: fb7ce7dbb58be9fef5ab087441457770828d73c8
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Content Credentials {#content-credentials}

各大品牌對於內容透明度、AI揭露以及防止資產竄改的關注度前所未有。 Adobe的Content Authenticity Initiative (CAI)建立符合[內容來源與真偽聯盟](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA)技術標準的工具。 Content Credentials是一種新型加密的、可顯示竄改的中繼資料，可協助檢視者瞭解內容譜系並確保品牌資產的完整性。 資料中可包含各種來源資料，可將insight納入數位資產的歷史中。

此資訊可能包括：

* **簽發者或簽署者：**&#x200B;發行數位簽章以驗證或簽署資產的實體或公司的相關資訊。
* **問題日期：** Content Credential套用至資產的日期。
* **評分和使用狀況：**&#x200B;資產製作者的相關資訊，包括名稱、社群媒體控制代碼或其他身分相關資訊。
* **處理序：**&#x200B;對資產進行任何編輯或修改的記錄。
* **裝置詳細資料：**&#x200B;用來建立或編輯資產的應用程式或裝置相關資訊。
* **使用的AI工具：**&#x200B;如果使用generative AI編輯或建立資產，則可能會包含使用的模型名稱。
* **其他相關資訊：**&#x200B;可能也會包含其他資料，以協助提供有關資產歷史記錄的更多內容。

如需完整檢視，[驗證](https://contentcredentials.org/verify)可提供更完整的資產歷史記錄insight。

Adobe Experience Manager Assets現在支援Content Credentials，可讓使用者直接在AEM的Assets檢視中檢視Content Credentials。 檢視資產詳細資訊時，任何包含Content Credentials的影像（例如使用GenAI服務建立的影像）都會在專用面板中顯示資訊清單詳細資訊。 如果資產已下載、發佈或共用，Content Credentials會與資產維持不變。

![個資產](/help/assets/assets/content-credentials.png)

## 存取Content Credentials {#access-content-credentials}

1. 前往Assets檢視UI，然後從左窗格按一下&#x200B;**Assets**。
1. 導覽至資料夾，然後選取所需的資產。
1. 按一下&#x200B;**詳細資料**，然後從最右邊的窗格中選取`Cr pin`。 Content Credentials標籤會顯示資產的下列資訊。
   1. **產生的影像：**&#x200B;套用Content Credentials的日期和時間。
   1. **內容摘要：**指出資產是部分或完全由AI產生，或是如何編輯。
      ![內容認證](/help/assets/assets/content-credentials1.png)
   1. **處理序：**詳細說明用來產生資產的應用程式、裝置和AI工具(例如Adobe Firefly)，以及後續進行的變更。
      ![處理程式](/help/assets/assets/CR-Process.png)
   1. **關於此Content Credentials：**簽發者的名稱以及簽發日期和時間。
      ![簽發者](/help/assets/assets/CR-issuer.png)
