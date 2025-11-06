---
title: 新增Edge Delivery管道
description: 瞭解如何新增Edge Delivery管道以建置計畫碼並將其部署到生產環境。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
hide: false
index: false
hidefromtoc: false
exl-id: 5ad342fa-dd71-4105-a9cb-2d999d402780
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 14%

---

# 新增Edge Delivery管道 {#configure-production-pipeline}

<!--badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket" -->

瞭解如何設定Edge Delivery管道以建置計畫碼並將其部署到生產環境。 Edge Delivery管道可讓您設定功能，包括記錄轉送和Adobe管理的CDN。

如需支援的組態清單，請參閱[使用組態管道 — 支援的組態](/help/operations/config-pipeline.md#configurations)。

使用者必須擁有&#x200B;**[部署管理員](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能設定生產管道。

>[!IMPORTANT]
>
>在下列情況發生之前，無法設定Edge Delivery管道：
>
>* 已建立包含一個Edge Delivery Services網站和一個對應網域的計畫。 否則，稱為「**新增Edge Delivery管道**」的選項在使用者介面中會顯示為停用，工具提示會說明缺少的需求。 請參閱[在Cloud Manager中建立Edge Delivery網站](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)
>* Git存放庫至少有一個分支。 請參閱[在Cloud Manager中管理存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)。
>* 生產和中繼環境隨即建立。 請參閱[ CI/CD管道簡介](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

<!-- CMGR‑69680 -->

開始部署程式碼之前，請從[!UICONTROL Cloud Manager]設定您的管道設定。

>[!NOTE]
>
>您可在初始設定後[編輯管道設定](managing-pipelines.md)。

**若要新增Edge Delivery管道：**

1. 在[experience.adobe.com](https://experience.adobe.com)登入Cloud Manager。
1. 在「**快速存取**」區段中，按一下「**Experience Manager**」。
1. 在左側面板中，按一下「**Cloud Manager**」。
1. 選取您想要的組織。
1. 在「**我的程式**」控制台中，按一下某個程式。

   在Cloud Manager中![我的方案頁面](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. 執行下列任一項作業：

   * **從管道卡新增Edge Delivery管道**

      1. 在左側邊欄的&#x200B;**方案**&#x200B;下，按一下&#x200B;**![總覽圖示](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) [總覽](/help/implementing/cloud-manager/navigation.md#my-programs)**。
      1. 在&#x200B;**方案總覽**&#x200B;頁面的&#x200B;**管道**&#x200B;卡片下，按一下&#x200B;**![加號](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)新增**，然後選取&#x200B;**新增Edge Delivery管道**。

         ![計畫總覽頁面上的管道卡](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

         >[!TIP]
         >
         >除了使用如上述熒幕擷圖所示的&#x200B;**管道**&#x200B;卡之外，您還可以從&#x200B;**管道**&#x200B;頁面管理您的管道。
         >
         >![Edge Delivery 管道小工具顯示管道名稱、狀態、存放庫和分支](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

   * **從管道頁面新增Edge Delivery管道**

      1. 在左側邊欄中的&#x200B;**方案**&#x200B;下方，按一下&#x200B;**![工作流程圖示或管道圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg)管道**。
      1. 在管道頁面右上角附近，按一下&#x200B;**新增管道** > **新增Edge Delivery管道**。

         ![具有新增管道按鈕的管道頁面](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

         >[!TIP]
         >
         >在左上角附近，按一下「**篩選器**」，然後在「**傳遞型別**」區段下方，選取「**Edge傳遞**」核取方塊，將清單篩選為僅限Edge Delivery管道(也就是使用Edge Delivery Services的管道)。<!-- (CMGR-69682) -->
         >
         >![篩選器面板顯示新的傳遞類型包括邊緣傳遞與發佈傳遞](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

1. 在&#x200B;**新增Edge Delivery管道**&#x200B;對話方塊的&#x200B;**管道名稱**&#x200B;文字欄位中，輸入描述性管道標籤。

   ![新增Edge Delivery管道對話方塊](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. 選取您想要的管道&#x200B;**部署觸發程式**&#x200B;選項。

   * **手動** — 您開始部署。
   * **在Git變更上** - Git認可會自動啟動部署。 如有必要，使用此選項仍可手動啟動管道。

1. 按一下「**繼續**」。

1. 在&#x200B;**Source程式碼**&#x200B;底下，設定下列選項：

   * **部署環境** — 顯示目標環境欄位；保持唯讀。

   * **存放庫** — 使用下拉式清單，將管道指向儲存Edge Delivery設定的確切Git存放庫。

     另請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，瞭解如何在Cloud Manager中新增和管理存放庫。

   * **Git分支** — 使用下拉式清單選取所選存放庫中的特定分支。 如有必要，請按一下[回收]圖示或[重新整理]圖示![，在最近的推播之後重新載入Git分支下拉式清單。](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg)
   * **程式碼位置** — 定義存放庫中的資料夾路徑，管道就緒的程式碼會在此存放庫開始（ `/`等於存放庫根目錄）。

   ![設定管道](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. 按一下&#x200B;**儲存**。

您現在可以從[方案總覽](managing-pipelines.md)頁面上的&#x200B;**管道**&#x200B;卡或從&#x200B;**管道**&#x200B;頁面&#x200B;**管理您的管道**。


![Edge Delivery 管道小工具顯示管道名稱、狀態、存放庫和分支](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)



