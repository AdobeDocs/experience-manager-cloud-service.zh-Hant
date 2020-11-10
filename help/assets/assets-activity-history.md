---
title: 時間軸中的活動串流
description: 本文說明如何在時間軸上顯示資產的活動記錄檔。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 36%

---


# 在活動串流中檢視資產作業記錄檔 {#activity-stream-in-timeline}

此功能會在時間軸上顯示資產的活動記錄。 如果您在Adobe Experience Manager(AEM)Assets中執行下列任何資產相關作業，「活動串流」功能會更新時間軸以反映活動。

活動流中記錄了以下操作：

* 建立
* 刪除
* 下載（包括轉譯）
* 發佈
* 未發佈
* 批准
* 拒絕
* 移動

將從儲存日誌檔案的CRX位置提取要在時 `/var/audit/com.day.cq.dam/content/dam` 間軸中顯示的活動日誌。此外，當上傳新資產或修改現有資產並透過 [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) 或 [[!DNL Experience Manager] 案頭應用程式簽入AEM時，會記錄時間軸活動](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en)。

>[!NOTE]
>
>暫時性工作流程不會顯示在時間軸中，因為不會儲存這些工作流程的歷史記錄資訊。

若要檢視活動串流，請對資產執行一或多個作業，選取資產，然後從GlobalNav清單中選 **[!UICONTROL 擇]** 「時間軸」。

<!-- ![timeline-2](assets/timeline-2.png) -->

時間軸會顯示您對資產執行之作業的活動資料流。

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>「發佈」和「取消發佈」任 **[!UICONTROL 務的預設日]** 志存 **[!UICONTROL 儲位置為]**`/var/audit/com.day.cq.replication/content`。對於 **[!UICONTROL 移動]** ，預設位置為 `/var/audit/com.day.cq.wcm.core.page`。
