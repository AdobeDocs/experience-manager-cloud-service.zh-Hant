---
title: AEM as a Cloud Service 上線歷程簡介
description: 從此處開始，逐步引導您了解 AEM as a Cloud Service 的上線流程。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 858a9c4b61fd3a80a257313e48816b067ca77175
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 93%

---


# 上線歷程 {#onboarding-journey}

恭喜您選擇了 AEM as a Cloud Service！本文件將逐步引導您了解上線流程。無論您是部署新應用程式或是移轉現有應用程式，此上線歷程會建立您的團隊，並確保他們擁有 AEM as a Cloud Service 的存取權。

## 簡介 {#introduction}

Adobe Experience Manager (AEM)在內容傳遞和編寫方法上提供靈活性，使團隊能夠根據其需求選擇最佳模型。

使用[Edge Delivery Services](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/overview)進行快速、反複的撰寫及高速的內容速度，或使用傳統的Publish傳遞服務建立強大的企業發佈模型。 無論是哪種方法，都可讓組織以最適合的方式提供卓越的數位體驗。 若要開始使用Edge Delivery Services，請探索[Edge Delivery Services概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/overview)，並深入瞭解現代撰寫選項，請參閱[撰寫指南](https://www.aem.live/docs/authoring-guide)。

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

<!-- Although there may appear to be a lot to learn when getting started with AEM as a Cloud Service, conceptually there are only a few, logical pieces.-->

AEM as a Cloud Service 的上線歷程圍繞以下核心要素：

* **合約** - 審閱您的 Adobe 合約，了解上線流程的關鍵細節。
* **Experience Hub** - 使用 [experience.adobe.com](https://experience.adobe.com/) 作為 AEM 功能的集中式進入點。Experience Hub 能適應您的人物誌和權利，讓您有效率地工作。可以從這裡導覽至：
   * **Admin Console** - 管理使用者及指派角色。
   * **Cloud Manager** - 設定方案和環境、存取 Git，以及建立管道用於管理和部署自訂程式碼。
   * **Sites** - 建立、管理和提供數位體驗。(授權式權利)
   * **Assets** - 組織、儲存和分發您的數位資產。(授權式權利)
   * **Forms** - 建立和管理自適應及回應式表單。(授權式權利)

此上線歷程中會詳細敘述這些概念。目標是在此歷程結束時，您可以執行以下操作：

* 授予使用者存取 AEM as a Cloud Service 的必要權限。
* 為您的專案設定第一個雲端資源。
* 知道如何部署您的第一個程式碼並製作您的第一個內容。

您將開始使用新的 AEM as a Cloud Service 專案！

## 客群 {#audience}

上線歷程是專為初次接觸 AEM as a Cloud Service 和 AEM 一般客戶的&#x200B;**系統管理員**&#x200B;而製作。系統管理員是在您簽署 AEM as a Cloud Service 合約後，Adobe 首先聯絡的人。他們通常是第一個在 AEM as a Cloud Service 存取和設定資源的人。如果您正在閱讀本主題，您很可能是系統管理員。

系統管理員負責管理其組織 AEMaaCS 使用者的所有方面事宜，涵蓋存取服務至權限。但是，系統管理員在此過程中必須與其他職務人物誌進行互動。

| 人物誌 | 描述 | 歷程中的角色 |
| --- | --- | --- |
| 系統管理員 | 此歷程的目標是進行雲端資源的初始佈建，以及根據使用者的工作職責為其指派適當角色。 | 角色能協助您管理使用者從存取到權限的各個層面。 |
| 內容作者 | 在 AEM 中建立和審閱內容。 | 獲得系統管理員授予權限後，作者即可開始其建立內容的歷程。 |
| 開發人員 | 開發使用不同來源內容的 AEM 應用程式。 | 獲得系統管理員授予權限後，開發人員即可開始其開發解決方案的歷程。 |
| 部署管理員 | 新增或更新環境、執行管道並將程式碼部署到 AEM 環境或程式碼品質。 | 獲得系統管理員授予權限後，部署管理員即可開始其管理解決方案的歷程。 |

本上線指南說明了作為系統管理員完整上線過程。將 AEM 使用者、開發人員和部署管理員的角色作為歷程的額外選擇性部分進行簡要探討。

>[!TIP]
>
>如果您初次使用 AEM as a Cloud Service，但熟悉 AEM 並正從內部部署或 Adobe Managed Services 移轉，請參閱「[AEM as a Cloud Service 移轉歷程](/help/journey-migration/getting-started.md)」。

## 上線歷程概觀 {#overview}

以下文章詳細介紹了核心上線概念，並為您提供了 AEM as a Cloud Service 的基礎知識。儘管您可以直接進入歷程的特定部分，但許多概念都是以先前文章中的概念為基礎。因此，如果您不熟悉上線流程，Adobe 建議您從頭開始，然後按順序進行。

| | 文章 | 說明 | 客群 |
| --- | --- | --- | --- |
| 0 | 上線歷程 | 本文件 | 系統管理員 |
| 1 | [上線準備](preparation.md) | 在啟動過程開始之前，系統管理員在登入系統之前必須了解一些準備步驟。 | 系統管理員 |
| 2 | [AEM as a Cloud Service 技術](terminology.md) | 在您第一次登入 AEMaaCS 之前，了解系統的一些術語及其基本結構會很有幫助。 | 系統管理員 |
| 3 | [Admin Console](admin-console.md) | 了解 Admin Console 是什麼、如何登入以及如何以系統管理員身分驗證您的設定檔。 | 系統管理員 |
| 4 | [指派 Cloud Manager 產品設定檔](assign-profiles-cloud-manager.md) | 審閱 Cloud Manager 產品設定檔，了解如何將團隊成員指派給 Cloud Manager 產品設定檔。 | 系統管理員 |
| 5 | [存取 Experience Hub](/help/experience-hub.md) | 將 Experience Hub 作為 AEM 生態系統的統一、個人化進入點。 | AEM 使用者 |
| 6 | [存取 Cloud Manager](cloud-manager.md) | 了解如何存取 Cloud Manager，讓您可以設定專案資源。 | 系統管理員 |
| 7 | [建立計畫](create-program.md) | 了解如何使用 Cloud Manager 建立計畫。 | 系統管理員 |
| 8 | [建立環境](create-environments.md) | 了解如何使用 Cloud Manager 建立環境。 | 系統管理員 |
| 9 | [指派 AEM 產品設定檔](assign-profiles-aem.md) | 了解系統管理員如何將您的團隊成員指派至 AEM as a Cloud Service 產品設定檔。 | 系統管理員 |
| 10 | [開發人員和部署管理員工作](developers.md) | 選用 - 以開發人員身分，了解如何存取和管理 Cloud Manager Git。作為部署管理員，了解如何在 Cloud Manager 中設定管道並部署程式碼。 | 開發人員和部署管理員 |
| 11 | [AEM 使用者工作](aem-users.md) | 選擇性 - 了解作為 AEM 作者如何存取 AEM as a Cloud Service 執行個體，並熟悉為 AEM as a Cloud Service 製作內容。 | AEM 使用者 |

## 後續步驟 {#what-is-next}

您現在已準備好開始您的 AEM as a Cloud Service 上線歷程。我們鼓勵您繼續下一段歷程並閱讀文章：[上線準備](preparation.md)

## AEM 文件歷程 {#documentation-journeys}

[文件歷程](/help/journey-documentation/documentation-journeys.md)將許多不同且複雜的主題和功能相互結合。此文件設定讀者對於主題或 AEM 事前所知甚少，因此提供文字敘述來全程協助初次使用 AEM 的讀者理解和解決業務問題。

文件歷程是根據最佳實務原則所設計。讀者可使用各種資源來深入了解，包括 Adobe 的最新研究、Adobe 顧問經驗證的實施經驗和客戶專案的意見回饋。

若要了解如何讓團隊上線使用新 AEM as a Cloud Service 應用程式以及 Adobe 的建議，請由此處開始。

## 其他資源 {#additional-resources}

如果您想了解上線歷程以外的內容，以下是其他選用資源。

* [開始使用 AEM as a Cloud Service](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding) - 本簡短影片將概觀 AEM Cloud Service 的入門流程。
