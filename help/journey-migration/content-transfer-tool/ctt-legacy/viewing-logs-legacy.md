---
title: 在內容傳輸工具（舊版）中查看遷移集的日誌
description: 在內容傳輸工具中查看遷移集的日誌
hide: true
hidefromtoc: true
exl-id: 01c8afd3-c594-4a41-b905-8c3a2d74db6f
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 74%

---

# 查看遷移集的日誌（舊版） {#view-logs-content-transfer-tool}

完成每個步驟（提取和攝取）後，檢查日誌並查找錯誤。  如有任何錯誤應立即處理，方法是處理回報的問題或聯絡 Adobe 支援人員。

## 查看日誌的步驟 {#viewing-logs}

您可以在&#x200B;*綜覽*頁面中檢視現有移轉集記錄。
請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要刪除的移轉集，然後按一下動作列中的&#x200B;**檢視記錄**。

   ![影像](/help/journey-migration/content-transfer-tool/assets/view-log1.png)

1. **記錄**&#x200B;對話框隨即顯示。按一下&#x200B;**提取記錄**，即可在新索引標籤中檢視記錄。

   ![影像](/help/journey-migration/content-transfer-tool/assets/view-log2.png)
或者，

   您也可以在&#x200B;*綜覽*&#x200B;畫面中檢視移轉集記錄。請選取移轉集，然後按一下&#x200B;**提取**&#x200B;欄位下的狀態。在這個情況下，按一下&#x200B;**已完成**&#x200B;即可在新索引標籤中檢視記錄。

   ![影像](/help/journey-migration/content-transfer-tool/assets/view-log3.png)

1. 若要追蹤記錄而不使用使用者介面，您可以透過 SSH 連線至來源 AEM 環境，並追蹤 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。
