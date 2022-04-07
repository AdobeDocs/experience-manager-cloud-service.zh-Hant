---
title: Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.4.0發行說明
description: 以下是Cloud Manager 2022.4.0在as a Cloud Service中的發行說明AEM。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: e448ee4ee2928a136bdab382c67104bedce28732
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---


# Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.4.0發行說明 {#release-notes}

本頁記錄了Cloud Manager 2022.4.0在as a Cloud Service中的發行說明AEM。

>[!NOTE]
>
>請參閱 [此頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 為Adobe Experience Manager as a Cloud Service提供的本發行說明。

## 發行日期 {#release-date}

2022年4月7日Cloud Manager版本2022.4.0的AEM發佈日期。 下一版計畫於2022年5月5日發行。

## 新增功能 {#what-is-new}

* 管道構建步驟的持續時間和成功率的改進已經實施，並將在4月份以增量方式向所有客戶推出。
* 現在，通過在「添加和編輯管道嚮導」的輸入欄位中鍵入名稱的前幾個字元，並從建議的匹配項中為這兩個字元選擇，可以輕鬆找到git分支 [生產](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 和 [非生產](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 管線。
* 4月發佈後不久，在建立環境時定義雲區域時，印度將可供選擇。
* 的 **管線** 頁面現在具有分頁功能，可提高具有大量管道的程式的可用性。
   * 表中將顯示每頁50行。
* 的版本 [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 已將雲管理器使用的版本更新為36。
* OracleJDK現在是應用程式開發和操作的預設JDKAEM。 即使在Maven工具鏈中顯式選擇了替代選項，Cloud Manager生成過程也將自動切換到使用OracleJDK。
   * 有關如何切換到OracleJDK的詳細資訊，請參閱 [生成環境文檔。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)
   * 請參閱 [Adobe Experience Manager常見問題的Java支援策略](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf) 以解決有關此更改的常見問題。
* 現在，在驗證步驟中檢測較舊版本AEM將加快管道執行失敗的速度。 用戶將在用戶介面中顯示一條消息來指導他們。

## 錯誤修正 {#bug-fixes}

* 在UITest步驟中建立的日誌現在可通過UI下載。
* Web層配置管道現在只能重用Web層配置執行中的包。
* UI中的消息更清楚地說明了如何更新過AEM時的環境。
