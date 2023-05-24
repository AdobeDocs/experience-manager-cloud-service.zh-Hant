---
title: 時間軸中的活動資料流
description: 本文說明如何在時間軸上顯示資產的活動記錄。
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 34%

---

# 在活動資料流中檢視資產操作記錄 {#activity-stream-in-timeline}

此功能會在時間軸上顯示資產的活動記錄。 如果您在中執行下列任何資產相關作業 [!DNL Experience Manager Assets]，活動資料流功能會更新時間軸以反映活動。

活動資料流中會記錄下列作業：

* 建立
* 刪除
* 下載（包括轉譯）
* 發佈
* 未發佈
* 批准
* 拒絕
* 移動

將從儲存日誌檔案的CRX位置提取要在時 `/var/audit/com.day.cq.dam/content/dam` 間軸中顯示的活動日誌。此外，上傳新資產或修改現有資產並簽入時，會記錄時間軸活動 [!DNL Experience Manager] 透過 [Adobe資產連結](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 或 [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>暫時性工作流程不會顯示在時間軸中，因為沒有為這些工作流程儲存歷史記錄資訊。

若要檢視活動資料流，請在資產上執行一或多個作業、選取資產，然後選擇 **[!UICONTROL 時間表]** 從GlobalNav清單。

<!-- ![timeline-2](assets/timeline-2.png) -->

時間軸會顯示您對資產執行之作業的活動資料流。

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
