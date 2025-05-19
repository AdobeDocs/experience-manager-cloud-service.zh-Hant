---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 53a2dd005de075c0f1e4bf83675995608e5f785d
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 13%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 20936 {#20936}

以下摘要說明維護版本20936數的持續改善，該版本於2025年5月19日公開發佈。 前一個維護版本為版本 20626。

啟用 2025.5.0 功能將可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!NOTE]
>
>發行說20783已於5月19日設為私人，並已由發行說20936取代。

### 增強功能 {#enhancements-20936}

* Forms-19125：核心元件最適化表單編輯器已增強，可在資料來源樹狀結構的對應區段放入表單畫布時，支援自動對應可用的最適化表單片段。 這會將基礎編輯器的重要生產力功能帶給核心元件。
* Forms-17107： AEM Forms現在提供增強的使用者端自訂函式剖析功能。 這包括支援現代JavaScript功能(ECMAScript ES10+)，例如選用的鏈結，並引進在自訂函式指令碼中使用靜態匯入的功能。 如此一來，開發人員就能更妥善地組織程式碼、利用ESM模組，以及移除先前在基於核心元件和Edge Delivery Services的最適化Forms中使用自訂函式時遇到的限制，尤其是針對先前需要這些功能因應措施的使用者。
* SITES-27775：發佈期間最佳化的參考搜尋。
* SITES-30885：在持續性查詢中最佳化的JSON處理。
* SITES-25433：搭配通用編輯器的Edge Delivery：比較舊版本時，支援完整頁面轉譯。
* SITES-27792：使用Universal Editor的Edge Delivery：新增Edge Delivery服務設定的特定範本
* SITES-19754：使用通用編輯器的Edge Delivery：當設定損壞時，出現令人信服的錯誤訊息。
* SITES-30328：使用通用編輯器的Edge Delivery：從Sidekick預覽支援。
* SITES-23499：搭配通用編輯器的Edge Delivery：允許多個欄位用於區塊選項。
* SITES-29987：在建立內容片段模型時新增設定`previewUrlPattern`的功能。
* SITES-29874：在內容片段API中新增對LongTextField參考的支援。
* SITES-29601：為透過LongText欄位參考的內容片段新增驗證。
* SITES-24623：讓GET和搜尋片段API傳回的ETags可用於修補程式。
* SITES-28557：允許PATCH內容片段中的URL引數`references`。
* SITES-5358： [OpenAPI]複製具有子系的內容片段。
* SITES-29614： GET工作流程端點。
* SITES-29615：列出批次請求API端點。
* SITES-25130：將核心元件升級至2.28.0
* SITES-10575：「MSM Blueprint Bloomfilter Loader」嘗試載入>100,000列。
* SITES-26711： RTE文字欄位的連結未更新為指向MSM轉出的即時副本。
* SITES-25976：體驗片段內的連結在MSM轉出後不適用。

### 已修正的問題 {#fixed-issues-20936}

* Assets-50994：在AemRequestEventFilter封鎖傳入流量。
* CQ-4358591：從具有「建立翻譯專案」選項的網站參考面板建立語言副本時，缺少少數語言的專案。
* CQ-4359108：使用人工翻譯匯入/匯出時，XLIFF 2.0格式失敗。
* CQ-4358722：由於Java 11和Java 17中的地區設定代碼不同，本地化不適用於舊版ISO代碼。
* Forms-19808：儲存大型表單時，其中包含已啟用延遲載入的片段，使用者無法提取草稿。
* Forms-19887：在HTML5中轉譯表單時，XFA表單中的下拉欄位（最初設定為唯讀存取）無法變更為開啟/可編輯狀態。 欄位保持唯讀狀態並防止使用者互動，不像在PDF呈現中它如預期般運作。
* Forms-19651：在規則編輯器中，當在二進位條件中使用按鈕點選，並且該規則的「then」陳述式中也使用相同按鈕時，規則無法正常運作。
* Forms-19628：在針對核心元件式最適化Forms自動產生的記錄檔案(DoR)中，如果根面板啟用「允許標題使用RTF格式」選項，則從DoR排除巢狀面板的標題時，也會錯誤地隱藏根面板的標題。
* Forms-18977：記錄檔案(DoR)服務產生的PDF缺少檔案標題。 這可能會導致不符合PDF/UA和WCAG 2.1協助工具標準，因為檔案標題是協助工具PDF的必要屬性。
* Forms-18526：當其條件中包含多個欄位的規則從一個欄位複製到另一個欄位時，這些條件中的固定欄位參考會錯誤地保留其對原始來源欄位的參考，而不是更新到複製規則的新欄位。
* Forms-19047：在AEM Forms （尤其是6.5.22.0）上修改並重新發佈最適化表單後，某些表單元素（尤其是文字方塊）的翻譯可能會遺失。
* Forms-19234： AEM Forms中PDF的時間軸功能，可讓使用者檢視PDF建立和版本設定的詳細資訊，任何PDF上傳到「Forms和檔案」區段後即停止運作。
* Forms-18196：當XDP範本所需的選用欄位資料在請求中留空時，`generatePrintedOutput` （或`generatePdfOutput`）同步HTTP API未正確地傳回200 （成功）回應代碼，而不是預期的400 （錯誤請求）錯誤代碼。
* Forms-19336：在核心元件最適化表單編輯器（AF2編輯器）中，資料Source樹狀結構中的搜尋功能無法正常或如預期運作，阻礙使用者輕鬆尋找特定資料元素。
* Forms-17707：AEP (Adobe Experience Platform)聯結器在設定為連線至AEP平台「舞台」環境時無法正常運作。
* Forms-18526：複製具有根據多個欄位之條件的規則時，在規則的條件或動作中參照的欄位（不是觸發規則的主要欄位）不會更新，以正確參照要向其複製規則的新欄位。 而是會繼續參照複製規則的原始來源欄位。
* Forms-18474：此規則設計為在特定欄位的值變更（例如欄位「A」）因表單上任何欄位的變更而錯誤觸發時，將焦點設定在特定面板或元件。 例如，如果欄位「B」被修改，即使規則僅針對欄位「A」的變更進行設定，焦點仍會設定為指定的面板。
* GRANITE-58276： OSGi相依性週期導致HTL指令碼引擎工廠無法正常運作。
* Oak-11673：Oak-segment-azure v12CPU增加是由於refreshLease所導致。
* SITES-30752：產生持續查詢回應時，請勿使用`If-modified-since`/`last-modified`標頭。
* SITES-30353： AEM內容片段中「src」欄位的GraphQL DataFetchingExceptions。
* SITES-30333：從jcr讀取資產中繼資料，以避免xmp剖析問題。
* SITES-30140：建立內容片段參考時出現雙視窗問題。
* SITES-29748：修正renderconditions，以在CF編輯器內顯示managepublication/quickpublish動作。
* SITES-15452：不應對啟動中的唯一CF元素副本進行檢查。
* SITES-30386：使用Universal Editor的Edge Delivery：重複的UE cors.js會在新增內容時導致UE重複區段。
* SITES-29745：修正參考變數未水合的罕見問題。
* SITES-30585：使用參照建立模型時無法設定「previewUrlPattern」。
* SITES-30327：發佈沒有許可權的內容片段時，會為每個裝載資源建立個別的工作流程。
* SITES-29528：ETag不能用於發佈執行個體上的快取。
* SITES-30583：尋找和取代工具會將所有字元變更為小寫。
* SITES-31157：由於ETag不一致，修補程式失敗。
* SITES-31327： [OpenAPI]作者執行個體上的Get內容片段要求可以以304回應。
* SITES-29691：嘗試移動頁面時出現NullPointerException。
* SITES-30728：在資產屬性上設定時，OnTime/OffTime未如預期發佈/取消發佈。
* SITES-29789：AEM中複製的根頁面上的元件連結變更。
* SITES-29191：無法將超過20個SKU新增到產品清單元件。
* SITES-30372：智慧型裁切在AEM的影像(V2)核心元件上無法運作。
* SITES-28693：標題為空時，Teaser元件會呈現損壞的HTML。
* SITES-28668：無法使用 LaunchPromotionParameters 提升啟動。
* SITES-31005：增強轉出工作UI以向客戶顯示進度。
* SITES-31020：增強建立即時副本工作UI以顯示客戶進度。
* SITES-29816：建立體驗片段的即時副本時出現「找不到資源」錯誤。
* SITES-29363：重設 Live Copy 按鈕不適用於巢狀的 Live Copy 內容階層。
* SITES-31467：頁面編輯器中的`contexthub.authoring-hook.js`出現JS錯誤。
* SKYOPS-106509：新增輔助的附加開啟標幟，以支援Java 21上的GSON反射式存取。

### 已知問題 {#known-issues-20936}

* SITES-28030：選取鎖定目標選項時遺失開始鎖定目標選項。

### 已過時的功能和 API {#deprecated-20936}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-20936}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 19 個已確認的弱點，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-20936}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.78.1公噸20250429061757 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
