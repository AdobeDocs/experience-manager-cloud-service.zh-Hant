---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: af9e30ffb585619d1581db94d3961f561e12df2b
workflow-type: tm+mt
source-wordcount: '2261'
ht-degree: 31%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本(2024.3.0)為2024年4月11日。 下一個功能版本(2024.4.0)計畫於2024年4月25日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- ## Release Video {#release-video}

Have a look at the March 2024 Release Overview video for a summary of the features added in the 2024.3.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

**Edge Delivery Services的AEM製作**

AEM Sites現在可作為Edge Delivery Services的內容來源。 作者使用新的通用編輯器在AEM中管理其網站，並搭配上下文中的wysiwyg撰寫功能。 如此一來，企業便能利用Edge Delivery Services快速建立高效能網頁，同時利用AEM強大的內容管理功能。

![AEM 製作](/help/edge/assets/universal_editor_edge_delivery_services.png)

如需詳細資訊，請參閱 [檔案](/help/edge/overview.md) 並觀看 [AEM Gems - AEM製作和Edge Delivery Services快速入門](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694#M43905)

**Headless實作的通用編輯器**

Universal Editor也讓分離的Web應用程式能夠運用傳統網站獨有的相同直覺式內容內WYSIWYG製作。 內容建立者現在可以使用內容片段，以與頁面內元件相同的簡易方式，以視覺化方式撰寫版面。

Universal Editor與眾不同之處在於它可適應不同的Web架構、同時容納伺服器端和使用者端轉譯、保持框架無關性，並消除了託管AEM的必要性。 將現有Web應用程式與通用編輯器整合以進行內容編輯相當簡單明瞭，這主要需要開發人員將特定資料屬性整合到其標籤中。

透過上述功能，Universal Editor可確保提供一致的編輯體驗，無論內容結構或基礎技術棧疊為何。 如需詳細資訊，請參閱 [通用編輯器簡介](/help/implementing/universal-editor/introduction.md).

**內容片段和模型的內容管理OpenAPI**

開發人員現在能以程式設計方式與內容片段和內容片段模型互動，並使用Content Management OpenAPI對其執行CruD操作。 如需詳細資訊，請參閱 [API檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)

**體驗片段的多網站管理支援**

已針對儲存體驗片段的資料夾結構擴充多網站管理支援，讓使用者推出包含體驗片段的完整內容結構。

**比較內容片段版本**

新的內容片段編輯器現在可讓內容作者比較及檢視內容片段的目前版本與先前版本之間的差異。

### 早期採用者計劃 {#sites-early-adopter}

**產生變數**

透過AEM新功能利用GenAI， [產生變數](/help/generative-ai/generate-variations.md)，現在可在Cloud Service中存取。 產生變體可協助您透過使用產生式AI來產生和擴展內容建立。 請洽詢您的Adobe客戶團隊，以考慮加入方案。

**在內容片段控制檯中瀏覽資產**

內容作者現在可以瀏覽、檢視影像，以及對其他「資產」採取動作，而不需要離開內容片段主控台。

![資產瀏覽](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

有興趣嘗試該功能並分享回饋意見嗎？使用您的正式電子郵件ID傳送電子郵件至aemcs-headless-adopter@adobe.com ，以進一步瞭解早期採用者計畫。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理員檢視中的新功能 {#admin-view}

**與 Adobe Express 原生整合**

AEM Assets與Adobe Express原生整合，可讓您從Adobe Express使用者介面直接存取AEM Assets中儲存的資產。 您可以將AEM Assets中管理的內容放在快速畫布中，然後將新內容或編輯過的內容儲存在AEM Assets存放庫中。

![包括資產附加元件中的資產](/help/assets/assets/adobe-express-native-integration.png)

**預覽所有支援影片類型的轉譯版**

Experience Manager Assets現在依預設會產生所有支援視訊型別的預覽轉譯，不需要處理設定檔設定。

### 資產檢視中的新功能 {#assets-view}

**管理集合的許可權**

Assets Essentials可讓管理員管理存放庫中私有集合的存取層級。 身為管理員，您可建立使用者群組並指派權限給這些群組，以管理存取層級。您也可以將許可權管理許可權委派給使用者群組。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms的新功能 {#forms-new-features}

* **[Adobe Experience Manager FormsEdge Delivery Services](/help/edge/docs/forms/overview.md)**：AEM Forms Edge Delivery Services是一組可撰寫的服務，可啟用快速的開發環境，讓作者可以快速更新、發佈和啟動新表單。 這些服務提供卓越且高影響力的表單體驗，進而促進使用者的參與度和轉換率。這些表單體驗易於製作和開發。

  ![EDS Forms功能](/help/edge/assets/eds-forms-features.png)

這些服務可讓您：

* 在相同的表單網站上使用多個內容來源，並使用您偏好的撰寫工具，例如Microsoft Excel、Google Sheets或Adaptive Forms Editor。
* 提供數位註冊體驗，透過真實使用者監控(RUM)快速且持續地載入及轉譯您的表單效能。
* 使用純HTML、新式CSS和vanilla JavaScript建立卓越的體驗，避免特定架構的陡峭學習曲線。


### AEM Forms搶鮮版中的新功能 {#forms-pre-release}

* **核心元件型最適化Forms的增強視覺規則編輯器**：此版本大幅升級基於核心元件之適用性表單的視覺規則編輯器。 此版本大幅升級基於核心元件之適用性表單的視覺規則編輯器。 本次更新著重於簡化與自訂函式的互動，讓您能夠建立更強大且有效的表單。

  您現在可以透過以下方式簡化自訂功能互動：

   * 運用新註解以提供更清楚的函式定義。
   * 針對自訂函式使用快取機制，以提高表單效能。
   * 可順暢地使用自訂函式中的全域物件。
   * 在自訂函式中定義及使用選用引數。

  此更新也會對規則編輯器功能帶來下列增強功能。 您可以：

   * 針對條件式執行實作強大的「when-then-else」邏輯。
   * 利用現代JavaScript功能，例如左鍵和箭頭函式（ES10支援）。
   * 不僅驗證或重設欄位，而且驗證或重設整個面板和表單，擴大對使用者互動的控制。

  這些改進在視覺規則編輯器中提供更直覺且功能強大的撰寫規則和自訂函式體驗。

* **建立最適化表單的多個版本**：您現在可以輕鬆管理現有表單的變體。 這可簡化版本控制，並協助進行表單最佳化的比較，全都透過單一、簡化的工作流程完成。

* **比較最適化表單**：您現在可以輕鬆比較兩個表單，以識別兩個表單之間的差異。 它可讓團隊成員有效率地比較修訂版本和討論變更，以利順暢的協同合作。

* **手寫簽名元件的協助工具增強功能**：此更新大幅改善塗鴉簽名元件的協助工具：

  **改良的鍵盤導覽：**
   * 按下Tab鍵可讓使用者瀏覽簽名對話方塊中的所有互動式元素。
   * 使用筆刷或鍵盤簽署並按Enter鍵會關閉對話方塊。
   * 簽署並按一下[確定]後，焦點仍會留在簽章控制項上。

  **清除簽章功能：**

   * 可透過Tab鍵存取清除簽名的清除十字圖示。
   * 您也可以透過索引標籤導覽存取「清除簽名確認」對話方塊。

  **增強的標籤和控制項：**
   * 鍵盤簽名按鈕的標籤現在更清楚，使用「aria-label」來宣告功能（例如「aria-label=&#39;Sign using Keyboard&#39;」）。
   * 改善的對比可確保手寫簽名中的所有控制項都能輕鬆區分。
   * 現在，「確定/核取記號」按鈕會以視覺化方式指出它何時處於非使用中狀態。

  **熒幕Reader的簽名意見反應：**
   * 輸入簽名時，熒幕助讀程式的使用者可以聽到用來建立簽名的文字。

此更新透過改善塗鴉簽名元件的導覽、清晰度和意見回饋，確保殘障使用者獲得更包容的體驗。

### 早期採用者計劃 {#forms-early-adopter}

* **[提交最適化表單至Adobe Workfront Fusion案例](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Formsas a Cloud Service提供立即可用的選項，讓您輕鬆將最適化表單與Adobe Workfront連線。 這簡化了將最適化表單提交到 Adobe Workfront 情境的程序，讓您在提交最適化表單時觸發 Workfront Fusion 情境。

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> 使用Adobe Workfront Fusion Connector，您可以設計在提交最適化表單時自動觸發的工作流程。 例如，設想一個情境，其中初始工作流程以指派給特定個人審查提交的資料，從而允許根據透過最適化表單擷取的資訊核准或拒絕應用程式。 這項簡化的整合可提升效率，並將工作流程自動化提升到新的水準。|

* **Reader延伸服務**： AEM Forms Communication API已推出Reader擴充功能，可讓您新增表單填寫和註解等功能至一般PDF，讓使用者能透過免費Adobe Reader互動。

* [從右至左語言支援](/help/forms/supporting-new-language-localization-core-components.md)：以核心元件為主的最適化表單現在可以呈現從右至左 (RTL) 語言 (如阿拉伯文、波斯文和烏都文)。全球有超過 20 億人使用 RTL 語言。使用 RTL 語言的表單可讓您擴展最適化表單的範圍，以滿足這些不同的受眾並選擇進入 RTL 市場。在某些地區，法律也強制要求以當地語言提供表單。透過適應當地語言，您不僅可以向更廣泛的受眾敞開大門，還可以確保遵守相關法律和法規。

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-ea@adobe.com`，加入早期採用者計畫並要求存取該功能。

* **[您可以利用真實使用者監控 (RUM) 資料服務](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**&#x200B;啟用 AEM as a Cloud Service 的用戶端系列。真實使用者監控 (RUM) 資料服務可以更準確地反映使用者互動，確保可靠地測量網站參與度。這是深入了解頁面效能的絕佳機會。這對於使用 Adobe 管理 CDN 或非 Adobe 管理 CDN 的客戶很有幫助。此外，對於使用非 Adobe 管理 CDN 的客戶，現在可以啟用自動流量報告，而無需與 Adobe 共享任何流量報告。

  如果您有興趣測試此新功能並分享意見回饋，請使用與您的 Adobe ID 相關聯的電子郵件地址，傳送電子郵件至 `aemcs-rum-adopter@adobe.com`，並在郵件中附上要啟用 RUM 的每個環境網域名稱。Adobe 的產品團隊隨後會為您啟用真實使用者監控 (RUM) 資料服務。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### 早期採用者計畫 {#foundation-early-adopter}

#### 流量篩選器規則警報（早期採用者計畫） {#traffic-filter-rules-alerts-early-adopter}

最近發行的 [流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)，其中包含可選擇性授權的Web應用程式防火牆(WAF)規則，可讓您設定允許或拒絕的流量。

現在您可以傳送電子郵件至 **<aemcs-cdn-config-adopter@adobe.com>** 以加入率先採用者計畫，這樣就能在流量篩選規則觸發時收到警報。 動作中心電子郵件通知會在發生某些流量狀況時隨時通知您，以便您採取適當的措施。

#### CDN設定（早期採用者計畫） {#cdn-config-early-adopter}

除了最近發行的 [流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)，其中包含可選擇性授權的Web應用程式防火牆(WAF)規則，您可利用設定管道來宣告及部署其他型別的CDN設定。 [瞭解更多](/help/implementing/dispatcher/cdn-configuring-traffic.md) 並透過電子郵件加入率先採用者計畫 **<aemcs-cdn-config-adopter@adobe.com>** 若要存取以下專案：

* 301/302 用戶端重新導向
* 在邊緣將請求代理到任意來源(例如非AEM應用程式)
* URL 轉換
* 設定或修改要求或回應標頭
* CDN 無法連接 AEM 時的自訂錯誤頁面

#### Apache/Dispatcher執行階段擷取重寫對應（早期採用者程式） {#apache-rewritemaps-early-adopter}

與AEM 6.5類似，Apache/Dispatcher將擷取重新寫入放置在發佈存放庫中的特定位置的對應，並載入這些對應，無需Web層管道執行。 這開啟了商業使用者使用UI宣告重新導向的機會，例如ACS Commons重新導向地圖管理員提供的UI。 請聯絡 **<aemcs-cdn-config-adopter@adobe.com>** 以取得詳細資訊。

#### 用於載入動態內容的Edge Side Include (ESI) （早期採用者計畫） {#esi-early-adopter}

Adobe Managed CDN現在支援Edge Side Include (ESI)，這是邊緣層級動態網頁內容組合的標籤語言。 加入ESI程式碼片段，您就能快取CDN的整體HTML頁面，其中包含較高TTL，同時更頻繁地從來源擷取需要較高步調更新（較低TTL）的較小區段。 請聯絡 **<aemcs-cdn-config-adopter@adobe.com>** 以取得詳細資訊。

#### RDE支援使用網站主題和網站範本的前端計畫碼（早期採用計畫） {#rde-frontend-early-adopter}

[快速開發環境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 現在支援以[網站主題](/help/sites-cloud/administering/site-creation/site-themes.md)和[網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)為主的前端程式碼 (適用於早期採用者)。對於 RDE，這是使用命令列指令完成，而不是使用 [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)來完成。請聯絡 **<aemcs-rde-support@adobe.com>** 進行試用並提供意見反應。

#### 增強RDE的記錄功能（早期採用者計畫） {#rde-logging-early-adopter}

在中偵錯程式碼時 [快速開發環境(RDE)](/help/implementing/developing/introduction/rapid-development-environments.md)，開發人員現在可以使用命令列，且無需修改版本控制中的OSGI屬性，更有效率地設定和串流記錄檔。 功能包括：

* 在每個套件或類別層級上宣告記錄層級
* 自訂日誌輸出格式
* 並行串流多個記錄檔

請聯絡 **<aemcs-rde-support@adobe.com>** 進行試用並提供意見反應。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

