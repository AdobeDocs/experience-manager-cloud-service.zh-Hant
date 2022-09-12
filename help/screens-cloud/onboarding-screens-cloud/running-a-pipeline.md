---
title: 執行管道
description: 本頁面說明如何在Cloud Manager中以Cloud Service專案的形式執行Screens管道。
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 8%

---

# 在Cloud Manager中執行Screensas a Cloud Service程式的管道 {#run-pipeline-screens-cloud}

本節說明如何在Cloud Manager中執行管道，以及部署程式的程式碼。

>[!NOTE]
>請參閱 [配置CD-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) 和 [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) 了解如何在Cloud Manager中為程式執行管道。

## 目標 {#objective}

以下章節說明如何在Cloud Manager中設定CI/CD管道，以及部署程式的程式碼。

## 在Cloud Manager中為Screens專案執行管道的步驟 {#steps-branch-creation}

1. 環境設定一旦成功完成，您就會在Cloud Manager的 **概述** 頁面。

   ![影像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. 按一下 **設定管道** 從 **概述** 頁面。

1. 按一下 **下一個** ，在選取分支後。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. 從 **設定管道** 嚮導。 按一下 **儲存**.

   >[!NOTE]
   >若要了解「設定管道」精靈中的選項，請參閱 [從Cloud Manager配置管道設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) 以取得更多詳細資訊。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 設定管道完成後，行動要求卡會更新，如下圖所示。 按一下部署。

   >[!NOTE]
   >若要了解Cloud Manager中的部署階段，請參閱 [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) 以取得更多詳細資訊。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 按一下 **建置** 來啟動建置程式。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. 建置程式完成後，您會看到 **環境** 來自Cloud Manager的資訊卡 **概述** 頁面。

   ![影像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 下一步 {#whats-next}

一旦您學習了如何在Cloud Manager中為您的程式設定環境，您現在就可以開始進行入門程式的下一個步驟，也就是， [導覽至Screens Services Provider](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
