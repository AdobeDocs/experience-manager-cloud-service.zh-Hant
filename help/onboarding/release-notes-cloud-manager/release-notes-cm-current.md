---
title: AEM as aCloud Service中Cloud Manager的發行說明2021.5.0版
description: AEM as aCloud Service中Cloud Manager的發行說明2021.5.0版
feature: 發行資訊
source-git-commit: d30f81b8d12a4136d96cdfd1fb8c3e9927c015d1
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---


# Adobe Experience Manager as aCloud Service2021.6.0 {#release-notes}中的Cloud Manager發行說明

本頁概述AEM as a 2021.6.0Cloud Service中Cloud Manager的發行說明。

>[!NOTE]
>若要查看Adobe Experience Manager as aCloud Service的最新發行說明，請按一下[here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html)。

## 發行日期 {#release-date}

AEM as aCloud Service2021.6.0中的Cloud Manager發行日期為2021年6月10日。
下一版預計於2021年7月15日發行。

### 新功能 {#what-is-new}

* 預覽服務將以滾動方式部署到所有程式。 當客戶的計畫啟用預覽服務時，將在產品中收到通知。 如需詳細資訊，請參閱[存取預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 。

* 現在，系統會在管道執行之間快取建置步驟期間下載的Maven相依性。 此功能將在未來數週內為客戶啟用。

* 現在可以通過編輯程式對話框編輯程式的名稱。

* 專案建立期間和透過管理Git工作流程的預設推送命令中使用的預設分支名稱已變更為`main`。

* 重新整理UI中的編輯方案體驗。

* 品質規則`ImmutableMutableMixCheck`已更新，將`/oak:index`節點分類為不可變。

* 品質規則`CQBP-84`和`CQBP-84--dependencies`已整合為單一規則。

* 為避免混淆，「環境詳細資料」頁面上的「發佈AEM」和「發佈Dispatcher」區段列已整合。

* 已新增新的程式碼品質規則，以驗證`damAssetLucene`索引的結構。 如需詳細資訊，請參閱[自訂DAM資產Lucene Oak Indexes](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) 。

* 環境詳細資訊頁面現在會顯示「發佈」和「預覽」服務的多個網域名稱（如適用）。 如需詳細資訊，請參閱[環境詳細資料](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 。

### 錯誤修正 {#bug-fixes}

* 未正確剖析根元素名稱后包含新行的JCR節點定義。

* 清單儲存庫API不會篩選已刪除的儲存庫。

* 為排程步驟提供無效值時，顯示錯誤錯誤訊息。

* 有時，即使未部署該配置，使用者仍可能在IP允許清單旁看到綠色的&#x200B;*active*&#x200B;狀態。

* 某些程式編輯序列可能導致無法建立或編輯生產管道。

* 某些程式編輯序列可能導致在&#x200B;**概述**&#x200B;頁中顯示一條誤導性消息以重新執行程式設定。
