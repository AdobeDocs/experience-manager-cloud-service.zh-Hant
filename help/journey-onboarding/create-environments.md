---
title: 建立環境
description: 了解如何使用 Cloud Manager 來建立您的首個環境。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 53%

---

# 建立環境 {#create-environments}

在 [登機之旅，](overview.md) 您將學習如何使用Cloud Manager建立第一個環境。

## 目標 {#objective}

在閱讀了此上線過程中的上一個文件後，[建立程序，](create-program.md)您現在擁有自己的 Cloud Manager 程序。了解如何使用 Cloud Manager 來建立您的首個環境。

閱讀本文件後，您將了解：

* 了解什麼是環境。
* 了解不同環境之間的區別。
* 能夠建立自己的環境。

## 什麼是環境？ {#environments}

環境位於 Cloud Manager 層次結構中的程序之下。雖然程序允許您組織您的解決方案並授予特定團隊成員對這些程序的存取權限，但環境屬於特定程序並且是這些程序中 Adobe 解決方案的各個實例。環境用於特定目的，例如創作內容或測試新開發。Cloud Manager 的 CI/CD 管道有助於將計劃碼從 git 存放庫部署到這些環境。

如果你回想一下WKND旅遊和冒險企業理論的例子，它們可能有兩個節目。 即，其WKND雜誌部門的一個網站方案和WKND媒體部門的一個資產方案。 每個程序都可能有幾個環境，例如一個為網站的實際流量提供服務的生產環境和一個用於測試新應用程序計劃碼的開發環境。

有四種不同的環境類型：

* **生產與暫存** - 生產環境和暫存環境組成一組使用，分別用於生產和測試目的。
* **開發**  — 開發環境可用於開發和測試目的，且僅可與非生產管道關聯。
* **快速發展**  — 快速開發環境(RDE)允許開發人員快速部署和審查更改，從而最大限度地減少test已證明可在本地開發環境上工作的功能的時間。

為了完成本入門旅程，為了以最小的速度開始，您建立了一個開發環境，可以用於AEM探索as a Cloud Service的功能。

## 建立環境 {#creating-environments}

1. 登錄到Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 選擇要為其添加環境的程式。

1. 要添加環境，請從 **計畫概述** 頁，在 **環境** 卡，選擇 **添加環境**。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

      ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在出現的&#x200B;**新增環境**&#x200B;對話框中：

   * 選取&#x200B;**環境類型**。
      * 可用/已使用環境的數量會顯示在開發環境類型後面的括號中。
   * 提供&#x200B;**環境名稱**。
   * 提供&#x200B;**環境說明**。
   * 選取&#x200B;**雲端區域**。

   ![新增環境對話框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

環境可用後，您組織的成員將指派到&#x200B;**開發商** product profile 可以登入 Cloud Manager 管理 Cloud Manager 的 git 倉庫。

## 下一步 {#whats-next}

您已閱讀此入門歷程部分，您應該：

* 了解什麼是環境。
* 了解不同環境之間的區別。
* 能夠建立自己的環境。

您的雲端資源已建立並可供您的團隊存取。作為系統管理員，您必須首先將團隊成員分配給與Adobe Admin ConsoleAEMas a Cloud Service的產品配置檔案，以便他們可以訪問這些資源。

因此，您應繼續登機旅程，下次查看文檔 [為as a Cloud Service產品配置AEM檔案分配團隊成員](assign-profiles-aem.md)。 在該文檔中，您將學習如何授予團隊成員訪問新環境的權限。

## 其他資源 {#additional-resources}

如果您想超越登機旅程的內容，請選擇以下附加資源。

* [管理環境](/help/implementing/cloud-manager/manage-environments.md)  — 瞭解您可以建立的環境類型以及如何為Cloud Manager項目建立這些環境
* [使用Adobe雲管理器 — 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=zh-Hant) - Cloud Manager環境由創作、發AEM布和Dispatcher服務組成。 了解不同的環境可支援角色，並使用不同的 CI/CD 管道與其互動。
* [快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md)  — 有關如何使用RDE的詳細資訊，請參閱本文檔

<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

