---
title: 將Adobe Analytics與Experience Cloud設定自動化整合
description: Experience Cloud設定自動化提供簡單且自動化的方式，透過簡單的UI精靈介面，整合及檢測Experience Manager Sites與Experience Platform標籤及Adobe Analytics。 了解如何透過您自己的網站使用自動化設定。
feature: Administering
role: Admin
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
source-git-commit: 539d3947964652dd92620ce0b0b057754742be96
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 2%

---

# 將Adobe Analytics與Experience Cloud設定自動化整合 {#integrate-adobe-analytics-automation-setup}

Experience Cloud設定自動化提供簡單且自動化的方式，透過簡單的UI精靈介面，整合及檢測Experience Manager Sites與Experience Platform標籤及Adobe Analytics。

將Adobe Analytics與AEM Sites整合從未像現在這樣簡單。 透過Experience Cloud設定自動化，您只需按幾下，即可設定、整合和檢測網站以擷取效能分析，以了解客戶的互動和轉換成效。

本影片探討如何使用AEM設定自動化將Experience Cloud網站與Experience Platform標籤和Analytics整合：

>[!VIDEO](https://video.tv.adobe.com/v/345372/?quality=12)

## 要求

自動化設定是專為使用 [AEM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [Adobe用戶端資料層](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) 已啟用。 您可以使用 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 或使用 [網站範本](/help/journey-sites/quick-site/create-site.md).

## 必備條件 {#prerequisites}

使用此功能之前，請務必依照下列指示操作，以確保在您的環境中已正確設定先決條件服務：

1. 登入Adobe Admin Console(https://adminconsole.adobe.com/)。
1. 請確定右上角已選取正確的IMS組織ID。
1. 按一下產品導覽選項。
1. 檢查是否已針對IMS組織布建「Adobe Experience Manager as a Cloud Service」。
1. 檢查是否已針對IMS組織布建「Adobe Analytics」。
1. 前往Cloud Manager(https://experience.adobe.com/cloud-manager)。
1. 選擇適當的方案。
1. 檢查「Cloud Service」是否位於最新版本的環境中（如果不是，請在菜單選項中選擇「更新」）。
1. 在Cloud Manager中執行完整堆疊管道。

環境現在應已準備好進行Experience Cloud設定自動化。

## 如何設定

1. 導覽至 **網站** 並選取要與Adobe Analytics整合之網站的根目錄。
1. 展開側邊欄選單並點選 **設定分析**.

   這是側邊欄中的新選項，可開啟一個面板，提供Experience Cloud設定自動化的控制項和狀態。
1. 點選 **整合Analytics** 按鈕。
1. 在產生的對話方塊中，提供 **報表套裝ID**.

   此字串將用於建立新 [報表套裝ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=en) 在Adobe Analytics中，作為所選AEM網站之analytics資料的資料存放區。 提供的字串將附加環境和層標識符，以確保獨特性。

1. 重新整理頁面和面板，然後點選 **檢查整合狀態** 來檢查自動化狀態。

   自動化設定會以非同步方式進行。 此 **檢查整合狀態** 會顯示整合的目前狀態。

   * **正在進行中**  — 表示作業正在運行。
   * **整合完成**  — 指出工作已完成整合Analytics與標籤、設定標籤擴充功能與標籤規則，以及在Adobe Analytics中建立新的報表套裝。
   * **失敗**  — 表示自動作業無法成功完成。 按一下「日誌」連結，檢查此作業的日誌檔案。

## 驗證AEM設定

自動化完成後，驗證您的網站現在是否觸發Analytics事件。

1. 使用 **網站編輯器**.
1. 使用 **檢視為已發佈** 選項來載入已發佈的頁面版本。
1. 使用瀏覽器的開發人員工具來檢查網路流量，以及 **標籤** 和 `AppMeasurement.js` 檔案現在正在載入。
1. Inspect瀏覽器的主控台，以查看Adobe用戶端資料層已引發並收集頁面和元件層級事件。

## 驗證Analytics設定

接下來，導覽至Adobe Analytics以檢視從AEM網站上的事件流入的資料。

1. 導覽至您AEM網站所在相同IMS組織中的Adobe Analytics。
1. 建立新的概述報表，供AEM Sites導覽至 **報表** > **參與** > **Adobe Experience Manager** > **網站效能概述**.
1. 點選 **開啟報表**.
1. 選取 **報表套裝ID** 的名稱，而此名稱會符合先前練習中使用的報表套裝名稱。
1. 檢視分析資料在一段時間內流入新範本。

   >[!NOTE]
   >
   > 有了新整合，報表填入資料可能需要數小時的時間。
