---
title: AEM快速網站建立歷程
description: 從這裡開始，透過簡單易用的AEM快速網站建立工具進行引導式歷程，以簡化AEM網站的前端開發，並在不具備AEM後端知識的情況下快速自訂您的網站。
source-git-commit: 8daa6bc7d5df3263e8f2b506d8e0a23ecc547872
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# AEM快速網站建立歷程 {#quick-site-creation-journey}

從這裡開始，透過簡單易用的AEM快速網站建立工具進行引導式歷程，以簡化AEM網站的前端開發，並在不具備AEM後端知識的情況下快速自訂您的網站。

>[!CAUTION]
>
>快速網站建立工具目前是技術預覽。 除非經Adobe支援同意，否則可供測試及評估之用，且非供生產使用。

## 簡介 {#introduction}

AEM Sites是功能強大的工具集，用於建立和管理數位體驗。 內容作者可以使用網站編輯器輕鬆建立數位體驗，並使用網站主控台整理內容，同時可以看到AEM即時內容，如同跨管道傳送給您的對象一樣。

AEM快速網站建立工具可讓非開發人員使用網站範本，從頭開始快速建立新網站。 建立後，「快速網站建立」工具也可讓您快速自訂AEM網站（JavaScript、CSS和靜態資源）的主題和樣式。 這可讓不需要AEM知識的前端開發人員，與內容建立者分開工作，並與其平行。 AEM管理員只需下載網站主題，並提供給前端開發人員，讓他們使用自己最喜愛的工具進行自訂，然後將變更提交至AEM程式碼存放庫，再由系統部署。

透過消除網站建立的任何開發人員知識、消除前端開發的AEM知識需求，以及允許主題開發與內容建立並行進行，AEM快速網站建立工具可大幅加快網站的價值實現速度，並提高網站的自訂和部署靈活性。

## 影片概述 {#video-overview}

若要快速概述此功能的實際運作，您可以觀看這五分鐘的簡介。

>[!VIDEO]
>
>https://www.youtube.com/watch?v=NQeQ1jZ7ZBw

本檔案歷程將逐步帶您了解影片中的所有功能，讓您了解程式，並在自己的環境中重新建立程式。

## AEM檔案歷程 {#documentation-journeys}

[檔案歷程](/help/journey-documentation/home.md) 將許多不同的、可能也很複雜的主題和特徵聯繫起來，提供一種敘述，幫助讀者從頭到尾理解並解決業務問題，同時假定事先的主題或AEM知識最少。

說明檔案歷程是根據最佳實務原則而設計，根據Adobe的最新研究、Adobe顧問經驗證的實作經驗，以及客戶專案的意見回饋。

如果您想了解Adobe建議如何透過AEM解決網站業務案例，AEM Sites歷程即為起點。

## 對象 {#audience}

此歷程說明自訂AEM Sites主題的需求、步驟和方法。 其主要受眾是前端開發人員，不需要AEM知識。 不過，為了說明整個程式，此歷程牽涉到管理員，他們假設具有基本的AEM Sites和Cloud Manager知識。 實際上，多人可擔任多個角色，此歷程可支援管理員和前端開發人員的觀點。

| 角色 | 說明 | 歷程中的角色 |
|---|---|---|
| 前端開發人員 | 自訂網站主題 | 取用AEM管理員提供的主題並自訂主題，以便部署至AEM網站。 |
| 內容作者 | 建立並管理以網站形式傳送的內容 | 內容作者在AEM上建立內容，內容會以前端開發人員自訂的主題呈現。 |
| AEM 管理員 | 建立新AEM網站 | AEM管理員會根據範本建立新網站，然後為前端開發人員提供可自訂的主題。 |
| Cloud Manager管理員 | 建立管道並授予存取權 | Cloud Manager管理員會建立前端管道，並授予前端開發人員的存取權，以便提交AEM Git存放庫的自訂項目。 |

## AEM快速網站建立歷程 {#the-journey}

您將在此歷程中探索許多主題。 以下文章提供您使用快速網站建立工具建立和自訂AEM網站的基本知識，並連結至詳細的技術檔案。

|#|文章|說明|負責角色| |—|—|—| |0|AEM快速網站建立歷程|本檔案|AEM &amp; Cloud Manager管理員| |1|[了解Cloud Manager和快速網站建立工作流程](cloud-manager.md)|了解Cloud Manager及其如何將新的快速網站建立程式連結在一起。|AEM管理員| |2|[從範本建立網站](create-site.md)|了解如何使用網站範本快速建立新AEM網站。|AEM管理員| |3|[設定管道](pipeline-setup.md)|建立前端管道以管理網站主題的定製。|Cloud Manager管理員| |4|[授予前端開發人員的存取權](grant-access.md)|將前端開發人員上線至Cloud Manager，讓他們能存取您的AEM網站Git存放庫和管道。|Cloud Manager管理員| |5|[擷取Git存放庫存取資訊](retrieve-access.md)|了解前端開發人員如何使用Cloud Manager存取Git存放庫資訊。|前端開發人員| |6|[自訂網站主題](customize-theme.md)|了解網站主題的建立方式、如何自訂主題，以及如何使用即時AEM內容測試主題。|前端開發人員| |7|[部署自定義的主題](deploy-theme.md)|了解如何使用管道部署網站主題。|前端開發人員|

## 下一步 {#what-is-next}

您現在已準備好開始Adobe快速網站建立歷程。

* 如果您是AEM或Cloud Manager管理員，或您同時提供前端開發人員和管理員角色，或如果您只想了解AEM中的端對端程式，請從歷程的開頭開始使用 [了解Cloud Manager](cloud-manager.md) 如下所述。
* 如果您只負責前端開發，並會與AEM和Cloud Manager管理員互動，可以直接跳到 [擷取Git存放庫存取資訊](retrieve-access.md) 存取AEM git存放庫並開始自訂。
* 如果您已了解AEM Sites和Cloud Manager可共同運作，且想直接從設定開始，您可以 [直接跳到從模板建立新站點。](create-site.md)

## 其他資源 {#additional-resources}

請查看這些其他資源，深入了解AEM強大功能如何搭配運作。

* [AEMas a Cloud Service技術檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已對AEM有明確的了解，建議您直接參閱深入的技術檔案。
* [網站管理檔案](/help/sites-cloud/administering/site-creation/create-site.md)  — 查看網站建立技術檔案，以取得快速網站建立工具功能的詳細資訊。
