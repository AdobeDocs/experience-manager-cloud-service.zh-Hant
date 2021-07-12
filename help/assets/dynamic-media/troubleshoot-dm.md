---
title: Dynamic Media 疑難排解
description: 使用Dynamic Media時的疑難排解提示。
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 1%

---

# Dynamic Media 疑難排解 {#troubleshooting-dynamic-media-scene-mode}

以下主題說明Dynamic Media的疑難排解。

## 新Dynamic Media設定 {#new-dm-config}

請參閱[疑難排解新的Dynamic Media設定](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config)。

## 一般（所有資產） {#general-all-assets}

以下是所有資產的一些一般提示和秘訣。

### 資產同步狀態屬性 {#asset-synchronization-status-properties}

您可以在CRXDE Lite中檢閱下列資產屬性，以確認資產是否成功從Adobe Experience Manager同步至Dynamic Media:

| **屬性** | **範例** | **說明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 節點連結至Dynamic Media的一般指標。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **** PublishCompleteor錯誤文字 | 資產上傳至Dynamic Media的狀態。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必須填入，才能產生URL至Dynamic Media的遠端資產。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **** 後繼 **失敗：`<error text>`** | 集（回轉集、影像集等）、影像預設集、檢視器預設集、資產的影像地圖更新或已編輯影像的同步狀態。 |

### 同步記錄 {#synchronization-logging}

同步錯誤和問題記錄在`error.log`(Experience Manager伺服器目錄`/crx-quickstart/logs/`)中。 有足夠的記錄可供判斷大部分問題的根本原因，但您可以透過Sling主控台([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))增加`com.adobe.cq.dam.ips`套件上的DEBUG記錄，以收集詳細資訊。

### 版本控制 {#version-control}

取代現有的Dynamic Media資產（相同名稱和位置）時，您可以保留兩個資產或取代/建立版本：

* 同時保留會為已發佈的資產URL建立一個唯一名稱的資產。 例如， `image.jpg`是原始資產，而`image1.jpg`是新上傳的資產。

* Dynamic Media不支援建立版本。 新版本會取代傳送中的現有資產。

## 影像和集 {#images-and-sets}

如果您對影像和集有問題，請參閱下列疑難排解指南。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何偵錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法存取資產詳細資料檢視中的複製URL/內嵌按鈕</td>
   <td>
    <ol>
     <li><p>前往CRX/DE:</p>
      <ul>
       <li>檢查JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code>中是否已定義預設集。 如果您從Experience Manager6.x升級至6.4，並選擇退出移轉，則此位置適用。 否則，位置為<code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>檢查以確定JCR中的資產在「中繼資料顯示為<code>PublishComplete</code>」下有<code>dam:scene7FileStatus</code><strong> </strong>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>重新整理頁面/導覽至其他頁面並返回（必須重新編譯側欄JSP）</p> <p>如果沒有用：</p>
    <ul>
     <li>發佈資產。</li>
     <li>重新上傳資產並發佈。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>切換投影片後，輪播熱點會四處移動</td>
   <td><p>檢查所有幻燈片的大小是否相同。</p> </td>
   <td><p>僅對輪播使用大小相同的影像。</p> </td>
  </tr>
  <tr>
   <td>影像未以Dynamic Media檢視器預覽</td>
   <td><p>檢查中繼資料屬性(CRXDE Lite)中的資產是否包含<code>dam:scene7File</code></p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>上傳的資產不會顯示在資產選取器中</td>
   <td><p>檢查資產的屬性<code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code>(CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>當資產尚未開始處理時，卡片檢視上的橫幅會顯示<strong>新增</strong></td>
   <td>檢查工作流程未擷取的資產<code>jcr:content</code> &gt; <code>dam:assetState</code> = <code>unprocessed</code>。</td>
   <td>等待工作流程擷取資產。</td>
  </tr>
  <tr>
   <td>影像或集不會顯示檢視器URL或內嵌程式碼</td>
   <td>檢查檢視器預設集是否已發佈。</td>
   <td><p>前往「<strong>工具</strong> &gt; <strong>資產</strong> &gt; <strong>檢視器預設集</strong>」並發佈檢視器預設集。</p> </td>
  </tr>
 </tbody>
</table>

## 影片 {#video}

如果您對視訊有問題，請參閱下列疑難排解指引。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何偵錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法預覽視訊</td>
   <td>
    <ul>
     <li>檢查資料夾是否已指派視訊描述檔（如果不支援檔案格式）。 如果不支援，則只會顯示影像。</li>
     <li>視頻配置檔案必須包含多個編碼預設集才能生成AVS集(單個編碼被視為MP4檔案的視頻內容；對於不支援的檔案，則視為與未處理的檔案相同)。</li>
     <li>確認中繼資料中<code>dam:scene7File</code>的<code>dam:scene7FileAvs</code>，以檢查視訊是否已完成處理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊描述檔指派給資料夾。</li>
     <li>編輯視訊設定檔以包含多個編碼預設集。</li>
     <li>等待視頻完成處理。</li>
     <li>重新載入視訊之前，請確定Dynamic Media編碼視訊工作流程未執行。<br/> </li>
     <li>重新上傳影片。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊未編碼</td>
   <td>
    <ul>
     <li>檢查是否已設定Dynamic MediaCloud Service。</li>
     <li>檢查視訊設定檔是否與上傳資料夾相關聯。</li>
    </ul> </td>
   <td>
    <ol>
     <li>檢查「Cloud Services」下的Dynamic Media設定是否已正確設定。</li>
     <li>檢查資料夾是否有視訊設定檔。 此外，檢查視訊設定檔。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊處理需要太長時間</td>
   <td><p>要確定視頻編碼是否仍在進行中，或是否已進入故障狀態：</p>
    <ul>
     <li>檢查視訊狀態<code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>視訊轉譯遺失</td>
   <td><p>上傳視訊時，但沒有編碼的轉譯：</p>
    <ul>
     <li>檢查資料夾是否已指派視訊設定檔。</li>
     <li>確認中繼資料中的<code>dam:scene7FileAvs</code>以檢查視訊已完成處理。</li>
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

如果您在檢視器上有問題，請參閱下列疑難排解指南。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何偵錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>未發佈查看器預設集</td>
   <td><p>繼續到示例管理器診斷頁： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>觀察計算值。 正確運作時，您會看到：</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注意</strong>:配置檢視器資產的Dynamic Media雲端設定後，可能需要約10分鐘的時間才能同步。</p> <p>如果未啟動的資產仍保留，請按一下<strong>列出所有未啟動的資產</strong>按鈕以查看詳細資訊。</p> </td>
   <td>
    <ol>
     <li>導覽至管理工具中的檢視器預設集清單： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>選取所有檢視器預設集，然後按一下「<strong>發佈</strong>」。</li>
     <li>導覽回範例管理員，並觀察未啟動的資產計數現在為零。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>檢視器預設集圖稿會從資產詳細資料中的預覽或複製URL/內嵌程式碼中傳回404</td>
   <td><p>在CRXDE Lite中執行下列操作：</p>
    <ol>
     <li>導覽至Dynamic Media同步資料夾內的<code>&lt;sync-folder&gt;/_CSS/_OOTB</code>資料夾（例如<code>/content/dam/_CSS/_OOTB</code>）,</li>
     <li>尋找有問題資產的中繼資料節點（例如<code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>）。</li>
     <li>檢查是否存在<code>dam:scene7*</code>屬性。 如果資產已成功同步和發佈，您會看到<code>dam:scene7FileStatus</code>集設為<strong>PublishComplete</strong>。</li>
     <li>嘗試串連下列屬性和字串文字的值，以直接從Dynamic Media請求圖稿
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>範例: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>如果範例資產或檢視器預設集圖稿尚未同步或發佈，請重新啟動整個複製/同步程式：</p>
    <ol>
     <li>導航到 <code>/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code>
     </li>
     <li>依順序選取下列動作：
      <ol>
       <li>刪除同步資料夾。</li>
       <li>刪除預設資料夾（<code>/conf</code>下）。
       <li>觸發DM設定非同步作業。</li>
      </ol> </li>
     <li>等待Experience Manager收件匣中同步成功的通知。
     </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
