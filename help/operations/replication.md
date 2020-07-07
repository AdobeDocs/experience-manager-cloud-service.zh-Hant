---
title: 複寫
description: 散佈 和複製故障排除。
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---


# 複寫 {#replication}

Adobe Experience Manager as a Cloud Service使用 [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) (Sling Content Distribution)功能，將要複製的內容移至在Adobe I/O上執行且不在AEM執行階段的管道服務。

>[!NOTE]
>
>閱讀 [散發](/help/core-concepts/architecture.md#content-distribution) ，以取得詳細資訊。

## 發佈內容的方法 {#methods-of-publishing-content}

### 快速取消／發佈——計畫取消／發佈 {#publish-unpublish}

作者適用的這些標準AEM功能不會隨AEM Cloud服務而改變。

### 樹狀結構啟動 {#tree-activation}

要執行樹狀結構激活：

1. 從「AEM開始」選單導覽至「工 **具>部署>散發」**
2. 選取卡片 **forwardPublisher**
3. 進入forwardPublisher Web控制台UI後，選擇「分 **發」**
   ![散](assets/distribute.png "發")
4. 在路徑瀏覽器中選擇路徑，選擇根據需要添加節點、樹或刪除，然後選擇「提交」( **Submit)**

## 疑難排解 {#troubleshooting}

若要疑難排解複製問題，請導覽至AEM Author Service Web UI中的「複製佇列」:

1. 從「AEM開始」選單導覽至「工 **具>部署>散發」**
2. 選取卡片 **forwardPublisher**
   ![狀](assets/status.png "態")
3. 檢查應為綠色的隊列狀態
4. 您可以測試到複製服務的連接
5. 選擇「 **記錄** 」標籤，顯示內容發佈的歷史記錄

![日](assets/logs.png "志")

如果內容無法發佈，則整個出版物會從AEM Publish Service回復。
在這種情況下，應審查隊列，以確定哪些項目導致出版物取消。 按一下顯示紅色狀態的佇列，即會顯示包含待審項目的佇列，視需要可清除單一或所有項目。
