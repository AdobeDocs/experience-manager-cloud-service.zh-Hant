---
title: 時間軸中的活動流
description: 本文介紹如何在時間線上顯示資產的活動日誌。
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 34%

---

# 查看活動流中的資產操作日誌 {#activity-stream-in-timeline}

此功能顯示時間線上資產的活動日誌。 如果在中執行以下與資產相關的任何操作 [!DNL Experience Manager Assets]，活動流功能將更新時間軸以反映活動。

活動流中記錄了以下操作：

* 建立
* 刪除
* 下載（包括格式副本）
* 發佈
* 未發佈
* 批准
* 拒絕
* 移動

將從儲存日誌檔案的CRX位置提取要在時 `/var/audit/com.day.cq.dam/content/dam` 間軸中顯示的活動日誌。此外，當上載新資產或修改現有資產並將其檢入時，將記錄時間線活動 [!DNL Experience Manager] 通過 [Adobe資產連結](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 或 [[!DNL Experience Manager] 案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)。

>[!NOTE]
>
>臨時工作流不會顯示在時間軸中，因為未保存這些工作流的歷史記錄資訊。

要查看活動流，請對資產執行一個或多個操作，選擇資產，然後選擇 **[!UICONTROL 時間軸]** 清單中。

<!-- ![timeline-2](assets/timeline-2.png) -->

時間軸顯示您對資產執行的操作的活動流。

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>「發佈」和「取消發佈」任 **[!UICONTROL 務的預設日]** 志存 **[!UICONTROL 儲位置為]**`/var/audit/com.day.cq.replication/content`。對於 **[!UICONTROL 移動]** ，預設位置為 `/var/audit/com.day.cq.wcm.core.page`。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
