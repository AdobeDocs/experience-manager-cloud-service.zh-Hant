---
title: AEM as a Cloud Service 上線歷程簡介
description: 從此處開始，逐步引導您了解 AEM as a Cloud Service 的上線流程。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: ht
source-wordcount: '1295'
ht-degree: 100%

---


# 上線歷程 {#onboarding-journey}

恭喜您選擇了 AEM as a Cloud Service！本文件將逐步引導您了解上線流程。無論您是部署新應用程式或是移轉現有應用程式，此上線歷程會建立您的團隊，並確保他們擁有 AEM as a Cloud Service 的存取權。

## 簡介 {#introduction}

Adobe Experience Manager 是一套功能強大的可組合內容服務，可在任何頻道中快速提供極具影響力的個人化體驗，為所有人解鎖所有內容。**Edge Delivery Services** 是 Adobe Experience Manager 的最創新服務，可使內容速度達到極限並提供卓越的體驗。參閱 [Edge Delivery Services 概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/overview)，了解如何開始使用 Edge Delivery Services。若要了解如何使用 Edge Delivery Services，請參閱[開發人員教學課程](https://www.aem.live/developer/tutorial)頁面。

上線是指定的系統管理員為您的組織設定 AEM as a Cloud Service 的過程。此程序包括雲端資源的初始設定，以及根據使用者的工作職責為其指派角色。因此，每個成員都能夠登入並存取他們的 AEM as a Cloud Service 資源。

![上線歷程](/help/journey-onboarding/assets/onboarding-journey.png)。

本指南將引導您了解最重要的上線主題，完成後您將會：

* 充分了解上線流程中涉及的不同條款、服務和使用者。
* 使您的團隊能夠啟動和執行，並邁出學習如何為您的 AEM as a Cloud Service 應用程式製作和開發內容的第一步。

因此：

* 您的團隊已建立並可以存取雲端資源。
* AEM 作者將可以存取 AEM as a Cloud Service，並開始建立內容。
* AEM 開發人員和部署管理員可以存取 AEM as a Cloud Service，並開始建立和部署自訂應用程式。

## 概念和目標 {#concepts}

儘管在開始使用 AEM as a Cloud Service 時可能需要學習很多東西，但從概念的角度來看，這只分為幾個邏輯部分。

* **合約** - 您必須熟悉您的 Adobe 合約，因為它定義了上線流程的各方面內容。
* **Admin Console** - 在此處管理使用者和指派角色。
* **Cloud Manager** - 這是設定程序和環境等資源的工具。您也可在那裡存取 Git 和建立管道，以管理和部署自訂程式碼。

此上線歷程中會詳細敘述這些概念。目標是在此歷程結束時，您可以執行以下操作：

* 授予使用者存取 AEM as a Cloud Service 的必要權限。
* 為您的專案設定第一個雲端資源。
* 知道如何部署您的第一個程式碼並製作您的第一個內容。

您將開始使用新的 AEM as a Cloud Service 專案！

## 客群 {#audience}

上線歷程是專為初次接觸 AEM as a Cloud Service 和 AEM 一般客戶的&#x200B;**系統管理員**&#x200B;而製作。系統管理員是在您簽署 AEM as a Cloud Service 合約後，Adobe 首先聯絡的人。他們通常是第一個在 AEM as a Cloud Service 存取和設定資源的人。如果您正在閱讀本主題，您很可能是系統管理員。

系統管理員負責管理其組織 AEMaaCS 使用者的所有方面事宜，涵蓋存取服務至權限。但是，系統管理員在此過程中必須與其他職務角色進行互動。

| 角色 | 說明 | 歷程中的角色 |
|---|---|---|
| 系統管理員 | 此歷程的目標是進行雲端資源的初始佈建，以及根據使用者的工作職責為其指派適當角色。 | 管理使用者從存取權到權限的各方面內容 |
| 內容作者 | 在 AEM 中建立和檢閱內容 | 作者獲得系統管理員授予權限後，便可以開始自己建立內容的歷程 |
| 開發人員 | 開發使用不同來源內容的 AEM 應用程式 | 開發人員獲得系統管理員授予權限後，便可以開始自己開發解決方案的歷程 |
| 部署管理員 | 新增或更新環境、執行管道並將程式碼部署到 AEM 環境或程式碼品質。 | 系統管理員授與權限後，部署管理員可以開始自己的管理解決方案歷程 |

本上線指南說明了作為系統管理員完整上線過程。將 AEM 使用者、開發人員和部署管理員的角色作為歷程的額外選擇性部分進行簡要探討。

>[!TIP]
>
>如果您初次使用 AEM as a Cloud Service，但熟悉 AEM 並正從內部部署或 Adobe Managed Services 移轉，請參閱「[AEM as a Cloud Service 移轉歷程](/help/journey-migration/getting-started.md)」。

## 上線歷程總覽 {#overview}

以下文章詳細介紹了核心上線概念，並為您提供了 AEM as a Cloud Service 的基礎知識。儘管您可以直接進入歷程的特定部分，但許多概念都是以先前文章中的概念為基礎。因此，如果您不熟悉上線流程，Adobe 建議您從頭開始，然後按順序進行。

| | 文章 | 說明 | 客群 |
|---|---|---|---|
| 0 | 上線歷程 | 本文件 | 系統管理員 |
| 1 | [上線準備](preparation.md) | 在啟動過程開始之前，系統管理員在登入系統之前必須了解一些準備步驟。 | 系統管理員 |
| 2 | [AEM as a Cloud Service 技術](terminology.md) | 在您第一次登入 AEMaaCS 之前，了解系統的一些術語及其基本結構會很有幫助。 | 系統管理員 |
| 3 | [Admin Console](admin-console.md) | 了解 Admin Console 是什麼、如何登入以及如何以系統管理員身分驗證您的設定檔。 | 系統管理員 |
| 4 | [指派 Cloud Manager 產品設定檔](assign-profiles-cloud-manager.md) | 查看 Cloud Manager 產品設定檔，並了解如何將團隊成員指派給 Cloud Manager 產品設定檔。 | 系統管理員 |
| 5 | [存取 Cloud Manager](cloud-manager.md) | 了解如何存取 Cloud Manager，以便您可以設定專案資源。 | 系統管理員 |
| 6 | [建立計畫](create-program.md) | 了解如何使用 Cloud Manager 建立計畫。 | 系統管理員 |
| 7 | [建立環境](create-environments.md) | 了解如何使用 Cloud Manager 建立環境。 | 系統管理員 |
| 8 | [指派 AEM 產品設定檔](assign-profiles-aem.md) | 了解系統管理員如何將您的團隊成員指派到 AEM as a Cloud Service 產品設定檔。 | 系統管理員 |
| 9 | [開發人員和部署管理員工作](developers.md) | 選擇性 - 了解作為開發人員如何存取和管理 Cloud Manager Git，以及作為部署管理員如何在 Cloud Manager 中設定管道和部署程式碼。 | 開發人員和部署管理員 |
| 10 | [AEM 使用者工作](aem-users.md) | 選擇性 - 了解作為 AEM 作者如何存取 AEM as a Cloud Service 執行個體，並熟悉為 AEM as a Cloud Service 製作內容。 | AEM 使用者 |

## 後續步驟 {#what-is-next}

您現在已準備好開始您的 AEM as a Cloud Service 上線歷程。我們鼓勵您繼續下一段歷程並閱讀文章：[上線準備](preparation.md)

## AEM 文件歷程 {#documentation-journeys}

[文件歷程](/help/journey-documentation/documentation-journeys.md)將許多不同且複雜的主題和功能相互結合。此文件設定讀者對於主題或 AEM 事前所知甚少，因此提供文字敘述來全程協助初次使用 AEM 的讀者理解和解決業務問題。

文件歷程是根據最佳實務原則所設計。讀者可使用各種資源來深入了解，包括 Adobe 的最新研究、Adobe 顧問經驗證的實施經驗和客戶專案的意見回饋。

若要了解如何讓團隊上線使用新 AEM as a Cloud Service 應用程式以及 Adobe 的建議，請由此處開始。

## 其他資源 {#additional-resources}

如果您想了解上線歷程以外的內容，以下是其他選用資源。

* [開始使用 AEM as a Cloud Service](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding) - 本簡短影片將概述 AEM Cloud Service 的入門流程。
