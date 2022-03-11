---
title: 授予對前端開發人員的訪問權限
description: 將前端開發人員裝載到Cloud Manager中，以便他們能夠訪問您的站AEM點Git儲存庫和管道。
exl-id: 58e95c92-b859-4bb9-aa62-7766510486fd
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# 授予對前端開發人員的訪問權限 {#grant-fed-access}

將前端開發人員裝載到Cloud Manager中，以便他們能夠訪問您的站AEM點Git儲存庫和管道。

## 到目前為止的故事 {#story-so-far}

在快速建立站AEM點的上一文檔中， [設定管道，](pipeline-setup.md) 您學會了如何建立前端管道來管理站點主題的自定義，現在您應該：

* 瞭解前端管線是什麼。
* 瞭解如何在雲管理器中設定前端管道。

您現在需要通過登入過程授予前端開發人員對Cloud Manager的訪問權限，以便前端開發人員可以訪問您建立的AEMgit儲存庫和管道。

## 目標 {#objective}

授予Cloud Manager訪問權限和為用戶分配用戶角色的過程稱為登機。 本文檔將概述登入前端開發人員的最重要步驟，閱讀後您將知道：

* 如何以用戶身份添加前端開發人員。
* 如何將所需角色授予前端開發人員。

>[!TIP]
>
>整個文檔記錄過程都是以雲服務形式將您AEM的團隊加入，連結在 [「其他資源」部分](#additional-resources) 的子文檔。

## 責任角色 {#responsible-role}

此部分路程適用於Cloud Manager管理員。

## 要求 {#requirements}

* 你需要成為 **業務所有者** 角色。
* 你需要成為 **系統管理** 中。
* 你需要有權進入Admin Console。

## 將前端開發人員添加為用戶 {#add-fed-user}

首先，您需要使用Admin Console將前端開發人員作為用戶添加。

1. 登錄Admin Console，地址為 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)。

1. 登錄後，將顯示與以下影像類似的概述頁面。

   ![Admin Console概述](assets/admin-console.png)

1. 通過檢查螢幕右上角的組織名稱，確保您位於相應的組織中。

   ![檢查組織名稱](assets/correct-org.png)

1. 選擇 **Adobe Experience Manager as a Cloud Service** 從 **產品和服務** 卡。

   ![選擇AEMaCS](assets/select-aemaacs.png)

1. 您可以看到預配置的Cloud Manager產品配置檔案的清單。 如果您未看到這些配置檔案，請與Cloud Manager管理員聯繫，因為您在組織中可能沒有正確的權限。

   ![產品配置檔案](assets/product-profiles.png)

1. 要將前端開發人員分配給正確的配置檔案，請點擊或按一下 **用戶** 的 **添加用戶** 按鈕

   ![添加用戶](assets/add-user.png)

1. 在 **將用戶添加到團隊** 對話框，鍵入要添加的用戶的電子郵件ID。 對於ID類型，如果尚未設定團隊成員的Federated ID，請選擇「Adobe ID」。

   ![將用戶添加到團隊](assets/add-to-team.png)

1. 在 **產品** 選擇，點擊或按一下加號，然後選擇 **Adobe Experience Manager as a Cloud Service** 並指定 **部署管理器** 和 **開發人員** 產品配置檔案。

   ![分配團隊配置檔案](assets/assign-team.png)

1. 點擊或按一下 **保存** 歡迎電子郵件將發送給您作為用戶添加的前端開發人員。

受邀的前端開發人員可以通過按一下歡迎電子郵件中的連結並使用其Adobe ID登錄來訪問雲管理器。

## 切換到前端開發人員 {#handover}

通過向前端開發人員發送電子郵件邀請到Cloud Manager，您和AEM管理員現在可以向前端開發人員提供開始自定義所需的剩餘資訊。

* A [典型內容路徑](#example-page)
* 主題源 [已下載](#download-theme)
* 的 [代理用戶憑據](#proxy-user)
* 程式的名稱或程式的URL [從雲管理器複製](pipeline-setup.md#login)
* 前端設計要求

## 下一步是什麼 {#what-is-next}

現在，您已完成快速站點創AEM建旅程的這一部分，您應該知道：

* 如何以用戶身份添加前端開發人員。
* 如何將所需角色授予前端開發人員。

在此知識基礎上構建並繼AEM續快速建立網站的過程，方法是下次查看文檔 [檢索Git儲存庫訪問資訊，](retrieve-access.md) 它只將視角切換到前端開發人員，並說明前端開發人員用戶Cloud Manager如何訪問git儲存庫資訊。

## 其他資源 {#additional-resources}

建議您通過審閱文檔進入快速站點建立過程的下一部分 [檢索前端開發人員憑據，](retrieve-access.md) 下面是一些附加的可選資源，這些資源對本文檔中提到的一些概念進行了更深入的瞭解，但不需要繼續旅行。

* [登機之旅](/help/journey-onboarding/home.md)  — 本指南是您的出發點，可確保您的團隊已建立並能夠訪問AEMas a Cloud Service。
