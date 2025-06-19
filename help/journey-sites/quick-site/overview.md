---
title: 'AEM 快速網站建立歷程 '
description: 從這裡開始，此歷程會逐步引導您了解簡單易用的 AEM 快速建立網站工具，以簡化 AEM 網站的前端開發，並在沒有 AEM 後端知識的情況下快速自訂您的網站。
exl-id: b8218232-0298-4b16-9dab-fa59be592a24
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: ht
source-wordcount: '1020'
ht-degree: 100%

---

# AEM 快速網站建立歷程  {#quick-site-creation-journey}

{{traditional-aem}}

從這裡開始，此歷程會逐步引導您了解簡單易用的 AEM 快速建立網站工具，以簡化 AEM 網站的前端開發，並在沒有 AEM 後端知識的情況下快速自訂您的網站。

## 簡介 {#introduction}

AEM Sites 是用於建立和管理數位體驗的強大工具集。內容作者可以使用網站編輯器輕鬆建立數位體驗，並使用Sites 主控台組織內容，同時能夠查看 AEM 跨管道傳遞給您客群的即時內容。

AEM 快速建立網站工具讓非開發人員使用網站範本從頭開始快速建立網站。建立後，快速建立網站工具還可讓您快速為 AEM 網站自訂主題並建立風格 (JavaScript、CSS 和靜態資源)。這使得前端開發人員即使不懂 AEM 也能與內容建立者分開且並行工作。AEM 管理員只需下載網站主題並將其提供給前端開發人員，前端開發人員使用他們偏好的工具自訂主題，然後將變更提交到 AEM 程式碼存放庫，然後進行部署。

快速建立網站工具讓開發人員不需具備網站建立知識，前端開發人員不需具備 AEM 知識，主題開發工作與內容建立工作可並行，因而大幅加速網站的價值實現時間並增加網站自訂和部署敏捷性。

## 影片概觀 {#video-overview}

如需快速了解此功能的實際運作，[您可以觀看這個五分鐘的簡介](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw)。

此文件歷程將逐步詳細地引導您了解影片中的所有功能，以便您了解工作流程，可在您自己的環境中重新建立此流程。

## AEM 文件歷程 {#documentation-journeys}

[文件歷程](/help/journey-documentation/documentation-journeys.md)連結許多不同的複雜主題和功能，提供相關敘述來協助剛開始使用 AEM 的讀者，讓他們能從頭到尾理解和解決業務問題，但是事前不需要知道太多主題資訊或 AEM 知識。

文件歷程根據最佳實務原則而設計，其中包含 Adobe 的最新研究、Adobe 顧問的成熟實作經驗以及客戶專案的意見回饋。

如果您想了解 Adobe 建議如何使用 AEM 解決網站業務案例，AEM Sites 歷程是理想的出發點。

## 客群 {#audience}

此歷程闡述自訂 AEM Sites 主題的要求、步驟和方法。主要客群是不需具備 AEM 知識的前端開發人員。但是，為了說明整個過程，該歷程涉及管理員，並假設他們具有基本的 AEM Sites 和 Cloud Manager 知識。在實務上，多個人可以擔任多個角色，此歷程以管理員和前端開發人員的角度出發。

| 角色 | 描述 | 歷程中的角色 |
|---|---|---|
| 前端開發人員 | 自訂網站主題 | 取得 AEM 管理員提供的主題並加以自訂，以便將其部署到 AEM 網站。 |
| 內容作者 | 建立和管理作為網站傳遞的內容 | 內容作者在 AEM 上建立內容，這些內容使用前端開發人員自訂的主題呈現。 |
| AEM 管理員 | 建立新的 AEM 網站 | AEM 管理員根據範本建立新網站，然後提供主題給前端開發人員以進行自訂。 |
| Cloud Manager 管理員 | 建立管道並授予存取權 | Cloud Manager 管理員建立前端管道，並授予存取權給前端開發人員，使其能夠將自訂項提交到 AEM Git 存放庫。 |

## AEM 快速網站建立歷程 {#the-journey}

您將在此歷程中探索許多主題。以下文章為您提供如何使用快速建立網站工具建立和自訂 AEM 網站的基本知識，以及詳細外部技術文件的連結。

| # | 文章 | 描述 | 負責角色 |
|---|---|---|--|
| 0 | AEM 快速網站建立歷程  | 本文件 | AEM &amp; Cloud Manager 管理員 |
| 1 | [了解 Cloud Manager 和快速網站建立工作流程](cloud-manager.md) | 了解 Cloud Manager 以及它與快速建立網站的新流程如何連結在一起。 | AEM 管理員 |
| 2 | [使用範本建立網站](create-site.md) | 了解如何使用網站範本快速建立新的 AEM 網站。 | AEM 管理員 |
| 3 | [設定您的管道](pipeline-setup.md) | 建立前端管道以管理網站主題的自訂。 | Cloud Manager 管理員 |
| 4 | [授予前端開發人員存取權](grant-access.md) | 讓前端開發人員加入 Cloud Manager，以便能存取您的 AEM 網站 Git 存放庫和管道。 | Cloud Manager 管理員 |
| 5 | [擷取 git 存放庫存取資訊](retrieve-access.md) | 了解前端開發人員如何使用 Cloud Manager 來存取 Git 存放庫資訊。 | 前端開發人員 |
| 6 | [自訂網站主題](customize-theme.md) | 了解如何建立網站主題、如何自訂網站主題，以及如何使用即時 AEM 內容測試網站主題。 | 前端開發人員 |
| 7 | [部署您的自訂主題](deploy-theme.md) | 了解如何使用管道部署網站主題。 | 前端開發人員 |

## 下一步 {#what-is-next}

您現在已準備好開始您的 Adobe 快速網站建立歷程。

* 如果您是 AEM 或 Cloud Manager 管理員，或者如果您同時擔任前端開發人員和管理員角色，或者如果您只是想了解 AEM 中的端到端流程，請從歷程的開頭：[了解 Cloud Manager](cloud-manager.md) 開始進行。
* 如果您只負責前端開發，會與 AEM 和 Cloud Manager 管理員互動，可以直接跳到「[擷取 Git 存放庫存取權資訊](retrieve-access.md)」，以取得 AEM Git 存放庫存取權並開始自訂。
* 如果您已經了解 AEM Sites 和 Cloud Manager 如何共同運作，而想直接開始設定，您可以[直接跳到使用範本建立網站](create-site.md)。

## 其他資源 {#additional-resources}

查看這些其他資源，進一步了解 AEM 的強大功能如何共同運作。

* [AEM as a Cloud Service 技術文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - 如果您已經對 AEM 有深入的了解，您可能想直接查閱深入的技術文件。
* [網站管理文件](/help/sites-cloud/administering/site-creation/create-site.md) - 查看關於建立網站的技術文件，了解快速建立網站工具功能的更多詳細資訊。
