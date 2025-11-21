---
title: Experience Development Agent概述
description: 瞭解AEM中的Experience Development Agent如何分析Cloud Manager中的失敗管道和建置記錄檔，以建議程式碼修正並加快偵錯速度。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 1f20d2825befa0345f9ebde3a9854cab591de0f6
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---


# Experience Development Agent概述 {#development-agent-overview}

Experience Development Agent可協助AEM開發人員和管理員更有效率地建立、偵錯、部署及最佳化程式碼。

目前，代理程式可以擷取管道狀態，並透過建議修正來協助您疑難排解失敗的建置步驟，進而節省在開發、中繼和生產環境中偵錯AEM as a Cloud Service部署的時間。 它會檢查組建記錄檔和相關程式碼，以建議您可以手動套用的修正。

>[!IMPORTANT]
>
>AI產生的回應可能不準確或誤導。 請務必仔細檢查建議的修正和回應。
>
>另請參閱[Adobe Experience Cloud Generative AI使用者指南](https://www.adobe.com/tw/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

## 透過Cloud Manager存取體驗開發代理程式 {#how-to-access-the-agent}

您透過使用者介面(包括Cloud Manager或Experience Hub)中的AI助理來存取Experience Development Agent。

**透過Cloud Manager存取Experience Development Agent：**

1. 若要開始使用，請按一下[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)以開啟其首頁。

   ![Adobe Experience Cloud首頁](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. 在左側邊欄的&#x200B;**服務**&#x200B;標題下，按一下&#x200B;**Cloud Manager**。

   ![已選取顯示內容作者預設集的下拉式清單](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >顯示的Widget、工具和成品取決於使用者角色、權益和AEM部署型別(AEM as a Cloud Service或Managed Services 6.5/6.5 LTS)。

1. 在左側邊欄的&#x200B;**方案**&#x200B;下，按一下&#x200B;**![總覽圖示](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg)總覽**。

1. 在&#x200B;**方案總覽**&#x200B;頁面的&#x200B;**管道**&#x200B;卡中，按一下管道。

   ![選取的管道](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-select.png)

1. 在&#x200B;**建置和程式碼掃描**&#x200B;頁面中，請注意失敗的管道。

   ![在建置和程式碼掃描頁面中看到管道失敗](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-failure.png)

1. 在AEM使用者介面(從Cloud Manager頁面或AEM環境的作者執行個體)的右上角附近，按一下&#x200B;**AI助理**&#x200B;圖示。

   工具列上的![AI助理圖示](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   另請參閱AEM中的[AI小幫手](/help/implementing/cloud-manager/ai-assistant-in-aem.md)。

1. 在底部附近的&#x200B;**AI小幫手**&#x200B;面板文字方塊中，輸入您的問題或提示，然後按`Enter`或按一下![傳送圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)。

   例如：
   *在[eda-org-01-no-access]程式中，分析[no-access]管道的失敗並進行疑難排解。*

   提示會產生以下回應。

   ![AI助理提示和產生的回應](/help/ai-in-aem/agents/development/assets/dev-agent-prompt-response.png)


## 權限 {#permissions}

Experience Development Agent的管道疑難排解工作需要Cloud Manager — 開發人員角色或Cloud Manager — 方案管理員角色。



## 範例提示 {#sample-prompts}

| 提示 | 結果 |
| --- | --- |
| *列出我失敗的主要程式管道。* | 雖然結果可能有所不同，但此提示應輸出失敗管道的表格，並提供後續建議，以參考要分析的特定管道。 |
| *分析我的失敗管道，稱為「開發管道」。* | 此提示應會分析失敗的管道，並提供修正的建議。 |

## 超出範圍的功能 {#out-of-scope-features}

管道疑難排解會在完整棧疊管道的建置步驟中操作。 對於其他管道型別和步驟，透過下載和檢查日誌來偵錯失敗。

檢視[存取及下載記錄檔](/help/implementing/cloud-manager/manage-logs.md)。

使用BYOGIT （自備Git）的程式不支援管道疑難排解。

