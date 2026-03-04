---
title: 如何匯入品牌原則
description: 使用Adobe Governance Agent匯入品牌原則
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 94d671ebbd5aeb5992fdbc9d779ffbca51f82585
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---


# 如何匯入品牌原則 {#how-to-import-a-brand-policy}

## 概觀 {#overview}

品牌原則定義規則、標準和限制，以確保Adobe Experience Manager產生或更新的所有內容都與公司的品牌識別一致。 這通常包括語調、術語、視覺准則和編輯規則。

治理代理程式會使用品牌政策作為信任來源，以分析現有頁面並引導內容產生。 客戶可以提供其原始品牌原則，治理代理程式會自動將其轉換為AI可讀的原則檢查。 這些檢查接著用於驗證內容，並為生產代理程式提供可靠、可執行的架構，以產生或更新與品牌一致的頁面。

## 什麼是治理代理程式中的品牌原則 {#what-is-a-brand-policy-in-the-governance-agent}

在治理代理程式的內容中，品牌政策是品牌規則的結構化表示，可由AI理解和執行。 治理代理程式不要求客戶以技術格式重寫其指引，而是接受原始格式的品牌原則（例如檔案、指引或規則說明）。

匯入後，該原則將轉換為一組AI原則檢查，這些檢查可以：

* 分析現有頁面以偵測品牌不一致
* 標示語氣、術語或強制規則的偏差
* 為下游代理程式提供明確指引
* 透過設計確保產生或更新內容符合品牌規範

此方法可讓團隊重複使用其現有的品牌檔案，同時受益於自動化治理和可擴展的內容生產。

## 如何使用品牌原則 {#how-brand-policies-are-used}

品牌原則匯入後：

* 治理代理程式會解譯原則並將原則標準化為可強制執行的AI檢查
* 可以根據原則來分析頁面，以找出差距或違規
* 生產代理程式在產生或更新內容時使用這些檢查作為限制
* 跨網站和團隊的品牌合規性變得一致、可重複和可稽核


## 匯入品牌原則 {#import-a-brand-policy}

若要將品牌匯入治理代理程式：

1. 藉由指定名稱和主網域來建立品牌。 若要這麼做，請按一下Experience Manager首頁左側導覽列中的&#x200B;**治理內容**&#x200B;按鈕，然後按「**+新增品牌**」按鈕，如下所示：

   ![新增品牌](/help/ai-in-aem/agents/governance/assets/add_brand.png){width="70%"}

1. 在下列視窗中設定品牌名稱和說明

   ![為品牌命名](/help/ai-in-aem/agents/governance/assets/add_brand_dialogue.png){width="60%"}

1. 新品牌會以草稿狀態建立。 請確定您已將新建立的品牌變更為使用中狀態，方法是按一下您品牌的卡片、按一下熒幕右上角的編輯（鉛筆）、在下列視窗中將&#x200B;**狀態**&#x200B;設定為&#x200B;**使用中**，然後按一下&#x200B;**儲存變更**。 您必須先將品牌設定為「作用中」以啟用品牌，才能使用品牌。

   ![將品牌狀態設定為[作用中]](/help/ai-in-aem/agents/governance/assets/set_brand_active.png){width="60%"}

1. 建立品牌後，按下左邊的&#x200B;**網域**&#x200B;連結，在下列視窗中建立主網域：

   ![設定品牌的網域](/help/ai-in-aem/agents/governance/assets/add_domain.png)

   >[!IMPORTANT]
   >
   >就像新品牌一樣，新網域是以預設草稿狀態建立的。 若要變更此專案，請移至您的品牌，按一下&#x200B;**網域**，然後使用鉛筆圖示編輯您的網域，並將其狀態設為&#x200B;**作用中**。

1. 設定主要網域後，您可以透過在視窗左上角的&#x200B;**原則**&#x200B;上按下&#x200B;**+新增原則**&#x200B;按鈕，上傳您的品牌原則檔案。

   ![從品牌卡新增原則](/help/ai-in-aem/agents/governance/assets/add_policy_treeview.png)

   >[!NOTE]
   >
   >或者，您也可以切換到&#x200B;**原則**&#x200B;索引標籤並按&#x200B;**+新增原則**&#x200B;連結，以新增原則。

1. 在下一個視窗中，按&#x200B;**上傳PDF**，並以PDF格式選取您的品牌原則檔案

   ![上傳您的品牌原則檔案](/help/ai-in-aem/agents/governance/assets/upload_brand_policy_document.png){width="70%"}

   治理代理程式將使用自然語言來剖析您的品牌政策指引，並會擷取從檔案取得的檢查，並將其翻譯成實際工作。 處理檔案後，您可以檢視匯入的摘要，包括檢查次數和原則的狀態，如下所示：

   ![品牌原則狀態的概觀視窗](/help/ai-in-aem/agents/governance/assets/policy_status.png)

1. 建立您的品牌並上傳原則檔案後，您可以前往「**品牌**」標籤，然後按一下品牌的卡片，取得每個品牌的詳細檢視。 這是您要用來建立檢查類別組的檢視表，方法是按現有類別旁的三個點，然後選取&#x200B;**+新增類別**，如下方熒幕擷取所示：

   ![新增類別](/help/ai-in-aem/agents/governance/assets/add_category.png)

   您也可以使用此檢視來建立、編輯和刪除檢查，我們將在以下步驟中詳述這些檢查。

1. 如需更精細的個別檢查檢視，您可以切換至&#x200B;**檢查**&#x200B;標籤，並檢視從指引檔案中擷取的個別檢查清單。 您可以根據品牌或狀態來篩選檢查：

   ![檢視個別品牌檢查](/help/ai-in-aem/agents/governance/assets/see_brand_checks.png)

   此外，您可以按一下支票左側的三個點(**...**)，並按&#x200B;**檢視詳細資料**，以檢視個別支票的其他詳細資料。 這將開啟一個新視窗，其中包含有關檢查的更多資訊：

   ![檢視個別支票詳細資料](/help/ai-in-aem/agents/governance/assets/view_check_details.png)

   您也可以在相同的功能表位置按&#x200B;**Delete**&#x200B;刪除支票，或按&#x200B;**編輯**&#x200B;編輯支票：

   ![編輯支票](/help/ai-in-aem/agents/governance/assets/edit_check.png)

1. 您可以在[支票]視窗的左上角按下&#x200B;**新增支票**，以手動方式新增支票：

   ![新增支票](/help/ai-in-aem/agents/governance/assets/add_check.png)

   在下列畫面中，您可以設定詳細資訊，例如：

   * 支票的名稱
   * 以自然語言描述的規則
   * 類別
   * 其套用的範圍

   ![設定檢查詳細資料](/help/ai-in-aem/agents/governance/assets/add_check_window.png)

1. 最後，若要取得網域及其關聯品牌的清單，您可以按下&#x200B;**網域**&#x200B;索引標籤。 此區段可讓您新增、刪除或修改清單中的網域。

