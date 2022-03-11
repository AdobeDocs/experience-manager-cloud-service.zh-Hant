---
title: 將Dispatcher配置從AMS遷移到AEMas a Cloud Service
description: 將Dispatcher配置從AMS遷移到AEMas a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 14%

---

# 將Dispatcher配置從AMS遷移到AEMas a Cloud Service {#Dispatcher-in-the-cloud}

## AMS調度器與AEMas a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

as a Cloud Service中的Apache和AEMDispatcher配置與AMS配置非常相似。 主要區別是：

* 在AEMas a Cloud Service中，不能使用某些Apache指令(例如 `Listen` 或 `LogLevel`)
* 在AEMas a Cloud Service中，只能將Dispatcher配置中的某些部分包含檔案，其命名非常重要。 例如，要跨不同主機重用的篩選器規則必須放入名為 `filters/filters.any`。 有關詳細資訊，請參閱參考頁。
* 在AEMas a Cloud Service中，有額外的驗證來禁止使用 `/glob` 防止安全問題。 自 `deny *` 將使用，而不是 `allow *` （無法使用），客戶將受益於在本地運行Dispatcher並執行試用和錯誤操作，查看日誌以確切瞭解Dispatcher篩選器為了添加這些路徑而阻止的路徑。

## 將調度程式配置從AMS遷移到AEMas a Cloud Service

Dispatcher配置結構在Managed Services和AEMas a Cloud Service之間有差異。 下面是有關如何從AMS Dispatcher配置版本2遷移到AEMas a Cloud Service的逐步指南。

## 如何將AMS轉換為雲服AEM務調度程式配置

以下部分提供了有關如何轉換AMS配置的逐步說明。 它假定您的存檔具有與中所述的結構類似的結構 [Cloud Manager Dispatcher配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### 提取封存並移除最終首碼

將存檔解壓到資料夾，並確保立即的子資料夾以 `conf`。 `conf.d`。
`conf.dispatcher.d` 和 `conf.modules.d`。 如果它們沒有，請在層次中上移。

### 刪除未使用的子資料夾和檔案

刪除子資料夾 `conf` 和 `conf.modules.d`，以及檔案匹配 `conf.d/*.conf`。

### 移除所有非發佈用的虛擬主機

刪除中的任何虛擬主機檔案 `conf.d/enabled_vhosts` 那 `author`。 `unhealthy`。 `health`。
`lc` 或 `flush` 名字。 中的所有虛擬主機檔案 `conf.d/available_vhosts` 也可以刪除未連結的。

### 移除或註解未引用連接埠 80 的虛擬主機區段

如果虛擬主機檔案中仍有專門引用埠80以外的其他埠的部分，例如：

```
<VirtualHost *:443>
...
</VirtualHost>
```


請移除或加上註解。系統將不會處理這些區段中的陳述式，但如果您保留這些陳述式，您最終可能仍會編輯，但將徒勞無功而倍感困惑。

### 檢查重新寫入

輸入目錄 `conf.d/rewrites`。

刪除名為 `base_rewrite.rules` 和 `xforwarded_forcessl_rewrite.rules` 記住刪除 `Include` 虛擬主機檔案中引用它們的語句。

如果 `conf.d/rewrites` 現在包含一個檔案，應將其更名為 `rewrite.rules` 別忘了適應 `Include` 語句也引用虛擬主機檔案中的該檔案。

如果資料夾中包含多個虛擬主機特定的檔案，則應將其內容複製到 `Include` 在虛擬主機檔案中引用它們的語句。

### 檢查變數

輸入目錄 `conf.d/variables`。

刪除名為 `ams_default.vars` 記住刪除 `Include` 虛擬主機檔案中引用它們的語句。

如果 `conf.d/variables` 現在包含一個檔案，應將其更名為 `custom.vars` 別忘了適應 `Include` 語句也引用虛擬主機檔案中的該檔案。

如果資料夾中包含多個虛擬主機特定的檔案，則應將其內容複製到 `Include` 在虛擬主機檔案中引用它們的語句。

### 刪除允許清單

刪除資料夾 `conf.d/whitelists` 刪除 `Include` 虛擬主機檔案中引用該子資料夾中某個檔案的語句。

### 取代任何已無法使用的變數

在所有虛擬主機檔案中：

更名 `PUBLISH_DOCROOT` 至 `DOCROOT`
刪除引用名為的變數的節 `DISP_ID`。 `PUBLISH_FORCE_SSL` 或 `PUBLISH_WHITELIST_ENABLED`

### 執行驗證器以檢查狀態

在目錄中運行Dispatcher驗證程式， `httpd` 子命令：

```
$ validator httpd .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果看到未允許列出的Apache指令，請刪除它們。

### 移除所有非發佈用的伺服器陣列

刪除中的任何場檔案 `conf.dispatcher.d/enabled_farms` 那 `author`。 `unhealthy`。 `health`。
`lc` 或 `flush` 名字。 所有場檔案 `conf.dispatcher.d/available_farms` 也可以刪除未連結的。

### 重新命名伺服器陣列檔案

所有農場 `conf.d/enabled_farms` 必須更名以匹配模式 `*.farm`，例如，名為 `customerX_farm.any` 應更名 `customerX.farm`。

### 檢查快取

輸入目錄 `conf.dispatcher.d/cache`。

移除任何以「`ams_`」為首碼的檔案。

如果 `conf.dispatcher.d/cache` 現在為空，複製檔案 `conf.dispatcher.d/cache/rules.any`
從標準Dispatcher配置到此資料夾。 可在資料夾中找到標準Dispatcher配置 `src` 本SDK。 別忘了適應
`$include` 提及 `ams_*_cache.any` 伺服器場檔案中的規則檔案。

如果 `conf.dispatcher.d/cache` 現在包含帶尾碼的單個檔案 `_cache.any`，應更名為 `rules.any` 別忘了適應 `$include` 語句也引用了場檔案中的該檔案。

如果資料夾中包含多個具有該模式的場特定檔案，則應將其內容複製到 `$include` 在場檔案中引用它們的語句。

刪除具有尾碼的任何檔案 `_invalidate_allowed.any`。

複製檔案 `conf.dispatcher.d/cache/default_invalidate_any` 從雲調度AEM器配置中的預設值到該位置。

在每個場檔案中，刪除 `cache/allowedClients` 將其替換為：

```
$include "../cache/default_invalidate.any"
```

### 檢查用戶端標頭

輸入目錄 `conf.dispatcher.d/clientheaders`。

移除任何以「`ams_`」為首碼的檔案。

如果 `conf.dispatcher.d/clientheaders` 現在包含帶尾碼的單個檔案 `_clientheaders.any`，應更名為 `clientheaders.any` 別忘了適應 `$include` 語句也引用了場檔案中的該檔案。

如果資料夾中包含多個具有該模式的場特定檔案，則應將其內容複製到 `$include` 在場檔案中引用它們的語句。

複製檔案 `conf.dispatcher/clientheaders/default_clientheaders.any` 從預設的AEMas a Cloud Service調度程式配置到該位置。

在每個場檔案中，替換所有clientheader include語句，如下所示：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

以及以下陳述式：

```
$include "../clientheaders/default_clientheaders.any"
```

### 檢查篩選器

輸入目錄 `conf.dispatcher.d/filters`。

移除任何以「`ams_`」為首碼的檔案。

如果 `conf.dispatcher.d/filters` 現在包含一個檔案，它應更名為
`filters.any` 別忘了適應 `$include` 語句也引用了場檔案中的該檔案。

如果資料夾中包含多個具有該模式的場特定檔案，則應將其內容複製到 `$include` 在場檔案中引用它們的語句。

複製檔案 `conf.dispatcher/filters/default_filters.any` 從預設的AEMas a Cloud Service調度程式配置到該位置。

在每個場檔案中，替換任何篩選器包括如下所示的語句：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

以及以下陳述式：

```
$include "../filters/default_filters.any"
```

### 檢查轉譯

輸入目錄 `conf.dispatcher.d/renders`。

移除該資料夾中的所有檔案。

複製檔案 `conf.dispatcher.d/renders/default_renders.any` 從預設的AEMas a Cloud Service調度程式配置到該位置。

在每個場檔案中，刪除 `renders` 將其替換為：

```
$include "../renders/default_renders.any"
```

### 檢查虛擬主機

更名目錄 `conf.dispatcher.d/vhosts` 至 `conf.dispatcher.d/virtualhosts` 然後輸入。

移除任何以「`ams_`」為首碼的檔案。

如果 `conf.dispatcher.d/virtualhosts` 現在包含一個檔案，它應更名為
`virtualhosts.any` 別忘了適應 `$include` 語句也引用了場檔案中的該檔案。

如果資料夾中包含多個具有該模式的場特定檔案，則應將其內容複製到 `$include` 在場檔案中引用它們的語句。

複製檔案 `conf.dispatcher/virtualhosts/default_virtualhosts.any` 從預設的AEMas a Cloud Service調度程式配置到該位置。

在每個場檔案中，替換任何篩選器包括如下所示的語句：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

以及以下陳述式：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 執行驗證器以檢查狀態

在目錄AEM中運行as a Cloud ServiceDispatcher驗證程式， `dispatcher` 子命令：

```
$ validator dispatcher .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看見有關未定義變數「`PUBLISH_DOCROOT`」的錯誤，請將其重新命名為「`DOCROOT`」。

如果看見其他錯誤，請參考驗證器工具文件的疑難排解章節。

### 使用本地部署test配置（需要安裝Docker）

使用指令碼 `docker_run.sh` 在AEMas a Cloud Service的Dispatcher工具中，您可以test您的配置不包含任何僅在部署中顯示的其他錯誤：

### 步驟1:使用驗證程式生成部署資訊

```
validator full -d out .
```

這將驗證完整配置並在 `out`

### 步驟2:使用該部署資訊在Docker映像中啟動Dispatcher

在您的AEMmacOS電腦上運行發佈伺服器並偵聽埠4503時，您可以按如下方式在該伺服器前面運行啟動Dispatcher:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

如此一來將啟動容器，並在本機連接埠 8080 上公開 Apache。

### 使用新的Dispatcher配置

恭喜！ 如果驗證程式不再報告任何問題，並且docker容器啟動時沒有任何故障或警告，則您已準備好將配置移到 `dispatcher/src` git儲存庫的子目錄。

**使用AMS Dispatcher配置版本1的客戶應聯繫客戶支援以幫助他們從版本1遷移到版本2 ，以便可以遵循上述說明。**
