---
title: 整合 Adobe Analytics
description: 整合 Adobe Analytics
feature: Administering
role: Admin
exl-id: e353a1fa-3e99-4d79-a0d1-40851bc55506
source-git-commit: e950f2399553c301c97c4fcac549a7ef6a234164
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 3%

---

# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

整合Adobe Analytics和AEMas a Cloud Service可讓您追蹤網頁活動。 整合需要：

* 使用觸控式UI在AEM as a Cloud Service中建立Analytics設定。 請注意，若要整合Adobe Analytics與AEMas a Cloud Service，需要IMS驗證。
* 將Adobe Analytics新增及設定為 [Adobe啟動](#analytics-launch). 如需Experience Launch的詳細資訊，請參閱 [本頁](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html).

與舊版AEM相比，AEMas a Cloud Service中的Analytics設定不提供架構支援。 現在改為透過AdobeLaunch完成，Launch是實際上用來檢測具有Analytics功能（JS資料庫）的AEM網站的工具。 在AdobeLaunch中，會建立屬性，可在此設定Adobe Analytics擴充功能，並建立規則以將資料傳送至Adobe Analytics。 Adobe啟動已取代sitecatalyst提供的分析工作。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service客戶若沒有現有的Analytics帳戶，可要求存取Analytics Foundation Pack以取得Experience Cloud。 此Foundation Pack提供Analytics的有限量使用。

## 建立Adobe Analytics設定 {#analytics-configuration}

1. 導覽至 **工具** → **Cloud Services**.
2. 選擇 **Adobe Analytics**.
   ![Adobe Analytics視窗](assets/analytics_screen2.png "Adobe Analytics視窗")
3. 選取 **建立** 按鈕。
4. 填寫詳細資訊（請參閱下方），然後按一下 **Connect**.

### 設定參數 {#configuration-parameters}

設定視窗中顯示的欄位如下：

![設定參數](assets/properties_field2.png "設定參數")

| 屬性 | 說明 |
|---|---|
| 標題 | 配置名稱 |
| IMS 設定 | 選取IMS設定（請參閱下文章節） |
| 區段 | 使用目前報表套裝中定義之Analytics區段的選項。 系統會根據區段來篩選Analytics報表。 請參閱 [本頁](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html) 以取得其他詳細資訊。 |
| 報表套裝 | 您傳送資料和提取報表的存放庫。 報表套裝可全面而獨立地定義針對選定網站、一組網站或網站頁面子集的報告。 您可以檢視從單一報表套裝擷取的報表，並隨時根據您的需求在設定中編輯此欄位。 |

### Adobe Analytics，具有IMS驗證 {#configuration-parameters-ims}

若要正確整合Adobe Analytics與AEMas a Cloud Service，需要IMS設定。 必須建立此配置，請參閱此 [頁面](/help/sites-cloud/integrating/integration-adobe-analytics-ims.md) 了解如何建立Analytics IMS設定。

### 將配置添加到站點 {#add-configuration}

若要將觸控式UI設定套用至網站，請前往： **網站** → **選擇任何網站頁面** → **屬性** → **進階** → **設定** →選擇配置租戶。

## 使用Launch整合AEM網站上的Adobe Analytics {#analytics-launch}

Adobe Analytics可在Launch屬性中以擴充功能的形式新增。 可定義規則，以執行對應及對Adobe Analytics進行後置呼叫：

* Watch [此影片](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html) 了解如何在Launch中為基本網站設定Analytics擴充功能。

* 請參閱 [本頁](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) 以取得如何建立規則和傳送資料至Adobe Analytics的詳細資訊。

>[!NOTE]
>
>Launch的IMS設定（技術帳戶）已在AEMas a Cloud Service中預先設定。 您不必建立此設定。

>[!NOTE]
>
>現有（舊版）架構仍可運作，但無法在觸控式UI中設定。 建議您在Launch中重建變數對應設定。
