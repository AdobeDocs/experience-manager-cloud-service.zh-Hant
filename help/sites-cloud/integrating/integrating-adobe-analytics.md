---
title: 整合 Adobe Analytics
description: '整合 Adobe Analytics '
feature: Administering
role: Admin
exl-id: e353a1fa-3e99-4d79-a0d1-40851bc55506
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 4%

---

# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

整合Adobe AnalyticsAEM和as a Cloud Service允許您跟蹤網頁活動。 整合需要：

* 使用Touch UI在as a Cloud Service中建立分析配AEM置。
* 添加和配置Adobe Analytics作為 [Adobe啟動](#analytics-launch)。 有關Adobe啟動的詳細資訊，請參閱 [此頁](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html)。

與以前版本相比AEM，在as a Cloud Service的分析配置中未提供框架AEM支援。 現在，它通過Adobe啟動完成，該啟動是使用分析功能（JS庫）AEM檢測站點的實際工具。 在「Adobe啟動」中，將建立一個屬性，在該屬性中可以配置Adobe Analytics擴展，並建立規則將資料發送到Adobe Analytics。 Adobe啟動已經取代了催化劑提供的分析任務。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service客戶如果沒有現有的Analytics帳戶，可以請求訪問Analytics Foundation Pack以進行Experience Cloud。 此Foundation Pack提供了分析的有限量使用。

## 建立Adobe Analytics配置 {#analytics-configuration}

1. 導航到 **工具** → **Cloud Services**。
2. 選擇 **Adobe Analytics**。
   ![Adobe Analytics窗](assets/analytics_screen2.png "Adobe Analytics窗")
3. 選擇 **建立** 按鈕
4. 填寫詳細資訊（請參閱下面），然後按一下 **連接**。

### 配置參數 {#configuration-parameters}

「Adobe Analytics配置」窗口中的配置欄位包括：

![配置參數](assets/properties_field1.png "配置參數")

| 屬性 | 說明 |
|---|---|
| 公司 | Adobe Analytics登陸公司 |
| 使用者名稱 | Adobe AnalyticsAPI用戶 |
| 密碼 | Adobe Analytics用於身份驗證的密碼 |
| 資料中心 | 您的帳戶與的Adobe Analytics資料中心（例如San Jose, London）關聯 |
| 區段 | 選項，用於使用在當前報告套件中定義的分析段。 分析報告將根據段進行篩選。 請參閱 [此頁](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html) 的雙曲餘切值。 |
| 報表套裝 | 用於發送資料和獲取報告的儲存庫。 報告套件定義所選網站、網站集或網站頁面子集上的完整、獨立的報告。 您可以查看從單個報告套件獲取的報告，並可以根據您的要求隨時在配置中編輯此欄位。 |

### 向站點添加配置 {#add-configuration}

要將Touch UI配置應用到站點，請轉至： **站點** → **選擇任何網站頁** → **屬性** → **高級** → **配置** →選擇配置租戶。

## 利用Adobe Analytics發AEM布將Adobe整合到現場 {#analytics-launch}

Adobe Analytics可以作為啟動屬性的擴展添加。 可以定義規則以執行映射和對Adobe Analytics進行後續調用：

* 監視 [這個視頻](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html) 瞭解如何在啟動中為基本站點配置分析擴展。

* 請參閱 [此頁](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) 有關如何建立規則和將資料發送到Adobe Analytics的詳細資訊。

>[!NOTE]
>
>現有（舊）框架仍然有效，但無法在Touch UI中配置。 建議在「啟動」中重建變數映射配置。

>[!NOTE]
>
>用於啟動的IMS配置（技術帳戶）已在AEMas a Cloud Service中預配置。 用戶不必建立此配置。
