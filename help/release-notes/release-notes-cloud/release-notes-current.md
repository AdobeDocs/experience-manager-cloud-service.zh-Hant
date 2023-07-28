---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 5995c416328e6f340285004ec2e723cc9279dabd
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 41%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本(2023.7.0)為2023年7月27日。 下一個功能版本(2023.8.0)計畫於2023年8月31日發行。

## 發行影片 {#release-video}

請觀看2023年7月版本概觀影片，瞭解2023.7.0版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

* 內容片段的MSM。 AEM Multisite Manager現在可用於內容片段，允許建立內容片段即時副本以進行大量內容發佈。 精細繼承控制項可向下提供至內容片段元素和變數層級。

### [!DNL Experience Manager Sites] 發行前版本的新功能 {#prerelease-sites}

* 此 [內容片段主控台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=zh-Hant) 現在可讓使用者檢視標籤，並按套用為內容片段中繼資料的標籤進行搜尋。 使用者無需再切換至Assets UI即可使用此功能，減少內容切換並提高效率。

![在內容片段控制檯中標籤](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產檢視中的新功能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

**改善影像智慧標籤的人工智慧架構**

Experience Manager Assets 現在為影像智慧標記使用改良的人工智慧框架。 此內容智慧可提高智慧標記的相關性和準確性，在擷取時可用於所有影像資產。

**設定「資產清單」檢視的欄顯示**

Assets Essentials現在提供選取「資產清單」檢視中顯示的欄的功能，例如狀態、格式、Dimension、大小等。

![設定欄](/help/release-notes/assets/configure-columns.png)

**根據相關性排序搜尋結果**

依預設，Assets Essentials現在會根據關聯性來排序搜尋結果。 您可以依照 `Name`、`Relevance`、`Size`、`Modified` 和 `Created` 的遞增或遞減順序排序搜尋的資產。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-forms-channel}

* [**現成主題**](/help/forms/using-themes-in-core-components.md) **和範本**：透過我們現成可用的OOTB主題和範本，啟動您的表單建立流程，量身打造以增強經驗豐富的專業人員和新表單作者的能力。 使用最適化Forms核心元件建立後，透過這些精心策劃的主題和範本，您可以快速建立適用於常見使用案例的表單。

  ![現成可用的範本](/help/forms/assets/form-templates-ootb.png)

* **Headless Forms的React元件**：您現在可以使用現成可用的React元件預覽和自訂Headless最適化表單轉譯。 這些元件利用最適化Forms核心元件的BEM類別進行樣式設定，讓您輕鬆根據特定需求自訂其外觀。

* [**使用可重複區段建立最適化Forms**](/help/forms/create-forms-repeatable-sections.md)：您現在可以製作 [摺疊面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)， [精靈](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)， [面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)、和 [水準索引標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) 適用於多筆資料記錄擷取的元件式最適化表單。  這些可重複的區段可讓您輕鬆提供多個資料專案。 當無法事先知道需要多少份的資料時，這就非常有用。表單填寫器可輕鬆新增或移除區段，使表單能適應不同的資料輸入情境，並簡化相同資料記錄多次出現次數的收集。


### 中可用的搶鮮版功能 [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA企業支援**](/help/forms/captcha-adaptive-forms.md)：在最適化表單中使用Google reCAPTCHA Enterprise，針對詐騙活動和垃圾郵件提供增強型保護，提供更安全的使用者體驗。 透過進階風險分析及緊密整合，正版使用者可輕鬆提交表單，同時有效封鎖機器人。

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### Headless 最適化表單早期採用者計畫 {#forms-early-adopter}

使用 [Headless 最適化表單](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)讓您的開發人員能夠建立、發佈和管理可透過 API 存取和互動的互動式表單，而不是透過傳統的圖形使用者介面。Headless 最適化表單可協助您：

* 使用您選擇的程式語言建置高品質的多管道表單
* 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
* 在表單應用程式中重複使用您的專屬 UI 元件
* 使用 Adobe Experience Manager Forms 的強大功能

使用您的官方電子郵件 ID 寄送電子郵件至 `aem-forms-headless@adobe.com`，即可加入早期採用者計畫。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 行動中心 {#actions-center}

訂閱電子郵件通知，在發生需要立即採取行動的嚴重事件時提醒您，並提供個人化建議以最佳化您的網站。 [動作中心](/help/operations/actions-center.md) 可做為中心，讓您檢閱這些警示（例如封鎖的復寫佇列或即將到期的認證），並將它們標示為已解決。

![動作中心熒幕擷圖](/help/assets/assets/actions-center.png)

### CDN和WAF規則早期採用者計畫 {#waf-early-adopter}

根據以下條件篩選CDN的流量：
* 請求標頭和屬性（例如IP位址）
* 已知與惡意流量相關聯的流量模式

有興趣試用此功能並分享意見回饋嗎？ 傳送電子郵件至 **aemcs-waf-adopter@adobe.com** 從您的官方電子郵件ID瞭解有關早期採用者計畫的更多資訊。 空間有限。

進一步瞭解文章中的功能 [此處](/help/security/cdn-and-waf-rules.md).

### 其他基礎變更 {#other-foundation-changes}

* 在8月7日當週，當AEM執行個體的請求超過正常程度時，AEM會傳回錯誤代碼429，而非錯誤代碼503。 [深入了解](/help/implementing/developing/introduction/development-guidelines.md).

## 維護版本發行說明 {#maintenance}

您可以在[此處](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
