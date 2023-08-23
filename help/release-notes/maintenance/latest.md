---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 10c495505b3997ec6360aa2764ead37725759cb2
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 83%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 13206 版 {#release-13206}

下面是 13206 維護版本的持續改善內容，該版本於 2023 年 8 月 21 日公開發行。此維護版本取代版本13173和13099，以修正影響收件匣功能的問題。

2023.8.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-13206}

- SITES-13906：GraphQL - 升級到 graphql-java 20.1。
- SITES-8972：GraphQL - 在 JSON 中新增列舉資料類型的選項標籤。
- SITES-9689：GraphQL - 在 JSON 中新增內容參考資料類型的標題和說明。
- SITES-13052：內容片段 - 將內容片段匯出至 Adob&#x200B;&#x200B;e Target.

### 已修正的問題 {#fixed-issues-13206}

- SITES-14937：MSM - 在 Live Copy 上點擊「儲存並關閉」時會切換從父值繼承推出設定。
- SITES-14847：內容片段 - 內容片段連結未醒目顯示。
- SITES-11620：內容片段 - 稍微切斷了 UI 中的參考路徑。
- SITES-14171：GraphQL - 在部分情況下，不會破壞快取資料的循環參考。
- SITES-14577：體驗片段 - 批次發佈不適用於 Live Copy。
- SITES-14341：管理員UI — 移除刪除許可權時，「屬性」按鈕的行為不一致。
- SITES-11000：管理員 UI - 參考：部分頁面中缺少傳入連結。
- SITES-11559：管理員 UI - 參考：傳入連結顯示錯誤頁面。
- SITES-14337：管理員 UI - 在特定情況下開啟編輯器頁面會產生錯誤。
- SITES-13425：ContextHub - 按一下 ContextHub 按鈕時，選單列未顯示。
- CQ-4354266：無法開啟收件匣專案。
- CQ-4354279：無法在「個人化」標籤下檢視活動報表。
- FORMS-9971：在不同的地區設定中轉譯最適化表單時，會將元件的可見度錯誤地解讀和套用。
- FORMS-9888：將最適化表單設定為在表單提交時重新導向至外部 URL (致謝頁面) 時，表單無法重新導向至外部 URL。
- FORMS-9845：使用規則編輯器清除下拉選單後，儘管已假定清除，但之前提供的值卻持續存在。
- FORMS-9263：當核取方塊的標籤包含特殊字元時，使用者若按一下該核取方塊，並無法選取核取方塊。
- FORMS-9254：使用者捲動以瀏覽條款和條件元件的文字內容時，元件內的核取方塊會在使用者捲動完整個文字內容之前即自動啟用。
- FORMS-9045：指令碼標記無法解析 BASE XDP 中的外部片段參考。
- FORMS-9026：嘗試使用 JSON 綱要 (具有包含空白字元的列舉並且驗證結果未出現錯誤) 建立最適化表單時，流程最後會失敗。接著，重新整理頁面後，表單無法正確地載入，顯示空白表單並在紀錄中顯示錯誤。
- FORMS-8964：在 Android™ Chrome/Firefox 中，如果達到字元數上限，則文字方框元件中的文字會變得無法編輯。
- FORMS-8668：儘管功能表單會轉譯，但錯誤紀錄中的 Java™ 堆疊傾印過多，導致紀錄檔案膨脹。
- FORMS-8554：啟用延遲載入的最適化表單在作者執行個體的預覽模式下無法運作。
- FORMS-8177：當表單服務使用中時，「com.adobe.aem.formsndocuments.publish.AssetReferenceProvider 無法擷取資產相依性。」的異常狀況發生。停用表單服務後該錯誤即消失。
- FORMS-3691：部分物件缺少 IIFE (立即呼叫函數運算式) 範圍。使用 IIFE 的主要目的是為函數內的變數建立範圍，以防止這些變數污染全域範圍。
- SITES-15463：網站範本 — 無法發佈範本。

### 已知問題 {#known-issues-13206}

- SITES-15359：內容片段 — 變數名稱模式無法正確比對具有 ```'_'``` 資源名稱中的。
- Forms-10444：最適化Forms範本 — 無法發佈範本（因應措施：使用發佈主控台）。
- CQ-4354191：工作流程 — 由於nt：unstructured節點上存在復寫中繼資料，自訂啟動器可能會觸發許多次（因應措施：更新啟動器以排除復寫中繼資料屬性以避免重疊）。
- SITES-15622： GraphQL — 使用數字引數的持續查詢問題。

### 內嵌技術 {#embedded-tech-13206}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
