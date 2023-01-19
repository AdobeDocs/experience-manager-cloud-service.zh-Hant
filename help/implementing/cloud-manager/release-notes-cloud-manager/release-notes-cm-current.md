---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.1.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2024.1.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 26a2ed4ee613b77c192652ae9afa99d5a86f72ce
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 30%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.1.0 的發行說明 {#release-notes}

本頁記錄AEM as a Cloud Service中Cloud Manager 2023.1.0版的發行說明。

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEMas a Cloud Service中Cloud Manager 2023.1.0版的發行日期為2023年1月19日。 下一版預計於2023年2月16日發行。

## 新增功能 {#what-is-new}

* 可用性增強是通過更新游標樣式來區分用戶可以採取操作的位置和預設指針。

* 在環境和管道執行的清單中，您現在可以按一下個別列來存取詳細資料。

* 自訂UI測試報表現在會複製到Cloud Manager儲存空間，並可透過Cloud Manager API呼叫存取。

* 使用者現在可使用向左箭頭，在上線介面工具集狀態之間轉換。

   ![上線介面工具集轉變](assets/go-live-transitions.gif)

* 自助服務 [建立支援HIPAA的計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 現在當有對應的權益和權限時即可使用。

## 錯誤修正 {#bug-fixes}

* Cloud Manager將防止兩個管道執行同時（或幾乎同時）啟動，從而避免管道故障。
