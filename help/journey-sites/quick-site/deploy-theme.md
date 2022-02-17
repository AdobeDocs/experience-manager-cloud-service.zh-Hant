---
title: 部署自定義主題
description: 瞭解如何使用管道部署站點主題。
source-git-commit: 97c7590fd7b77e78cf2d465454fac80906d37803
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 1%

---


# 部署自定義主題 {#deploy-your-customized-theme}

瞭解如何使用管道部署站點主題。

## 到目前為止的故事 {#story-so-far}

在快速建立站AEM點的上一文檔中， [自定義網站主題，](customize-theme.md) 您瞭解了主題是如何構建的、如何自定義主題以及如何使用即時內容test主題AEM，現在您應該：

* 瞭解網站主題的基本結構以及如何編輯它。
* 瞭解如何通過本地代理使用真實內容AEMtest主題自定義。
* 瞭解如何將更改提交到AEMGit儲存庫。

現在，您可以執行最後一步，並使用管道來部署它們。

## 目標 {#objective}

本文檔介紹如何使用管道部署主題。 閱讀完後，您應：

* 瞭解如何觸發管道部署。
* 請參閱如何檢查部署狀態。

## 責任角色 {#responsible-role}

這部分行程適用於前端開發商。

## 啟動管線 {#start-pipeline}

將主題自定義更改提交到AEMGit儲存庫後，可以運行 [管理員建立的管道](pipeline-setup.md) 以部署更改。

1. 登錄雲管理器 [就像你檢索git訪問資訊](retrieve-access.md) 並訪問你的程式。 在 **概述** 頁籤 **管線**。

   ![雲管理器概述](assets/cloud-manager-overview.png)

1. 點擊或按一下需要啟動的管線旁的省略號。 從下拉菜單中，選擇 **運行**。

   ![運行管道](assets/run-pipeline.png)

1. 在 **運行管道** 確認對話框，點擊或按一下 **是**。

   ![確認管道運行](assets/pipeline-confirm.png)

1. 在管道清單中，狀態列指示管道正在運行。

   ![管道運行狀態](assets/pipeline-running.png)

## 檢查管道狀態 {#pipeline-status}

您可以隨時檢查管道的狀態以查看其進度的詳細資訊。

1. 點擊或按一下管道旁的省略號。

   ![查看管道詳細資訊](assets/view-pipeline-details.png)

1. 管道詳細資訊窗口顯示管道進度的細分。

   ![管道詳細資訊](assets/pipeline-details.png)

>[!TIP]
>
>在管線詳細資訊窗口中，可點擊或按一下 **下載日誌** 如果任何步驟都會失敗，則可用於管線的任何步驟以進行調試。 調試管線超出了此行的範圍。 請參閱 [其他資源](#additional-resources) 的子菜單。

## 驗證已部署的自定義項 {#view-customizations}

管道完成後，可通知管理員驗證更改。 然後，管理員將：

1. 開啟創AEM作環境。
1. 導航到 [管理員先前建立的站點。](create-site.md)
1. 編輯其中一個內容頁面。
1. 請參閱應用的更改。

![應用的更改](assets/changes-applied.png)

## 旅程結束？ {#end-of-journey}

恭喜！ 您已完成快速AEM站點建立過程！ 您現在應該：

* 瞭解Cloud Manager和前端管道如何管理和部署前端定制。
* 瞭解如何根據模AEM板建立網站以及如何下載網站主題。
* 如何裝載前端開發人員以便他們能夠訪問AEMGit儲存庫。
* 如何使用代理內容自定義和test主AEM題，並將這些更改提交AEM到git。
* 如何使用管道部署前端定制。

您現在已準備好自定義自己網站的AEM主題。 但是，在開始使用多個前端管道建立不同的工作流之前，請查看文檔 [使用前端管道開發站點。](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 它通過以下方式幫助您充分利用前端開發：

* 保持單一的真相來源。
* 保持關注的分離。

是AEM一種強大的工具，並有許多其他選項。 簽出中的某些可用額外資源 [「其他資源」部分](#additional-resources) 瞭解您在此過程中看到的功能。

## 其他資源 {#additional-resources}

以下是一些附加資源，可對本文檔中提到的一些概念進行更深入的介紹。

* [使用站點導軌管理站點主題](/help/sites-cloud/administering/site-creation/site-rail.md)  — 瞭解「站點」欄的強大功能，幫助您輕鬆定制和管理站點主題，包括下載主題源和管理主題版本。
* [AEMas a Cloud Service技術文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已經對此有了確切的了AEM解，您可能需要直接咨詢深入的技術文檔。
* [Cloud Manager文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您想更詳細地瞭解Cloud Manager的功能，則可能需要直接查閱深入的技術文檔。
* [基於角色的權限](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html)  — 雲管理器具有預配置的具有適當權限的角色。 有關這些角色以及如何管理這些角色的詳細資訊，請參閱本文檔。
* [Cloud Manager資料庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)  — 如果您需要有關如何為AEMaaCS項目設定和管理Git儲存庫的詳細資訊，請參閱此文檔。
* [配置CI/CD管道 — Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)  — 瞭解有關在本文檔中設定管道（完整堆棧和前端）的詳細資訊。
* [標AEM準站點模板](https://github.com/adobe/aem-site-template-standard)  — 這是「標準站點」模板的GitHubAEM儲存庫。
* [網AEM站主題](https://github.com/adobe/aem-site-template-standard-theme-e2e)  — 這是網站主題的GitHubAEM儲存庫。
* [npm](https://www.npmjs.com)  — 用AEM於快速構建站點的主題基於npm。
* [網路包](https://webpack.js.org)  — 用AEM於快速構建網站的主題依賴webpack。
* [建立和組織頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md)  — 本指南詳細說明了在從模板建立網站AEM後，如果您希望進一步自定義網站的頁面，如何管理網站頁面。
* [如何使用包](/help/implementing/developing/tools/package-manager.md)  — 包允許導入和導出儲存庫內容。 本文檔介紹了如何處理6.5AEM中的包，該軟體包也適用於AEMaaCS。
* [登機之旅](/help/journey-onboarding/home.md)  — 本指南是您的出發點，可確保您的團隊已建立並能夠訪問AEMas a Cloud Service。
* [Adobe Experience Manager雲管理器文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant)  — 瀏覽Cloud Manager文檔以瞭解其功能的全部詳細資訊。
* [站點管理文檔](/help/sites-cloud/administering/site-creation/create-site.md)  — 查看現場建立技術文檔，瞭解有關快速站點建立工具功能的詳細資訊。
* [利用前端管道開發站點](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)  — 本文檔介紹了一些需要注意的注意事項，以便利用前端管道從前端開發過程中充分挖掘潛力。
