---
title: 預覽內容
description: 了解如何使用AEM預覽服務在上線前預覽內容。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: c30470b321a4fba8c8de9becb62c518faff05498
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 預覽內容 {#previewing-content}

>[!NOTE]
>
>「預覽」功能是2021.5.0版的一部分，將在未來幾週逐步推出。

AEM提供網站預覽服務，其設計是讓開發人員和內容作者在到達發佈環境前，先預覽網站的最終體驗，然後才可公開使用。

它有助於預覽原本無法從製作環境看到的頁面體驗，例如頁面轉變和其他僅發佈端內容。

## 發佈要預覽的內容 {#publishing-content-to-preview}

您可以使用Managed Publication UI將內容發佈至預覽服務，如下所示：

1. 選擇要在站點控制台中發送以預覽的頁面，然後按一下&#x200B;**管理出版物**&#x200B;按鈕
1. 在以下嚮導中，選擇&#x200B;**預覽**&#x200B;作為目標

   ![托管出版物](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 按一下&#x200B;**Next**，然後按一下&#x200B;**Publish**&#x200B;以確認。

1. 對話方塊會顯示用於存取預覽環境中內容的URL。

   或者，若要查看預覽內容，您也可以將&#x200B;**preview**&#x200B;附加至生產執行個體的發佈URL。

   URL的建構方式如下：

   ```
   https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
   ```

請參閱[管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) ，以取得如何取得環境URL的詳細資訊。

也可以使用將agentId參數設定為預覽的[發佈內容樹工作流](/help/operations/replication.md#publish-content-tree-workflow)，或使用[複製API](/help/operations/replication.md#replication-api)並配置為預覽的AgentFilter，來發佈內容以預覽。

## 為預覽層配置OSGi設定 {#configuring-osgi-settings-for-the-preview-tier}

預覽層的OSGI屬性值繼承自發佈層，但可使用環境特定值來設定具有「預覽」值的服務參數，從發佈層區分預覽層值。 以下是決定整合端點URL的OSGI屬性範例：

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

如需詳細資訊，請參閱OSGi設定檔案的[本區段](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration)。

## 使用開發人員控制台進行除錯預覽 {#debugging-preview-using-the-developer-console}

請依照下列步驟，使用「開發人員控制台」對預覽層層除錯：

* 在[開發人員控制台](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)中，選擇&#x200B;**— 所有預覽 —**&#x200B;或名稱中包含&#x200B;**prev**&#x200B;的生產環境
* 生成預覽實例的相關資訊
請參閱[管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) ，以取得如何取得環境URL的詳細資訊。
