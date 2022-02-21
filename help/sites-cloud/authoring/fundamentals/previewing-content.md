---
title: 預覽內容
description: 瞭解如何使用預AEM覽服務在上線前預覽內容。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: e70e6ee055c2542752e66e53aa70a9378b1bc5c0
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 預覽內容 {#previewing-content}

提AEM供站點預覽服務，讓開發人員和內容作者在網站到達發佈環境並公開提供之前預覽其最終體驗。

它便於預覽在作者環境中無法看到的頁面體驗，如頁面過渡和僅發佈端內容。

有關預覽環境的詳細資訊，請參閱文檔 [管理環境。](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)。

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

## 為預覽層配置OSGi設定 {#configuring-osgi-settings-for-the-preview-tier}

預覽層的OSGi屬性值從發佈層繼承。 但是，通過設定 `service` 參數到值 `preview`。 OSGi屬性的以下示例確定整合終結點的URL。

```
[
{
"name":"INTEGRATION_URL",
"type":"string",
"value":"http://s2.integrationvendor.com",
"service": "preview"
}
]
```

有關詳細資訊，請參見 [此部分](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration) OSGi配置文檔的。

## 使用開發人員控制台調試預覽 {#debugging-preview-using-the-developer-console}

按照以下步驟使用Developer Console調試預覽層：

* 在 [開發人員控制台](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)選擇 **— 所有預覽 —** 或包括 **前** 以
* 生成預覽實例的相關資訊請參閱 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 的子菜單。
