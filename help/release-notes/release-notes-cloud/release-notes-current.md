---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 8c33426c38b087c83b945572374089ad9cb44daf
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 64%

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

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本(2024.1.0)為2024年1月25日。 下一個功能版本(2024.2.0)計畫於2024年2月29日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2024 年 1 月發行概觀影片，了解 2024.1.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AEM Sites中的Extension Manager {#sites-extension-manager}

**探索新的 [AEM Sites中的Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)** 透過設定UI擴充功能來個人化AEM設定。

![AEM Sites中的Extension Manager](/help/assets/sites/extension-manager/homepage.png)

AEM Sites中的Extension Manager可讓開發人員和從業人員存取、管理和自訂UI擴充功能，這些擴充功能是用來增強AEM Sites的功能。
使用Extension Manager，您可以：

* 為每個執行個體啟用或停用擴充功能；
* 設定擴充功能引數；
* 預覽擴充功能並產生可共用的預覽連結；
* 透過互動式示範探索UI擴充功能；
* 透過第一方擴充功能存取Adobe的實驗性功能。

我們正在積極搜尋UI擴充功能的意見與新使用案例。 如果您想要連線，請傳送電子郵件至 `uix@adobe.com`.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理員檢視發行前功能 {#admin-view-prerelease}

**預覽所有支援視訊型別的轉譯**

Experience Manager Assets現在預設會產生所有支援視訊型別的預覽轉譯，不需要處理設定檔設定

### 資產檢視 {#assets-view-features}

**智慧標記封鎖清單**

Assets Essentials 現在允許您定義封鎖清單，其中包含上傳到存放庫時，不應當成智慧標記上傳到資產的單詞。此功能可協助您維持品牌合規性，並減少審核智慧標記的工作量。

![智慧標籤封鎖清單](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期採用者計劃 {#forms-early-adopter}

* **[將最適化表單提交到 Adobe Workfront Fusion 情境](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Forms as a Cloud Service 提供開箱即用的選項，可輕鬆將最適化表單與 Adobe Workfront 連接。這簡化了將最適化表單提交到 Adobe Workfront 情境的程序，讓您在提交最適化表單時觸發 Workfront Fusion 情境。

* **[從右至左語言支援](/help/forms/supporting-new-language-localization-core-components.md)**：以核心元件為主的最適化表單現在可以呈現從右至左 (RTL) 語言 (如阿拉伯文、波斯文和烏都文)。全球有超過 20 億人使用 RTL 語言。使用 RTL 語言的表單可讓您擴展最適化表單的範圍，以滿足這些不同的受眾並選擇進入 RTL 市場。在某些地區，法律也強制要求以當地語言提供表單。透過適應當地語言，您不僅可以向更廣泛的受眾敞開大門，還可以確保遵守相關法律和法規。

  ![從右至左語言支援](/help/forms/assets/right-to-left-language-support.png)

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-early-adopter-program@adobe.com`，加入早期採用者計畫並要求存取該功能。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 支援Dynatrace {#dynatrace}

Dynatrace客戶可監控其AEM使用情況。 [瞭解如何](/help/implementing/cloud-manager/dynatrace.md) 請求與您的Dynatrace環境連線，以進行應用程式效能監控。 請注意，如果啟用Dynatrace，則可供所有客戶使用的New Relic APM將停止收集資料。

### 使用網站主題和網站範本的前端計畫碼RDE支援：早期採用者計畫 {#rde-frontend-early-adopter}

[快速開發環境(RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 現在支援的前端程式碼，根據 [網站主題](/help/sites-cloud/administering/site-creation/site-themes.md) 和 [網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)，適用於早期採用者。 若使用RDE，這是使用命令列指示詞完成的，而非 [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). 請聯絡 **aemcs-rde-support@adobe.com** 進行試用並提供意見反應。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
