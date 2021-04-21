---
title: Dynamic Media 疑難排解
description: 使用Dynamic Media時的疑難排解提示。
role: Administrator,Business Practitioner
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 1%

---

# Dynamic Media 疑難排解 {#troubleshooting-dynamic-media-scene-mode}

以下主題介紹Dynamic Media的故障排除。

## 新Dynamic Media配置{#new-dm-config}

請參閱[疑難排解新的Dynamic Media配置](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config)。

## 一般（所有資產）{#general-all-assets}

以下是所有資產的一些一般提示和秘訣。

### 資產同步狀態屬性{#asset-synchronization-status-properties}

以下資產屬性可以在CRXDE Lite中查看，以確認資產從Adobe Experience Manager到Dynamic Media的成功同步：

| **屬性** | **範例** | **說明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 一般指示該節點已連結至Dynamic Media。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **** PublishCompleteor錯誤文字 | 資產上傳至Dynamic Media的狀態。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必須填入，才能產生Dynamic Media遠端資產的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **繼** 承 **者失敗：`<error text>`** | 集（回轉集、影像集等）、影像預設集、檢視器預設集、資產的影像地圖更新，或已編輯的影像的同步狀態。 |

### 同步記錄{#synchronization-logging}

同步錯誤和問題記錄在`error.log`(Experience Manager伺服器目錄`/crx-quickstart/logs/`)中。 您可使用充份的記錄功能來判斷大多數問題的根本原因，不過您可以透過Sling Console([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))，將`com.adobe.cq.dam.ips`套件上的記錄功能增加為DEBUG，以收集更多資訊。

### 版本控制 {#version-control}

取代現有的Dynamic Media資產（相同名稱和位置）時，您可以同時保留這兩個資產或取代／建立版本：

* 同時保留兩者會為已發佈的資產URL建立具有唯一名稱的資產。 例如，`image.jpg`是原始資產，而`image1.jpg`是新上傳的資產。

* Dynamic Media不支援建立版本。 新版本會取代傳送中的現有資產。

## 影像和集{#images-and-sets}

如果您對影像和設定有任何問題，請參閱下列疑難排解指引。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何除錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法在資產詳細資料檢視中存取複製URL/內嵌按鈕</td>
   <td>
    <ol>
     <li><p>前往CRX/DE:</p>
      <ul>
       <li>檢查JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code>中是否定義了預設集。 如果您從Experience Manager6.x升級到6.4，並選擇退出遷移，則此位置適用。 否則，位置為<code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>檢查以確定JCR中的資產在「中繼資料」下有<code>dam:scene7FileStatus</code><strong> </strong>顯示為<code>PublishComplete</code>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>重新整理頁面／導覽至另一頁並返回（必須重新編譯側欄JSP）</p> <p>如果這不管用：</p>
    <ul>
     <li>發佈資產。</li>
     <li>重新上傳資產並發佈。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>切換投影片後，轉盤熱點會四處移動</td>
   <td><p>檢查所有投影片的大小是否相同。</p> </td>
   <td><p>僅對轉盤使用相同大小的影像。</p> </td>
  </tr>
  <tr>
   <td>影像不會使用Dynamic Media檢視器預覽</td>
   <td><p>在中繼資料屬性(CRXDE Lite)中檢查資產是否包含<code>dam:scene7File</code></p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>已上傳的資產不會顯示在資產選擇器中</td>
   <td><p>Check Asset has property <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code>(CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>卡片檢視上的橫幅會顯示資產尚未開始處理時的<strong>New</strong></td>
   <td>檢查<code>jcr:content</code> &gt; <code>dam:assetState</code> =如果<code>unprocessed</code>未被工作流挑選。</td>
   <td>等待工作流程擷取資產。</td>
  </tr>
  <tr>
   <td>影像或影像集不會顯示檢視器URL或內嵌代碼</td>
   <td>檢查檢視器預設集是否已發佈。</td>
   <td><p>前往「<strong>工具</strong> &gt; <strong>資產</strong> &gt; <strong>檢視器預設集</strong>」並發佈檢視器預設集。</p> </td>
  </tr>
 </tbody>
</table>

## 影片 {#video}

如果您對視訊有任何問題，請參閱下列疑難排解指引。

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
     <li>檢查資料夾是否已指派視訊描述檔（如果不支援檔案格式）。 如果不支援，則只會顯示影像。</li>
     <li>視訊設定檔必須包含多個編碼預設集，才能產生AVS集(單一編碼視為MP4檔案的視訊內容；對於不支援的檔案，會視為與未處理的檔案相同)。</li>
     <li>確認中繼資料中<code>dam:scene7File</code>的<code>dam:scene7FileAvs</code>，檢查視訊是否已完成處理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊描述檔指派給資料夾。</li>
     <li>編輯視訊設定檔以包含多個編碼預設集。</li>
     <li>等待視訊完成處理。</li>
     <li>在重新載入視訊之前，請確定Dynamic Media編碼視訊工作流程未執行。<br/> </li>
     <li>重新上傳影片。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊未編碼</td>
   <td>
    <ul>
     <li>檢查是否配置了Dynamic MediaCloud Service。</li>
     <li>檢查視訊描述檔是否與上傳資料夾相關聯。</li>
    </ul> </td>
   <td>
    <ol>
     <li>檢查Cloud Services下的「Dynamic Media配置」是否已正確設定。</li>
     <li>檢查資料夾是否有視訊描述檔。 此外，檢查視訊設定檔。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊處理需要太長時間</td>
   <td><p>若要判斷視訊編碼是否仍在進行中，或已進入失敗狀態：</p>
    <ul>
     <li>檢查視頻狀態<code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>影片轉譯遺失</td>
   <td><p>上傳視訊時，但沒有編碼轉譯：</p>
    <ul>
     <li>檢查資料夾是否已指派視訊描述檔。</li>
     <li>確認中繼資料中的<code>dam:scene7FileAvs</code>，檢查視訊是否已完成處理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊描述檔指派給資料夾。</li>
     <li>等待視頻完成處理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 檢視器 {#viewers}

如果您對檢視器有任何問題，請參閱下列疑難排解指引。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何除錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>檢視器預設集未發佈</td>
   <td><p>繼續到示例管理器診斷頁： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>觀察計算值。 當正確運作時，您會看到：</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注意</strong>:設定檢視器資產的Dynamic Media雲端設定進行同步後，大約需要10分鐘。</p> <p>如果未啟動的資產仍保留，請按一下<strong>列出所有未啟動的資產</strong>按鈕以檢視詳細資訊。</p> </td>
   <td>
    <ol>
     <li>導覽至管理工具中的檢視器預設集清單： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>選取所有檢視器預設集，然後按一下「發佈」。<strong></strong></li>
     <li>返回範例管理員，並觀察未啟動的資產計數現在為零。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>檢視器預設集圖稿會從資產詳細資料的預覽或複製URL/內嵌代碼傳回404</td>
   <td><p>在CRXDE Lite語中，請執行下列操作：</p>
    <ol>
     <li>導覽至您的Dynamic Media同步資料夾內的<code>&lt;sync-folder&gt;/_CSS/_OOTB</code>資料夾（例如<code>/content/dam/_CSS/_OOTB</code>）,</li>
     <li>尋找有問題資產的中繼資料節點（例如<code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>）。</li>
     <li>檢查是否存在<code>dam:scene7*</code>屬性。 如果資產已成功同步並發佈，您會看到<code>dam:scene7FileStatus</code>設定為<strong>PublishComplete</strong>。</li>
     <li>嘗試串連下列屬性和字串文字的值，直接從Dynamic Media要求圖稿
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>範例: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>如果範例資產或檢視器預設圖稿尚未同步或發佈，請重新啟動整個複製／同步程式：</p>
    <ol>
     <li>導航到 <code>/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code>
     </li>
     <li>按順序選擇以下操作：
      <ol>
       <li>刪除同步資料夾。</li>
       <li>刪除預設集資料夾（<code>/conf</code>下方）。
       <li>觸發DM設定非同步作業。</li>
      </ol> </li>
     <li>等待Experience Manager收件箱中成功同步的通知。
     </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
