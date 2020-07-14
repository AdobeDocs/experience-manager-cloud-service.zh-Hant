---
title: Adobe Experience Manager 雲端服務 2020.6.0 版發行說明
description: Experience Manager 2020.6.0 版發行說明
translation-type: ht
source-git-commit: fcae90c8e24dbd2994e8700daf22f5dff039b299
workflow-type: ht
source-wordcount: '1942'
ht-degree: 100%

---


# AEM 雲端服務 2020.6.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.6.0 版的一般發行說明。

## 發行日期 {#release-date}

[!DNL Experience Manager] 雲端服務 2020.6.0 版的發行日期為 2020 年 6 月 4 日。

## AEM Sites 新增功能 {#aem-sites}

請詳閱本節，了解 AEM 雲端服務 2020.6.0 版中 AEM Sites 的新增功能和更新。

### 新功能 {#whats-new-2020.6.0}

[核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 2.9.0 版現已隨附於 AEM Sites，其中包含：

* [Adobe 用戶端資料層](https://github.com/adobe/adobe-client-data-layer)與核心元件的整合
* 所有元件可設定的 HTML ID 屬性
* 新的進度列元件
* 多項錯誤修正

### 錯誤修正 {#sites-bug-fixes}

* 當「配置」容器複製並轉貼到某個頁面時，配置容器內的元件不會顯示。

* 已修正配置元件大小調整的問題。

* 已新增僅限 Angular 頁面和 AEM/Angular 頁面的路由管理功能。

### 協助工具 {#accessibility}

* 現在，使用向下箭頭在瀏覽模式中導覽時，可以針對&#x200B;**建立頁面**&#x200B;對話方塊中的「石造」項目提供角色和狀態旁白。

* 已在導覽中新增連結，讓使用者可跳至主要內容。

* 螢幕助讀程式的改良。

## AEM 雲端服務基礎的新增功能 {#foundations}

AEM 專案的 pom.xml 中所有的參照移至遠端存放庫 `https://downloads.experiencecloud.adobe.com/content/maven/public` 之後，AEM 專案建置時間將有所改善。

先前託管於該位置的 AEM 雲端服務 SDK API Jar，現在位於 Maven 的預設成品存放庫 Maven Central 上。

## Cloud Manager 新增功能 {#cloud-manager}

請詳閱本節，了解 AEM 雲端服務 2020.6.0 版中 Cloud Manager 的新增功能和更新。

### 新功能 {#what-is-new-cloud-manager}

* 在 Cloud Manager 中，屬於&#x200B;*業務擁有者*&#x200B;角色的使用者現在可以從登陸頁面 (透過「方案」卡片上的快速動作按鈕) 或從方案中刪除沙箱方案。

   如需詳細資訊，請參閱[刪除沙箱方案](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html)。

* 在 Cloud Manager 中，屬於&#x200B;*業務擁有者*&#x200B;或&#x200B;*部署管理員*&#x200B;角色的沙箱方案使用者現在可以刪除透過 Cloud Manager UI 設定的生產和預備環境。現在，您可以從&#x200B;**方案概覽**&#x200B;頁面和&#x200B;**環境**&#x200B;頁面上的「環境」卡片中使用刪除選項。在「生產」或「預備」上選取刪除選項，也可刪除集合中的其他項目。

   如需詳細資訊，請參閱[刪除沙箱方案](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html)。

* 登陸頁面上的「指導」標記可為使用者提供關於基本導覽的通知和指示。

* **方案概覽**&#x200B;頁面上的「指導」標記，可為使用者提供與 Cloud Manager 中的基本導覽有關的通知和指示，方便他們開始使用。

* 現在，Cloud Manager 中提供&#x200B;**學習**&#x200B;頁面，可透過上層導覽存取。此頁面提供相關資源，可協助使用者了解與他們在 Cloud Manager 中指派的角色有關的常用工作流程。

* 「沙箱方案」現在可透過&#x200B;**沙箱**&#x200B;徽章來識別，此徽章會顯示在登陸頁面的方案卡片上，以及&#x200B;**方案概覽**&#x200B;頁面中的方案名稱旁。

* 現在，SysAdmin 角色中的使用者可以從可管理 Cloud Manager 使用者角色或權限的位置，單鍵存取 Admin Console 中的位置。在登陸頁面上，**新增方案**&#x200B;按鈕旁現在有&#x200B;**管理存取**&#x200B;按鈕可供使用。

   如需詳細資訊，請參閱 [SysAdmin 任務](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks)。

* SysAdmin 角色中的使用者現在可以直接從 Cloud Manager 單鍵存取製作例項。

   如需詳細資訊，請參閱[管理對製作例項的存取](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem)。

* 「建置」記錄現在包含探索到的成品清單，包括略過的內容封裝。

* 「建置」步驟現在會驗證所有產生的內容封裝皆包含所有必要屬性 - 名稱、群組和版本。

* 「建置」步驟現在會驗證組建是否至少產生了一個內容封裝。

### 錯誤修正 {#bug-fixes-cm}

* 在某些情況下，**建立方案**&#x200B;對話方塊中的圖示不會對齊。

* AEM 版本識別碼不一定會顯示在&#x200B;**方案概覽**&#x200B;頁面上。

* 在設定生產管道時，某些客戶看不到&#x200B;**排定的部署**&#x200B;選項。

### 已知問題 {#known-issues-cm}

* 在特定期間內未偵測到任何活動時，沙箱方案中的環境將會休眠。在 Cloud Manager 中不會觀察到此狀態。不過，您可透過開發人員控制台來觀察此狀態。此問題將在即將發行的版本中解決。

* 直接從 Cloud Manager 連結至開發人員控制台時，不會顯示將沙箱方案的環境解除休眠/休眠的選項。若要解決此問題，請於開發人員控制台中，在 URL 的結尾處加上 `#release-cm-p1234-e5678` 模式，其中，*1234* 是方案 ID，*5678* 是環境 ID。此問題將在即將發行的版本中解決。

## [!DNL Adobe Experience Manager Assets] 新增功能 {#aem-assets}

**增強型智慧標記的引導式使用者體驗 (由 Adobe Sensei 提供技術支援)**

增強型智慧標記可讓組織訓練智慧標記模型，以在一般智慧標記以外，還能根據客戶特定的商業標記來識別影像。

此版本提供了新的引導式使用者體驗，有助於針對客戶特定的標記集設定智慧標記訓練，並使用資產加以訓練，以便在日後以標記來辨識和標示這些資產。現在的體驗更符合直覺。訓練增強型智慧標記，讓智慧標記的訓練更符合直覺。請參閱[如何將智慧標記新增至資產](/help/assets/smart-tags.md)和[設定智慧標記](/help/assets/smart-tags-configuration.md)。

**擷取、預覽和傳遞 3D 內容的支援**

現在，組織可以在 AEM Assets 中儲存和使用 3D 檔案。使用者可上傳、預覽和使用多種核心 3D 檔案，包括 OBJ、STL、GLTF 和 GLB 檔案。除了 [!DNL Dynamic Media] 以外，您也可以使用在多種環境中可用的 URL 或檢視器來設定及傳遞 3D 體驗。其中包括 [!DNL Dynamic Media] 3D Experience Viewer、Sites 3D Viewer 元件，以及透過 [!DNL Dynamic Media] (AR/VR) 傳遞 3D 檔案的功能。請參閱[在 Dynamic Media 中使用 3D 資產](/help/assets/dynamic-media/assets-3d.md)。

**Adobe XD 的 Adobe Asset Link 支援**

在最新版本中，[!DNL Experience Manager Assets] 支援隨 [!DNL Adobe Asset Link] v29.3 一起發行的 [!DNL Adobe XD] 新外掛程式。此整合可讓設計人員直接在其設計中存取和使用 [!DNL Experience Manager] 中的資產，而無須退出 [!DNL Adobe XD] 應用程式。請參閱 [Adobe XD 的 Adobe Asset Link 文件](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link-for-xd.html)。

在此版本中，創意使用者和設計人員現在可以在多種 Creative Cloud 桌面應用程式 (包括 [!DNL Adobe XD]、[!DNL Photoshop]、[!DNL Illustrator] 和 [!DNL InDesign]) 中，透過 [!DNL Adobe Asset Link] 使用在 [!DNL AEM Assets] 中受到管理的資產。

**協助工具增強功能**

現在，[!DNL Adobe Experience Manager Assets] 在符合網頁內容協助工具準則 (WCAG) v2.1 的情況下，比以往更容易存取。協助工具在下列使用案例或介面中的功能已有所改善：

使用者介面元素在螢幕助讀程式中更為適用，而且可使用鍵盤存取，對比也優於以往。以下是增強功能的詳細清單：

* 螢幕助讀程式不會將[!UICONTROL 管理發佈]頁面上的[!UICONTROL 選項]、[!UICONTROL 範圍]和[!UICONTROL 工作流程]進度列朗讀為進度列。對於螢幕助讀程式的使用者，這些狀態指標會讀為索引標籤清單。(CQ-4273015)

* 在資產的[!UICONTROL 屬性]頁面中新增標記時，使用者會導覽標記的樹狀結構。螢幕助讀程式的使用者在導覽時不會聽到任何提示，因此無法存取樹狀結構。(CQ-4272964)

* 在連結共用對話方塊中，以瀏覽模式導覽時，螢幕助讀程式會：

   * 在對話方塊載入時立即提供表格資訊的旁白。
   * 無法導覽至列出的所有自動建議。
   * 不會提供旁白來敘述針對[!UICONTROL 新增電子郵件地址/搜尋]下拉式方塊顯示的自動建議。(CQ-4294232)

* [!UICONTROL 中繼資料結構編輯器]頁面及其元素現在可使用鍵盤來存取，且在螢幕助讀程式中很容易操作。(CQ-4272953) 使用者可在 NVDA 瀏覽模式中使用鍵盤來拖曳元件。(CQ-4296326)

* 在「資產」使用者介面上，無法使用鍵盤存取視圖設定。(CQ-4289038)

* 黃色評等圖示的明度比小於 3:1。對於視力不良和無法分辨顏色的使用者而言，此功能並不實用。評等星級會顯示在資產的索引標籤中或卡片視圖中

* 某些使用者介面元素的顏色和對比已更新，以便視力不良和無法分辨顏色的使用者區分這些使用者介面元素。例如，在資產的[!UICONTROL 屬性]中，[!UICONTROL 進階]索引標籤的[!UICONTROL 評等]區段中的評等星級圖示色彩已變更，以提供適當的對比，而卡片視圖中的圖示也是如此。(CQ-4295106)

* 螢幕助讀程式現在可以將下拉式方塊的清單方塊快顯功能表 (位於不同頁面的不同欄位中) 的項目朗讀為選項清單。(CQ-4294017)

* 若要將工作流程套用至資產，可以使用鍵盤存取[!UICONTROL 時間軸]中的＞形箭頭。(CQ-4289268)

* 使用者可以使用 `x` 符號，在資產[!UICONTROL 屬性]頁面的[!UICONTROL 基本]索引標籤中，將[!UICONTROL 標記]欄位中已取的標記移除。螢幕助讀程式現在會朗讀所選標記的用途和數目 (CQ-4273033)。

* 使用者可使用鍵盤將焦點置於唯讀表單欄位上。例如，在資產的[!UICONTROL 屬性]頁面上，將焦點置於[!UICONTROL 基本]索引標籤中已停用的欄位上。(CQ-4273031)

* 現在，可以使用鍵盤存取在左邊側欄中篩選資產的選項。(CQ-4273018)

* 螢幕助讀程式會朗讀各種下拉式方塊元素的用途，例如「路徑」欄位，以及在資產[!UICONTROL 屬性]頁面的[!UICONTROL 基本]索引標籤中開啟「選取」對話方塊的選項。(CQ-4273016)

* 影片的音量控制可使用鍵盤存取。(CQ-4272696)

* 使用鍵盤時，Assets 使用者介面上許多可操作的選項並不會指出焦點。(CQ-4272694)

* 現在，螢幕助讀程式的使用者可得知何時可使用鍵盤選取清單視圖中的列。當指標置於列上方時，會朗讀資訊。(CQ-4271824)

* 有些表單欄位 (例如登入頁面上的使用者名稱和密碼欄位) 會藉由預留位置值來提供可存取的標籤。(CQ-4271716)

* 現在，互動式使用者介面元素 (例如連結) 和選項 (例如資產頁面或資料夾導覽的頁首和縮放選項)，均可使用鍵盤來存取。(CQ-4271412)

* [!DNL Adobe Experience Manager] Assets 上所有已瀏覽頁面的標題現在都是唯一的。(CQ-4271409)

**其他增強功能**

此版本提供下列其他增強功能：

* 能夠使用資產處理設定檔重新處理資產，讓使用者完全掌控處理程序 (執行完整的資產處理、僅套用特定處理設定檔，以及決定是否應執行後續處理工作流程)。
* 現在，當基礎叢集例項在幕後重新啟動時，搜尋查詢傳回結果的速度會比以往快 (過去在這類情況下，初始搜尋執行的所需時間可能會更久)。
* 在 Assets 介面和搜尋結果中檢視清單視圖中的資產時，依「名稱」排序。請參閱[搜尋資產](/help/assets/search-assets.md#sort)。
* 在 Assets 介面和搜尋結果中檢視清單視圖中的資產時，依「建立日期」排序。請參閱[搜尋資產](/help/assets/search-assets.md#sort)。
* 支援使用資產微服務將 EPS 檔案轉換為影像。

### 錯誤修正 {#assets-bug-fixes}

<!-- TBD: Add enhancements above and bug fixes below.
Seek DM bug fixes if any.
Add Nui update as shared on Slack: https://git.corp.adobe.com/nui/app/releases/tag/22
-->

除了上述新功能以外，目前的版本還根據 [!DNL Assets] 客戶的意見回應提供下列錯誤修正。

* 對於 MP3 音樂檔案，DAM 預覽中的縮圖所顯示的播放按鈕無法運作。(CQ-4294731)
* 將指標置於卡片視圖上方，卡片中可用的快速動作就會自動取得焦點，而使畫面可以捲動。(GRANITE-26895)
* 在捲動許多搜尋結果後若顯示太多影像，會導致瀏覽器當機。(GRANITE-26432)
* 在下載資產時，如果選取了電子郵件選項，即使已提供有效的電子郵件 ID，下載選項仍無法使用。(CQ-4296535)
* 儲存為智慧型集合的自訂篩選器無法正確套用至資產。(CQ-4294942)
* 有多項搜尋和索引增強功能以及錯誤修正可改善效能。(CQ-4286373)
