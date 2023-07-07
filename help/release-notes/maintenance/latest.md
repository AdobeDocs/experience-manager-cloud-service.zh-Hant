---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1251f36ece4449d8be6a40f34421351161bf3b23
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 19%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 12549 版 {#release-12549}

以下摘要說明2023年7月4日公開發佈的維護版本資12549的持續改善。 此維護版本是先前 12255 維護版的更新。維護發行說12549會取代12441以修正兩個問題。

2023.7.0 Feature Activation將提供此維護版本的完整功能集。 請參閱 [Experience Manager發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) 以取得詳細資訊。

### 增強功能 {#enhancements-12549}

- Forms-5054：新增對所有 [雕像](https://opensource.adobe.com/acrobat-sign/acrobat_sign_events/webhookeventsagreements.html) Adobe Sign支援。

### 已修正的問題 {#fixed-issues-12549}

- 各種與協助工具相關的更新
- SITES-12688：頁面編輯器：邏輯運運算元或無法在資產尋找器搜尋中正常運作
- SITES-4951：頁面編輯器：頁面編輯器中的標籤搜尋找不到子標籤
- SITES-12465：體驗片段：體驗片段元件對話方塊中的箭頭鍵無法運作
- SITES-12893：體驗片段：套用體驗片段的循環參考驗證
- SITES-12715：體驗片段：套用至體驗片段資料夾的雲端服務設定未持續存在
- SITES-13097：體驗片段：無法新增體驗片段至翻譯專案
- SITES-13165： GraphQL：還原篩選null值的預設行為
- SITES-12577：連結檢查器：轉換器不會間歇性地重寫連結
- SITES-13559： MSM：轉出元件時擲回「不可修改」例外狀況
- SITES-11757： MSM：從父項繼承轉出設定不會為子頁面回覆
- SITES-14073：網站管理員：選取沒有要匯出的屬性時，CSV報表因500失敗
- Forms-7648：無法驗證數值方塊元件中的最大位數。 驗證指令碼無法運作。
- Forms-8177： Forms服務作用中時， `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider Failed to retrieve asset dependencies` 發生錯誤。
- Forms-8300：當使用者嘗試在開啟任務後委派任務時，委派回應會重新載入任務，而不是開啟使用者的AEM收件匣UI。
- Forms-8500：在啟用IE模式選項的Microsoft® Edge瀏覽器上，HTML5 Forms無法開啟。
- Forms-8541：轉譯最適化Forms時，會發生Null指標例外狀況。
- Forms-8964：在Google Chrome或Mozilla Firefox的Android™裝置上開啟表單時，無法移除文字方塊元件中輸入的文字。
- Forms-9026：當使用者根據複雜且有效的JSON結構描述建立調適型表單時，將相關的JSON結構描述欄位拖曳至調適型Forms編輯器以建立調適型Forms欄位，並重新整理「調適型Forms編輯器」視窗，所有欄位都會被刪除，且調適型Forms編輯器顯示為空白。
- Forms-9263：當核取方塊選項的顯示文字包含特殊字元時，使用者無法選取這類核取方塊。
- Forms-8668：呈現表單的「PDF預覽」時，錯誤記錄中會出現一些非必要的Java™棧疊傾印。 不過，轉譯表單時沒有問題。
- Forms-8116：將規則套用至最適化Forms容器元件時，未儲存套用的規則。
- Forms-7906：將最適化表單新增至AEM Sites Container元件時，無法開啟規則編輯器。
- Forms-8846： Bind參考屬性不適用於最適化Forms附件元件。
- Forms-9072：當您在建立表單片段時搜尋配置時，搜尋結果不會傳回任何供選取的結構描述。
- Forms：修正多項與協助工具相關的錯誤，以改善AEM Forms功能的協助工具。

### 已知問題 {#known-issues-12549}

- SKYOPS-61385：透過最新的Dispatcher更新，某些先前被無訊息忽略的無效規則運算式 `libpcre1` 不再為已更新的接受 `libpcre2` 部署期間。 Dispatcher設定檢查即將更新，以便更早識別這些專案。

### 內嵌技術 {#embedded-tech-12549}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | 2.27.0 版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.0 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
