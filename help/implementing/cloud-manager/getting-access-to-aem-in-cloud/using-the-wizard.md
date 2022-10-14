---
title: 專案建立精靈
description: 了解專案建立精靈，以幫助您在建立生產計畫後快速設定專案。
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
source-git-commit: 93cb0ffa87f2338518c2a23de4e0a692031e1a71
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 100%

---

# 專案建立精靈 {#project-creation-wizard}

建立生產計畫後，Cloud Manger 會提供一個精靈根據 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)來建立最小的 AEM 專案，以便您快速開始。

請按照下列步驟，使用精靈在 Cloud Manager 中建立 AEM 應用計劃專案。

1. 按照[建立生產計畫](creating-production-programs.md)文件中的步驟建立生產計畫

1. 計畫設定完成後，存取計畫的&#x200B;**總覽**&#x200B;畫面，然後在頂端查看&#x200B;**建立分支和專案**&#x200B;召喚行動卡。

   ![精靈的召喚行動卡](assets/create-wizard1.png)

1. 按一下&#x200B;**建立**&#x200B;以啟動精靈，並在&#x200B;**建立分支和專案**&#x200B;視窗確認您的專案&#x200B;**標題**&#x200B;和&#x200B;**新分支名稱**。

   ![建立分支和專案](assets/create-wizard2.png)

1. 或者，按一下分隔線以顯示專案的其他參數。預設值由 AEM Project Archetype 提供，通常不需要變更。

   ![其他專案參數](assets/create-wizard5.png)

1. 按一下&#x200B;**「建立」**，以開始專案建立計畫。


**正在建立專案**&#x200B;卡會取代&#x200B;**建立分支和專案**&#x200B;召喚行動卡，成為&#x200B;**計畫總覽**&#x200B;畫面的頂端。

![正在建立專案](assets/create-wizard3.png)

計畫建立完後，**新增環境**&#x200B;卡會取代&#x200B;**計畫總覽**&#x200B;畫面頂端的&#x200B;**正在建立專案**&#x200B;卡。

![新增環境](assets/create-wizard4.png)

現在，您已將根據 AEM 原型的 AEM 專案新增到您的 Git 存放庫中，作為您專案開發的基礎。接下來，您可以建立能部署專案計劃碼的環境。

若要了解如何新增或管理環境的詳細資訊，請參閱文件：[管理您的環境](/help/implementing/cloud-manager/manage-environments.md)。

>[!NOTE]
>
>該精靈僅適用於生產計畫。因為[沙箱計畫](introduction-sandbox-programs.md#auto-creation)包括自動建立專案，而精靈不是必要的。