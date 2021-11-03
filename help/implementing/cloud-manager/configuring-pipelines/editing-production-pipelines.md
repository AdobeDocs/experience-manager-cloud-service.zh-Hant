---
title: 編輯生產管道
description: 編輯生產管道
index: false
source-git-commit: b9d28088ad18a389108ebfb81aa750c63e637922
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# 編輯生產管道 {#edit-prod-pipeline}

可以從 **計畫概述** 頁面。

請依照下列步驟編輯已設定的管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **編輯**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. 此 **編輯生產管道** 對話框。

   1. 此 **設定** 索引標籤可讓您更新 **管道名稱**, **部署觸發程式**，和 **重要量度失敗行為**.

      >[!NOTE]
      >請參閱 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. 此 **來源** 索引標籤提供可勾選或取消勾選的選項 **部署至生產環境前暫停** 和 **已排程** 選項 **生產部署選項**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. 此 **體驗稽核** 選項可讓您更新或新增頁面。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. 按一下 **更新** 編輯管道後。

## 其他生產管道動作 {#additional-prod-actions}

### 執行生產管道 {#run-prod}

可以從「管道」卡運行生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **執行**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

### 刪除生產管道 {#delete-prod}

您可以從「管道」卡中刪除生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **刪除**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >部署管理員角色中的使用者現在可以透過 **刪除** 選項。