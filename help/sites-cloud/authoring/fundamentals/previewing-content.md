---
title: 預覽內容
description: 了解如何使用AEM預覽服務在上線前預覽內容。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 7b56bb05e31d7a61d7a8fb13e2bd0ff6e4fb301d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---


# 預覽內容 {#previewing-content}

AEM提供網站預覽服務，讓開發人員和內容作者在到達發佈環境且可供公開使用之前，先預覽網站的最終體驗。

它有助於預覽原本無法從製作環境看到的頁面體驗，例如頁面轉變和其他僅發佈端內容。

如需預覽環境的詳細資訊，請參閱本檔案 [管理環境](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## 發佈要預覽的內容 {#publishing-content-to-preview}

您可以使用 **托管出版物** UI。

1. 在Sites Console中，選取您要傳送以預覽的頁面，然後按一下 **管理出版物** 按鈕
1. 在以下嚮導中，選擇 **預覽** 作為目的地

   ![托管出版物](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 按一下 **下一個**，然後 **發佈** 確認。

1. 對話方塊會顯示用於存取預覽環境中內容的URL。


或者，若要使用精靈中顯示的URL來查看預覽內容，您也可以在 `preview-` 至生產執行個體的發佈URL。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

請參閱檔案 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 以取得如何擷取環境URL的詳細資訊。

內容也可以使用 [發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow) 和 `agentId` 參數設定為 `preview` 或使用 [復寫API](/help/operations/replication.md#replication-api) 帶 `AgentFilter` 已設定為預覽。

## 從預覽中取消發佈內容 {#unpublishing-content-from-preview}

取消發佈來自 **預覽** 環境與 [取消發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) 從 **發佈** 環境。

唯一的差異是您可以選取 **目的地** 為 **預覽**.

## 更多資訊 {#further-information}

另請參閱:

* [為預覽層配置OSGi設定](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#configuring-osgi-settings-for-the-preview-tier)

* [使用開發人員控制台進行除錯預覽](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#debugging-preview-using-the-developer-console)