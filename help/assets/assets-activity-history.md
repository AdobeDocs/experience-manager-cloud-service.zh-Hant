---
title: 時間軸中的活動串流
description: 本文說明如何在時間軸上顯示資產的活動記錄檔。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3207151a76c51637551907d15a34f1a6b7450d02
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 24%

---


# 在活動流{#activity-stream-in-timeline}中查看資產操作日誌

此功能會在時間軸上顯示資產的活動記錄。 如果您在[!DNL Experience Manager Assets]中執行下列任何與資產相關的作業，「活動串流」功能會更新時間軸以反映活動。

活動流中記錄了以下操作：

* 建立
* 刪除
* 下載（包括轉譯）
* 發佈
* 未發佈
* 批准
* 拒絕
* 移動

將從儲存日誌檔案的CRX位置提取要在時 `/var/audit/com.day.cq.dam/content/dam` 間軸中顯示的活動日誌。此外，當上傳新資產或修改現有資產並透過[Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html)或[[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en)簽入[!DNL Experience Manager]時，會記錄時間軸活動。

>[!NOTE]
>
>暫時性工作流程不會顯示在時間軸中，因為不會儲存這些工作流程的歷史記錄資訊。

若要檢視活動串流，請對資產執行一或多個作業，選取資產，然後從GlobalNav清單中選擇&#x200B;**[!UICONTROL Timeline]**。

<!-- ![timeline-2](assets/timeline-2.png) -->

時間軸會顯示您對資產執行之作業的活動資料流。

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>「發佈」和「取消發佈」任 **[!UICONTROL 務的預設日]** 志存 **[!UICONTROL 儲位置為]**`/var/audit/com.day.cq.replication/content`。對於 **[!UICONTROL 移動]** ，預設位置為 `/var/audit/com.day.cq.wcm.core.page`。
