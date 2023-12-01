---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1a128e35be06d018ec25fb0e6a479cfd0d242dbd
workflow-type: ht
source-wordcount: '1114'
ht-degree: 100%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 14227 版 {#release-14227}

下面是 14227 維護版本持續改善的內容，該版本於 2023 年 11 月 9 日公開發佈。此維護版本是先前 14029 維護版本的更新。維護版本 14227 取代了 14157，以修正一個問題。

2023.11.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-14227}

<!--* ASSETS-29631: Assets Cloud: Use dam:roles for secure delivery/search.-->
* CQ-4354515：翻譯：禁止翻譯引用資源的選項。
* FORMS-9993：定義將 Forms 核心元件移至 Skyline 的步驟。
* FORMS-10570：將 EC API 加入 API - 第一個路由器。
* GRANITE-48143：將 Sling ResourceMerger 升級至 1.4.4。
* SITES-14874：事件：展開模型事件的 CFM 樹狀以包含中繼資料變更。
* SITES-2719：內容片段：對內容片段變化的標記支援 (重新啟用)。
* SITES-3619：內容片段：以 JSON 格式輸出的 GraphQL CF 變化標籤並按變化標籤進行篩選 (重新啟用)。
* SITES-13750：內容片段：刪除內容片段模型的標籤。
* SITES-13920：內容片段：支援多個欄位的 minItems 設定 (預先發布)。
* SITES-14080：內容片段：刪除內容片段變化的標籤。
* SITES-14770：內容片段：片段變化應包含 fieldTags 屬性。
* SITES-15356：內容片段：建立資源時會傳回 etag 作為回應標頭。
* SITES-15357：內容片段：允許發布沒有內容片段參考的片段。
* SITES-15938：內容片段：缺少內容參考的中繼資料。
* SITES-16078：內容片段：在擷取片段時填寫變化的驗證結果屬性。
* SITES-16545：內容片段：新增端點以檢索內容片段變化的參考。
* SITES-16853：內容片段：刪除 /adobe/sites/cf/fragments/{fragmentId}/variation/{name}/tags 端點。

### 已修正的問題 {#fixed-issues-14227}

* 各種已修正的協助工具問題
* ASSETS-31015：無法將檔案上傳至檔案副檔名不明的資產。
* ASSETS-24739：在發佈時停用 Frame.io 自訂動作端點。
* CMGR-49845：內容回流：識別特定查核點的正確根路徑時出現問題。
* CMGR-49709：內容回流：更新屬性篩選器以忽略其他屬性。
* CQ-4354503：Adobe IMS 設定被隨機刪除。
* CQ-4354414：ConfigurationReplicationEventHandler 建立許多單獨的排清動作。
* CQ-4354401：翻譯：在開始資產處理之前，必須儲存專案所建立的資產。
* CQ-4354430：翻譯：將不屬於語言資料夾結構一部分的資產加入翻譯專案時發生錯誤。
* CQ-4354412：翻譯：刪除翻譯作業內容而不刪除所有已參考的內容。
* CQ-4354636：翻譯：在語言根層級建立語言副本不會調整頁面中的路徑。
* CQ-4354700：工作流程：工作流程承載畫面未載入。
* CQ-4354834：工作流程：無法在工作流程收件匣任務中新增註解
* FORMS-11302：在 RTE 中編輯的元件標題在「調適型表單編輯器 > 規則編輯器」中顯示不正確。
* GRANITE-45706：如果鍵值包含 ‚Äú))‚Äù，i18n 的匯入會失敗。
* SITES-14156：事件：發布事件不一定隨時會發送。
* SITES-14520：GraphQL：由於 FT_SITES-2719，分頁 graphql 查詢效能不佳。
* SITES-16444：GraphQL：GraphQL 查詢中缺少同名欄位的 DataFetchingException。
* SITES-16225：GraphQL：Java API 傳回的模型和片段 RTE 欄位的內容類型不正確。
* SITES-15373：內容片段：/adobe/sites/cf/fragments/{fragmentId}/variation/{name}/tags 端點未使用正確的資源命名慣例。
* SITES-15709：內容片段：建立布林欄位時建立模型端點問題。
* SITES-15727：內容片段：「標籤」類型的欄位只能在模型編輯器中新增一次。
* SITES-15782：內容片段：分項清單類型的欄位模型中缺少唯一屬性。
* SITES-15786：內容片段：內容片段無法在包含 &#39; 資料夾內建立。
* SITES-15790：內容片段：更新版本建立的位置標頭。
* SITES-15923：內容片段：CF Admin 不會顯示所有資料夾。
* SITES-15987：內容片段：建立變體時取得 500。
* SITES-16067：內容片段：無法修改長文字片段欄位的 mime 類型。
* SITES-16074：內容片段：非字串的標籤欄位[]無法從 JCR 檢索。
* SITES-16079：內容片段：/fragments/{id}/references 開始傳回重複內容。
* SITES-16118：內容片段：如果修補片段且模型中缺少片段欄位，則會引發異常。
* SITES-16119：內容片段：如果片段中繼資料包含無法辨識的欄位，則會引發異常。
* SITES-16121：內容片段：檢索模型日期欄位會引發異常。
* SITES-16123：內容片段：如果資源不是內容片段，則取得片段端點會引發異常。
* SITES-16208：內容片段：ContentFragmentModelIdentifier 公開了誤導性的標題屬性。
* SITES-16707：內容片段：無法正確讀取內容片段模型資料類型。
* SITES-16818：內容片段：只有在出現標籤時會執行刪除。
* SITES-16207：內容片段：POST /adobe/sites/cf/models 操作傳回兩個不同的 OK 狀態碼。
* SITES-15616：內容片段：發佈端點有時不會發佈內容片段的所有參考內容。
* SITES-16027：內容片段：片段回應中缺少變化參考資訊。
* SITES-16243：內容片段：尋找和取代不適用轉譯器為 Multiple 的欄位。
* SITES-16250：內容片段：修補 CF 有時會傳回不正確的 etag 標頭。
* SITES-16686：內容片段：當父參考處於最大深度時，內容片段非片段參考將會被序列化。
* SITES-12880：快速追蹤：修復「網站 > 設定分析」的本土化問題。
* SITES-16103：體驗片段：由於控制台錯誤，目標選項未顯示在雲端服務下。
* SITES-16001：MSM：能夠在建立 Live Copy 時從轉出設定中排除多重欄位元件。
* SITES-16559：MSM：在體驗片段的推出過程中刪除了推出設定。
* SITES-16797：MSM：修正了編輯器中 CF 欄位的重新啟用傳承問題。
* SITES-16273：頁面編輯器：從剪貼簿複製並貼上到 aem 網站頁面內時發生錯誤。
* SITES-16126：Sites 管理員：SITES-10288 之後非管理者使用者的編寫效能降低。
* FORMS-10534：選擇布林運算元選項時，規則編輯器中發生錯誤。
* FORMS-10248：在調適型表單中，當資料值為布林類型時，規則無法正確設定單選按鈕或複選框元件的值。
* FORMS-11361：下拉式選單元件自動預設為選取清單中的第一個選項。
* FORMS-11413：即使未使用該服務，調適型表單也會觸發與表單入口網站預填服務相關的錯誤。
* FORMS-11433：當調適型表單內含有非表單元件時，提交程序將無法完成。
* FORMS-11206：當使用者嘗試為調適型表單安排發布工作流程時，調適型表單無法如預期運作。
* FORMS-11546：Lighthouse 偵測到調適型表單中重複面板缺少 ARIA 標籤，並因而影響協助工具。
* FORMS-11095：電話號碼、電子郵件地址和號碼欄位的 ARIA 屬性定義不正確，因而造成協助工具問題。

### 已知問題 {#known-issues-14227}

無。

### 內嵌技術 {#embedded-tech-14227}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
