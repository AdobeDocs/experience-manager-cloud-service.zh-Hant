---
title: 預覽內容
description: 瞭解如何使用AEM預覽服務在內容上線前進行預覽。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: a9a2362903e8eec25393e2ceb307814e1a21f142
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 4%

---


# 預覽內容 {#previewing-content}

AEM提供Sites預覽服務，可讓開發人員和內容作者在網站到達發佈環境並公開使用之前，預覽網站的最終體驗。

它有助於預覽從製作環境看不到的頁面體驗，例如頁面轉變和其他僅發佈端的內容。

>[!NOTE]
>
>由於內容是&#x200B;*已發佈至預覽環境*，因此可透過URL存取(因此不需要存取AEM)。

如需有關預覽環境的更多詳細資訊，請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)。

## 發佈內容以預覽 {#publishing-content-to-preview}

您可以使用&#x200B;**Managed Publication** UI將內容發佈到預覽服務。

1. 在Sites主控台中，選取您要傳送給預覽的一或多個頁面，然後按一下&#x200B;**管理出版物**&#x200B;按鈕。
1. 在下列精靈中，選取&#x200B;**預覽**&#x200B;作為目的地。

   ![受管理的出版物](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 按一下[下一步]****，然後按一下[Publish]**進行確認。**

1. 對話方塊將顯示用於在預覽環境中存取內容的URL。

   >[!NOTE]
   >
   >由於內容是&#x200B;*已發佈至預覽環境*，因此可透過URL存取(因此不需要存取AEM)。

除了使用精靈中顯示的URL檢視預覽內容之外，您還可以將`preview-`加到生產執行個體的發佈URL前面。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

如需有關如何為您的環境擷取URL的詳細資訊，請參閱檔案[管理環境](/help/implementing/cloud-manager/manage-environments.md)。

也可以使用[發佈內容樹狀工作流程](/help/operations/replication.md#publish-content-tree-workflow)並將`agentId`引數設定為`preview`，或使用[復寫API](/help/operations/replication.md#replication-api)並將`AgentFilter`設定為預覽，將內容發佈到預覽。

## 從預覽中取消發佈內容 {#unpublishing-content-from-preview}

從您的&#x200B;**預覽**&#x200B;環境中取消發佈內容基本上與從&#x200B;**Publish**&#x200B;環境中[取消發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)的程式相同。

唯一的差異是您可以選取&#x200B;**目的地**&#x200B;為&#x200B;**預覽**。
