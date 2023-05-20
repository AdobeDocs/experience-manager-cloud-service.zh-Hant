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

恭喜您選擇了 AEM as a Cloud Service！本文件將逐步引導您了解入門流程。無論您是部署新應用程式還是遷移現有應用程式，此入門過程都可確保您的團隊已建立並可以訪問AEMas a Cloud Service。

## 簡介 {#introduction}

入門是指指定系統管理員為您的組織設定 AEM as a Cloud Service 的過程。此過程包括初始配置雲資源和根據用戶的工作職責將用戶分配給角色。 因此，每個成員都能夠登錄並訪問其資源在AEMas a Cloud Service。

![入門歷程](/help/journey-onboarding/assets/onboarding-journey.png)

本指南引導您瞭解最重要的登機主題，以便完成後您可以執行以下操作：

* 充分了解入門流程中涉及的不同條款、服務和使用者。
* 使您的團隊能夠啟動和執行，並邁出學習如何為您的 AEM as a Cloud Service 應用程式編寫和開發內容的第一步。

因此：

* 您的團隊已建立並有權訪問雲資源。
* 作AEM者可以訪AEM問as a Cloud Service並開始建立內容。
* 開AEM發人員和部署經理可以訪AEM問as a Cloud Service，並可以開始建立和部署自定義應用程式。

## 概念和目標 {#concepts}

儘管在開始使用 AEM as a Cloud Service 時可能需要學習很多東西，但從概念的角度來看，這只分為幾個邏輯部分。

* **合同**  — 您必須熟悉您的Adobe合同，因為合同定義了登機過程的各個方面。
* **Admin Console**  — 管理用戶和分配角色的位置。
* **雲管理器**  — 設定資源（如方案和環境）的工具。 您也可在此處存取 Git 和建立管道，以管理和部署自訂程式碼。

這些概念在登機旅程中作了詳細闡述。 目標是在歷程結束時，您：

* 已授予必要用戶訪問AEMas a Cloud Service。
* 已為您的專案設定了第一個雲端資源.
* 知道如何部署您的第一個程式碼並製作您的第一個內容。

基本上，你用你的新as a Cloud Service項目AEM開始了！

## 對象 {#audience}

入門歷程是專門為剛接觸 AEM as a Cloud Service 和一般 AEM 客戶的&#x200B;**系統管理員**&#x200B;編寫的。系統管理員是在您的as a Cloud Service合同簽訂後，Adobe首次聯繫AEM到的個人。 他們通常是第一個訪問和設定您的資源的AEMas a Cloud Service。 如果您正在閱讀本主題，則可能是系統管理員。

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
>如果您對as a Cloud ServiceAEM和熟悉AEM有新的瞭解，並且要從內部或Adobe托管服務進行遷移，請務必簽出 [AEMas a Cloud Service遷移](/help/journey-migration/getting-started.md)。

## 入門歷程總覽 {#overview}

以下文章詳細介紹了核心入門概念，並為您提供了 AEM as a Cloud Service 的基礎知識。儘管您可以直接進入歷程的特定部分，但許多概念都是以先前文章中的概念為基礎。因此，如果您是新入職者，Adobe建議您從開始開始按順序開始。

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
| 8 | [指派 AEM 產品設定檔](assign-profiles-aem.md) | 瞭解系統管理員如何將團隊成員分配到as a Cloud Service的產品配置AEM檔案。 | 系統管理員 |
| 9 | [開發人員和部署管理員工作](developers.md) | 可選 — 作為開發人員，瞭解如何訪問和管理Cloud Manager Git，以及如何作為部署管理器在Cloud Manager中設定管道和部署代碼。 | 開發人員和部署管理員 |
| 10 | [AEM 使用者工作](aem-users.md) | 可選 — 作為AEM作者，瞭解如何訪AEM問as a Cloud Service實例並熟悉as a Cloud Service的創作AEM內容。 | AEM 使用者 |

## 下一步 {#what-is-next}

您現在已準備好開始您的 AEM as a Cloud Service 入門歷程。我們鼓勵您繼續下一段旅程，閱讀文章 [登機準備](preparation.md)

## AEM 文件歷程 {#documentation-journeys}

[文檔旅程](/help/journey-documentation/documentation-journeys.md) 將許多不同、複雜的主題和特徵聯繫起來。 它提供一種敘事，幫助新讀者從AEM頭到尾瞭解並解決業務問題，同時假定最少的先前主題或AEM知識。

文件歷程根據最佳實務原則而設計，其中包含 Adobe 的最新研究、Adobe 顧問的成熟實作經驗以及客戶專案的意見回饋。

如果您想瞭解Adobe建議如何將團隊裝入新as a Cloud Service應用程式，請AEM從此處開始！

<!-- ERROR: Not Found (HTTP error 404)
## Additional Resources {#additional-resources}

The following are additional, optional resources if you would like to go beyond the content of the onboarding journey.

* [AEM Champion Tips and Tricks - Cloud Manager Onboarding Playbook](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Watch this video to learn Cloud Manager onboarding tips and trick from an AEM champion. -->


