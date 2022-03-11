---
title: 排除Dynamic Media故障
description: 使用Dynamic Media時的故障排除技巧。
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 1%

---

# 排除Dynamic Media故障 {#troubleshooting-dynamic-media-scene-mode}

以下主題介紹Dynamic Media的故障排除。

## 新Dynamic Media配置 {#new-dm-config}

請參閱 [排除新Dynamic Media配置的故障](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config)。

## 常規（所有資產） {#general-all-assets}

以下是所有資產的一些一般提示和技巧。

### 資產同步狀態屬性 {#asset-synchronization-status-properties}

可以CRXDE Lite查看以下資產屬性，以確認資產從Adobe Experience Manager到Dynamic Media的成功同步：

| **屬性** | **範例** | **說明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 節點連結到Dynamic Media的一般指示。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **發佈完成** 錯誤文本 | 資產上載到Dynamic Media的狀態。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必須填充以生成Dynamic Media遠程資產的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **成功** 或 **失敗：`<error text>`** | 集（旋轉集、影像集等）、影像預設、查看器預設、資產的影像映射更新或已編輯的影像的同步狀態。 |

### 同步記錄 {#synchronization-logging}

同步錯誤和問題已登錄 `error.log` (Experience Manager伺服器目錄) `/crx-quickstart/logs/`)。 可以使用足夠的日誌記錄來確定大多數問題的根本原因，但您可以將日誌記錄增加到 `com.adobe.cq.dam.ips` 通過Sling控制台進行打包([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))以收集更多資訊。

### 版本控制 {#version-control}

替換現有Dynamic Media資產（同名和地點）時，您可以保留兩個資產或替換/建立版本：

* 保留兩者都會為已發佈資產URL建立具有唯一名稱的資產。 比如說， `image.jpg` 是原始資產 `image1.jpg` 是新上載的資產。

* Dynamic Media不支援建立版本。 新版本將替換交付中的現有資產。

## 影像和集 {#images-and-sets}

如果您對映像和集有問題，請參閱以下故障排除指導。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何調試</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法訪問資產詳細資訊視圖中的複製URL/嵌入按鈕</td>
   <td>
    <ol>
     <li><p>轉至CRX/DE:</p>
      <ul>
       <li>檢查JCR中是否有預設 <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> 定義。 如果您從Experience Manager6.x升級到6.4並選擇退出遷移，則此位置適用。 否則，位置 <code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>檢查以確保JCR中的資產 <code>dam:scene7FileStatus</code><strong> </strong>在元資料下顯示為 <code>PublishComplete</code>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>刷新頁面/導航到另一頁並返回（必須重新編譯側軌JSP）</p> <p>如果這行不通：</p>
    <ul>
     <li>發佈資產。</li>
     <li>重新上載資產並發佈。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>在幻燈片之間切換後，旋轉木馬熱點會移動</td>
   <td><p>檢查所有幻燈片的大小是否相同。</p> </td>
   <td><p>僅對旋轉木馬使用大小相同的影像。</p> </td>
  </tr>
  <tr>
   <td>影像不與Dynamic Media查看器預覽</td>
   <td><p>檢查資產是否包含 <code>dam:scene7File</code> 元資料屬性(CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>上載的資產不顯示在資產選擇器中</td>
   <td><p>檢查資產具有屬性 <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>卡上的橫幅顯示 <strong>新建</strong> 當資產未開始處理時</td>
   <td>檢查資產 <code>jcr:content</code> &gt; <code>dam:assetState</code> =if <code>unprocessed</code> 工作流沒有採集。</td>
   <td>等待工作流提取資產。</td>
  </tr>
  <tr>
   <td>影像或集不顯示查看器URL或嵌入代碼</td>
   <td>檢查查看器預設是否已發佈。</td>
   <td><p>轉到 <strong>工具</strong> &gt; <strong>資產</strong> &gt; <strong>查看器預設</strong> 並發佈查看器預設。</p> </td>
  </tr>
 </tbody>
</table>

## 影片 {#video}

如果您對視頻有問題，請參閱以下故障排除指導。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何調試</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法預覽視頻</td>
   <td>
    <ul>
     <li>檢查資料夾是否已為其分配視頻配置檔案（如果不支援檔案格式）。 如果不支援，則只顯示影像。</li>
     <li>視頻配置檔案必須包含多個編碼預設以生成AVS集(單個編碼被視為MP4檔案的視頻內容；對於不支援的檔案，與未處理檔案相同)。</li>
     <li>通過確認 <code>dam:scene7FileAvs</code> 共 <code>dam:scene7File</code> 元資料。</li>
    </ul> </td>
   <td>
    <ol>
     <li>為資料夾分配視頻配置檔案。</li>
     <li>編輯視頻配置檔案以包括多個編碼預設。</li>
     <li>等待視頻完成處理。</li>
     <li>重新載入視頻之前，請確保Dynamic Media編碼視頻工作流未運行。<br/> </li>
     <li>重新上載視頻。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視頻未編碼</td>
   <td>
    <ul>
     <li>檢查是否配置了Dynamic MediaCloud Service。</li>
     <li>檢查視頻配置檔案是否與上載資料夾關聯。</li>
    </ul> </td>
   <td>
    <ol>
     <li>檢查Cloud Services下的Dynamic Media配置是否已正確設定。</li>
     <li>檢查資料夾是否具有視頻配置檔案。 另外，檢查視頻配置檔案。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視頻處理耗時太長</td>
   <td><p>要確定視頻編碼是否仍在進行中或是否已進入失敗狀態：</p>
    <ul>
     <li>檢查視頻狀態 <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>缺少視頻格式副本</td>
   <td><p>上載視頻時，但沒有編碼格式副本：</p>
    <ul>
     <li>檢查資料夾是否已分配視頻配置檔案。</li>
     <li>通過確認 <code>dam:scene7FileAvs</code> 元資料。</li>
    </ul> </td>
   <td>
    <ol>
     <li>為資料夾分配視頻配置檔案。</li>
     <li>等待視頻完成處理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 檢視器 {#viewers}

如果與查看者有問題，請參閱以下故障排除指南。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何調試</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>未發佈查看器預設</td>
   <td><p>繼續到示例管理器診斷頁： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>觀察計算值。 正確操作時，您會看到：</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注釋</strong>:配置查看器資產的Dynamic Media雲設定後，可能需要大約10分鐘才能同步。</p> <p>如果未激活的資產仍然存在，請選擇 <strong>列出所有未激活的資產</strong> 按鈕以查看詳細資訊。</p> </td>
   <td>
    <ol>
     <li>導航到管理工具中的查看器預設清單： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>選擇所有查看器預設，然後選擇 <strong>發佈</strong>。</li>
     <li>返回至示例經理，並觀察未激活的資產計數現在為零。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>查看器預設圖稿從資產詳細資訊或複製URL/嵌入代碼中的預覽返回404</td>
   <td><p>在CRXDE Lite中，執行以下操作：</p>
    <ol>
     <li>導航到 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> 資料夾(例如， <code>/content/dam/_CSS/_OOTB</code>)</li>
     <li>查找有問題資產的元資料節點(例如， <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>)。</li>
     <li>檢查是否存在 <code>dam:scene7*</code> 屬性。 如果資產已成功同步並發佈，您將看到 <code>dam:scene7FileStatus</code> 設定為 <strong>發佈完成</strong>。</li>
     <li>嘗試通過連接以下屬性和字串文本的值來直接從Dynamic Media請求圖稿
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>範例: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>如果示例資產或查看器預設圖稿尚未同步或發佈，請重新啟動整個複製/同步過程：</p>
    <ol>
     <li>導航到 <code>/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code>
     </li>
     <li>按順序選擇以下操作：
      <ol>
       <li>刪除同步資料夾。</li>
       <li>刪除預設資料夾（下） <code>/conf</code>)。
       <li>觸發DM安裝非同步作業。</li>
      </ol> </li>
     <li>等待Experience Manager收件箱中同步成功的通知。
     </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
