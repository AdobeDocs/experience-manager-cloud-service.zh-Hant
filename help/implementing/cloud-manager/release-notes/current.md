---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.5.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.5.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4340b957cea86452f916ab615b383aabacc21676
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 41%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.5.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 發行 2023.5.0 的發行說明。

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEMas a Cloud Service中Cloud Manager 2023.5.0版的發行日期為2023年5月11日。 下一版本計劃於 2023 年 6 月 8 日發行。

## 新增功能 {#what-is-new}

* 產品、功能和UI測試支援已擴充至 [非生產管道測試。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
* 除了啟用上游測試外， [UI測試支援已擴充至Cypress測試。](/help/implementing/cloud-manager/ui-testing.md)
* [自助服務內容副本](/help/implementing/developing/tools/content-copy.md) 現在可透過Cloud Manager UI從更高到更低的環境使用。
* 已增強管道執行驗證步驟，以在執行程式早期驗證復寫佇列的狀態。 這可確保部署步驟不受應由AEM管理員用戶直接在創作環境中處理的已阻止隊列的影響。

## 錯誤修正 {#bug-fixes}

* 環境名稱中使用多位元組字元時，環境建立不再失敗。
