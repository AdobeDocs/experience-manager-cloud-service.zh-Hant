---
title: 為Cloud Manager產品配置檔案分配團隊成員
description: 按照此頁瞭解如何將團隊成員分配給Cloud Manager產品配置檔案
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 0%

---


# 將團隊成員分配給Cloud Manager產品配置檔案 {#assign-team-members}

在 [登機之旅，](overview.md) 您將學習如何將團隊成員分配給Cloud Manager產品配置檔案。

## 目標 {#objective}

在前一步， [訪問Admin Console,](admin-console.md) 您現在已學會登錄到Admin Console並以系統管理員身份驗證您的權限。 您現在已準備好允許團隊成員訪問雲管理器。 通過分配產品配置檔案來執行此操作。

在授予用戶對Adobe解決方案的訪問權限時，您不一定希望授予他們完全訪問權限。 產品配置檔案使每個解決方案都擁有自己的一組用戶權限。 您可以使用Admin Console來分配產品配置檔案。

第一步是授予用戶對雲管理器的訪問權限。 雲管理器通過企業開發設定及其專門構建的CI/CD管道為您提供支援，這些管道旨在確保徹底的測試和最高的代碼質量，以提供卓越的體驗。

閱讀此文檔後，您應：

* 瞭解產品配置檔案。
* 瞭解雲管理器是什麼。
* 瞭解三個重要的Cloud Manager產品配置檔案： **業務所有者**。 **部署管理器**, **開發人員**。
* 能夠將團隊成員分配給Cloud Manager產品配置檔案。

## 必備條件 {#prerequisites}

要將團隊成員分配給產品配置檔案，您需要瞭解有關團隊成員的詳細資訊，這些成員需要訪問AEMas a Cloud Service，包括：

* 名稱
* 電子郵件地址
* 角色和職責

>[!TIP]
>
>為了加入，Adobe建議您首先添加將參與即時任務的用戶，如管理員、開發人員和內容作者。
>
>您可以繼續登機過程，而不添加所有用戶。 完成登錄後，可以添加其他用戶。

## 產品配置檔案 {#product-profiles}

在授予用戶對Adobe解決方案的訪問權限時，您不一定希望授予他們完全訪問權限。 產品配置檔案使每個解決方案都具有自己的一組用戶權限，這些權限是使用Admin Console設定的。

例如，在此路程的稍後部分，您將使用該Admin Console為管理員和作者分配AEM產品配置檔案，以授予用戶對解決AEM方案的訪AEM問權。

但下一步是授予產品配置檔案，以便您的團隊成員首先可以訪問雲管理器。

## Cloud Manager {#cloud-manager}

作為系統管理員，您知AEM道成功的as a Cloud Service項目不僅取決於使用建立驚人內容AEM，還取決於開發和部署您自己的自定義代碼和應用程式以交付您AEM的內容。

Cloud Manager是as a Cloud Service的一個組成部AEM分，用於管理CI/CD管道以進行代碼部署、管理代碼儲存庫和管理環境。

在您的團隊可以執行其他操作之前，必須通過向他們授予必要的產品配置檔案，將他們加入雲管理器。 接下來的步驟將向您顯示如何使用Admin Console查找Cloud Manager產品配置檔案以及如何將它們分配給您的團隊成員。

## 查看Cloud Manager產品配置檔案 {#review-product-profiles}

使用Admin Console，您可以看到Cloud Manager配置檔案的清單。

1. 登錄Adobe Admin Console，時間： [adminconsole.adobe.com](https://adminconsole.adobe.com/) 和 **概述** ，選擇 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡。

   ![AEM作為產品](/help/journey-onboarding/assets/assign-team1.png)

1. 導航到 **雲管理器** 實例。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 您將看到預配置的Cloud Manager產品配置檔案的清單。

   ![產品配置檔案](/help/journey-onboarding/assets/assign-team3.png)

在初始登機過程中要分配的最重要配置檔案包括：

* **業務所有者**  — 這些用戶管理不同的程式。
* **部署管理器**  — 這些用戶將代碼從您的儲存庫部署到運行AEM環境。
* **開發人員**  — 這些用戶開發您的自AEM定義應用程式並將代碼提交到儲存庫。

瞭解這些角色是什麼以及它們所做的，請查看您的團隊成員清單以確定誰需要哪個配置檔案。 請記住，用戶在您的團隊中可能有多個角色，並且通常有多個角色，因此也需要多個配置檔案。

## 分配業務所有者產品配置檔案 {#assign-business-owner}

您現在已準備好添加用戶並將其分配給 **業務所有者** 產品配置檔案。

1. 確定需要管理Cloud Manager程式的用戶。 這些將是 **企業所有者**。

1. 登錄到Admin Console，位於 `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 在 **概述** ，選擇 **Adobe Experience Manager as a Cloud Service** 產品 **產品和服務** 卡。

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

您 **業務所有者**&#x200B;已分配，現在可以訪問雲管理器。 不要忘記還將您作為系統管理員分配給 **業務所有者** 檔案。

## 分配部署管理器產品配置檔案 {#assign-deployment-manager}

1. 確定需要部署代碼的用戶。

1. 登錄到Admin Console，位於 `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 在 **概述** 頁面選擇 **Adobe Experience Manager as a Cloud Service** 產品 **產品和服務** 卡。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 選擇 **用戶** 頁籤，然後選擇 **添加用戶**。

   ![添加用戶](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **將用戶添加到團隊** 對話框，輸入要添加的用戶的電子郵件ID。

   * 如果尚未設定團隊成員的聯合ID，請選擇 **Adobe ID** 為 **ID類型**。

   ![輸入ID](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下「 **選擇產品或用戶組** 標題開始產品選擇並選擇 **Adobe Experience Manager as a Cloud Service** 分配 **部署管理器** 產品配置檔案。

   ![分配配置檔案](/help/journey-onboarding/assets/assign-team6.png)

您 **部署管理器**&#x200B;已分配，現在可以訪問雲管理器。 根據您將來的職責，您可能也不需要將您作為系統管理員分配給 **部署管理器** 檔案。

## 分配開發人員產品配置檔案 {#assign-developer}

1. 確定需要開發應用程式和管理代AEM碼的用戶。

1. 登錄到Admin Console，位於 `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 在 **概述** 頁面選擇 **Adobe Experience Manager as a Cloud Service** 產品 **產品和服務** 卡。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 選擇 **用戶** 頁籤，然後選擇 **添加用戶**。

   ![添加用戶](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **將用戶添加到團隊** 對話框，輸入要添加的用戶的電子郵件ID。

   * 如果尚未設定團隊成員的聯合ID，請選擇 **Adobe ID** 為 **ID類型**。

   ![添加用戶ID](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下「 **選擇產品或用戶組** 標題開始產品選擇並選擇 **Adobe Experience Manager as a Cloud Service** 分配 **開發人員** 產品配置檔案。

   ![分配配置檔案](/help/journey-onboarding/assets/assign-team6.png)。

您 **開發人員**&#x200B;已分配，現在可以訪問雲管理器。 根據您將來的職責，您可能也不需要將您作為系統管理員分配給 **開發人員** 檔案。

## 下一步是什麼 {#whats-next}

恭喜！ 您新組建的雲管理器團隊(包括您已分配給 **業務所有者** 配置檔案)已設定。 在角色中 **業務所有者**&#x200B;現在，您只需一步即可登錄到Cloud Manager並啟用雲資源的建立。

在登機過程的這一部分，您學習了如何將團隊成員分配給Admin Console中的配置檔案。 您現在應該：

* 瞭解產品配置檔案。
* 瞭解雲管理器是什麼。
* 瞭解三個重要的Cloud Manager產品配置檔案： **業務所有者**。 **部署管理器**, **開發人員**。
* 能夠將團隊成員分配給Cloud Manager產品配置檔案。

現在，您已準備好通過下一步查看文檔繼續登機之旅 [訪問雲管理器，](cloud-manager.md) 您將在其中學習如何訪問雲管理器並建立項目資源。

## 其他資源 {#additional-resources}

建議繼續按前所述進行登機旅程。 如果您希望從此旅程中對特定主題進行深入探討，則這些是一些額外資源。

* [Cloud Manager簡介](/help/onboarding/cloud-manager-introduction.md)  — 瞭解Cloud Manager、Cloud Manager程式和環境。
* [Cloud Manager產品配置檔案](/help/onboarding/aem-cs-team-product-profiles.md)  — 瞭解AEMas a Cloud Service團隊和產品配置檔案。
* [Adobe Admin Console上的身份類型](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html) -Adobe的身份管理系統可幫助管理員建立和管理用戶對應用程式和服務的訪問。 Adobe提供這些身份類型或帳戶來驗證和授權用戶。

