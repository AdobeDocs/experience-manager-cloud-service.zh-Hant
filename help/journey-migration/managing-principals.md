---
title: 管理主參與者
description: 管理移轉主體，使用Admin Console
source-git-commit: 5bf497fb2122cc3d3ff0903aeb680a35e90f33b0
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# 管理主參與者 {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="管理主參與者"
>abstract="瞭解在內容移轉期間或之後管理使用者需要採取哪些動作"

在將內容轉移到AEM as a Cloud Service雲端環境之前，可以在Admin Console上執行一些任務。  它們是：建立使用者、建立群組以及將使用者指派給群組；這些使用者和群組將存在於IMS (Adobe的Identity Management服務)中，用於管理所有Adobe雲端型服務的使用者和群組。

### 在Admin Console中建立群組及其使用者

[使用AEM主體的Admin Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up)提供如何在IMS中建立使用者和群組，以及如何同時或稍後將使用者新增到群組的詳細指示。  檔案包含三個用於建立它們的選項：透過Admin Console手動建立、透過Admin Console透過CSV上傳以及透過使用者同步工具。

手動選項可讓您一次建立一個群組或使用者；CSV上傳功能可讓您一次建立和連結多個使用者和群組；使用者同步工具可讓您使用現有的IDP來建立和管理IMS使用者和群組。

當使用者使用IMS登入AEM後，將會建立該使用者的AEM表示法。  此外，使用者所在的任何IMS群組都會在AEM中建立同等的AEM群組。  這些IMS建立的AEM使用者和群組仍主要使用Admin Console來管理。

內容移轉完成後，IMS群組通常需要額外設定，使用者才能存取移轉的內容。  請參閱[移轉後移轉主體](/help/journey-migration/managing-principals-after-migration.md)

另請參閱[教學課程、AEM使用者、群組和許可權](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions)，以進一步瞭解AEM和IMS使用者和群組如何整合和管理。