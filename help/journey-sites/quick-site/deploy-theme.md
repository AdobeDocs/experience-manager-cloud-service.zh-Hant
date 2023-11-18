---
title: 部署您的自訂主題
description: 了解如何使用管道部署網站主題。
exl-id: fe065972-39db-4074-a802-85895c701efd
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 17%

---

# 部署您的自訂主題 {#deploy-your-customized-theme}

了解如何使用管道部署網站主題。

## 到目前為止 {#story-so-far}

在AEM快速網站建立歷程的上一個檔案中， [自訂網站主題](customize-theme.md) 您已瞭解如何建置主題、如何自訂主題，以及如何使用即時AEM內容來測試主題，您現在應：

* 瞭解網站主題的基本結構以及如何進行編輯。
* 瞭解如何透過本機Proxy使用真實的AEM內容來測試您的主題自訂。
* 瞭解如何將變更提交至AEM Git存放庫。

您現在可以執行最後一個步驟，並使用管道來部署它們。

## 目標 {#objective}

本檔案說明如何使用管道部署主題。 閱讀本文件後，您應該：

* 瞭解如何觸發管道部署。
* 瞭解如何檢查部署狀態。

## 負責角色 {#responsible-role}

此歷程的這一部分適用於前端開發人員。

## 啟動管道 {#start-pipeline}

在將主題自訂變更認可到AEM Git存放庫後，您可以執行 [管理員建立的管道](pipeline-setup.md) 以部署變更。

1. 登入Cloud Manager [就像您擷取Git存取資訊時所做的那樣](retrieve-access.md) 並存取您的程式。 在 **概觀** 標籤，您會看到一張資訊卡 **管道**.

   ![Cloud Manager總覽](assets/cloud-manager-overview.png)

1. 選取您需要啟動的管道旁邊的省略符號。 從下拉式功能表中選取 **執行**.

   ![執行管道](assets/run-pipeline.png)

1. 在 **執行管道** 確認對話方塊，選取 **是**.

   ![確認管道執行](assets/pipeline-confirm.png)

1. 在管道清單中，狀態列表示您的管道目前正在執行。

   ![管道執行狀態](assets/pipeline-running.png)

## 檢查管道狀態 {#pipeline-status}

您可以隨時檢查管道的狀態以檢視其進度的詳細資訊。

1. 選取管道旁的省略符號。

   ![檢視管道詳細資料](assets/view-pipeline-details.png)

1. 管道詳細資料視窗會顯示管道進度的劃分。

   ![管道詳情](assets/pipeline-details.png)

>[!TIP]
>
>在管線詳細資訊視窗中，您可以選取 **下載記錄** 用於管道的任意步驟進行偵錯（如果任意步驟失敗）。 管道偵錯超出了此歷程的範圍。 請參閱下列Cloud Manager的技術檔案： [其他資源](#additional-resources) 的區段。

## 驗證已部署的自訂 {#view-customizations}

管道完成後，您可以通知管理員驗證變更。 然後，管理員將：

1. 開啟AEM編寫環境。
1. 瀏覽至 [管理員先前建立的網站。](create-site.md)
1. 編輯其中一個內容頁面。
1. 檢視套用的變更。

![變更已套用](assets/changes-applied.png)

## 歷程結尾？ {#end-of-journey}

恭喜！您已完成AEM快速網站建立歷程！ 您現在應該：

* 瞭解Cloud Manager和前端管道如何管理和部署前端自訂。
* 瞭解如何根據範本建立AEM網站，以及如何下載網站主題。
* 如何將前端開發人員上線，以便他們能夠存取AEM Git存放庫。
* 如何使用代理的AEM內容自訂和測試主題，並將這些變更提交到AEM Git。
* 如何使用管道部署前端自訂。

您現在已準備好自訂您自己的AEM網站的主題。 但在您開始使用多個前端配管建立不同的工作流程之前，請先檢閱檔案 [使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md). 它可協助您透過以下方式充分利用前端開發：

* 維護單一信任來源。
* 維護關注點分離。

AEM是一個功能強大的工具，並且有許多其他選項可供使用。 查看[其他資源章節](#additional-resources)提供的一些其他資源，以詳細了解您在此歷程中看到的功能。

## 其他資源 {#additional-resources}

以下是一些其他資源，它們對本文件提到的一些概念有更深入的探討。

* [使用網站邊欄管理您的網站主題](/help/sites-cloud/administering/site-creation/site-rail.md)  — 瞭解網站邊欄的強大功能，協助您輕鬆自訂和管理網站主題，包括下載主題來源和管理主題版本。
* [AEM as a Cloud Service 技術文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - 如果您已經對 AEM 有深入的了解，您可能想要直接查閱深入的技術文件。
* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想要直接查閱深入的技術文件。
* [角色型許可權](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Cloud Manager已預先設定角色，賦予適當許可權。 請參閱本檔案以瞭解這些角色的詳細資訊及管理方法。
* [Cloud Manager存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)  — 如果您需要更多有關如何為您的AEMaaCS專案設定和管理Git存放庫的資訊，請參閱本檔案。
* [設定CI/CD管道 — Cloud Service](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)  — 在本檔案中瞭解有關設定完整棧疊和前端管道的更多詳細資訊。
* [AEM標準網站範本](https://github.com/adobe/aem-site-template-standard)  — 這是AEM標準網站範本的GitHub存放庫。
* [AEM網站主題](https://github.com/adobe/aem-site-template-standard-theme-e2e)  — 這是AEM網站主題的GitHub存放庫。
* [npm](https://www.npmjs.com)  — 用來快速建立網站的AEM主題是以npm為基礎。
* [webpack](https://webpack.js.org)  — 用於快速建立網站的AEM主題依賴webpack。
* [建立及組織頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md)  — 如果您想要在從範本建立AEM網站後進一步自訂，本指南會詳細說明如何管理您的網站頁面。
* [如何使用封裝](/help/implementing/developing/tools/package-manager.md)  — 套件可匯入和匯出存放庫內容。 本檔案說明如何在AEM 6.5中使用套件（同樣適用於AEMaaCS）。
* [入門歷程](/help/journey-onboarding/overview.md)  — 本指南可作為您的起點，確保您的團隊已設定並可as a Cloud Service存取AEM。
* [Adobe Experience Manager Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant)  — 探索Cloud Manager檔案以取得其功能的完整詳細資訊。
* [網站管理文件](/help/sites-cloud/administering/site-creation/create-site.md) - 查看關於建立網站的技術文件，了解快速網站建立工具功能的更多詳細資訊。
* [使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)  — 本檔案說明需注意的一些事項，以便您能使用前端管道充分發揮前端開發流程的潛力。
