---
title: AEM as a Cloud Service 版本 2020.10.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2020.10.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: 129d0dd8-3d6e-4cf0-b42e-5526f5cf0836
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2020.10.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2020.10.0 中 Cloud Manager 的發行說明

## 發行日期 {#release-date}

AEM as a Cloud Service 2020.10.0 中的 Cloud Manager 發行日期是 2020 年 10 月 01 日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 環境頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* Cloud Manager 建置容器現可支援使用 Java 8 或 Java 11 編譯專案。Maven 工具鏈系統支援 Java 11。

* 每個環境的環境變數數量提高至 200 個。

* 「總覽」頁面上的「環境」卡現在會列出最多三個環境。使用者可以選擇&#x200B;**全部顯示**按鈕，瀏覽到「環境摘要」頁面以查看包含完整環境清單的表格。
如需詳細資訊，請參閱[檢視環境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。


### 錯誤修正 {#bug-fixes-cloud-manager}

* 環境完全建立前，從 Cloud Manager 到開發人員控制台的連結未正確啟用。

* 直接從 Cloud Manager 連結至開發人員控制台時，系統未顯示將沙箱方案的環境解除休眠/休眠的選項。

* 非生產管道編輯頁面有時未顯示取消和儲存按鈕。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立新方案時，建議的名稱有時會傳回重複的現有方案名稱。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 環境頁面有時會在未顯示任何內容的情況下，顯示發佈和發送器區段。
