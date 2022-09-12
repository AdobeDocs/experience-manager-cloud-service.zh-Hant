---
title: 管理管道
description: 了解如何管理現有的管道，包括編輯、執行和刪除管道。
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# 管理管道 {#managing-pipelines}

了解如何管理現有的管道，包括編輯、執行和刪除管道。

## 管道卡 {#pipeline-card}

此 **管道** 卡 **計畫概述** Cloud Manager中的頁面提供所有管道及其目前狀態的概述。

![Cloud Manager中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

按一下每條管道旁的刪節號按鈕，可執行下列操作。

* [執行管道](#running-pipelines)
* [編輯管道](#editing-pipelines)
* [刪除管道](#deleting-pipelines)
* [檢視詳情](#view-details)

在管道清單的底部，您有常規選項。

* **新增**  — 至 [新增生產管道](configuring-production-pipelines.md) 或 [新增非生產管道](configuring-non-production-pipelines.md)
* **全部顯示**  — 將用戶帶到管道螢幕，在更詳細的表中查看所有管道。
* **存取存放庫資訊**  — 顯示存取Cloud Manager Git存放庫所需的資訊
* **更多詳情**  — 導覽至CI/CD管道檔案資源。

## 正在運行管道 {#running-pipelines}

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **管道** 卡片 **計畫概述** 頁面，然後按一下您所執行之選取管道旁的刪節號按鈕 **執行** 的上界。

1. 管道運行開始，由 **狀態** 欄。

您可以再次按一下省略號按鈕，然後選取 **[查看詳細資訊。](#view-details)**

根據管道類型，您可以再次按一下省略號按鈕並選擇 **取消**.

## 編輯管道 {#editing-pipelines}

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **管道** 卡片 **計畫概述** 頁面，按一下要編輯的管道旁的刪節號按鈕，然後選取 **編輯** 的上界。

1. 此 **編輯生產管道** 或 **編輯非生產管道** 對話框，允許您編輯建立管道時輸入的相同詳細資訊。

   * 有關管道可用的所有欄位和配置選項的詳細資訊，請參閱以下頁。
      * [設定生產管道](configuring-production-pipelines.md)
      * [設定非生產管道](configuring-non-production-pipelines.md)

1. 按一下 **更新** 編輯管道後。

>[!NOTE]
>
>無法編輯正在運行的管道。

## 刪除管道 {#deleting-pipelines}

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **管道** 卡片 **計畫概述** 頁面，然後按一下您所執行之選取管道旁的刪節號按鈕 **刪除** 的上界。

>[!NOTE]
>
>無法刪除正在運行的管道。

## 檢視詳情 {#view-details}

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **管道** 卡片 **計畫概述** 頁面，然後按一下您所執行之選取管道旁的刪節號按鈕 **查看詳細資訊** 的上界。

1. 系統會將您帶至執行中管道的詳細資訊頁面。

![管道詳細資訊](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

從這裡，您可以查看管道各個步驟的狀態，並擷取建置記錄以用於診斷用途。 請參閱檔案 [部署程式碼](/help/implementing/cloud-manager/deploy-code.md) 以取得更多資訊。

>[!NOTE]
>
>只能查看正在運行或至少已運行一次的管道的詳細資訊。
