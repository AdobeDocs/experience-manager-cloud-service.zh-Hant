---
title: Adobe Experience Manager (Beta)中的AI助理
description: 使用AI助理協助您針對Adobe Experience Manager中可用的解決方案尋找答案和進行疑難排解。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 577e15165057fcf6537b4b0b738a1f45e5feb097
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 1%

---

# Adobe Experience Manager中的AI助理 {#aem-home}

AEM (Adobe Experience Manager) AI Assistant提供對話式介面，旨在簡化為Adobe Experience Manager相關查詢尋找答案的程式。 它可協助您即時取得與AEM產品相關問題的解答（*可供所有使用者使用*），並自動建立支援票證（*可供支援管理員使用*）。

在私人測試版期間，AEM AI Assistant支援AEM as a Cloud Service，包括下列解決方案：

* Sites
* Assets
* Dynamic Media
* Edge Delivery Services
* Cloud Manager
* Forms

此視覺效果直接內嵌於AEM中，並可從AEM Experience Hub、Cloud Manager及作者UI存取。

>[!IMPORTANT]
>請確定您已檢閱並提交使用者合約，因此Adobe可以啟用AI Assistant功能，供您測試並參與私人測試版計畫。
>
>如有任何問題，請透過與Adobe ID相關聯的電子郵件地址傳送電子郵件至[Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com)。

## 範圍 {#scope}

AEM AI Assistant目前的範圍著重於解決Adobe Experience Manager as a Cloud Service的產品知識問題。 此範圍包含關鍵領域的完整支援，例如Sites、Assets、Forms、Edge Delivery Services和Cloud Manager。

* **介面**：適用於AEM Experience Hub、作者UI、Cloud Manager。
* **功能**：產品知識以及疑難排解和指引的第一站、自動建立支援票證和查詢。
* **Value**：節省時間、加速學習及創造價值的時間、減少手動建立支援票證的需求，並提高建立支援票證的效率。

## 隱私權、安全性和治理{#privacy-security-governance}

AEM AI Assistant的設計強調隱私、安全性和治理。

本文概述您可以從AEM AI Assistant期待的以信任為中心的功能：

* AEM AI Assistant不使用任何個人資料，包括訓練用資料。
* AEM AI助理無法存取消費者資料。
* 需要明確許可權才能與AEM AI助理互動。
* 使用者提供的提示（問題、查詢等）不會與其他客戶共用。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->


## 瞭解產品知識和自動支援票證建立的AEM AI Assistant {#ai-prod-insights}

產品知識包含從Adobe Experience League檔案衍生的概念和主題。 這些問題可以歸類為以下子群組：


| 產品知識 | 可供所有使用者使用<br>範例 |
| :--- | :--- |
| 點式學習 | <ul><li>什麼是通用編輯器？</li><li>如何在Cloud Manager中建立程式？</li></ul> |
| 開啟探索 | <ul><li>如何使用通用編輯器？</li><li>是否有辦法將內容從一個環境複製到另一個環境？</li></ul> |
| 疑難排解 | <ul><li>為何無法存取通用編輯器？</li><li>我的管道為什麼會失敗？</li></ul> |
| **支援票證建立** | **僅支援管理員&#x200B;**<br>**範例** |
| 自動建立支援票證，擷取AI助理聊天記錄與內容 | <ul><li>為我建立支援票證。</li></ul> |
| 擷取支援票證的狀態 | <ul><li>顯示我已開啟的所有支援票證。</li><li>顯示票證「E-----------」的狀態</li></ul> |

{style="table-layout:auto"}


## 如何製作有效的問題 {#ai-craft-questions}

若要從AEM AI Assistant收到最準確的回應，請務必以清楚明瞭的內容表述您的問題。 使用下列提示來確保您的查詢清晰且結構良好：

* 以簡潔明瞭的方式清楚說明您的任務或問題。
* 請避免含糊不清的措辭或過於複雜的語法，以增進瞭解。
* 加入您任務或問題的相關內容，因為此方法有助於AEM AI助理提供更精確且相關的答案。
例如，在您的提示中，為您目前使用的AEM解決方案命名(Sites、Assets、Dynamic Media、Edge Delivery Services、Cloud Manager或Forms)會有所幫助。

### 不支援的問題範例 {#ai-unsupported-questions}

| 區域 | 範例 |
| --- | --- |
| 營運分析 | <ul><li>我的租使用者中有多少開發環境？</li><li>誰啟動了最後一個生產管道？</li></ul> |
| 疑難排解 | <ul><li>為什麼我的生產管道失敗？</li></ul> |
| 工作與自動化 | <ul><li>為我從開發分支設定程式碼品質管道。</li></ul> |


## 使用AEM AI助理 {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AEM AI Assistant access through Admin Console 

To use the AEM AI Assistant, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AEM AI Assistant in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AEM AI Assistant of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### 開始或重設交談

您可以重設AEM AI助理，並在想要變更主題時開始新的對話。 在疑難排解失敗的查詢或提供不正確的資訊時，此功能特別實用。

![開始交談按鈕](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**若要啟動或重設交談：**

1. 在AEM AI助理上，按一下![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 若要通知AEM AI助理有關新主題或主題變更，請按一下[開始新交談] **&#x200B;**。

### 使用可發現性

AEM AI Assistant包含可發現性功能，可協助您探索支援的主題和類別。

![創意燈泡圖示](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**使用可發現性：**

1. 在AEM AI Assistant的右上角附近，按一下![學習圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)。
1. 選取類別以檢視相關提示清單。
1. 選擇提示以更瞭解AEM AI Assistant可回答的問題型別。

### 提供AEM AI助理的意見回饋

您的輸入有助於改善AEM AI Assistant，以獲得更出色的效能和準確性。

透過下列選項，分享您對AEM AI Assistant體驗的意見反應：

![豎起大拇指、豎下大拇指和旗標圖示](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| 圖示 | 說明 |
| --- | --- |
| ![向上縮圖圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 按一下以指出哪些專案進展順利，並分享正面回饋。 |
| ![向下縮圖圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 按一下以提供改善建議。 新增有關您體驗的特定註解，這些註解每天都會稽核。 |
| ![標幟圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | 按一下「 」即可回報疑慮，或針對您與AEM AI助理的互動提供詳細的意見回饋。 |

## 關於AEM AI Assistant的常見問題 {#ai-faq}

以下是AI助理部分常見問題的解答：

* **AEM AI Assistant即時提供的資訊嗎？**\
  不行。AI助理從Adobe Experience League檔案取得其內容。 內容的更新可能需要一些時間才能反映在回應中。
* **AEM AI Assistant支援哪些Adobe應用程式？**\
  目前，AI Assistant支援AEM as a Cloud Service中的產品知識查詢，包括Sites、Assets、Dynamic Media、Cloud Manager和Forms。
* **AEM AI Assistant有哪些功能？**\
  AEM AI Assistant可回答與Adobe產品知識相關的查詢。
* **AEM AI助理是否使用個人資訊來訓練資料？**\
  不行。AEM AI助理不會將個人資訊用於訓練目的。 避免與AEM AI助理分享您或其他人的個人資訊，包括姓名或聯絡詳細資訊。


## AEM Forms AI助理(Forms Experience Builder) {#ai-forms-builder}

除了用於產品知識的一般AEM AI助理之外，AEM還提供專門的&#x200B;**[AEM Forms AI助理(Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**。 此增強型助理可以透過自然語言提示和回答表單特定問題，主動協助您建立及設定表單。

### 主要功能

AEM Forms AI Assistant提供：

* **表單建立**：使用自然語言說明從頭開始建立新表單。
* **設計匯入**：將現有的設計(PDF、Figma、影像)轉換為功能性AEM Forms。
* **表單設定**：新增欄位、面板、驗證規則和條件式邏輯。
* **配置管理**：組織表單結構並最佳化不同的裝置。
* **整合設定**：設定表單提交與資料處理。
* **產品知識**：回答有關AEM Forms功能和最佳實務的問題。

### 存取位置

AEM Forms AI Assistant的可用功能如下：

* **通用編輯器**：適用於具有視覺化編輯功能的Edge Delivery Services表單。
* **最適化Forms編輯器**：有關詳細的表單設定和進階功能。
* **Forms管理UI**：用於高階表單建立和管理工作。

### 快速入門

>[!NOTE]
>
> AEM Forms AI助理(Forms Experience Builder)可在私人測試版計畫下使用。 從您的工作地址傳送電子郵件至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)以要求存取權。

若要進一步瞭解如何使用AEM Forms AI小幫手，請參閱[AEM Forms AI小幫手](/help/edge/docs/forms/forms-ai-assistant.md)檔案。

### 範例使用案例

* **「建立包含名稱、電子郵件、評分和評論欄位的客戶意見回饋表單」**
* **&quot;將此上傳的PDF應用程式表單轉換為數位最適化表單&quot;**
* **「新增條件式邏輯，僅在婚姻狀態為「已婚」時顯示配偶資訊」**
* **&quot;設定此表單以提交資料至客戶關係管理系統&quot;**

這個專門的AEM Forms AI Assistant代表表單建立的下一個演化，結合AI的強大功能與AEM的強大表單功能，精簡您的表單建立工作流程。
