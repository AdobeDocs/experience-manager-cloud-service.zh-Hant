---
title: 設定管道
description: 建立前端管道以管理站點主題的自定義。
exl-id: 0d77d1a6-98f3-4961-9283-f52c1b5b2a7b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# 設定管道 {#set-up-your-pipeline}

建立前端管道以管理站點主題的自定義。

## 到目前為止的故事 {#story-so-far}

在快速建立站AEM點的上一文檔中， [從模板建立站點，](create-site.md) 您學會了如何使用站點模板快速建立AEM一個可以使用前端工具進一步自定義的站點，現在您應該：

* 瞭解如何獲取網AEM站模板。
* 瞭解如何使用模板建立新站點。
* 瞭解如何從新站點下載模板以提供給前端開發人員。

本文基於這些基礎知識，因此您可以設定前端管道，前端開發人員稍後將在部署前端定制時使用該管道。

## 目標 {#objective}

本文檔幫助您瞭解前端管道以及如何建立管道來管理站點自定義主題的部署。 閱讀完後，您應：

* 瞭解前端管線是什麼。
* 瞭解如何在雲管理器中設定前端管道。

## 責任角色 {#responsible-role}

此部分路程適用於Cloud Manager管理員。

## 要求 {#requirements}

* 您需要訪問雲管理器。
* 你需要成為 **部署管理器** 角色。
* 必須在雲管AEM理器中設定環境的Git回購。
   * 通常，任何活動項目都已出現這種情況。 但是，如果不是，請參閱「Cloud Manager Repositories（Cloud Manager資料庫）」下的 [其他資源](#additional-resources) 的子菜單。

## 什麼是前端管線 {#front-end-pipeline}

前端開發涉及定制JavaScript、CSS和靜態資源，這些資源定義了站點的AEM樣式。 前端開發人員將在自己的本地環境中進行這些定制。 一旦準備好，更改將提交到AEMGit儲存庫。 但他們只提交原始碼。 他們還沒活著。

前端管道將這些已提交的自定義內容部署到AEM一個環境，通常是生產或非生產環境。

這樣，前端開發可以與具有自己部署管道的任何全堆棧後端開發分開工作AEM，並與之並行。

>[!NOTE]
>
>前端管道只能部署JavaScript、CSS和靜態資源來設定站點的AEM樣式。 無法在管道中部署網站內容（如頁面或資產）。

## 訪問雲管理器 {#login}

1. 登錄到Adobe雲管理器，位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)。

1. 雲管理器列出了各種可用程式。 點擊或按一下要管理的。 如果您只是從AEMas a Cloud Service開始，則可能只有一個程式可用。

   ![在雲管理器中選擇程式](assets/cloud-manager-select-program.png)

您現在可以看到您的程式的概述。 您的頁面看起來會有所不同，但與此示例類似。

![雲管理器概述](assets/cloud-manager-overview.png)

記下您訪問或複製URL的程式的名稱。 您以後需要將此資訊提供給前端開發人員。

## 建立前端管線 {#create-front-end-pipeline}

現在您已訪問Cloud Manager，可以建立用於前端部署的管道。

1. 在 **管線** 按一下或按一下 **添加** 按鈕

   ![管線](assets/pipelines-add.png)

1. 在 **添加** 按鈕 **添加非生產管道** 為了這趟旅程。

1. 在 **配置** 頁籤 **添加非生產管道** 對話框：
   * 選擇 **部署管道**。
   * 在中為管線提供名稱 **非生產管道名稱** 的子菜單。

   ![添加管道配置](assets/add-pipeline-configuration.png)

1. 點擊或按一下 **繼續**。

1. 在 **原始碼** 頁籤：
   * 選擇 **前端代碼** 作為要部署的代碼類型。
   * 確保在下面選擇了正確的環境 **合格的部署環境**。
   * 選擇正確的 **儲存庫**。
   * 定義 **Git分支** 管道應與關聯。
   * 定義 **代碼位置** 如果前端開發位於選定儲存庫中的特定路徑下。 預設值是儲存庫的根，但通常前端開發和後端將位於不同的路徑下。

   ![用於添加管道的原始碼資訊](assets/add-pipeline-source-code.png)

1. 點擊或按一下 **保存**。

新管線將在 **管線** 的下界。 在管線名稱后按一下省略號的輕擊可顯示選項，以便根據需要進一步編輯或查看詳細資訊。

![管線選項](assets/new-pipeline.png)

>[!TIP]
>
>如果您已熟悉AEMaaCS中的管道，並希望瞭解有關不同類型管道之間差異的詳細資訊，包括有關前端管道的進一步詳細資訊，請參閱配置CI/CD管道 — 連結在 [其他資源](#additional-resources) 的下界。

## 下一步是什麼 {#what-is-next}

現在，您已完成快速站點創AEM建過程的這一部分：

* 瞭解前端管線是什麼。
* 瞭解如何在雲管理器中設定前端管道。

在此知識基礎上構建並繼AEM續快速建立網站的過程，方法是下次查看文檔 [授予對前端開發人員的訪問權限，](grant-access.md) 在此，您將將前端開發人員裝載到Cloud Manager中，以便他們能夠訪問您的站AEM點git儲存庫和管道。

## 其他資源 {#additional-resources}

建議您通過審閱文檔進入快速站點建立過程的下一部分 [自定義網站主題，](customize-theme.md) 下面是一些附加的可選資源，這些資源對本文檔中提到的一些概念進行了更深入的瞭解，但不需要繼續旅行。

* [Cloud Manager文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您想更詳細地瞭解Cloud Manager的功能，則可能需要直接查閱深入的技術文檔。
* [Cloud Manager資料庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)  — 如果您需要有關如何為AEMaaCS項目設定和管理Git儲存庫的詳細資訊，請參閱此文檔。
* [配置CI/CD管道 — Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)  — 瞭解有關在本文檔中設定管道（完整堆棧和前端）的詳細資訊。
