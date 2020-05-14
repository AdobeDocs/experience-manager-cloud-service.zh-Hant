---
title: Adobe Experience Manager 雲端服務 2020.4.0 版發行說明
description: Experience Manager 2020.4.0 版發行說明
translation-type: tm+mt
source-git-commit: 94a732f56929ad4af23855152e258f82ad61ee2c
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 100%

---


# Adobe Experience Manager 雲端服務 2020.4.0 版發行說明 {#release-notes}

以下章節概述 雲端服務 2020.4.0 版的一般發行說明。[!DNL Experience Manager]

## 發行日期 {#release-date}

[!DNL Experience Manager] 雲端服務 2020.4.0 版的發行日期為 2020 年 4 月 9 日。

## 新增資產 {#assets}

瞭解目前版本的新功能、增強功能，以及 [!DNL Experience Manager Assets] 和 [!DNL Dynamic Media] 的錯誤修正。

* [Brand Portal](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/home.html) 支援 Experience Manager Assets 的資產發佈使用案例。[!DNL Brand Portal] 藉由安全方式向外部機構、合作夥伴、內部團隊和經銷商散佈經過核准的品牌和產品資產以供下載，協助組織滿足其行銷需求。
   * [!DNL Brand Portal] 設定已透過 [!DNL Adobe I/O] 控制台完成。請參閱[設定 Brand Portal](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)。
   * [!DNL Experience Manager] 雲端服務尚不支援 [!DNL Brand Portal] 的資產來源取得。

* [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) v2.0 可搭配 [!DNL Experience Manager] 雲端服務運作。透過經由應用程式內的 [!DNL Asset Link] 面板來連接 [!DNL Experience Manager Assets] 與 [!DNL Creative Cloud] 桌面應用程式 [!DNL Adobe Photoshop]、[!DNL Adobe Illustrator] 和 [!DNL Adobe InDesign]，[!DNL Adobe Asset Link] 可簡化創意人員與行銷人員在內容建立過程中的協作。
   * [!DNL Experience Manager] 已針對 [!DNL Adobe Asset Link] 完成預先設定，因此您可[輕鬆進行設定](https://helpx.adobe.com/tw/enterprise/using/configure-aem-assets-for-asset-link.html) ，並加快交接給創意專家。
   * [!DNL Asset Link] 現已支援 [Experience Manager 環境切換程式](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)，方便創意人員輕鬆連接至不同的 [!DNL Experience Manager] 環境。事務所設計師需要透過不同部署 [!DNL Experience Manager Assets] 與多家客戶合作時，這項功能就會非常實用。

* 使用者可以設定[處理後工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)，以便針對特定資料夾階層在資料夾[!UICONTROL 屬性]使用者介面中自動啟動。
   * 資料夾[!UICONTROL 屬性]使用者介面經過簡化，當中的全新[!UICONTROL 資產處理]標籤包含中繼資料設定檔、處理設定檔和新的自動啟動工作流程設定。

      ![處理設定檔可輕鬆套用至資料夾，所有上傳至資料夾的資產都可使用這些設定檔來處理](/help/assets/assets/asset-processing-folder-properties.png)

   * 資產重新處理選項可讓您選取特定的處理設定檔，以重新處理子資料夾中使用者所選取的資產。

      ![使用特定處理設定檔重新處理選取的資產](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]：新增選擇性發佈設定，方便資產僅供安全預覽而自動發佈。此外，資產可明確發佈至 Experience Manager，無需發佈至 DMS7 再於公共網域中遞送。

### 錯誤修正 {#assets-bug-fixes}

* 修正資產處理問題。
* 修正 [!DNL Dynamic Media] 設定及向 [!DNL Dynamic Media] 遞送服務發佈資產的問題。

>[!MORELIKETHIS]
>
>* [關於 Adobe Asset Link](https://www.adobe.com/tw/creativecloud/business/enterprise/adobe-asset-link.html)
>* [設定 Brand Portal](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [設定 Experience Manager 以搭配 Asset Link 運作](https://helpx.adobe.com/tw/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [使用資產微服務在 Experience Manager 中建立工作流程](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Cloud Manager 的新增功能 {#whats-new-cloud-manager}

* Cloud Manager UI 的「環境」頁面現在已可使用發佈者 URL。
* 導覽的變更項目可供使用者從 Cloud Manager 概覽頁面編輯、切換或新增程式。
* 變更項目可讓使用者在 Cloud Manager 登陸頁面上的程式資訊卡編輯程式。
* 新管道狀態&#x200B;**管道正在執行**&#x200B;會針對關聯環境而顯示。
* 改良管道執行頁面的可理解性。這項改良包括管道名稱 (僅限非生產用管道) 和類型的顯示，以及指出管道狀態為「處理中/已取消/失敗」的徽章。
* 透過工具提示改善使用者體驗及「新增程式/環境」按鈕遭停用原因的可理解性。
* 失敗的環境現在可透過 UI 和 API 刪除。
* 用於產生 git 密碼的程式對於基礎服務層的問題更具彈性。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 管道執行詳細資訊頁面上的中繼環境連結無法一致地導覽至正確位置。
* 環境建立程序中的各個步驟會比所需時間提前逾時，導致程序失敗。
* 已建置容器中使用的 Maven 設定經過更新，可避免在下載成品中繼資料時發生鎖死。
* 某些情況下，「建置影像」步驟會無法成功下載客戶封裝。
* 某些罕見情況會導致環境無法刪除。
* 無法一致地收到 Experience Cloud 通知。
