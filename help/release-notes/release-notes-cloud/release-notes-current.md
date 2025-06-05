---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: f01e5f505074ea32f313ba781ddb4e026cd47888
workflow-type: tm+mt
source-wordcount: '2067'
ht-degree: 30%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>您可以從這裡瀏覽至先前版本 (例如 2023 或 2024 版) 的發行說明。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}


[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2025.5.0)的發行日期是2025年6月5日。 下一個功能版本(2025.6.0)計畫於2025年6月26日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440931?quality=12&captions=chi_hant)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**AI產生的中繼資料**

AEM Assets現在使用[AI來自動產生中繼資料，包括標題、說明和關鍵字](/help/assets/metadata-assets-view.md#ai-smart-tags)。 這些AI產生的欄位可增強中繼資料的準確性，讓資產更容易搜尋、分類和推薦。 此方法不僅可避免手動標籤，進而提升效率，還可確保大量數位內容的一致性和擴充性。

![AI產生的中繼資料](/help/assets/assets/enhanced-smart-tags.png)

**與Figma整合**

AEM Assets與Figma原生整合，可讓設計人員從Figma使用者介面內直接存取AEM Assets中儲存的資產。 您可以在Figma畫布中置入AEM Assets中管理的內容，然後將新內容或編輯過的內容儲存在AEM Assets存放庫中。

![與Figma整合](/help/assets/assets/figma-integration.png)


### Content Hub中的新功能 {#new-features-content-hub}

**以屬性為基礎的存取控制(ABAC)**

Content Hub現在可讓您套用規則型限制來存取資產。 資產許可權可確保治理，也確保使用者只能存取相關的資產。

資產限制規則是根據中繼資料，如果規則中定義的條件符合資產中繼資料，則會向使用者群組顯示資產。

屬性式存取控制的一些主要優點包括：

* 消除許可權對檔案夾結構的相依性

* 允許管理員上傳資產並回溯決定許可權結構

* 減少重複專案數量 — 改善資產完整性。 當相同的資產與不同群組共用時，資料夾型許可權需要重複專案。

**UI品牌**

Content Hub現在可讓管理員使用品牌特定元素來自訂使用者介面，包括橫幅影像、橫幅標題和本文文字，以及主要和次要顏色。 這些增強功能有助於確保品牌一致性、簡化使用者上線並建立信任。

![UI品牌](/help/assets/assets/content-hub-ui-branding.png)

**公用連結共用**

Content Hub現在支援產生分享連結，讓沒有應用程式存取權的外部使用者檢視資產中繼資料或下載資產。

![UI品牌](/help/assets/assets/public-and-private-link.png)

**集合治理**

Content Hub現在可讓您在建立期間控制對集合的存取權，確保只有授權使用者才能檢視或管理已分組的資產。 它可確保改善安全性、改善共同作業、井然有序的資產管理，以及簡化治理。

![集合治理](/help/assets/assets/collection-permissions.png)

>[!NOTE]
>
>集合治理是有限的可用性功能。 您可以透過建立支援票證來啟用它。

**以ZIP檔下載多個資產**

Content Hub現在也可讓您將選取的資產及其轉譯下載為ZIP檔案，而非個別檔案，以簡化您的檔案管理。

**Content Hub中的Dynamic Media轉譯**

直接從Content Hub使用者介面存取下載的所有Dynamic Media預設集轉譯和智慧型裁切。

{&#x200B;0}Dynamic Media轉譯![&#128279;](/help/assets/assets/dm-renditions-content-hub.png)

### Dynamic Media中的新功能 {#new-features-dynamic-media}

**Dynamic Media與AJO B2C原生整合&#x200B;**

Experience Manager (AEM) Dynamic Media與Journey Optimizer (AJO) B2C的原生整合，使行銷人員可輕鬆將AEM Dynamic Media資產（轉譯和DM範本）內嵌至AJO內容，並提供即時更新和跨管道的超個人化體驗。

{&#x200B;0}Dynamic Media轉譯![&#128279;](/help/assets/assets/dm-ajo-integration.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 搶鮮版功能

* [通用編輯器：表單片段](/help/edge/docs/forms/universal-editor/creating-form-fragments.md)：您現在可以透過通用編輯器為自適應表單建立表單片段並重複使用。這些片段是可重複使用的表單區段 (例如，聯絡資訊、同意欄位)，僅需建置一次即可套用於多個表單。此功能可以簡化表單建立過程、確保一致性，並且提高製作效率。

* [SharePoint 文件庫：以原始檔案名稱儲存附件](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library)：您現在將表單附件儲存於 SharePoint 文件庫中時，可以選擇使用其原始檔案名稱。此增強功能可以簡化上傳之檔案的識別和管理。

* **規則編輯器**：
   * [「When」子句中點擊事件的二元條件](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：規則編輯器現在可以將按鈕點擊事件 (_Is Clicked_) 與「When」子句中的其他條件結合。因此可以根據使用者互動和其他因素，對規則執行進行更精確的控制。備註：使用多個條件時，點擊事件必須是列出的第一個條件。
   * [欄位和面板的驗證條件](/help/forms/rule-editor-core-components-usecases.md)：規則編輯器現在包含 _IsValid_ 和 _IsNotValid_ 條件。因此您可以查看特定欄位或整個面板 (包括水平標籤、垂直標籤、摺疊式面板和精靈等版面) 的驗證狀態，進而根據驗證結果改善表單導覽和使用者體驗。
* [改進 SharePoint 清單的範圍管理](/help/forms/connect-forms-to-sharepoint-list.md)：SharePoint 網站現在支援所有受管理的路徑，例如 /sites 和 /teams。此增強功能讓跨各種 SharePoint 網站結構的整合範圍更為寬廣，在連結組織內容方面提供更大的靈活度。
* [支援將記錄文件儲存至 SharePoint 清單](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields)：使用 SharePoint 清單式表單資料模型 (FDM) 所建立的表單，現在可以透過設定記錄文件繫結參考欄位屬性，將記錄文件 (DoR) 儲存至 SharePoint 清單。此增強功能可以將支援的表單資料和文件與 SharePoint 儲存空間緊密整合。

### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### Adobe Experience Platform (AEP) 與 Forms 的整合

早期採用者現在可以使用 Forms 和 AEP 之間的整合功能。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 已更新淘汰流程 {#updated-deprecation-process}

Adobe會定期審查功能、程式庫、API和設定，以確保符合效能、安全性和價值標準。 當功能不再符合這些標準時，就會標示為過時，並且必須在指定的移除日期前停止使用。 在此日期之前，Adobe會透過電子郵件通知提醒客戶，以及在繼續或部署新組建之前需要在Cloud Manager中採取的動作。 若未採取必要的行動，可能會導致無法升級至新版AEM，進而對安全性、效能、可靠性和可用性造成潛在影響。

如需進一步資訊，請參閱[過時文章](/help/release-notes/deprecated-removed-features.md)。

#### 即將移除的棄用Java API和OSGi設定 {#deprecated-near-removals}

展開下列清單以檢視不再使用的已棄用API和OSGi設定。 如需完整詳細資訊（包括移除時間表），請參閱淘汰文章。

<details>
  <summary>展開以檢視棄用的專案</summary>

Java API：
* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

OSGi屬性：

* `org.apache.sling.commons.log.LogManager` （所有屬性）
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`， `org.apache.sling.commons.log.pattern`)

</details>

### 不再使用Java 11執行階段 {#java11-runtime-deprecation}

**Java 11執行階段**&#x200B;現已棄用，且大部分環境已升級至效能更高的&#x200B;**Java 21執行階段**。

如果因為不受支援的相依性而無法升級您的環境（請參閱[Java 21執行階段需求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)），您應該已經收到來自Adobe的電子郵件，其中包含特定的後續步驟。 請確定所有必要的更新已於&#x200B;**2025年8月28日**&#x200B;前完成，以便您的環境可以升級而不會中斷。

注意：執行階段版本與您的程式碼組建版本不同。 雖然我們建議您使用Java 21進行建置，但目前仍支援Java 11建置。 未來將針對Java 11組建分享獨立的淘汰通知。

### 實施AEM Java記錄檔設定原則 {#logconfig-policy}

如4月發行說明中所述，AEM Java記錄必須遵循標準格式，以確保在所有客戶環境中進行可靠的監控。 不再支援自訂日誌配置，例如對日誌格式、輸出檔案或預設日誌層級的變更。 記錄檔必須保持導向至預設檔案，且AEM產品代碼的預設記錄層級必須保留。 請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)中的完整詳細資料。

從&#x200B;**8月**&#x200B;日下旬開始，任何不支援的自訂記錄覆寫都會被忽略。 根據我們的分析，大部分客戶將不會受到影響，而Adobe將直接聯絡其目前設定可能受到影響的任何客戶。

請檢閱並更新依賴自訂記錄行為的任何下遊程式。 例如：

* 如果您的記錄轉送系統需要自訂記錄格式，您可能需要調整擷取規則。
* 如果您先前已透過變更記錄層級來減少記錄詳細程度，請注意，回覆至預設層級可能會增加記錄數量。

### 預設清除舊版和稽核記錄 {#mt-defaults}

目前，內容版本和稽核記錄預設會停用其相關聯的&#x200B;*清除維護任務*，因此除非透過其各自的OSGi屬性明確設定，否則不會移除任何資料。

但是，為了最佳化存放庫效能，從&#x200B;**2025年6月下旬**&#x200B;開始，將依照以下准則預設啟用清除：

#### 內容版本 {#mt-content}

* **新環境** (建立於即將來臨的日期之後（稍後通知）
   * 將定期刪除超過&#x200B;**30天**&#x200B;的版本。
   * 會保留最近30天內的5個版本，以及最新版本和目前版本，無論其年齡為何。

* **現有環境** （在此即將到來的日期之前建立）：
   * 將定期刪除超過&#x200B;**7年**&#x200B;的版本。
   * 系統會保留過去7年內的所有版本。
   * 此高預設臨界值可防止近期資料意外移除。 不過，建議設定較低的值，將存放庫效能最佳化。

* 您可以透過OSGi設定覆寫來修改這些預設值。

#### 稽核記錄 {#mt-auditlogs}

* **新環境** （建立於即將來臨的日期之後，將另行通知）：
   * 將定期刪除超過&#x200B;**7天**&#x200B;的復寫、DAM和頁面稽核記錄。
   * 預設會記錄所有事件。

* **現有環境** （在此即將到來的日期之前建立）：
   * 將定期刪除超過&#x200B;**7年**&#x200B;的復寫、DAM和頁面稽核記錄。
   * 預設會記錄所有事件。
   * 此高預設臨界值可防止近期資料意外移除。 不過，建議設定較低的值，將存放庫效能最佳化。

* 您可以透過OSGi設定覆寫來修改這些預設值。

如需詳細資訊，請參閱[維護任務文章](/help/operations/maintenance.md#default)。

### Edge運算(Alpha計畫) {#edge-computing}

Edge運算可讓您在CDN層執行JavaScript，讓資料處理更貼近使用者。 這能減少延遲，並啟用邊緣的回應式動態體驗。

常見使用案例包含：

* 在授與內容的存取權之前，使用身分提供者來驗證使用者
* 根據地理位置、裝置型別或使用者屬性製作個人化內容
* 充當CDN與您的來源之間的中介軟體
* 將來自協力廠商API的回應重新格式化（並可能彙總多個API回應），然後再傳送給瀏覽器
* 使用從不同後端拼接的內容，在邊緣構成及提供伺服器轉譯的HTML

我們對於即時生產網站的AEM發佈傳遞或Edge Delivery Services專案的可用機會有限。 若您有興趣參與或想深入瞭解，請傳送電子郵件至[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，簡述您的使用案例。

### Edge Delivery Services (Beta計畫)的CDN設定 {#cdn-eds-beta}

Adobe-Managed CDN提供彈性的設定選項，如[設定管道文章](/help/operations/config-pipeline.md#configurations)所述。

現在在Beta版中，針對包括CDN來源選擇器、回應和請求轉換等功能部署設定管道。 請聯絡[aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com)並提供您使用案例的詳細資料。

### AEM記錄轉送至更多目的地(Beta計畫) {#log-forwarding-beta}

雖然可以從 Cloud Manager 下載記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是很有幫助的。AEM已支援AEM和CDN記錄轉送至Azure Blob Storage、Datadog、HTTPS、Elasticsearch （和OpenSearch）和Splunk。 此功能是以自助方式設定，並透過設定管道進行部署。

現在處於Beta版，您可以將AEM記錄轉送至Amazon S3、Sumo Logic和您自己的New Relic帳戶(非Adobe提供的帳戶)。 請注意，這些記錄目的地支援AEM記錄(包括Apache/Dispatcher)，但CDN記錄不受支援。 發送電子郵件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) 以獲得存取權。

如需了解更多，請參閱[記錄轉送文件](/help/implementing/developing/introduction/log-forwarding.md)。

## [!DNL Experience Manager] Guides {#guides}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)找到最新版 Adobe Experience Manager Guides 的新功能和增強功能完整清單。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

## 通用編輯器 {#universal-editor}

您可以在[這裡](/help/release-notes/universal-editor/current.md)找到通用編輯器版本的完整清單。

## 產生變化版本 {#generate-variations}

您可以在[這裡](/help/generative-ai/release-notes-generate-variations.md)找到「產生變化版本」版本的完整清單。

## Experience Cloud 發行說明 {#experience-cloud}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/release-notes/experience-cloud/current)查看其他 Experience Cloud 應用程式版本的相關資訊。
