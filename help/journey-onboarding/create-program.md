---
title: 建立計畫
description: 了解如何使用 Cloud Manager 來建立您的第一個計畫。
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: b916bf5b252045120659600293e004fc34b96e7a
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 87%

---

# 建立計畫 {#create-program}

在[到職歷程](overview.md)的這一部分，您將學習如何使用 Cloud Manager 建立您的第一個計畫。

## 目標 {#objective}

在查看了此上線過程中的上一個文件後，[ Access 雲管理器，](cloud-manager.md)您已確保您擁有對 Cloud Manager 的適當存取權限。現在您可以建立您的第一個計畫。

閱讀本文件後，您將了解：

* 了解什麼是計畫。
* 了解生產計畫和沙箱計畫之間的區別。
* 能夠建立自己的計畫。

## 了解什麼是計畫？ {#programs}

計畫是 Cloud Manager 中最高級別的組織。根據您的 Adobe 授權，計畫允許您組織您的解決方案並授予特定團隊成員對這些計畫的存取權限。

Cloud Manager 計畫代表一組 Cloud Manager 環境。這些計畫支援業務倡議的邏輯集，通常對應於許可的服務水平協議 (SLA)。例如，一個計畫可能代表 AEM 資源以支援組織的全球公共網站，而另一個計畫代表內部的中央 DAM。

如果您回想一下理論上的 WKND Travel and Adventure Enterprises 的範例，他們是一家專注於旅遊相關媒體的租使用者，他們可能有兩個計畫：一個用於 WKND 雜誌部門的 Assets 計畫和一個用於 WKND 媒體部門的 Assets 計畫。由於他們自己的分工要求，不同的團隊成員將可以存取不同的計畫。

有兩種不同類型的計畫：

* **生產計畫**&#x200B;是為啟用網站的即時流量而建立的。這是您的「真實」環境。
* **沙箱計畫**&#x200B;通常建立的目的是提供培訓、執行示範、培訓、POC 或文件。

由於它們服務於不同的目的，不同的環境有不同的選擇。但是建立它們的過程是相似的。對於此入門之旅，我們將建立一個沙箱環境。

>[!TIP]
>
>如果您需要建立生產計畫，請參閱[其他資源](#additional-resources)一節，以取得詳細描述計畫的文件連結。

## 建立沙箱計畫 {#create-sandbox}

請依照以下步驟建立沙箱計畫。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 從 Cloud Manager 的登陸頁面，按一下畫面的右上角的&#x200B;**新增計畫**。

   ![Cloud Manager 登陸頁面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/cloud-manager-my-programs.png)

1. 在建立程式嚮導中，選擇 **設定沙盒** 並提供程式名稱，點擊或按一下 **繼續**。

   ![程序類型建立](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

1. 在 **設定沙盒** 對話框，您可以選擇要在沙盒程式中啟用的解決方案。 的 **站點** 和 **資產** 解決方案始終包含在沙盒程式中，並自動選擇。 這就足以供我們舉例。 按一下&#x200B;**建立**。

   ![解決方案選擇](assets/set-up-sandbox-onboarding.png)

隨著設定過程的進行，您將在登入頁面上看到一個帶有狀態指示器的新沙箱程序卡。

![從概覽頁面建立沙箱](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

程序完成後，您組織的成員將指派到&#x200B;**開發商** product profile 可以登入 Cloud Manager 管理 Cloud Manager 的 git 倉庫。

## 下一步 {#whats-next}

現在您的第一個程序已建立，您可以為其建立環境。您應該透過下一次查看文件來繼續您的上線之旅[建立環境。](create-environments.md)

## 其他資源 {#additional-resources}

如果您想超越登機旅程的內容，請選擇以下附加資源。

* [程序和程序類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) - 了解 Cloud Manager 的階層以及不同類型的程序如何適應其結構以及它們之間的差異。
* [建立沙箱程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) - 了解如何使用 Cloud Manager 建立您自己的沙箱程序，用於培訓、演示、POC 或其他非生產目的。
* [建立生產程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)- 了解如何使用 Cloud Manager 建立您自己的生產程序來託管實時流量。
* [使用 Adobe Cloud Manager - 程序](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) - Cloud Manager 程序代表支援邏輯業務程序集合的 AEM 環境集合，通常會對應到已購買的服務等級協定 (SLA)。
* [AEM as a Cloud Service 團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md) - 了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。
