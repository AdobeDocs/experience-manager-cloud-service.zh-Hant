---
title: AEM as a Cloud Service2021.6.0版中Cloud Manager發行說明
description: AEM as a Cloud Service2021.5.0版中Cloud Manager發行說明
feature: Release Information
exl-id: 9a0a53d3-31d4-493d-ba2e-b4bb22f60351
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service 2021.6.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2021.6.0as a Cloud Service版中Cloud Manager的發行說明。

>[!NOTE]
>若要查看最新的Adobe Experience Manager as a Cloud Service發行說明，請按一下 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## 發行日期 {#release-date}

AEM 2021.6.0中的Cloud Manageras a Cloud Service日期為2021年6月10日。

### 新增功能 {#what-is-new}

* 預覽服務將以滾動方式部署到所有程式。 當客戶的計畫啟用預覽服務時，將在產品中收到通知。 請參閱 [存取預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 以取得更多詳細資訊。

* 現在，系統會在管道執行之間快取建置步驟期間下載的Maven相依性。 此功能將在未來數週內為客戶啟用。

* 現在可以通過編輯程式對話框編輯程式的名稱。

* 在專案建立期間和透過管理Git工作流程的預設推送命令中使用的預設分支名稱，已變更為 `main`.

* 重新整理UI中的編輯方案體驗。

* 品質規則 `ImmutableMutableMixCheck` 已更新為可分類 `/oak:index` 節點不可修改。

* 品質規則 `CQBP-84` 和 `CQBP-84--dependencies` 已整合為單一規則。 作為此整合的一部分，對依賴項的掃描可以更準確地識別部署到AEM運行時的第三方依賴項中的問題。

* 為避免混淆，「環境詳細資料」頁面上的「發佈AEM」和「發佈Dispatcher」區段列已整合。

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 已新增新的程式碼品質規則，以驗證 `damAssetLucene` 索引。 請參閱 [自訂DAM資產Lucene Oak索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) 以取得更多詳細資訊。

* 環境詳細資訊頁面現在會顯示「發佈」和「預覽」服務的多個網域名稱（如適用）。 請參閱 [環境詳細資訊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#viewing-environment) 以取得更多詳細資訊。

### 錯誤修正 {#bug-fixes}

* 未正確剖析根元素名稱后包含新行的JCR節點定義。

* 清單儲存庫API不會篩選已刪除的儲存庫。

* 為排程步驟提供無效值時，顯示錯誤錯誤訊息。

* 有時，使用者可能會看到綠色 *活動* 狀態（即使未部署該配置）。

* 某些程式編輯序列可能導致無法建立或編輯生產管道。

* 某些程式編輯序列可能會導致 **概述** 顯示誤導性消息的頁面，以重新執行程式設定。
