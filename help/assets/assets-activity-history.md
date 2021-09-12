---
title: 時間軸中的活動資料流
description: 本文說明如何在時間軸上顯示資產的活動記錄。
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 24%

---

# 在活動資料流中檢視資產作業記錄 {#activity-stream-in-timeline}

此功能會顯示時間軸上資產的活動記錄。 如果您在[!DNL Experience Manager Assets]中執行下列任何資產相關操作，活動資料流功能會更新時間軸以反映活動。

活動資料流中記錄下列操作：

* 建立
* 刪除
* 下載（包括轉譯）
* 發佈
* 未發佈
* 批准
* 拒絕
* 移動

將從儲存日誌檔案的CRX位置提取要在時 `/var/audit/com.day.cq.dam/content/dam` 間軸中顯示的活動日誌。此外，當上傳新資產或修改現有資產並透過[Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html)或[[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)簽入[!DNL Experience Manager]時，會記錄時間軸活動。

>[!NOTE]
>
>時間軸中不會顯示暫時性工作流程，因為不會儲存這些工作流程的歷史資訊。

若要檢視活動資料流，請對資產執行一或多個操作，選取資產，然後從GlobalNav清單中選擇&#x200B;**[!UICONTROL 時間軸]**。

<!-- ![timeline-2](assets/timeline-2.png) -->

時間軸會顯示您對資產執行之作業的活動資料流。

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>「發佈」和「取消發佈」任 **[!UICONTROL 務的預設日]** 志存 **[!UICONTROL 儲位置為]**`/var/audit/com.day.cq.replication/content`。對於 **[!UICONTROL 移動]** ，預設位置為 `/var/audit/com.day.cq.wcm.core.page`。
