---
title: Backup and Restore in AEM as a Cloud Service
description: Backup and Restore in AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: cac25668240a87ecbf86c4f71881310b3c3d17d2
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# 在AEMas a Cloud Service中備份和還原

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="備份和還原"
>abstract="AEM as a Cloud Service can restore a customer&#39;s full application (code and content) to specific, predetermined times in the last seven days, replacing what was on production. 只有在程式碼或內容發生嚴重問題時，才應使用此功能。 從恢復備份到當前備份之間的最近資料將丟失。 Staging will also be restored to the old version."

Should content or data corruption occur, AEM as a Cloud Service can restore a customer&#39;s full application (code and content) to specific, predetermined times in the last seven days, replacing what was on production.
如果客戶的部署（即部署的應用程式代碼已損壞或有故障），最好修復它並轉到新版本，而不是從備份中還原它。 備份的執行方式對應用程式的運行時效能沒有影響。

>[!CAUTION]
>
>只有在程式碼或內容發生嚴重問題時，才應使用此功能。 從恢復備份到當前備份之間的最近資料將丟失。 測試環境也會還原為舊版本。

## 使用方式

客戶應提交支援票證，說明所遇到的問題。 This will lead to an investigation by Adobe support who will determine if a restore is necessary.

AEMas a Cloud Service支援：

* 24小時時間點恢復，這意味著系統可以在過去24小時內恢復到任何點。
* Restore from a specific, Adobe-defined timestamp taken twice a day for the last 7 days.  任何復寫訊息（刪除、更新、建立）都將保留。

In all cases, the custom code version will be the taken from the last successful deployment before the restore point.

恢復時間目標(RTO)將因儲存庫的大小而異，但恢復序列開始後，作為一般准則，大約需要30分鐘。

還原後，AEM版本將更新為最新版本。

>[!CAUTION]
>
>來自已刪除環境的資料會永久丟失，且無法恢復。
