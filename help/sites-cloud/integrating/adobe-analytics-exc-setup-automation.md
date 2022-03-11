---
title: 將Adobe Analytics與Experience Cloud設定自動化整合
description: Experience Cloud設定自動化提供了一種簡單而自動化的方法，可以將Experience Manager Sites與Experience Platform Launch整合，使用簡單的UI嚮導介面對Adobe Analytics進行測試。 瞭解如何在您自己的站點上使用自動設定。
feature: Administering
role: Admin
hide: true
hidefromtoc: true
index: false
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 將Adobe Analytics與Experience Cloud設定自動化整合 {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> 此功能當前處於內部測試版中。 目標發佈日期為2022年第一季度。

Experience Cloud設定自動化提供了一種簡單而自動化的方法，可以將Experience Manager Sites與Experience Platform Launch整合，使用簡單的UI嚮導介面對Adobe Analytics進行測試。

將Adobe Analytics與AEM Sites整合起來，從未像現在這樣簡單。 通過Experience Cloud設定自動化，只需按一下幾下即可設定、整合和檢測您的站點以捕獲效能分析，以瞭解您的客戶對和轉換的參與程度如何。

此視頻探討如何使AEM用Experience Platform Launch設定自動化與Experience Cloud和分析整合站點：

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## 要求

自動化設定設計為在使用 [核AEM心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 和 [Adobe客戶端資料層](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) 啟用。 您可以使用 [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 或通過使用 [站點模板](/help/journey-sites/quick-site/create-site.md)。

## 如何設定

1. 導航到 **站點** 並選擇與Adobe Analytics整合的站點根。
1. 展開側軌菜單並點擊 **設定分析**。

   這是側軌中的一個新選項，它將開啟一個面板，該面板將提供Experience Cloud設定自動化的控制項和狀態。
1. 點擊 **整合分析** 按鈕
1. 在生成的對話框中，為 **報表套件ID**。

   此字串將用於建立新 [報表套件ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=en) 在Adobe Analytics作為所選站點的分析資料的資料存AEM儲。 提供的字串將附加環境和層標識符以確保唯一性。

1. 刷新頁面和面板並點擊 **檢查整合狀態** 以檢查自動化的狀態。

   自動設定非同步進行。 的 **檢查整合狀態** 將顯示整合的當前狀態。

   * **正在進行**  — 表示作業正在運行。
   * **整合完成**  — 表示作業已完成整合分析和啟動、設定啟動擴展和啟動規則以及在Adobe Analytics建立新的報告套件。
   * **失敗**  — 表示自動作業無法成功完成。 按一下日誌連結檢查此作業的日誌檔案。

## 驗證設AEM置

自動化完成後，驗證您的站點是否正在激活分析事件。

1. 使用 **站點編輯器**。
1. 使用 **查看為已發佈** 的子菜單。
1. 使用瀏覽器的開發人員工具來檢查網路流量， **啟動** 和 `AppMeasurement.js` 正在載入檔案。
1. Inspect瀏覽器的控制台，用於查看Adobe客戶端資料層觸發和收集的頁面和元件級事件。

## 驗證分析設定

接下來，導航到Adobe Analytics以查看從站點上的事件傳入的AEM資料。

1. 在與您的站點相同的IMS組織中導航到AEMAdobe Analytics。
1. 為AEM Sites導航至 **報告** > **參與** > **Adobe Experience Manager** > **站點效能概述**。
1. 點擊 **開啟報表**。
1. 選擇 **報表套件ID** 與上一練習中使用的報表套件名稱匹配。
1. 查看隨時間推移流入新模板的分析資料。

   >[!NOTE]
   >
   > 對於新的整合，報告填充資料可能需要幾個小時。
