---
title: Adobe Experience Manager 雲端服務 2020.6.0 版發行說明
description: Experience Manager 2020.6.0 版發行說明
translation-type: tm+mt
source-git-commit: c5ee964fad3e1430e7c08f0cca76aecfae8bd44f
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 6%

---


# AEM 雲端服務 2020.6.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.6.0 版的一般發行說明。

## 發行日期 {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.6.0 is June 04, 2020.

## AEM Sites 新增功能 {#aem-sites}

請詳閱本節，了解 AEM 雲端服務 2020.6.0 版中 AEM Sites 的新增功能和更新。

### 新功能 {#whats-new-2020.6.0}

核心元件2.9.0版現 [已隨附於AEM Sites](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) ，包括：

* [Adobe用戶端資料層](https://github.com/adobe/adobe-client-data-layer) 與核心元件的整合
* 所有元件的可設定HTML ID屬性
* 新的進度列元件
* 許多錯誤修正

### 錯誤修正 {#sites-bug-fixes}

* 當「版面」容器被複製並再貼至頁面上時，版面容器內的元件不可見。

* 修正版面元件大小調整的問題。

* 已新增管理僅限Angular的路由頁面和AEM/Angular頁面的功能。

### 協助工具 {#accessibility}

* 現在，使用向下箭頭在瀏覽模式中導覽時，「建立頁面」對話方塊中的「砌體」項目可能會具有旁白角色和狀態。 ****

* 在導覽中新增連結，讓使用者可跳至主要內容。

* 螢幕閱讀程式改良功能。


## AEM As a Cloud Service的基礎新功能 {#foundations}

AEM專案建立時間會因為將AEM專案的pom.xml中的所有參照移除至遠端儲存庫而有所改善 `https://downloads.experiencecloud.adobe.com/content/maven/public`。

AEM a Cloud Service SDK API Jar（先前代管於該位置）現在位於Maven Central（Maven的預設工件儲存庫）。

## Cloud Manager 新增功能 {#cloud-manager}

請詳閱本節，了解 AEM 雲端服務 2020.6.0 版中 Cloud Manager 的新增功能和更新。

### 新功能 {#what-is-new-cloud-manager}

* Cloud Manager中「業務擁有者 ** 」角色的使用者現在可以從登陸頁面（透過方案卡上的快速動作按鈕）或從程式中刪除沙盒程式。

   如需詳細 [資訊，請參閱刪除沙盒程式](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) 。

* Cloud Manager中「業務擁 *有者* 」或「部署管理員 ** 」角色的「沙箱程式」使用者現在可以刪除透過Cloud Manager UI設定的「生產」和「階段」環境。 刪除選項現在可從「程式概述」頁面和「環 **境** 」頁面上的「環境」卡 **中使用** 。 在「生產」或「舞台」上選取刪除選項，也會刪除集合中的其他選項。

   如需詳細 [資訊，請參閱刪除沙盒程式](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) 。

* 引導著陸頁面上的標籤，以通知並指示使用者基本導覽。

* 指導「方案概 **述」頁面上的標籤** ，以通知並指示使用者在Cloud Manager中進行基本導覽，以開始使用。

* 現在 **Cloud Manager中提供** LEARN頁面，可透過頂端導覽存取。 本頁提供相關資源，可協助使用者瞭解最常使用的工作流程，這些工作流程與他們在Cloud Manager中指派的角色相關。

* 「沙盒程式」現在可透過「 **Sandbox** 」標章來識別，此標章會顯示在著陸頁面上的程式卡上，以及「程式概述」頁面中的程式名稱旁 **** 邊。

* SysAdmin角色中的用戶現在可以單鍵訪問Admin Console中的位置，從中可以管理用戶角色或Cloud Manager權限。 「 **Add Program** 」（新增程式）按鈕旁的著陸頁面現在提供 **「Manage Access** 」（管理存取）按鈕。

   有關詳細 [資訊，請參閱](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) 「系統管理任務」。

* SysAdmin角色中的用戶現在可以通過單鍵訪問直接從Cloud Manager建立實例。

   如需詳細 [資訊，請參閱「管理作者例項的存取](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) 」。

* 「構建日誌」現在包含已發現對象的清單，包括跳過的內容包。

* 「建立」步驟現在會驗證所有產生的內容封裝是否包含所有必要屬性——名稱、群組和版本。

* 「建置」步驟現在可驗證建置是否至少產生了一個內容套件。

### 錯誤修正 {#bug-fixes-cm}

* 在某些情況下，「建立程式」( **Create Program** )對話框中的表徵圖未對齊。

* AEM發行識別碼未一致顯示在「 **Programs Overview** 」（程式綜覽）頁面上。

* 在設定生產管線時，某些客 **戶看不到「排程部署** 」選項。

### 已知問題 {#known-issues-cm}

* 在特定期間內未偵測到任何活動時，沙盒程式中的環境將會休眠。 Cloud Manager中不會觀察到此狀態。 不過，您可透過Developer Console觀察狀態。 這個問題將在即將發行的版本中解決。

* 直接從Cloud Manager連結至Developer Console時，不會顯示沙盒程式環境的解除休眠／休眠選項。 若要解決此問題，請在Developer Console中加入一 `#release-cm-p1234-e5678` 次模式至URL結尾， *1234* 是Program ID, *5678* 是Environment ID。 這個問題將在即將發行的版本中解決。

## What&#39;s New in [!DNL Adobe Experience Manager Assets] {#aem-assets}

<!-- 
Assets RNs are being authored and are a work in progress.
PM/EM review required before publishing.
-->

**Adobe Sensei提供增強智慧型標籤的引導式使用者體驗**

增強的智慧型標籤可讓組織訓練智慧型標籤模型，以除一般智慧型標籤外，還能根據客戶特定的商業標籤識別影像。

在此版本中，提供全新的引導式使用者體驗，可協助針對客戶特定標籤集設定智慧標籤訓練，並訓練他們使用資產，這些資產應該在日後加以辨識和標籤。 這是更直覺的體驗。
訓練增強的智慧型標籤，以更直覺式的智慧型標籤訓練。 瞭解 [如何智慧標籤](/help/assets/smart-tags.md) , [以及設定智慧標籤](/help/assets/smart-tags-configuration.md)。

**支援擷取、預覽和傳送3D內容**

組織現在可以在AEM Assets中儲存和使用3D檔案。 使用者可以上傳、預覽和運用多種核心3D檔案，包括。obj、.stl、.gltf和。glb檔案。 此外，您還 [!DNL Dynamic Media]可以設定3D體驗，並透過不可知的URL或檢視器提供。 這包括 [!DNL Dynamic Media] 3D Experience Viewer、Sites 3D Viewer元件，以及透過(AR/VR)傳送3D [!DNL Dynamic Media] 檔案的功能。

<!-- TBD: Add link to the DM help article, if any. -->

<!-- Hiding this as the GA is at a later date. 
TBD: Add link to the AAL help article. 

**Adobe Asset Link support for Adobe XD**

With the latest release, [!DNL Experience Manager Assets] provides support for a new [!DNL Adobe Asset Link] plug-in that is released with [!DNL Adobe XD] v29. The integration allows designers to access and use assets from [!DNL Experience Manager] in their designs, without the need to leave [!DNL Adobe XD] application.

-->

**協助工具增強功能**

[!DNL Adobe Experience Manager Assets] 現在可依照網頁內容協助工具准則(WCAG)2.1版的准則，更方便存取。 下列使用案例或介面的協助功能已改善：

* 使用者介面元素、控制項、頁面和對話方塊都適合螢幕閱讀程式。
* 使用者介面元素、控制項和輸入表單欄位都可使用鍵盤存取。
* 變更某些介面元素的顏色或對比，讓視力有限且無色彩感知的使用者更容易辨識這些元素。 例如，「資產」現在在「屬性」頁面和卡片檢視中的星號分級圖示 [!UICONTROL 中] ，有適當的對比。

<!-- TBD: Add link to the a11y help article if created. Else add it post-GA. -->

**其他增強功能**

此版本提供下列其他增強功能：

* Assets使用者介面的協助工具改進。
* 能夠使用資產處理設定檔重新處理資產，讓使用者完全掌控流程（執行完整資產處理、只要套用特定處理設定檔，並決定是否應執行後置處理工作流程）。
* 現在，當底層群集實例在後台重新啟動時，搜索查詢返回結果的速度更快（在此類情況下，初始搜索運行可能會持續更久）。
* 在「資產」介面和搜尋結果中，在清單檢視中檢視資產時，依「名稱」排序。
* 在「資產」介面和搜尋結果的清單檢視中檢視資產時，依「已建立」（日期）排序。
* 支援將EPS檔案轉換為影像。

### 錯誤修正 {#assets-bug-fixes}

<!-- TBD: Add enhancements above and bug fixes below.
Seek DM bug fixes if any.
Add Nui update as shared on Slack: https://git.corp.adobe.com/nui/app/releases/tag/22
-->

除了上述新功能外，目前的版本還根據客戶的意見回應，提供下列增強功能和錯誤修正 [!DNL Assets]。

* 對於MP3音樂檔案，DAM預覽中縮圖上顯示的播放按鈕無法運作。 (CQ-4294731)
* 暫留指標在卡片檢視上，會使螢幕捲動（自動）集中在卡片中可用的快速動作。 (GRANITE-26895)
* 在捲動大量搜尋結果後顯示太多影像會導致瀏覽器當機。 (GRANITE-26432)
* 「管 [!UICONTROL 理出版物]」頁面上的「選項」、「範圍 [!UICONTROL 」和「工作流」] 進度指標不會被螢幕閱讀為進度指標。 螢幕閱讀程式的使用者會將這些狀態指示器視為標籤清單。 (CQ-4273015)
* 下載資產時，如果選取了電子郵件選項，而且即使已提供有效的電子郵件ID，也無法使用下載選項。 (CQ-4296535)

* 在資產的「屬 [!UICONTROL 性] 」頁面中新增標籤時，使用者會導覽標籤的樹狀結構。 樹狀結構無法存取，因為螢幕閱讀器使用者在導覽時不會聽到任何聲音。 (CQ-4272964)
* 在連結共用對話方塊中，在瀏覽模式中導覽時，螢幕閱讀程式

   * 在載入對話方塊後，立即對表格資訊加以描述。
   * 無法導覽至所有列出的自動建議。
   * 不會為「新增電子郵件地址／搜尋」組合方 [!UICONTROL 塊的顯示自動建議] ，做出旁白。 (CQ-4294232)

* 在元資料架構編輯器的NVDA瀏覽模式下，使用鍵盤時拖動選項無效。 (CQ-4296326)
* 在「資產」使用者介面上，檢視設定無法透過鍵盤存取。 (CQ-4289038)
* 儲存為智慧型系列的自訂篩選器無法正確套用至資產。 (CQ-4294942)
* 多項搜尋和索引增強功能和錯誤修正可改善效能。 (CQ-4286373)
* 對於黃色分級表徵圖，明度比小於3:1。 對於視力有限且對顏色沒有感知的使用者而言，此功能並不實用。 評等星號會顯示在資產 [!UICONTROL 屬性中] 「進階」標籤的「評等」區段中，或顯示在資產  「資訊卡檢視」中(CQ-4295106)
* 組合方塊的清單方塊下拉式清單（位於不同頁面上的各種欄位中）現在會將項目顯示為螢幕閱讀程式可宣佈的選項清單。 (CQ-4294017)
* 無法使用鍵盤來 [!UICONTROL 存取] 「時間軸」中的Chevron向上箭頭，以套用工作流程至資產。 (CQ-4289268)
* 現在，螢幕閱讀器可以 [!UICONTROL 訪問用於刪除Basic](屬性 [!UICONTROL )頁籤中] Basic [!UICONTROL （基本）頁籤中Tags（標籤）欄位下] 的每個選定標籤的選項（具有x）。 (CQ-4273033)
* 唯讀表單欄位(例如，資產屬性的「基本 [!UICONTROL 」索引標籤上停] 用的欄位 )現在可使用鍵盤。 (CQ-4273031)
* 開啟篩選邊欄的選項現在可使用鍵盤存取。 (CQ-4273018)
* 螢幕閱讀程式現在可正確宣佈各種組合方塊元素（例如「路徑」欄位和在資產屬性的「基本」索引標籤中開啟「選取範圍」對話方塊的選項）的用途。 (CQ-4273016)
* [!UICONTROL 中繼資料結構編輯器] (Metadata Schema Editor)頁面及其元素無法使用鍵盤存取，而且不適合螢幕閱讀程式。 (CQ-4272953)
* 無法使用鍵盤來存取視訊音量控制項。 (CQ-4272696)
* 使用鍵盤時，Assets使用者介面上許多可操作的選項並不表示焦點。 (CQ-4272694)
* 使用鍵盤時，螢幕閱讀程式的使用者不知道清單檢視中的列是可選取的。 只有當滑鼠停留在列上時，才會公佈資訊。 (CQ-4271824)
* 有些表單欄位（例如登入頁面上的使用者名稱和密碼欄位）僅依賴預留位置值來提供可存取的標籤。 (CQ-4271716)
* 互動式使用者介面元素，例如連結和選項（在資產頁面的標題和縮放選項，資料夾導覽）現在可使用鍵盤來存取。 (CQ-4271412)
* 「資產」上所有已瀏覽頁面的 [!DNL Adobe Experience Manager] 標題現在都是唯一的。 (CQ-4271409)
