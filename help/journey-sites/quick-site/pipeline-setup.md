---
title: 設定您的管道
description: 建立前端管道以管理網站主題的自訂。
exl-id: 0d77d1a6-98f3-4961-9283-f52c1b5b2a7b
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 10%

---

# 設定您的管道 {#set-up-your-pipeline}

建立前端管道以管理網站主題的自訂。

## 到目前為止 {#story-so-far}

在AEM快速網站建立歷程的上一個檔案中， [從範本建立網站，](create-site.md) 您已瞭解如何使用網站範本快速建立可以使用前端工具進一步自訂的AEM網站，現在您應該：

* 瞭解如何取得AEM網站範本。
* 瞭解如何使用範本建立網站。
* 瞭解如何從新網站下載範本以提供給前端開發人員。

本文基於這些基礎之上，因此您可以設定前端管道，前端開發人員稍後將在歷程中使用它來部署前端自訂。

## 目標 {#objective}

本檔案可協助您瞭解前端管道，以及如何建立前端管道來管理網站自訂主題的部署。 閱讀本文件後，您應該：

* 瞭解什麼是前端管道。
* 瞭解如何在Cloud Manager中設定前端管道。

## 負責角色 {#responsible-role}

此歷程的這一部分適用於Cloud Manager管理員。

## 要求 {#requirements}

* 您需要具有對Cloud Manager的存取權。
* 您必須是 **部署管理員** Cloud Manager中的角色。
* 必須在Cloud Manager中設定AEM環境的Git存放庫。
   * 任何使用中專案通常都會如此。 但如果不是這種情況，請參閱下可用的Cloud Manager存放庫檔案 [其他資源](#additional-resources) 區段。

## 什麼是前端管道 {#front-end-pipeline}

前端開發涉及定義AEM網站樣式的JavaScript、CSS和靜態資源的自訂。 前端開發人員將在自己的本機環境中工作，以進行這些自訂。 準備就緒後，變更會提交到AEM Git存放庫。 但它們只會認可原始程式碼。 它們尚未上線。

前端管道會採用這些認可的自訂並將它們部署到AEM環境，通常是生產或非生產環境。

如此一來，前端開發可與AEM上的任何全棧疊後端開發分開及並行運作，後者有自己的部署管道。

>[!NOTE]
>
>前端管道只能部署JavaScript、CSS和靜態資源來設定AEM網站的樣式。 頁面或資產等網站內容無法在管道中部署。

## 存取 Cloud Manager {#login}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Adobe Cloud Manager。

1. Cloud Manager 列出了可用的各種計畫。點選或按一下您要管理的專案。 如果您剛開始使用AEMas a Cloud Service，則可能只有一個可用計畫。

   ![在Cloud Manager中選取計畫](assets/cloud-manager-select-program.png)

您現在可以看到方案的概觀。 您的頁面看起來會有所不同，但與此範例類似。

![Cloud Manager總覽](assets/cloud-manager-overview.png)

記下您已存取的程式名稱或複製URL。 您稍後需要將此提供給前端開發人員。

## 建立前端管道 {#create-front-end-pipeline}

現在您已存取Cloud Manager，可以為前端部署建立管道。

1. 在 **管道** 部分，點選或按一下 **新增** 按鈕。

   ![管道](assets/pipelines-add.png)

1. 在出現的彈出式選單中 **新增** 按鈕選取 **新增非生產管道** 在此歷程中。

1. 在 **設定** 的標籤 **新增非生產管道** 開啟的對話方塊：
   * 選取 **部署管道**.
   * 在下列位置為管道命名： **非生產管道名稱** 欄位。

   ![新增管道設定](assets/add-pipeline-configuration.png)

1. 點選或按一下&#x200B;**繼續**。

1. 在 **原始碼** 標籤：
   * 選取 **前端計畫碼** 作為要部署的程式碼型別。
   * 請務必在「 」底下選取正確的環境 **符合資格的部署環境**.
   * 選取正確的 **存放庫**.
   * 定義哪些 **Git分支** 管道應該有關聯性。
   * 定義 **程式碼位置** 前端開發位於所選存放庫中的特定路徑下。 預設值是存放庫的根，但前端開發和後端通常位於不同的路徑下。

   ![用於新增管道的原始碼資訊](assets/add-pipeline-source-code.png)

1. 點選或按一下&#x200B;**儲存**。

新管道建立並顯示在中 **管道** 部分。 點選並按一下管道名稱后的省略符號會顯示選項，以便視需要進一步編輯或檢視詳細資料。

![管道選項](assets/new-pipeline.png)

>[!TIP]
>
>如果您已熟悉AEMaaCS中的管道並希望詳細瞭解不同型別管道之間的差異，包括有關前端管道的更多詳細資訊，請參閱設定CI/CD管道 — 中連結的Cloud Service [其他資源](#additional-resources) 一節。

## 下一步 {#what-is-next}

現在您已完成AEM快速網站建立歷程的這一部分，您應：

* 瞭解什麼是前端管道。
* 瞭解如何在Cloud Manager中設定前端管道。

在此基礎上繼續您的AEM快速網站建立歷程，接下來檢閱檔案 [授予前端開發人員存取權，](grant-access.md) 在這裡，您會將前端開發人員帶入Cloud Manager，以便他們能夠存取您的AEM網站Git存放庫和管道。

## 其他資源 {#additional-resources}

我們建議您檢閱檔案，繼續快速網站建立歷程的下一部分 [自訂網站主題](customize-theme.md) 以下是一些其他可選資源，這些資源對本文中提到的一些概念進行了更深入的探究，但並非繼續此歷程所必需的。

* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想要直接查閱深入的技術文件。
* [Cloud Manager存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)  — 如果您需要更多有關如何為您的AEMaaCS專案設定和管理Git存放庫的資訊，請參閱本檔案。
* [設定CI/CD管道 — Cloud Service](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)  — 在本檔案中瞭解有關設定完整棧疊和前端管道的更多詳細資訊。
