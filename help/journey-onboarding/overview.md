---
title: AEM as a Cloud Service 入門歷程簡介
description: 從此處開始，逐步引導您了解 AEM as a Cloud Service 的入門流程。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 58%

---


# 入門歷程 {#onboarding-journey}

恭喜您選擇了 AEM as a Cloud Service！本文件將逐步引導您了解入門流程。無論您是部署新應用程式還是移轉現有應用程式，此入門歷程都能確保您的團隊已完成設定，且可存取AEMas a Cloud Service。

## 簡介 {#introduction}

入門是指指定系統管理員為您的組織設定 AEM as a Cloud Service 的過程。此程式包括初始布建雲端資源，並根據使用者的工作職責指派使用者至角色。 因此，每個成員都能登入並存取其AEMas a Cloud Service的資源。

![入門歷程](/help/journey-onboarding/assets/onboarding-journey.png)

本指南會引導您了解最重要的入門主題，以便您在完成時能有下列內容：

* 充分了解入門流程中涉及的不同條款、服務和使用者。
* 使您的團隊能夠啟動和執行，並邁出學習如何為您的 AEM as a Cloud Service 應用程式編寫和開發內容的第一步。

因此：

* 您的團隊已設定且可存取雲端資源。
* AEM作者可存取AEMas a Cloud Service，並可開始建立內容。
* AEM開發人員和部署管理員可存取AEMas a Cloud Service，並可開始建立和部署自訂應用程式。

## 概念和目標 {#concepts}

儘管在開始使用 AEM as a Cloud Service 時可能需要學習很多東西，但從概念的角度來看，這只分為幾個邏輯部分。

* **合同**  — 您必須熟悉Adobe合約，因為合約會定義上線程的各個方面。
* **Admin Console**  — 管理使用者並指派角色的位置。
* **Cloud Manager**  — 設定資源（如方案和環境）的工具。 您也可在此處存取 Git 和建立管道，以管理和部署自訂程式碼。

這些概念在入門歷程中會詳細說明。 目標是在歷程結束時，您：

* 已授予必要使用者AEM as a Cloud Service的存取權。
* 已為您的專案設定了第一個雲端資源.
* 知道如何部署您的第一個程式碼並製作您的第一個內容。

基本上，您的新AEMas a Cloud Service專案已順利展開！

## 對象 {#audience}

入門歷程是專門為剛接觸 AEM as a Cloud Service 和一般 AEM 客戶的&#x200B;**系統管理員**&#x200B;編寫的。系統管理員是在簽署AEMas a Cloud Service合約後，Adobe首次聯絡的個人。 他們通常是第一個在AEM as a Cloud Service上存取和設定您資源的人。 如果您正在閱讀本主題，則可能是系統管理員。

系統管理員會管理其組織 AEMaaCS 使用者的各個方面，從存取權到權限都是。但是，系統管理員必須在此過程中與其他角色進行互動。

| 角色 | 說明 | 歷程中的角色 |
|---|---|---|
| 系統管理員 | 此歷程的目標是提供雲端資源的初始設定，以及根據使用者的工作職責為其指派適當角色。 | 管理使用者從存取權到權限的各方面內容 |
| 內容作者 | 在 AEM 中建立和檢閱內容 | 系統管理員授與權限後，作者可以開始自己的內容製作歷程 |
| 開發人員 | 開發使用來自不同來源內容的 AEM 應用程式 | 系統管理員授與權限後，開發人員可以開始自己的開發解決方案歷程 |
| 部署管理員 | 新增或更新環境、執行管道並將程式碼部署到 AEM 環境或程式碼品質。 | 系統管理員授與權限後，部署管理員可以開始自己的管理解決方案歷程 |

本入門指南說明了作為系統管理員入門的完整過程。將 AEM 使用者、開發人員和部署管理員的角色作為歷程的額外選擇性部分進行簡要探討。

>[!TIP]
>
>若您是初次接觸AEM as a Cloud Service並熟悉AEM，且要從內部部署或Adobe Managed Services移轉，請務必查看 [AEMas a Cloud Service移轉歷程](/help/journey-migration/getting-started.md).

## 入門歷程總覽 {#overview}

以下文章詳細介紹了核心入門概念，並為您提供了 AEM as a Cloud Service 的基礎知識。儘管您可以直接進入歷程的特定部分，但許多概念都是以先前文章中的概念為基礎。因此，如果您剛上線，Adobe建議您從頭開始，並依序進行。

| # | 文章 | 說明 | 對象 |
|---|---|---|---|
| 0 | 入門歷程 | 本文件 | 系統管理員 |
| 1 | [入門準備](preparation.md) | 在啟動過程開始之前，系統管理員在登入系統之前必須了解一些準備步驟。 | 系統管理員 |
| 2 | [AEM as a Cloud Service 技術](terminology.md) | 在您第一次登入 AEMaaCS 之前，了解系統的一些術語及其基本結構會很有幫助。 | 系統管理員 |
| 3 | [Admin Console](admin-console.md) | 了解 Admin Console 是什麼、如何登入以及如何以系統管理員身分驗證您的設定檔。 | 系統管理員 |
| 4 | [指派 Cloud Manager 產品設定檔](assign-profiles-cloud-manager.md) | 查看 Cloud Manager 產品設定檔，並了解如何將團隊成員指派給 Cloud Manager 產品設定檔。 | 系統管理員 |
| 5 | [存取 Cloud Manager](cloud-manager.md) | 了解如何存取 Cloud Manager，以便您可以設定專案資源。 | 系統管理員 |
| 6 | [建立計畫](create-program.md) | 了解如何使用 Cloud Manager 建立計畫。 | 系統管理員 |
| 7 | [建立環境](create-environments.md) | 了解如何使用 Cloud Manager 建立環境。 | 系統管理員 |
| 8 | [指派 AEM 產品設定檔](assign-profiles-aem.md) | 了解系統管理員如何在AEM as a Cloud Service中將您的團隊成員指派給產品設定檔。 | 系統管理員 |
| 9 | [開發人員和部署管理員工作](developers.md) | 選用 — 身為開發人員，了解如何存取和管理Cloud Manager Git，以及身為部署管理員，如何在Cloud Manager中設定管道和部署程式碼。 | 開發人員和部署管理員 |
| 10 | [AEM 使用者工作](aem-users.md) | 選用 — 身為AEM作者，了解如何存取AEMas a Cloud Service例項，並熟悉AEMas a Cloud Service的編寫內容。 | AEM 使用者 |

## 下一步 {#what-is-next}

您現在已準備好開始您的 AEM as a Cloud Service 入門歷程。我們鼓勵您繼續前往歷程的下一個部分並閱讀文章 [入門準備](preparation.md)

## AEM 文件歷程 {#documentation-journeys}

[檔案歷程](/help/journey-documentation/documentation-journeys.md) 將許多不同、複雜的主題和特徵聯繫在一起。 它提供一種敘述，幫助剛接觸AEM的讀者從頭到尾了解並解決業務問題，同時假定先前主題或AEM知識最少。

文件歷程根據最佳實務原則而設計，其中包含 Adobe 的最新研究、Adobe 顧問的成熟實作經驗以及客戶專案的意見回饋。

如果您想了解Adobe建議如何讓您的團隊上線至新的AEMas a Cloud Service應用程式，請從這裡開始！

<!-- ERROR: Not Found (HTTP error 404)
## Additional Resources {#additional-resources}

The following are additional, optional resources if you would like to go beyond the content of the onboarding journey.

* [AEM Champion Tips and Tricks - Cloud Manager Onboarding Playbook](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Watch this video to learn Cloud Manager onboarding tips and trick from an AEM champion. -->


