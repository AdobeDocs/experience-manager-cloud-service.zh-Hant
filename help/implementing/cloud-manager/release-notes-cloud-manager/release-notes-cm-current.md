---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.1.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2024.1.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 26a2ed4ee613b77c192652ae9afa99d5a86f72ce
workflow-type: ht
source-wordcount: '207'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.1.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 發行 2023.1.0 的發行說明。

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2023.1.0 發行日期是 2023 年 1 月 19 日。下一版計劃於 2023 年 2 月 16 日發行。

## 新增功能 {#what-is-new}

* 可用性增強是透過更新游標樣式來區分使用者可以在何處執行操作和預設指標。

* 在環境和管道執行列表中，您現在可以透過點擊個別資料列來存取詳細資訊。

* 自訂 UI 測試報告現已複製到 Cloud Manager 儲存空間，並且可以透過 Cloud Manager API 叫用進行存取。

* 使用者現在可以使用左右箭在線上小工具狀態之間轉換。

   ![線上小工具轉換](assets/go-live-transitions.gif)

* 當相應的權利和權限可用時，可以自助[建立支持 HIPAA 的程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。

## 錯誤修正 {#bug-fixes}

* Cloud Manager 將防止兩個管道執行同時 (或幾乎同時) 開始，從而避免管道故障。
