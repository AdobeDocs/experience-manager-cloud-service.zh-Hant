---
title: 整合 Adobe Analytics
description: 瞭解如何使用觸控式UI和Adobe Launch，將Adobe Analytics與AEM as a Cloud Service整合。
feature: Integration
role: Admin
exl-id: e353a1fa-3e99-4d79-a0d1-40851bc55506
solution: Experience Manager Sites
source-git-commit: 1289da67452be7fc0fa7f3126d2a3dbf051aa9b5
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 2%

---

# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

整合Adobe Analytics和AEM as a Cloud Service可讓您追蹤您的網頁活動。 此整合需要：

* 使用Touch UI在AEM as a Cloud Service中建立Analytics設定。 將Adobe Analytics與AEM as a Cloud Service整合需要IMS驗證。
* 在[Adobe啟動項](#analytics-launch)中新增並設定Adobe Analytics為擴充功能。 如需Adobe啟動的相關詳細資訊，您可以從[快速入門手冊](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html?lang=zh-Hant)開始。

與舊版AEM相比，AEM as a Cloud Service的Analytics設定中不提供框架支援。 相反地，現在透過Analytics Launch完成，這是使用Adobe功能（JS程式庫）檢測AEM網站的實用工具。 在Adobe Launch中，會建立一個屬性，您可在其中設定Adobe Analytics擴充功能，並建立規則以將資料傳送至Adobe Analytics。 Adobe Launch已取代sitecatalyst所提供的分析工作。

>[!NOTE]
>
>沒有現有Analytics帳戶的Adobe Experience Manager as a Cloud Service客戶可以要求存取Analytics Foundation Pack以進行Experience Cloud。 此Foundation Pack提供對Analytics的限量使用。

## 建立Adobe Analytics設定 {#analytics-configuration}

1. 瀏覽至&#x200B;**工具** → **Cloud Service**。
2. 選取&#x200B;**Adobe Analytics**。
   ![Adobe Analytics視窗](assets/analytics_screen2.png "Adobe Analytics視窗")
3. 選取&#x200B;**建立**&#x200B;按鈕。
4. 填寫詳細資料（請參閱下文），然後按一下[連線]。**&#x200B;**。

### 設定引數 {#configuration-parameters}

設定視窗中顯示的欄位如下：

![組態引數](assets/properties_field2.png "組態引數")

| 屬性 | 說明 |
|---|---|
| 標題 | 設定名稱 |
| IMS 設定 | 選取IMS設定（請參閱下章） |
| 區段 | 使用目前報表套裝中定義的Analytics區段的選項。 Analytics報表會根據區段進行篩選。 如需詳細資訊，請參閱[關於區段](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=zh-Hant)。 |
| 報表套裝 | 您傳送資料和提取報表的存放庫。 報表套裝主要定義選定網站、一組網站或網頁子集如何全面且獨立地呈現報告內容。 您可以檢視從單一報告套裝擷取的報告，並可隨時根據您的需求在設定中編輯此欄位。 |

### 具有IMS驗證的Adobe Analytics {#configuration-parameters-ims}

透過Analytics Standard API將Adobe Experience Manager as a Cloud Service (AEMaaCS)與Adobe Analytics整合需要設定Adobe IMS (Identity Management系統)。

請參閱[設定AEM as a Cloud Service的IMS整合](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md)以瞭解如何建立IMS設定。

>[!NOTE]
>
>[IMS整合現在已設定為S2S OAuth](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md)。
>
>先前是使用[JWT認證進行設定，而現在Adobe Developer Console](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)已棄用。

### 將設定新增至站台 {#add-configuration}

若要將Touch UI組態套用至網站，請移至： **網站** → **選取任何網站頁面** → **屬性** → **進階** → **組態** →選取組態租使用者。

## 使用Adobe Launch在AEM網站上整合Adobe Analytics {#analytics-launch}

Adobe Analytics可新增為Launch屬性中的擴充功能。 可以定義規則來執行對應並對Adobe Analytics進行後續呼叫：

* 觀看[此影片](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html?lang=zh-Hant)，瞭解如何在Launch中設定基本網站的Analytics擴充功能。

* 請參閱[新增Adobe Analytics](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=zh-Hant)，以取得有關如何建立規則及傳送資料至Adobe Analytics的詳細資訊。

>[!NOTE]
>
>已在AEM as a Cloud Service中預先設定Launch的IMS設定（技術帳戶）。 您不需要建立此設定。

>[!NOTE]
>
>現有（舊版）架構仍可運作，但無法在Touch UI中設定。 建議您在Launch中重新建置變數對應設定。
