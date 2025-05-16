---
title: 將Adobe Analytics與Experience Cloud Setup Automation整合
description: Experience Cloud Setup Automation提供簡單且自動化的方式，透過簡單的UI精靈介面，將Experience Manager Sites與Experience Platform Tags和Adobe Analytics整合及檢測。 瞭解如何對您自己的網站使用自動化設定。
feature: Integration
role: Admin
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
solution: Experience Manager Sites
source-git-commit: 4a3e65ef6a8aa08c8bc78db31f94272334994ac5
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# 將Adobe Analytics與Experience Cloud Setup Automation整合 {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
>Experience Cloud設定自動化功能已過時。

Experience Cloud Setup Automation提供簡單且自動化的方式，透過簡單的UI精靈介面，將Experience Manager Sites與Experience Platform Tags和Adobe Analytics整合及檢測。

將Adobe Analytics與AEM Sites整合從未如此簡單。 透過Experience Cloud設定自動化，只需按幾下滑鼠，即可設定、整合及檢測您的網站以擷取效能分析，以瞭解客戶的參與及轉換程度。

本影片探討AEM網站如何使用Experience Cloud Setup Automation與Experience Platform Tags和Analytics整合：

>[!VIDEO](https://video.tv.adobe.com/v/345372/?quality=12)

## 要求

自動化設定可立即使用[AEM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hant)建立的AEM網站，並啟用[Adobe使用者端資料層](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)。 您可以使用[AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)或使用[網站範本](/help/journey-sites/quick-site/create-site.md)建立網站，來產生已自動啟用這些功能的新網站。

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

1. 導覽至&#x200B;**網站**，並選取要與Adobe Analytics整合的網站根目錄。
1. 展開側邊欄功能表並選取&#x200B;**設定Analytics**。

   這是側邊欄中的新選項，可開啟一個面板，提供Experience Cloud設定自動化的控制項和狀態。
1. 選取&#x200B;**整合Analytics**&#x200B;按鈕。
1. 在產生的對話方塊中，提供&#x200B;**報表套裝ID**&#x200B;的名稱。

   此字串用來在Adobe Analytics中建立[報表套裝ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html)，作為所選AEM網站分析資料的資料存放區。 提供的字串會附加環境和層級識別碼以確保唯一性。

1. 重新整理頁面和面板，然後選取&#x200B;**檢查整合狀態**&#x200B;以檢查自動化的狀態。

   自動化設定為非同步進行。 **檢查整合狀態**&#x200B;將顯示整合的目前狀態。

   * **進行中** — 表示工作正在執行。
   * **整合完成** — 表示工作已完成整合Analytics和Tags、設定Tags擴充功能和Tags規則，以及在Adobe Analytics中建立新的報表套裝。
   * **失敗** — 表示自動化工作無法成功完成。 按一下記錄檔連結，檢查此工作的記錄檔。

## 驗證AEM設定

自動化完成後，請驗證您的網站現在是否正在引發Analytics事件。

1. 使用&#x200B;**網站編輯器**&#x200B;在您的網站中開啟網頁。
1. 使用&#x200B;**以發佈的形式檢視**&#x200B;選項載入頁面的發佈版本。
1. 使用瀏覽器的開發人員工具來檢查網路流量，並檢查是否正在載入&#x200B;**標籤**&#x200B;和`AppMeasurement.js`檔案。
1. 檢查瀏覽器的主控台，以檢視頁面和元件層級事件是否由Adobe使用者端資料層觸發和收集。

## 驗證Analytics設定

接著，導覽至Adobe Analytics以檢視從AEM網站上的事件流入的資料。

1. 導覽至與AEM網站相同的IMS組織中的Adobe Analytics。
1. 建立AEM Sites的新概述報告，並導覽至&#x200B;**報告** > **參與** > **Adobe Experience Manager** > **網站效能概述**。
1. 選取&#x200B;**開啟報告**。
1. 選取符合上一個練習中所使用報表套裝名稱的&#x200B;**報表套裝ID**。
1. 檢視一段時間內流入新範本的分析資料。

   >[!NOTE]
   >
   > 透過新的整合，可能需要幾個小時才能將資料填入報表中。
