---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.6.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.6.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 80a5f58119dc304161d324491cd65c50e981ccd4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 37%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.6.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 發行 2023.6.0 的發行說明。

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEMas a Cloud Service中的Cloud Manager版本2023.6.0發行日期是2023年6月8日。 下一版本計畫於2023年7月6日發行。

## 新增功能 {#what-is-new}

* 建立新時 [程式或環境，](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 名稱現在限製為僅接受英數字元和一組有限的特殊字元。
* 恢復時 [生產管道，](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 確認對話方塊現在顯示在核准步驟中。
* 對於 **[客戶功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)** 和 **[自訂UI測試](/help/implementing/cloud-manager/ui-testing.md)** 管道步驟，新的 `INCOMPLETE` status現在為可能，這表示此類測試不存在，因此未執行。
   * 在這種情況下，管道不會失敗並繼續進行下一個步驟。

## 錯誤修正 {#bug-fixes}

* 此 [Web層設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 不再錯誤地為僅限資產的計畫啟用。
* 已新增更強大的驗證，以防止在環境布建期間發生某些型別的失敗。
