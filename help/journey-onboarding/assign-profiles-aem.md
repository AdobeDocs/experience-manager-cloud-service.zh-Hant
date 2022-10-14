---
title: 指派 AEM 產品設定檔
description: 設定雲端資源後，您需要使用 AEM 產品設定檔授與您的團隊對 AEM 的存取權。
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 100%

---

# 指派 AEM 產品設定檔 {#assign-profiles-aem}

在[入門歷程](overview.md)的這一部分，您將了解如何使用 AEM 產品設定檔向您的團隊授與對 AEM 的存取權。

## 目標 {#objective}

閱讀此入門歷程[建立環境](create-environments.md)中的上一個文件並設定雲端資源後，您將需要使用 AEM 產品設定檔授與您的團隊對 AEM 的存取權。作為系統管理員，您可以透過指派 AEM 產品設定檔來執行此操作。

閱讀本文件後，您應會了解：

* 什麼是 AEM 產品設定檔。
* 如何將團隊成員新增到 AEM 使用者產品設定檔。
* 如何將團隊成員新增到 AEM 管理員產品設定檔。

## AEM 產品設定檔 {#aem-product-profiles}

若要使用 AEM，您的團隊成員必須獲指派至少一個 AEM 產品設定檔。存取 Cloud Manager 的權限是不夠的。使用者必須屬於以下兩個產品設定檔之一：

* `AEM Users` - 該群組包括執行日常內容製作任務的一般使用者。
* `AEM Administrators` - 該群組包括負責進階功能或 AEM 的使用者。

指派給 AEM 產品設定檔的每個使用者也將取得對 Cloud Manager 的唯讀存取權。可以透過其他產品設定檔授與對 Cloud Manager 的寫入權限。

## 必備條件 {#prerequisites}

在開始閱讀本節之前，您應該具備以下將使用 AEM 之團隊的資訊。

* 名稱
* 電子郵件地址
* 角色和責任

>[!TIP]
>
>出於入門目的，建議您先新增將參與即時任務的使用者，例如管理員、開發人員和內容作者。您可以在不新增所有使用者的情況下繼續其他的入門流程。完成入門後，稍後您可以擴展到更多使用者。

## 檢視 AEM 產品設定檔 {#view-profiles}

按照以下步驟從 Admin Console 查看 AEM 產品設定檔。

1. 請上 [`https://adminconsole.adobe.com` 登入 Admin Console。](https://adminconsole.adobe.com)

1. 在&#x200B;**總覽**&#x200B;頁面，從&#x200B;**產品和服務**&#x200B;卡選取 **Adobe Experience Manager as a Cloud Service**。

   ![產品和服務卡](/help/journey-onboarding/assets/assign-team1.png)

1. 瀏覽並選擇執行個體。

   選取「![選取執行個體](/help/journey-onboarding/assets/cloud-profiles-1.png)。

1. 您將看到 AEM as a Cloud Service 產品設定檔清單，這些設定檔可以根據使用者的角色指派給使用者。

   ![產品設定檔](/help/journey-onboarding/assets/cloud-profiles-2.png)

## 將團隊成員新增至產品設定檔 {#add-team-members}

現在您已經熟悉了可用的設定檔，您可以根據需要將它們指派給您的團隊成員。

這些工作要求您是擁有&#x200B;**業務負責人** Cloud Manager 產品設定檔的系統管理員。

1. 從 Cloud Manager 瀏覽到您的計劃，然後從感興趣的環境內容中選取&#x200B;**管理存取權**&#x200B;按鈕。

   ![管理存取權](/help/journey-onboarding/assets/add-team1.png)

1. 會有新索引標籤將您引導至 Admin Console，您可以在其中存取環境的作者執行個體。根據需要授與此人的權限選擇 **AEM 管理員**&#x200B;或 **AEM 使用者**。

   ![指派存取權](/help/journey-onboarding/assets/add-team2.png)

1. 選擇 `AEM Administrator` 或 `AEM User`，然後如下所示按一下&#x200B;**新增使用者**，並提交必要的詳細資訊以完成新增團隊成員。

   ![新增團隊成員](/help/journey-onboarding/assets/add-team3.png)

1. 如果您擁有需要存取權之團隊成員的資訊，請對包括開發、測試和生產在內的所有環境重複這些步驟。

您新增的使用者現在可以存取 AEM as a Cloud Service 作者服務！

## 歷程結尾？ {#the-end}

恭喜！您指派給 AEM as a Cloud Service 產品設定檔的使用者現在可以存取 AEM 製作環境，並開始使用 AEM as a Cloud Service 建立內容。同樣，開發人員現在可以存取 Cloud Manager 以使用 Git 儲存自訂應用計劃計劃碼並進行部署。從這個角度來看，您的入門歷程已經完成，您的使用者現在可以使用 AEMaaCS。

但是，如果您想更了解作者和開發人員如何使用該系統，您可以選擇繼續此入門歷程的兩個部分：

* [開發人員和部署管理員任務](developers.md) - 您將了解開發人員如何存取 Git 以儲存他們的自訂計劃碼，並使用 Cloud Manager 管道進行部署。
* [AEM 使用者任務](aem-users.md) - 您將在其中學習如何存取可以開始建立內容的 AEM 環境。

## 其他資源 {#additional-resources}

* [在 Admin Console 中管理產品和使用者存取權](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) - 了解如何使用 Admin Console 來管理使用存取權。
* [設定 AEM 存取權逐步說明](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=zh-Hant) - 查看這個簡短的逐步說明，了解如何在 Admin Console 中設定 Adobe IMS 使用者、使用者群組和產品設定檔。

