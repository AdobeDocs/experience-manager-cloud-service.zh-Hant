---
title: 執行管道
description: 本頁說明如何在Cloud Manager中執行Screens的管道作為Cloud Service專案。
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# 在Cloud Manager中執行Screensas a Cloud Service計畫的管道 {#run-pipeline-screens-cloud}

本節說明如何在Cloud Manager中針對您的程式執行管道和部署程式碼。

>[!NOTE]
>請參閱[設定您的CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html)和[部署您的程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)，瞭解如何在Cloud Manager中執行您程式的管道。

## 目標 {#objective}

以下章節說明如何在Cloud Manager中設定CI/CD管道並為您的方案部署程式碼。

## 在Cloud Manager中執行Screens專案管道的步驟 {#steps-branch-creation}

1. 環境設定成功完成後，您會在Cloud Manager的&#x200B;**總覽**&#x200B;頁面中看到行動號召卡更新。

   ![影像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. 從&#x200B;**總覽**&#x200B;頁面按一下&#x200B;**設定管道**。

1. 選取分支後，按一下&#x200B;**下一步**。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. 從&#x200B;**安裝管道**&#x200B;精靈中選取您的選項。 按一下「**儲存**」。

   >[!NOTE]
   >若要瞭解設定管道精靈中的選項，請參閱[從Cloud Manager設定管道設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html)以取得詳細資訊。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 設定管道完成後，會更新行動號召卡。

   >[!NOTE]
   >若要瞭解Cloud Manager中的部署階段，請參閱[部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)以取得詳細資訊。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 按一下&#x200B;**部署**。

1. 按一下&#x200B;**建置**&#x200B;以開始建置程式。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. 建置程式完成後，您可以從Cloud Manager的&#x200B;**總覽**&#x200B;頁面中的&#x200B;**環境**&#x200B;卡片看到作者連結。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 下一步 {#whats-next}

瞭解如何在Cloud Manager中設定方案的環境後，您就可以開始入門流程的下一步了：[瀏覽至Screens服務提供者](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md)。
