---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 6e82bbcc1b83fa9216831f6f746665507a46eec7
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 24%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 14029 版 {#release-14029}

以下摘要說明維護版本14029數的持續改善，該版本於2023年10月25日公開發佈。 此維護版本是先前 13804 維護版本的更新。

2023.11.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-14029}

* ASSETS-28551：改善「我的連結共用」UI的擴充性
* ASSETS-28566：新增dam：metadataForm Lucene索引
* ASSETS-29281：更新RAPI以傳送v2下載事件

### 已修正的問題 {#fixed-issues-14029}

* ASSETS-25199：影像核心元件未顯示正確的智慧型裁切
* ASSETS-26142：如果探索要求失敗或中斷，則未設定或重新嘗試unified-shell.js customEnvLabel
* ASSETS-26416：在搜尋表單中，相對日期述詞一律定義為「1天前」
* ASSETS-27321：清除群組快取中有關團隊成員資格的變更
* ASSETS-27591：修正對舊版org.json的相依性
* ASSETS-28439：未設定全域封鎖清單時的智慧標籤封鎖清單NPE
* ASSETS-28612： &quot;repository-api&quot;中的BlockedTagResolver修正
* ASSETS-28634：Adobe存量中的Omnisearch欄位未自動新增資產資料
* ASSETS-28727：處理設定檔設定清單未顯示指定的自訂高度和寬度值
* ASSETS-29056：新增轉碼轉譯AEM標準處理設定檔
* ASSETS-29105： RDE功能模型中SecurityProviderRegistration requiredServicePids缺少限制提供者
* ASSETS-29106：在啟用Unified Shell的AEM上檢視Adobe庫存擲回錯誤
* ASSETS-29115：移除限制提供者路徑的設定屬性
* ASSETS-29208：註冊CompleteUploadAssetServlet服務之前，傳送至作者Pod的請求造成資產上傳錯誤
* ASSETS-29297：使用已簽出篩選器選項建立儲存搜尋時的問題
* ASSETS-29363：中繼資料設定檔未套用IPTC的預設值
* ASSETS-29404：連結共用報表達到查詢限制
* ASSETS-29431：移除舊功能標幟
* ASSETS-29443：當Granite Shell標頭模式變更為「選取」時，Unified Shell Hero仍可見，且可供點選
* ASSETS-29476： scene7DAMService.getS7FileReference(asset) Api呼叫未傳回預期值。
* ASSETS-29515：具有「jcr：lastModifiedBy」的資產/節點：「workflow-process-service」在清單檢視中顯示為「外部使用者」
* ASSETS-29579：非管理員使用者無法建立影像集
* ASSETS-29631：使用dam：roles進行安全傳送/搜尋
* ASSETS-29689：dc：roles （以及新屬性dam：roles）應該從AEM端篩選
* ASSETS-29738：資產上傳限制因NullPointerException而失敗
* ASSETS-29779：小型資產無法處理至Webp，因為不在Blob儲存體中
* ASSETS-29892：中繼資料匯出在包含大量資產的資料夾上失敗
* ASSETS-29996：僅在PROD例項上間歇性上傳資產時，以「外部使用者」作為修飾元
* ASSETS-30167：上傳資產後adobe_dam：restrictions的HTML中斷
* ASSETS-30276：共用連結UI：無法從assetdetails共用
* ASSETS-30434：資產處理完成事件未傳送至管道
* ASSETS-30519：將RAPI新增至REDMetricsServletFilter
* CQ-4354413： QueryBuilder：含方括弧的查詢被錯誤轉譯為xpath
* CQ-4354834：無法在收件匣任務中新增評論
* CQ-4354836：無法從專案控制檯啟動工作流程或建立任務
* CQ-4354867： ToggleCondition參考參考InstanceActionServlet中不存在的欄位
* CQ-4354895：AEM翻譯套件：10月12日
* GRANITE-45560：事件信封中的通用結構描述表示
* GRANITE-47267：更新到 Apache Felix Http Jetty 4.2.18
* GRANITE-47599：內容匯入自13323升級後失敗(JCRVLT-721)
* GRANITE-47873：Apache Felix Webconsole 4.9.6的更新

### 已知問題 {#known-issues-14029}

無。

### 內嵌技術 {#embedded-tech-14029}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
