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

## AMS Dispatcher與AEM as a Cloud Service之間的主要差異 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEM as a Cloud Service中的Apache和Dispatcher設定相當類似於AMS。 主要差異如下：

* 在AEM as a Cloud Service中，可能無法使用某些Apache指示詞（例如，`Listen`或`LogLevel`）
* 在AEM as a Cloud Service中，只有部分Dispatcher設定可以放入包含檔案中，其命名很重要。 例如，您要在不同主機上重複使用的篩選規則必須放在名為`filters/filters.any`的檔案中。 如需詳細資訊，請參閱參考頁面。
* 在AEM as a Cloud Service中有額外的驗證，可不允許使用`/glob`撰寫篩選規則以防止安全性問題。 由於`deny *`已使用，而非`allow *` （無法使用），因此客戶可受益於在本機執行Dispatcher以及進行試用和錯誤、檢視記錄以確切瞭解Dispatcher篩選器正在封鎖哪些路徑，以便可以新增這些路徑。
* 在AEM as a Cloud Service中，目前強烈建議[選擇加入以使用Dispatcher設定的彈性來源模式](/help/implementing/dispatcher/disp-overview.md#validation-debug)，例如，使用Web層設定管道，或在設定檔案的數量和結構上有更好的彈性。

## 將Dispatcher設定從AMS移轉至AEM as a Cloud Service的准則

Dispatcher的設定結構在Managed Services和AEM as a Cloud Service之間有所差異。 以下提供如何從AMS Dispatcher設定版本2移轉至AEM as a Cloud Service的逐步指南。

## 如何將AMS轉換為AEM as a Cloud Service Dispatcher設定

以下章節提供如何轉換AMS設定的逐步指示。 其假設
您的封存具有類似於[Cloud Manager Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html?lang=zh-Hant)中說明的結構

### 提取封存並移除最終首碼

將封存解壓縮至資料夾，並確定直接子資料夾以`conf`、`conf.d`、
`conf.dispatcher.d`和`conf.modules.d`。 如果沒有，請在階層中向上移動它們。

### 移除未使用的子資料夾和檔案

移除子資料夾`conf`和`conf.modules.d`，以及符合`conf.d/*.conf`的檔案。

### 移除所有非發佈用的虛擬主機

移除`conf.d/enabled_vhosts`中具有`author`、`unhealthy`、`health`的任何虛擬主機檔案
名稱中有`lc`或`flush`。 `conf.d/available_vhosts`中所有非虛擬主機檔案
連結到的也可移除。

### 移除或註解未引用連接埠 80 的虛擬主機區段

例如，如果您的虛擬主機檔案中仍有區段專門引用連線埠80以外的連線埠：

```
<VirtualHost *:443>
...
</VirtualHost>
```

請移除或加上註解。 系統將不會處理這些區段中的陳述式，但如果
保留它們，您最終可能仍會編輯它們，並且不會有任何效果，這是令人困惑的。

### 檢查重新寫入

輸入目錄`conf.d/rewrites`。

移除任何名為`base_rewrite.rules`和`xforwarded_forcessl_rewrite.rules`的檔案並記住
移除虛擬主機檔案中引用它們的`Include`陳述式。

如果`conf.d/rewrites`現在包含單一檔案，則應將其重新命名為`rewrite.rules`，而不要這麼做
也忘記調整在虛擬主機檔案中引用該檔案的`Include`陳述式。

然而，如果該資料夾包含多個虛擬主機專屬檔案，則其內容應該是
已複製至虛擬主機檔案中引用它們的`Include`陳述式。

### 檢查變數

輸入目錄`conf.d/variables`。

移除任何名為`ams_default.vars`的檔案，並記得移除虛擬中的`Include`陳述式
主機檔案引用這些檔案。

如果`conf.d/variables`現在包含單一檔案，則應將其重新命名為`custom.vars`，而不要這麼做
也忘記調整在虛擬主機檔案中引用該檔案的`Include`陳述式。

然而，如果該資料夾包含多個虛擬主機專屬檔案，則其內容應該是
已複製至虛擬主機檔案中引用它們的`Include`陳述式。

### 移除允許清單

移除資料夾`conf.d/whitelists`，並移除虛擬主機檔案中引用的`Include`陳述式
該子資料夾中的某個檔案。

### 取代任何已無法使用的變數

在所有虛擬主機檔案中：

將`PUBLISH_DOCROOT`重新命名為`DOCROOT`
移除引用名為`DISP_ID`、`PUBLISH_FORCE_SSL`或`PUBLISH_WHITELIST_ENABLED`之變數的區段

### 執行驗證器以檢查狀態

使用`httpd`子命令在您的目錄中執行Dispatcher驗證器：

```
$ validator httpd .
```

如果您看見有關遺失Include檔案的錯誤，請檢查您是否已正確地重新命名那些檔案
檔案。

如果您看到未加入允許清單的Apache指示詞，請將其移除。

### 移除所有非發佈用的伺服器陣列

移除`conf.dispatcher.d/enabled_farms`中任何含有`author`、`unhealthy`、`health`的伺服器陣列檔案
名稱中有`lc`或`flush`。 `conf.dispatcher.d/available_farms`中所有非伺服器陣列檔案
連結到的也可移除。

### 重新命名伺服器陣列檔案

必須重新命名`conf.dispatcher.d/enabled_farms`中的所有陣列以符合模式`*.farm`，例如
名為`customerX_farm.any`的伺服器陣列檔案應重新命名為`customerX.farm`。

### 檢查快取

輸入目錄`conf.dispatcher.d/cache`。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/cache`現在為空白，請複製檔案`conf.dispatcher.d/cache/rules.any`
從標準Dispatcher設定至此資料夾。 標準Dispatcher
您可以在此SDK的資料夾`src`中找到設定。 別忘了改寫
`$include`陳述式引用伺服器陣列檔案中的`ams_*_cache.any`個規則檔案
以及。

如果`conf.dispatcher.d/cache`現在包含尾碼為`_cache.any`的單一檔案，
應將其重新命名為`rules.any`，別忘了調整`$include`陳述式
在伺服器陣列檔案中也會參照該檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製至在伺服器陣列檔案中引用它們的`$include`陳述式。

移除任何尾碼為`_invalidate_allowed.any`的檔案。

從預設值複製檔案`conf.dispatcher.d/cache/default_invalidate_any`
雲端Dispatcher設定中的AEM移至該位置。

在每個伺服器陣列檔案中，移除`cache/allowedClients`區段中的任何內容並加以取代
替換為：

```
$include "../cache/default_invalidate.any"
```

### 檢查使用者端標頭

輸入目錄`conf.dispatcher.d/clientheaders`。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/clientheaders`現在包含尾碼為`_clientheaders.any`的單一檔案，
應將其重新命名為`clientheaders.any`，別忘了調整`$include`陳述式
在伺服器陣列檔案中也會參照該檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製至在伺服器陣列檔案中引用它們的`$include`陳述式。

從預設值複製檔案`conf.dispatcher/clientheaders/default_clientheaders.any`
AEM as a Cloud Service Dispatcher設定至該位置。

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

輸入目錄`conf.dispatcher.d/filters`。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/filters`現在包含單一檔案，則應將其重新命名為
`filters.any`且別忘了調整引用該內容的`$include`陳述式
伺服器陣列檔案中的檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製至在伺服器陣列檔案中引用它們的`$include`陳述式。

從預設值複製檔案`conf.dispatcher/filters/default_filters.any`
AEM as a Cloud Service Dispatcher設定至該位置。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

以及以下陳述式：

```
$include "../filters/default_filters.any"
```

### 檢查轉譯

輸入目錄`conf.dispatcher.d/renders`。

移除該資料夾中的所有檔案。

從預設值複製檔案`conf.dispatcher.d/renders/default_renders.any`
AEM as a Cloud Service Dispatcher設定至該位置。

在每個伺服器陣列檔案中，移除`renders`區段中的任何內容並加以取代
替換為：

```
$include "../renders/default_renders.any"
```

### 檢查虛擬主機

將目錄`conf.dispatcher.d/vhosts`重新命名為`conf.dispatcher.d/virtualhosts`並輸入它。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/virtualhosts`現在包含單一檔案，則應將其重新命名為
`virtualhosts.any`且別忘了調整引用該內容的`$include`陳述式
伺服器陣列檔案中的檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製至在伺服器陣列檔案中引用它們的`$include`陳述式。

從預設值複製檔案`conf.dispatcher/virtualhosts/default_virtualhosts.any`
AEM as a Cloud Service Dispatcher設定至該位置。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

以及以下陳述式：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 執行驗證器以檢查狀態

使用`dispatcher`子命令在您的目錄中執行AEM as a Cloud Service Dispatcher驗證器：

```
$ validator dispatcher .
```

如果您看見有關遺失Include檔案的錯誤，請檢查您是否已正確地重新命名那些檔案
檔案。

如果您看見有關未定義變數「`PUBLISH_DOCROOT`」的錯誤，請將其重新命名為「`DOCROOT`」。

若需瞭解其他每個錯誤，請參閱
驗證器工具檔案。

### 使用本機部署測試您的設定（需要安裝Docker）

使用AEM as a Cloud Service Dispatcher工具中的指令碼`docker_run.sh`，您可以測試它
您的設定未包含任何其他只會在下列位置顯示的錯誤：
部署：

### 步驟1：使用驗證器產生部署資訊

```
validator full -d out .
```

這會驗證完整設定並在`out`中產生部署資訊

### 步驟2：使用該部署資訊在Docker映像中啟動Dispatcher

在您的macOS電腦上執行AEM發佈伺服器，接聽連線埠4503，
您可以在該伺服器前面執行啟動Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

如此一來將啟動容器，並在本機連接埠 8080 上公開 Apache。

### 使用新的Dispatcher設定

恭喜！如果驗證器不再回報任何問題，而且
Docker容器啟動時沒有出現任何失敗情況或警告，您
準備將您的設定移至`dispatcher/src`子目錄
，屬於您的git存放庫。

**使用AMS Dispatcher設定版本1的客戶應聯絡客戶支援，協助他們從版本1移轉至版本2，以便遵循上述指示。**
