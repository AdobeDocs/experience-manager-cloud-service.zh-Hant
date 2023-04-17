---
title: 為預覽層配置OSGi設定
description: 了解如何設定AEM預覽服務以在上線前預覽內容。
source-git-commit: 7b56bb05e31d7a61d7a8fb13e2bd0ff6e4fb301d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# 為預覽層配置OSGi設定 {#configure-osgi-preview-tier}

AEM提供網站預覽服務，讓開發人員和內容作者在到達發佈環境且可供公開使用之前，先預覽網站的最終體驗。

它有助於預覽從製作環境中看不到的體驗範圍。 例如，頁面轉變、體驗片段，以及其他僅發佈端內容。

預覽層級的OSGi屬性值繼承自發佈層級。 不過，透過設定 `service` 參數 `preview`.

>[!NOTE]
>
>如需預覽環境的詳細資訊，請參閱本檔案 [管理環境。](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## 為預覽層配置OSGi設定 {#configuring-osgi-settings-for-the-preview-tier}

下列OSGi屬性的範例決定整合端點的URL。

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

如需詳細資訊，請參閱 [本節](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration) 填入OSGi設定檔案。

## 使用開發人員控制台進行除錯預覽 {#debugging-preview-using-the-developer-console}

請依照下列步驟，使用「開發人員控制台」對預覽層層除錯：

* 在 [開發人員控制台](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)選取 **— 全部預覽 —** 或生產環境，包括 **prev** 在
* 生成預覽實例的相關資訊請參閱 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 以取得環境URL的詳細資訊。
