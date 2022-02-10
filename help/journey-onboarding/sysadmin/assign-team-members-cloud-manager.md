---
title: 為Cloud Manager產品配置檔案分配團隊成員
description: 按照此頁瞭解如何將團隊成員分配給Cloud Manager產品配置檔案
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---

# 將團隊成員分配給Cloud Manager產品配置檔案 {#assign-team-members}

在前一步， [入門流程](/help/journey-onboarding/sysadmin/get-started-onboarding-journey.md)，您現在已學會登錄到Admin Console並以系統管理員身份查看您的權限。 您現在已準備好將團隊成員分配給Cloud Manager產品配置檔案。

## 目標 {#objective}

本文檔總結了如何從Adobe Admin Console向Cloud Manager產品配置檔案分配團隊成員。 分配後，這些成員就可以建立訪問雲資源，如此路程的下一步所述。

閱讀此部分後，您應能夠：

* 瞭解您必須添加團隊成員的原因和方式。
* 瞭解三個重要的Cloud Manager產品配置檔案： **業務所有者**。 **部署管理器**, **開發人員**。
* 將團隊成員分配給Cloud Manager產品配置檔案。

>[!TIP]
>
>為了加入，Adobe建議您首先添加將參與立即任務的用戶，如管理員、開發人員和內容作者。 您可以繼續登機過程，而不添加所有用戶。 完成登錄後，可以添加其他用戶。

## 必備條件 {#prerequisites}

在開始本節之前，應滿足以下先決條件。 您必須：

* 成為系統管理員並瞭解Cloud Manager產品配置檔案。
   * 返回到 [登機旅程概述](onboarding-journey-overview.md) 如果你不熟悉這些概念。
* 瞭解Adobe Admin Console的基本知識。
   * 返回到 [登機旅程概述](onboarding-journey-overview.md) 如果你不熟悉這些概念。
* 瞭解有關團隊成員的詳細資訊，這些成員需要訪問AEMas a Cloud Service，包括
   * 名稱
   * 電子郵件地址
   * 角色和職責

## 查看Cloud Manager產品配置檔案 {#review-product-profiles}

從Adobe Admin Console，您可以看到Cloud Manager配置檔案的清單。

1. 登錄Adobe Admin Console，時間： [adminconsole.adobe.com](https://adminconsole.adobe.com/) 和 **概述** ，選擇 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡。

   ![AEM作為產品](/help/journey-onboarding/assets/assign-team1.png)

1. 導航到 **雲管理器** 實例。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 您將看到預配置的Cloud Manager產品配置檔案的清單。

   ![產品配置檔案](/help/journey-onboarding/assets/assign-team3.png)

## 將用戶分配給業務所有者產品配置檔案 {#assign-users-business-owner}

您現在已準備好添加用戶並將其分配給 **業務所有者** 產品配置檔案。

1. 確定將管理Cloud Manager程式並將它們添加到業務所有者產品配置檔案的用戶。

1. 登錄到Admin Console，位於 [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) 在 **概述** ，選擇 **Adobe Experience Manager as a Cloud Service** 產品 **產品和服務** 卡。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 選擇 **用戶** 頁籤，然後選擇 **添加用戶**。

   ![添加用戶](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **將用戶添加到團隊** 對話框，輸入要添加的用戶的電子郵件ID。

   * 如果尚未設定團隊成員的聯合ID，請選擇 **Adobe ID** 為 **ID類型**。

   ![添加用戶詳細資訊](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下「 **選擇產品或用戶組** 標題開始產品選擇並選擇 **Adobe Experience Manager as a Cloud Service** 分配 **業務所有者** 產品配置檔案。

   * 將每個用戶分配至少一個產品配置檔案，以便用戶可以訪問雲管理器。
   * 切記將您作為系統管理員分配給 **業務所有者** 角色。

   ![分配用戶](/help/journey-onboarding/assets/assign-team6.png)

1. 按一下 **保存** 並向您添加的用戶發送歡迎電子郵件。 受邀用戶可以通過按一下歡迎電子郵件中的連結並使用其Adobe ID登錄來訪問雲管理器。

1. 對團隊中的用戶重複這些步驟。

您新組建的雲管理器團隊(包括您已分配給 **業務所有者** 角色)。 在角色中 **業務所有者**&#x200B;現在，您只需一步即可登錄到Cloud Manager並啟用雲資源的建立。

## 將用戶分配給Deployment Manager產品配置檔案 {#assign-users-deployment-manager}

1. 確定將管理Cloud Manager程式並將它們添加到部署管理器產品配置檔案的用戶。

1. 登錄到Admin Console，位於 [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) 在 **概述** 頁面選擇 **Adobe Experience Manager as a Cloud Service** 產品 **產品和服務** 卡。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 選擇 **用戶** 頁籤，然後選擇 **添加用戶**。

   ![添加用戶](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **將用戶添加到團隊** 對話框，輸入要添加的用戶的電子郵件ID。

   * 如果尚未設定團隊成員的聯合ID，請選擇 **Adobe ID** 為 **ID類型**。

   ![輸入ID](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下「 **選擇產品或用戶組** 標題開始產品選擇並選擇 **Adobe Experience Manager as a Cloud Service** 分配 **部署管理器** 產品配置檔案。

   ![分配配置檔案](/help/journey-onboarding/assets/assign-team6.png)。

## 將用戶分配給開發人員產品配置檔案 {#assign-users-developer}

1. 確定將管理Cloud Manager程式的用戶。

1. 登錄到Admin Console，位於 [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) 在 **概述** 頁面選擇 **Adobe Experience Manager as a Cloud Service** 產品 **產品和服務** 卡。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 選擇 **用戶** 頁籤，然後選擇 **添加用戶**。

   ![添加用戶](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **將用戶添加到團隊** 對話框，輸入要添加的用戶的電子郵件ID。

   * 如果尚未設定團隊成員的聯合ID，請選擇 **Adobe ID** 為 **ID類型**。

   ![添加用戶ID](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下「 **選擇產品或用戶組** 標題開始產品選擇並選擇 **Adobe Experience Manager as a Cloud Service** 分配 **開發人員** 產品配置檔案。

   ![分配配置檔案](/help/journey-onboarding/assets/assign-team6.png)。

## 下一步是什麼 {#whats-next}

在入職過程的這一部分，您學習了有關將團隊成員分配給Admin Console中角色的全部內容。 您現在應該：

* 瞭解您必須添加團隊成員的原因和方式。
* 瞭解三個重要的Cloud Manager產品配置檔案： **業務所有者**。 **部署管理器**, **開發人員**。
* 能夠將團隊成員分配給Cloud Manager產品配置檔案。

現在，您已準備好通過下一步查看文檔繼續登機之旅 [通過雲管理器設定雲資源](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md)，您可以在其中學習：

1. 對於其他業務所有者建立程式，您是分配給 **業務所有者** 角色，必須首先訪問並登錄雲管理器。
1. 用戶與 **業務所有者** 角色可以登錄和設定雲資源，包括雲計畫和環境。
1. 用戶與 **開發人員** 和 **部署管理器** 角色可以訪問雲管理器。

## 其他資源 {#additional-resources}

建議繼續按前所述進行登機旅程。 如果您希望從此旅程中對特定主題進行深入探討，則這些是一些額外資源。

* [雲管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Cloud Manager產品配置檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Admin Console身份概述](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
