---
title: 開發工作總覽
description: 瞭解AEM中的開發工作如何分析Cloud Manager中的失敗管道和建置記錄檔，以建議程式碼修正並加快偵錯速度。
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Architect, Developer
exl-id: 2194556f-aac2-4cdd-8f7f-00c92c8c4424
source-git-commit: a38d153194f977cf305bece1d9cae676800f52d6
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---


# 開發工作總覽 {#development-job-overview}

[作為Brand Experience Agent的一部分，](/help/ai-in-aem/agents/brand-experience/overview.md)開發工作可協助AEM開發人員和管理員更有效率地建立、偵錯、部署及最佳化程式碼。

這項工作可以擷取管道狀態，並透過建議修正來幫助疑難排解失敗的建置步驟，以節省在開發、中繼和生產環境中對AEM as a Cloud Service部署進行偵錯的時間。 它會檢查組建記錄檔和相關程式碼，以建議您可以手動套用的修正。

>[!VIDEO](https://video.tv.adobe.com/v/3478006?quality=12&learn=on)

>[!IMPORTANT]
>
>AI產生的回應可能不準確或誤導。 請務必仔細檢查建議的修正和回應。
>
>另請參閱[Adobe Experience Cloud Generative AI使用者指南](https://www.adobe.com/tw/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

>[!NOTE]
>
>管道疑難排解僅限於完整棧疊管道（部署和程式碼品質），但現在在Beta版中提供&#x200B;**Web層設定管道**&#x200B;的支援。 若要要求存取權，請傳送電子郵件至[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)。 需要預先存取AEM中的代理程式。

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

若要存取此工作，請參閱[發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)中有關如何註冊Beta版計畫的說明，請務必指出您對開發工作的興趣。 您也可以以電子郵件將開發工作的特定意見回饋傳送至[aem-devagent@adobe.com。](mailto:aem-devagent@adobe.com)

[觀看教學課程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/development-agent-troubleshoot-ci-cd-pipeline)，瞭解如何使用開發代理程式來疑難排解管道故障。

## 透過Cloud Manager存取開發工作 {#how-to-access-the-job}

您透過使用者介面(包括Cloud Manager或Experience Hub)中的AI助理存取開發工作。

1. 若要開始使用，請按一下[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)以開啟其首頁。

   ![Adobe Experience Cloud首頁](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. 在左側邊欄的&#x200B;**服務**&#x200B;標題下，按一下&#x200B;**Cloud Manager**。

   ![已選取顯示內容作者預設集的下拉式清單](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >顯示的Widget、工具和成品取決於使用者角色、權益和AEM部署型別(AEM as a Cloud Service或Managed Services 6.5/6.5 LTS)。

1. 在左側邊欄的&#x200B;**方案**&#x200B;下，按一下&#x200B;**![總覽圖示](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg)總覽**。

1. 在&#x200B;**方案總覽**&#x200B;頁面的&#x200B;**管道**&#x200B;卡中，按一下管道。

   ![選取的管道](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-select.png)

1. 在&#x200B;**建置和程式碼掃描**&#x200B;頁面中，請注意失敗的管道。

   ![在建置和程式碼掃描頁面中看到管道失敗](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-failure.png)

1. 在AEM使用者介面(從Cloud Manager頁面或AEM環境的作者執行個體)的右上角附近，按一下&#x200B;**AI助理**&#x200B;圖示。

   工具列上的![AI助理圖示](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   另請參閱AEM中的[AI小幫手](/help/implementing/cloud-manager/ai-assistant-in-aem.md)。

1. 在底部附近的&#x200B;**AI小幫手**&#x200B;面板文字方塊中，輸入您的問題或提示，然後按`Enter`或按一下![傳送圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)。

   例如：
   *在[eda-org-01-no-access]程式中，分析[no-access]管道的失敗並進行疑難排解。*

   提示會產生以下回應。

   ![AI助理提示和產生的回應](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-prompt-response.png)


## 權限 {#permissions}

開發工作需要Cloud Manager — 開發人員角色或Cloud Manager — 方案管理員角色。

## 範例提示 {#sample-prompts}

| 提示 | 結果 |
| --- | --- |
| *疑難排解我失敗的管道* | 執行管道失敗原因的分析；如果不清楚引用了哪個管道，將向使用者詢問其他問題。 |
| *列出我失敗的主要程式管道。* | 雖然結果可能有所不同，但此提示會輸出失敗管道的表格，並提供後續建議，以參考要分析的特定管道。 |
| *分析我的失敗管道，稱為「開發管道」。* | 此提示會分析失敗的管道，並提供修正的建議。 如果多次失敗，則會詢問使用者的其他問題。 |
| *疑難排解管道執行1234567* | 透過提供精確的管道執行ID，會執行管道分析。 |

## 超出範圍的功能 {#out-of-scope-features}

管道疑難排解會在完整棧疊部署和計畫碼品質管道中的建置和單元測試步驟和計畫碼掃描步驟中操作。 對於其他管道型別和步驟，透過下載和檢查日誌來偵錯失敗。

如需詳細資訊，請參閱[存取及下載記錄檔](/help/implementing/cloud-manager/manage-logs.md)。
