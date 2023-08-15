---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b2c67687e2f3577b44929777a31b6ce85a5f1877
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 22%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 13099 版 {#release-13099}

以下摘要說明維護版本13099數的持續改善，該版本於2023年8月15日公開發佈。 此維護版本是先前 12874 維護版本的更新。

2023.8.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-13099}

- SITES-13906： GraphQL — 升級至graphql-java 20.1。
- SITES-8972： GraphQL — 新增選項```label``` JSON中用於列舉資料型別。
- SITES-9689： GraphQL — 在JSON中新增內容參考資料型別的標題和說明。
- SITES-13052：內容片段 — 將內容片段匯出至Adobe Target

### 已修正的問題 {#fixed-issues-13099}

- SITES-14937： MSM — 從父項繼承轉出設定值在點選即時副本的儲存並關閉時切換。
- SITES-14847：內容片段 — 內容片段連結未醒目提示。
- SITES-11620：內容片段 — 參考路徑在UI中稍微剪下。
- SITES-14171： GraphQL — 在某些情況下，快取資料的循環參考不會失效。
- SITES-14577：體驗片段 — 大量發佈不適用於即時副本。
- SITES-14341：管理員UI — 移除刪除許可權時，「屬性」按鈕的行為不一致。
- SITES-11000：管理員UI — 參考：某些頁面中缺少傳入連結。
- SITES-11559：管理員UI — 參考：傳入連結顯示錯誤的頁面。
- SITES-14337：管理員UI — 開啟編輯器頁面會在特定情況下產生錯誤。
- SITES-13425：按一下ContextHub按鈕時，ContextHub — 功能表列未顯示。
- Forms-9971：以其他語言環境轉譯調適型表單時，會解譯和錯誤套用元件的可見度。
- Forms-9888：當最適化表單設定為在表單提交時重新導向至外部URL （感謝頁面）時，它無法重新導向至外部URL。
- Forms-9845：使用規則編輯器清除下拉式清單後，儘管假設有間隙，先前提供的值仍會持續存在。
- Forms-9263：當核取方塊的標籤包含特殊字元，且使用者按一下核取方塊時，個別核取方塊未選取。
- Forms-9254：當使用者捲動條款與條件元件的文字時，元件內的核取方塊甚至在使用者捲動整個文字之前都會自動啟用。
- Forms-9045：指令碼標籤無法解析基礎XDP中的外部片段參考。
- Forms-9026：嘗試使用JSON結構描述建立最適化表單時，該結構描述具有包含空字串的列舉且驗證沒有錯誤，流程會導致失敗。 接下來，在重新整理頁面時，表單無法正確載入，顯示空白表單並在日誌中顯示錯誤。
- Forms-8964：在Android™ Chrome/Firefox中，如果達到字元數上限，文字方塊元件中的文字會變成無法編輯。
- Forms-8668：儘管呈現了功能表單，但錯誤記錄中仍存在過多的Java™棧疊傾印，導致記錄檔案膨脹。
- Forms-8554：啟用延遲載入的最適化Forms無法在作者執行個體的預覽模式中運作。
- Forms-8177：當表單服務作用中時，例外狀況「com.adobe.aem.formsndocuments.publish.AssetReferenceProvider無法擷取資產相依性」。 發生。 停用表單服務時，錯誤會消失。
- Forms-3691：某些物件遺失IIFE （立即叫用函式運算式）範圍。 使用IIFE的主要目的，是為了在函式內建立變數的範圍，防止這些變數汙染全域範圍。


### 已知問題 {#known-issues-13099}

- SITES-15359：變數名稱模式無法正確比對具有 ```'_'``` 資源名稱中的。

### 內嵌技術 {#embedded-tech-13099}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
