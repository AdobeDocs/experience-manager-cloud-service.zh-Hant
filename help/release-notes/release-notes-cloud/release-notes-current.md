---
title: Adobe Experience Manager雲端服務版本注意事項2020.4.0
description: Experience Manager 2020.4.0發行說明
translation-type: tm+mt
source-git-commit: b05fe7e9150649b49fc5dae2e33955afc6a1acab

---


# Release Notes for Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

The following section outlines the general release notes for [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Release Date {#release-date}

雲端服務2020.4.0 [!DNL Experience Manager] 的發行日期為2020年4月9日。

## What&#39;s New in Assets {#assets}

瞭解目前版本的新功能、增強功能 [!DNL Experience Manager Assets] 和 [!DNL Dynamic Media] 錯誤修正。

* [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) 支援Experience Manager Assets的資產分發使用案例。 [!DNL Brand Portal] 藉由安全方式向外部機構、合作夥伴、內部團隊和經銷商散佈經過核准的品牌和產品資產以供下載，協助組織滿足其行銷需求。
   * [!DNL Brand Portal] 配置通過控制台 [!DNL Adobe I/O] 完成。
   * Experience Manager作為雲 [!DNL Brand Portal] 端服務尚不支 [!DNLE] 援中的資產採購。

* [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) v2.0可搭配雲 [!DNL Experience Manager] 端服務運作。 [!DNL Adobe Asset Link] 透過連接案頭應用程式和應用程式內面板，簡化創意人員與行銷人員 [!DNL Experience Manager Assets] 在內容建 [!DNL Creative Cloud] 立程式 [!DNL Adobe Photoshop]中的協作 [!DNL Adobe Illustrator]作業，並 [!DNL Adobe InDesign] 簡化應用程式內 [!DNL Asset Link] 面板。
   * [!DNL Experience Manager] 已預先設定， [!DNL Adobe Asset Link]可讓您輕鬆 [設定](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) ，並更快速地向創意專業人員推展。
   * [!DNL Asset Link] 現在支援 [Experience Manager環境切換器](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) ，讓創意使用者輕鬆連接至不同的 [!DNL Experience Manager] 環境。 此功能有用的範例是，對於使用不同部署與多個客戶合作的機構設計 [!DNL Experience Manager Assets] 人員。

* 使用者可以 [設定後處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) ，以在特定資料夾階層的資料夾  屬性使用者介面中自動啟動。
   * 資料夾 [!UICONTROL 「屬性] 」使用者介面已簡化，新的「資產處理」標籤包含中繼資料描述檔、處理描述檔，以及新的自動啟動工作流程設定。
   * 資產重新處理對話框允許選擇特定的處理配置檔案並決定在子資料夾中重新處理。
   * [!DNL Dynamic Media]:已新增選擇性發佈設定，如此資產就會自動發佈，以便僅安全預覽。 此外，資產可明確發佈至Experience Manager，而不發佈至DMS7，以便在公共網域中傳送。

* 已解決下列問題：
   * 資產處理問題的修正。
   * 設定和 [!DNL Dynamic Media] 發佈資產至傳送服務 [!DNL Dynamic Media] 的修正。

>[!MORELIKETHIS]
>
>* [關於Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [設定品牌入口網站](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [設定Experience Manager以搭配資產連結運作](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [在Experience Manager中使用Assets microservices建立工作流程](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)

