---
title: 執行管道
description: 本頁說明如何在Cloud Manager中以Cloud Service專案形式執行Screens管道。
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 3%

---

# 在Cloud Manager中執行Screensas a Cloud Service程式管道 {#run-pipeline-screens-cloud}

本節說明如何在Cloud Manager中執行管道並部署您的程式碼。

>[!NOTE]
>請參閱 [設定CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) 和 [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) 以瞭解如何在Cloud Manager中執行計畫的管道。

## 目標 {#objective}

以下章節說明如何在Cloud Manager中設定CI/CD管道並為您的方案部署程式碼。

## 在Cloud Manager中為Screens專案執行管道的步驟 {#steps-branch-creation}

1. 環境設定成功完成後，您會在Cloud Manager的 **概觀** 頁面。

   ![影像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. 按一下 **設定管道** 從 **概觀** 頁面。

1. 按一下 **下一個** 選取分支後。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. 從以下專案選取您的選項： **設定管道** 精靈。 按一下「**儲存**」。

   >[!NOTE]
   >若要瞭解設定管道精靈中的選項，請參閱 [從Cloud Manager配置管道設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) 以取得更多詳細資料。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 完成設定管道後，會更新召喚行動卡。

   >[!NOTE]
   >若要瞭解Cloud Manager中的部署階段，請參閱 [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) 以取得更多詳細資料。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 按一下 **部署**.

1. 按一下 **建置** 以開始建置流程。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. 建置程式完成後，您將會看到以下連結中的作者連結： **環境** 來自Cloud Manager的卡片 **概觀** 頁面。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 下一步 {#whats-next}

在您瞭解如何在Cloud Manager中為您的計畫設定環境後，就可以繼續入門流程的下一步： [瀏覽至Screens服務提供者](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
