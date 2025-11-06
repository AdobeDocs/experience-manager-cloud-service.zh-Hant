---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.7.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.7.0 版發行說明。'
exl-id: 7866d94c-e54c-4bb2-aaa6-66c019e46336
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.7.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2023.7.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.7.0) 的發行日期為 2023 年 7 月 27 日。下一個功能版本 (2023.8.0) 預計於 2023 年 8 月 31 日發行。

## 發行影片 {#release-video}

請觀看 2023 年 7 月版本概觀影片，了解 2023.7.0 版本新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

* 內容片段的 MSM。AEM Multisite Manager 現在可用於內容片段，以便建立用於批次內容發佈的內容片段 Live Copies。精細的傳承控制可細化至內容片段元素和變體層級。

### [!DNL Experience Manager Sites] 發行前版本的新功能 {#prerelease-sites}

* [內容片段主控台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html)現在可讓使用者檢視標記，並依據作為中繼資料套用於內容片段的標記進行搜尋。使用者即不必再為了此功能而切換到資產 UI，減少了內容切換並提高了效率。

![在內容片段主控台中進行標記](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產檢視中的新功能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

 **影像智慧標記已改良的人工智慧框架**

Experience Manager Assets 現在為影像智慧標記使用改良的人工智慧框架。 此內容智慧可提高智慧標記的相關性和準確性，在擷取時可用於所有影像資產。

**設定「資產清單」視圖的資料欄顯示**

Assets Essentials 現在提供可選取顯示在「資產清單」視圖中的資料欄功能，例如「狀態」、「格式」、「維度」、「大小」等。

![設定資料欄](/help/release-notes/assets/configure-columns.png)

**根據相關性對為搜尋結果進行排序**

Assets Essentials 現在會根據相關性 (依預設) 為搜尋結果進行排序。您可以依照 `Name`、`Relevance`、`Size`、`Modified` 和 `Created` 的遞增或遞減順序排序搜尋的資產。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-forms-channel}

* [**現成可用的主題**](/help/forms/using-themes-in-core-components.md)**和範本**：使用我們現成的 OOTB 主題和範本啟動您的表單建立流程，這些主題和範本都是專為支援經驗豐富的專業人士和新表單作者量身打造。使用最適化表單元核心元件無縫建置的這些精心策劃的主題和範本，可讓您迅速地開始針對常見使用案例建立表單。

* **[Headless 表單的 React 元件](https://github.com/adobe/aem-forms-headless-components/tree/main/packages/react-vanilla-components)**：您現在可以使用現成的 React 元件預覽和自訂 Headless 最適化表單轉譯。這些元件會運用最適化表單核心元件中的 BEM 類別進行樣式設定，讓您能夠輕鬆地根據特定需求自訂其外觀。

* [**建立具有可重複區段的最適化表單**](/help/forms/create-forms-repeatable-sections.md)：您現在可製作可重複進行多筆資料紀錄擷取並以[折疊式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)、[精靈](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)、[面板](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)和[水平索引標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)元件為主的最適化表單。這些可重複的區段可讓您輕鬆提供多個資料條目。當無法事先知道需要多少份的資料時，這就非常有用。填表人可輕鬆新增或移除區段，使表單可依不同資料輸入情境進行調整，並簡化相同資料紀錄多次出現的收集作業。


### [!DNL Forms] 中可用的搶鮮版功能 {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA 企業支援**](/help/forms/captcha-adaptive-forms.md)：以最適化表單使用 Google reCAPTCHA 企業版，以針對詐欺活動和垃圾郵件提供增強的保護，進而提供更安全的使用者體驗。透過進階的風險分析和緊密整合，真實的使用者可輕鬆地提交表單，同時有效地封鎖機器人。

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### Headless 最適化表單早期採用者方案 {#forms-early-adopter}

使用 [Headless 最適化表單](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)讓您的開發人員能夠建立、發佈和管理可透過 API 存取和互動的互動式表單，而不是透過傳統的圖形使用者介面。Headless 最適化表單可協助您：

* 使用您選擇的程式語言建置高品質的多管道表單
* 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
* 在表單應用程式中重複使用您的專屬 UI 元件
* 使用 Adobe Experience Manager Forms 的強大功能

使用您的官方電子郵件 ID 寄送電子郵件至 `aem-forms-headless@adobe.com`，即可加入早期採用者方案。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 行動中心 {#actions-center}

訂閱電子郵件通知，可在發生需要立即採取行動的重大事件時提醒您，還能提供個人化的建議，讓您的網站發揮最大效益。[行動中心](/help/operations/actions-center.md)可作為提供服務的中心；您可以在此中心檢閱這些提醒內容，例如被封鎖的複寫佇列或即將到期的認證，並將它們標記為已解決。

![行動中心螢幕擷圖](/help/assets/assets/actions-center.png)

### CDN 和 WAF 規則早期採用者方案 {#waf-early-adopter}

在 CDN 篩選流量的根據：

* 要求的標頭和屬性 (例如 IP 位址)
* 已知和惡意流量相關的流量模式

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 **aemcs-waf-adopter@adobe.com**，深入了解有關早期採用者方案的資訊。名額有限。

若要深入了解該功能，請點選[這裡](/help/security/traffic-filter-rules-including-waf.md)參閱文章。

### 其他基礎變更 {#other-foundation-changes}

* 在 8 月 7 日這一週，對 AEM 執行個體的要求超出健全值時，AEM 會傳回錯誤代碼 429，而不是錯誤代碼 503。[深入了解](/help/implementing/developing/introduction/development-guidelines.md)。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
