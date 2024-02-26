---
title: 預覽內容
description: 瞭解如何使用AEM預覽服務在內容上線前進行預覽。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 9%

---


# 預覽內容 {#previewing-content}

AEM提供Sites預覽服務，可讓開發人員和內容作者在網站到達發佈環境並公開使用之前，預覽網站的最終體驗。

它有助於預覽從製作環境看不到的頁面體驗，例如頁面轉變和其他僅發佈端的內容。

>[!NOTE]
>
>由於內容為 *已發佈* 對於預覽環境，它可透過URL存取(因此不需要存取AEM)。

如需有關預覽環境的更多詳細資訊，請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)。

## 發佈內容以預覽 {#publishing-content-to-preview}

您可以使用將內容發佈到預覽服務 **受管理的出版物** UI。

1. 在Sites Console中，選取您要傳送以預覽的一個或多個頁面，然後按一下 **管理發布** 按鈕。
1. 在下列精靈中，選取 **預覽** 作為目的地。

   ![受管理的出版物](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 按一下 **下一個**，然後 **發佈** 以確認。

1. 對話方塊將顯示用於在預覽環境中存取內容的URL。

   >[!NOTE]
   >
   >由於內容為 *已發佈* 對於預覽環境，它可透過URL存取(因此不需要存取AEM)。

除了使用精靈中顯示的URL檢視預覽內容之外，您還可以在 `preview-` 至生產執行個體的發佈URL。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

檢視檔案 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 有關如何為您的環境擷取URL的詳細資訊。

也可以使用發佈內容以進行預覽 [發佈內容樹狀工作流程](/help/operations/replication.md#publish-content-tree-workflow) 使用 `agentId` 引數設為 `preview` 或透過使用 [復寫API](/help/operations/replication.md#replication-api) 具有 `AgentFilter` 已設定預覽。

## 從預覽中取消發佈內容 {#unpublishing-content-from-preview}

正在取消發佈您的內容 **預覽** 環境基本上與相同的流程 [取消發佈頁面](/help/sites-cloud/authoring/sites-console/publishing-pages.md#unpublishing-pages) 從 **發佈** 環境。

唯一的區別是您可以選取 **目的地** 成為 **預覽**.

## 更多資訊 {#further-information}

另請參閱：

* [設定預覽階層的 OSGi 設定](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#configuring-osgi-settings-for-the-preview-tier)

* [使用 Developer Console 偵錯預覽](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#debugging-preview-using-the-developer-console)