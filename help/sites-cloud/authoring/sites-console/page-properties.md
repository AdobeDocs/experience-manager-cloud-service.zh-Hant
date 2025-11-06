---
title: 頁面屬性
description: 瞭解頁面可以擁有的不同屬性，以及這些屬性如何控制頁面行為以及如何管理頁面。
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
solution: Experience Manager Sites
feature: Authoring
role: User
mini-toc-levels: 2
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 2%

---


# 頁面屬性 {#page-properties}

瞭解頁面可以擁有的不同屬性，以及這些屬性如何控制頁面行為以及如何管理頁面。

>[!TIP]
>
>如需有關如何編輯和變更頁面屬性的詳細資訊，請參閱檔案[編輯頁面屬性。](/help/sites-cloud/authoring/sites-console/edit-page-properties.md)

## 概述和屬性可用性 {#overview}

頁面屬性可控制頁面的許多方面，從頁面的標題和品牌推廣到其許可權。 屬性分佈於數個索引標籤中，有些索引標籤會根據頁面型別而隱藏。 與AEM中的大部分屬性一樣，[頁面屬性也可以繼承。](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#inheritance)

>[!NOTE]
>
>本檔案說明所有可能的頁面屬性。 根據頁面型別，並非所有屬性都可用。

## 基本索引標籤 {#basic}

### 標題和標籤 {#title-tags}

* **Title** — 定義用於SEO目的的頁面中繼標題，以及頁面內容中顯示的標題（除非被覆寫）

   * 頁面的標題會顯示在AEM UI中的各種位置，包括&#x200B;**網站主控台**&#x200B;網站[卡片/清單檢視。](/help/sites-cloud/authoring/sites-console/introduction.md)
   * 這是必要欄位。

* **標籤** — 定義用於SEO的頁面中繼標籤

   * 您可以更新選取方塊中的清單，在頁面中新增或移除標籤。
   * 使用下拉式清單從現有標籤中選取。
   * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
   * 在空白選取方塊中輸入名稱，即可輸入全新的標籤。

      * 當您按下Enter鍵時，就會建立新標籤。
      * 然後，新標籤將顯示為右側的小型星號，表示它是新標籤。

   * 當您將滑鼠移到選取方塊中的標籤專案上時，會出現x，可用來為此頁面移除該標籤。
   * 如需關於標籤的詳細資訊，請參閱[使用標籤。](/help/sites-cloud/authoring/sites-console/tags.md)

* **在導覽中隱藏** — 指示在產生的網站頁面導覽中是顯示還是隱藏頁面

### 品牌元素 {#branding}

藉由將品牌概要附加至每個頁面標題，跨頁面套用一致的品牌識別。 此功能需要使用2.14.0版或更新版本的[核心元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)的頁面元件

* **品牌概要**

   * **覆寫** — 檢查以在此頁面上定義品牌概要。

      * 此值由任何子頁面繼承，除非它們也設定了&#x200B;**覆寫**&#x200B;值。

   * **覆寫值** — 要附加至頁面標題的品牌概要文字。

      * 值會附加至頁面標題後的垂直號字元，例如`Cycling Tuscany | Always ready for the WKND`

### HTML ID {#html-id}

* **ID** — 要套用至元件的HTML ID。

### 更多標題和說明 {#more-titles}

* **頁面標題** — 要在頁面上使用的標題

   * 這通常由標題元件使用。
   * 如果空白，則使用&#x200B;**標題**。

* **導覽標題** — 您可以指定單獨的標題以用於導覽（例如，如果您想要更簡潔的標題）。

   * 如果空白，則使用&#x200B;**頁面標題**。

* **子標題** — 頁面上使用的子標題
* **描述** — 頁面的描述、用途或您要新增的任何其他詳細資訊

### 開啟/關閉時間 {#on-off-time}

頁面的開啟/關閉時間是一種暫時隱藏已發佈內容的便利方式。 內容在關閉時仍會留在發佈執行個體上。 關閉頁面不會取消發佈內容。

* **開啟時間** — 已發佈頁面在發佈環境中可見（轉譯）的日期和時間。 頁面必須以手動方式或預先設定的自動復寫方式發佈。

   * 如果已經[發佈，](/help/sites-cloud/authoring/sites-console/publishing-pages.md)此頁面可在發佈執行個體上使用，但會保持隱匿（隱藏）狀態，直到在指定時間才呈現。
   * 如果未發佈且[已設定為自動復寫，](/help/operations/replication.md#on-and-off-times-trigger-configuratio)則會自動發佈頁面，然後在指定的時間轉譯。
   * 如果未發佈且未設定為自動復寫，則不會自動發佈頁面，因此嘗試存取該頁面時會顯示404。

* **關閉時間** — 類似於&#x200B;**開啟時間**，且經常與其搭配使用，這會定義發佈頁面在發佈環境中隱藏的時間。

對於您要發佈的頁面，請將這些欄位（**開啟時間**&#x200B;和&#x200B;**關閉時間**）留空，這些欄位可立即使用並在發佈環境中使用，直到它們停用（一般案例）為止。

>[!NOTE]
>如果&#x200B;**開啟時間**&#x200B;或&#x200B;**關閉時間**&#x200B;是過去的時間，且已設定自動復寫，則會立即觸發相關動作。

>[!TIP]
>
>開啟/關閉時間需嚴格處理已發佈的內容（手動或透過自動復寫）。 因此，不會觸發發佈工作流程（例如核准內容的工作流程），開啟/關閉時間也不會影響頁面的發佈狀態。 因此，開啟/關閉時間最適合暫時顯示/隱藏已核准和發佈的內容。
>
>如果您想要發佈包含所有關聯工作流程的新內容，或從您的網站中完全移除（取消發佈內容），請考慮[管理您的出版物。](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)

### 虛名 URL {#vanity-url}

此屬性可讓您輸入此頁面的虛名URL，此URL可讓您使用較短和/或較具表現力的URL。 例如，如果網站`welcome`的虛名URL設定為路徑`/v1.0/startpage`所識別的頁面`http://example.com`，則`http://example.com/welcome`將是`http://example.com/content/v1.0/startpage`的虛名URL

>[!CAUTION]
>
>虛名URL：
>
>* 必須是唯一的。
>* 不支援規則運算式模式。
>* 不應設為現有頁面。

* **新增** — 選取以顯示欄位來定義頁面的虛名URL。
   * 再次選取以新增多個。
   * 選取&#x200B;**移除**&#x200B;圖示以刪除虛名URL。
* **重新導向虛名URL** — 指出您是要讓頁面使用虛名URL，還是重新導向至頁面的實際URL

## 進階 {#advanced}

### 設定 {#settings}

* **語言** — 頁面語言
* **語言根** — 如果頁面是語言副本的根，則必須檢查
* **重新導向** — 指出此頁面應該以HTML `302 Found`狀態自動重新導向的頁面
   * **永久重新導向** — 選取後，頁面會重新導向至與HTML `301 Moved Permanently`狀態一起提供的目標路徑。
* **Design**
* **別名** — 指定要用於此頁面的別名
   * 例如，如果您為頁面`private`定義別名`/content/wknd/us/en/magazine/members-only`，則也可以透過`/content/wknd/us/en/magazine/private`存取此頁面
   * 建立別名會設定頁面節點上的`sling:alias`屬性，這只會影響資源，而不會影響存放庫路徑。
   * 無法發佈編輯器中以別名存取的頁面。 編輯器中的[發佈選項](/help/sites-cloud/authoring/sites-console/publishing-pages.md)僅適用於透過實際路徑存取的頁面。
   * 如需詳細資訊，請參閱SEO和URL管理最佳實務底下的[本地化頁面名稱](/help/overview/seo-and-url-management.md#localized-page-names)。

### 設定 {#configuration}

* **繼承自&lt;path>** — 啟用/停用頁面&#x200B;**雲端設定**&#x200B;的繼承
   * 切換&#x200B;**雲端設定**&#x200B;的可用性以進行編輯

* **雲端設定** — 所選設定的路徑

### 範本設定 {#template-settings}

* **允許的範本** - [定義此子分支內可用的範本清單](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author)
   * 每個值都必須是範本的絕對路徑。
   * 使用`/.*`以允許此路徑下的所有範本。
* **使用頁面作為範本** - [根據目前頁面建立新範本。](/help/sites-cloud/authoring/universal-editor/templates.md)
   * 僅適用於搭配Universal Editor (善用Edge Delivery Services)使用而建立的頁面。

### 驗證需求 {#authentication}

* **啟用** — 允許使用驗證來存取頁面

>[!NOTE]
>
>已關閉的使用者群組定義於&#x200B;**[許可權](#permissions)**&#x200B;索引標籤上。

* **登入頁面** — 要用於登入的頁面

### 匯出 {#export}

* **匯出組態** — 指定匯出組態

## SEO {#seo}

* **標準URL** — 用於覆寫頁面的標準URL
   * 如果保留為空白，頁面的URL將是其標準URL。

* **Robots標籤** — 使用下拉式清單來選取Robots標籤，以控制搜尋引擎編目程式的行為
   * 有些選項會相互衝突，以較寬鬆的選項優先。

* **產生Sitemap** — 選取時，會為此頁面及其子系產生`sitemap.xml`。

## 影像 {#images}

### 精選影像 {#featured-image}

此區段用於選取和設定要精選的影像。 這用於參考頁面的元件中；例如，Teaser、頁面清單等。

* **影像** — 您可以&#x200B;**挑選**&#x200B;資產，或瀏覽要上傳的檔案，然後&#x200B;**編輯**&#x200B;或&#x200B;**清除**&#x200B;選取的影像。
* **替代文字** — 用來代表影像含義及/或功能的文字，通常由熒幕朗讀程式使用
* **繼承 — 取自DAM資產的值** — 選取後，替代文字會填入DAM中`dc:description`中繼資料的值。

### 縮圖 {#thumbnail}

此區段用於選取和設定頁面的影像縮圖。 這用於參考頁面的元件中；例如，Teaser、頁面清單等。

* **產生預覽** — 產生頁面預覽，以做為縮圖使用
* **上傳影像** — 上傳要做為縮圖的影像
* **選取影像** — 選取要當作縮圖的現有資產
* **回覆** — 在您變更縮圖後，此選項即可使用。 如果您不想保留變更，則可以在儲存前還原該變更。

## 雲端服務 {#cloud-services}

* **Cloud Service設定** — 定義用於頁面的雲端服務設定
* **繼承自** — 對於即時副本和語言副本，預設會從Blueprint繼承雲端設定。
   * 取消勾選以覆寫繼承

## 個人化 {#personalization}

### ContextHub 組態 {#contexthub-config}

* **ContextHub路徑** — 定義[ContextHub設定](/help/sites-cloud/authoring/personalization/contexthub.md)
* **區段路徑** — 定義[區段路徑](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

### 定位組態 {#targeting-config}

* **品牌** — 定義[品牌以指定目標定位的範圍](/help/sites-cloud/authoring/personalization/targeted-content.md)
   * 此選項要求使用者帳戶必須位於`Target Administrators`群組中。

## 權限 {#permissions}

使用&#x200B;**許可權**&#x200B;索引標籤來定義哪些使用者、群組或[已關閉的使用者群組(CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=zh-Hant)可以存取和/或修改頁面。

* **新增權限**
* **編輯已關閉的使用者群組**
* 檢視&#x200B;**有效許可權**

## 藍圖 {#blueprint}

此索引標籤僅對做為Blueprint的頁面可見。 藍圖是即時副本的基礎，也是[多網站管理的一部分。](/help/sites-cloud/administering/msm/overview.md)

* **轉出** — 開始將Blueprint內容轉出至即時副本
* **即時副本總覽** — 開啟視窗以瀏覽即時副本頁面結構
* **目前的即時副本** — 以所選Blueprint頁面為基礎（即即時副本）的頁面清單

## Live Copy {#live-copy}

此標籤僅對設定為即時副本的頁面可見。 和[藍圖一樣，](#blueprint)即時副本是[多網站管理的一部分。](/help/sites-cloud/administering/msm/overview.md)

* **同步** — 同步即時副本與藍圖，並保留本機修改
* **重設** — 將即時副本重設為Blueprint的狀態，並移除本機修改
* **暫停** — 暫停即時副本，以防止進一步的轉出修改
* **分離** — 從Blueprint分離即時副本

### 來源 {#source}

* 顯示此即時副本的Blueprint路徑

### 狀態 {#status}

* 列出頁面的目前即時副本狀態

### 設定 {#live-copy-config}

* **即時副本繼承** — 如果勾選，即時副本設定將在所有子項上都有效。
* **從父項繼承轉出設定** — 如果勾選，則從頁面的父項繼承轉出設定。
* **選擇轉出設定** — 定義從Blueprint傳播修改的情況，且僅當未選取&#x200B;**從父項繼承轉出設定**&#x200B;時可用
* **排除的路徑清單**

## 預覽 {#preview}

啟用[預覽環境](/help/sites-cloud/authoring/sites-console/previewing-content.md)時，可以使用下列詳細資料：

* **預覽URL** — 用來存取預覽環境中內容的URL

## 漸進式網頁應用程式 {#progressive-web-app}

透過簡單的設定，內容作者就能為AEM Sites中建立的體驗啟用漸進式網頁應用程式(PWA)功能。 然後，您的網站便可安裝在訪客裝置的首頁畫面上，並可供離線使用，其行為與原生應用程式類似。

{{pwa-deprecation}}

### 設定可安裝體驗 {#config-pwa}

* **啟用PWA** — 啟用後，頁面的訪客可以安裝網站作為PWA。
* **啟動URL** — 使用者啟動網頁應用程式時應載入的URL
   * 如果URL是相對的，則資訊清單URL會作為基礎URL來解析
   * 當空白時，系統會使用安裝應用程式所在頁面的URL。
   * 建議設定值。
* **顯示模式** — 如何隱藏瀏覽器或如何以其他方式顯示給本機裝置上的使用者
* **熒幕方向** - PWA如何處理裝置方向
* **佈景主題色彩** — 應用程式的色彩，會影響本機使用者的作業系統顯示原生UI工具列和導覽控制項的方式
* **背景色彩** — 應用程式的背景色彩，會在應用程式載入時顯示
* **圖示** — 安裝PWA時，代表使用者裝置上的應用程式的圖示

### 快取管理 (進階) {#cache-management}

* **快取策略與內容重新整理頻率** — 定義PWA的快取模型。
* **要快取供離線使用的檔案**
   * **檔案預先快取（技術預覽）** — 在AEM上託管的檔案會在安裝Service Worker時和使用它之前儲存到本機瀏覽器快取。
   * **使用者端資料庫** — 要快取以供離線體驗的使用者端資料庫
   * **路徑包含** — 已攔截定義路徑的網路要求，並根據設定的快取策略與內容重新整理頻率傳回快取的內容
   * **路徑排除** — 無論檔案預先快取和路徑包含下的設定為何，都不會快取這些檔案。

>[!NOTE]
>
>如需詳細資訊，請參閱[啟用漸進式網頁應用程式功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md)。

