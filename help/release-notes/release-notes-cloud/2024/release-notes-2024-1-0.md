---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.1.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.1.0 版發行說明。'
exl-id: 9f5d97c6-6536-4593-acbf-cbe8bf9b5eeb
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 89%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.1.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2024.1.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hant)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hant)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本 (2024.1.0) 的發行日期是 2024 年 1 月 25 日。 下一個功能版本 (2024.3.0) 預計於 2024 年 4 月 11 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2024 年 1 月發行概觀影片，了解 2024.1.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AEM Sites 的 Extension Manager {#sites-extension-manager}

**探索 [&#x200B; AEM Sites 的全新 Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)** ，透過設定 UI 擴充功能為您的 AEM 設定進行個人化。

![AEM Sites 的 Extension Manager](/help/assets/sites/extension-manager/homepage.png)

AEM Sites 中的 Extension Manager 可讓開發人員和從業人員存取、管理和自訂 [UI 擴充功能](https://developer.adobe.com/uix/docs/)；此功能是透過 [Adobe 應用程式建立工具](https://developer.adobe.com/app-builder/)所建立，可增強 AEM Sites 的功能。
Extension Manager 可讓您：

* 根據每個實例啟用或停用擴充功能；
* 設定擴充功能參數；
* 預覽擴充功能並產生可分享的預覽連結；
* 透過互動式示範，探索 UI 可擴充性功能；
* 透過第一方擴充功能來存取 Adobe 的實驗性功能。

我們現正積極尋求對於 UI 擴充功能的意見回饋和新使用案例。如果您想聯繫我們，請發送電子郵件至 `uix@adobe.com`。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理員檢視的發行前功能 {#admin-view-prerelease}

**預覽所有支援影片類型的轉譯版**

Experience Manager Assets 現在會依預設產生所有支援影片類型的預覽轉譯，而無需處理設定檔的設定

### 資產檢視 {#assets-view-features}

**智慧標記封鎖清單**

Assets Essentials 現在允許您定義封鎖清單，其中包含上傳到存放庫時，不應當成智慧標記上傳到資產的單詞。此功能可協助您維持品牌合規性，並減少審核智慧標記的工作量。

![智慧標記封鎖清單](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期採用者計劃 {#forms-early-adopter}

* **[將最適化表單提交到 Adobe Workfront Fusion 情境](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Forms as a Cloud Service 提供開箱即用的選項，可輕鬆將最適化表單與 Adobe Workfront 連接。這簡化了將最適化表單提交到 Adobe Workfront 情境的程序，讓您在提交最適化表單時觸發 Workfront Fusion 情境。

* **[從右至左語言支援](/help/forms/supporting-new-language-localization-core-components.md)**：以核心元件為主的最適化表單現在可以呈現從右至左 (RTL) 語言 (如阿拉伯文、波斯文和烏都文)。全球有超過 20 億人使用 RTL 語言。使用 RTL 語言的表單可讓您擴展最適化表單的範圍，以滿足這些不同的客群並選擇進入 RTL 市場。在某些地區，法律也強制要求以當地語言提供表單。透過適應當地語言，您不僅可以向更廣泛的客群敞開大門，還可以確保遵守相關法律和法規。

  ![從右至左語言支援](/help/forms/assets/right-to-left-language-support.png)

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-early-adopter-program@adobe.com`，加入早期採用者計畫並要求存取該功能。

* **[您可以利用作業遙測服務](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**&#x200B;來啟用AEM as a Cloud Service的使用者端集合。
作業遙測服務可更精確地反映使用者互動，確保網站互動的可靠測量。 這是深入了解頁面效能的絕佳機會。這對於使用 Adobe 管理 CDN 或非 Adobe 管理 CDN 的客戶很有幫助。此外，對於使用非 Adobe 管理 CDN 的客戶，現在可以啟用自動流量報告，而無需與 Adobe 共享任何流量報告。

  如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至`aemcs-rum-adopter@adobe.com`，連同您想要從與Adobe ID關聯的電子郵件地址為每個環境啟用作業遙測的網域名稱。 Adobe的產品團隊會接著為您啟用作業遙測服務。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### Dynatrace 的支援 {#dynatrace}

Dynatrace 客戶可以監控他們的 AEM 使用情況。[了解如何](/help/implementing/cloud-manager/dynatrace.md)請求與您的 Dynatrace 環境連接以進行應用程式效能監控。請注意，如果啟用 Dynatrace，可供所有客戶使用的 New Relic APM 將停止收集資料。

### 使用網站主題和網站範本對前端程式碼的 RDE 支援：早期採用者計劃 {#rde-frontend-early-adopter}

[快速開發環境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 現在支援以[網站主題](/help/sites-cloud/administering/site-creation/site-themes.md)和[網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)為主的前端程式碼 (適用於早期採用者)。對於 RDE，這是使用命令列指令完成，而不是使用 [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)來完成。請聯絡 **aemcs-rde-support@adobe.com**，可嘗試使用並提供意見回饋。

### 網域對應早期採用者計畫 {#cdn-config-early-adopter}

除了最近發佈的[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) (其中包含可以選擇授權的 Web 應用程式防火牆 (WAF) 規則)，也可以使用設定管道來聲明及部署[其他類型的 CDN 設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)。透過寄送電子郵件給&#x200B;**`aemcs-cdn-config-adopter@adobe.com`**&#x200B;加入早期採用者計畫，以取得：

* 301/302 用戶端重新導向
* 將邊緣要求代理到任意來源
* URL 轉換
* 設定或修改要求或回應標頭
* CDN 無法連接 AEM 時的自訂錯誤頁面

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
