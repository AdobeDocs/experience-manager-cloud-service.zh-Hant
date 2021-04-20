---
title: 整合 Adobe Analytics
description: '整合 Adobe Analytics '
feature: Administering
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 4%

---


# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

將Adobe AnalyticsAEM與Cloud Service整合，讓您追蹤網頁活動。 整合需要：

* 使用Touch UI建立Analytics組態AEM做為Cloud Service。
* 在[AdobeLaunch](#analytics-launch)中添加和配置Adobe Analytics作為擴展。 如需Adobe啟動的詳細資訊，請參閱[本頁](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html)。

與舊版相AEM比，Analytics設定中不提供架構支援做為AEMCloud Service。 現在，它是透過Adobe啟動完成，而啟動實際上是利用Analytics功能(JSAEM程式庫)檢測網站的工具。 在「Adobe啟動」中，會建立屬性，可在其中設定Adobe Analytics擴充功能，並建立規則以傳送資料至Adobe Analytics。 Adobe啟動已取代sitecatalyst提供的分析工作。

>[!NOTE]
>
>Adobe Experience Manager是沒有現有Analytics帳戶的Cloud Service客戶，可要求存取Analytics Foundation Pack以進行Experience Cloud。 此Foundation Pack提供Analytics的使用量有限。

## 建立Adobe Analytics配置{#analytics-configuration}

1. 導覽至&#x200B;**工具** → **Cloud Services**。
2. 選擇&#x200B;**Adobe Analytics**。
   ![Adobe Analytics](assets/analytics_screen2.png "視窗Adobe Analytics視窗")
3. 選擇&#x200B;**建立**&#x200B;按鈕。
4. 填寫詳細資訊（請參閱下面），然後按一下&#x200B;**Connect**。

### 配置參數{#configuration-parameters}

「Adobe Analytics配置」窗口中的配置欄位包括：

![配置參](assets/properties_field1.png "數配置參數")

| 屬性 | 說明 |
|---|---|
| 公司 | Adobe Analytics登入公司 |
| 使用者名稱 | Adobe AnalyticsAPI使用者 |
| 密碼 | 用於驗證的Adobe Analytics密碼 |
| 資料中心 | 您帳戶所關聯的Adobe Analytics資料中心（例如，San Jose, London） |
| 區段 | 使用目前報表套裝中定義之Analytics區段的選項。 Analytics報表會根據區段進行篩選。 如需詳細資訊，請參閱[本頁](https://docs.adobe.com/content/help/en/analytics/components/segmentation/seg-overview.html)。 |
| 報表套裝 | 傳送資料和提取報表的儲存庫。 報表套裝會定義所選網站、網站集或網站頁面子集的完整獨立報表。 您可以檢視從單一報表套裝擷取的報表，並可隨時根據您的需求在設定中編輯此欄位。 |

### 將配置添加到站點{#add-configuration}

若要將Touch UI設定套用至網站，請前往：**Sites** → **選擇任何站點頁** → **Properties** → **Advanced** → **Configuration** →選擇配置租用戶。

## 使用AdobeAEM啟動{#analytics-launch}將Adobe Analytics整合在網站上

Adobe Analytics可以新增為Launch屬性的擴充功能。 可定義規則以執行映射並對Adobe Analytics進行後置調用：

* 觀看[此影片](https://docs.adobe.com/content/help/en/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html)，瞭解如何在Launch中為基本網站設定Analytics擴充功能。

* 如需如何建立規則及傳送資料至Adobe Analytics的詳細資訊，請參閱[本頁](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html)。

>[!NOTE]
>
>現有（舊版）架構仍然有效，但無法在Touch UI中設定。 建議在Launch中重建變數對應設定。

>[!NOTE]
>
>Launch的IMS設定（技術帳戶）已預先設定為AEMCloud Service。 使用者不必建立此設定。
