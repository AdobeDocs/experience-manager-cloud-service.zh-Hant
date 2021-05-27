---
title: 預覽內容
description: 了解如何使用AEM預覽服務在上線前預覽內容。
source-git-commit: 9b4ac173c55380cbc06de64677470818aa801df4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# 預覽內容{#previewing-content}

>[!NOTE]
>
>「預覽」功能是2021.5.0版的一部分，將在未來幾週逐步推出。

AEM提供網站預覽服務，其設計是讓開發人員和內容作者在到達發佈環境前，先預覽網站的最終體驗，然後才可公開使用。

它有助於預覽原本無法從製作環境看到的頁面體驗，例如頁面轉變和其他僅發佈端內容。

## 發佈內容以預覽{#publishing-content-to-preview}

您可以使用Managed Publication UI將內容發佈至預覽服務，如下所示：

1. 選擇要在站點控制台中進行預覽的要發送的頁面，然後按一下&#x200B;**管理出版物**&#x200B;按鈕
1. 在以下嚮導中，選擇&#x200B;**預覽**&#x200B;作為目標

   ![托管出版物](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 按一下&#x200B;**Next**，然後按一下&#x200B;**Publish**&#x200B;以確認。

請參閱預覽內容，將&#x200B;**preview**&#x200B;附加至生產執行個體的發佈URL。 URL的建構方式如下：

```
https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
```

請參閱[管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) ，以取得如何取得環境URL的詳細資訊。

