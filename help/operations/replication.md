---
title: 複寫
description: 散佈 和複製故障排除。
translation-type: tm+mt
source-git-commit: abb45225e880f3d08b9d26c29e243037564acef0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# 複寫 {#replication}

Adobe Experience Manager做為Cloud服務會使用[Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html)功能，將要複製的內容移至在AEM執行階段以外的Adobe I/O上執行的管道服務。

>[!NOTE]
>
>如需詳細資訊，請閱讀[Distribution](/help/core-concepts/architecture.md#content-distribution)。

## 發佈內容{#methods-of-publishing-content}的方法

### 快速取消／發佈——計畫取消／發佈{#publish-unpublish}

作者適用的這些標準AEM功能不會隨著AEM Cloud服務而改變。

### 開啟和關閉時間——觸發器配置{#on-and-off-times-trigger-configuration}

從「頁面屬性」的「基本」標籤中可以找到&#x200B;**On Time**&#x200B;和&#x200B;**Off Time**&#x200B;的其他可能性。[](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

要實現自動複製，您需要在[OSGi配置](/help/implementing/deploying/configuring-osgi.md)**開關觸發器配置**&#x200B;中啟用&#x200B;**自動複製**:

![OSGi On Off觸發器配置](/help/operations/assets/replication-on-off-trigger.png)

### 樹激活{#tree-activation}

要執行樹狀結構激活：

1. 從「AEM開始功能表」導覽至「**工具>部署>散發」**
2. 選擇卡片&#x200B;**forwardPublisher**
3. 進入forwardPublisher Web控制台UI後，**選擇Distribute**

   ![散](assets/distribute.png "發")
4. 在路徑瀏覽器中選擇路徑，選擇根據需要添加節點、樹或刪除，然後選擇&#x200B;**提交**

## 疑難排解 {#troubleshooting}

若要疑難排解複製問題，請導覽至AEM Author Service Web UI中的「複製佇列」:

1. 從「AEM開始功能表」導覽至「**工具>部署>散發」**
2. 選擇卡片&#x200B;**forwardPublisher**
   ![狀](assets/status.png "態")
3. 檢查應為綠色的隊列狀態
4. 您可以測試到複製服務的連接
5. 選擇&#x200B;**日誌**&#x200B;頁籤，該頁籤顯示內容發佈的歷史記錄

![日](assets/logs.png "志")

如果內容無法發佈，則整個出版物會從AEM Publish Service回復。
在這種情況下，應審查隊列，以確定哪些項目導致出版物取消。 按一下顯示紅色狀態的佇列，即會顯示包含待審項目的佇列，視需要可清除單一或所有項目。
