---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.12.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.12.0 版發行說明。'
exl-id: b36add58-a2ba-4299-94be-e0026e9c553c
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 93%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.12.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2023.12.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hant)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hant)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本 (2023.12.0) 的發行日期是 2023 年 12 月 14 日。下一個功能版本 (2024.1.0) 規劃於 2024 年 1 月 25 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the December 2023 Release Overview video for a summary of the features added in the 2023.12.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期採用者計劃 {#sites-early-adopter}

**您可以利用[作業遙測服務](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**&#x200B;來啟用AEM as a Cloud Service的使用者端集合。

作業遙測資料服務可更精確地反映使用者互動，確保網站互動的可靠測量。 這是深入了解頁面效能的絕佳機會。這對於使用 Adobe 管理 CDN 或非 Adobe 管理 CDN 的客戶很有幫助。此外，對於使用非 Adobe 管理 CDN 的客戶，現在可以啟用自動流量報告，而無需與 Adobe 共享任何流量報告。

如果您有興趣測試此新功能並分享意見反應，請使用與您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `aemcs-rum-adopter@adobe.com`，並在電子郵件中附上生產、階段和開發環境的網域名稱。Adobe的產品團隊會接著為您啟用作業遙測資料服務。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產檢視中的新功能 {#assets-view-features}

**使用 Adobe Firefly 建立 GenAI 影像**

透過整合 Adobe Firefly 以文字建立影像功能 (需要 Adobe Firefly 授權)，根據搜尋查詢建立新影像。

![Assets Firefly 整合](/help/assets/assets/assets-firefly-integration.png)

**尋找類似影像**

現在，您可以透過選取影像並在 Experience Manager Assets 存放庫中查看類似影像來輕鬆找到內容。

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)


**Video Preview**: AEM Assets now generates preview renditions of all supported video formats by default, without the need to configure a processing profile.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新功能 {#forms-features}

* **[將最適化表單與 Microsoft® SharePoint 清單連接](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**：AEM Forms 提供 OOTB 整合，可將表單資料直接提交到 SharePoint 清單，讓您使用 SharePoint 清單功能。您可以將 Microsoft SharePoint 清單設定為表單資料模型的資料來源，並透過&#x200B;**使用表單資料模型提交**&#x200B;這個提交動作，將最適化表單與 SharePoint 清單連接。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期採用者計劃 {#forms-early-adopter}

* **[將最適化表單提交到 Adobe Workfront Fusion 情境](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Forms as a Cloud Service 提供開箱即用的選項，可輕鬆將最適化表單與 Adobe Workfront 連接。這簡化了將最適化表單提交到 Adobe Workfront 情境的程序，讓您在提交最適化表單時觸發 Workfront Fusion 情境。

* **[從右至左語言支援](/help/forms/supporting-new-language-localization-core-components.md)**：以核心元件為主的最適化表單現在可以呈現從右至左 (RTL) 語言 (如阿拉伯文、波斯文和烏都文)。全球有超過 20 億人使用 RTL 語言。使用 RTL 語言的表單可讓您擴展最適化表單的範圍，以滿足這些不同的客群並選擇進入 RTL 市場。在某些地區，法律也強制要求以當地語言提供表單。透過適應當地語言，您不僅可以向更廣泛的客群敞開大門，還可以確保遵守相關法律和法規。

  ![從右至左語言支援](/help/forms/assets/right-to-left-language-support.png)

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-ea@adobe.com`，加入早期採用者計畫並要求存取該功能。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 網域對應早期採用者計畫 {#cdn-config-early-adopter}

除了最近發佈的[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) (其中包含可以選擇授權的 Web 應用程式防火牆 (WAF) 規則)，也可以使用設定管道來聲明及部署其他類型的 CDN 設定。我們很想聽聽您的使用案例，包括：

* 301/302 用戶端重新導向
* 將邊緣要求代理到任意來源
* URL 轉換
* 設定或修改要求或回應標頭
* CDN 無法連接 AEM 時的自訂錯誤頁面
* 透過使用者名稱/密碼進行身份驗證
* 任何其他有用的 CDN 設定

使用您的官方電子郵件 ID 將您的回饋意見透過電子郵件寄送至：**aemcs-cdn-config-adopter@adobe.com**。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
