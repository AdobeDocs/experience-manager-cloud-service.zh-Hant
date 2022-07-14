---
title: 開發人員和部署管理器任務
description: 一旦系統管理員設定了必要的雲資源，瞭解開發人員和部署經理如何訪問git來開發應用程式並使用管道來部署它們。
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 1%

---


# 開發人員和部署管理器任務 {#developer-deployment-manager}

在 [登機之旅，](overview.md) 您將瞭解開發人員和部署經理如何訪問git來開發應用程式並使用管道來部署它們。

## 到目前為止的故事 {#story-so-far}

你在登機旅程中走了很遠的路！ 恭喜！ 系統管理員已通過設定必要的雲資源並授予文檔中的訪問權限來完成登陸過程 [分配AEM產品配置檔案。](assign-profiles-aem.md)

此時，您的開發人員和部署經理可以開始建立您自己的應用程式，而AEM您的用戶可以開始建立內容。 從這個意義上講，您的入職已經完成，現在是時候使用您的AEM新as a Cloud Service系統了，本文檔將說明這一點。

## 對象 {#audience}

因此，本檔案是從 **開發者** 和 **部署管理器**。

系統管理員也可以執行這些相同的任務，但通常這些角色由不同的用戶擔任。

## 目標 {#objective}

本文檔是對登陸過程的補充，以在系統管理員已登陸所有用戶並建立了必要的雲資源後，演示開發人員和部署經理的基本任務。

閱讀此文檔後，您應：

* 作為開發人員，瞭解如何訪問和管理Cloud Manager Git儲存庫。
* 作為部署管理器，可以在雲管理器中設定管道並部署代碼。

## 開發人員和部署經理 {#roles}

一旦系統管理員完成了建立用戶和設定雲資源等主要登陸任務，通常最急切地訪問系統的用戶是開發人員和部署經理。 這是因為他們是負責在as a Cloud Service之上構建自定義應用程式的AEM用戶。

* **開發人員**  — 這些用戶訪問Cloud Manager Git儲存庫，在該儲存庫中他們將管理您的自定義應AEM用程式碼。
* **部署管理器**  — 這些用戶使用雲管理器建立並運行管道，這些管道將代碼從Git儲存庫部署到您運行的AEM環境。

根據您的組織需要，同一個用戶可以同時具有兩個角色。

## 必備條件 {#prerequisites}

在您以開發人員或部署經理的身份開始本文檔中描述的任務之前，請確保您的系統管理員已經完成了登機過程中的所有步驟。 這意味著：

* 系統管理員已將開發人員和部署經理分配給他們各自的產品配置檔案。
* 開發人員必須另外分配給 **用AEM戶** 或 **管AEM理員** 產品配置檔案，以便也使AEM用。
* 已設定雲資源。

## 訪問Git {#accessing-git}

您可以使用Cloud Manager中的自助Git帳戶管理來訪問和管理您的Git儲存庫。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **管線** 卡 **計畫概述** 頁面並查找 **訪問回購資訊** 按鈕來訪問和管理git儲存庫。

   ![訪問環境卡上的「回購資訊」按鈕](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 按一下 **查看回購資訊** 按鈕開啟對話框以查看：

   * Cloud Manager Git儲存庫的URL。
   * Git用戶名。
   * git密碼，其值在 **生成密碼** 按鈕

   ![儲存庫資訊](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用這些憑據，用戶可以克隆儲存庫的本地副本，並在該本地儲存庫中進行更改，並且在準備就緒後，可以將任何代碼更改提交回雲管理器中的遠程代碼儲存庫。

## 管道設定 {#setup-pipeline}

一旦開發人員將其自定義代碼添加到您的Git儲存庫，部署管理器就可以建立並執行管道，以將該代碼部署到您AEM的環境。

按照以下步驟建立第一個非生產部署管道。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 訪問 **管線** 從Cloud Manager主螢幕獲取卡。 按一下 **+添加** 選擇 **添加非生產管道**。

   ![添加非生產管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在 **配置** 頁籤 **添加非生產管道** 對話框，選擇要添加的非生產管線類型。 對於此示例，選擇 **部署管道**。

   ![「添加非生產管道」對話框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 提供 **非生產管道名稱** 以標識管線以及以下附加資訊。

1. 對於 **部署觸發器** 選擇 **手動** 這樣管道才會在啟動時運行。

1. 按一下 **繼續**。

1. 在 **原始碼** 頁籤 **添加非生產管道** 對話框，必須選擇管道應處理的代碼類型。 對於此示例，選擇 **完整堆棧代碼**。

1. 在 **原始碼** 頁籤。

   * **合格的部署環境**  — 必須選擇管道應部署到的環境。
   * **儲存庫**  — 此選項定義管道應從哪個git回購中檢索代碼。
   * **Git分支**  — 此選項定義管線中應從哪個分支檢索代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將查找匹配的分支以幫助您選擇。

   ![全堆棧管線](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 按一下「**儲存**」。

您現在已建立第一個管道！ 具有部署管理器角色的用戶現在可以從雲管理器UI啟動管道。

## 部署 {#deploy}

現在，開發人員已將其自定義代碼添加到git儲存庫，並且您已建立了管道來部署該代碼，現在是時候執行該管道，將該代碼從git實際移動到您的環境了。

![雲管理器中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **管線** 卡 **計畫概述** 並按一下上一節中建立的管線旁邊的省略號按鈕，然後選擇 **運行** 的子菜單。

1. 管線運行開始，並由 **狀態** 的雙曲餘切值。

通過再次按一下省略號按鈕並選擇 **查看詳細資訊**。

恭喜！ 您現在已將代碼從Git儲存庫部署到非生產環境！

## 下一步是什麼 {#whats-next}

現在您已閱讀了此文檔，您應：

* 作為開發人員，瞭解如何訪問和管理Cloud Manager Git儲存庫。
* 作為部署管理器，可以在雲管理器中設定管道並部署代碼。

您已以開發人員或部署經理的身份開始運行，不僅具備Cloud Manager的工作知識，還具備工作環境、儲存庫和管道！ 但是，要瞭解AEMas a Cloud Service強大的CI/CD工具，還有更多需要。 查看 [其他資源](#additional-resources) 的子菜單。

如果您對內容作者如何訪問和使用雲服務感AEM興趣，請繼續執行登入過程的最後一部分， [用AEM戶任務。](aem-users.md)

>[!TIP]
>
>現在你已經上船了 [瞭解如何輕鬆添加AEM參考演示載入項](/help/journey-sites/demos-add-on/overview.md) 以最少的配AEM置到沙盒環境，並能夠test功能強大的功能AEM，並提供基於最佳實踐的豐富示例。

## 其他資源 {#additional-resources}

* [訪問儲存庫](/help/implementing/cloud-manager/managing-code/accessing-repos.md)  — 瞭解如何使用Cloud Manager的自助Git帳戶管理來訪問和管理您的Git儲存庫。
* [將Git與雲管理器一起使用](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)  — 瞭解如何使用Cloud Manager的Git儲存庫，以及如何將您自己的內部客戶管理的Git儲存庫與Cloud Manager整合。
* [建立地方發展環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)  — 本教程將指導您使用as a Cloud ServiceSDK為Adobe Experience Manager(AEM)設定本AEM地開發環境。
* [AEM Sites入門 — WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)  — 本多部分教程是為Adobe Experience Manager()的新開發人員設計AEM的。 本教程將介紹虛擬生AEM活品牌WKND的站點實施。 本教程介紹一些基本主題，如項目設定、核心元件、可編輯模板、客戶端庫以及與Adobe Experience Manager Sites的元件開發。
* [使用SPA反AEM應](/help/implementing/developing/hybrid/getting-started-react.md)  — 本文介紹一SPA個示例應用程式，說明它的組合方式，並允許您使用React框架快速啟動SPA並運行。
* [使用AngularSPA入門AEM](/help/implementing/developing/hybrid/getting-started-angular.md)  — 本文介紹一SPA個示例應用程式，說明它的組合方式，並允許您使用Angular框架快速啟動和運SPA行自己的應用程式。
* [無頭開發者之旅](/help/journey-headless/developer/overview.md)  — 從此處開始，學習有關開發無頭應用程式的指導課程AEM。
