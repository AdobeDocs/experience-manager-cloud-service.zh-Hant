---
title: 整合 Adobe Analytics
description: '整合 Adobe Analytics '
feature: 管理
role: Administrator
exl-id: e353a1fa-3e99-4d79-a0d1-40851bc55506
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 4%

---

# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

將Adobe Analytics和AEM整合為Cloud Service，即可追蹤網頁活動。 整合需要：

* 使用觸控式UI，在AEM中建立Analytics設定作為Cloud Service。
* 在[AdobeLaunch](#analytics-launch)中新增並設定Adobe Analytics為擴充功能。 如需AdobeLaunch的詳細資訊，請參閱[本頁面](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/quick-start.html)。

與舊版AEM相比，AEM as aCloud Service中的Analytics設定不提供架構支援。 現在改為透過AdobeLaunch完成，Launch是實際上用來檢測具有Analytics功能（JS資料庫）的AEM網站的工具。 在AdobeLaunch中，會建立屬性，可在此設定Adobe Analytics擴充功能，並建立規則以將資料傳送至Adobe Analytics。 Adobe啟動已取代sitecatalyst提供的分析工作。

>[!NOTE]
>
>Adobe Experience Manager作為沒有現有Analytics帳戶的Cloud Service客戶，可以要求存取Analytics Foundation Pack以進行Experience Cloud。 此Foundation Pack提供Analytics的有限量使用。

## 建立Adobe Analytics配置{#analytics-configuration}

1. 導覽至&#x200B;**工具** → **Cloud Services**。
2. 選擇&#x200B;**Adobe Analytics**。
   ![Adobe Analytics ](assets/analytics_screen2.png "WindowAdobe Analytics視窗")
3. 選擇&#x200B;**Create**&#x200B;按鈕。
4. 填寫詳細資訊（請參閱下面），然後按一下&#x200B;**Connect**。

### 配置參數{#configuration-parameters}

「 Adobe Analytics設定」視窗中顯示的設定欄位為：

![配置參](assets/properties_field1.png "數配置參數")

| 屬性 | 說明 |
|---|---|
| 公司 | Adobe Analytics登入公司 |
| 使用者名稱 | Adobe Analytics API使用者 |
| 密碼 | 用於驗證的Adobe Analytics密碼 |
| 資料中心 | 您帳戶關聯的Adobe Analytics資料中心（例如San Jose, London） |
| 區段 | 使用目前報表套裝中定義之Analytics區段的選項。 系統會根據區段來篩選Analytics報表。 如需其他詳細資訊，請參閱[此頁面](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html)。 |
| 報表套裝 | 您傳送資料和提取報表的存放庫。 報表套裝可全面而獨立地定義針對選定網站、一組網站或網站頁面子集的報告。 您可以檢視從單一報表套裝擷取的報表，並隨時根據您的需求在設定中編輯此欄位。 |

### 將配置添加到站點{#add-configuration}

若要將觸控式UI設定套用至網站，請前往：**Sites** → **選擇任何站點頁面** → **屬性** → **Advanced** → **Configuration** →選擇配置租戶。

## 使用Launch {#analytics-launch}在AEM網站上整合Adobe Analytics

Adobe Analytics可在Launch屬性中以擴充功能的形式新增。 可定義規則，以執行對應及對Adobe Analytics進行後置呼叫：

* 請觀看[此影片](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html)，了解如何在Launch中為基本網站設定Analytics擴充功能。

* 如需如何建立規則及將資料傳送至Adobe Analytics的詳細資訊，請參閱[本頁面](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html)。

>[!NOTE]
>
>現有（舊版）架構仍可運作，但無法在觸控式UI中設定。 建議您在Launch中重建變數對應設定。

>[!NOTE]
>
>Launch的IMS設定（技術帳戶）已在AEM中預先設定為Cloud Service。 使用者不需要建立此設定。
