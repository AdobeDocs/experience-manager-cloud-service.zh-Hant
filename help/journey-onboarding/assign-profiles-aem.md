---
title: 指派AEM產品設定檔
description: 在設定雲端資源後，您需要使用AEM產品設定檔授予團隊AEM本身的存取權。
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# 指派AEM產品設定檔 {#assign-profiles-aem}

在 [入門旅程，](overview.md) 您將學習如何使用AEM產品設定檔授予您的團隊AEM存取權。

## 目標 {#objective}

一旦您閱讀了上一期入門歷程的檔案， [建立環境、](create-environments.md) 並設定雲端資源後，您將需要使用AEM產品設定檔授予團隊AEM本身的存取權。 身為系統管理員，您需指派AEM產品設定檔來執行此作業。

閱讀本檔案後，您應了解：

* 什麼是AEM產品設定檔。
* 如何將團隊成員新增至AEM使用者產品設定檔。
* 如何將團隊成員新增至AEM管理員產品設定檔。

## AEM產品設定檔 {#aem-product-profiles}

若要使用AEM，您的團隊成員必須指派給至少一個AEM產品設定檔。 存取Cloud Manager的權限不足。 使用者必須屬於下列兩個產品設定檔之一：

* `AEM Users`  — 此群組包括執行日常內容製作工作的一般使用者。
* `AEM Administrators`  — 此群組包含負責進階功能或AEM的使用者。

指派給AEM產品設定檔的每位使用者也將取得Cloud Manager的唯讀存取權。 可透過其他產品設定檔授予Cloud Manager的寫入存取權。

## 必備條件 {#prerequisites}

開始閱讀本小節之前，您應有下列關於將使用AEM的團隊的資訊。

* 名稱
* 電子郵件地址
* 角色與責任

>[!TIP]
>
>為了上線，建議您先新增將參與即時工作的使用者，例如管理員、開發人員和內容作者。 您可以繼續上線的其餘部分，而不需新增所有使用者。 上線完成後，您稍後可以擴充至更多使用者。

## 檢視AEM產品設定檔 {#view-profiles}

請依照下列步驟，從Admin Console中查看AEM產品設定檔。

1. 登入Admin Console: [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. 從 **概述** 頁面，選取 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡片。

   ![產品和服務卡](/help/journey-onboarding/assets/assign-team1.png)

1. 導覽並選取執行個體。

   ![選擇實例](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. 您會看到AEMas a Cloud Service產品設定檔清單，這些設定檔可根據使用者的角色指派給使用者。

   ![產品設定檔](/help/journey-onboarding/assets/cloud-profiles-2.png)

## 將團隊成員新增至產品設定檔 {#add-team-members}

現在您已熟悉可用的設定檔，可視需要將其指派給團隊成員。

這些任務要求您是 **業務負責人** Cloud Manager產品設定檔。

1. 從Cloud Manager導覽至您的方案，然後選取 **管理存取** 按鈕。

   ![管理存取](/help/journey-onboarding/assets/add-team1.png)

1. 新索引標籤會將您導覽至Admin Console，您可在其中存取環境的製作例項。 選擇 **AEM管理員** 或 **AEM使用者** 根據需要授予的權限。

   ![指派存取權](/help/journey-onboarding/assets/add-team2.png)

1. 選擇 `AEM Administrator` 或 `AEM User` 按一下 **添加用戶** 如下所示，並提交完成添加團隊成員所需的詳細資訊。

   ![添加團隊成員](/help/journey-onboarding/assets/add-team3.png)

1. 如果您有需要存取權的團隊成員資訊，請對所有環境（包括開發、測試和生產）重複執行這些步驟。

您新增的使用者現在可以存取AEMas a Cloud Service作者服務！

## 旅程的結束？ {#the-end}

恭喜！ 您指派給AEMas a Cloud Service產品設定檔的使用者現在已準備好存取AEM製作環境，並開始使用AEMas a Cloud Service建立內容。 同樣地，開發人員現在可以存取Cloud Manager，使用git來儲存自訂應用程式程式碼並加以部署。 從這個意義上講，您的入門歷程已經完成，您的使用者現在可以使用AEMaaCS。

不過，如果您想要進一步了解作者和開發人員如何使用系統，您可以繼續進行本入門歷程的兩個選用部分：

* [開發人員和部署管理員任務](developers.md)  — 您可在此了解開發人員如何存取git以儲存其自訂程式碼，並使用Cloud Manager管道進行部署。
* [AEM使用者任務](aem-users.md)  — 了解如何存取AEM環境，以便開始建立內容。

## 其他資源 {#additional-resources}

* [在Admin Console中管理產品和使用者存取](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console)  — 了解如何使用Admin Console管理使用存取權。
* [設定AEM存取權逐步說明](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)  — 請參閱本概要教學，了解如何在Admin Console中設定Adobe IMS使用者、使用者群組和產品設定檔。

