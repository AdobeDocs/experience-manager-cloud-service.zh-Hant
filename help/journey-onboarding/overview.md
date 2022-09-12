---
title: AEMas a Cloud Service入門歷程簡介
description: 從此處開始，逐步引導您了解 AEM as a Cloud Service 的上線流程。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 75c0e8cbaa409fa48750e794c27ace98eda107d0
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 3%

---


# 入門歷程 {#onboarding-journey}

祝賀您選擇AEMas a Cloud Service! 本檔案是您逐步完成入門程式的引導式歷程的起點。 無論您是部署新應用程式還是移轉現有應用程式，此入門歷程都能確保您的團隊已完成設定，且可存取AEMas a Cloud Service。

## 簡介 {#introduction}

上線是指定系統管理員為貴組織設定AEMas a Cloud Service的程式。 這包括初始布建雲端資源，以及根據使用者的工作職責指派使用者角色。 因此，每個成員都能登入並存取其AEMas a Cloud Service資源。

![入門歷程](/help/journey-onboarding/assets/onboarding-journey.png)

本指南會引導您了解最重要的入門主題，以便您在完成後能有：

* 充分了解入門程式中涉及的不同條款、服務和使用者。
* 讓您的團隊能夠開始並執行，並採取第一步，了解如何為您的AEMas a Cloud Service應用程式編寫和開發內容。

因此：

* 您的團隊將會完成設定，且可存取雲端資源。
* AEM作者將可存取AEMas a Cloud Service，並可開始建立內容。
* AEM開發人員和部署管理員將能存取AEMas a Cloud Service，並可開始建立和部署自訂應用程式。

## 概念與目標 {#concepts}

雖然開始使用AEM時似乎要學很多，但從概念上講，只有幾個邏輯部分。

* **合同**  — 您必須熟悉您的Adobe合約，因為合約會定義上線程的各個方面。
* **Admin Console**  — 這是管理使用者和指派角色的位置。
* **Cloud Manager**  — 這是設定資源（如方案和環境）的工具。 您也可在此存取Git和建立管道，以管理和部署自訂程式碼。

這些概念將在入門歷程中詳細說明。 目標是在歷程結束時，您：

* 已授予必要使用者AEMaaCS的存取權
* 已為您的專案設定第一個雲端資源
* 了解如何部署您的第一個程式碼，並撰寫您的第一個內容。

基本上，您的新AEMas a Cloud Service專案會順利運作！

## 對象 {#audience}

入門歷程是專為 **系統管理員** 客戶對AEM as a Cloud Service和AEM的全新了解。 系統管理員是在簽署AEMas a Cloud Service合約後，由Adobe第一次聯絡的個人，通常是第一個存取和設定AEMas a Cloud Service資源的人。 如果讀到此資訊，則可能是系統管理員。

系統管理員負責管理其組織的AEMaaCS使用者從存取到權限的所有方面。 但是，系統管理員必須在過程中與其他角色交互。

| 角色 | 說明 | 歷程中的角色 |
|---|---|---|
| 系統管理員 | 此歷程的目標，提供雲資源的初始布建，以及根據使用者的工作職責，將使用者指派給適當的角色 | 管理使用者從存取權限到存取權限的所有方面 |
| 內容作者 | 在AEM中建立和檢閱內容 | 系統管理員授予權限後，作者就可以開始建立內容的歷程 |
| 開發人員 | 開發使用不同來源內容的AEM應用程式 | 一旦系統管理員授予權限，開發人員就可以開始自己的歷程，開發解決方案 |
| 部署管理員 | 新增或更新環境、執行管道，以及將程式碼部署至AEM環境或程式碼品質。 | 一旦系統管理員授予權限，部署管理員就可以開始管理部署的自己歷程 |

本入門指南說明以系統管理員身分上線的完整流程。 我們會簡短地探討AEM使用者、開發人員和部署管理員的角色，作為歷程的其他選用部分。

>[!TIP]
>
>若您是初次使用AEMas a Cloud Service人員，但已熟悉AEM，且正在從內部部署或Adobe Managed Services移轉，請務必查看 [AEMas a Cloud Service移轉歷程。](/help/journey-migration/getting-started.md)

## 入門歷程概觀 {#overview}

以下文章詳細說明核心入門概念，並提供您AEM as a Cloud Service的基本知識。 雖然您可以直接前往歷程的特定部分，但許多概念都是以先前文章中的概念為基礎而建立。 因此，如果您是剛上線的，建議您從頭開始，依序進行。

| # | 文章 | 說明 | 對象 |
|---|---|---|---|
| 0 | 入門歷程 | 此文檔 | 系統管理員 |
| 1 | [入門準備](preparation.md) | 登錄過程開始之前，系統管理員在登錄系統之前必須了解一些數字或準備步驟。 | 系統管理員 |
| 2 | [AEMas a Cloud Service術語](terminology.md) | 在您首次登入AEMaCS之前，請先了解系統的某些術語及其基本結構，這是很有幫助的。 | 系統管理員 |
| 3 | [Admin Console](admin-console.md) | 了解Admin Console、登入方式，以及如何以系統管理員身分驗證您的設定檔。 | 系統管理員 |
| 4 | [指派Cloud Manager產品設定檔](assign-profiles-cloud-manager.md) | 檢閱Cloud Manager產品設定檔，並了解如何將團隊成員指派給Cloud Manager產品設定檔。 | 系統管理員 |
| 5 | [存取Cloud Manager](cloud-manager.md) | 了解如何存取Cloud Manager，以便設定專案資源。 | 系統管理員 |
| 6 | [建立方案](create-program.md) | 了解如何使用Cloud Manager建立方案。 | 系統管理員 |
| 7 | [建立環境](create-environments.md) | 了解如何使用Cloud Manager建立環境。 | 系統管理員 |
| 8 | [指派AEM產品設定檔](assign-profiles-aem.md) | 了解系統管理員如何將您的團隊成員指派給AEMas a Cloud Service的產品設定檔。 | 系統管理員 |
| 9 | [開發人員和部署管理員任務](developers.md) | 可選 — 了解身為開發人員，您如何存取和管理Cloud Manager Git，以及作為部署管理員，如何在Cloud Manager中設定管道和部署程式碼。 | 開發人員和部署經理 |
| 10 | [AEM使用者任務](aem-users.md) | 選用 — 了解身為AEM作者，如何存取AEMas a Cloud Service例項，並熟悉AEMas a Cloud Service的編寫內容。 | AEM使用者 |

## 下一步 {#what-is-next}

您現在已準備好開始AEMas a Cloud Service入門歷程。 我們鼓勵您繼續前往歷程的下一個部分並閱讀文章 [入門準備](preparation.md)

## AEM檔案歷程 {#documentation-journeys}

[檔案歷程](/help/journey-documentation/documentation-journeys.md) 將許多不同的、可能複雜的主題和特徵聯繫起來，提供一種敘述，幫助讀者從頭到尾理解並解決業務問題，同時假定事先的主題或AEM知識最少。

說明檔案歷程是根據最佳實務原則而設計，根據Adobe的最新研究、Adobe顧問經驗證的實作經驗，以及客戶專案的意見回饋。

如果您想了解Adobe建議如何讓您的團隊上線至新的AEMas a Cloud Service應用程式，請從這裡開始！
