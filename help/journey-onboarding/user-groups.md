---
title: 通知的使用者群組
description: 了解如何在Admin Console中建立使用者群組，以管理重要電子郵件通知的接收。
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 532184edca597452e76fdf763e7377d5e835bebc
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---


# 通知的使用者群組 {#user-groups}

了解如何在Admin Console中建立使用者群組，以管理重要電子郵件通知的接收。

## 總覽 {#overview}

Adobe不時需要聯絡有關其AEMas a Cloud Service環境的資訊。 除了產品內通知外，Adobe偶爾也會使用電子郵件來傳送此類通知。 此類通知有兩種類型：

* **事件通知 — Cloud Service**  — 這些通知會在發生事件或Adobe發現AEMas a Cloud Service環境可能有可用性問題時傳送。
* **主動通知 — Cloud Service**  — 當Adobe支援團隊成員想要提供潛在最佳化或建議的指引，以利於您的AEMas a Cloud Service環境時，會傳送這些通知。

若要讓正確的使用者收到這些通知，您必須設定使用者群組。

## 必備條件 {#prerequisites}

由於使用者群組是在Admin Console中建立和維護的，因此在建立通知的使用者群組之前，您必須：

* 具有添加和編輯組成員資格的權限。
* 具有有效的Adobe Admin Console設定檔。

## 建立新的Cloud Manager產品設定檔 {#create-groups}

若要正確設定接收通知，您需要建立兩個使用者群組。 這些步驟只能執行一次。

1. 登入Admin Console: [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. 從 **概述** 頁面，選取 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡片。

   ![使用者群組](assets/products_services.png)

1. 導覽至 **Cloud Manager** 例項（從所有例項清單）。

   ![建立使用者群組](assets/cloud_manager_instance.png)

1. 您會看到所有已設定Cloud Manager產品設定檔的清單。 例如：

   ![建立使用者群組](assets/cloud_manager_profiles.png)

1. 按一下 **新設定檔** 並介紹以下細節：

   * 產品設定檔名稱：事件通知 — Cloud Service
   * 顯示名稱：事件通知 — Cloud Service
   * 說明：適用於在事件期間或Adobe發現AEMas a Cloud Service環境可能存在可用性問題時會收到通知之使用者的Cloud Manager設定檔。

1. 按一下 **儲存** 並重複步驟5，並提供下列詳細資訊：

   * 產品設定檔名稱：主動通知 — Cloud Service
   * 顯示名稱：主動通知 — Cloud Service
   * 說明：適用於當Adobe支援團隊成員想要針對您的AEMas a Cloud Service環境設定提供潛在最佳化或建議的指引時，會收到通知之使用者的Cloud Manager設定檔。

>[!NOTE]
>
>請務必使Cloud Manager設定檔名稱與上述完全相同。 請從提供的說明複製並貼上產品設定檔名稱。 任何偏差或錯字都會導致通知無法視需要傳送。 如果發生錯誤或尚未定義設定檔，Adobe會預設通知指派給Cloud Manager開發人員（是、或和）Deployment Manager設定檔的現有使用者。

## 將使用者指派至新通知產品設定檔 {#add-users}

現在已建立群組，您必須指派適當的使用者。 您可以在建立新使用者或更新現有使用者時執行此操作。

### 新增使用者至群組 {#new-user}

1. 識別應接收事件或主動通知的使用者。

1. 登入Admin Console: [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) 如果您尚未登入。

1. 從 **概述** 頁面，選取 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡片。

   ![使用者](assets/product_services.png)

1. 選取 **使用者** 標籤，然後選取 **添加用戶**.

   ![使用者](assets/cloud_manager_add_user.png)

1. 在 **新增使用者至您的團隊** 對話框，輸入要添加的用戶的電子郵件ID。

   * 如果尚未設定團隊成員的Federated ID，請為ID類型選取Adobe ID 。
   * 如果用戶已存在，請參閱步驟9。

1. 按一下 **選擇產品** 開始選擇產品並選擇 **Adobe Experience Manager as a Cloud Service** 並指派 **事件通知 — Cloud Service** 或 **主動通知 — Cloud Service**，或兩者皆對使用者。

1. 按一下 **儲存** 會傳送歡迎電子郵件給您新增的使用者。 受邀的使用者現在會收到通知。

1. 對您要接收通知的團隊使用者重複這些步驟。

1. 如果用戶已存在，請搜索用戶的名稱，並：

   * 按一下使用者的名稱。
   * 在 **產品** ，按一下 **編輯**.
   * 按一下鉛筆按鈕 **選擇產品** 開始選擇產品並選擇 **Adobe Experience Manager as a Cloud Service** 並指派 **事件通知 — Cloud Service** 或 **主動通知 — Cloud Service**，或兩者皆對使用者。
   * 按一下 **儲存** 會傳送歡迎電子郵件給您新增的使用者。 受邀的使用者現在會收到通知。
