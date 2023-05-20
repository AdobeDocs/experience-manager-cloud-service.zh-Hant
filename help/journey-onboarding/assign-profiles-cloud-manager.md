---
title: 將團隊成員指派給 Cloud Manager 產品設定檔
description: 按照此頁面了解如何將團隊成員指派給 Cloud Manager 產品設定檔
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 100%

---


# 將團隊成員指派給 Cloud Manager 產品設定檔 {#assign-team-members}

在[入門歷程](overview.md)的這一部分，您將了解如何將團隊成員指派給 Cloud Manager 產品設定檔

## 目標 {#objective}

在此歷程的上一步[存取 Admin Console](admin-console.md)中，您已學習了登入 Admin Console 並驗證您作為系統管理員的權限。現在您已準備好允許您的團隊成員存取 Cloud Manager。您可以透過指派產品設定檔來執行此操作。

在授與使用者 Adobe 解決方案的存取權時，您不一定要授與他們完整的存取權。產品設定檔使每個解決方案都可以擁有自己的一組使用者權限。您可以使用 Admin Console 指派產品設定檔。

您的第一步是授與使用者存取 Cloud Manager 的權限。雲端管理員可透過企業開發設定及其專門建置的 CI/CD 管道為您提供支援，這些管道可確保全面測試和最高的計劃碼品質，從而提供卓越的體驗。

閱讀本文件後，您應該：

* 了解什麼是產品設定檔。
* 了解什麼是 Cloud Manager。
* 了解三個重要的 Cloud Manager 產品設定檔：**業務負責人**、**部署管理員**&#x200B;和&#x200B;**開發人員**。
* 能夠將團隊成員指派給 Cloud Manager 產品設定檔。

## 必備條件 {#prerequisites}

要將團隊成員指派給產品設定檔，您需要那些要存取 AEM as a Cloud Service 的團隊成員的詳細資訊，包括：

* 名稱
* 電子郵件地址
* 角色和責任

>[!TIP]
>
>出於入門目的，Adobe 建議您先新增將參與即時任務的使用者，例如管理員、開發人員和內容作者。
>
>您可以在不新增所有使用者的情況下繼續入門流程。完成入門後，您可以新增其他使用者。

## 產品設定檔 {#product-profiles}

在授與使用者 Adobe 解決方案的存取權時，您不一定要授與他們完整的存取權。產品設定檔可讓每個解決方案都可擁有自己的一組使用者權限，這些權限是使用 Admin Console 設定的。

例如，在此歷程的後期，您將使用 Admin Console 透過為 AEM 管理員和 AEM 作者指派產品設定檔來授與使用者對 AEM 解決方案的存取權。

但是，下一步是授與產品設定檔，以便您的團隊成員可以先存取 Cloud Manager。

## Cloud Manager {#cloud-manager}

作為系統管理員，您知道成功的 AEM as a Cloud Service 專案不僅取決於使用 AEM 建立令人驚嘆的內容，還取決於開發和部署您自己的自訂計劃碼和應用計劃以傳達您的 AEM 內容。

Cloud Manager 是 AEM as a Cloud Service 不可或缺的一部分，用於管理 CI/CD 管道以進行計劃碼部署、管理計劃碼存放庫和管理環境。

您必須授與您的團隊成員必要的產品設定檔來讓他們加入 Cloud Manager，然後他們才可以進行下一步。接下來的步驟將說明如何使用 Admin Console 找到 Cloud Manager 產品設定檔，以及如何將設定檔指派給您的團隊成員。

## 檢閱 Cloud Manager 產品設定檔 {#review-product-profiles}

使用 Admin Console，您可以查看 Cloud Manager 設定檔清單。

1. 在 [adminconsole.adobe.com](https://adminconsole.adobe.com/) 登入 Adobe Admin Console，然後在&#x200B;**總覽**&#x200B;頁面上，從&#x200B;**產品和服務**&#x200B;卡中選擇 **Adobe Experience Manager as a Cloud Service**。

   ![AEM 作為產品](/help/journey-onboarding/assets/assign-team1.png)

1. 從所有執行個體清單瀏覽至 **Cloud Manager** 執行個體。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 您將看到預先設定的 Cloud Manager 產品設定檔清單。

   ![產品設定檔](/help/journey-onboarding/assets/assign-team3.png)

在初始入門流程中要指派的最重要設定檔是：

* **業務負責人** - 這些使用者管理不同的計畫。
* **部署管理員** - 這些使用者要將計劃碼從您的存放庫部署到正在執行的 AEM 環境。
* **開發人員** - 這些使用者要開發您的自訂 AEM 應用計劃並將計劃碼認可到您的存放庫。

了解這些角色的本質及其功用，查看您的團隊成員清單以確定誰需要哪個設定檔。請記住，使用者可以在您的團隊中擁有多個角色，因此也需要多個設定檔。

## 指派業務負責人產品設定檔 {#assign-business-owner}

您現在可以新增使用者並將其指派給&#x200B;**業務負責人**&#x200B;產品設定檔。

1. 確定需要管理 Cloud Manager 計畫的使用者。這些會是您的&#x200B;**業務負責人**。

1. 在 `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 登入 Admin Console，然後在&#x200B;**總覽**&#x200B;頁面上，從&#x200B;**產品和服務**&#x200B;卡中選擇 **Adobe Experience Manager as a Cloud Service** 產品。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 在頂端導覽中選取&#x200B;**「使用者」**&#x200B;索引標籤，然後選取&#x200B;**新增使用者**。

   ![新增使用者](/help/journey-onboarding/assets/assign-team4.png)

1. 在「**新增使用者至團隊**」對話方塊中，輸入您要新增使用者的電子郵件識別碼。

   * 如果您的團隊成員尚未設定 Federated ID，請在 **ID 類型**&#x200B;選擇 **Adobe ID**。

   ![新增使用者詳細資訊](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下&#x200B;**選擇產品或使用者群組**&#x200B;標題底下的加號按鈕以開始選擇產品，選擇 **Adobe Experience Manager as a Cloud Service**，然後將&#x200B;**業務負責人**&#x200B;產品設定檔指派給使用者。

   * 每個使用者需獲指派至少一個產品設定檔，以便使用者可以存取 Cloud Manager。
   * 記得把自己作為系統管理員指派給&#x200B;**業務負責人**&#x200B;設定檔。

   ![指派使用者](/help/journey-onboarding/assets/assign-team6.png)

1. 按一下&#x200B;**儲存**&#x200B;即會傳送一封歡迎電子郵件給您新增的使用者。受邀使用者可以按一下歡迎電子郵件中的連結，並使用其 Adobe ID 登入來存取 Cloud Manager。

1. 對團隊中的使用者重複這些步驟。

已指派您的&#x200B;**業務負責人**，其現在可以存取 Cloud Manager。別忘了把自己作為系統管理員指派給&#x200B;**業務負責人**&#x200B;設定檔。

## 指派部屬管理員產品設定檔 {#assign-deployment-manager}

1. 確定需要部署計劃碼的使用者。

1. 在 `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 登入 Admin Console，然後在&#x200B;**總覽**&#x200B;頁面上，從&#x200B;**產品和服務**&#x200B;卡中選擇 **Adobe Experience Manager as a Cloud Service** 產品。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 在頂端導覽中選取&#x200B;**「使用者」**&#x200B;索引標籤，然後選取&#x200B;**新增使用者**。

   ![新增使用者](/help/journey-onboarding/assets/assign-team4.png)

1. 在「**新增使用者至團隊**」對話方塊中，輸入您要新增使用者的電子郵件識別碼。

   * 如果您的團隊成員尚未設定 Federated ID，請在 **ID 類型**&#x200B;選擇 **Adobe ID**。

   按 ![輸入識別碼](/help/journey-onboarding/assets/assign-team5.png)。

1. 按一下&#x200B;**選擇產品或使用者群組**&#x200B;標題底下的加號按鈕以開始選擇產品，選擇 **Adobe Experience Manager as a Cloud Service**，然後將&#x200B;**部屬管理員**&#x200B;產品設定檔指派給使用者。

   ![指派設定檔](/help/journey-onboarding/assets/assign-team6.png)

您的&#x200B;**部屬管理員**&#x200B;已指派，現在可以存取 Cloud Manager。根據您未來的職責，您可以視需要將自己作為系統管理員指派給&#x200B;**部署管理員**&#x200B;設定檔。

## 指派開發人員產品設定檔 {#assign-developer}

1. 確定需要開發 AEM 應用計劃和管理計劃碼的使用者。

1. 在 `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 登入 Admin Console，然後在&#x200B;**總覽**&#x200B;頁面上，從&#x200B;**產品和服務**&#x200B;卡中選擇 **Adobe Experience Manager as a Cloud Service** 產品。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 在頂端導覽中選取&#x200B;**「使用者」**&#x200B;索引標籤，然後選取&#x200B;**新增使用者**。

   ![新增使用者](/help/journey-onboarding/assets/assign-team4.png)

1. 在「**新增使用者至團隊**」對話方塊中，輸入您要新增使用者的電子郵件識別碼。

   * 如果您的團隊成員尚未設定 Federated ID，請在 **ID 類型**&#x200B;選擇 **Adobe ID**。

   ![新增使用者識別碼](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下&#x200B;**選擇產品或使用者群組**&#x200B;標題底下的加號按鈕以開始選擇產品，選擇 **Adobe Experience Manager as a Cloud Service**，然後將&#x200B;**開發人員**&#x200B;產品設定檔指派給使用者。

   ![指派設定檔](/help/journey-onboarding/assets/assign-team6.png)。

您的&#x200B;**開發人員**&#x200B;已指派，現在可以存取 Cloud Manager。根據您未來的職責，您可以視需要將自己作為系統管理員指派給&#x200B;**開發人員**&#x200B;設定檔。

## 下一步 {#whats-next}

恭喜！您新組建的 Cloud Manager 團隊 (包括您自己指派到&#x200B;**業務負責人**&#x200B;設定檔) 已完成設定。在&#x200B;**業務負責人**&#x200B;角色中，您現在距離登入 Cloud Manager 並啟用建立雲端資源只差一步。

在入門歷程的這一部分中，您已了解如何在 Admin Console 中將您的團隊成員指派至設定檔。您現在應該：

* 了解什麼是產品設定檔。
* 了解什麼是 Cloud Manager。
* 了解三個重要的 Cloud Manager 產品設定檔：**業務負責人**、**部署管理員**&#x200B;和&#x200B;**開發人員**。
* 能夠將團隊成員指派給 Cloud Manager 產品設定檔。

您現在已準備好繼續您的入門歷程，接下來查看文件[存取 Cloud Manager](cloud-manager.md)，您將在該文件中了解如何存取 Cloud Manager 和建立專案資源。

## 其他資源 {#additional-resources}

建議繼續如前所述的入門歷程。如果您想深入了解此歷程中的特定主題，請參閱以下其他資源。

* [Cloud Manager 簡介](/help/onboarding/cloud-manager-introduction.md) - 了解 Cloud Manager、Cloud Manager 計畫和環境。
* [Cloud Manager 產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md) - 了解 AEM as a Cloud Service 團隊和產品設定檔。
* [Adobe Admin Console 上的身分類型](https://helpx.adobe.com/tw/enterprise/admin-guide.html/enterprise/using/identity.ug.html) - Adobe 的 Identity Management 系統可協助管理員建立和管理使用者對應用計劃和服務的存取權。Adobe 提供這些身份類型或帳戶來對使用者進行驗證和授權。

