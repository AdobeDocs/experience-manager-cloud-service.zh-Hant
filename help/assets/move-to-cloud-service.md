---
title: 從Adobe Experience Manager 6.x移轉至雲端服務
description: 從Adobe Experience Manager 6.x移轉至雲端服務
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 以雲端服務的形式移轉至Adobe Experience Manager資產 {#move-to-assets-cloud-service}

<!-- About the need to move from previous AEM deployment to a cloud service deployment. And how does Adobe help do it OOTB?
-->

## 關於移轉工具 {#migration-tool}

<!-- 
Link back to information about the tool in the Experience Manager as a Cloud Service docs if the tool works the same for Sites and Assets. Document the Assets-specific information here.

* What is the migration tool called? Is there a branding term for it?
* How much do we want to elaborate about the Pattern Detector rules? Is there a branding term for it?
* Before migrating using the tool, is any prepping required?
* See CQ-4271901

-->

移轉工具可協助您達成下列目標：

* 將現有的工作流程模型轉換為處理可搭配Assets Compute service運作的設定檔。
* 從工作流程模型移除不支援的步驟。
* 停用工作流程啟動器。
* 在使用者確認／驗證後，在現有原始碼中合併設定。

移轉工具會在Maven模組中建立處理設定檔，使用者可透過下列兩種方式使用：

* 合併成其現有的專案。
* 將模組添加為新子模組。

移轉工具會提供其所做變更的報表，以及變更的相關資訊。

<!--  

What is the output of the tool, besides migrated content.

Give details about reports and logs of the tool. 

* How to access the report, including required permissions.
* How to read/interpret the report.
* Location of logs. How to read the logs.
* What common errors to look for. Troubleshooting for these errors.

-->

## 將內容移轉至新部署 {#content-migration-across-deployments}
