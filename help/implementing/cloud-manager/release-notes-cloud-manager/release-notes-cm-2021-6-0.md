---
title: AEM as a Cloud Service 版本 2021.6.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2021.5.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: 9a0a53d3-31d4-493d-ba2e-b4bb22f60351
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.6.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.6.0 中 Cloud Manager 的發行說明

>[!NOTE]
>若要閱讀 Adobe Experience Manager as a Cloud Service 的目前發行說明，請按一下[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.6.0 中的 Cloud Manager 發行日期是 2021 年 6 月 10 日。

### 新增功能 {#what-is-new}

* 預覽服務將會以滾動方式部署到所有計劃。 當客戶的計劃有啟用預覽服務時，他們會在產品內收到通知。 參考[存取預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)更多細節。

* 現在，在建置步驟中所下載的 Maven Dependencies 會在管道執行之間快取。在未來幾週內將會為客戶啟用此功能。

* 現在可以透過編輯程序對話框編輯程序名稱。

* 在專案建立期間以及透過管理 Git 工作流程在預設推送命令中所使用的預設分支名稱已變更為 `main`。

* UI 中的編輯計劃體驗已更新。

* 已更新品質規則 `ImmutableMutableMixCheck`，可將 `/oak:index` 節點分類為不可變動。

* 品質規則 `CQBP-84` 和 `CQBP-84--dependencies` 已合併為單一規則。在此合併過程中，更準確地掃描相依性會識別部署到 AEM 執行階段的第三方相依性的問題。

* 為避免混淆，「環境詳細資料」頁面上的「發佈 AEM」和「發佈 Dispatcher」區段列已合併。

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 已新增計劃碼品質規則來驗證 `damAssetLucene` 索引的結構。 參考[自訂 DAM 資產 Lucene Oak 索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)更多細節。

* 「環境詳細資料」頁面現在會適當地顯示發佈和預覽服務的多個網域名稱 (如適用)。如需詳細資訊，請參閱[環境細節](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=zh-Hant#viewing-environment)。

### 錯誤修正 {#bug-fixes}

* 未正確解析根元素名稱後包含換行符的 JCR 節點定義。

* 列出存放庫 API 不會過濾已刪除的存放庫。

* 當為計劃步驟提供無效值時，會顯示不正確的錯誤消息。

* 有時，即使未部署該設定，使用者也可能會在 IP 允許清單旁邊看到綠色的&#x200B;*活動*&#x200B;狀態。

* 某些程序編輯序列可能會導致無法建立或編輯生產管道。

* 某些程序編輯序列可能會導致&#x200B;**總覽**&#x200B;頁面顯示誤導性消息以重新執行程序設定。
