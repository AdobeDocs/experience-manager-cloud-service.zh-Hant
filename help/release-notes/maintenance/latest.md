---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 5e01d1674134db73fc0f5c0013e10170ad6747f7
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 18%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 23862 版 {#23862}

以下摘要說明維護版本23862數的持續改善，該版本於2025年12月23日公開發佈。 前一個維護版本是 23482 版。

啟用 2026.1.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-23862}

* CQ-4361812：新增對rest api中選用的param folderPath的支援。 說明：新的翻譯專案由API建立，將放置在選用的`folderPath`引數指定的路徑內，否則預設為根專案路徑`/content/projects`。
* Forms-21960：新增本機畫布編輯的互動式通訊支援，與forms-spa類似。
* Forms-22001：新增指引，以減少AEM Forms as a Cloud Service中的大量`/etc.clientlibs/toggles.json`請求。
* Forms-22496：在Invoke服務中公開原始ResponseBody。
* Forms-22495：在SetProperty規則中新增預留位置屬性。
* Forms-21925： UBS註腳格式：載入表單時顯示表單中的所有註腳。
* Forms-20536：在規則編輯器中公開完整回應的選項，但不進行對應。
* SITES-37199：註解功能透過未驗證的`authorizables.json`呼叫觸發存放庫周遊，導致效能降低。
* SITES-37118：產品駕駛艙中的Commerce Optimizer支援。
* SITES-38029：新增記錄以在修改事件時追蹤MSM推送。
* SITES-37050：支援「強製取消發佈」，可取消發佈其他已發佈資源所參考的內容片段。
* SITES-37142：新增透過內容片段PATCH簽入/簽出內容片段的功能。
* SITES-37613：在CF API許可權端點中，如果使用者可以簽入內容片段，則傳回簽入，或者如果使用者可以簽出內容片段，則簽出。
* SITES-37835：嘗試建立多個具有相同標題但未提供名稱的內容片段時，會自動產生新名稱，而不會因衝突而失敗。
* SITES-36823：使用Universal Editor的Edge Delivery：移除對索引反向對應的必要性。
* SITES-34751：使用通用編輯器的Edge Delivery：發佈時不受支援的檔案型別和路徑超出限制（搶先存取）時失敗。
* SITES-37888：使用通用編輯器的Edge Delivery：將Alt尾碼用作連結文字的同義詞。
* SITES-19850：使用通用編輯器的Edge Delivery：新增對試算表中多個工作表的支援。
* SITES-32490：使用通用編輯器的Edge Delivery：將對data-aue-component和使用者定義的data-aue-label的支援新增到區塊和預設內容。
* SITES-37794：使用通用編輯器的Edge Delivery：簡化頁面建立精靈。
* SITES-36963：將對象/區段端點移轉至Target API v3以獲得Workspace支援。

### 已修正的問題 {#fixed-issues-23862}

* CQ-4361831：修正導致genai_dropdown_span未定義的問題。
* CQ-4360895：修正並行更新期間專案中翻譯工作狀態計數不準確的問題。
* CQ-4361599：修正2025.7升級後略過翻譯工作的內容片段問題。
* CQ-4360747：固定的可重複翻譯工作會建立空的負載並經常觸發（ScheduleRepeatTranslationProject中的NullPointerException）。
* CQ-4359994：修正單一語言和多語言專案的destinationLanguage欄位型別不一致問題。
* SITES-38153：修正uuid型參考的cf發佈參考提供者。
* SITES-37594：依據標籤功能的模型效能改善。
* SITES-37337： FragmentCreateProcessor：在記錄中提供其他錯誤詳細資料。
* SITES-33666：內容片段編輯器中未本地化的「無法列印片段的Json」錯誤訊息。
* SITES-33675：在內容片段編輯器>關聯內容中硬式編碼的「未定義」字串。
* SITES-30715：內容片段編輯器中未本地化的「一般」字串。
* SITES-28592：內容片段模型編輯器> 「模型已鎖定」對話方塊中未本地化的字串。
* SITES-977：字串「標籤」和「集合」在編輯內容片段頁面上未本地化。
* SITES-29699：內容片段編輯器中允許的資產型別未本地化。
* SITES-25240： Teaser強制回應視窗中的Call to action欄位沒有可見標籤。
* SITES-24869：範本編輯器>分隔符號>原則中的工具提示遭截斷。
* SITES-19313：在範本編輯器中將元件拖放至已刪除的範本時，發生未當地語系化錯誤。
* SITES-18103：在「頁面編輯器>工作流程」中未當地語系化的字串。
* SITES-17501：範本編輯器>元件原則編輯器中的未當地語系化字串。
* SITES-15091：體驗片段的文字元件屬性上的字串未本地化。
* SITES-8113：「工具」選單中「範本」的「選取影像」對話方塊中的「Assets」字串未本地化。
* SITES-37587：在RolloutManagerImpl中具有NPE的PROD中，即時副本建立仍會失敗。
* SITES-37335：即時副本頁面屬性在與cq標籤相關的主控台中顯示錯誤。
* SITES-36972：可編輯工具列中缺少「轉出」按鈕。
* SITES-36570：啟動分塊建立即時副本切換後，建立即時副本失敗。
* SITES-36158：轉出失敗，作業由於例外狀況而失敗。
* SITES-35655：新的CF編輯器在中斷後會顯示作用中繼承。
* SITES-31425：在網站的開始工作流程中顯示未本地化的錯誤訊息「錯誤：需要{}欄位」。
* SITES-19802：工具提示在「核心元件網站>目錄」中未本地化。
* SITES-36543：修正允許管理員編輯已簽出內容片段的問題。
* SITES-36967：修正嘗試為損毀的內容片段產生縮圖資料時發生的NullPointerExceptions。
* SITES-37791：修正呼叫包含`$`之字串的FindAndReplace會失敗的問題。
* SITES-37018：複製包含不允許的範本路徑的頁面時出現空白錯誤快顯視窗。
* SITES-36243：使用通用編輯器的Edge Delivery：發佈`sling:OrderedFolder`時修正404。
* SITES-37684：使用通用編輯器的Edge Delivery：修復有許多網站的環境中的效能降低。
* SITES-37840：使用通用編輯器的Edge Delivery：修正由於Edge Delivery的存取權杖過期而造成的發佈失敗。
* SITES-37933：使用Universal Editor的Edge Delivery：修正（取消）發佈啟動中所刪除資源的失敗。
* SITES-37870：使用通用編輯器的Edge Delivery：啟用多欄位支援後，修正自訂頁面中繼資料轉譯中斷的問題。
* SITES-37349：使用通用編輯器的Edge Delivery：將具有單一專案的多個欄位顯示為具有單一清單專案的清單。
* SITES-36148：使用通用編輯器的Edge Delivery：修正複合多欄位的data-aue-label。

### 已知問題 {#known-issues-23862}

無。

### 已過時的功能和 API {#deprecated-23862}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-23862}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決 23 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-23862}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.88.0 | [Oak 1.88.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.2 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
