---
title: 部署您的自訂主題
description: 了解如何使用管道部署網站主題。
exl-id: fe065972-39db-4074-a802-85895c701efd
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 100%

---

# 部署您的自訂主題 {#deploy-your-customized-theme}

{{traditional-aem}}

了解如何使用管道部署網站主題。

## 目前進度 {#story-so-far}

在 AEM 快速建立網站歷程的上一份文件「[自訂網站主題](customize-theme.md)」中，您已了解建置主題的方式、如何自訂主題以及如何使用即時 AEM 內容對主題進行測試，現在您應該：

* 了解網站主題的基本結構以及如何編輯。
* 了解如何透過本機 Proxy 測試使用真實 AEM 內容的主題自訂內容。
* 了解如何將變更提交至 AEM Git 存放庫。

現在您可以執行最後一步並使用管道來部署它們。

## 目標 {#objective}

本文件說明如何使用管道部署主題。閱讀本文件後，您應該：

* 了解如何觸發管道部署。
* 了解如何檢查部署狀態。

## 負責角色 {#responsible-role}

歷程的這個部分適用於前端開發人員。

## 啟動管道 {#start-pipeline}

將主題自訂變更提交至 AEM Git 儲存庫後，您可以執行[管理員建立的管道](pipeline-setup.md)來部署變更。

1. 登入 Cloud Manager，[如同您擷取 Git 存取資訊時所做](retrieve-access.md)並存取您的方案。在「**概觀**」標籤上，您會看到一張「**管道**」的卡片。

   ![Cloud Manager 概觀](assets/cloud-manager-overview.png)

1. 選取需要啟動的管道旁邊的省略號。在下拉式選單中選取「**執行**」。

   ![執行管道](assets/run-pipeline.png)

1. 在「**執行管道**」確認對話框中，選取「**是**」。

   ![確認管道執行](assets/pipeline-confirm.png)

1. 在管道清單中，狀態欄表示您的管道現在正在執行。

   ![管道執行狀態](assets/pipeline-running.png)

## 檢查管道狀態 {#pipeline-status}

您可以隨時查看管道的狀態，以了解其進度的詳細資訊。

1. 選擇管道旁邊的省略號。

   ![檢視管道詳細資訊](assets/view-pipeline-details.png)

1. 管道詳細資訊視窗顯示管道進度的細目。

   ![管道詳細資訊](assets/pipeline-details.png)

>[!TIP]
>
>在管道詳細資訊視窗中，若有任何步驟執行失敗，您可以基於除錯目的針對管道任何步驟選取「**下載記錄**」。管道除錯超出此歷程的範圍。請參閱本頁面「[其他資源](#additional-resources)」區段來查看 Cloud Manager 的技術文件。

## 驗證已部署的自訂內容 {#view-customizations}

管道完成後，您可以通知管理員驗證變更。然後管理員將：

1. 開啟 AEM 製作環境。
1. 瀏覽至[管理員之前建立的網站](create-site.md)。
1. 編輯其中一個內容頁面。
1. 查看所套用的變更。

![已套用變更](assets/changes-applied.png)

## 歷程結尾？ {#end-of-journey}

恭喜！您已完成 AEM 快速建立網站歷程！您現在應該：

* 了解 Cloud Manager 和前端管道如何管理和部署前端自訂內容。
* 了解如何根據範本建立 AEM 網站以及如何下載網站主題。
* 前端開發人員如何上線，以便他們可以存取 AEM Git 存放庫。
* 如何使用 Proxy 處理的 AEM 內容來自訂和測試主題並將這些變更提交到 AEM Git。
* 如何使用管道部署前端自訂內容。

現在您已準備好自訂自己的 AEM 網站主題。但是，在開始使用多個前端管道建立不同的工作流程之前，請先檢閱文件「[使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)」。它可以透過以下方式幫助您充分利用前端開發：

* 維持單一真實來源。
* 將不同的關注事項分開處理。

AEM 是一個強大的工具並有許多其他選項可用。查看[其他資源區段](#additional-resources)提供的一些其他資源，以詳細了解您在此歷程中看到的功能。

## 其他資源 {#additional-resources}

以下是一些其他資源，它們對本文件提到的一些概念有更深入的探討。

* [使用網站邊欄管理您的網站主題](/help/sites-cloud/administering/site-creation/site-rail.md) - 了解網站邊欄的強大功能，幫助您輕鬆自訂和管理網站主題，包括下載主題來源和管理主題版本。
* [AEM as a Cloud Service 技術文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - 如果您已經對 AEM 有深入的了解，您可能想直接查閱深入的技術文件。
* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想直接查閱深入的技術文件。
* [角色型權限](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Cloud Manager 已預先設定角色並授予適當權限。有關這些角色以及如何管理它們的詳細資訊，請參閱本文件。
* [Cloud Manager 存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md) - 如果您需要有關如何為 AEMaaCS 專案設定和管理 Git 存放庫的更多資訊，請參閱此文件。
* [設定 CI/CD 管道 - 雲端服務](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) - 在本文件中了解更多關於設定全堆疊管道與前端管道的詳細資訊。
* [AEM 標準網站範本](https://github.com/adobe/aem-site-template-standard) - 這是 AEM 標準網站範本的 GitHub 存放庫。
* [AEM 網站主題](https://github.com/adobe/aem-site-template-standard-theme-e2e)- 這是 AEM 網站主題的 GitHub 存放庫。
* [npm](https://www.npmjs.com) - 用於快速建立網站的 AEM 主題以 npm 為基礎。
* [webpack](https://webpack.js.org) - 用於快速建立網站的 AEM 主題以 webpack 為基礎。
* [組織頁面](/help/sites-cloud/authoring/sites-console/organizing-pages.md) - 本指南詳細介紹如何組織 AEM 網站的頁面。
* [建立頁面](/help/sites-cloud/authoring/sites-console/creating-pages.md) - 本指南詳細介紹如何為您的網站新增頁面。
* [管理頁面](/help/sites-cloud/authoring/sites-console/managing-pages.md) - 本指南詳細介紹如何管理網站頁面，包括移動、複製和刪除。
* [如何使用套件](/help/implementing/developing/tools/package-manager.md) - 套件允許匯入和匯出存放庫內容。本文件說明如何使用 AEM 6.5 的套件，同樣適用於 AEMaaCS。
* [上線歷程](/help/journey-onboarding/overview.md) - 本指南可作為您的起點，確保您的團隊已設定完成並可存取 AEM as a Cloud Service。
* [Adobe Experience Manager Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) - 瀏覽 Cloud Manager 文件以了解其功能的完整詳細資訊。
* [網站管理文件](/help/sites-cloud/administering/site-creation/create-site.md) - 查看關於建立網站的技術文件，了解快速建立網站工具功能的更多詳細資訊。
* [使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) - 本文件說明一些需留意的考量事項，以便您可以使用前端管道充分發揮前端開發流程的潛力。
