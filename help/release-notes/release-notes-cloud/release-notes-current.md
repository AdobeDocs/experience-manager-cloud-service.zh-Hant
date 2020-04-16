---
title: Adobe Experience Manager雲端服務版本注意事項2020.4.0
description: Experience Manager 2020.4.0發行說明
translation-type: tm+mt
source-git-commit: 98de3a6674aaef5228e96e0bf72e67de861f858e

---


# Release Notes for Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

The following section outlines the general release notes for [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Release Date {#release-date}

雲端服務2020.4.0 [!DNL Experience Manager] 的發行日期為2020年4月9日。

## What&#39;s New in Assets {#assets}

瞭解目前版本的新功能、增強功能 [!DNL Experience Manager Assets] 和 [!DNL Dynamic Media] 錯誤修正。

* [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) 支援Experience Manager Assets的資產分發使用案例。 [!DNL Brand Portal] 藉由安全方式向外部機構、合作夥伴、內部團隊和經銷商散佈經過核准的品牌和產品資產以供下載，協助組織滿足其行銷需求。
   * [!DNL Brand Portal] 配置通過控制台 [!DNL Adobe I/O] 完成。 請參 [閱設定品牌入口網站](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)。
   * 雲端服務尚 [!DNL Brand Portal] 未支援中的資 [!DNL Experience Manager] 產來源補充。

* [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) v2.0可搭配雲 [!DNL Experience Manager] 端服務運作。 [!DNL Adobe Asset Link] 透過連接案頭應用程式和應用程式內面板，簡化創意人員與行銷人員 [!DNL Experience Manager Assets] 在內容建 [!DNL Creative Cloud] 立程式 [!DNL Adobe Photoshop]中的協作 [!DNL Adobe Illustrator]作業，並 [!DNL Adobe InDesign] 簡化應用程式內 [!DNL Asset Link] 面板。
   * [!DNL Experience Manager] 已預先設定， [!DNL Adobe Asset Link]可讓您輕鬆 [設定](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) ，並更快速地向創意專業人員推展。
   * [!DNL Asset Link] 現在支援 [Experience Manager環境切換器](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) ，讓創意使用者輕鬆連接至不同的 [!DNL Experience Manager] 環境。 此功能有用的範例是，對於使用不同部署與多個客戶合作的機構設計 [!DNL Experience Manager Assets] 人員。

* 使用者可以 [設定後處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) ，以在特定資料夾階層的資料夾  屬性使用者介面中自動啟動。
   * 資料夾 [!UICONTROL 「屬性] 」使用者介面已簡化，新的「資產處理」標籤包含中繼資料描述檔、處理描述檔，以及新的自動啟動工作流程設定。

      ![處理設定檔可輕鬆套用至資料夾，而且所有上傳至資料夾的資產都可使用這些設定檔來處理](/help/assets/assets/asset-processing-folder-properties.png)

   * 資產重新處理選項允許選擇特定的處理設定檔，以重新處理子資料夾中使用者選取的資產。

      ![使用特定處理設定檔重新處理選取的資產](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]:已新增選擇性發佈設定，如此資產就會自動發佈，以便僅安全預覽。 此外，資產可明確發佈至Experience Manager，而不發佈至DMS7，以便在公共網域中傳送。

### 錯誤修正 {#assets-bug-fixes}

* 資產處理問題的修正。
* 設定和 [!DNL Dynamic Media] 發佈資產至傳送服務 [!DNL Dynamic Media] 的修正。

>[!MORELIKETHIS]
>
>* [關於Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [設定品牌入口網站](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [設定Experience Manager以搭配資產連結運作](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [在Experience Manager中使用Assets microservices建立工作流程](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Cloud Manager的新增功能 {#whats-new-cloud-manager}

* Cloud Manager UI的「環境」頁面現在提供發佈者URL。
* 對導覽的變更，可讓使用者從Cloud Manager概述頁面編輯、切換或新增程式。
* 變更可讓使用者從Cloud Manager登陸頁面上的程式卡編輯程式。
* 新管線狀 **態「管線運行** 」(Pipeline Running)對其關聯的環境顯示。
* 管道執行頁面的增強功能。 這包括顯示管線名稱（僅限非生產管線）和類型，以及指示管線狀態為「進行中／已取消／失敗」的徽章。
* 工具提示，可改善使用者體驗，並瞭解為何停用「新增程式／環境」按鈕。
* 現在可以透過UI和API刪除失敗的環境。
* 用來產生Git密碼的程式對底層服務層中的問題具有更強的適應能力。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 管線執行詳細資訊頁面上到舞台環境的連結不能始終導航到正確的位置。
* 環境建立進程中的各個步驟將比需要的時間提前超時，導致進程失敗。
* 已更新建置容器中使用的Maven組態，以避免在下載對象中繼資料時造成死鎖。
* 在某些情況下，「建立影像」步驟將無法成功下載客戶套件。
* 某些不常發生的情況將阻止刪除環境。
* 未一致收到Experience Cloud通知。
