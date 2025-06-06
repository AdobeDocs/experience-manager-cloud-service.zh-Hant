---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.8.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.8.0 版發行說明。'
exl-id: 0eff8100-5990-4553-8373-445fb7e6fb27
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 56%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2022.8.0 版發行說明 {#release-notes}

以下章節概述2022.8.0版[!DNL Experience Manager]as a Cloud Service的功能發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hant)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service]目前版本(2022.8.0)的發行日期為2022年9月1日。
下一個版本(2022.10.0)計畫於2022年11月10日發行。

## 發行影片 {#release-video}

請觀看 2022 年 8 月發行概觀影片，了解 2022.8.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新功能 {#sites-features}

* 電子郵件元件可讓您在AEM中建立內容，然後透過Campaign Classic將其傳遞為電子郵件。 核心電子郵件元件：
   * 是以[核心WCM元件](https://github.com/adobe/aem-core-wcm-components)為基礎，該元件支援可編輯的範本和樣式系統。
   * 提供10個電子郵件最佳化的立即可用元件（頁面、容器、標題、文字、影像、按鈕、Teaser、體驗片段、內容片段、分段）。
   * 提供進階個人化與分段，這要歸功於大多數對話方塊欄位上的[Campaign變數](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization)插入以及彈性的[分段元件](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation))。
   * 提供最佳的電子郵件易用HTML輸出，這要歸功於[CSS樣式內嵌器](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)、[HTML屬性內嵌器](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)和[HTML清理程式](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation)。
   * 可讓您隨處建立電子郵件。

### [!DNL Sites] 發行前通道中可用的新功能 {#prerelease-features-sites}

* [內容片段主控台](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)為使用者提供一個選項，以顯示與內容片段相關的語言副本總數。 另外提供一鍵式存取，以便檢視所有語言版本。 使用者也可以依照他們感興趣的地區設定來篩選表格檢視。

![內容片段語言](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#features-assets}

* 您現在可以將Adobe Experience Manager Assets設定為[根據MIME型別](/help/assets/configure-asset-upload-restrictions.md)限制使用者可以上傳的資產型別。

  ![資產上傳限制](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 發行前通道中可用的新功能 {#prerelease-features-forms}

* [調適型表單精靈](/help/forms/creating-adaptive-form.md)：AEM Forms 為商業使用者提供好用的精靈，以便快速撰寫調適型表單。 此精靈具有快速索引標籤導覽，可輕鬆選取預先設定的範本、樣式、欄位和提交選項來建立調適型表單。 此版本引進了對此精靈的以下改良：

   * 選取或取消選取欄位：此精靈可讓您根據JSON和表單資料模型結構描述建立調適型表單。 您現在可以選取結構描述中的欄位子集以納入調適型表單中。 選取的欄位會轉換成對應的調適型表單資料結構元件，以快速建立所需的調適型表單。

   * 使用靜態範本：已投資於舊型靜態範本的客戶可以在此精靈中使用靜態範本來撰寫調適型表單，繼續他們的雲端採用之旅。 這讓客戶有更多時間可以將舊的靜態範本移轉到可編輯的新式範本。

* [在伺服器端進行處理時從記錄文件 (DoR) 中移除隱藏欄位](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)：您可以為一般使用者產生記錄文件 PDF，檔案中僅包含他們在資料擷取體驗期間可以看到的那些欄位。 在提交表單時，伺服器會根據提交的資料驗證哪些欄位已對使用者隱藏，並從記錄檔案中排除以達到一致性。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 透過AEM頁面屬性以及產品主控室中的概觀，將AEM頁面與產品和類別相關聯
  ![產品駕駛艙頁面關聯](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
