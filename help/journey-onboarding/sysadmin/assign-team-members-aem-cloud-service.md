---
title: 將團隊成員分配AEM給as a Cloud Service產品配置檔案
description: 按照本頁瞭解如何將團隊成員分配到AEMas a Cloud Service產品配置檔案
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 2%

---

# 將團隊成員分配AEM給as a Cloud Service產品配置檔案 {#assign-team-members-cloud-service}

## 目標 {#objective}

本文檔幫助您瞭解系統管理員為將團隊成員分配到AEMas a Cloud Service產品配置檔案而必須採取的步驟，以及為什麼使您的AEM作者能夠踏上其旅程至關重要AEM。

讀完本節後，您應瞭解：

* 為什麼以及如何將團隊成員分配給AEMas a Cloud Service產品配置檔案。
* 如何將團隊成員添加AEM到用戶產品配置檔案。
* 如何將團隊成員添加AEM到Administrators產品配置檔案。


## 簡介 {#introduction}

要授予對as a Cloud Service用AEM戶的訪問權限，必須屬於以下兩種產品配置檔案之一：  `AEM Users` 或 `AEM Administrators`。 您的團隊成員必須被授予對實AEM例的權限，因為管理雲管理器的權限不夠。

>[!NOTE]
>系統管理員分AEM配給用戶產品配置檔案的每個用戶都將擁有（只讀）Cloud Manager訪問權限。

## 先決條件 {#prerequisites}

在開始閱讀本節之前，您應考慮以下先決條件：

* 瞭解 [AEMas a Cloud Service產品配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* 熟悉 [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* 已將Cloud Manager產品配置檔案分配給您的團隊成員，並且已設定雲資源
* 有關團隊成員的詳細資訊：系統管理員必須具有需要訪問as a Cloud Service的團隊成員的姓名和電子郵件地址以及角色和AEM職責。

   >[!NOTE]
   >為了加入，我們建議您首先添加將參與立即任務的用戶，如管理員、開發人員和內容作者。 您可以繼續其餘的登錄，而不添加所有用戶。 完成登錄後，您可以稍後擴展到更多用戶。


   >[!IMPORTANT]
   >在開始複查將團隊成員分配給AEMas a Cloud Service產品配置檔案的步驟之前，請確保執行以下兩個步驟：
   >
   >1. 登錄到 [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)。 有關詳細資訊，請參閱登錄到Admin Console。
   >
   >1. 審閱 [AEMas a Cloud Service產品配置檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)。


按照以下步驟查看Adobe Admin Console的Cloud Manager配置檔案清單：

1. 登錄到 [Adobe Admin Console](https://adminconsole.adobe.com/)。 從 **概述** ，選擇 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡。

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. 導航並選擇實例（開發環境的作者實例），如下圖所示。

   ![](/help/journey-onboarding/assets/cloud-profiles-1.png)


1. 您將看到根據用AEM戶角色需要分配給用戶的as a Cloud Service產品配置檔案清單。

   >[!NOTE]
   >要瞭解有關這些內容的詳細資訊，請參閱 [AEMas a Cloud Service產品配置檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)。

   ![](/help/journey-onboarding/assets/cloud-profiles-2.png)


## 將團隊成員添加AEM到用戶或AEM管理員產品配置檔案 {#add-team-members}

要授予對as a Cloud Service實AEM例用戶的訪問權限，用戶必須屬於兩個產品配置檔案之一 `AEM Users` 或 `AEM Administrators`。

>[!NOTE]
>您必須被授予該實例的權限，管理雲管理器的權限不足。 了解更多.

以下步驟必須由同時具有業務所有者角色的系統管理員執行。

1. 從Cloud Manager導航到您的程式，然後選擇 **管理訪問** 按鈕。

   ![](/help/journey-onboarding/assets/add-team1.png)

1. 新頁籤可將您導航到Adobe Admin Console，從那裡您可以訪問環境的作者實例。 選擇 **管AEM理員** 或 **用AEM戶** 根據此個人需要授予的權限。 瞭解有關 [AEMas a Cloud Service產品配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)。

   ![](/help/journey-onboarding/assets/add-team2.png)

1. 選擇 `AEM Administrator` 或 `AEM User` 按一下 **添加用戶** 如下所示，並提交完成添加團隊成員所需的詳細資訊。

   ![](/help/journey-onboarding/assets/add-team3.png)

   您添加的用戶現在可以訪問AEMas a Cloud Service作者服務！

   >[!NOTE]
   >如果您有需要訪問的團隊成員的資訊，您將希望對所有環境（包括開發、階段和生產）重複這些步驟。


## 下一步是什麼 {#whats-next}

您分配給AEMas a Cloud Service產品配置檔案的用戶現在可以學習如何訪問「作者」並熟悉as a Cloud Service中的創作AEM頁面。 您應遵循該路徑，接下來查看文檔學習路徑 [用AEM戶](/help/journey-onboarding/sysadmin/learning-path-aem-users.md) 或 [開發人員和部署經理](/help/journey-onboarding/sysadmin/learning-path-developers-deploymentmanagers.md)。

## 其他資源 {#additional-resources}

* [在 Admin Console 中管理產品和使用者存取權限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)
* [配置訪問權AEM限](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [製作頁面的快速入門手冊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)
