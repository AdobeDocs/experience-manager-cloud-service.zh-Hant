---
title: Cloud Manager在as a Cloud Service版AEM2021.6.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2021.5.0中的發行說明
feature: Release Information
exl-id: 9a0a53d3-31d4-493d-ba2e-b4bb22f60351
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.6.0 {#release-notes}

本頁概述了as a Cloud Service2021.6.0中Cloud Manager的發行說明AEM。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的當前發行說明，請按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年6月10日。

### 新增功能 {#what-is-new}

* 預覽服務將以滾動方式部署到所有程式。 客戶在為其預覽服務啟用計畫時將收到產品通知。 請參閱 [訪問預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 的子菜單。

* 現在，在生成步驟期間下載的Maven Dependencies將在管道執行之間快取。 此功能將在未來幾週內為客戶啟用。

* 現在，可以通過編輯程式對話框編輯程式的名稱。

* 在項目建立期間和通過管理Git工作流在預設推送命令中使用的預設分支名稱已更改為 `main`。

* 已刷新UI中的編輯程式體驗。

* 質量規則 `ImmutableMutableMixCheck` 已更新以分類 `/oak:index` 節點是不可變的。

* 質量規則 `CQBP-84` 和 `CQBP-84--dependencies` 被整合為一條規則。 作為此整合的一部分，對依賴項的掃描可以更準確地確定正在部署到運行時的第三方依賴項中AEM的問題。

* 為避免混淆，「環境詳細AEM資訊」頁上的「發佈」和「發佈調度程式」段行已合併。

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 新代碼質量規則已添加以驗證 `damAssetLucene` 索引。 請參閱 [自定義DAM資產Lucene Oak索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) 的子菜單。

* 「環境詳細資訊」頁面現在將顯示發佈和預覽服務的多個域名（如果適用）。 請參閱 [環境詳細資訊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#viewing-environment) 的雙曲餘切值。

### 錯誤修正 {#bug-fixes}

* 未正確分析根元素名稱后包含換行符的JCR節點定義。

* 清單儲存庫API不會篩選已刪除的儲存庫。

* 為計畫步驟提供了無效值時，顯示錯誤錯誤消息。

* 有時，用戶可能看到綠色 *活動* 即使未部署該配置，「IP允許清單」旁邊的狀態也仍然存在。

* 某些程式編輯序列可能導致無法建立或編輯生產管線。

* 某些程式編輯序列可能導致 **概述** 顯示誤導性消息以重新執行程式設定。
