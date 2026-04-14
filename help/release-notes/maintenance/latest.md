---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d2c26a122bd2a0a970af7578932d88e6f93487d5
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 12%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 25194 版 {#25194}

以下摘要說明維護版本25194數的持續改善，該版本於2026年4月1日公開發佈。 前一個維護版本是版本 24678。

2026.4.0 功能啟用會提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!NOTE]
>
>發行說24893已設為私人。

### 增強功能 {#enhancements-25194}

* Assets-65127：事件自訂中繼資料：改善中繼資料名稱的處理。
* Assets-63313：根據C2PA資訊清單，自動建立匯出資產和父項的相關連結。
* Assets-10995：限制下載zip檔中的資產數量。
* Forms-24388：新增互動式通訊(IC)編輯器的本機開發環境，讓開發人員不需依賴共用伺服器即可建置和測試設定。 此增強功能可協助企業客戶加快迭代速度、減少環境相依性，並提升整體開發生產力。
* Forms-24014：加強檔案附件元件的規則編輯器，以支援使用「AND」邏輯來合併條件，例如，允許「如果檔案附件已變更且面板有效，則執行此動作」等規則。 以前，檔案附件無法使用其他條件；此更新可啟用更複雜的規則定義來支援進階工作流程。
* Forms-23571：除了自訂事件之外，新增對現成(OOTB)事件的支援，已增強觸發事件規則的現有簡化文法檢視。 以前，使用者只能使用自訂事件的簡化語法，且必須在「WHEN」和「ON TRIGGER EVENT」規則之間切換，以分別設定OOTB和自訂事件。 透過此更新，OOTB和自訂事件均可在相同的簡化語法中使用，精簡規則設定並減少對切換內容的需求。
* Forms-24462：針對Headless最適化Forms (AF)在React Vanilla元件中新增對手寫簽名元件的支援。 此增強功能可讓使用者直接在React式表格中擷取手寫簽名，支援數位簽名工作流程以及規劃的企業客戶上線時間表。
* Forms-24343：在表單模型JavaScript Object Notation (JSON)中新增`custom:setProperty`的最佳化處理，可讓您更快速地處理動態屬性更新。 此增強功能可改善複雜最適化Forms (AF)的效能，這類效能依賴頻繁的執行階段變更，導致更順暢的使用者互動並降低載入時間。
* Forms-24358：新增在模型JavaScript物件標籤法(JSON)結構中使用`items`屬性（而非`:items`和`:itemsOrder`）的支援。 此增強功能可讓開發人員使用更清晰、更直覺的資料模型，更符合常見JSON慣例，並簡化與外部系統的整合。
* Forms-24087：新增在Adaptive Forms (AF)中直接在片段容器上定義規則和事件的支援。 此增強功能可讓作者在容器層級套用條件式邏輯和互動，進而提高重複使用率，並減少跨個別片段欄位重複規則的需求。
* Forms-24440：在互動式通訊編輯器的規則編輯器的THEN下拉式清單中新增新的「移除欄位」動作，可讓使用者在滿足規則條件時，從表單中完全移除選取的元件。 此增強功能支援需要動態重新建構表單的工作流程，而非僅隱藏欄位，同時仍會觸發適當的`forms_ready`指令碼以維持一致行為。
* Forms-23898：新增在互動式通訊(IC)編輯器中使用`@`標籤法定義變數的支援，讓使用者能更直覺地設定動態表格。 此增強功能簡化變數驅動表格內容的設定，並改善編寫體驗中管理動態資料時的清晰度。
* Forms-23702：為SharePoint List (SPList)連線新增憑證式驗證，實現對SharePoint資料更安全、憑證導向的存取。 此增強功能可協助企業客戶滿足更嚴格的安全性與法規遵循需求，同時減少對密碼式驗證的依賴。
* Forms-23800：新增在Sling設定中覆寫reCAPTCHA密碼金鑰的支援，讓企業客戶符合自己的安全性和合規性要求。 此增強功能允許環境特定的秘密金鑰管理，因此管理員可以安全地整合reCAPTCHA，而不需要變更程式碼。

### 已修正的問題 {#fixed-issues-25194}

* Assets-62882：管理員檢視：上傳多個無效檔案名稱時資訊工具提示中斷。
* Assets-63642：共用連結無法在某些開發環境(SLA3)上轉譯資產。
* Assets-59267：載入傳遞裝載的應用程式中繼資料時出現NPE。
* Assets-59227：中繼資料匯出：由於regex相符，不再包含未選取的屬性。
* Assets-65187：當欄資料包含逸出逗號時，在雲端中進行CSV預覽。
* Assets-63441：確保所有使用者都有權讀取Assets Omnisearch設定。
* SITES-40095：中繼資料編輯器：本機內容片段參考超過10個專案。
* Forms-24811：使用者在管理表單邏輯規則時遇到問題。 當他們嘗試修改先前建立的規則時，規則編輯器不允許變更，強制使用者從頭開始重新建立規則，並減慢表單維護速度。
* Forms-24720：使用者在自適應Forms (AF)中設定新建立的變數時遇到問題。 當他們將規則新增到資料繫結或未繫結變數時，規則沒有按預期儲存，強制使用者重新建立其邏輯，並減慢編寫工作流程的速度。
* Forms-24195：使用者在重設最適化Forms (AF)中的下拉式欄位時遇到不一致的行為。 當下拉式清單設定了預留位置且表單或元件重設時，欄位會變為空白而不是返回到預留位置值，導致對所需選擇產生混淆。
* Forms-24718：使用者在選取「首頁」按鈕時，在互動式通訊(IC)編輯器中遇到導覽問題。 按鈕沒有返回主要Adobe Experience Manager (AEM)介面，而是未如預期重新導向，在IC編輯和AEM首頁畫面之間移動時會中斷使用者的工作流程。
* Forms-24810：使用者在第一次嘗試載入表單的最適化使用者介面(AUI)時遇到間歇性失敗。 在某些工作階段中，初始頁面無法正確轉譯，強制使用者重新整理或重試，然後才能開始填寫表單。
* Forms-24520：使用者在使用最適化使用者介面(AUI)的表單列印預覽中，遇到代理使用者介面(UI)缺少頁碼的問題。 當代理程式開啟列印預覽時，頁碼欄位有時會顯示為空白，使得在檢閱或共用列印復本時更難以參考特定頁面。
* Forms-24532：使用者使用表單資料模型(FDM)預先填入SharePoint `/teams`清單設定時遇到失敗。 依賴這些清單的政府組織發現，表單載入時沒有預期的預先填入資料，這會中斷資料收集工作流程，並增加手動輸入工作。
* Forms-24516：在AEM Forms as a Cloud Service中升級SDK後，使用者在記錄檔案(DoR)中遇到缺少手寫簽名資料的情況。 使用手寫選項簽署表單時，產生的DoR不會顯示擷取的簽名，導致企業客戶混淆和不完整的記錄。
* Forms-18631：使用者在案頭、回應式網頁設計(RWD)平板電腦和RWD行動檢視上遇到格線配置無障礙問題。 在Windows 11上使用Chrome搭配NVDA (NonVisual Desktop Access)熒幕助讀程式時，格線缺少適當的角色和屬性，使得輔助技術難以正確解讀和導覽內容。
* Forms-24798：在AEM Forms使用者介面(UI)中使用最適化Forms (AF)規則中的`else`條件時，使用者遇到不一致的行為。 不符合主要規則條件時，關聯的`else`動作未執行，導致表單邏輯和欄位可見度的行為與作者設定的不同。
* Forms-24334：使用者在JavaScript (AEM) Forms as a Cloud Service上使用內嵌式調適型表單(AF)時遇到預填失敗和Adobe Experience Manager物件標籤法(JSON)合併問題。 載入已移轉的表單時，未出現預期的預填資料，且合併的JSON內容不完整或不正確。 針對受影響的環境，這會封鎖從內部部署AEM 6.5移轉至AEM Forms as a Cloud Service的作業。
* Forms-24441：使用者在Adobe Experience Manager (AEM) Forms as a Cloud Service中遇到記錄檔案(DoR)範本設定問題。 當他們在快速開發環境中儲存自訂的DoR範本時，範本會恢復為預設版本，以防止他們保留其預期的版面和設定。
* Forms-24393：當舊範本繼續顯示為「未命名」而非顯示有意義的名稱時，使用者會遇到混淆。 這使得在日常編寫工作中難以區分和重複使用現有範本。
* Forms-24163：使用者在預覽包含片段的版本2表單時遇到問題。 在預覽模式中，表單內容未如預期呈現，導致使用者無法在發佈前驗證版面和行為。
* Forms-24328：使用者體驗到表單提交作業在將「隱藏的reCAPTCHA v2」與「在使用者動作時驗證碼」選項搭配使用時未完成。 企業客戶發現受影響環境上的表單未如預期提交，導致聯絡和提案請求工作流程中斷。

#### AEM Guides {#guides-25194}

* GUIDES-38412 ：在編輯Schematron `(*.sch)`檔案並使用尋找和取代功能時，尋找和取代面板會在底部部分地顯示在畫面外，阻止存取其輸入欄位和控制項。
* GUIDES-37806：使用不同條件預設集的多個地圖重複使用相同主題時，將最新地圖發佈至Salesforce會覆寫主題內容，導致向先前發佈地圖的使用者顯示不正確的資料。
* GUIDES-39394：當最初受管理為具有特定版本（例如，在`/en/`下）的語言特定資產的影像移至具有更新版本的全域資料夾並執行基準匯出時，新基準會繼續參考該影像的過時語言特定版本，導致基準匯出失敗。
* GUIDES-39054：建立動態基準線時，編輯器有時會因為多個並行的API請求而停止回應，導致所有其他作業暫停。
* GUIDES-37781：將使用者指派給稽核任務時，下拉式清單會列出所有使用者，而非僅列出與所選專案關聯的使用者，導致無效的使用者選項。
* GUIDES-39385：開啟地圖的報表時，「篩選器」面板的載入有所延遲。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-25194}

無。

### 已過時的功能和 API {#deprecated-25194}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-25194}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 9 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-25194}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
