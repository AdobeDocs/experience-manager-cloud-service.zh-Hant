---
title: 連結AEM Forms與Adobe Experience Platform (AEP) | Data Integration指南
description: 瞭解如何將AEM Forms與Adobe Experience Platform整合，以運用客戶設定檔、提交表單資料及建立個人化體驗。 逐步指南。
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: b0eb19d3-0297-4583-8471-edbb7257ded4
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 2%

---

# Adobe Experience Platform (AEP) 與 AEM Forms 整合 {#aem-forms-aep-integration}

<span class="preview">連線Adaptive Forms (AEM Forms)與Adobe Experience Platform (AEP)的功能屬於搶先使用方案。 若要要求存取功能，只要從您的正式地址傳送電子郵件至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D)即可。 您也可以造訪<a href="/help/forms/early-access-ea-features.md">搶先使用方案</a>頁面，探索所有可用的創新與功能。. </span>

## 概觀 {#overview}

您可以將AEM Forms與Adobe Experience Platform連線起來，轉換您的表單體驗。 這項強大的整合可讓組織運用即時客戶設定檔來提供個人化的表單體驗、簡化&#x200B;**AEM Forms資料提交至Experience Platform**，以及建立整個Adobe生態系統的統一客戶記錄。 將最適化表單與Experience Platform強大的資料管理功能連線起來，您可以建立更相關的體驗並提高轉換率，同時維持客戶資料的單一信任來源。

### 什麼是Adobe Experience Platform (AEP)的AEM Forms Connector？ {#what-is-connector}

Adobe Experience Platform適用的AEM Forms Connector (AEP)是AEM Forms提供的現成可用的(OOTB)聯結器，可實現AEM Forms與Adobe Experience Platform (AEP)之間的無縫整合。 此整合可讓您使用AEP中可用的XDM結構描述建立表單，並將資料提交回AEP以用於個人化和個人資料合併目的。

## 為何要將AEM Forms與Adobe Experience Platform (AEP)連線？ {#benefits}

將最適化Forms與Adobe Experience Platform連線後，可為貴組織和客戶帶來以下顯著優勢：

* **整合式客戶設定檔** — 使用表單提交資料擴充客戶設定檔，建立客戶互動和偏好設定的完整檢視
* **個人化表單體驗** — 利用現有的設定檔資料，預先填入欄位並根據已知的客戶資訊自訂表單
* **簡化資料彙集** — 直接將表單資料擷取到AEP資料集，無需建置自訂聯結器或整合程式碼
* **即時資料啟用** — 透過Real-Time CDP將表單提交資料傳送至其他Adobe應用程式，以立即啟用
* **簡化的合規性管理** — 透過AEP集中管理同意和資料治理原則
* **縮短開發時間** — 使用遵循最佳實務的預先建立聯結器，消除自訂整合工作
* **使用表單資料擴充客戶設定檔** — 透過提交每個表單自動更新及增強客戶設定檔，建立更豐富的客戶深入分析

## 主要功能 {#key-features}

* 使用AEP XDM結構描述建立表單
* 將表單資料提交至AEP以進行個人化
* 支援串流資料擷取
* 為增強的使用者體驗啟用設定檔水合
* 與AEP的設定檔系統整合
* XDM結構描述與用於標準化資料收集的最適化表單整合
* 表單的AEP串流連線可即時處理資料

以下影片提供必備條件（如建立結構、設定資料設定和驗證）的逐步指南，並示範如何建立最適化Forms並將其連線至Adobe Experience Platform (AEP)

>[!VIDEO](https://video.tv.adobe.com/v/3457850/)

<span>此影片僅適用於核心元件。 若為UE/Foundation元件，請參閱文章。</span>

## 先決條件 {#prerequisites}

在AEM Forms中設定AEP Connector之前，請確定您已在Adobe Experience Platform中完成下列操作：

1. 結構描述設定
   * [建立XDM結構描述](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/tutorials/create-schema-ui)
   * [啟用結構描述以進行效能分析](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)
   * [定義身分欄位](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)

2. 資料設定
   * [建立資料集](https://experienceleague.adobe.com/zh-hant/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-datasets)
   * [設定串流連線](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/ingestion/tutorials/create-streaming-connection) （您稍後需要串流端點URL，所以請記下它。）

3. 驗證
   * 從Adobe Developer Console [產生API認證](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/landing/platform-apis/api-authentication#generate-credentials) （使用者端ID和使用者端密碼）


## 實作步驟

### 1.建立AEP雲端設定

1. 導覽至您的&#x200B;**Adobe Experience Manager執行個體** > **工具** > **雲端服務** > **Adobe Experience Platform**。
1. 選取&#x200B;**設定容器**&#x200B;以儲存設定。
1. 按一下&#x200B;**建立**&#x200B;以開啟AEP設定精靈
1. 輸入下列明細：
   * 標題
   * 使用者端ID （取自開發人員主控台）
   * 使用者端密碼（從開發人員控制檯取得）
   * OAuth URL （有預設URL，但也可以從開發人員主控台取得）

   ![AEP雲端設定](/help/forms/assets/aep-cloud-configuration.png)

1. 按一下&#x200B;**連線**&#x200B;以建立連線。 建立連線後，請進行下列額外設定：
   * 基礎URL： platform.adobe.io （這是預設URL，也可以從開發人員控制檯取得），oauth和platform URL預設為生產URL。 若是這種情況，您需要連線到stage — 應使用stage URL。)
   * 組織ID （這是從開發人員控制檯取得的，連同使用者端ID/密碼）
   * 沙箱名稱（開發和生產環境都需要此名稱）

### 2.使用XDM結構描述整合建立表單 {#form-creation}

>[!BEGINTABS]

>[!TAB 基礎元件]

執行以下步驟，透過結構描述整合根據基礎元件建立最適化表單：

1. 存取表單建立精靈：
   * 導覽至您的&#x200B;**Adobe Experience Manager執行個體** > **Forms** > **Forms與檔案**。
   * 按一下&#x200B;**建立** > **最適化表單**。
1. 在&#x200B;**來源**&#x200B;索引標籤中，選取基礎範本。
1. 在&#x200B;**資料**&#x200B;索引標籤中，選取&#x200B;**Adobe Experience Platform**&#x200B;選項。
1. 在屬性窗格中，選取您的雲端設定。

   ![](/help/forms/assets/xdm-schema-integration.png)

   系統會從Adobe Experience Platform載入所有可用的結構描述

   >[!NOTE]
   >
   >
   > * 只會擷取已啟用設定檔且非系統產生的結構描述。
   > * 首次設定時，初始結構描述載入可能需要一些時間。

1. 選取結構描述的適當/必要欄位。 （如需詳細步驟，請參閱影片）
1. 在提交索引標籤中：
   * 選取&#x200B;**提交至Adobe Experience Platform**&#x200B;提交動作
   * 設定&#x200B;**AEM Forms資料提交至Experience Platform**&#x200B;的表單提交設定
1. 在屬性窗格中：
   * 新增串流URL (取自「AEP來源>串流連線」)
   * 新增資料流程ID (可在AEP來源>流程> API使用資訊中找到)
1. 按一下「**儲存**」。提供表單詳細資料：
   * 標題
   * 名稱
   * 儲存路徑
1. 將提交按鈕新增至表單。 您的表單已準備好將資料提交至AEP。

>[!TAB 核心元件]

執行以下步驟，透過結構描述整合根據核心元件建立最適化表單：

1. 存取表單建立精靈：
   * 導覽至您的&#x200B;**Adobe Experience Manager執行個體** > **Forms** > **Forms與檔案**。
   * 按一下&#x200B;**建立** > **最適化表單**。
1. 在&#x200B;**來源**&#x200B;索引標籤中，選取以核心元件為基礎的範本。
1. 在&#x200B;**資料**&#x200B;索引標籤中，選取&#x200B;**Adobe Experience Platform**&#x200B;選項。
1. 在屬性窗格中，選取您的雲端設定。

   ![](/help/forms/assets/xdm-schema-integration.png)

   系統會從Adobe Experience Platform載入所有可用的結構描述

   >[!NOTE]
   >
   >
   > * 只會擷取已啟用設定檔且非系統產生的結構描述。
   > * 首次設定時，初始結構描述載入可能需要一些時間。

1. 選取結構描述的適當/必要欄位。 （如需詳細步驟，請參閱影片）
1. 在提交索引標籤中：
   * 選取&#x200B;**提交至Adobe Experience Platform**&#x200B;提交動作
   * 設定&#x200B;**AEM Forms資料提交至Experience Platform**&#x200B;的表單提交設定
1. 在屬性窗格中：
   * 新增串流URL (取自「AEP來源>串流連線」)
   * 新增資料流程ID (可在AEP來源>流程> API使用資訊中找到)
1. 按一下「**儲存**」。提供表單詳細資料：
   * 標題
   * 名稱
   * 儲存路徑
1. 將提交按鈕新增至表單。 您的表單已準備好將資料提交至AEP。

>[!TAB 通用編輯器]

執行以下步驟，透過結構描述整合來建立使用通用編輯器編寫的最適化表單：

1. 存取表單建立精靈：
   * 導覽至您的&#x200B;**Adobe Experience Manager執行個體** > **Forms** > **Forms與檔案**。
   * 按一下&#x200B;**建立** > **最適化表單**。
1. 在&#x200B;**來源**&#x200B;索引標籤中，選取Edge Delivery範本。
1. 在&#x200B;**資料**&#x200B;索引標籤中，選取&#x200B;**Adobe Experience Platform**&#x200B;選項。
1. 在屬性窗格中，選取您的雲端設定。

   ![結構描述整合](/help/forms/assets/xdm-schema-integration.png)

   系統會從Adobe Experience Platform載入所有可用的結構描述

   >[!NOTE]
   >
   >
   > * 只會擷取已啟用設定檔且非系統產生的結構描述。
   > * 首次設定時，初始結構描述載入可能需要一些時間。

1. 選取結構描述的適當/必要欄位。 （如需詳細步驟，請參閱影片）
1. 在提交索引標籤中：
   * 選取&#x200B;**提交至Adobe Experience Platform**&#x200B;提交動作
   * 設定&#x200B;**AEM Forms資料提交至Experience Platform**&#x200B;的表單提交設定

     >[!NOTE]
     >
     >* 如果您在Universal Editor介面中沒有看到「資料來源」圖示，或在右側屬性面板中沒有看到「繫結參考」屬性，請在Extension Manager中啟用&#x200B;**資料來源**&#x200B;擴充功能。
     >* 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
     > 
     > * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。

   通用編輯器目前不支援表單預填服務。

1. 在屬性窗格中：
   * 新增串流URL (取自「AEP來源>串流連線」)
   * 新增資料流程ID (可在AEP來源>流程> API使用資訊中找到)
1. 按一下「**儲存**」。提供表單詳細資料：
   * 標題
   * 名稱
   * 儲存路徑
1. 將提交按鈕新增至表單。 您的表單已準備好將資料提交至AEP。

>[!ENDTABS]

## 重要附註 {#important-notes}

* 透過表單提交的資料在約10-15分鐘後可在AEP中顯示
* 依預設，僅列出已啟用設定檔的結構描述
* 雖然資料提交適用於所有結構描述，但預填功能僅限於已啟用設定檔的結構描述
* 不會使用未啟用設定檔的結構描述中的資料來建立設定檔，即使稍後啟用此結構描述來進行設定檔分析亦然
* **使用表單資料擴充客戶設定檔**&#x200B;需要在您的XDM結構描述中進行適當的身分欄位設定
* **AEM Forms資料提交至Experience Platform**&#x200B;使用&#x200B;**AEP表單串流連線**&#x200B;以確保即時資料流量

## 最佳實務 {#best-practices}

1. 在啟用設定檔之前，請仔細規劃您的結構描述結構
1. 為表單&#x200B;**設定** AEP串流連線時，請考慮資料磁碟區和系統縮放需求
1. 在生產部署之前徹底測試整合
1. 監視資料擷取和設定檔建立流程
1. 設計您的&#x200B;**XDM結構描述與最適化表單**&#x200B;的整合，以僅收集必要的資料
1. 策略性地搭配表單資料&#x200B;**使用**&#x200B;客戶設定檔擴充，以強化個人化

## 技術考量 {#technical-considerations}

* 聯結器使用公開串流API來提交資料
* 設定檔建立是以身分欄位為基礎
* AEP會自動進行資料統一
* 此整合約時支援建立新表單和修改現有表單
* XDM結構描述與調適型表單的整合可標準化不同接觸點的資料結構
* 適用於表單的AEP串流連線提供即時資料擷取功能

## 常見問題集 (FAQ) {#faq}

### 一般問題 {#general-questions}

**問：「此聯結器是否適用於AEM Forms的多個方案？**
答：不需要。此整合僅適用於AEM Forms as a Cloud Service，並位於搶先存取計畫下。

**問：此聯結器是否可同時搭配最適化Forms核心元件與基礎元件使用？**
答：此聯結器可同時使用最適化Forms核心元件和最適化Forms基礎元件。

**問：我是否可從單一表單傳送資料至多個AEP資料集？**
答：目前每個表單只能提交至一個資料集。

**問：可以處理多少表單提交是有限制的？**
答：表單提交受限於您的AEP串流擷取[配額和速率限制](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/data-lifecycle/api/quota)。

<!-- 
>
**Q: Can form attachments be sent to AEP?**
A: No, form attachments cannot be directly sent to AEP. You would need to store attachments separately and only send metadata to AEP. -->

### 實作問題 {#implementation-questions}

**問：如何疑難排解AEM Forms和AEP之間的連線問題？**
答：驗證您的雲端組態設定，確保API憑證正確，並檢查串流端點URL是否已正確設定。

**問：我可以將此整合使用自訂XDM結構描述嗎？**
答：是，只要在AEP中正確設定，並為設定檔啟用預填功能，您就可以使用任何自訂XDM結構描述。

**問：如何使用AEP設定檔資料啟用表單預填功能？**
答：請確認您的結構描述已啟用設定檔功能，且您的表單已設定為使用結構描述中定義的相同身分欄位。

**問：如果我需要在將資料傳送到AEP之前轉換資料，該怎麼辦？**
答：您可以使用表單規則或自訂函式，在提交之前先轉換資料。 對於複雜的轉換，請考慮使用自訂提交動作。

**問：我可以在混合部署模式中使用此整合嗎？**
答：不需要。此整合專屬於AEM Forms as a Cloud Service。

## 摘要和後續步驟 {#summary-next-steps}

AEM Forms與Adobe Experience Platform的整合可讓組織在表單與更廣泛的Experience Platform生態系統之間建立順暢的資料流。 此整合可讓您建立更個人化的表單體驗、簡化資料收集，並透過有價值的表單提交資料來增強客戶設定檔。

若要開始使用這項整合：

1. **要求存取權** — 如果您尚未取得存取權，請連絡[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D)加入搶先存取計畫
2. **準備您的環境** — 確保您在AEM Forms和Adobe Experience Platform中擁有必要的許可權和設定
3. **遵循實作步驟** — 使用上述指南設定您的雲端設定，並透過XDM結構描述整合建立您的第一個AEP連線表單
4. **徹底測試** — 在開發環境中驗證資料提交和預填功能
5. **生產計畫** — 與您的實作團隊合作，排程在生產中將AEM Forms資料提交至Experience Platform的部署作業

## 相關資源 {#related-resources}

* [AEM Forms as a Cloud Service檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=zh-Hant)
* [Adobe Experience Platform檔案](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html?lang=zh-Hant)
* [XDM系統總覽](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant)
* [在Adobe Experience Platform中串流擷取](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=zh-Hant)
* [即時客戶個人檔案總覽](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=zh-Hant)
* [AEM Forms搶先存取功能](/help/forms/early-access-ea-features.md)
* [使用核心元件建立最適化Forms](/help/forms/creating-adaptive-form-core-components.md)
* [在AEM Forms中使用表單資料模型](/help/forms/using-form-data-model.md)

<!--
Schema markup for technical documentation
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "Connect AEM Forms with Adobe Experience Platform (AEP) | Data Integration Guide",
  "description": "Learn how to integrate AEM Forms with Adobe Experience Platform to leverage customer profiles, submit form data, and create personalized experiences.",
  "datePublished": "2025-05-28",
  "author": {
    "@type": "Corporation",
    "name": "Adobe"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Adobe Experience League",
    "logo": {
      "@type": "ImageObject",
      "url": "https://experienceleague.adobe.com/assets/img/favicons/apple-touch-icon.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/aem-forms-aep-connector.html"
  },
  "articleSection": "AEM Forms",
  "keywords": "AEM Forms, Adobe Experience Platform, XDM schema, data integration, form submission, customer profiles, personalization"
}
-->
