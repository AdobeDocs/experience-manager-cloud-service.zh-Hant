---
title: 2020.4.0 版發行說明
description: 2020.4.0 版發行說明
translation-type: tm+mt
source-git-commit: c6c0e93d881762a2b501abb3d8c8356046a5f082

---


# AEM 雲端服務 2020.4.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.4.0 版的一般發行說明。

## Release Date {#release-date}

Experience Manager作為Cloud Service 2020.4.0的發行日期為2020年4月9日。

## 資產 {#assets}

請依照本節內容，瞭解AEM中Experience Manager Assets和Dynamic Media的新增功能和更新，即雲端服務版本2020.4.0。

### 新功能 {#assets-what-is-new}

* [品牌入口網站](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) (Brand Portal)是以雲端服務資產形式提供給AEM，可支援資產散發使用案例。 Brand Portal 藉由安全方式向外部機構、合作夥伴、內部團隊和經銷商散佈經過核准的品牌和產品資產以供下載，協助組織滿足其行銷需求。
   * 品牌入口網站的設定是透過Adobe I/O主控台完成
   * AEM雲端服務尚未支援品牌入口網站中的資產採購
* AEM雲端服務 [支援新版Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) 2.0。 Adobe Asset Link透過應用程式內資產連結面板，將AEM Assets與Creative Cloud案頭應用程式Photoshop、Illustrator和InDesign連接，簡化了創意人員與行銷人員在內容建立程式中的協作。
   * AEM為雲端服務已預先設定為Adobe Asset Link，可簡化 [設定](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)。
   * Asset Link現在支援 [AEM環境切換器](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)，讓創意使用者更輕鬆地連線至不同的AEM環境（例如，當機構設計人員與多個客戶搭配使用AEM資產時）
* 在資料夾屬性UI中 [可針對特定資料夾階層](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) ，設定後處理工作流程的自動啟動。
   * 資料夾屬性UI已經簡化，新的「資產處理」標籤包含中繼資料設定檔、處理設定檔和新的「自動啟動工作流程」設定
* 資產重新處理對話框允許選擇特定的處理配置檔案並決定在子資料夾中重新處理
* 動態媒體：新增「選擇性發佈」設定，這表示資產會自動發佈，僅提供安全預覽，而且可明確發佈至AEM，而不需發佈至DMS7，以便在公共網域中傳送。

### 錯誤修正 {#assets-bug-fixes}

* 資產處理中的修正
* 動態媒體設定中的修正，以及將資產發佈至動態媒體傳送服務
