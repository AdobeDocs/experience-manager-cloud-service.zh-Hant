---
title: 開發人員和部署管理員工作
description: 他們的系統管理員設定了必要的雲端資源後，了解開發人員和部署管理員如何存取 Git 來開發應用程式，並使用管道來部署它們。
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1397'
ht-degree: 100%

---


# 開發人員和部署管理員工作 {#developer-deployment-manager}

在此選用部分的[上線歷程](overview.md)中，您會了解開發人員和部署管理員如何存取 Git 來開發應用程式，並使用管道來進行部署。

## 目前進度 {#story-so-far}

您已在上線歷程中走了很長一段路！恭喜！系統管理員已透過設定必要的雲端資源，並在文件「[指派 AEM 產品設定檔](assign-profiles-aem.md)」中授與存取權，來完成上線歷程。

此時，您的開發人員和部署管理員可以開始建立您自己的應用程式，而您的 AEM 使用者可以開始建立內容。從這個角度上說，您的上線工作已經完成，現在是時候使用您的新 AEM as a Cloud Service 系統了，本文件將對此進行說明。

## 客群 {#audience}

因此，本文件是從&#x200B;**開發人員**&#x200B;和&#x200B;**部署管理員**&#x200B;角度編寫的。

系統管理員也可以執行這些相同的任務，但通常這些角色由不同的使用者擔任。

## 目標 {#objective}

本文件是對上線歷程的補充，用於示範在系統管理員讓所有使用者上線並建立必要的雲端資源後開發人員和部署管理員的基本任務。

閱讀本文件後，您應該：

* 作為開發人員，了解如何存取和管理您的 Cloud Manager Git 存放庫。
* 作為部署管理員，能夠在 Cloud Manager 中設定管道並部署您的程式碼。

## 開發人員和部署管理員 {#roles}

系統管理員完成建立使用者和設定雲端資源的主要上線任務後，通常最急於存取系統的使用者是開發人員和部署管理員。這是因為他們是負責在 AEM as a Cloud Service 之上建置您自訂應用程式的使用者。

* **開發者** - 這些使用者存取 Cloud Manager Git 存放庫，他們將在其中管理您的 AEM 自訂應用程式的程式碼。
* **部署管理員** - 這些使用者會使用 Cloud Manager 建立和執行將程式碼從 Git 存放庫部署到您正在執行 AEM 環境的管道。

根據您的組織需求，相同的使用者可以同時具備這兩個角色。

## 必備條件 {#prerequisites}

在您作為開發人員或部署管理員開始本文件中描述的任務之前，請確保您的系統管理員已完成此上線歷程中的所有步驟。這表示：

* 您的系統管理員已將開發人員和部署管理員指派給他們各自的產品設定檔。
* 開發人員必須另外指派到 **AEM 使用者**&#x200B;或 **AEM 管理員**&#x200B;產品設定檔，才能使用 AEM。
* 雲端資源已設定完畢。

## 存取 Git {#accessing-git}

您可以使用 Cloud Manager 中的自助服務 Git 帳戶管理存取和管理您的 Git 存放庫。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從&#x200B;**方案概觀**&#x200B;頁面瀏覽至&#x200B;**管道**&#x200B;卡，尋找&#x200B;**存取存放庫資訊**&#x200B;按鈕，以存取和管理您的 Git 存放庫。

   ![環境卡片上的存取存放庫資訊按鈕](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 按一下「**檢視存放庫資訊**」按鈕來開啟對話框以檢視：

   * Cloud Manager Git 存放庫的 URL。
   * Git 使用者名稱。
   * Git 密碼，其值在按一下&#x200B;**產生密碼**&#x200B;按鈕時顯示。

   ![存放庫資訊](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用這些憑證，使用者可以複製存放庫的本機副本，並在該本機存放庫中進行變更，且在準備好後可以將任何程式碼變更提交回 Cloud Manager 中的遠端程式碼存放庫。

## 管道設定 {#setup-pipeline}

開發人員將他們的自訂程式碼新增到您的 Git 存放庫後，部署管理員可以建立和執行管道以將該程式碼部署到您的 AEM 環境。

按照以下步驟建立您的第一個非生產部署管道。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從 Cloud Manager 首頁畫面存取&#x200B;**管道**&#x200B;卡。按一下「**+新增**」並選取「**新增非生產管道**」。

   ![新增非生產管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在&#x200B;**新增非生產管道**&#x200B;對話框的&#x200B;**設定**&#x200B;索引標籤上，選取您要新增的非生產管道。對於此範例，選擇&#x200B;**部署管道**。

   ![新增非生產管道對話框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 在&#x200B;**非生產管道名稱**&#x200B;以識別您的管道以及以下附加資訊。

1. 在&#x200B;**部署觸發方案**&#x200B;選擇&#x200B;**手動**，以便管道僅在您啟動時執行。

1. 按一下「**繼續**」。

1. 在&#x200B;**新增非生產管道**&#x200B;對話框的&#x200B;**來原始程式碼**&#x200B;索引標籤上，您必須選擇管道應處理的程式碼類型。對於此範例，選擇&#x200B;**完整堆疊程式碼**。

1. 在&#x200B;**原始程式碼**&#x200B;索引標籤上，您必須定義以下選項。

   * **合格的部署環境** - 您必須選擇管道應部署到的環境。
   * **存放庫** - 此選項會定義管道應該從哪個 Git 存放庫擷取程式碼。
   * **Git 分支** - 此選項會定義管道應該選取哪個分支來擷取程式碼。
      * 輸入分支名稱的前幾個字元，該欄位的自動完成功能將會尋找相符的分支以幫助您進行選擇。

   ![完整堆疊管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 按一下「**儲存**」。

您現在已經建立了您的第一個管道！具有部署管理員角色的使用者現在可以從 Cloud Manager UI 啟動管道。

## 部署 {#deploy}

開發人員已經將他們的自訂程式碼新增到 Git 存放庫，且您也建立了管道來部署該程式碼，是時候執行該管道以將該程式碼從 Git 移動到您的環境中了。

![Cloud Manager 中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至「**管道**」卡 (位於「**方案概觀**」頁面)，並按一下您在前一節建立的管道旁邊的省略號按鈕，然後從選單中選取「**執行**」。

1. 此管道執行開始，並由&#x200B;**狀態**&#x200B;欄顯示。

您可以查看執行的詳細資訊，只要再按一下省略符號按鈕，並選取 **檢視詳細資訊**。

恭喜！您現在已將程式碼從 Git 存放庫部署到非生產環境！

## 下一步 {#whats-next}

閱讀本文件後，您應該：

* 作為開發人員，了解如何存取和管理您的 Cloud Manager Git 存放庫。
* 作為部署管理員，能夠在 Cloud Manager 中設定管道並部署您的程式碼。

作為開發人員或部署管理員，您不僅具備 Cloud Manager 的工作知識，還具備工作環境、存放庫和管道的知識！但 AEM as a Cloud Service 的強大 CI/CD 工具還有許多值得深入了解之處。如需更多詳細資訊，請參閱[其他資源](#additional-resources)一節。

如果您對內容作者如何存取和使用 AEM as a Cloud Service 感興趣，請繼續進行上線歷程的最後一部分：[AEM 使用者任務](aem-users.md)。

>[!TIP]
>
>現在您已上線，您可以了解如何以最少的 AEM 設定，[輕鬆將 AEM 參考示範附加元件](/help/journey-sites/demos-add-on/overview.md)新增到沙箱環境，並能夠使用根據最佳實務的豐富範例來測試 AEM 的強大功能。

## 其他資源 {#additional-resources}

如果您想要此上線歷程以外的內容，以下是您可選擇的其他資源。

* [存取存放庫](/help/implementing/cloud-manager/managing-code/accessing-repos.md) - 了解如何使用 Cloud Manager 中的自助服務 Git 帳戶管理存取和管理您的 Git 存放庫。
* [將 Git 與 Cloud Manager 搭配使用](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) - 了解如何使用 Cloud Manager 的 Git 存放庫以及如何將您內部部署客戶管理的 Git 存放庫與 Cloud Manager 整合。
* [本機開發環境設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=zh-Hant) - 本教程將引導您使用 AEM as a Cloud Service SDK 為 Adobe Experience Manager (AEM) 設定本機開發環境。
* [開始使用 AEM Sites - WKND 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant) - 這個多部分教學課程是專為 Adobe Experience Manager 的新手開發人員設計的。此教學課程會逐步引導您實作虛擬生活風格品牌 WKND 的 AEM 網站。此教學課程涵蓋基礎的主題，例如專案設定、核心元件、可編輯的範本、用戶端資料庫以及使用 Adobe Experience Manager Sites 的元件開發。
* [使用 React 在 AEM 中開始使用 SPA](/help/implementing/developing/hybrid/getting-started-react.md) - 本文會介紹一個 SPA 應用程式範例，說明其組合方式，並可讓您使用 React 架構快速啟動並執行您自己的 SPA。
* [使用 Angular 在 AEM 中開始使用 SPA](/help/implementing/developing/hybrid/getting-started-angular.md) - 本文會介紹一個 SPA 應用程式範例，說明其組合方式，並可讓您使用 Angular 架構快速啟動並執行您自己的 SPA。
* [ Headless 開發人員歷程](/help/journey-headless/developer/overview.md) - 開始學習使用 AEM 開發 Headless 應用程式的引導課程。
