---
title: AEMas a Cloud Service登機
description: 從此處開始，概括瞭解從登機過程到AEMas a Cloud Service的指導。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 75c0e8cbaa409fa48750e794c27ace98eda107d0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 登機之旅 {#onboarding-journey}

祝賀您選擇AEMas a Cloud Service! 本文檔是您引導您完成登機過程的起點。 無論您是部署新應用程式還是遷移現有應用程式，這一入門過程都確保您的團隊已建立，並能夠訪問AEMas a Cloud Service。

## 簡介 {#introduction}

登機是指定系統管理員為您的組織設定AEMas a Cloud Service的過程。 這包括初始配置雲資源和根據用戶的工作職責將用戶分配給角色。 因此，每個成員都能夠登錄並訪問其AEMas a Cloud Service資源。

![登機之旅](/help/journey-onboarding/assets/onboarding-journey.png)

本指南將引導您瞭解最重要的登機主題，以便在完成後，您可以：

* 充分瞭解參與登機過程的不同術語、服務和用戶。
* 使您的團隊能夠啟動並運行，並採取第一步步驟學習如何為您的as a Cloud Service應用程式編寫和開AEM發內容。

因此：

* 您的團隊將被設定，並有權訪問雲資源。
* 作AEM者將有權訪AEM問as a Cloud Service並開始建立內容。
* 開AEM發人員和部署經理將有權訪AEM問as a Cloud Service，並可以開始建立和部署自定義應用程式。

## 概念和目標 {#concepts}

雖然從as a Cloud Service入手似乎要學AEM很多，但概念上只有少數邏輯部分。

* **合同**  — 您需要熟悉您的Adobe合同，因為它定義了登機流程的各個方面。
* **Admin Console**  — 這是管理用戶和分配角色的位置。
* **雲管理器**  — 這是設定資源（如方案和環境）的工具。 您也可以在此訪問git並建立管道來管理和部署自定義代碼。

這些概念將在這次登機旅程中詳細闡述。 目標是在旅程結束時，您：

* 已授予必要用戶對AEMaaCS的訪問權限
* 已為項目設定第一個雲資源
* 瞭解如何部署您的第一個代碼並編寫您的第一個內容。

基本上，你會用你的新as a Cloud Service項目AEM開始行動！

## 對象 {#audience}

登機旅程是專門為 **系統管理員** 對as a Cloud Service和一般AEM客戶都AEM很新。 系統管理員是在您的as a Cloud Service合同簽署後首次通過Adobe聯繫AEM的個人，通常是訪問和設定您的as a Cloud Service資源AEM的第一人。 如果您正在閱讀，則可能是系統管理員。

系統管理員管理其組織的AEMaaCS用戶的所有方面，從訪問權限到權限。 但是，系統管理員必須在此過程中與其他人員進行交互。

| 角色 | 說明 | 《旅程中的角色》 |
|---|---|---|
| 系統管理員 | 此旅程的目標是，提供雲資源的初始配置和根據用戶的工作職責將用戶分配給適當的角色 | 管理用戶從訪問權限到訪問權限的所有方面 |
| 內容作者 | 建立和查看中的內AEM容 | 一旦系統管理員授予權限，作者就可以開始自己的建立內容的旅程 |
| 開發人員 | 開發AEM從不同來源使用內容的應用程式 | 一旦系統管理員授予了權限，開發人員就可以開始自己的旅程開發解決方案 |
| 部署管理器 | 添加或更新環境、運行管道，並將代碼部署到AEM環境或代碼質量。 | 一旦系統管理員授予權限，部署經理就可以開始自己的管理部署之旅 |

本入門指南說明了以系統管理員身份入門的完整過程。 用戶、開AEM發人員和部署經理的角色作為旅程中的附加、可選部分進行了簡要的探討。

>[!TIP]
>
>如果您剛剛學AEM習as a Cloud Service，但已熟悉AEM並且正在從內部部署或Adobe托管服務進行遷移，請務必簽出 [AEMas a Cloud Service遷移。](/help/journey-migration/getting-started.md)

## 登機旅程概述 {#overview}

以下文章詳細介紹了入門概念的核心，並向您提供了有關AEMas a Cloud Service的基礎知識。 雖然你可以直接進入旅程的某個特定部分，但許多概念都建立在先前文章中的概念之上。 因此，如果您是新入職者，我們建議您從開始開始按順序開始。

| # | 文章 | 說明 | 對象 |
|---|---|---|---|
| 0 | 登機之旅 | 此文檔 | 系統管理員 |
| 1 | [登機準備](preparation.md) | 登錄過程開始之前，系統管理員在登錄系統之前必須瞭解一些數字或準備步驟。 | 系統管理員 |
| 2 | [AEMas a Cloud Service術語](terminology.md) | 在首次登錄AEMaaCS之前，瞭解系統的一些術語及其基本結構會有所幫助。 | 系統管理員 |
| 3 | [Admin Console](admin-console.md) | 瞭解Admin Console是什麼、如何登錄以及如何以系統管理員身份驗證您的配置檔案。 | 系統管理員 |
| 4 | [分配Cloud Manager產品配置檔案](assign-profiles-cloud-manager.md) | 查看Cloud Manager產品配置檔案並瞭解如何將團隊成員分配給Cloud Manager產品配置檔案。 | 系統管理員 |
| 5 | [訪問雲管理器](cloud-manager.md) | 瞭解如何訪問雲管理器，以便設定項目資源。 | 系統管理員 |
| 6 | [建立程式](create-program.md) | 瞭解如何使用雲管理器建立程式。 | 系統管理員 |
| 7 | [建立環境](create-environments.md) | 瞭解如何使用雲管理器建立環境。 | 系統管理員 |
| 8 | [分配AEM產品配置檔案](assign-profiles-aem.md) | 瞭解系統管理員如何將團隊成員分配AEM到as a Cloud Service的產品配置檔案。 | 系統管理員 |
| 9 | [開發人員和部署管理器任務](developers.md) | 可選 — 瞭解作為開發人員您如何訪問和管理Cloud Manager Git，以及作為部署管理器，如何在Cloud Manager中設定管道和部署代碼。 | 開發人員和部署經理 |
| 10 | [用AEM戶任務](aem-users.md) | 可選 — 瞭解作AEM者如何訪問AEMas a Cloud Service實例並熟悉as a Cloud Service的創作AEM內容。 | 用AEM戶 |

## 下一步 {#what-is-next}

您現在已準備好開始AEMas a Cloud Service的登機之旅。 我們鼓勵您繼續下一段旅程，閱讀文章 [登機準備](preparation.md)

## 文檔AEM旅程 {#documentation-journeys}

[文檔旅程](/help/journey-documentation/documentation-journeys.md) 通過提供幫助讀者瞭解和解決商業問題的敘事，將許多不同的、或許複雜的主題和特徵聯繫起來AEM，讀者可以從頭到尾對商業問題有新意，但只要假設事先的主題或知AEM識很少。

文檔旅程是圍繞最佳做法原則設計的，這些原則由Adobe的最新研究、Adobe顧問的經驗證的實施經驗和客戶項目的反饋所指導。

如果您想瞭解Adobe建議如何將您的團隊安裝到您的新as a Cloud Service應用AEM程式上，請從此開始！
