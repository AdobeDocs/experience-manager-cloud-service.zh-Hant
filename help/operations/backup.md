---
title: 在AEM as aCloud Service中備份和還原
description: 在AEM as aCloud Service中備份和還原
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 在AEM as aCloud Service中備份和還原


>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="備份和還原"
>abstract="AEM as aCloud Service可將客戶的完整應用程式（程式碼和內容）在過去七天內還原為特定、預定的時間，取代生產環境。 只有在程式碼或內容發生嚴重問題時，才應使用此功能。 從恢復備份到當前備份之間的最近資料將丟失。 測試環境也會還原為舊版本。"

如果發生內容或資料損毀，AEM as aCloud Service可將客戶的完整應用程式（程式碼和內容）還原為過去七天內預先決定的特定時間，取代生產環境。
如果客戶的部署（即部署的應用程式代碼已損壞或有故障），最好修復它並轉到新版本，而不是從備份中還原它。 備份的執行方式對應用程式的運行時效能沒有影響。

>[!CAUTION]
>
>只有在程式碼或內容發生嚴重問題時，才應使用此功能。 從恢復備份到當前備份之間的最近資料將丟失。 測試環境也會還原為舊版本。

## 使用方式

客戶應提交支援票證，說明所遇到的問題。 這將導致Adobe支援進行調查，由他們確定是否需要恢復。

AEM as aCloud Service支援：

* 24小時時間點恢復，這意味著系統可以在過去24小時內恢復到任何點。
* 從過去7天每天擷取一次的特定Adobe定義時間戳記進行還原。  任何復寫訊息（刪除、更新、建立）都將保留。

在所有情況下，自訂程式碼版本都會從還原點之前上次成功部署取得。

恢復時間目標(RTO)將因儲存庫的大小而異，但恢復序列開始後，作為一般准則，大約需要30分鐘。

還原後，AEM版本將更新為最新版本。

**來自已刪除環境的資料將永久丟失，且無法恢復。**
