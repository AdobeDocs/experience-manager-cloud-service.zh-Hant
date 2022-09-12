---
title: 將團隊成員指派給Cloud Manager產品設定檔
description: 請詳閱本頁，了解如何將團隊成員指派給Cloud Manager產品設定檔
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 0%

---


# 將團隊成員指派給Cloud Manager產品設定檔 {#assign-team-members}

在 [入門旅程，](overview.md) 您將學習如何指派團隊成員至Cloud Manager產品設定檔。

## 目標 {#objective}

在此歷程的上一步中， [存取Admin Console、](admin-console.md) 您現在已學會登入Admin Console，並以系統管理員身分驗證您的權限。 您現在已準備好讓團隊成員存取Cloud Manager。 您可以指派產品設定檔來執行此作業。

授予使用者Adobe解決方案的存取權時，您不一定想授予使用者完整存取權。 產品設定檔可讓每個解決方案擁有其專屬的一組使用者權限。 您可使用Admin Console來指派產品設定檔。

第一步是授與使用者對Cloud Manager的存取權。 Cloud manager透過企業開發設定及其專門建立的CI/CD管道，為您提供支援，這些管道可確保徹底測試和最高的程式碼品質，以提供絕佳的體驗。

閱讀本檔案後，您應：

* 了解哪些產品設定檔。
* 了解Cloud Manager是什麼。
* 了解三個重要的Cloud Manager產品設定檔： **業務負責人**, **部署管理員**，和 **開發人員**.
* 能將團隊成員指派給Cloud Manager產品設定檔。

## 必備條件 {#prerequisites}

若要將團隊成員指派給產品設定檔，您需要有關團隊成員的詳細資訊，這些成員需要存取AEMas a Cloud Service，包括：

* 名稱
* 電子郵件地址
* 角色與責任

>[!TIP]
>
>為了上線，Adobe建議您先新增將參與即時工作的使用者，例如管理員、開發人員和內容作者。
>
>您可以繼續上線程式，而不新增所有使用者。 上線完成後，您可以新增其他使用者。

## 產品設定檔 {#product-profiles}

授予使用者Adobe解決方案的存取權時，您不一定想授予使用者完整存取權。 產品設定檔可讓每個解決方案擁有其專屬的一組使用者權限，這些權限是使用Admin Console設定。

例如，在此歷程的稍後部分，您將會使用Admin Console，為AEM管理員和AEM作者指派產品設定檔，以授與使用者對AEM解決方案的存取權。

不過，下一步是授與產品設定檔，讓您的團隊成員可以先存取Cloud Manager。

## Cloud Manager {#cloud-manager}

身為系統管理員，您知道成功的AEMas a Cloud Service專案不僅取決於使用AEM建立令人讚嘆的內容，還取決於開發及部署您自己的自訂程式碼和應用程式，以傳送您的AEM內容。

Cloud Manager是AEMas a Cloud Service不可或缺的一部分，可用來管理程式碼部署的CI/CD管道、管理程式碼存放庫及管理環境。

您的團隊必須先授與必要的產品設定檔，才能執行其他作業，才能將其上線至Cloud Manager。 後續步驟會顯示如何使用Admin Console尋找Cloud Manager產品設定檔，以及如何將其指派給您的團隊成員。

## 檢閱Cloud Manager產品設定檔 {#review-product-profiles}

使用此Admin Console，您可以看到Cloud Manager設定檔清單。

1. 登入Adobe Admin Console，網址為 [adminconsole.adobe.com](https://adminconsole.adobe.com/) 和 **概述** 頁面，選取 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡片。

   ![AEM as a product](/help/journey-onboarding/assets/assign-team1.png)

1. 導覽至 **Cloud Manager** 例項（從所有例項清單）。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 您會看到預先設定的Cloud Manager產品設定檔清單。

   ![產品設定檔](/help/journey-onboarding/assets/assign-team3.png)

在初始上線程式中指派的最重要設定檔為：

* **業務負責人**  — 這些用戶管理不同的程式。
* **部署管理員**  — 這些使用者會將程式碼從您的存放庫部署至執行中的AEM環境。
* **開發人員**  — 這些使用者開發您的自訂AEM應用程式，並將程式碼提交至您的存放庫。

了解這些角色是什麼及其作用，並檢閱您的團隊成員清單，以決定誰需要哪個設定檔。 請記得，使用者在您的團隊中可能有且通常擁有多個角色，因此也需要多個設定檔。

## 分配業務負責人產品配置檔案 {#assign-business-owner}

您現在可以新增使用者，並將他們指派至 **業務負責人** 產品設定檔。

1. 識別需要管理Cloud Manager程式的使用者。 這些將是您的 **企業主**.

1. 登入Admin Console: `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 和 **概述** 頁面，選取 **Adobe Experience Manager as a Cloud Service** 產品來源 **產品和服務** 卡片。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 選取 **使用者** 標籤，然後選取 **添加用戶**.

   ![新增使用者](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **新增使用者至您的團隊** 對話框，輸入要添加的用戶的電子郵件ID。

   * 如果尚未設定團隊成員的Federated ID，請選取 **Adobe ID** 針對 **ID類型**.

   ![添加用戶詳細資訊](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下 **選取產品或使用者群組** 開始選擇產品並選擇 **Adobe Experience Manager as a Cloud Service** 並指派 **業務負責人** 產品設定檔傳送給使用者。

   * 將每個使用者指派至少一個產品設定檔，讓該使用者可以存取Cloud Manager。
   * 請記得將自己指派為 **業務負責人** 角色。

   ![指派使用者](/help/journey-onboarding/assets/assign-team6.png)

1. 按一下 **儲存** 會傳送歡迎電子郵件給您新增的使用者。 受邀的使用者可按一下歡迎電子郵件中的連結，並使用其Adobe ID登入，以存取Cloud Manager。

1. 對您團隊中的使用者重複這些步驟。

您的 **業務負責人**&#x200B;已指派，現在可存取Cloud Manager。 別忘了將自己指派為 **業務負責人** 設定檔。

## 分配部署管理員產品配置檔案 {#assign-deployment-manager}

1. 識別需要部署程式碼的使用者。

1. 登入Admin Console: `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 和 **概述** 頁面選取 **Adobe Experience Manager as a Cloud Service** 產品 **產品和服務** 卡片。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 選取 **使用者** 標籤，然後選取 **添加用戶**.

   ![新增使用者](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **新增使用者至您的團隊** 對話框，輸入要添加的用戶的電子郵件ID。

   * 如果尚未設定團隊成員的Federated ID，請選取 **Adobe ID** 針對 **ID類型**.

   ![輸入ID](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下 **選取產品或使用者群組** 開始選擇產品並選擇 **Adobe Experience Manager as a Cloud Service** 並指派 **部署管理員** 產品設定檔傳送給使用者。

   ![指派設定檔](/help/journey-onboarding/assets/assign-team6.png)

您的 **部署管理員**&#x200B;已指派，現在可存取Cloud Manager。 根據您將來的責任，您可能也不需要將自己指派為 **部署管理員** 設定檔。

## 指派開發人員產品設定檔 {#assign-developer}

1. 識別需要開發AEM應用程式和管理程式碼的使用者。

1. 登入Admin Console: `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 和 **概述** 頁面選取 **Adobe Experience Manager as a Cloud Service** 產品 **產品和服務** 卡片。

   ![產品和服務](/help/journey-onboarding/assets/assign-team1.png)

1. 選取 **使用者** 標籤，然後選取 **添加用戶**.

   ![新增使用者](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **新增使用者至您的團隊** 對話框，輸入要添加的用戶的電子郵件ID。

   * 如果尚未設定團隊成員的Federated ID，請選取 **Adobe ID** 針對 **ID類型**.

   ![新增使用者ID](/help/journey-onboarding/assets/assign-team5.png)

1. 按一下 **選取產品或使用者群組** 開始選擇產品並選擇 **Adobe Experience Manager as a Cloud Service** 並指派 **開發人員** 產品設定檔傳送給使用者。

   ![指派設定檔](/help/journey-onboarding/assets/assign-team6.png).

您的 **開發人員**&#x200B;已指派，現在可存取Cloud Manager。 根據您將來的責任，您可能也不需要將自己指派為 **開發人員** 設定檔。

## 下一步 {#whats-next}

恭喜！ 您新組建的Cloud Manager團隊(包括您自己指派給 **業務負責人** 設定檔)。 在 **業務負責人**，您現在只需要一步即可登入Cloud Manager並啟用雲端資源的建立。

在入門歷程的這部分，您學習了如何將團隊成員指派給Admin Console中的設定檔。 您現在應該：

* 了解哪些產品設定檔。
* 了解Cloud Manager是什麼。
* 了解三個重要的Cloud Manager產品設定檔： **業務負責人**, **部署管理員**，和 **開發人員**.
* 能將團隊成員指派給Cloud Manager產品設定檔。

您現在已準備好繼續上線歷程，繼續檢閱此檔案 [存取Cloud Manager、](cloud-manager.md) 您將在何處學習如何存取Cloud Manager及建立專案資源。

## 其他資源 {#additional-resources}

建議您繼續前述的入門歷程。 如果您想從此歷程對特定主題進行深入探討，這些是額外的資源。

* [Cloud Manager簡介](/help/onboarding/cloud-manager-introduction.md)  — 了解Cloud Manager、Cloud Manager程式和環境。
* [Cloud Manager產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md)  — 了解AEMas a Cloud Service團隊和產品設定檔。
* [Adobe Admin Console上的身分類型](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html) -Adobe的身份管理系統可幫助管理員建立和管理用戶對應用程式和服務的訪問。 Adobe提供這些身分類型或帳戶，以驗證和授權使用者。

