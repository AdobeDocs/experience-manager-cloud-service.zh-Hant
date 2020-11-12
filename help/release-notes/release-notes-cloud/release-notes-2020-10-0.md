---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] 作為2020.10.0的雲端服務發行說明。'
translation-type: tm+mt
source-git-commit: eb4a567e7ae2aac7260aae28e2b91b088e42f945
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 55%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM中Cloud Manager作為Cloud Service 2020.10.0的發行日期為2020年10月2日。

### What is new in [!DNL Cloud Manager] {#what-is-new-cm}

* 「環境」頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* Cloud Manager組建容器現在支援使用Java 8或Java 11編譯專案。 Maven工具鏈系統提供對Java 11的支援。

* 每個環境的環境變數數量提高至 200 個。

* 「概述」頁面上的「環境」卡現在最多可列出三個環境。 用戶可以選擇「顯 **示全部** 」按鈕，以導航至「環境」摘要頁，以查看包含完整環境清單的表。
有關詳細 [資訊，請參閱](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 「查看環境」。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 環境完全建立前，從 Cloud Manager 到開發人員控制台的連結未正確啟用。

* 直接從 Cloud Manager 連結至開發人員控制台時，系統未顯示將沙箱方案的環境解除休眠/休眠的選項。

* 「非生產管線編輯」(Non-Production Pipeline Edit)頁面上的「取消」(Cancel)和「保存」(Save)按鈕不一律可見。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立新方案時，建議的名稱有時會傳回重複的現有方案名稱。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 環境頁面有時會在未顯示任何內容的情況下，顯示發佈和發送器區段。
