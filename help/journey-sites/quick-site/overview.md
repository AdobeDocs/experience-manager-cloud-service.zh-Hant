---
title: 快速AEM建立站點
description: 從此開始，引導您瀏覽易用的AEM快速站點建立工具，以簡化站點的前端開發，並在不具備後端知識的情況下快速自AEM定義您的AEM站點。
exl-id: b8218232-0298-4b16-9dab-fa59be592a24
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 1%

---

# 快速AEM建立站點 {#quick-site-creation-journey}

從此開始，引導您瀏覽易用的AEM快速站點建立工具，以簡化站點的前端開發，並在不具備後端知識的情況下快速自AEM定義您的AEM站點。

## 簡介 {#introduction}

AEM Sites是建立和管理數字型驗的強大工具集。 內容作者可以使用站點編輯器輕鬆建立數字型驗，並使用站點控制台組織內容，同時能夠看到內容的即時性，因為內容將通過不同渠道交付AEM給您的觀眾。

「快AEM速站點建立」工具允許非開發人員使用站點模板從頭快速建立新站點。 建立網站後，「快速建立網站」工具還可以快速定制網站的主題和樣式AEM（JavaScript、CSS和靜態資源）。 這樣，前端開發人員就可以與內容建立者分AEM開工作，並與內容建立者並行。 管AEM理員只需下載網站主題，並將其提供給前端開發人員，後者使用他們喜愛的工具定制網站主題，然後將更改提交到AEM代碼儲存庫，然後進行部署。

快速站點建立工具消除了站點建立的任何開發人員知識AEM，消除了前端開發的知識要求，並允許主題開發與內容建立並行進行，從而大大加快了站點的價值實現時間，提高了站點定制和部署靈活性。

## 視頻概述 {#video-overview}

要快速瞭解此功能的使用過程， [你可以看這五分鐘的介紹。](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw)

本文檔將逐步詳細介紹視頻中的所有功能，以便您瞭解工作流，並可以在您自己的環境中重新建立該流程。

## 文檔AEM旅程 {#documentation-journeys}

[文檔旅程](/help/journey-documentation/documentation-journeys.md) 通過提供幫助讀者瞭解和解決商業問題的敘事，將許多不同的、或許複雜的主題和特徵聯繫起來AEM，讀者可以從頭到尾對商業問題有新意，但只要假設事先的主題或知AEM識很少。

文檔旅程是圍繞最佳做法原則設計的，這些原則由Adobe的最新研究、Adobe顧問的經驗證的實施經驗和客戶項目的反饋所指導。

如果您想瞭解Adobe如何推薦如何解決網站業務案例AEM,AEM Sites旅程就是起點。

## 對象 {#audience}

這一歷程列出了定制AEM Sites主題的要求、步驟和方法。 它的主要受眾是前端開發商，他們不需要任何知識AEM。 但是，為了說明整個過程，此過程涉及管理員，他們假定擁有基本的AEM Sites和雲管理器知識。 實際上，多人可以擔任多個角色，這一過程支援管理員和前端開發人員的觀點。

| 角色 | 說明 | 《旅程中的角色》 |
|---|---|---|
| 前端開發人員 | 自定義網站主題 | 獲取管理員提AEM供的主題並自定義，以便可以部署到站AEM點。 |
| 內容作者 | 建立並管理作為站點提供的內容 | 內容作者在AEM前端開發人員自定義的主題上建立內容。 |
| AEM 管理員 | 建立新網AEM站 | 管AEM理員根據模板建立新站點，然後為前端開發人員提供要自定義的主題。 |
| Cloud Manager管理員 | 建立管線並授予訪問權 | Cloud Manager管理員建立前端管道並授予前端開發人員訪問權限，以便能夠向AEMgit儲存庫提交自定義項。 |

## 快速AEM站點建立之旅 {#the-journey}

您將在此旅途中探索許多主題。 以下文章為您提供了使用快速站點建立工具建立和自AEM定義站點的基本知識，並連結到詳細的技術文檔。

|#|文章|說明|責任角色| |—|—| |0|快AEM速網站建立行程|此文檔|AEM &amp; Cloud Manager管理員| |1|[瞭解雲管理器和快速站點建立工作流](cloud-manager.md)|瞭解Cloud Manager及其如何將新的快速網站建立過程聯繫起來。|AEM管理員| |2|[從模板建立站點](create-site.md)|瞭解如何使用網站模板快AEM速建立新網站。|AEM管理員| |3|[設定管道](pipeline-setup.md)|建立前端管道以管理網站主題的自定義。|Cloud Manager管理員| |4|[授予對前端開發人員的訪問權限](grant-access.md)|將前端開發人員裝載到雲管理器中，以便他們能夠訪問您的站AEM點Git儲存庫和管道。|Cloud Manager管理員| |5|[檢索Git儲存庫訪問資訊](retrieve-access.md)|瞭解前端開發人員如何使用Cloud Manager訪問Git儲存庫資訊。|前端開發人員| |6|[自定義網站主題](customize-theme.md)|瞭解如何構建網站主題、如何自定義網站主題以及如何使用即時內容test網AEM站主題。|前端開發人員| |7|[部署您的自定義主題](deploy-theme.md)|瞭解如何使用管道部署網站主題。|前端開發人員|

## 下一步是什麼 {#what-is-next}

您現在已準備好開始Adobe快速站點建立之旅。

* 如果您是AEM或Cloud Manager管理員，或者您同時擔任前端開發人員和管理員角色，或者您只想瞭解中的端到端流程AEM，請從旅程的開始開始 [瞭解雲管理器](cloud-manager.md) 如下。
* 如果您只負責前端開發並將與Cloud Manager管理員和AEMCloud Manager管理員進行交互，則可以直接跳至 [檢索Git儲存庫訪問資訊](retrieve-access.md) 訪問AEMgit儲存庫並開始自定義。
* 如果您已經瞭解AEM Sites和雲管理器協同工作，並且希望直接從配置開始，您可以 [直接跳到從模板建立新站點。](create-site.md)

## 其他資源 {#additional-resources}

查看這些附加資源，瞭解有關功能強大的功能AEM如何協同工作的詳細資訊。

* [AEMas a Cloud Service技術文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已經對此有了確切的了AEM解，您可能需要直接咨詢深入的技術文檔。
* [站點管理文檔](/help/sites-cloud/administering/site-creation/create-site.md)  — 查看現場建立技術文檔，瞭解有關快速站點建立工具功能的詳細資訊。
