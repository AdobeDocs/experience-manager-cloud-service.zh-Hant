---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.7.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.7.0 版發行說明。'
source-git-commit: b1c4706d2d148c136eed66b0bff6f792a89e9d8c
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 5%

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

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2022.7.0)為2022年8月8日。

下一版(2022.8.0)預計於2022年9月1日推出。

## 發行影片 {#release-video}

請觀看2022年7月版本概述影片，以取得2022.7.0版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 此 [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 現在支援 [鍵盤快捷鍵](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

* AEM asCloud Service [網頁最佳化的影像傳送](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) 可傳送WebP等格式，大幅改善頁面速度。 這項新服務還提供更靈活的影像大小調整和轉換選項。 所有版本 [核心影像元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) 允許利用此服務，並通過按一下映像元件策略中的選項以WebP的形式提供映像。

* AEM個人化活動現在可以運用體驗片段，取代舊版選件。 此功能：
   * 可啟用移轉路徑，讓AEM內容可促銷體驗片段選件，而非舊版資料庫選件，以提供符合未來規模個人化之適當樣式的內容。
   * 防止內容作者意外提供網站上未設定樣式的內容。
   * 允許將任何元件的鎖定目標模式轉換為使用可編輯範本的體驗片段(包括JSON和HTML類型)。

>[!NOTE]
>
>已使用舊版選件的現有個人化活動可以繼續這麼做，但新的個人化活動應建立為體驗片段，因為這是日後的建議方法。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 搶鮮版頻道中可用的新功能 {#prerelease-features-assets}

您現在可以將Adobe Experience Manager Assets設定為 [根據MIME類型限制使用者可上傳的資產類型](/help/assets/configure-asset-upload-restrictions.md).

![資產上傳限制](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 中的新功能 [!DNL Forms] {#forms-features}

* **[手寫簽名的鍵盤輸入支援](/help/forms/signing-forms-using-scribble.md)**:適用性Forms在觸控裝置上的使用日益增加，一項常見需求是支援簽名。 在觸控式裝置上簽署檔案已成為簽署表單的公認方式。 適用性Forms針對這類使用案例原生支援手寫簽名和Adobe Sign。 現在，除了其他已支援的選項外，您還可以使用鍵盤在適用性表單中手寫簽名。 它還有助於改善無障礙法規遵循。

![iphone上手寫簽名的鍵盤輸入支援](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **以本機語言使用適用性Forms精靈**:您可以使用您所選擇的語言來使用精靈。 現在支援Adobe Experience Manager支援的所有語言。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[叫用DDX - AEM工作流程步驟](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**:文檔描述XML(DDX)是一種聲明性標注語言，其元素表示文檔的構成塊。 這些建置區塊包括PDF和XDP檔案，以及其他元素，例如註解、書籤和已設定樣式的文字。 DDX文檔是文檔的模板，描述源文檔的所需特性，這些特性應出現在產生的文檔中。 單個DDX可與一系列源文檔一起使用。 您可以使用「叫用步驟和AEM工作流程」來執行各種操作，例如組裝拆卸文檔、建立和修改Acrobat和XFA Forms，以及 [DDX參考](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) 檔案。

* **[轉換為PDF/A -AEM工作流程步驟](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**:PDF/A是用於長期保存文檔內容的存檔格式，所有字型都嵌入並解壓檔案。 現在，您可以使用AEM Workflow(轉換為PDF/A)步驟，將任何格式的檔案或檔案轉換為PDF/A格式。


## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 產品目錄擴充現在支援AEM頁面。 這可讓作者管理頁面 — 產品關聯。

* 各種CIF核心元件改良

### 錯誤修正 {#bug-fixes-cif}

* 將登入代號新增至用戶端取價

* 資料層中的頁面元件錯誤

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 此 [存放庫瀏覽器](/help/implementing/developing/tools/repository-browser.md) 現在有路徑輸入欄位，可直接跳至存放庫階層中的特定資料夾
* Sling Content Distribution(SCD)現在支援明確的「無效」動作，以便在未發佈該內容的情況下使內容無效。 請參閱 [AEMas a Cloud Service中的快取](/help/implementing/dispatcher/caching.md#explicit-invalidation) 頁面以取得詳細資訊。
* mod_macro現在可在AEM as a Cloud Service中使用。 請參閱 [此表](/help/implementing/dispatcher/disp-overview.md) 以取得支援的Apache模組清單。

### AEMas a Cloud ServiceSDK Dispatcher工具增強功能 {#dispatcher-tools-enhancements}

* Apache可以以 `docker_run_hot_reload.sh` 指令碼，此指令碼會自動載入及驗證apache和dispatcher設定的任何後續變更，進而提升開發人員速度。 僅支援調度工具的靈活模式。 另請參閱 [對Apache和Dispatcher設定進行除錯](/help/implementing/dispatcher/validation-debug.md#automatic-reloading) 有關自動重新載入和驗證的其他詳細資訊。
* 本機Apache/Dispatcher設定將更密切地追蹤雲端環境中的變更，提高兩個環境之間的對等關係。

### [!DNL Experience Manager] 搶鮮版頻道中可用的新功能 {#prerelease-features-foundation}

* AEM as a Cloud Service現已與Unified Shell整合，以改善使用者體驗，並與所有其他Experience Cloud應用程式統一。 請參閱 [AEMas a Cloud Service於Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) 以取得更多詳細資訊。

## Adobe學習管理器連接器 {#learn-manage}

* 新的Adobe學習管理器具有連接Adobe Experience Manager Sites、Marketo Engage和Adobe Commerce的連接器。 若要深入了解，請參閱： [Adobe學習管理器使用手冊](https://helpx.adobe.com/learning-manager/user-guide.html).

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月發行的完整清單 [此處](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## 移轉工具 {#migration-tools}

您可以找到移轉工具發行的完整清單 [此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
