---
title: 將Dispatcher設定從AMS移轉至AEM作為Cloud Service
description: '將Dispatcher設定從AMS移轉至AEM作為Cloud Service '
feature: Dispatcher
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 14%

---

# 將Dispatcher設定從AMS移轉至AEM作為Cloud Service {#Dispatcher-in-the-cloud}

## AMS Dispatcher與AEM as aCloud Service之間的主要差異 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEM as aCloud Service中的Apache和Dispatcher設定與AMS 1相當類似。 主要差異為：

* 在AEM as aCloud Service中，某些Apache指令不得使用（例如`Listen`或`LogLevel`）
* 在AEM as aCloud Service中，只能將Dispatcher設定的某些片段放入包含檔案中，而且其命名很重要。 例如，要在不同主機間重複使用的篩選規則必須放在名為`filters/filters.any`的檔案中。 如需詳細資訊，請參閱參考頁面。
* 在AEM as aCloud Service中，有額外驗證可禁止使用`/glob`撰寫的篩選規則，以防止發生安全性問題。 由於將使用`deny *`而非`allow *`（無法使用），因此客戶將受益於在本機執行Dispatcher，以及執行試用和錯誤，查看記錄檔，以明確知道Dispatcher篩選器封鎖哪些路徑，以便新增這些路徑。

## 將Dispatcher設定從AMS移轉至AEM作為Cloud Service的准則

Managed Services和AEM as aCloud Service之間的Dispatcher設定結構有差異。 以下提供逐步指南，說明如何從AMS Dispatcher設定第2版移轉至AEM as aCloud Service。

## 如何將AMS轉換為AEM as a Cloud service Dispatcher設定

以下章節提供如何轉換AMS設定的逐步指示。 這是假設
封存的結構類似於[Cloud Manager Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)中所述的結構

### 提取封存並移除最終首碼

將存檔解壓到資料夾，並確保直接子資料夾以`conf`、`conf.d`開頭，
`conf.dispatcher.d`和`conf.modules.d`。 如果沒有，請在階層中向上移動。

### 移除未使用的子資料夾和檔案

移除子資料夾`conf`和`conf.modules.d`，以及符合`conf.d/*.conf`的檔案。

### 移除所有非發佈用的虛擬主機

刪除`conf.d/enabled_vhosts`中具有`author`、`unhealthy`、`health`、
`lc`或`flush`。 `conf.d/available_vhosts`中所有非虛擬主機檔案
連結至的也可移除。

### 移除或註解未引用連接埠 80 的虛擬主機區段

如果您的虛擬主機檔案中仍有區段專門引用埠80以外的其他埠，例如：

```
<VirtualHost *:443>
...
</VirtualHost>
```


請移除或加上註解。系統將不會處理這些區段中的陳述式，但如果您保留這些陳述式，您最終可能仍會編輯，但將徒勞無功而倍感困惑。

### 檢查重新寫入

輸入目錄`conf.d/rewrites`。

移除任何名為`base_rewrite.rules`和`xforwarded_forcessl_rewrite.rules`的檔案，並記得
在虛擬主機檔案中移除引用了`Include`陳述式。

如果`conf.d/rewrites`目前包含單一檔案，則應將其重新命名為`rewrite.rules`，否則不應
也別忘了調整在虛擬主機檔案中引用該檔案的`Include`陳述式。

但是，如果資料夾包含多個虛擬主機專用檔案，則其內容應為
複製到`Include`陳述式，在虛擬主機檔案中引用這些語句。

### 檢查變數

輸入目錄`conf.d/variables`。

移除任何名為`ams_default.vars`的檔案，並記得在虛擬檔案中移除`Include`陳述式
主機引用檔案的檔案。

如果`conf.d/variables`目前包含單一檔案，則應將其重新命名為`custom.vars`，否則不應
也別忘了調整在虛擬主機檔案中引用該檔案的`Include`陳述式。

但是，如果資料夾包含多個虛擬主機專用檔案，則其內容應為
複製到`Include`陳述式，在虛擬主機檔案中引用這些語句。

### 移除允許清單

移除資料夾`conf.d/whitelists`，並移除虛擬主機檔案中引用`Include`的陳述式
子資料夾中的檔案。

### 取代任何已無法使用的變數

在所有虛擬主機檔案中：

將`PUBLISH_DOCROOT`更名為`DOCROOT`
移除引用`DISP_ID`、`PUBLISH_FORCE_SSL`或`PUBLISH_WHITELIST_ENABLED`變數的區段

### 執行驗證器以檢查狀態

使用`httpd`子命令，在您的目錄中執行Dispatcher驗證器：

```
$ validator httpd .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看到未列入允許清單的Apache指示，請將其移除。

### 移除所有非發佈用的伺服器陣列

移除`conf.dispatcher.d/enabled_farms`中具有`author`、`unhealthy`、`health`、
`lc`或`flush`。 `conf.dispatcher.d/available_farms`中所有非
連結至的也可移除。

### 重新命名伺服器陣列檔案

必須更名`conf.d/enabled_farms`中的所有伺服器陣列以符合模式`*.farm`，例如
名為`customerX_farm.any`的伺服器陣列檔案應重新命名為`customerX.farm`。

### 檢查快取

輸入目錄`conf.dispatcher.d/cache`。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/cache`現在為空，請複製檔案`conf.dispatcher.d/cache/rules.any`
從標準Dispatcher設定傳送至此資料夾。 標準Dispatcher
可在此SDK的資料夾`src`中找到設定。 別忘了調整
`$include`引用伺服器陣列檔案中`ams_*_cache.any`規則檔案的語句
還有。

如果`conf.dispatcher.d/cache`現在包含尾碼為`_cache.any`的單一檔案，
應將其重新命名為`rules.any`，同時別忘了調整`$include`陳述式
在伺服器陣列檔案中也參考該檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製到`$include`陳述式，在伺服器陣列檔案中引用這些陳述式。

移除尾碼為`_invalidate_allowed.any`的任何檔案。

從預設值複製檔案`conf.dispatcher.d/cache/default_invalidate_any`
AEM。

在每個伺服器陣列檔案中，移除`cache/allowedClients`區段中的任何內容並加以取代
包含：

```
$include "../cache/default_invalidate.any"
```

### 檢查用戶端標頭

輸入目錄`conf.dispatcher.d/clientheaders`。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/clientheaders`現在包含尾碼為`_clientheaders.any`的單一檔案，
應將其重新命名為`clientheaders.any`，同時別忘了調整`$include`陳述式
在伺服器陣列檔案中也參考該檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製到`$include`陳述式，在伺服器陣列檔案中引用這些陳述式。

從預設值複製檔案`conf.dispatcher/clientheaders/default_clientheaders.any`
AEM作為該位置的Cloud ServiceDispatcher設定。

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
`filters.any`，別忘記調整引用該的`$include`陳述式
檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製到`$include`陳述式，在伺服器陣列檔案中引用這些陳述式。

從預設值複製檔案`conf.dispatcher/filters/default_filters.any`
AEM作為該位置的Cloud ServiceDispatcher設定。

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
AEM作為該位置的Cloud ServiceDispatcher設定。

在每個伺服器陣列檔案中，移除`renders`區段中的任何內容並加以取代
包含：

```
$include "../renders/default_renders.any"
```

### 檢查虛擬主機

將目錄`conf.dispatcher.d/vhosts`更名為`conf.dispatcher.d/virtualhosts`並輸入。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/virtualhosts`現在包含單一檔案，則應將其重新命名為
`virtualhosts.any`，別忘記調整引用該的`$include`陳述式
檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製到`$include`陳述式，在伺服器陣列檔案中引用這些陳述式。

從預設值複製檔案`conf.dispatcher/virtualhosts/default_virtualhosts.any`
AEM作為該位置的Cloud ServiceDispatcher設定。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

以及以下陳述式：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 執行驗證器以檢查狀態

使用`dispatcher`子命令，在目錄中以Cloud ServiceDispatcher驗證器的形式執行AEM :

```
$ validator dispatcher .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看見有關未定義變數「`PUBLISH_DOCROOT`」的錯誤，請將其重新命名為「`DOCROOT`」。

如果看見其他錯誤，請參考驗證器工具文件的疑難排解章節。

### 使用本機部署測試配置（需要安裝Docker）

使用AEM中的指令碼`docker_run.sh`做為Cloud ServiceDispatcher工具，即可進行測試
您的設定不包含任何只會顯示在
部署：

### 步驟1:使用驗證器產生部署資訊

```
validator full -d out .
```

這將驗證完整配置並在`out`中生成部署資訊

### 步驟2:使用該部署資訊在Docker映像中啟動Dispatcher

當AEM發佈伺服器在macOS電腦上執行，並在連接埠4503上接聽時，
您可以依照下列方式，在該伺服器前面執行Dispatcher:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

如此一來將啟動容器，並在本機連接埠 8080 上公開 Apache。

### 使用您的新Dispatcher設定

恭喜！ 如果驗證器不再回報任何問題，且
docker容器啟動時沒有任何故障或警告，您
準備將配置移至`dispatcher/src`子目錄
的URL。

**使用AMS Dispatcher設定1版的客戶應聯絡客戶支援，協助他們從第1版移轉至第2版，以便遵循上述指示。**
