---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 859af15f4038b28e6e1398e5168dc008d22985e9
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 96%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

>[!NOTE]
>
> 發行版本20936和20783已設為私人。

## 版本 20626 {#20626}

以下為 20626 維護版本持續改善內容的摘要；該版本於 2025 年 4 月 29 日公開發行。前一個維護版本為版本 20476。

2025.5.0功能啟動提供此維護版本的完整功能集。 如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-20626}

* ASSETS-46413、ASSETS-46580：新增新的審查狀態「預覽」。
* ASSETS-49542：擴充影片和音訊轉錄與翻譯的支援語言。
* ASSETS-48264：擴充針對轉譯的 PNG 品質支援。

### 已修正的問題 {#fixed-issues-20626}

* ASSETS-50387：更正於 GenStudio 中使用的內容片段預設縮圖。
* ASSETS-49006：當使用者沒有寫入權限時，顯示影片屬性。
* ASSETS-46757、ASSETS-46997：提升智慧裁切編輯器的可存取性。
* ASSETS-48018：改善資產發佈報告中的資產參考追蹤。
* ASSETS-35846：提升作者和交付層之間的存取一致性。
* ASSETS-48171：提升 Dynamic Media 範本與 Canvas 的一致性。
* ASSETS-49813：改善過期通知。
* ASSETS-47768、ASSETS-49825、ASSETS-49008、ASSETS-48287：提升批次作業的管理與可見性。
* ASSETS-50003、ASSETS-50004：改善資產下載中所包含之版本的命名和控制。
* ASSETS-47939：改善 Content Hub 的回應組織。
* ASSETS-46738：提升極大集合的績效。
* ASSETS-50121：提升資產發佈事件的可靠性。
* ASSETS-48490：提升影像攝取期間自動處理的彈性。
* ASSETS-28106、ASSETS-49404：提升全文搜尋的穩健性。
* ASSETS-50006、ASSETS-50423：提升大型資料夾內的搜尋和周遊效能。
* ASSETS-46021：改善 Safari 和行動瀏覽器的影片顯示。
* ASSETS-49002：改善編輯 Dynamic Media 範本的處理過程。
* ASSETS-48376：Content Hub 使用者介面中的其他改善。
* ASSETS-48504、ASSETS-49378：對使用者介面行為進行的其他改善。
* ASSETS-49540：將資產關係 OpenAPI 移出實驗性階段。
* ASSETS-40284：更新關於 Adobe Stock 整合的文件。
* ASSETS-49739：致力於自 Asset Selector 整合 Figma。

#### AEM 指南 {#guides}

* GUIDES-21734：當透過片段新增元素，或透過範本建立元素時，即使在 XMLEditorConfig 中啟用自動產生 ID 選項，仍無法為元素產生新的 ID。
* GUIDES-25969：如果 DITA 主題中的外部連結缺少 `scope=external` 屬性，HTML5 會發佈失敗，但不會在錯誤記錄中指出遺失此屬性的檔案，尤其是啟用微服務時。
* GUIDES-27288：無法將中繼資料屬性傳遞給使用新 AEM Sites 發佈所產生之對應的登陸頁面。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-20626}

無。

### 已過時的功能和 API {#deprecated-20626}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-20626}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 11 個已確認的弱點，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-20626}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.78.0 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
