---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.7.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.7.0 版發行說明。'
exl-id: b339ab48-e836-4589-a573-9c50917b9280
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 18%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 202278.0 版發行說明 {#release-notes}

以下章節概述2022.7.0版的功能發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2022.7.0)為2022年8月8日。

下一個版本(2022.8.0)計畫於2022年9月1日發行。

## 發行影片 {#release-video}

請觀看 2022 年 7 月版本概觀影片，了解 2022.7.0 版本新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新功能 {#sites-features}

* 此 [內容片段主控台](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) 現在支援 [鍵盤快速鍵](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md).

* AEM作為Cloud Service [網頁最佳化的影像傳遞](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) 可透過傳遞如WebP等格式來大幅提升頁面速度。 這項新服務也提供更彈性的影像調整大小和變形選項。 所有版本的 [核心影像元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) 可讓您使用此服務，並藉由按一下影像元件原則中的選項，將影像傳遞為WebP。

* AEM個人化活動現在可以使用體驗片段，以取代我們的舊版選件。 此功能：
   * 啟用移轉路徑，其中AEM內容會推廣體驗片段選件，而非舊版資料庫選件，以提供符合未來大規模個人化、樣式設定適當的內容。
   * 避免內容作者不小心在其網站上提供無樣式的內容。
   * 允許將任何元件的目標模式轉換為使用可編輯範本的體驗片段(JSON和HTML型別)。

>[!NOTE]
>
>已使用舊版優惠方案的現有個人化活動可繼續這麼做，但新的個人化活動應建立為體驗片段，因為這是日後建議的方法。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 發行前通道中可用的新功能 {#prerelease-features-assets}

您現在可以將Adobe Experience Manager Assets設定為 [根據MIME型別限制使用者可以上傳的資產型別](/help/assets/configure-asset-upload-restrictions.md).

![資產上傳限制](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新功能 {#forms-features}

* **[鍵盤輸入支援Scribble簽名](/help/forms/signing-forms-using-scribble.md)**：最適化Forms越來越多地用於觸控裝置，而常見的要求之一便是支援簽名。 在觸控裝置上簽署檔案已成為一種可接受的表格簽署方式。 最適化Forms對於這類使用案例提供手寫簽名和Adobe Sign的原生支援。 現在，有了其他已支援的選項，您也可以在最適化表單中使用鍵盤進行手寫簽名。 它還有助於改善協助工具合規性。

![iPhone上鍵盤輸入支援手寫簽名](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **使用本機語言的最適化Forms精靈**：您可以使用自己所選語言的精靈。 它現在支援Adobe Experience Manager支援的所有語言。

### [!DNL Forms] 發行前通道中可用的新功能 {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[叫用DDX - AEM工作流程步驟](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**：檔案描述XML (DDX)是一種宣告式標籤語言，其元素代表檔案的建置組塊。 這些建置區塊包括PDF和XDP檔案以及其他元素，例如註解、書籤和樣式化文字。 DDX檔案是檔案的範本，並描述來原始檔應在結果檔案中出現的所需特性。 單一DDX可用於一系列來原始檔。 您可以使用AEM工作流程中的叫用步驟來執行各種作業，例如組譯和解譯檔案、建立和修改Acrobat和XFA Forms，以及其他中所述的作業。 [DDX參考](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) 檔案。

* **[轉換為PDF/A - AEM工作流程步驟](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**：PDF/A是用於長期儲存檔案內容的封存格式，所有字型全都內嵌且檔案都未壓縮。 現在，您可以使用AEM Workflow中的「轉換為PDF/A」步驟，將任何格式的檔案或檔案轉換為PDF/A格式。


## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 產品目錄擴充現在支援AEM頁面。 這可讓作者管理頁面 — 產品關聯。

* 各種CIF核心元件改善專案

### 錯誤修正 {#bug-fixes-cif}

* 新增登入權杖至使用者端價格擷取

* 資料層中的頁面元件錯誤

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 此 [存放庫瀏覽器](/help/implementing/developing/tools/repository-browser.md) 現在有路徑輸入欄位，因此可以直接跳至存放庫階層中的特定資料夾
* Sling內容發佈(SCD)現在支援明確的「失效」動作，以使內容失效，而不發佈內容。 另請參閱 [AEMas a Cloud Service中的快取](/help/implementing/dispatcher/caching.md#explicit-invalidation) 頁面，以取得更多詳細資料。
* AEMas a Cloud Service現在提供mod_macro。 另請參閱 [此表格](/help/implementing/dispatcher/disp-overview.md) 以取得支援的Apache模組清單。

### AEMas a Cloud ServiceSDK Dispatcher工具增強功能 {#dispatcher-tools-enhancements}

* Apache啟動可使用 `docker_run_hot_reload.sh` 指令碼，會自動載入並驗證apache和dispatcher設定的任何後續變更，因此可提升開發人員速度。 僅支援Dispatcher工具的彈性模式。 另請參閱 [偵錯您的Apache和Dispatcher設定](/help/implementing/dispatcher/validation-debug.md#automatic-reloading) 以取得關於自動重新載入與驗證的其他詳細資訊。
* 本機Apache/Dispatcher設定將更緊密地追蹤雲端環境中的變更，從而提高兩個環境之間的對等性。

### [!DNL Experience Manager] 發行前通道中可用的新功能 {#prerelease-features-foundation}

* AEMas a Cloud Service現在與Unified Shell整合，以改進使用者體驗，並將其與所有其他Experience Cloud應用程式統一。 另請參閱 [統一命令介面上的AEMas a Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) 以取得更多詳細資料。

## AdobeLearning Manager聯結器 {#learn-manage}

* 全新Adobe Learning Manager內建Adobe Experience Manager Sites、Marketo Engage和Adobe Commerce的聯結器。 若要深入瞭解，請參閱： [AdobeLearning Manager使用手冊](https://helpx.adobe.com/learning-manager/user-guide.html).

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
