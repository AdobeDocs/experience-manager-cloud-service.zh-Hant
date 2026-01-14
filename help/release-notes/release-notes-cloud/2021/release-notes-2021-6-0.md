---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0 版發行說明。'
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 48%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0的發行日期為2021年6月28日。
下列版本(2021.7.0)將於2021年7月29日發行。

## 發行影片 {#release-video}

請觀看[2021年6月版本總覽](https://video.tv.adobe.com/v/334296)影片，以瞭解新增功能的摘要。

## 適用於AEM as a Cloud Service的XML Documentation {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

* 適用於AEM as a Cloud Service的XML Documentation現已正式推出。
* 這將允許現有AEM Cloud Service客戶採購XML Documentation附加元件，以跨多個管道(包括AEM網站)匯入、建立、管理和傳遞技術內容

## Cloud Manager {#cloud-manager}

本節概述AEM as a Cloud Service 2021.6.0和2021.5.0中Cloud Manager的發行說明

### 發行日期 {#release-date-june-cm}

AEM as a Cloud Service 2021.6.0中Cloud Manager的發行日期為2021年6月10日。
下一版本計畫於2021年7月15日發行。

### 新增功能 {#what-is-new-junecm}

* 預覽服務將會以滾動方式部署到所有計劃。 當客戶的計畫有啟用預覽服務時，他們會在產品內收到通知。如需更多詳細資訊，請參閱[存取預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)。

* 現在，在建置步驟中所下載的 Maven Dependencies 會在管道執行之間快取。在未來幾週內將會為客戶啟用此功能。

* 現在可以透過編輯計畫對話框編輯計畫名稱。

* 在專案建立期間以及透過管理 Git 工作流程在預設推送命令中所使用的預設分支名稱已變更為 `main`。

* UI 中的編輯計畫體驗已更新。

* 已更新品質規則 `ImmutableMutableMixCheck`，可將 `/oak:index` 節點分類為不可變動。

* 品質規則 `CQBP-84` 和 `CQBP-84--dependencies` 已合併為單一規則。在此合併過程中，更準確地掃描相依性會識別部署到 AEM 執行階段的第三方相依性的問題。

* 為避免混淆，「環境詳細資料」頁面上的「發佈 AEM」和「發佈 Dispatcher」區段列已合併。

  ![Dispatcher環境](/help/implementing/cloud-manager/release-notes/assets/aem-dispatcher.png)

* 已新增程式碼品質規則來驗證 `damAssetLucene` 索引的結構。如需更多詳細資訊，請參閱[自訂 DAM 資產 Lucene Oak 索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)。

* 「環境詳細資料」頁面現在會適當地顯示發佈和預覽服務的多個網域名稱 (如適用)。如需詳細資訊，請參閱[環境詳細資訊](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。

### 錯誤修正 {#bug-fixes-junecm}

* 未正確解析根元素名稱後包含換行符的 JCR 節點定義。

* 列出存放庫 API 不會過濾已刪除的存放庫。

* 當為計畫步驟提供無效值時，會顯示不正確的錯誤消息。

* 有時，即使未部署該設定，使用者也可能會在 IP 允許清單旁邊看到綠色的&#x200B;*活動*&#x200B;狀態。

* 某些計畫編輯序列可能會導致無法建立或編輯生產管道。

* 某些程序編輯序列可能會導致&#x200B;**概觀**&#x200B;頁面顯示誤導性消息以重新執行程序設定。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#ga-features-assets}

* 內容自動化功能可讓[!DNL Experience Manager Assets]使用[!DNL Adobe Creative Cloud] API來大規模自動化資產的製作。 它大幅減少了建立相同資產的變體所需的時間和反複工作，進而加快提供內容的速度。 此功能不需要任何程式碼，並且可在DAM內運作。
* 已發行[!DNL Adobe Asset Link]的[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]和[!DNL Adobe InDesign]的[!DNL Adobe Asset Link] v3.0和[!DNL Adobe XD] v2.0。 它提供：

   * 支援[!DNL Assets Essentials]。
   * 能夠以[!DNL Experience Manager]或[!DNL Cloud Service]形式自動連線至[!DNL Assets Essentials]。

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### [!DNL Assets]發行前通道中可用的新功能 {#beta-features-assets}

* 已增強檢視設定，讓使用者可選擇預設檢視和預設排序引數。
* Linkshare下載功能使用可提高下載速度的非同步下載。
* 使用者可以根據屬性述詞搜尋及篩選檔案夾。
* [!DNL Experience Manager Assets]內嵌[!DNL Adobe Document Cloud]支援的PDF Viewer以預覽支援的檔案。 此功能可讓使用者預覽PDF和其他多頁檔案，而不需要任何複雜的處理。 如此可改善與[!DNL Experience Manager] 6.5的功能同位性。

### 修正在 [!DNL Assets] 中的錯誤 {#bugs-fixed-assets}

* 將擁有者新增至子資料夾時，[!DNL Assets]也會將相同的使用者新增為父資料夾的擁有者。 (CQ-4323737)
* 將資產新增至收藏集時，如果使用者對收藏集搜尋套用篩選器，則使用者無法在清單檢視中檢視收藏集。 (CQ-4323181)
* 搜尋檔案和資料夾時，如果使用者套用篩選器並選擇[!UICONTROL 檔案和資料夾]，則只會顯示檔案，而不會顯示資料夾。 (CQ-4319543)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新功能 {#ga-features-sites}

* 發佈到預覽層現在會在網站管理UI中顯示為頁面狀態
* 「發佈到預覽層」現在會在動作結束時顯示預覽URL，並將該URL儲存在頁面屬性中以供日後參考

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* 新增篩選 AEM 收件匣中自訂欄的功能
* 新增使用最適化表單的主題編輯器和樣式圖層的功能，以設定驗證碼元件的樣式。
* 改善自動偵測來源 PDF 表單中邏輯區段並將這些區段轉換成對應的最適化表單面板的速度和準確性。
* 新增將 PDF 或 XDP 檔案從一個資料夾移至另一個資料夾的移動動作。

### [!DNL Forms] 的 Beta 版功能  {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：通訊 API 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：
   * 使用 XML 資料填寫範本檔案來產生最終表單文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   * 從 XFA 表單 PDF 和 Adobe Acrobat 表單 (AcroForm) 產生列印 PDF。

* **Variable Data Externalizer**：您可以將 AEM 工作流程變數的資料儲存於您的組織管理的外部儲存系統。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

### 修正在 [!DNL Forms] 中的錯誤 {#forms-bugs-fixed}

* 當欄位在透過表單資料模型 (FDM) 提交資料到後端服務前驗證時，雖然會成功驗證，但表單資料模型無法叫用發佈驗證。
* 從 Apple iOS 裝置提交包含標準 HTML 上傳欄位的表單時，有時不會傳送檔案內容並在另一端收到 0 位元組檔案。這是 Apple iOS 的已知問題。[FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

本節概述AEM Screens as a Cloud Service的發行說明。

### 發行日期 {#release-date-june-screens}

AEM Screens as a Cloud Service的發行日期為2021年6月24日。

### 新增功能 {#what-is-new-screens-june}

>[!NOTE]
>請參閱[AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html)指南，以取得成功安裝、設定和執行Screens as a Cloud Service所需的基礎知識，以及指向詳細概念技術檔案的連結。

* 大量裝置註冊管理意味著布建大量播放器裝置變得更快且更有效率。

* 改良每個裝置、顯示和通路庫存檢視的搜尋和篩選選項。

* 裝置運作狀況快照藉由提供一目瞭然的重要狀態來節省時間。

* 「物件詳細資料」頁面提供專案中每個物件的最相關資訊摘要。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新的CIF產品和內容片段的類別參考資料型別(包括 產品/類別選擇器UI支援)
* 全新Commerce內容片段核心元件
* AEM後端支援全文檢索商務搜尋
* Commerce核心元件支援Adobe Commerce AI Recs資料收集
* 改善類別頁面的SEO易記URL
* 支援每個網站/設定的自訂HTTP標頭

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具v1.5.4的發行日期為2021年6月28日。

### 新增功能 {#what-is-new-ctt-latest}

* 新增支援選用的[預先複製](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html)步驟，以搭配CTT使用。 當來源AEM例項設定為使用Amazon S3或Azure Blob儲存體資料存放區時，預先複製步驟可用來大幅加快內容轉移活動的擷取和擷取階段。

* CTT新增了護欄，以防止使用者在擷取階段期間達到關鍵點時停止擷取並可能損壞資料。

* 擷取記錄檔提供更多說明性，以協助疑難排解。

* 在UI中新增更多描述性擷取狀態訊息。

### 錯誤修正 {#bug-fixes-ctt-latest}

* 停止作者執行個體上的擷取時，UI會覆寫先前在發佈執行個體上完成的擷取至`STOPPED` （從`FINISHED`）。 此問題已修正。

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.16的發行日期為2021年6月30日。

### 新增功能 {#what-is-new-bpa-latest}

* 能夠偵測並報告`/content/dam`下資料夾中缺少的子節點。

* 能夠偵測和報告所使用Best Practices Analyzer的版本。

### 錯誤修正 {#bug-fixes-bpa-latest}

* 已修正與不支援的存放庫結構(URS)相關的記錄錯誤。
