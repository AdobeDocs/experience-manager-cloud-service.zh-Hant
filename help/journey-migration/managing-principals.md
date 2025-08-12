---
title: 管理主體
description: 使用 Admin Console 管理主體以進行遷移
exl-id: a75598d0-8f59-466b-984e-dfe527388c2a
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 100%

---

# 管理主體 {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="管理主體"
>abstract="了解在內容移轉期間或之後需要完成哪些工作來管理使用者"

將內容傳輸至 AEM as a Cloud Service 雲端環境之前，有一些任務可以在 Admin Console 上執行。這些任務是：建立使用者、建立群組，以及將使用者指派至群組；這些使用者和群組將存在於 Adobe 的 Identity Management 服務中，而該服務會用於管理所有 Adobe 雲端型服務的使用者和群組。

## 在 Admin Console 中建立群組及其使用者

[使用 Admin Console 管理 AEM 主體](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up)提供詳細指示，說明如何在 IMS 中建立使用者和群組，以及如何同時或稍後將使用者新增至群組。該文件包括三個建立選項：透過 Admin Console 手動建立、透過 Admin Console 上傳 CSV，以及透過使用者同步工具。

手動選項可讓您一次建立一個群組或一位使用者；CSV 上傳可讓您同時建立和連結多個使用者與群組；使用者同步工具則可讓您使用現有的 IDP 來建立和管理 IMS 使用者與群組。

使用者透過 IMS 登入 AEM 後，便會建立該使用者的 AEM 表示方式。此外，使用者所屬的任何 IMS 群組都將具有在 AEM 中建立的同等 AEM 群組。這些 IMS 建立的 AEM 使用者和群組主要仍是透過 Admin Console 來管理。

內容遷移完成後，IMS 群組通常會需要進行一些額外的設定，以便使用者存取遷移的內容。請參閱[遷移後管理主體](/help/journey-migration/managing-principals-after-migration.md)

另請參閱[教學課程：AEM 使用者、群組和權限](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions)，以了解更多有關如何整合和管理 AEM 及 IMS 使用者與群組的資訊。
