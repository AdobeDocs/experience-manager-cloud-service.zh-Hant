---
title: 執行管道
description: 本頁說明如何在Cloud Manager中以Cloud Service專案形式執行Screens管道。
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# 在Cloud Manager中執行Screensas a Cloud Service程式管道 {#run-pipeline-screens-cloud}

本節說明如何在Cloud Manager中執行管道並為您的程式部署程式碼。

>[!NOTE]
>另請參閱 [設定CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) 和 [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) 以瞭解如何在Cloud Manager中執行方案的管道。

## 目標 {#objective}

以下章節說明如何在Cloud Manager中設定CI/CD管道並為您的方案部署計畫碼。

## 在Cloud Manager中為Screens專案執行管道的步驟 {#steps-branch-creation}

1. 環境設定成功完成後，您會在Cloud Manager的 **概觀** 頁面。

   ![影像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. 按一下 **設定管道** 從 **概觀** 頁面。

1. 按一下 **下一個** 選取分支後。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. 從以下位置選擇您的選項： **設定管道** 精靈。 按一下「**儲存**」。

   >[!NOTE]
   >若要瞭解設定管道精靈中的選項，請參閱 [從Cloud Manager設定管道設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) 以取得更多詳細資料。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 設定管道完成後，會更新行動號召卡。

   >[!NOTE]
   >若要瞭解Cloud Manager中的部署階段，請參閱 [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) 以取得更多詳細資料。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 按一下 **部署**.

1. 按一下 **建置** 以開始建置流程。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. 建置流程完成後，您可以從 **環境** 來自Cloud Manager的卡片 **概觀** 頁面。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 下一步 {#whats-next}

瞭解如何在Cloud Manager中為您的方案設定環境後，您就可以開始入門流程的下一個步驟了： [瀏覽至Screens服務提供者](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
