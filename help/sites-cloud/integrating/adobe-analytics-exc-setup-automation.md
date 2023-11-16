---
title: 將Adobe Analytics與Experience Cloud設定自動化整合
description: Experience Cloud設定自動化透過簡單的UI精靈介面，提供簡單且自動化的方法來整合和檢測Experience Manager Sites與Experience Platform標籤和Adobe Analytics。 瞭解如何對您自己的網站使用自動化設定。
feature: Administering
role: Admin
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 2%

---

# 將Adobe Analytics與Experience Cloud設定自動化整合 {#integrate-adobe-analytics-automation-setup}

Experience Cloud設定自動化透過簡單的UI精靈介面，提供簡單且自動化的方法來整合和檢測Experience Manager Sites與Experience Platform標籤和Adobe Analytics。

將Adobe Analytics與AEM Sites整合從未如此簡單。 透過Experience Cloud設定自動化，只需按幾下滑鼠，即可設定、整合及檢測您的網站以擷取效能分析，以瞭解客戶的參與及轉換程度。

本影片探討AEM網站如何使用Experience Platform設定自動化與Experience Cloud標籤和分析整合：

>[!VIDEO](https://video.tv.adobe.com/v/345372/?quality=12)

## 要求

自動化設定可立即使用建置的AEM網站運作 [AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 使用 [Adobe使用者端資料層](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) 已啟用。 您可以使用產生已自動啟用這些功能的新網站 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 或透過使用建立網站 [網站範本](/help/journey-sites/quick-site/create-site.md).

## 先決條件 {#prerequisites}

使用此功能之前，請務必遵循這些指示，以確保已在您的環境中正確設定必要服務：

1. 登入Adobe Admin Console (https://adminconsole.adobe.com/)。
1. 請確保在右上角選取正確的IMS組織ID。
1. 按一下產品導覽選項。
1. 檢查是否已為IMS組織布建「Adobe Experience Manager as a Cloud Service」。
1. 檢查是否已為IMS組織布建「Adobe Analytics」。
1. 前往Cloud Manager (https://experience.adobe.com/cloud-manager)。
1. 選取適當的計畫。
1. 檢查環境是否在最新版的Cloud Service上（如果不是，請選取功能表選項中的「更新」）。
1. 在Cloud Manager中執行完整棧疊管道。

環境現在應該準備好進行Experience Cloud設定自動化。

## 設定方法

1. 瀏覽至 **網站** 並選取要與Adobe Analytics整合的網站根目錄。
1. 展開側邊欄功能表並點選 **設定Analytics**.

   這是側邊欄中的新選項，可開啟一個面板，提供「Experience Cloud設定自動化」的控制項和狀態。
1. 點選 **整合Analytics** 按鈕。
1. 在產生的對話方塊中，提供名稱， **報告套裝ID**.

   此字串用於建立新的 [報告套裝ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=en) Adobe Analytics中作為所選AEM網站分析資料的資料存放區。 提供的字串會附加環境和層級識別碼以確保唯一性。

1. 重新整理頁面和面板，然後點選 **檢查整合狀態** 以檢查自動化的狀態。

   自動化設定為非同步進行。 此 **檢查整合狀態** 將顯示整合的目前狀態。

   * **進行中**  — 表示工作正在執行。
   * **整合完成**  — 表示工作已將Analytics和Tags整合、設定Tags擴充功能和Tags規則，並在Adobe Analytics中建立新的報表套裝。
   * **失敗**  — 表示自動化工作無法成功完成。 按一下記錄檔連結，檢查此工作的記錄檔。

## 驗證AEM設定

自動化完成後，請驗證您的網站現在是否正在引發Analytics事件。

1. 使用在您的網站中開啟頁面 **網站編輯器**.
1. 使用 **以發佈的形式檢視** 用於載入頁面發佈版本的選項。
1. 使用瀏覽器的開發人員工具來檢查網路流量，並 **標籤** 和 `AppMeasurement.js` 正在載入檔案。
1. Inspect瀏覽器的主控台，可檢視Adobe使用者端資料層是否觸發和收集頁面和元件層級事件。

## 驗證Analytics設定

接著，導覽至Adobe Analytics以檢視從AEM網站上的事件流入的資料。

1. 導覽至與AEM網站相同的IMS組織中的Adobe Analytics。
1. 建立新的AEM Sites概觀報表，並導覽至 **報表** > **參與** > **Adobe Experience Manager** > **網站績效概觀**.
1. 點選 **開啟報告**.
1. 選取 **報告套裝ID** 符合上一個練習中使用的報表套裝名稱。
1. 檢視一段時間內流入新範本的分析資料。

   >[!NOTE]
   >
   > 透過新的整合，可能需要幾個小時才能將資料填入報表中。
