---
title: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: e76ee82b44e48e88d5c750ebb22db11067cb11b5
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 2%

---


# 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下章節概述目前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>請參閱 [近期檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 如需與版本不直接相關的檔案更新詳細資訊。

## 發行日期 {#release-date}

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2021.11.0)為2021年12月16日。
下列版本(2022.1.0)將於2022年1月27日發行。

## 發行影片 {#release-video}

查看 [2021年12月發行概述](https://video.tv.adobe.com/v/339278) 影片，以取得2021.11.0（2021年11月）版本中新增功能的摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* Dynamic Media影像智慧型裁切和色票現在由最新的Sensei服務提供技術支援，可產生改良的裁切和色票。 此外，已推出增強功能，以產生不同的裁切內容，針對相同外觀比例，但跨不同解析度。 此外，如果影像描述檔中的寬度和高度沒有變更，則任何手動編輯都會保留在重新處理時。

### 中的新功能 [!DNL Assets] 預發行管道 {#assets-prerelease-features}

* [!DNL Dynamic Media]  — 您現在可以使用AEM Dynamic Media介面來設定「一般設定」和「發佈設定」，而不需要透過Dynamic Media Classic案頭應用程式。

* [!DNL Dynamic Media] 現在支援MXF影片的擷取、預覽、播放和發佈。 尚不支援MXF視訊的註解和可購買視訊。

* 在遠端DAM和Sites部署之間設定連線後，即可在Sites部署中使用遠端DAM上的資產。 您現在可以執行 [更新、刪除、更名和移動操作](../../assets/use-assets-across-connected-assets-instances.md) 在遠端DAM資產或資料夾上。 Sites部署會自動提供延遲的更新。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 新增功能 [!DNL Forms] {#what-is-new-forms}

* **將AEM工作流程資料外部化，以安全處理**:您可以將包含敏感個人資料(SPD)元素的處理中AEM工作流程資料(AEM工作流程變數資料)儲存在客戶管理的存放庫中，以進行安全處理。 資料元素和工作流程變數不會儲存在AEM存放庫中，並會在處理工作流程時，從客戶管理的存放庫隨選擷取。

### 中提供的新功能 [!DNL Forms] 預發行管道 {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通訊API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 幫助您結合模板和XML資料，以生成各種格式的打印文檔。 此服務可讓您以同步和批次模式產生檔案。 API可讓您建立應用程式，以便您：

   * 使用XML資料填入範本檔案(PDF和XDP)，以產生檔案。
   * 以各種格式生成輸出表單，包括非互動式PDF打印流。

* **記錄檔的自訂字型和使用通訊API建立的PDF檔案**:您現在可以在使用通訊API產生的PDF檔案中使用品牌核准字型，以符合您的組織需求。

* **Forms入口網站**:您可以使用 [Forms入口網站](/help/forms/configure-forms-portal.md) 將已發佈的最適化表單列在AEM Sites頁面上。 可協助網站訪客探索所有可用的表單。 此外，訪客可使用表單入口網站來儲存及存取最適化表單的草稿，並查看已提交最適化表單的PDF版本。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 擴展了基於Commerce可擴展的Peregrine元件的myAccount元件

![擴展myAccount元件](/help/assets/CIF/extended-myAccount-components.png)

* 作者可使用其他建議類型建立隨選商務產品Recommendations

* 支援AEM Storefront中的禮品卡

## Cloud Manager {#cloud-manager}

本節概述AEM as a Cloud Service的2021.11.0版發行說明。

### 發行日期 {#release-date-cm-nov}

AEMas a Cloud Service的Cloud Manager發行日期2021.11.0為2021年11月4日。
下一版預計於2021年12月9日發行。

### 新增功能 {#what-is-new-cm-nov}

* 使用者現在可以運用新的前端管道，以加速方式專門部署前端程式碼。 請參閱 [Cloud Manager前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 了解更多。

   >[!IMPORTANT]
   >您必須使用AEM版本 `2021.10.5933.20211012T154732Z` 或更高版本，以利用新的前端管道。

* 以更有效的方式執行程式碼分析，而不需要建立整個AEM影像，可大幅縮短程式碼品質管道持續時間。 此變更將在發行後的數週內逐步推出。

* Git提交ID現在會顯示在管道執行詳細資訊中，以便更輕鬆追蹤已建置的程式碼。

* 現在可透過公開的API建立方案。

* 現在可透過公開的API建立環境。

* 此 `x-request-id` 回應標題現在會顯示在 [www.adobe.io](https://www.adobe.io/). 提交客戶服務問題以進行疑難排解時，此標題相當實用。

* 身為使用者，我看到管道為零的管道卡為我提供適當的指引。

* 現在提供新的「活動頁面」，供檢視活動（例如管道和程式碼執行）及其相關詳細資訊之用。 隨著時間推移，此頁面所列的活動將會擴展範圍以及提供的詳細資料。

* 提供新的管道頁面，可在暫留時顯示狀態彈出視窗，方便您檢視詳細資訊摘要。 可檢視管道執行及其相關聯的詳細資訊。

* 「編輯管道API」現在支援變更部署階段所使用的環境。

* 已針對大型封裝導入OakPal掃描程式的最佳化。

* 品質問題CSV檔案現在會包含每個品質問題的時間戳記。

### 錯誤修正 {#bug-fixes-nov}

* 某些非正統的組建設定會導致管道的Maven工件快取中儲存不必要的檔案，導致在啟動和停止組建容器時產生多餘的網路I/O。

* 如果部署階段不存在，管道PATCHAPI就會失敗。

* 此 `ClientlibProxyResourceCheck` 當有具有共同基本路徑的用戶端程式庫時，品質規則會產生誤判問題。

* 達到最大儲存庫數時，錯誤訊息未指定錯誤的原因。

* 在少數情況下，管道由於某些回應代碼的重試處理不當而失敗。

## Best Practices Analyzer {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.22的發行日期為2021年12月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠檢測並報告所使用的ACS公域的版本。
* 偵測群組中使用者和子群組數目並製作報表的功能。
* 能夠偵測並報告MongoDB中超過16MB的節點屬性值。

### 錯誤修正 {#bug-fixes-bpa}

* 對基礎元件的檢測進行了細化，以減少偽陰性。
* 針對AEM Forms客戶，BPA傳訊關於 `EMAIL_PDF_SUBMIT_ACTION` 「AEMas a Cloud Service」上無法使用的問題已修正。
