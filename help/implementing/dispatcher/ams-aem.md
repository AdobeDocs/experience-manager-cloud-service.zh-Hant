---
title: 將Dispatcher設定從AMS移轉至AEMas a Cloud Service
description: 將Dispatcher設定從AMS移轉至AEMas a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 14%

---

# 將Dispatcher設定從AMS移轉至AEMas a Cloud Service {#Dispatcher-in-the-cloud}

## AMS Dispatcher與AEM as a Cloud Service的主要差異 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEMas a Cloud Service中的Apache和Dispatcher設定與AMS 1相當類似。 主要差異為：

* 在AEMas a Cloud Service中，某些Apache指令可能無法使用(例如 `Listen` 或 `LogLevel`)
* 在AEMas a Cloud Service中，只有Dispatcher設定的某些片段可放入包含檔案中，而且其命名很重要。 例如，您必須將要在不同主機間重複使用的篩選規則放入名為 `filters/filters.any`. 如需詳細資訊，請參閱參考頁面。
* 在AEM中，有額外驗證可禁止使用 `/glob` 來防止安全問題。 自 `deny *` 會使用，而非 `allow *` （無法使用），客戶將能從在本機執行Dispatcher以及執行試用和錯誤、查看記錄檔中確切知道Dispatcher篩選器要封鎖哪些路徑，以便新增這些路徑而獲益。

## 將Dispatcher設定從AMS移轉至AEMas a Cloud Service的准則

Managed Services和AEMas a Cloud Service之間的Dispatcher設定結構有差異。 以下提供逐步指南，說明如何從AMS Dispatcher設定第2版移轉至AEMas a Cloud Service。

## 如何將AMS轉換為AEM as a Cloud service Dispatcher設定

以下章節提供如何轉換AMS設定的逐步指示。 此處假設您有一個封存，其結構類似於 [Cloud Manager Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### 提取封存並移除最終首碼

將封存解壓縮至資料夾，並確認直接子資料夾的開頭為 `conf`, `conf.d`,
`conf.dispatcher.d` 和 `conf.modules.d`. 如果沒有，請在階層中向上移動。

### 移除未使用的子資料夾和檔案

移除子資料夾 `conf` 和 `conf.modules.d`，以及檔案比對 `conf.d/*.conf`.

### 移除所有非發佈用的虛擬主機

移除 `conf.d/enabled_vhosts` thas `author`, `unhealthy`, `health`,
`lc` 或 `flush` 以其名義。 中的所有虛擬主機檔案 `conf.d/available_vhosts` 也可移除未連結的項目。

### 移除或註解未引用連接埠 80 的虛擬主機區段

如果您的虛擬主機檔案中仍有區段專門引用埠80以外的其他埠，例如：

```
<VirtualHost *:443>
...
</VirtualHost>
```


請移除或加上註解。系統將不會處理這些區段中的陳述式，但如果您保留這些陳述式，您最終可能仍會編輯，但將徒勞無功而倍感困惑。

### 檢查重新寫入

輸入目錄 `conf.d/rewrites`.

移除任何名為 `base_rewrite.rules` 和 `xforwarded_forcessl_rewrite.rules` 記得移除 `Include` 在虛擬主機檔案中引用語句。

若 `conf.d/rewrites` 現在包含單一檔案，則應將其重新命名為 `rewrite.rules` 別忘了調整 `Include` 在虛擬主機檔案中引用該檔案的語句。

但是，如果資料夾包含多個虛擬主機專用檔案，則其內容應複製到 `Include` 在虛擬主機檔案中引用它們的語句。

### 檢查變數

輸入目錄 `conf.d/variables`.

移除任何名為 `ams_default.vars` 記得移除 `Include` 在虛擬主機檔案中引用語句。

若 `conf.d/variables` 現在包含單一檔案，則應將其重新命名為 `custom.vars` 別忘了調整 `Include` 在虛擬主機檔案中引用該檔案的語句。

但是，如果資料夾包含多個虛擬主機專用檔案，則其內容應複製到 `Include` 在虛擬主機檔案中引用它們的語句。

### 移除允許清單

移除資料夾 `conf.d/whitelists` 移除 `Include` 虛擬主機檔案中引用該子資料夾中某個檔案的語句。

### 取代任何已無法使用的變數

在所有虛擬主機檔案中：

重新命名 `PUBLISH_DOCROOT` to `DOCROOT`
移除引用以下變數的區段： `DISP_ID`, `PUBLISH_FORCE_SSL` 或 `PUBLISH_WHITELIST_ENABLED`

### 執行驗證器以檢查狀態

在您的目錄中，使用 `httpd` 子命令：

```
$ validator httpd .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看到未列入允許清單的Apache指示，請將其移除。

### 移除所有非發佈用的伺服器陣列

移除 `conf.dispatcher.d/enabled_farms` thas `author`, `unhealthy`, `health`,
`lc` 或 `flush` 以其名義。 中的所有伺服器陣列檔案 `conf.dispatcher.d/available_farms` 也可移除未連結的項目。

### 重新命名伺服器陣列檔案

所有農場 `conf.d/enabled_farms` 必須重新命名以符合模式 `*.farm`，例如，伺服器陣列檔案，稱為 `customerX_farm.any` 應重新命名 `customerX.farm`.

### 檢查快取

輸入目錄 `conf.dispatcher.d/cache`.

移除任何以「`ams_`」為首碼的檔案。

若 `conf.dispatcher.d/cache` 現在空白，請複製檔案 `conf.dispatcher.d/cache/rules.any`
從標準Dispatcher設定傳送至此資料夾。 您可以在資料夾中找到標準Dispatcher設定 `src` 的SDK。 別忘了調整
`$include` 引用 `ams_*_cache.any` 規則檔案。

若 `conf.dispatcher.d/cache` 現在包含尾碼為的單一檔案 `_cache.any`，則應重新命名為 `rules.any` 別忘了調整 `$include` 在伺服器陣列檔案中引用該檔案的語句。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容應複製到 `$include` 在伺服器陣列檔案中引用這些檔案的語句。

移除任何尾碼為的檔案 `_invalidate_allowed.any`.

複製檔案 `conf.dispatcher.d/cache/default_invalidate_any` 從雲端Dispatcher設定中的預設AEM到該位置。

在每個伺服器陣列檔案中，移除 `cache/allowedClients` 部分，替換為：

```
$include "../cache/default_invalidate.any"
```

### 檢查用戶端標頭

輸入目錄 `conf.dispatcher.d/clientheaders`.

移除任何以「`ams_`」為首碼的檔案。

若 `conf.dispatcher.d/clientheaders` 現在包含尾碼為的單一檔案 `_clientheaders.any`，則應重新命名為 `clientheaders.any` 別忘了調整 `$include` 在伺服器陣列檔案中引用該檔案的語句。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容應複製到 `$include` 在伺服器陣列檔案中引用這些檔案的語句。

複製檔案 `conf.dispatcher/clientheaders/default_clientheaders.any` 從預設的AEMas a Cloud ServiceDispatcher設定到該位置。

在每個伺服器陣列檔案中，取代任何如下所示的clientheader include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

以及以下陳述式：

```
$include "../clientheaders/default_clientheaders.any"
```

### 檢查篩選器

輸入目錄 `conf.dispatcher.d/filters`.

移除任何以「`ams_`」為首碼的檔案。

若 `conf.dispatcher.d/filters` 現在包含單一檔案，應將其重新命名為
`filters.any` 別忘了調整 `$include` 在伺服器陣列檔案中引用該檔案的語句。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容應複製到 `$include` 在伺服器陣列檔案中引用這些檔案的語句。

複製檔案 `conf.dispatcher/filters/default_filters.any` 從預設的AEMas a Cloud ServiceDispatcher設定到該位置。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

以及以下陳述式：

```
$include "../filters/default_filters.any"
```

### 檢查轉譯

輸入目錄 `conf.dispatcher.d/renders`.

移除該資料夾中的所有檔案。

複製檔案 `conf.dispatcher.d/renders/default_renders.any` 從預設的AEMas a Cloud ServiceDispatcher設定到該位置。

在每個伺服器陣列檔案中，移除 `renders` 部分，替換為：

```
$include "../renders/default_renders.any"
```

### 檢查虛擬主機

更名目錄 `conf.dispatcher.d/vhosts` to `conf.dispatcher.d/virtualhosts` 然後輸入。

移除任何以「`ams_`」為首碼的檔案。

若 `conf.dispatcher.d/virtualhosts` 現在包含單一檔案，應將其重新命名為
`virtualhosts.any` 別忘了調整 `$include` 在伺服器陣列檔案中引用該檔案的語句。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容應複製到 `$include` 在伺服器陣列檔案中引用這些檔案的語句。

複製檔案 `conf.dispatcher/virtualhosts/default_virtualhosts.any` 從預設的AEMas a Cloud ServiceDispatcher設定到該位置。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

以及以下陳述式：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 執行驗證器以檢查狀態

在您的目錄中，使用 `dispatcher` 子命令：

```
$ validator dispatcher .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看見有關未定義變數「`PUBLISH_DOCROOT`」的錯誤，請將其重新命名為「`DOCROOT`」。

如果看見其他錯誤，請參考驗證器工具文件的疑難排解章節。

### 使用本機部署測試配置（需要安裝Docker）

使用指令碼 `docker_run.sh` 在AEMas a Cloud ServiceDispatcher工具中，您可以測試您的設定是否不包含任何僅顯示在部署中的其他錯誤：

### 步驟1:使用驗證器產生部署資訊

```
validator full -d out .
```

如此可驗證完整設定，並在中產生部署資訊 `out`

### 步驟2:使用該部署資訊在Docker映像中啟動Dispatcher

在macOS電腦上執行AEM發佈伺服器，並在連接埠4503上接聽後，您就可以在該伺服器前面執行Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

如此一來將啟動容器，並在本機連接埠 8080 上公開 Apache。

### 使用您的新Dispatcher設定

恭喜！ 如果驗證器不再回報任何問題，且Docker容器啟動時未出現任何失敗情況或警告，即可將您的設定移至 `dispatcher/src` 的子目錄。

**使用AMS Dispatcher設定1版的客戶應聯絡客戶支援，協助他們從第1版移轉至第2版，以便遵循上述指示。**
