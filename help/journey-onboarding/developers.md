---
title: 開發人員和部署管理員任務
description: 系統管理員設定好必要的雲端資源後，即可了解開發人員和部署管理員如何存取git來開發應用程式，並使用管道來部署應用程式。
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 1%

---


# 開發人員和部署管理員任務 {#developer-deployment-manager}

在此選用部分中， [入門旅程，](overview.md) 您將了解開發人員和部署經理如何存取git來開發應用程式，並使用管道來部署應用程式。

## 迄今為止的故事 {#story-so-far}

您在上線過程中已經走了很長的路！ 恭喜！ 系統管理員已完成上線歷程，方法是在檔案中設定必要的雲端資源並授予存取權 [指派AEM產品設定檔。](assign-profiles-aem.md)

此時，您的開發人員和部署經理就可以開始建立自己的應用程式，而AEM的使用者則可以開始建立內容。 從這個意義上講，您的入門已完成，現在是時候使用新的AEMas a Cloud Service系統了，本檔案將說明這一點。

## 對象 {#audience}

因此，本檔案是從 **開發人員** 和 **部署管理員**.

系統管理員也可以執行這些相同的任務，但通常這些角色由不同的用戶擔任。

## 目標 {#objective}

本檔案是上線歷程的補充，說明一旦系統管理員上線所有使用者並建立必要的雲端資源，開發人員和部署管理員的基本工作。

閱讀本檔案後，您應：

* 身為開發人員，了解如何存取及管理您的Cloud Manager Git存放庫。
* 身為部署管理員，您可以在Cloud Manager中設定管道並部署程式碼。

## 開發人員和部署經理 {#roles}

一旦系統管理員完成建立用戶和設定雲資源等入門任務後，通常最渴望訪問系統的用戶就是開發人員和部署經理。 這是因為他們是負責在AEM as a Cloud Service上建立自訂應用程式的使用者。

* **開發人員**  — 這些使用者可存取Cloud Manager Git存放庫，管理AEM自訂應用程式的程式碼。
* **部署管理員**  — 這些使用者可使用Cloud Manager建立並執行管道，將程式碼從Git存放庫部署至執行中的AEM環境。

根據您的組織需求，相同的使用者可以同時具有兩個角色。

## 必備條件 {#prerequisites}

以開發人員或部署管理員身分開始本檔案中所述的工作之前，請確定您的系統管理員已完成本入門歷程中的所有步驟。 這表示：

* 您的系統管理員已將開發人員和部署經理指派給其各自的產品設定檔。
* 開發人員必須另外指派給 **AEM使用者** 或 **AEM管理員** 產品設定檔，以便也使用AEM。
* 雲資源已設定。

## 存取Git {#accessing-git}

您可以使用Cloud Manager的自助Git帳戶管理來存取和管理您的Git存放庫。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **管道** 卡片 **計畫概述** 頁面，並尋找 **存取存放庫資訊** 按鈕來存取和管理您的git存放庫。

   ![「環境」卡上的「存取存放庫資訊」按鈕](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 按一下 **檢視存放庫資訊** 按鈕以開啟要檢視的對話方塊：

   * Cloud Manager Git存放庫的URL。
   * Git使用者名稱。
   * git密碼，其值會在 **生成密碼** 按鈕。

   ![儲存庫資訊](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用這些憑證，使用者可以複製存放庫的本機副本，並在該本機存放庫中進行變更，在準備就緒時，即可將任何程式碼變更提交回Cloud Manager的遠端程式碼存放庫。

## 管道設定 {#setup-pipeline}

開發人員將自訂程式碼新增至您的Git存放庫後，部署管理員就可建立並執行管道，將該程式碼部署至您的AEM環境。

請依照下列步驟，建立您的第一個非生產部署管道。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 存取 **管道** Cloud Manager主畫面中的資訊卡。 按一下 **+添加** 選取 **新增非生產管道**.

   ![新增非生產管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在 **設定** 的 **新增非生產管道** 對話框，選擇要添加的非生產管道類型。 在此範例中，選取 **部署管道**.

   ![新增非生產管道對話方塊](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 提供 **非生產管道名稱** 以識別管道，以及下列其他資訊。

1. 若 **部署觸發程式** 選取 **手動** 這樣管道才會在啟動時運行。

1. 按一下 **繼續**.

1. 在 **原始碼** 的 **新增非生產管道** 對話框中，必須選擇管道應處理的代碼類型。 在此範例中，選取 **完整堆疊程式碼**.

1. 在 **原始碼** 頁簽，必須定義以下選項。

   * **合格的部署環境**  — 必須選擇管道應部署到哪個環境。
   * **存放庫**  — 此選項會定義管道應從哪個Git存放庫擷取程式碼。
   * **Git分支**  — 此選項定義管道中應從哪個分支擷取代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將找到匹配的分支，以幫助您選擇。

   ![全堆疊管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 按一下「**儲存**」。

您現在已建立第一個管道！ 具有部署管理員角色的使用者現在可以從Cloud Manager UI啟動管道。

## 部署 {#deploy}

現在開發人員已將自訂程式碼新增至Git存放庫，且您已建立管道來部署該程式碼，您可以開始執行管道，將程式碼從Git實際移至您的環境。

![Cloud Manager中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **管道** 卡片 **計畫概述** 頁面，然後按一下上一節中建立的管道旁的刪節號按鈕，然後選擇 **執行** 的上界。

1. 管道運行開始，由 **狀態** 欄。

您可以再次按一下省略號按鈕，然後選取 **查看詳細資訊**.

恭喜！ 您現在已將程式碼從Git存放庫部署至非生產環境！

## 下一步 {#whats-next}

現在您已閱讀本檔案，您應：

* 身為開發人員，了解如何存取及管理您的Cloud Manager Git存放庫。
* 身為部署管理員，您可以在Cloud Manager中設定管道並部署程式碼。

您不僅具備Cloud Manager的實用知識，而且具備工作環境、儲存庫和管道，因此，您已成為開發人員或部署經理。 但要了解AEM as a Cloud Service強大的CI/CD工具，還有更多需要了解的。 查看 [其他資源](#additional-resources) 一節以取得詳細資訊。

如果您對內容作者存取和使用AEM as a Cloud Service的方式感興趣，請繼續進行入門歷程的最後一部分， [AEM使用者任務。](aem-users.md)

>[!TIP]
>
>現在您已上線，您可以 [了解如何輕鬆新增AEM參考示範附加元件](/help/journey-sites/demos-add-on/overview.md) 以最少的AEM設定傳至沙箱環境，並能根據最佳實務以豐富的範例來測試AEM的強大功能。

## 其他資源 {#additional-resources}

* [存取儲存庫](/help/implementing/cloud-manager/managing-code/accessing-repos.md)  — 了解如何使用Cloud Manager的自助服務Git帳戶管理來存取及管理您的Git存放庫。
* [搭配Cloud Manager使用Git](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)  — 了解如何使用Cloud Manager的Git存放庫，以及如何將您自己的內部部署客戶管理的Git存放庫與Cloud Manager整合。
* [本地開發環境設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)  — 本教學課程會逐步引導您使用AEMas a Cloud ServiceSDK，為Adobe Experience Manager(AEM)設定本機開發環境。
* [AEM Sites快速入門 — WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)  — 本多部分教學課程是為剛接觸Adobe Experience Manager(AEM)的開發人員所設計。 本教學課程會逐步說明WKND虛構生活風格品牌AEM網站的實作。 本教學課程涵蓋基本主題，例如專案設定、核心元件、可編輯範本、用戶端程式庫，以及使用Adobe Experience Manager Sites開發元件。
* [AEM中使用React的SPA快速入門](/help/implementing/developing/hybrid/getting-started-react.md)  — 本文提供範例SPA應用程式，說明其組合方式，並可讓您使用React架構快速上手並執行自己的SPA。
* [AEM中使用SPA快速入門Angular](/help/implementing/developing/hybrid/getting-started-angular.md)  — 本文提供範例SPA應用程式，說明其組合方式，並可讓您使用Angular架構快速上手並執行自己的SPA。
* [無頭式開發人員歷程](/help/journey-headless/developer/overview.md)  — 從這裡開始，學習使用AEM開發無頭式應用程式的指導課程。
