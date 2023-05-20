---
title: 預覽內容
description: 瞭解如何使用預AEM覽服務在上線前預覽內容。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 7b56bb05e31d7a61d7a8fb13e2bd0ff6e4fb301d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 7%

---


# 預覽內容 {#previewing-content}

提AEM供站點預覽服務，讓開發人員和內容作者在網站到達發佈環境並公開提供之前預覽其最終體驗。

它便於預覽在作者環境中無法看到的頁面體驗，如頁面過渡和僅發佈端內容。

有關預覽環境的詳細資訊，請參閱文檔 [管理環境](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)。

## 發佈內容以預覽 {#publishing-content-to-preview}

您可以使用 **托管發佈** UI。

1. 在「站點」控制台中，選擇要發送至預覽的頁面，然後按一下 **管理發布** 按鈕
1. 在以下嚮導中，選擇 **預覽** 作為目標

   ![托管出版物](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 按一下 **下一個**，然後 **發佈** 確認。

1. 對話框將顯示用於訪問預覽環境中內容的URL。


或者，使用嚮導中顯示的URL查看預覽內容，還可以預先 `preview-` 到生產實例的發佈URL。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

查看文檔 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 的子菜單。

也可以通過使用 [發佈內容樹工作流](/help/operations/replication.md#publish-content-tree-workflow) 和 `agentId` 參數設定為 `preview` 或使用 [複製API](/help/operations/replication.md#replication-api) 和 `AgentFilter` 已配置為預覽。

## 從預覽中取消發佈內容 {#unpublishing-content-from-preview}

正在從您的 **預覽** 環境與 [取消發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) 從 **發佈** 環境。

唯一的區別是， **目標** 要 **預覽**。

## 更多資訊 {#further-information}

另請參閱:

* [設定預覽階層的 OSGi 設定](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#configuring-osgi-settings-for-the-preview-tier)

* [使用 Developer Console 偵錯預覽](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#debugging-preview-using-the-developer-console)