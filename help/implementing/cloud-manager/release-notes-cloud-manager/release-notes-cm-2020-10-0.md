---
title: AEM as aCloud Service中的Cloud Manager發行說明2020.10.0版
description: AEM as aCloud Service中的Cloud Manager發行說明2020.10.0版
feature: 發行資訊
exl-id: 129d0dd8-3d6e-4cf0-b42e-5526f5cf0836
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 48%

---

# Adobe Experience Manager as aCloud Service中的Cloud Manager發行說明2020.10.0 {#release-notes}

本頁概述AEM as a Cloud 2020.10.0中Cloud Manager的發行說明。

## 發行日期 {#release-date}

AEM as aCloud Service中的Cloud Manager 2020.10.0的發行日期為2020年10月1日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 環境頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* Cloud Manager建置容器現在支援使用Java 8或Java 11來編譯專案。 Maven工具鏈系統支援Java 11。

* 每個環境的環境變數數量提高至 200 個。

* 「概述」頁面上的「環境」卡片現在會列出最多三個環境。 用戶可以選擇&#x200B;**全部顯示**按鈕以導航到「環境」摘要頁以查看包含完整環境清單的表。
如需詳細資訊，請參閱[檢視環境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 。


### 錯誤修正 {#bug-fixes-cloud-manager}

* 環境完全建立前，從 Cloud Manager 到開發人員控制台的連結未正確啟用。

* 直接從 Cloud Manager 連結至開發人員控制台時，系統未顯示將沙箱方案的環境解除休眠/休眠的選項。

* 非生產管道編輯頁面上的取消和儲存按鈕不一定會顯示。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立新方案時，建議的名稱有時會傳回重複的現有方案名稱。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 環境頁面有時會在未顯示任何內容的情況下，顯示發佈和發送器區段。
