---
title: 授予前端開發人員存取權
description: 將前端開發人員載入Cloud Manager，以便他們能夠存取您的AEM網站Git存放庫和管道。
exl-id: 58e95c92-b859-4bb9-aa62-7766510486fd
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 2%

---

# 授予前端開發人員存取權 {#grant-fed-access}

將前端開發人員載入Cloud Manager，以便他們能夠存取您的AEM網站Git存放庫和管道。

## 到目前為止 {#story-so-far}

在AEM快速網站建立歷程的上一個檔案中， [設定您的管道，](pipeline-setup.md) 您已瞭解如何建立前端管道來管理網站主題的自訂，現在應：

* 瞭解什麼是前端管道。
* 瞭解如何在Cloud Manager中設定前端管道。

您現在需要透過上線流程授予前端開發人員對Cloud Manager的存取權，以便前端開發人員可以存取AEM Git存放庫和您建立的管道。

## 目標 {#objective}

授與對Cloud Manager的存取權並將使用者角色指派給您的使用者的程式稱為上線。 本檔案將概述入門前端開發人員的最重要步驟，閱讀後您將瞭解：

* 如何將前端開發人員新增為使用者。
* 如何將所需的角色授與給前端開發人員。

>[!TIP]
>
>有專門用於將您的團隊上線到AEM as a Cloud Service的完整檔案歷程，連結在 [其他資源區段](#additional-resources) 如果您需要此流程的更多詳細資訊，請參閱本檔案以瞭解詳情。

## 負責角色 {#responsible-role}

此歷程的這一部分適用於Cloud Manager管理員。

## 要求 {#requirements}

* 您必須成為以下群組成員： **業務負責人** Cloud Manager中的角色。
* 您需要成為 **系統管理員** 在Cloud Manager中。
* 您需要該Admin Console的存取權。

## 將前端開發人員新增為使用者 {#add-fed-user}

首先，您需要使用Admin Console將前端開發人員新增為使用者。

1. 登入Admin Console於 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).

1. 登入後，畫面會顯示類似下列影像的概觀頁面。

   ![Admin Console概觀](assets/admin-console.png)

1. 檢查畫面右上角的組織名稱，確認您隸屬於適當的組織。

   ![檢查組織名稱](assets/correct-org.png)

1. 選取 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡片。

   ![選取AEMaaCS](assets/select-aemaacs.png)

1. 您可以看到預先設定的Cloud Manager產品設定檔清單。 如果您沒有看到這些設定檔，請聯絡您的Cloud Manager管理員，因為您的組織中可能沒有正確的許可權。

   ![產品設定檔](assets/product-profiles.png)

1. 若要將前端開發人員指派給正確的設定檔，請點選或按一下 **使用者** 標籤然後按一下 **新增使用者** 按鈕。

   ![新增使用者](assets/add-user.png)

1. 在 **新增使用者至您的團隊** 對話方塊中，輸入您要新增之使用者的電子郵件識別碼。 在ID型別中，如果尚未設定團隊成員的Federated ID，請選取Adobe ID 。

   ![新增使用者至團隊](assets/add-to-team.png)

1. 在 **產品** 選取、點選或按一下加號，然後選取 **Adobe Experience Manager as a Cloud Service** 並指派 **部署管理員** 和 **開發人員** 給使用者的產品設定檔。

   ![指派團隊設定檔](assets/assign-team.png)

1. 點選或按一下 **儲存** 並且會傳送一封歡迎電子郵件給您新增為使用者的前端開發人員。

受邀的前端開發人員可以按一下歡迎電子郵件中的連結並使用其Adobe ID登入來存取Cloud Manager。

## 移交給前端開發人員 {#handover}

在前往前端開發人員的途中，透過向Cloud Manager發出的電子郵件邀請，您和AEM管理員現在可以向前端開發人員提供開始自訂所需的剩餘資訊。

* A [典型內容的路徑](#example-page)
* 主題來源 [您已下載](#download-theme)
* 此 [proxy使用者認證](#proxy-user)
* 方案的名稱或URL [複製自Cloud Manager](pipeline-setup.md#login)
* 前端設計需求

## 下一步 {#what-is-next}

現在您已完成AEM快速網站建立歷程的這一部分，您應瞭解：

* 如何將前端開發人員新增為使用者。
* 如何將所需的角色授與給前端開發人員。

在此知識的基礎上繼續您的AEM快速網站建立歷程，接下來檢視檔案 [擷取Git存放庫存取資訊，](retrieve-access.md) 這會將視角專門切換到前端開發人員，並說明前端開發人員如何使用Cloud Manager存取Git存放庫資訊。

## 其他資源 {#additional-resources}

我們建議您檢閱檔案，繼續快速網站建立歷程的下一部分 [擷取前端開發人員憑證，](retrieve-access.md) 以下是一些其他可選資源，這些資源對本文檔中提到的一些概念進行了更深入的探究，但並非繼續此歷程所必需的。

* [入門歷程](/help/journey-onboarding/overview.md)  — 本指南可作為您的起點，確保您的團隊已建立並擁有AEMas a Cloud Service的存取權。
