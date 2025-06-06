---
title: 編輯頁面屬性
description: 瞭解如何定義在AEM中管理頁面所需的屬性。
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 8d31907392e09bc5b3c669b8f8f23d6a2a26ced4
workflow-type: tm+mt
source-wordcount: '2454'
ht-degree: 3%

---

# 編輯頁面屬性 {#editing-page-properties}

您可以定義頁面的必要屬性。 這些值可能會因頁面性質而異。 例如，有些頁面可能已連線至即時副本，有些頁面則未連線，因此即時副本資訊可供適當使用。

## 頁面屬性 {#page-properties}

屬性分佈於數個索引標籤中。

### 基本 {#basic}

* **標題和標籤**

   * **標題** — 頁面的標題會顯示在不同的位置。 例如，**網站**&#x200B;索引標籤清單和&#x200B;**網站**&#x200B;卡片/清單檢視。
      * 這是必要欄位。
   * **標籤** — 您可以在此處更新選取方塊中的清單，在頁面中新增或移除標籤。
      * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
      * 在空白選取方塊中輸入名稱，即可輸入全新的標籤。
         * 當您按下Enter鍵時，就會建立新標籤。
         * 然後，新標籤將顯示為右側的小型星號，表示它是新標籤。
      * 使用下拉式功能，您可以從現有標籤中選取。
      * 當您將滑鼠移到選取方塊中的標籤專案上時，會出現x，可用來為此頁面移除該標籤。
      * 如需關於標籤的詳細資訊，請參閱[使用標籤](/help/sites-cloud/authoring/sites-console/tags.md)。
   * **在導覽中隱藏** — 指示在產生的網站頁面導覽中是顯示還是隱藏頁面。

* **品牌**

  藉由將品牌概要附加至每個頁面標題，跨頁面套用一致的品牌識別。 此功能需要使用2.14.0版或更新版本的[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hant)的頁面元件。

   * **品牌概要**

      * **覆寫** — 檢查以在此頁面上定義品牌概要。
         * 此值由任何子頁面繼承，除非它們也設定了&#x200B;**覆寫**&#x200B;值。
      * **覆寫值** — 要附加至頁面標題的品牌概要文字。
         * 此值會附加至頁面標題後的垂直號字元，例如「騎行Tuscany」 | 隨時準備使用WKND」

* **HTML ID**

   * **ID** — 要套用至元件的HTML ID。

* **更多標題和說明**

   * **頁面標題** — 要在頁面上使用的標題。 通常由標題元件使用。 如果空白，則使用&#x200B;**標題**。
   * **導覽標題** — 您可以指定單獨的標題以用於導覽（例如，如果您想要更簡潔的標題）。 如果空白，則使用&#x200B;**標題**。
   * **標題** — 頁面上使用的子標題。
   * **描述** — 頁面的描述、用途或您要新增的任何其他詳細資訊。

* **開啟/關閉時間**

  >[!NOTE]
  >
  > 請參閱[開啟和關閉時間 — 觸發器組態](/help/operations/replication.md#on-and-off-times-trigger-configuration)，以取得有關如何設定相關自動復寫的詳細資訊。

  >[!NOTE]
  >如果&#x200B;**開啟時間**&#x200B;或&#x200B;**關閉時間**&#x200B;是過去的時間，且已設定自動復寫，則會立即觸發相關動作。

   * **開啟時間** — 已發佈頁面在發佈環境中可見（轉譯）的日期和時間。 頁面必須以手動方式或預先設定的自動復寫方式發佈。

      * 如果已經[發佈（手動）](/help/sites-cloud/authoring/sites-console/publishing-pages.md)此頁面會保持隱匿（隱藏）狀態，直到在指定時間才呈現。
      * 如果未發佈且已設定為自動復寫，則頁面會在指定時間自動發佈，然後呈現。
      * 如果未發佈且未設定為自動復寫，則不會自動發佈頁面，因此嘗試存取該頁面時會顯示404。

   * **關閉時間** — 類似於&#x200B;**開啟時間**，且經常與其搭配使用，這會定義發佈頁面在發佈環境中隱藏的時間。

   * 對於您要立即發佈並在發佈環境中可用的頁面，請將這些欄位（**開啟時間**&#x200B;和&#x200B;**關閉時間**）保留空白，直到它們停用（一般案例）。

* **虛名URL**

   * 可讓您輸入此頁面的虛名URL，此URL可讓您擁有較短和/或較具表現力的URL。
   * 例如，如果網站`http://example.com`的虛名URL設定為路徑`/v1.0/startpage`所識別的頁面`welcome`，則`http://example.com/welcome`將是`http://example.com/content/v1.0/startpage`的虛名URL

  >[!CAUTION]
  >
  >虛名URL：
  >
  >* 必須是唯一的，因此您應該注意該值尚未被其他頁面使用。
  >* 不支援規則運算式模式。
  >* 不應設為現有頁面。

   * **新增** — 選取以顯示欄位來定義頁面的虛名URL。
      * 再次選取以新增多個。
      * 選取&#x200B;**移除**&#x200B;圖示以刪除虛名URL。
   * **重新導向虛名URL** — 指出您是否希望頁面使用虛名URL。

### 進階 {#advanced}

* **設定**

   * **語言** — 頁面語言
   * **語言根** — 如果頁面是語言副本的根，則必須檢查
   * **重新導向** — 指出此頁面應該以HTML `302 Found`狀態自動重新導向的頁面。
      * **永久重新導向** — 選取後，頁面會重新導向至與HTML `301 Moved Permanently`狀態一起提供的目標路徑。
   * **設計** — 指出在產生的網站頁面導覽中顯示或隱藏頁面
   * **別名** — 指定要用於此頁面的別名
      * 例如，如果您為頁面`/content/wknd/us/en/magazine/members-only`定義別名`private`，則也可以透過`/content/wknd/us/en/magazine/private`存取此頁面
      * 建立別名會設定頁面節點上的`sling:alias`屬性，這只會影響資源，而不會影響存放庫路徑。
      * 無法發佈編輯器中以別名存取的頁面。 編輯器中的[發佈選項](/help/sites-cloud/authoring/sites-console/publishing-pages.md)僅適用於透過實際路徑存取的頁面。
      * 請參閱SEO和URL管理最佳實務下的[本地化頁面名稱](/help/overview/seo-and-url-management.md#localized-page-names)。

* **組態**

   * **繼承自&lt;path>** — 啟用/停用繼承；切換&#x200B;**雲端設定**&#x200B;的可用性以進行選擇

   * **雲端設定** — 所選設定的路徑

* **範本設定**

   * **允許的範本** - [定義此子分支內可用的範本清單](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author)
   * **使用頁面作為範本** - [根據目前頁面建立新範本。](/help/sites-cloud/authoring/universal-editor/templates.md)
      * 僅適用於搭配Universal Editor (善用Edge Delivery Services)使用而建立的頁面。

* **驗證需求**

   * **啟用** — 啟用使用驗證來存取頁面

     >[!NOTE]
     >
     >已關閉的使用者群組定義於&#x200B;**[許可權](#permissions)**&#x200B;索引標籤上。

   * **登入頁面** — 要用於登入的頁面

* **匯出**

   * **匯出組態** — 指定匯出組態

* **SEO**

   * **標準URL** — 可用於覆寫頁面的標準URL；如果留白，則頁面的URL為標準URL

   * **Robots標籤** — 選取Robots標籤來控制搜尋引擎編目程式的行為。

     >[!NOTE]
     >
     >有些選項會相互衝突。 發生衝突時，以更寬鬆的選項優先。

   * **產生Sitemap** — 選取時，會為此頁面及其子系產生sitemap.xml

### 影像 {#images}

* **精選影像**

  選取並設定要精選的影像。 這用於參考頁面的元件中；例如，Teaser、頁面清單等。

   * **影像**

     您可以&#x200B;**挑選**&#x200B;資產，或瀏覽檔案以上傳，然後&#x200B;**編輯**&#x200B;或&#x200B;**清除**。

   * **替代文字** — 用來代表影像含義及/或功能的文字；例如，供熒幕閱讀程式使用。

   * **繼承 — 從DAM資產中取得的值** — 勾選時，這會以DAM中`dc:description`中繼資料的值填入替代文字

* **縮圖**

  設定頁面縮圖

   * **產生預覽** — 產生頁面預覽，以做為縮圖使用
   * **上傳影像** — 上傳要做為縮圖的影像
   * **選取影像** — 選取要當作縮圖的現有資產
   * **回覆** — 在您變更縮圖後，此選項即可使用。 如果您不想保留變更，則可以在儲存前還原該變更。

### 雲端服務 {#cloud-services}

* **Cloud Service設定** — 定義雲端服務的屬性

### 個人化 {#personalization}

* **ContextHub設定**

   * **繼承自&lt;path>** — 啟用/停用繼承；切換&#x200B;**ContextHub路徑**&#x200B;和&#x200B;**區段路徑**&#x200B;的可用性以進行選擇

   * **ContextHub路徑** — 定義[ContextHub設定](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **區段路徑** — 定義[區段路徑](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **目標定位組態**

   * **品牌** — 定義[品牌以指定鎖定目標](/help/sites-cloud/authoring/personalization/targeted-content.md)的範圍。

  >[!NOTE]
  >此選項要求使用者帳戶必須屬於`Target Administrators`群組。

### 權限 {#permissions}

* **許可權**

   * **新增權限**
   * **編輯已關閉的使用者群組**
   * 檢視&#x200B;**有效許可權**

### 藍圖 {#blueprint}

此索引標籤僅對做為Blueprint的頁面可見。 藍圖是即時副本的基礎，也是[多網站管理](/help/sites-cloud/administering/msm/overview.md)的一部分。

* **目前的即時副本** — 列出以此Blueprint頁面為根據的頁面（即即時副本）

* **轉出設定** — 控制將修改傳播至即時副本的情況

### Live Copy {#live-copy}

此標籤僅對設定為即時副本的頁面可見。 如同藍圖，即時副本是[多網站管理](/help/sites-cloud/administering/msm/overview.md)的一部分。

* **同步** — 同步即時副本與藍圖，並保留本機修改
* **重設** — 將即時副本重設為Blueprint的狀態，並移除本機修改
* **暫停** — 暫停即時副本，以防止進一步的轉出修改
* **分離** — 從Blueprint分離即時副本

* **Source**

   * 顯示此即時副本的Blueprint路徑

* **狀態**

   * 列出頁面的目前即時副本狀態

* **組態**

   * **即時副本繼承** — 如果勾選，即時副本設定將在所有子項上都有效
   * **從父項繼承轉出設定** — 如果勾選，則從頁面的父項繼承轉出設定
   * **選擇轉出設定** — 定義從Blueprint傳播修改的情況，且僅當未選取&#x200B;**從父項繼承轉出設定**&#x200B;時可用

### 預覽 {#preview}

啟用預覽環境時，您會看到下列內容：

* 預覽URL — 在預覽環境中用於存取內容的URL

### 漸進式網頁應用程式 {#progressive-web-app}

透過簡單的設定，內容作者現在可以為在AEM Sites中建立的體驗啟用漸進式網頁應用程式(PWA)功能。

>[!NOTE]
>
>如需詳細資訊，請參閱[啟用漸進式網頁應用程式功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md)。

{{pwa-deprecation}}

* **設定可安裝的體驗**

   * **啟用PWA** — 啟用/停用此功能；允許使用者將網站安裝為PWA
   * **StartupURL** — 偏好的啟動URL
   * **顯示模式** — 如何隱藏瀏覽器或如何以其他方式顯示給本機裝置上的使用者
   * **熒幕方向** - PWA如何處理裝置方向
   * **佈景主題色彩** — 應用程式的色彩，會影響本機使用者的作業系統顯示原生UI工具列和導覽控制項的方式
   * **背景色彩** — 應用程式的背景色彩，會在應用程式載入時顯示
   * **圖示** — 代表使用者裝置上的應用程式的圖示

* **快取管理（進階）**

   * **快取策略與內容重新整理頻率** — 定義PWA的快取模型
   * **要快取供離線使用的檔案**
      * **檔案預先快取（技術預覽）** — 在AEM上託管的檔案會在安裝Service Worker時和使用它之前儲存到本機瀏覽器快取
      * **使用者端資料庫** — 要快取以供離線體驗的使用者端資料庫
      * **路徑包含** — 已攔截定義路徑的網路要求，並根據設定的快取策略與內容重新整理頻率傳回快取的內容
      * **路徑排除** — 無論檔案預先快取和路徑包含下的設定為何，都不會快取這些檔案

## 編輯頁面屬性 {#editing-page-properties-1}

* 從&#x200B;**網站**&#x200B;主控台：
   * [建立新頁面](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page) （屬性的子集）
   * 按一下或點選&#x200B;**屬性**
      * 針對單一頁面
      * 針對多個頁面（只有屬性的子集可整體編輯）
* 從頁面編輯器：
   * 使用 **頁面資訊** (接著 **開啟屬性**)

### 從Sites Console — 單一頁面 {#from-the-sites-console-single-page}

按一下或點選&#x200B;**屬性**&#x200B;以定義頁面屬性：

1. 使用&#x200B;**網站**&#x200B;主控台，導覽至您要檢視及編輯屬性的頁面位置。
1. 使用以下其中一種方式，為必要頁面選取&#x200B;**屬性**&#x200B;選項：
   * [快速動作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/basic-handling.md#selecting-resources)
   * 頁面屬性會使用適當的索引標籤顯示。
1. 視需要檢視或編輯屬性。
1. 然後使用&#x200B;**儲存**&#x200B;儲存您的更新，接著使用&#x200B;**關閉**&#x200B;返回主控台。

### 編輯頁面時 {#when-editing-a-page}

編輯頁面時，您可以使用&#x200B;**頁面資訊**&#x200B;來定義頁面屬性：

1. 開啟您要編輯屬性的頁面。
1. 選取&#x200B;**頁面資訊**&#x200B;圖示以開啟選取功能表：
1. 選取「**開啟屬性**」，並開啟一個對話方塊，讓您按適當的索引標籤排序來編輯屬性。 工具列右側也提供下列按鈕：
   * **取消**
   * **儲存並關閉**
1. 使用&#x200B;**儲存並關閉**&#x200B;按鈕來儲存變更。

### 從Sites Console — 多個頁面 {#from-the-sites-console-multiple-pages}

從Sites **&#x200B;**&#x200B;Console中，您可以選取數個頁面，然後使用 **View Properties**  (檢視屬性) 來檢視和/或編輯頁面屬性。這稱為頁面屬性的大量編輯。

您可以選取多個頁面以透過各種方法進行大量編輯，包括：

* 瀏覽&#x200B;**網站**&#x200B;主控台時
* 使用&#x200B;**搜尋**&#x200B;尋找一組頁面之後

選取頁面，然後按一下或點選「**屬性」選項**，就會顯示大量屬性：

![大量編輯頁面屬性](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

您只能大量編輯符合以下條件的頁面：

* 共用相同的資源型別
* 不是Livecopy的一部分
   * 如果有任何頁面位於即時副本中，則會在屬性開啟時顯示訊息。

進入「大量編輯」後，您可以：

* **檢視**

   * 受影響的頁面清單
      * 您可以選取/取消選取（如有必要）
      * 標籤
         * 和檢視單一頁面屬性時一樣，屬性會依索引標籤排序。
   * 屬性的子集
      * 會顯示所有選定頁面上可用的屬性，這些屬性已明確定義為可大量編輯。
      * 如果您將頁面選取範圍縮小至一頁，則會顯示所有屬性。
   * 具有共同值的共同屬性
      * 在「檢視」模式中只會顯示具有相同值的屬性。
      * 當欄位有多個值時（例如Tags），只有在&#x200B;*所有*&#x200B;為通用時，才會顯示值。 如果只有部分相同，則僅在編輯時顯示。
      * 如果沒有任何具有相同值的屬性存在，則會顯示訊息。

* **編輯**

   * 您可以更新可用欄位中的值。
      * 當您選取&#x200B;**完成**&#x200B;時，新值會套用至所有選取的頁面。
      * 當欄位有多個值時（例如「標籤」），您可以附加新值或移除通用值。
   * 不同頁面中相同但值不同的欄位會以特殊值（例如文字`<Mixed Entries>`）表示。

## 屬性繼承 {#inheritance}

如果頁面是根據Blueprint或繼承其他頁面的內容，繼承會反映在個別欄位的&#x200B;**頁面屬性**&#x200B;視窗中。

![繼承的屬性](assets/property-inhertiance.png)

繼承的屬性無法編輯。 點選或按一下特定欄位旁的&#x200B;**取消繼承**&#x200B;圖示以中斷其繼承。

![取消繼承](assets/cancel-inheritance.png)

在&#x200B;**取消繼承**&#x200B;強制回應視窗中確認取消。

![取消繼承確認模式](assets/cancel-inheriance-confirmation.png)

取消欄位的繼承後，該欄位就會變成可編輯。

![已取消繼承](assets/property-inheritance-broken.png)

若要恢復繼承，請點選或按一下欄位旁的&#x200B;**還原繼承**&#x200B;圖示。

![還原繼承](assets/revert-inheritance.png)

在&#x200B;**還原繼承**&#x200B;強制回應中確認重新版本。

![還原繼承確認強制回應視窗](assets/revert-inhertiance-confirmation.png)

在恢復繼承&#x200B;**後選取「**&#x200B;同步頁面」以使用Blueprint中的最新值更新欄位。 否則，下次同步化LiveCopy時將會更新值。

>[!TIP]
>
>如需繼承的詳細資訊，請參閱檔案[多網站管理員與翻譯](/help/sites-cloud/administering/msm-and-translation.md)
