---
title: 分配AEM產品配置檔案
description: 配置雲資源後，您需要使用產品配置檔案授予團隊對AEM自己的AEM訪問權。
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# 分配AEM產品配置檔案 {#assign-profiles-aem}

在 [登機之旅，](overview.md) 您將學習如何授予您團隊使用產品配置AEM文AEM件的權限。

## 目標 {#objective}

一旦你讀了上次登機旅程的檔案， [建立環境，](create-environments.md) 配置雲資源後，您需要使用產品配置檔案授予團隊對AEM自身的AEM訪問權限。 作為系統管理員，您可以通過分配產品配置AEM檔案來執行此操作。

閱讀完此文檔後，您應該瞭解：

* 產AEM品配置檔案。
* 如何將團隊成員添加AEM到用戶產品配置檔案。
* 如何將團隊成員添加AEM到Administrators產品配置檔案。

## 產AEM品配置檔案 {#aem-product-profiles}

要使AEM用，必須將團隊成員至少分配給一個產AEM品配置檔案。 訪問雲管理器的權限不足。 用戶必須屬於以下兩種產品配置檔案之一：

* `AEM Users`  — 此組包括執行日常內容創作任務的普通用戶。
* `AEM Administrators`  — 此組包括負責高級功能或的用AEM戶。

分配給產品配置AEM檔案的每個用戶也將獲得對Cloud Manager的只讀訪問權限。 可以通過其他產品配置檔案授予對雲管理器的寫訪問權限。

## 必備條件 {#prerequisites}

在開始閱讀本節之前，您應提供以下有關將使用的團隊的信AEM息。

* 名稱
* 電子郵件地址
* 角色和職責

>[!TIP]
>
>為了加入，我們建議您首先添加將參與立即任務的用戶，如管理員、開發人員和內容作者。 您可以繼續其餘的登錄，而不添加所有用戶。 完成登錄後，您可以稍後擴展到更多用戶。

## 查看產AEM品配置檔案 {#view-profiles}

按照以下步驟從AEMAdmin Console查看產品配置檔案。

1. 登錄到Admin Console [`https://adminconsole.adobe.com`。](https://adminconsole.adobe.com)

1. 從 **概述** ，選擇 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡。

   ![產品和服務卡](/help/journey-onboarding/assets/assign-team1.png)

1. 導航並選擇實例。

   ![選擇實例](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. 您將看到可以根據AEM用戶的角色分配給用戶的as a Cloud Service產品配置檔案的清單。

   ![產品配置檔案](/help/journey-onboarding/assets/cloud-profiles-2.png)

## 將團隊成員添加到產品配置檔案 {#add-team-members}

現在，您已熟悉可用的配置檔案，可根據需要將其分配給團隊成員。

這些任務要求您是系統管理員， **業務所有者** Cloud Manager產品配置檔案。

1. 從Cloud Manager導航到您的程式，然後選擇 **管理訪問** 按鈕。

   ![管理訪問](/help/journey-onboarding/assets/add-team1.png)

1. 新頁籤將您導航到Admin Console，您可以從該環境的作者實例訪問該環境。 選擇 **管AEM理員** 或 **用AEM戶** 根據此個人需要獲得的權限。

   ![分配訪問權限](/help/journey-onboarding/assets/add-team2.png)

1. 選擇 `AEM Administrator` 或 `AEM User` 按一下 **添加用戶** 如下所示，並提交完成添加團隊成員所需的詳細資訊。

   ![添加團隊成員](/help/journey-onboarding/assets/add-team3.png)

1. 如果您有需要訪問的團隊成員的資訊，請對所有環境重複這些步驟，包括開發、準備和生產。

您添加的用戶現在可以訪問AEMas a Cloud Service作者服務！

## 旅程結束？ {#the-end}

恭喜！ 您分配給AEMas a Cloud Service產品配置檔案的用戶現在可以訪問AEM創作環境並開始建立as a Cloud ServiceAEM內容。 同樣，開發人員現在可以訪問雲管理器，以使用git儲存自定義應用程式碼並部署它。 從這個意義上講，您的登機過程已經完成，您的用戶現在可以使用AEMaaCS。

但是，如果您希望更好地瞭解作者和開發人員如何使用系統，您可以繼續執行登機過程的兩個可選部分：

* [開發人員和部署管理器任務](developers.md)  — 在何處，您將瞭解開發人員如何訪問git以儲存其自定義代碼並使用Cloud Manager管道部署它。
* [用AEM戶任務](aem-users.md)  — 在何處，您將學習如何訪問AEM可開始建立內容的環境。

## 其他資源 {#additional-resources}

* [在Admin Console中管理產品和用戶訪問](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console)  — 瞭解如何使用Admin Console管理使用訪問權限。
* [配置對AEM瀏覽的訪問](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)  — 查看此簡略的瀏覽，瞭解如何在Admin Console中配置Adobe IMS用戶、用戶組和產品配置檔案。

