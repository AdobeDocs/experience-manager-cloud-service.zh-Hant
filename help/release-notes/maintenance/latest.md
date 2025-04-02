---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 7d93af706d8b0556e9e26282d339794447eb0a41
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 19%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 20133 {#20133}

以下摘要說明維護版本20133數的持續改善，該版本於2025年4月1日公開發佈。 前一個維護版本是版本 19823。

啟用 2025.4.0 功能將可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-20133}

* Assets-47850：如果AEM CS已啟用ES，請限制新增Scene7設定。
* CQ-4359547：從https://git.corp.adobe.com/target-sdk/tsdk-core存放庫完全移除Guava。
* Forms-17551：新增SharePoint清單整合的記錄檔案(DoR)支援。
* Forms-18432：實作表單專用（規則運算式）使用者端預填設定，以啟用選擇性預填功能而無OSGI層級變更。
* Forms-18513：在AEP Connector中實作資料樹狀結構轉換支援，以增強精靈功能和資料處理功能。
* Forms-19068：新增對Forms API中AEP Connector提交動作的支援，以增強表單資料整合功能。
* GRANITE-57717：更新AEM中的使用者端套件組合。
* SITES-10469： AdapterFactory應一律傳回相同的PageManager執行個體。
* SITES-25130：發行核心元件2.28.0。
* SITES-25433：比較舊版本時支援完整頁面轉譯。
* SITES-25923：不再儲存url時，LinkInfoStorageImpl可能會遭到封鎖。
* SITES-26208：透過工作流程刪除內容片段現在允許選項透過移除新刪除的片段來更新參考資源。
* SITES-26500：新增透過工作流程移動內容片段的選項 — `move-fragments`。
* SITES-26711：轉出觸發器 — 連結未更新。
* SITES-27583：體驗片段在移動後會遺失版本記錄。
* SITES-27618：搜尋頁面中片段的參考未傳回所有結果。
* SITES-27781：為內容片段參考實作模型層級驗證，允許參考片段根據其模型限制和所需標籤進行驗證。
* SITES-27784：更新SQL查詢產生以使用PATH函式，而非`jcr:path`。
* SITES-28040： Adobe Target ExperienceFragmentsReplicationListener已損毀。
* SITES-28051：取得目前使用者對內容片段的許可權： GET /cf/fragments/{fragmentId}/permissions。
* SITES-28190：預覽整合測試的設定。
* SITES-28227：將資產新增為片段參考時，我們會驗證資產是否存在。
* SITES-28248：根據OSGI設定切換網站事件。
* SITES-28255：所有3個稽核屬性都缺少完整名稱：已建立、已修改、已發佈。
* SITES-28390： PageImpl：最佳化hasContent()。
* SITES-28404：刪除作者上的頁面應會從預覽服務中取消發佈這些頁面。
* SITES-28446：新增2個回應中看不見的新欄位 — NumberModelField中的預留位置和LongTextModelField允許的模型。
* SITES-28536：為內容片段建立`RENAME`端點。
* SITES-28537：新增透過工作流程重新命名內容片段的選項 — `rename-fragments`。
* SITES-28538：參考必須重新發佈，才能維護製作和發佈的有效內容。
* SITES-28549：建立`/cf/domains`以根據AEM層傳回網域ID。
* SITES-29026：新增選用引數，使用語言和國家/地區代碼指定內容片段的地區設定。
* SITES-29031：改善PATCH執行片段的邏輯，因此提供較出色的效能。
* SITES-29169：如果所有已發佈的資源（無論處於「已發佈」或「已修改」狀態）參照已移動、重新命名或刪除的資源，則會重新發佈。
* SITES-29376：新增程式碼切換至驗證已發佈的資源刪除。
* SITES-29417：更新/libs/cq/Page/proxy.jsp以將請求轉送至jcr：content節點而非include。
* SITES-2947：建立/修改Kibana視覺效果以比較發佈rasp。
* SITES-29733：依內容片段標籤提高模型搜尋效能。
* SITES-8316：內容原則：快取ContentPolicyManager。
* SITES-24906：使用通用編輯器的Edge Delivery：支援作者建立的試算表，但不含對應（搶先存取）
* SITES-24907：具有通用編輯器的Edge Delivery：支援將Assets發佈到多個網站以供MSM使用案例（搶先存取）
* SITES-27956：使用Universal Editor的Edge Delivery：改善發佈輸送量（搶先使用）
* SITES-27956：使用通用編輯器的Edge Delivery：改善發佈至Edge Delivery Services的錯誤處理（搶先存取）

### 已修正的問題 {#fixed-issues-20133}

* cq-4358378：處理翻譯執行中的授權錯誤。
* CQ-4359263：工作完成時，對話方塊中不會顯示任何訊息。
* CQ-4359386：無法在AEMaaCS中新增i18n字典至翻譯專案。
* Forms-18068：使用RTF欄位的選項按鈕和核取方塊群組的記錄檔案(DoR)中出現粗體文字轉譯問題。
* Forms-18189：修改自訂函式處理，以防止空白使用者端程式庫的錯誤記錄，並改善UI中的錯誤顯示。
* Forms-18213：實作功能以隱藏/排除記錄檔案(DoR)中已停用的欄位，以改善檔案清晰度和使用者體驗。
* Forms-18271： Forms主題編輯器顯示未本地化的錯誤訊息，這會影響表單設定和主題自訂的使用者體驗。
* Forms-18304：在Acrobat和LiveCycle ES4中通過驗證的PDF/A-1b檔案在AEM 6.5 Forms中被錯誤地標籤為不相容，因為發生了與裝置相關的顏色錯誤。
* Forms-18325：新增Adobe Experience Platform (AEP)雲端設定，以增強表單資料整合與處理功能。
* Forms-18360：在SharePoint檔案管理中增強團隊網站的Forms清單範圍管理，以改善資料組織和存取控制。
* Forms-18375：當未選取特定組態容器時，基礎元件型表單從`conf/global`資料夾中錯誤地選取recaptcha組態。
* Forms-18426：當清單名稱包含特殊字元（例如，「 — 」）時，SharePoint清單查詢功能會失敗，影響表單與SharePoint清單的整合。
* Forms-19028：使用者端預填功能會中斷表單事件處理，導致Value commit和DOMContentLoaded事件無法在表單載入時正確觸發。
* Forms-6950：為檔案系統導覽器樹狀檢視元件新增必要的ARIA角色和屬性，以改進熒幕助讀程式的可存取性，並符合WCAG 4.1.2名稱、角色、值（A級）標準。
* Forms-7016：表單編輯器中的鍵盤焦點順序未依循邏輯導覽。
* SITES-1960：改善內容片段編輯器JSON預覽操作的效能。
* SITES-24308：將內容大小調整為400%時出現水準卷軸。
* SITES-24493：互動式元素沒有必要的角色。
* SITES-24669：無法透過鍵盤存取參考邊欄視窗分隔器。
* SITES-26881： AEMaaCS協助工具錯誤 — 評論輸入欄位旁的「三點」圖示提供的角色不正確。
* SITES-26956：在SITES上追蹤 — 24920無法在生產環境中移動頁面。
* SITES-27707：內容尋找器資產清單因資產名稱問題而失敗（6.5 SP22回歸）。
* SITES-27757：使用通用編輯器的Edge Delivery：根據helix-html-pipeline語意重寫圖示。
* SITES-27780： SP22上的純文字DefaultPasteMode的RTE中出現未預期的&lt;br>標籤。
* SITES-27958： Linkchecker擲回「此工作階段已關閉」錯誤。
* SITES-28149：在XF匯出至Target期間未觸發自訂ExperienceFragmentLinkRewriterProvider。
* SITES-28449：工作流程Widget UI錯誤 — 包含未在AEM中顯示所有子頁面的子頁面。
* SITES-28456：在GraphiQL Explorer中儲存不正確的持久查詢時，UI上缺少通知(後續追蹤 — SITES-28313)。
* SITES-28464：更新片段查詢以使用帶有毫秒的格式化日期。
* SITES-28486：在新內容片段編輯器中就地編輯不會重新導向到舊編輯器。
* SITES-28570：遺失的資產中繼資料已由內容片段的GraphQL正確處理。
* SITES-28580：SP22升級後傳統影像資產尋找器損毀。
* SITES-28600：啟動 — 內容重複。
* SITES-28668：無法使用LaunchPromotionParameters提升啟動。
* SITES-28820：在重新基底建立的新變數中新增了兩次啟動前置詞。
* SITES-28877：未定義本機外部化器端點時，UE URL服務擲回例外狀況。
* SITES-28956：如果標籤由內容片段參考，標籤刪除操作會顯示警告。
* SITES-29208：在參考欄位包含無效路徑的情況下，會正確傳回參考和變數。
* SITES-29363：重設即時副本按鈕對巢狀即時副本內容階層無效。
* SITES-29369：AIO中的Assets事件問題 | 錯誤地觸發頁面發佈/取消發佈的事件。
* SITES-29972：「刪除」和「重新命名」動作有時會產生不正確的工作流程註解。

### 已知問題 {#known-issues-20133}

無。

### 已過時的功能和 API {#deprecated-20133}

 [已過時和移除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文件中詳細介紹了 AEM as a Cloud Service 已過時和移除的功能和 API。

#### 使用者群組和產品設定檔同步的變更 {#changes-user-groups}

使用 Adob&#x200B;&#x200B;e Admin Console 進行權限管理時，不得使用下列群組，因為這些群組將不再同步至 AEM：
* 以 _GROUP_NAME_SUFFIX 結尾的 AEM 群組。
* 來自其他環境、程式或產品的產品設定檔。

若要了解更多詳情，請查看「[使用者群組和產品設定檔同步的變更](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)」。

#### 不再使用 SPA 編輯器 {#deprecate-spa-editor}

自 2025.4.0 版本開始，新專案已汰除 [SPA 編輯器](/help/implementing/developing/hybrid/introduction.md)。現有專案仍支援 SPA 編輯器，但新專案不應使用。

AEM 中用於管理 Headless 內容的首選編輯器為：

* [通用編輯器](/help/edge/wysiwyg-authoring/authoring.md)，用於視覺化編輯。
* [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。

有關這個棄用的進一步詳細資訊，請參閱檔案[SPA Editor Deprecation。](/help/implementing/developing/hybrid/spa-editor-deprecation.md)

### 安全性修正 {#security-20133}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 34 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-20133}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.28.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
