---
title: Dynamic Media 疑難排解
description: 瞭解當您在Dynamic Media中處理影像、集和檢視器時，可以嘗試的疑難排解提示。
contentOwner: Rick Brough
feature: Troubleshooting,Image Sets,Viewers
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 1%

---

# Dynamic Media 疑難排解 {#troubleshooting-dynamic-media-scene-mode}

下列主題說明Dynamic Media的疑難排解。

## 新增Dynamic Media設定 {#new-dm-config}

請參閱[新Dynamic Media組態的疑難排解](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config)。

## 一般(所有Assets) {#general-all-assets}

以下是適用於所有資產的一些一般提示和訣竅。

### 資產同步狀態屬性 {#asset-synchronization-status-properties}

您可在CRXDE Lite中檢閱下列資產屬性，以確認資產成功從Adobe Experience Manager同步至Dynamic Media：

| **屬性** | **範例** | **說明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | 節點連結至Dynamic Media的一般指標。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete**&#x200B;或錯誤文字 | 將資產上傳至Dynamic Media的狀態。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必須填入才能產生Dynamic Media遠端資產的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **成功**&#x200B;或&#x200B;**失敗：`<error text>`** | 集合（迴轉集、影像集等）、影像預設集、檢視器預設集、資產的影像地圖更新或已編輯影像的同步狀態。 |

### 同步記錄 {#synchronization-logging}

同步處理錯誤和問題記錄在`error.log` (Experience Manager伺服器目錄`/crx-quickstart/logs/`)。 有充足的記錄可判斷大部分問題的根本原因，但您可以透過Sling主控台(`com.adobe.cq.dam.ips`https://localhost[/system/console/slinglog:4502)增加](https://localhost:4502/system/console/slinglog)套件上DEBUG的記錄以收集詳細資訊。

### 版本控制 {#version-control}

取代現有的Dynamic Media資產（相同的名稱和位置）時，您可以保留兩個資產或取代/建立版本：

* 同時保留這兩個專案，可為已發佈的資產URL建立唯一名稱的資產。 例如，`image.jpg`是原始資產，`image1.jpg`是新上傳的資產。

* Dynamic Media不支援建立版本。 新版本會取代傳送中的現有資產。

## 影像和集合 {#images-and-sets}

如果您遇到影像和集問題，請參閱下列疑難排解指南。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何除錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法存取資產詳細資料檢視中的複製URL/內嵌按鈕</td>
   <td>
    <ol>
     <li><p>前往CRX/DE：</p>
      <ul>
       <li>檢查JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code>中的預設集是否已定義。 如果您從Experience Manager 6.x升級至6.4並選擇退出移轉，則此位置適用。 否則，位置為<code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>確認JCR中的資產在中繼資料下有<code>dam:scene7FileStatus</code><strong> </strong>顯示為<code>PublishComplete</code>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>重新整理頁面/導覽至其他頁面並返回（側邊欄JSP必須重新編譯）</p> <p>如果這樣行不通：</p>
    <ul>
     <li>發佈資產。</li>
     <li>重新上傳資產並發佈。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>在幻燈片之間切換後，輪播熱點會四處移動</td>
   <td><p>檢查所有幻燈片的大小是否相同。</p> </td>
   <td><p>轉盤僅使用相同大小的影像。</p> </td>
  </tr>
  <tr>
   <td>影像未使用動態媒體檢視器預覽</td>
   <td><p>檢查資產的中繼資料屬性(CRXDE Lite)中是否包含<code>dam:scene7File</code></p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>上傳的資產未顯示在資產選擇器中</td>
   <td><p>檢查資產具有屬性<code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>當資產尚未開始處理時，卡片檢視上的橫幅會顯示<strong>新的</strong></td>
   <td>檢查資產<code>jcr:content</code> &gt; <code>dam:assetState</code> =如果工作流程未擷取資產<code>unprocessed</code>。</td>
   <td>等到工作流程擷取資產為止。</td>
  </tr>
  <tr>
   <td>影像或集未顯示檢視器URL或內嵌程式碼</td>
   <td>檢查檢視器預設集是否已發佈。</td>
   <td><p>移至<strong>工具</strong> &gt; <strong>Assets</strong> &gt; <strong>檢視器預設集</strong>並發佈檢視器預設集。</p> </td>
  </tr>
 </tbody>
</table>

## 影片 {#video}

如果您有視訊問題，請參閱下列疑難排解指南。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何除錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法預覽視訊</td>
   <td>
    <ul>
     <li>檢查資料夾是否已指派視訊設定檔（如果不支援的檔案格式）。 如果不支援，則只會顯示影像。</li>
     <li>視訊設定檔必須包含多個編碼預設集，才能產生AVS集（單一編碼會視為MP4檔案的視訊內容；若為非支援的檔案，則會視為非處理的檔案）。</li>
     <li>確認中繼資料中的<code>dam:scene7FileAvs</code>個（共<code>dam:scene7File</code>個），以檢查視訊是否已完成處理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊設定檔指派至資料夾。</li>
     <li>編輯視訊設定檔以包含一個以上的編碼預設集。</li>
     <li>等候視訊完成處理。</li>
     <li>在您重新載入視訊之前，請確定Dynamic Media編碼視訊工作流程未執行。<br/> </li>
     <li>重新上傳視訊。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊未編碼</td>
   <td>
    <ul>
     <li>檢查是否已設定Dynamic Media Cloud Service。</li>
     <li>檢查視訊設定檔是否與上傳資料夾相關聯。</li>
    </ul> </td>
   <td>
    <ol>
     <li>檢查雲端服務底下的Dynamic Media設定是否已正確設定。</li>
     <li>檢查資料夾是否有視訊設定檔。 此外，檢查視訊設定檔。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊處理花費太長時間</td>
   <td><p>若要判斷視訊編碼是否仍在進行中，或已進入失敗狀態：</p>
    <ul>
     <li>檢查視訊狀態<code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>缺少視訊轉譯</td>
   <td><p>已上傳視訊，但無編碼轉譯時：</p>
    <ul>
     <li>檢查資料夾是否已指派視訊設定檔。</li>
     <li>確認中繼資料中的<code>dam:scene7FileAvs</code>，以檢查視訊是否已完成處理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊設定檔指派至資料夾。</li>
     <li>等候視訊完成處理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 檢視器 {#viewers}

若檢視器發生問題，請參閱下列疑難排解指南。

### 問題：檢視器預設集未發佈 {#viewers-not-published}

**如何偵錯**

1. 繼續範例管理員診斷頁面： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`。
1. 觀察計算值。 正確操作時，您會看到下列專案： `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`。

   >[!NOTE]
   >
   >設定Dynamic Media雲端設定後，檢視器資產可能需要約10分鐘的時間才能同步。

1. 如果未啟用的資產仍保留，請選取&#x200B;**列出所有未啟用的Assets**&#x200B;按鈕之一，以檢視詳細資料。

**解決方案**

1. 瀏覽至管理工具中的檢視器預設集清單： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. 選取所有檢視器預設集，然後選取&#x200B;**發佈**。
1. 導覽回範例管理員，並觀察未啟用的資產計數現在為零。

### 問題：檢視器預設集圖稿從資產詳細資料中的預覽或複製URL/內嵌程式碼中返回404 {#viewer-preset-404}

**如何偵錯**

在CRXDE Lite中執行下列動作：

1. 導覽至Dynamic Media同步處理資料夾中的`<sync-folder>/_CSS/_OOTB`資料夾（例如`/content/dam/_CSS/_OOTB`）。
1. 尋找有問題的資產的中繼資料節點（例如，`<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`）。
1. 檢查`dam:scene7*`屬性是否存在。 如果資產已成功同步和發佈，您會看到`dam:scene7FileStatus`集合為&#x200B;**PublishComplete**。
1. 串連下列屬性和字串常值的值，嘗試直接向Dynamic Media要求圖稿：

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
範例： `https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**解決方案**

如果範例資產或檢視器預設集圖稿尚未同步或發佈，請重新啟動整個複製/同步程式：

1. 導覽至CRXDE Lite。
1. 刪除`<sync-folder>/_CSS/_OOTB`。
1. 瀏覽至CRX封裝管理員： `https://localhost:4502/crx/packmgr/`。
1. 在清單中搜尋檢視器套件；它以`cq-dam-scene7-viewers-content`開頭。
1. 選取&#x200B;**重新安裝**。
1. 在雲端服務底下，導覽至Dynamic Media設定頁面，然後開啟Dynamic Media - S7設定的設定對話方塊。
1. 不做任何變更，選取&#x200B;**儲存**。
這個儲存動作會再次觸發邏輯，以建立並同步範例資產、檢視器預設集CSS和圖稿。

### 問題：檢視器預設集製作中未載入影像預覽 {#image-preview-not-loading}

**解決方案**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**。
1. 在左側邊欄中，導覽至下列位置的範例內容資料夾：

   `/content/dam/_DMSAMPLE`

1. 刪除`_DMSAMPLE`資料夾。
1. 在左側邊欄中，導覽至下列位置的預設集資料夾：

   `/conf/global/settings/dam/dm/presets/viewer`

1. 刪除`viewer`資料夾。
1. 在CRXDE Lite頁面的左上角附近，選取&#x200B;**[!UICONTROL 全部儲存]**。
1. 在CRXDE Lite頁面的左上角，選取&#x200B;**首頁**&#x200B;圖示。
1. 在雲端服務[中重新建立](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)Dynamic Media設定。
