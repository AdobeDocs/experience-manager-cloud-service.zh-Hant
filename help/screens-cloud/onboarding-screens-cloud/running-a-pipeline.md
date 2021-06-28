---
title: 執行管道
description: 本頁面說明如何在Cloud Manager中以Cloud Service專案的形式執行Screens管道。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---


# 在Cloud Manager中執行以Cloud Service程式形式顯示畫面的管道 {#run-pipeline-screens-cloud}

本節說明如何在Cloud Manager中執行管道，以及為程式部署程式的程式碼。

>[!NOTE]
>請參閱[配置CD-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en)和[部署代碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) ，了解如何在Cloud Manager中為程式運行管道。

## 目標 {#objective}

以下章節說明如何在Cloud Manager中設定CI/CD管道，以及部署程式的程式碼。

## 在Cloud Manager中為Screens專案執行管道的步驟 {#steps-branch-creation}

1. 環境設定一旦成功完成，您就會在Cloud Manager的&#x200B;**概述**&#x200B;頁面中看到動作呼叫卡更新。

   ![影像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. 按一下&#x200B;**概述**&#x200B;頁面中的「設定管道」**。**

1. 選取分支後，按一下&#x200B;**Next**。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. 從&#x200B;**設定管道**&#x200B;精靈中選取選項。 按一下&#x200B;**Save**。

   >[!NOTE]
   >若要了解「設定管道」精靈中的選項，請參閱[從Cloud Manager設定管道設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en)以取得詳細資訊。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 設定管道完成後，行動要求卡會更新，如下圖所示。 按一下部署。

   >[!NOTE]
   >若要了解Cloud Manager中的部署階段，請參閱[部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en)以取得詳細資訊。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 按一下&#x200B;**Build**&#x200B;以啟動建置程式。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. 建置程式完成後，您會從Cloud Manager的&#x200B;**概述**&#x200B;頁面，看到「**環境**」卡片中的製作連結。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 下一步 {#whats-next}

一旦您學會如何在Cloud Manager中為您的程式設定環境，現在就可以開始進行入門程式的下一個步驟，即[導覽至Screens服務提供者](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md)。