---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 2f0a7171f93bb5bc947dba5edb59a8e0e538e052
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 13%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 14157 版 {#release-14157}

以下摘要說明維護版本14157數的持續改善，該版本於2023年11月7日公開發佈。 此維護版本是先前 14029 維護版本的更新。

2023.11.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-14157}

* ASSETS-29631： Assets Cloud：使用dam：roles進行安全的傳送/搜尋。
* CQ-4354515：翻譯：用於抑制參照資源翻譯的選項。
* Forms-9993：定義將Forms核心元件移入Skyline的步驟。
* Forms-10570：將EC API掛載至API — 第一台路由器。
* GRANITE-48143：將Sling ResourceMerger升級至1.4.4。
* SITES-14874：事件：展開模型事件的CFM樹狀結構以包含中繼資料變更。
* SITES-2719：內容片段：標籤支援內容片段變數（重新啟用）。
* SITES-3619：內容片段：以JSON輸出的GraphQL CF變數標籤，並依變數標籤篩選（重新啟用）。
* SITES-13750：內容片段：刪除內容片段模型的標籤。
* SITES-13920：內容片段：支援為多個欄位設定的minItems （搶鮮版）。
* SITES-14080：內容片段：刪除內容片段變數的標籤。
* SITES-14770：內容片段：片段變數應包含fieldTags屬性。
* SITES-15356：內容片段：在建立資源時傳回etag作為回應標頭。
* SITES-15357：內容片段：允許發佈沒有參考的片段。
* SITES-15938：內容片段：缺少內容參考中繼資料。
* SITES-16078：內容片段：擷取片段時，填寫變數的驗證結果屬性。
* SITES-16545：內容片段：新增端點以擷取內容片段變數的參考。
* SITES-16853：內容片段：移除/adobe/sites/cf/fragments/{fragmentId}/variation/{name}/tags端點。

### 已修正的問題 {#fixed-issues-14157}

* 已修正各種協助工具問題
* ASSETS-31015：無法將副檔名未知的檔案上傳到資產。
* ASSETS-24739：在發佈上停用Frame.io自訂動作端點。
* CMGR-49845：內容回流：識別指定查核點的正確根路徑時發生問題。
* CMGR-49709：內容回流：更新屬性篩選器以忽略其他屬性。
* CQ-4354503：隨機移除Adobe IMS設定。
* CQ-4354414： ConfigurationReplicationEventHandler會建立許多個別排清動作。
* CQ-4354401：翻譯：必須先儲存專案建立的資產，才能開始資產處理。
* CQ-4354430：翻譯：將不屬於語言資料夾結構的資產新增至翻譯專案時發生錯誤。
* CQ-4354412：翻譯：刪除翻譯工作內容未刪除所有參考內容。
* CQ-4354636：翻譯：在語言根層級建立語言副本不會調整頁面中的路徑。
* cq-4354700：工作流程：工作流程裝載畫面未載入。
* CQ-4354834：工作流程：無法在工作流程收件匣任務中新增評論。
* Forms-11302：在RTE中編輯的元件標題，在調適型表單編輯器>規則編輯器中無法正確顯示。
* GRANITE-45706：如果索引鍵值有&#39;Äú)&#39;Äu，i18n匯入會失敗。
* SITES-14156：事件：不一定會傳送發佈事件。
* SITES-14520：GraphQL：由於FT_SITES-2719，導致分頁graphql查詢效能不佳。
* SITES-16444： GraphQL：GraphQL查詢中缺少相同名稱欄位的DataFetchingException。
* SITES-16225： GraphQL： Java API傳回的模型和片段RTE欄位內容型別不正確。
* SITES-15373：內容片段： /adobe/sites/cf/fragments/{fragmentId}/variation/{name}/tags端點未使用正確的資源命名慣例。
* SITES-15709：內容片段：建立布林值欄位時建立模型端點問題。
* SITES-15727：內容片段：「標籤」型別的欄位在模型編輯器中只能新增一次。
* SITES-15782：內容片段：列舉型別的欄位模型缺少唯一屬性。
* SITES-15786：內容片段：無法在包含&#39;的資料夾中建立內容片段。
* SITES-15790：內容片段：更新版本建立的位置標頭。
* SITES-15923：內容片段： CF管理員未顯示所有資料夾。
* SITES-15987：內容片段：建立變體時取得500。
* SITES-16067：內容片段：無法修改長文字片段欄位的mime型別。
* SITES-16074：內容片段：非字串的標籤欄位[]無法從 JCR 檢索。
* SITES-16079：內容片段： /fragments/{id}/references已開始傳回重複專案。
* SITES-16118：內容片段：如果片段已修補，但模型中缺少片段欄位，則會擲回例外狀況。
* SITES-16119：內容片段：如果片段中繼資料包含無法辨識的欄位，則會擲回例外狀況。
* SITES-16121：內容片段：擷取模型日期欄位時會擲回例外狀況。
* SITES-16123：內容片段：如果資源不是內容片段，則取得片段端點會擲回例外狀況。
* SITES-16208：內容片段： ContentFragmentModelIdentifier公開誤導性的標題屬性。
* SITES-16707：內容片段：無法正確讀取內容片段模型資料型別。
* SITES-16818：內容片段：僅在出現標籤時執行刪除。
* SITES-16207：內容片段：POST/adobe/sites/cf/models作業會傳回兩個不同的OK狀態代碼。
* SITES-15616：內容片段：發佈端點不會發佈內容片段的所有參考資料。
* SITES-16027：內容片段：片段回應中缺少變數參考資訊。
* SITES-16243：內容片段：尋找和取代不適用於具有「轉譯為：多個」的欄位。
* SITES-16250：內容片段：修補CF有時會傳回不正確的etag標頭。
* SITES-16686：內容片段：當父參考位於最大深度時，會序列化內容片段非片段參考。
* SITES-16234： ContextHub：開始鎖定目標時未顯示正確選取的品牌活動名稱。
* SITES-12880：快速流程：修正Sites >設定分析的本地化。
* SITES-16103：體驗片段：由於主控台錯誤，Target選項不會顯示在Cloud Service下方。
* SITES-16001： MSM：建立即時副本時，可從轉出設定中排除多欄位元件。
* SITES-16559： MSM：體驗片段的轉出程式中移除了轉出設定。
* SITES-16797： MSM：修正編輯器中CF欄位的重新啟用繼承問題。
* SITES-16273：頁面編輯器：從剪貼簿在aem sites頁面內複製貼上錯誤。
* SITES-16126：網站管理員：非管理員使用者在SITES-10288之後編寫效能緩慢。
* Forms-10534：選取布林運算元選項時，規則編輯器發生錯誤。
* Forms-10248：在調適型表單中，當資料值的型別為布林值時，規則無法正確設定選項按鈕或核取方塊元件的值。
* Forms-11361：下拉式元件會自動預設為從清單中選取第一個選項。
* Forms-11413：最適化Forms會觸發與Forms入口網站預填服務相關的錯誤，即使服務未在使用中亦然。
* Forms-11433：當非表單元件包含在調適型表單中時，提交程式無法完成。
* Forms-11206：使用者嘗試排程最適化表單的發佈工作流程時，無法如預期運作。
* Forms-11546： Lighthouse偵測到最適化表單中重複面板缺少ARIA標籤，影響協助工具。
* Forms-11095：電話號碼、電子郵件地址和號碼欄位的ARIA屬性定義不正確，導致無障礙問題。

### 已知問題 {#known-issues-14157}

無。

### 內嵌技術 {#embedded-tech-14157}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
