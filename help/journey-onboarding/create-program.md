---
title: 建立程序
description: 了解如何使用 Cloud Manager 來建立您的首個程序。
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: 971ef47b66da6d7e032f6109afb4830d49c00071
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 96%

---

# 建立程序 {#create-program}

在[到職歷程](overview.md)的這一部分，您將學習如何使用 Cloud Manager 建立您的第一個程序。

## 目標 {#objective}

在查看了此上線過程中的上一個文件後，[ Access 雲管理器，](cloud-manager.md)您已確保您擁有對 Cloud Manager 的適當存取權限。現在您可以建立您的第一個程序。

閱讀本文件後，您將了解：

* 了解什麼是程序。
* 了解生產程序和沙箱程序之間的區別。
* 能夠建立自己的程序。

## 了解什麼是程序？ {#programs}

程序是 Cloud Manager 中最高級別的組織。根據您的 Adobe 授權，程序允許您組織您的解決方案並授予特定團隊成員對這些程序的存取權限。

Cloud Manager 程序代表一組 Cloud Manager 環境。這些程序支援業務程序的邏輯集，通常對應於許可的服務水平協議 (SLA)。例如，一個程序可能代表 AEM 資源以支援組織的全球公共網站，而另一個程序代表內部的中央 DAM。

如果您回想一下理論上的 WKND Travel and Adventure Enterprises 的範例，他們是一家專注於旅遊相關媒體的租使用者，他們可能有兩個程序：一個用於 WKND 雜誌部門的 Assets 程序和一個用於 WKND 媒體部門的 Assets 程序。由於他們自己的分工要求，不同的團隊成員將可以存取不同的程序。

有兩種不同類型的程序：

* **生產程序**&#x200B;是為啟用網站的即時流量而建立的。這是您的「真實」環境。
* **沙箱程序**&#x200B;通常建立的目的是提供培訓、執行示範、培訓、POC 或文件。

由於它們服務於不同的目的，不同的環境有不同的選擇。但是建立它們的過程是相似的。對於此入門之旅，我們將建立一個沙箱環境。

>[!TIP]
>
>如果您需要建立生產程式，請參閱 [其他資源](#additional-resources) 一節，以取得詳細說明方案的檔案連結。

## 建立沙箱程序 {#create-sandbox}

請依照以下步驟建立沙箱程序。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 從 Cloud Manager 的登入頁面單擊&#x200B;**新增程序**&#x200B;在畫面的右上角。

   ![Cloud Manager 登陸頁面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. 從建立程序嚮導中，選擇&#x200B;**設定沙箱**，提供程序名稱，然後單擊&#x200B;**創造**.

   ![程序類型建立](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

隨著設定過程的進行，您將在登入頁面上看到一個帶有狀態指示器的新沙箱程序卡。

![從概覽頁面建立沙箱](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

程序完成後，您組織的成員將指派到&#x200B;**開發商** product profile 可以登入 Cloud Manager 管理 Cloud Manager 的 git 倉庫。

## 下一步 {#whats-next}

現在您的第一個程序已建立，您可以為其建立環境。您應該透過下一次查看文件來繼續您的上線之旅[建立環境。](create-environments.md)

## 其他資源 {#additional-resources}

按照其他資源了解：

* [程序和程序類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) - 了解 Cloud Manager 的階層以及不同類型的程序如何適應其結構以及它們之間的差異。
* [建立沙箱程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) - 了解如何使用 Cloud Manager 建立您自己的沙箱程序，用於培訓、演示、POC 或其他非生產目的。
* [建立生產程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)- 了解如何使用 Cloud Manager 建立您自己的生產程序來託管實時流量。
* [使用 Adobe Cloud Manager - 程序](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=zh-Hant) - Cloud Manager 程序代表支援邏輯業務程序集合的 AEM 環境集合，通常會對應到已購買的服務等級協定 (SLA)。
* [AEM as a Cloud Service 團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md) - 了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。
