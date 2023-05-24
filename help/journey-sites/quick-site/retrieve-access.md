---
title: 擷取Git存放庫存取資訊
description: 瞭解前端開發人員如何使用Cloud Manager存取Git存放庫資訊。
exl-id: 3ef1cf86-6da4-4c09-9cfc-acafc8f6dd5c
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 6%

---

# 擷取Git存放庫存取資訊 {#retrieve-access}

瞭解前端開發人員如何使用Cloud Manager存取Git存放庫資訊。

## 到目前為止 {#story-so-far}

如果您是隻負責自訂網站主題的前端開發人員，則不需要瞭解AEM的設定方式，可以直接跳至 [目標](#objective) 區段。

如果您還擔任Cloud Manager或AEM管理員以及前端開發人員的角色，您已在AEM快速網站建立歷程的上一個檔案中瞭解， [授予前端開發人員存取權，](grant-access.md) 如何入門前端開發人員，讓他們能存取Git存放庫，您現在應該知道：

* 如何將前端開發人員新增為使用者。
* 如何將所需的角色授與給前端開發人員。

本文接下來會說明前端開發人員如何使用Cloud Manager存取權來擷取憑證以存取AEM Git存放庫。

現在已根據範本建立網站，設定了管道，前端開發人員已上線並擁有他們所需的所有資訊，本文將視角從管理員轉移到前端開發人員角色專用。

## 目標 {#objective}

本檔案說明您如何在前端開發人員角色中存取Cloud Manager並擷取AEM Git存放庫的存取認證。 閱讀本檔案後，您將：

* 深入瞭解Cloud Manager是什麼。
* 已擷取您的認證以存取AEM Git，以便您可以認可自訂。

## 負責角色 {#responsible-role}

此歷程的這一部分適用於前端開發人員。

## 要求 {#requirements}

「快速網站建立」工具可讓前端開發人員獨立工作，而無需瞭解AEM或其設定方式。 但是，Cloud Manager管理員必須將前端開發人員載入專案團隊，並且AEM管理員必須為您提供一些必要的資訊。 在繼續之前，請確定您有下列資訊。

* 從AEM管理員：
   * 要自訂的主題來源檔案
   * 用作參考基礎的範例頁面的路徑
   * 根據即時AEM內容測試您自訂內容的Proxy使用者憑證
   * 前端設計需求
* 從Cloud Manager管理員：
   * 來自Cloud Manager的歡迎電子郵件，通知您存取權
   * Cloud Manager中的方案名稱或URL

如果您缺少這些專案中的任何一項，請聯絡AEM管理員或Cloud Manager管理員。

我們假設前端開發人員在前端開發工作流程以及安裝的常見工具方面具有豐富的經驗，包括：

* git
* npm
* webpack
* 偏好的編輯器

## 瞭解Cloud Manager {#understanding-cloud-manager}

Cloud Manager可讓組織在雲端中自行管理AEM。 其內容包含持續整合與持續傳遞 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加速自訂項目或更新的傳遞，而不會影響效能或安全性。

對於前端開發人員而言，它是進行以下操作的閘道：

* 存取AEM Git存放庫資訊，以便認可前端自訂。
* 啟動部署管道以部署您的自訂。

Cloud Manager管理員會將您加入Cloud Manager使用者。 您應該已收到類似下列的歡迎電子郵件。

![歡迎電子郵件](assets/welcome-email.png)

如果您尚未收到此電子郵件，請聯絡Cloud Manager管理員。

## 存取 Cloud Manager {#access-cloud-manager}

1. 登入Adobe Experience Cloud於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 或按一下歡迎電子郵件中提供的連結。

1. Cloud Manager 列出了可用的各種計畫。點選或按一下Cloud Manager管理員提供的您需要存取的專案。 如果這是您的第一個AEMaaCS前端專案，您可能只有一個可用計畫。

   ![在Cloud Manager中選取計畫](assets/cloud-manager-select-program.png)

您現在可以看到計畫的概覽。 您的頁面看起來會有所不同，但與此範例類似。

![Cloud Manager概觀](assets/cloud-manager-overview.png)

## 擷取存放庫存取資訊 {#repo-access}

1. 在 **管道** 部分，點選或按一下 **存取存放庫資訊** 按鈕。

   ![管道](assets/pipelines-repo-info.png)

1. 此 **存放庫資訊** 對話方塊開啟。

   ![存放庫資訊](assets/repo-info.png)

1. 點選或按一下 **產生密碼** 按鈕為您建立密碼。

1. 將產生的密碼儲存至安全密碼管理員。 密碼將永不再顯示。

1. 同時複製 **使用者名稱** 和 **Git命令列** 欄位。 您稍後會使用此資訊來存取存放庫。

1. 點選或按一下 **關閉**.

## 下一步 {#what-is-next}

現在您已完成AEM快速網站建立歷程的這一部分，您應：

* 深入瞭解Cloud Manager是什麼。
* 已擷取您的認證以存取AEM Git，以便您可以認可自訂。

在此知識的基礎上繼續您的AEM快速網站建立歷程，接下來檢視檔案 [自訂網站主題](customize-theme.md) 您將在其中瞭解如何使用即時AEM內容建置網站主題、如何自訂和測試。

## 其他資源 {#additional-resources}

我們建議您檢閱檔案，繼續快速網站建立歷程的下一部分 [自訂網站主題](customize-theme.md) 以下是一些其他可選資源，這些資源對本文檔中提到的一些概念進行了更深入的探究，但並非繼續此歷程所必需的。

* [Adobe Experience Manager Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant)  — 探索Cloud Manager檔案以取得其功能的完整詳細資訊。
