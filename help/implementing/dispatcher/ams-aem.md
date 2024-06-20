---
title: 將 Dispatcher 設定從 AMS 移轉到 AEM as a Cloud Service
description: 將 Dispatcher 設定從 AMS 移轉到 AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 7%

---

# 將 Dispatcher 設定從 AMS 移轉到 AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## AMS Dispatcher與AEMas a Cloud Service之間的主要差異 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEMas a Cloud Service中的Apache和Dispatcher設定相當類似於AMS。 主要差異如下：

* 在AEMas a Cloud Service中，可能不使用某些Apache指示詞(例如 `Listen` 或 `LogLevel`)
* 在AEMas a Cloud Service中，只能將Dispatcher設定的某些片段放入包含檔案中，其命名很重要。 例如，您要跨不同主機重複使用的篩選規則必須放在名為的檔案中 `filters/filters.any`. 如需詳細資訊，請參閱參考頁面。
* AEMas a Cloud Service中有額外的驗證，不允許使用撰寫篩選規則 `/glob` 以防止安全性問題。 因為 `deny *` 已使用，而非 `allow *` （無法使用），客戶受益於在本機執行Dispatcher並進行測試和錯誤，檢視記錄以準確瞭解Dispatcher篩選器阻止了哪些路徑以便可以新增。
* 在AEMas a Cloud Service中，目前強烈建議 [選擇加入以使用Dispatcher設定的靈活來源模式](/help/implementing/dispatcher/disp-overview.md#validation-debug) 例如使用Web層設定管道，或在設定檔案的數量和結構上有更好的彈性。

## 將Dispatcher設定從AMS移轉至AEMas a Cloud Service的准則

Managed Services和AEMas a Cloud Service中的Dispatcher設定結構有所差異。 以下提供的逐步指南會說明如何從AMS Dispatcher設定版本2移轉至AEMas a Cloud Service。

## 如何將AMS轉換為AEM as a Cloud Service Dispatcher設定

以下章節提供如何轉換AMS設定的逐步指示。 此工具假設您有一個封存，其結構與中所述的結構類似 [Cloud Manager Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### 提取封存並移除最終首碼

將封存提取至資料夾，並確定直接子資料夾的開頭為 `conf`， `conf.d`，
`conf.dispatcher.d` 和 `conf.modules.d`. 如果沒有，請在階層中向上移動它們。

### 移除未使用的子資料夾和檔案

移除子資料夾 `conf` 和 `conf.modules.d`和檔案比對 `conf.d/*.conf`.

### 移除所有非發佈用的虛擬主機

移除中的任何虛擬主機檔案 `conf.d/enabled_vhosts` 具有 `author`， `unhealthy`， `health`，
`lc` 或 `flush` 在其名稱中。 所有虛擬主機檔案 `conf.d/available_vhosts` 您也可以移除未連結的。

### 移除或註解未引用連接埠 80 的虛擬主機區段

例如，如果您的虛擬主機檔案中仍有區段專門引用連線埠80以外的連線埠：

```
<VirtualHost *:443>
...
</VirtualHost>
```

請移除或加上註解。 系統將不會處理這些區段中的陳述式，但如果您保留這些陳述式，您最終可能仍會編輯它們，但將徒勞無功而倍感困惑。

### 檢查重新寫入

輸入目錄 `conf.d/rewrites`.

移除任何名為的檔案 `base_rewrite.rules` 和 `xforwarded_forcessl_rewrite.rules` 並記得要移除 `Include` 虛擬主機檔案中引用這些陳述式的陳述式。

如果 `conf.d/rewrites` 現在包含單一檔案，應將其重新命名為 `rewrite.rules` 還有，別忘了改寫 `Include` 陳述式也在虛擬主機檔案中引用該檔案。

然而，如果該資料夾包含多個虛擬主機專屬檔案，則應將其內容複製到 `Include` 在虛擬主機檔案中引用它們的陳述式。

### 檢查變數

輸入目錄 `conf.d/variables`.

移除任何名為的檔案 `ams_default.vars` 並記得要移除 `Include` 虛擬主機檔案中引用這些陳述式的陳述式。

如果 `conf.d/variables` 現在包含單一檔案，應將其重新命名為 `custom.vars` 還有，別忘了改寫 `Include` 陳述式也在虛擬主機檔案中引用該檔案。

然而，如果該資料夾包含多個虛擬主機專屬檔案，則應將其內容複製到 `Include` 在虛擬主機檔案中引用它們的陳述式。

### 移除允許清單

移除資料夾 `conf.d/whitelists` 並移除 `Include` 虛擬主機檔案中參照該子資料夾中某個檔案的陳述式。

### 取代任何已無法使用的變數

在所有虛擬主機檔案中：

重新命名 `PUBLISH_DOCROOT` 至 `DOCROOT`
移除引用下列變數的章節： `DISP_ID`， `PUBLISH_FORCE_SSL` 或 `PUBLISH_WHITELIST_ENABLED`

### 執行驗證器以檢查狀態

使用在您的目錄中執行Dispatcher驗證器 `httpd` 子命令：

```
$ validator httpd .
```

如果您看見有關遺失Include檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看到未加入允許清單的Apache指示詞，請將其移除。

### 移除所有非發佈用的伺服器陣列

移除中的任何伺服器陣列檔案 `conf.dispatcher.d/enabled_farms` 具有 `author`， `unhealthy`， `health`，
`lc` 或 `flush` 在其名稱中。 中的所有伺服器陣列檔案 `conf.dispatcher.d/available_farms` 您也可以移除未連結的。

### 重新命名伺服器陣列檔案

中的所有陣列 `conf.dispatcher.d/enabled_farms` 必須重新命名以符合模式 `*.farm`，例如，名為的伺服器陣列檔案 `customerX_farm.any` 應重新命名 `customerX.farm`.

### 檢查快取

輸入目錄 `conf.dispatcher.d/cache`.

移除任何以「`ams_`」為首碼的檔案。

如果 `conf.dispatcher.d/cache` 現在為空，請複製檔案 `conf.dispatcher.d/cache/rules.any`
從標準Dispatcher設定移至此資料夾。 您可以在資料夾中找到標準Dispatcher設定 `src` 此SDK的。 別忘了改寫
`$include` 陳述式指的是 `ams_*_cache.any` 伺服器陣列檔案中的規則檔案。

若改用 `conf.dispatcher.d/cache` 現在包含含有尾碼的單一檔案 `_cache.any`，應重新命名為 `rules.any` 還有，別忘了改寫 `$include` 在伺服器陣列檔案中引用該檔案的陳述式。

然而，如果資料夾包含多個使用該模式的伺服器陣列特定檔案，則應將其內容複製到 `$include` 在伺服器陣列檔案中引用它們的陳述式。

移除任何尾碼的檔案 `_invalidate_allowed.any`.

複製檔案 `conf.dispatcher.d/cache/default_invalidate_any` 從雲端Dispatcher設定中的預設AEM移至該位置。

在每個伺服器陣列檔案中，移除 `cache/allowedClients` 區段並取代為：

```
$include "../cache/default_invalidate.any"
```

### 檢查使用者端標頭

輸入目錄 `conf.dispatcher.d/clientheaders`.

移除任何以「`ams_`」為首碼的檔案。

如果 `conf.dispatcher.d/clientheaders` 現在包含含有尾碼的單一檔案 `_clientheaders.any`，應重新命名為 `clientheaders.any` 還有，別忘了改寫 `$include` 在伺服器陣列檔案中引用該檔案的陳述式。

然而，如果資料夾包含多個使用該模式的伺服器陣列特定檔案，則應將其內容複製到 `$include` 在伺服器陣列檔案中引用它們的陳述式。

複製檔案 `conf.dispatcher/clientheaders/default_clientheaders.any` 從預設的AEMas a Cloud ServiceDispatcher設定恢復到該位置。

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

如果 `conf.dispatcher.d/filters` 現在包含單一檔案，應將其重新命名為
`filters.any` 還有，別忘了改寫 `$include` 在伺服器陣列檔案中引用該檔案的陳述式。

然而，如果資料夾包含多個使用該模式的伺服器陣列特定檔案，則應將其內容複製到 `$include` 在伺服器陣列檔案中引用它們的陳述式。

複製檔案 `conf.dispatcher/filters/default_filters.any` 從預設的AEMas a Cloud ServiceDispatcher設定恢復到該位置。

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

複製檔案 `conf.dispatcher.d/renders/default_renders.any` 從預設的AEMas a Cloud ServiceDispatcher設定恢復到該位置。

在每個伺服器陣列檔案中，移除 `renders` 區段並取代為：

```
$include "../renders/default_renders.any"
```

### 檢查虛擬主機

重新命名目錄 `conf.dispatcher.d/vhosts` 至 `conf.dispatcher.d/virtualhosts` 並輸入。

移除任何以「`ams_`」為首碼的檔案。

如果 `conf.dispatcher.d/virtualhosts` 現在包含單一檔案，應將其重新命名為
`virtualhosts.any` 還有，別忘了改寫 `$include` 在伺服器陣列檔案中引用該檔案的陳述式。

然而，如果資料夾包含多個使用該模式的伺服器陣列特定檔案，則應將其內容複製到 `$include` 在伺服器陣列檔案中引用它們的陳述式。

複製檔案 `conf.dispatcher/virtualhosts/default_virtualhosts.any` 從預設的AEMas a Cloud ServiceDispatcher設定恢復到該位置。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

以及以下陳述式：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 執行驗證器以檢查狀態

使用在您的目錄中執行AEMas a Cloud ServiceDispatcher驗證器 `dispatcher` 子命令：

```
$ validator dispatcher .
```

如果您看見有關遺失Include檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看見有關未定義變數「`PUBLISH_DOCROOT`」的錯誤，請將其重新命名為「`DOCROOT`」。

如需其他每個錯誤的相關資訊，請參閱驗證器工具檔案的疑難排解一節。

### 使用本機部署測試您的設定（需要安裝Docker）

使用指令碼 `docker_run.sh` 在AEMas a Cloud ServiceDispatcher工具中，您可以測試您的設定不包含任何僅顯示在部署中的其他錯誤：

### 步驟1：使用驗證器產生部署資訊

```
validator full -d out .
```

如此一來，即可驗證完整設定並產生部署資訊 `out`

### 步驟2：使用該部署資訊在Docker映像中啟動Dispatcher

在您的macOS電腦上執行AEM發佈伺服器，並在連線埠4503上接聽後，您就可以在該伺服器前面執行啟動Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

如此一來將啟動容器，並在本機連接埠 8080 上公開 Apache。

### 使用您的新Dispatcher設定

恭喜！如果驗證器不再回報任何問題，且Docker容器啟動時未出現任何失敗情況或警告，即可將您的設定移至 `dispatcher/src` Git存放庫的子目錄。

**使用AMS Dispatcher設定版本1的客戶應聯絡客戶支援，協助他們從版本1移轉至版本2，以便遵循上述指示。**
