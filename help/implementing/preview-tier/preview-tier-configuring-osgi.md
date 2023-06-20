---
title: 設定預覽階層的 OSGi 設定
description: 了解如何設定 AEM 預覽服務，以在上線前預覽內容。
exl-id: 1200bb17-8a3c-4e41-85f4-ed2334b61f69
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 93%

---

# 設定預覽階層的 OSGi 設定 {#configure-osgi-preview-tier}

AEM 提供 Sites 預覽服務，可讓開發人員和內容作者在網站到達發佈環境並正式推出之前，預覽網站的最終體驗。

這有助於預覽在作者環境中看不見的一系列體驗。例如，頁面轉換、體驗片段和其他僅發佈端的內容。

預覽階層的 OSGi 屬性值是從發佈層繼承的。但是，透過將 `service` 參數設為值 `preview`，預覽階層的值可以與發佈階層不同

>[!NOTE]
>
>有關預覽環境的更多詳細資料，請參閱文件[管理環境](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)。

## 設定預覽階層的 OSGi 設定 {#configuring-osgi-settings-for-the-preview-tier}

以下 OSGi 屬性範例確定整合端點的 URL。

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

如需詳細資訊，請參閱 OSGi 設定文件的[此節](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration)。

## 使用 Developer Console 偵錯預覽 {#debugging-preview-using-the-developer-console}

請依照以下步驟操作，以便您可以使用開發人員控制檯對預覽層進行偵錯：

* 在 [Developer Console](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) 中，選取&#x200B;**-- 全部預覽 --**&#x200B;或其名稱包含&#x200B;**預覽**&#x200B;的生產環境
* 產生預覽執行個體的相關資訊
請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md)，了解如何取得環境 URL 的更多資訊。
