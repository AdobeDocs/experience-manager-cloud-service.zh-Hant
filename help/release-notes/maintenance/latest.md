---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9d9acd2151aca65a0c988b90bc4f94e088395f3f
workflow-type: tm+mt
source-wordcount: '2221'
ht-degree: 8%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 25520 版 {#25520}

Summarized below are the continuous improvements for maintenance release 25520, which was publicly released on April 23, 2026. 前一個維護版本是版本 25194。

2026.4.0 功能啟用會提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。


### 增強功能 {#enhancements-25520}

* Forms-24388：新增互動式通訊(IC)編輯器的本機開發環境，讓開發人員不需依賴共用伺服器即可建置和測試設定。 此增強功能可協助企業客戶加快迭代速度、減少環境相依性，並提升整體開發生產力。
* Forms-24014：加強檔案附件元件的規則編輯器，以支援使用「AND」邏輯來合併條件，例如，允許「如果檔案附件已變更且面板有效，則執行此動作」等規則。 以前，檔案附件無法使用其他條件；此更新可啟用更複雜的規則定義來支援進階工作流程。
* FORMS-23571: Enhanced the existing simplified grammar view for trigger event rules by adding support for out-of-the-box (OOTB) events in addition to custom events. Previously, users could only use the simplified grammar for custom events and had to switch between &quot;WHEN&quot; and &quot;ON TRIGGER EVENT&quot; rules to configure OOTB and custom events separately. With this update, both OOTB and custom events can be used in the same simplified grammar, streamlining rule configuration and reducing the need to switch contexts.
* Forms-24462：針對Headless最適化Forms (AF)在React Vanilla元件中新增對手寫簽名元件的支援。 此增強功能可讓使用者直接在React式表格中擷取手寫簽名，支援數位簽名工作流程以及規劃的企業客戶上線時間表。
* Forms-24343：在表單模型JavaScript Object Notation (JSON)中新增`custom:setProperty`的最佳化處理，可讓您更快速地處理動態屬性更新。 此增強功能可改善複雜最適化Forms (AF)的效能，這類效能依賴頻繁的執行階段變更，導致更順暢的使用者互動並降低載入時間。
* Forms-24358：新增在模型JavaScript物件標籤法(JSON)結構中使用`items`屬性（而非`:items`和`:itemsOrder`）的支援。 此增強功能可讓開發人員使用更清晰、更直覺的資料模型，更符合常見JSON慣例，並簡化與外部系統的整合。
* Forms-24087：新增在Adaptive Forms (AF)中直接在片段容器上定義規則和事件的支援。 此增強功能可讓作者在容器層級套用條件式邏輯和互動，進而提高重複使用率，並減少跨個別片段欄位重複規則的需求。
* Forms-24440：在互動式通訊編輯器的規則編輯器的THEN下拉式清單中新增新的「移除欄位」動作，可讓使用者在滿足規則條件時，從表單中完全移除選取的元件。 此增強功能支援需要動態重新建構表單的工作流程，而非僅隱藏欄位，同時仍會觸發適當的`forms_ready`指令碼以維持一致行為。
* Forms-23898：新增在互動式通訊(IC)編輯器中使用`@`標籤法定義變數的支援，讓使用者能更直覺地設定動態表格。 此增強功能簡化變數驅動表格內容的設定，並改善編寫體驗中管理動態資料時的清晰度。
* Forms-23702：為SharePoint List (SPList)連線新增憑證式驗證，實現對SharePoint資料更安全、憑證導向的存取。 此增強功能可協助企業客戶滿足更嚴格的安全性與法規遵循需求，同時減少對密碼式驗證的依賴。
* Forms-23800：新增在Sling設定中覆寫reCAPTCHA密碼金鑰的支援，讓企業客戶符合自己的安全性和合規性要求。 This enhancement allows environment-specific secret key management so administrators can safely integrate reCAPTCHA without code changes.
* SITES-39116: Content Fragment GET endpoint now includes metadata schema information.
* SITES-41449：新的專用GET端點，用於擷取內容片段中繼資料。
* SITES-39434：內容片段和資料夾現在可以連結到中繼資料結構，以進行結構化的中繼資料管理。
* SITES-39567：內容片段中繼資料現在會根據連結的中繼資料結構描述進行驗證和儲存。
* SITES-40006：現在可以使用中繼資料欄位值來搜尋和篩選內容片段。
* SITES-41391：單一內容片段擷取API現在包含簽入/簽出狀態資訊
* SITES-42214：改善內容片段移動作業的可靠性和效能
* SITES-41351: Improved the display format of metadata in Content Fragments for better readability.
* SITES-42458: Default metadata can now be added without strict schema validation for greater flexibility.
* SITES-35508: Edge Delivery with Universal Editor: Add support for images in RTE.
* SITES-37078：使用通用編輯器的Edge Delivery：當頁面為唯讀時移除通用編輯器工具。
* SITES-40206：使用通用編輯器的Edge Delivery：將名稱驗證新增至頁面建立精靈。
* SITES-40255：使用通用編輯器的Edge Delivery：防止將試算表發佈為`/config.json`。
* SITES-40757：使用Universal Editor的Edge Delivery：確保在網站建立精靈中Edge Delivery設定的唯一性。
* SITES-41134：使用通用編輯器的Edge Delivery：無法發佈檔案型設定。

### 已修正的問題 {#fixed-issues-25520}

* FORMS-24811: Users experienced issues managing form logic rules. When they tried to modify rules that had been created earlier, the rule editor did not allow changes, forcing users to recreate rules from scratch and slowing down form maintenance.
* FORMS-24720: Users experienced issues when configuring newly created variables in Adaptive Forms (AF). When they added rules to data-bound or unbound variables, the rules did not save as expected, forcing users to recreate their logic and slowing down form authoring workflows.
* FORMS-24195: Users experienced inconsistent behavior when resetting dropdown fields in Adaptive Forms (AF). When a dropdown had a placeholder configured and the form or component was reset, the field became blank instead of returning to the placeholder value, causing confusion about required selections.
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
* FORMS-24328: Users experienced form submissions not completing when using Invisible reCAPTCHA v2 with the &quot;Validate CAPTCHA on a user action&quot; option. Enterprise customers saw that forms on affected environments did not submit as expected, disrupting contact and request-for-proposal workflows.
* SITES-42118: Skip rewrite rules for `/graphql/execute.json`.
* SITES-40095: Fix local reference list in the metadata editor.
* SITES-42191：當DAM檔案名稱包含空格/非ASCII字元時，修正GraphQL JSON省略內嵌的影像參考。
* SITES-22336： 「Assets >建立>內容片段」中未本地化的「內容片段模型」字串。
* SITES-19796：在Assets下建立內容片段時，新增無效字元時會顯示未本地化的字串「提供的名稱無效」。
* SITES-42531：在「Assets」頁面中鎖定「內容片段」時，工具提示未本地化。
* SITES-42532：在Assets中發佈CF至AEM時未本地化的「稍後」字串。
* SITES-39250: Localized characters are incorrectly displayed in link in Assets > Content Fragment Editor.
* SITES-41117: Unlocalized &#39;The selected value needs to be a valid Model Type inside `{}` or a global model.&#39; string in Content Fragment Model Editor.
* SITES-41431：減少熒幕助讀程式對鎖定按鈕回饋的詳細程度，以提供更清晰、更精簡的公告。
* SITES-40819：修正鍵盤焦點在互動後未返回觸發元素的問題，確保焦點順序可預測。
* SITES-40751：在工具列專案的鍵盤焦點上新增可見標籤，讓鍵盤使用者可以清楚識別動作。
* SITES-25524：修正裝置按鈕上按Aria鍵的使用，讓輔助技術接收精確的狀態資訊。
* SITES-25321：更新文字顏色，以符合最低對比需求，並改善低視力使用者的可讀性。
* SITES-25304：防止摺疊的人口統計工具列錯誤地接收焦點，維持邏輯的焦點順序。
* SITES-25292：釐清熒幕助讀程式對旋轉裝置按鈕的宣告，以便更清楚描述其用途和狀態。
* SITES-25290：新增案頭切換按鈕的可見按下狀態，讓使用者可清楚瞭解其選取狀態。
* SITES-25287：改善編輯版面時的尺標測量內容，讓熒幕助讀程式使用者更容易理解測量資訊。
* SITES-25284：修正在未勾選狀態中截斷「iPhone 8 Plus」按鈕標籤的問題，以便公告和顯示完整裝置名稱。
* SITES-25251：篩選「插入新元件」清單（表示結果已變更）時，為熒幕助讀程式使用者引入意見回饋。
* SITES-25221: Increased the touch target size of the Edit button in the Asset Side Rail to meet minimum target size guidelines.
* SITES-25220: Added warning/indication that the Edit button in the Assets Left Rail opens a new tab, improving predictability for assistive tech users.
* SITES-24993：更新編輯器畫布標題標題以使用適當的標題角色，改善熒幕助讀程式的檔案結構。
* SITES-24954：修正模擬器按鈕的焦點順序，使其遵循自然和邏輯的導覽順序。
* SITES-41586：修正編輯器內內容片段元件的複製貼上遺失內容片段參照的問題。
* SITES-42195：修正`CommerceLinksTransformerFactory`在發佈執行個體上不遵守Sling對應。
* SITES-41238：修正ThumbnailServlet中導致記錄泛濫的錯誤。
* SITES-41041：修正版本預覽/比較中未轉譯的CIF元件。
* SITES-40756：在「即時副本概述>關係狀態」中修正未本地化的日期格式。
* SITES-40219：修正未針對特定產品或類別頁面呼叫CatalogPageNotFoundFilter的問題。
* SITES-40218：修正SpecificPageFilterFactory遺失v3頁面資源型別登入。
* SITES-40347：使用新標題集建立即時副本時，中斷標題的繼承。
* SITES-41544：內容片段ETag計算現在排除中繼資料。
* SITES-42734：修正使用預設結構描述時，GET中繼資料端點傳回空白欄位的問題。
* SITES-37955：使用通用編輯器的Edge Delivery：確保一致檢查發佈先決條件。
* SITES-40877：使用通用編輯器的Edge Delivery：修正包含非ascii特殊字元之頁面的發佈失敗。
* SITES-42092：使用通用編輯器的Edge Delivery：修正以`-s`結尾的路徑的深層取消發佈。
* SITES-24650: iframe does not have a title.

### 已知問題 {#known-issues-25520}

無。

### 已過時的功能和 API {#deprecated-25520}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-25520}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 24 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-25520}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
