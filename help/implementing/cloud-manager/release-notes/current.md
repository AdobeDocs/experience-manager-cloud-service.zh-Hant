---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.6.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.6.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 93%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.6.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 2023.6.0 版的發行說明。

>[!NOTE]
>
>另請參閱 [此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md) 以瞭解Adobe Experience Manager as a Cloud Service目前的發行說明。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2022.11.0 版發行日期為 2023 年 6 月 8 日。下一版本預計於 2023 年 7 月 6 日發行。

## 新增功能 {#what-is-new}

* 除了主要區域之外，客戶還可以購買額外的次要發佈區域，如此即可獲得和減少延遲及提高可用性相關的優勢。注意：可能適用特定限制。
* 建立新的[計畫或環境時，](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)該名稱現在受到限制，僅接受英數字元和有限的特殊字元組。
* 恢復[生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)時，核准步驟現在會顯示確認對話框。
* 對於&#x200B;**[客戶功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)**&#x200B;和&#x200B;**[自訂 UI 測試](/help/implementing/cloud-manager/ui-testing.md)**&#x200B;管道步驟，現在可能有新的 `INCOMPLETE` 狀態，這表示這類測試不存在，因此未執行。
   * 這種情況下，管道不會失敗並會繼續進行下一步。

## 錯誤修正 {#bug-fixes}

* 此 [Web 層設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)不會再錯誤地為僅限資產計畫啟用。
* 已新增更強大的驗證以防止在環境佈建期間出現特定類型的失敗。
