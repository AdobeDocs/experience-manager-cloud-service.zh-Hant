---
title: 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: f947a328897387d37e2092580e6992f14a344eb2
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 3%

---


# 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下部分概述了當前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從此處，您可以導航到以前版本的發行說明；比如2020年，2021年等等。

>[!NOTE]
>
>請參閱 [最近的文檔更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 有關與版本不直接相關的文檔更新的詳細資訊。

## 發行日期 {#release-date}

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 當前版本(2022.7.0)為2022年8月8日。

下一版(2022.8.0)計畫於2022年8月25日發行。

## 發佈視頻 {#release-video}

查看2022年7月版本概述視頻，瞭解2022.7.0版中添加的功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 的 [內容片段控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 現在支援 [鍵盤快捷鍵](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md)。

* AEM作為Cloud Service [Web優化的影像傳送](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) 允許通過提供WebP等格式來顯著提高頁面速度。 此新服務還提供了更靈活的影像調整和轉換選項。 所有版本 [核心影像元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) 允許通過按一下映像元件策略中的選項來利用此服務並將映像作為WebP提供。

* 個AEM性化活動現在可以利用體驗片段代替我們的傳統產品。 此功能：
   * 支援遷移路徑，其AEM中內容將提升體驗片段提供，而不是舊版庫提供，以提供與個性化在未來的擴展中保持一致的適當樣式的內容。
   * 防止內容作者在其站點上意外地提供無樣式的內容。
   * 允許將任何元件的目標模式轉換為使用可編輯模板的體驗片段(JSON和HTML類型)。

>[!NOTE]
>
>現有已使用舊式優惠的個性化活動可以繼續這樣做，但新的個性化活動應作為經驗片段建立，因為這是今後的建議方法。

## [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] {#assets}

### [!DNL Assets] 搶鮮版頻道中可用的新功能 {#prerelease-features-assets}

您現在可以將Adobe Experience Manager資產配置為 [根據MIME類型限制用戶可以上載的資產類型](/help/assets/configure-asset-upload-restrictions.md)。

![資產上載限制](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

### 中的新功能 [!DNL Forms] {#forms-features}

* **[對Scribble簽名的鍵盤輸入支援](/help/forms/signing-forms-using-scribble.md)**:自適應Forms正越來越多地被用於觸摸設備，一個常見要求是支援簽名。 在觸摸設備上簽名文檔已成為一種公認的簽名方式。 AdaptiveForms公司對Scribble簽名和Adobe Sign公司的此類使用案例有本地支援。 現在，除了其他已受支援的選項外，您還可以使用鍵盤在自適應表單中對簽名進行塗抹。 它還有助於提高可訪問性合規性。

![iphone上Scribble簽名的鍵盤輸入支援](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **在本地語言中使用「自適應Forms」嚮導**:您可以使用所選語言使用嚮導。 它現在支援Adobe Experience Manager支援的所有語言。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[調用DDX — 工AEM作流步驟](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**:文檔描述XML(DDX)是聲明性標籤語言，其元素表示文檔的構建塊。 這些構造塊包括PDF和XDP文檔，以及諸如注釋、書籤和樣式文本等其他元素。 DDX文檔是文檔的模板，描述了源文檔的所需特徵，這些特徵應出現在生成的文檔中。 單個DDX可與一系列源文檔一起使用。 您可以使用調用步驟和AEM工作流來執行各種操作，如匯編拆卸文檔、建立和修改Acrobat和XFAForms，以及中所述的其他操作 [DDX參考](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) 文檔。

* **[轉換為PDF/A — 工作AEM流步驟](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**:PDF/A是一種存檔格式，用於長期保存文檔的內容，所有字型都被嵌入，檔案也未壓縮。 現在，您可以使用「轉換為PDF/A」步驟和「工作流」AEM將任何格式的文檔或檔案轉換為PDF/A格式。


## CIF附加模組 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 產品目錄豐富現在支援AEM頁面。 這使作者能夠管理頁面 — 產品關聯。

* 各種CIF核心元件改進

### 錯誤修正 {#bug-fixes-cif}

* 將登錄令牌添加到客戶端價格提取

* 資料層中的頁元件錯誤

## [!DNL Experience Manager] 作為 [!DNL Cloud Service] 基礎 {#foundation}

### 新增功能 {#what-is-new-foundation}

* 的 [儲存庫瀏覽器](/help/implementing/developing/tools/repository-browser.md) 現在具有路徑輸入欄位，因此可以直接跳轉到儲存庫層次結構中的特定資料夾
* Sling Content Distribution(SCD)現在支援顯式的「無效」操作，以便使內容無效而不發佈該內容。 請參閱 [在AEMas a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation) 的子菜單。
* mod_macro現在在AEMas a Cloud Service中可用。 請參閱 [此表](/help/implementing/dispatcher/disp-overview.md) 的子菜單。

### AEMas a Cloud ServiceSDK Dispatcher Tools增強 {#dispatcher-tools-enhancements}

* Apache可以使用 `update_sdk.sh` 指令碼，它將自動載入和驗證對apache和dispatcher配置的任何後續更改，從而提高開發人員速度。 僅支援調度程式工具靈活模式。 另請參見 [調試Apache和Dispatcher配置](/help/implementing/dispatcher/validation-debug.md#automatic-loading) 有關自動載入和驗證的其他詳細資訊。
* 本地apache/dispatcher配置將更密切地跟蹤雲環境中的更改，從而提高兩個環境之間的奇偶校驗。

### [!DNL Experience Manager] 搶鮮版頻道中可用的新功能 {#prerelease-features-foundation}

* 現AEM在as a Cloud Service與Unified Shell整合，以改進用戶體驗，並將其與所有其它Experience Cloud應用程式統一。 請參閱 [統一AEMShell上的as a Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) 的子菜單。

## Adobe學習管理器連接器 {#learn-manage}

* 新的Adobe學習管理器連接了Adobe Experience Manager Sites、Marketo Engage和Adobe Commerce。 要瞭解更多資訊，請參閱： [Adobe學習管理器使用手冊](https://helpx.adobe.com/learning-manager/user-guide.html)。


## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月版本的完整清單 [這裡](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)。

## 遷移工具 {#migration-tools}

您可以找到遷移工具版本的完整清單 [這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)。
