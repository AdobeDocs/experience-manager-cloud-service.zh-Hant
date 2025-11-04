---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 89597ae0c54b1b2f42f597f556276700545ecd26
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 42%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

>[!NOTE]
>
>發行說23122已於11月3日設為私人。

## 22943 版 {#22943}

以下摘要說明維護版本22943數的持續改善，該版本於2025年10月14日公開發佈。 前一個維護版本是 22758 版。

2025.10.0 功能啟用會提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-22943}

* Assets-57809： damAssetLucene-13的索引定義更新。
* Assets-36521：改善DM重新上傳工作流程，確保後續處理的一致性。
* Assets-56400：為具透明度的資產新增新的OOTB縮放PNG轉譯。
* Assets-55326：透過HTTP事件啟用AI中繼資料資料夾設定檢視。
* Assets-56905：支援透過Proxy連線至Indesign。
* Assets-48286：將CAI屬性新增至GenStudio的Algoria。
* Assets-48653：在預先處理階段套用隱藏的浮水印。
* Assets-55874：將影像預設集從scene7移轉至DMWithOpenapi。
* SITES-30452： /content/definition端點上ASO的內容API改善。

### 已修正的問題 {#fixed-issues-22943}

* Assets-56301：修正選擇性中繼資料匯出以包含CSV中的PredictedTags。
* Assets-55543：將非同步處理邏輯重構為可重複使用的套件組合。
* Assets-54789：啟用DM ACL時，修正ACLPermissionsValidator中的NPE。
* Assets-55888：修正UI轉譯面板中顯示的惡意程式碼轉譯。
* GRANITE-62236：修正智慧型集合的已儲存搜尋中的關鍵字本地化問題。
* GRANITE-61875：修正無法儲存內容片段和資產下載的「運算式評估無效」Hotfix問題。
* SITES-24074：修正在鍵盤標籤導覽期間接收焦點的隱藏行動導覽。
* SITES-33611：修正大量市場的即時副本概觀問題。

#### AEM Guides {#guides-22943}

* GUIDES-31421：開啟多個DITA map或主題，且其中一個主題關閉時，顯示所有開啟索引標籤的&#x200B;**>>**&#x200B;按鈕與索引標籤列上的其餘開啟索引標籤重疊。
* GUIDES-33229：產生PDF時，如果任何屬性名稱包含句點，則會忽略DITAVAL檔案中的篩選規則。
* GUIDES-33720：縮放翻譯UI畫面時，傳送以供翻譯按鈕會移至省略符號下方，即使未選取任何資產也會啟用。
* GUIDES-33590：當稽核者完成稽核任務或發起者更新稽核任務而未輸入註解時，傳送的通知電子郵件會顯示最近的前一個註解。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已過時的功能和 API {#deprecated-22943}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-22943}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決 14 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 變更通知

* 此版本包含以下新產品索引版本：
* **damAssetLucene-13**

### 嵌入技術 {#embedded-tech-22943}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.2 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
