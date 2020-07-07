---
title: 將 AMS 轉換為 Adobe Experience Manager 雲端服務 Dispatcher 設定
description: 將 AMS 轉換為 Adobe Experience Manager 雲端服務 Dispatcher 設定
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 100%

---


# 將 AMS 轉換為 Adobe Experience Manager (AEM) 雲端服務 Dispatcher 設定

## 簡介 {#introduction}

本節提供逐步指示，說明如何轉換 AMS 設定。

>[!NOTE]
>此工具假設您有一個封存，其結構類似於[管理 Dispatcher 設定](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)中所述的結構。

## 將 AMS 轉換為 AEM 雲端服務 Dispatcher 設定的步驟

1. **提取封存並移除最終首碼**

   將封存提取至資料夾，並確認直接子資料夾是否以「conf」、「conf.d」、「conf.dispatcher.d」和「conf.modules.d」開頭。若不是，請在階層中向上移動它們。

1. **移除未使用的子資料夾和檔案**

   移除子資料夾「conf」和「conf.modules.d」，以及符合「conf.d/*.conf」的檔案。

1. **移除所有非發佈用的虛擬主機**

1. **移除任何虛擬主機檔案**

   在「conf.d/enabled_vhosts」中，移除名稱包含「author」、「unhealthy」、「health」、「lc」或「flush」的虛擬主機檔案。您也可以移除所有在「conf.d/available_vhosts」中未連結的虛擬主機檔案。

1. 移除或註解未引用連接埠 80 的虛擬主機區段

   如果您的虛擬主機檔案中，仍有區段單獨引用連接埠 80 以外的連接埠，例如：

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
請移除它們或加上註解。這些區段中的陳述式將不會進行處理，但如果您保留這些陳述式，您最終可能仍會編輯它們，並因為徒勞無功地而感到困惑。

1. **檢查重新寫入**

   * 輸入目錄「conf.d/rewrites」。

   * 請移除任何名為「base_rewrite.rules」和「xforwarded_forcessl_rewrite.rules」的檔案，也要記得在虛擬主機中移除引用了上述檔案的 Include 陳述式。

   * 如果「conf.d/rewrites」目前包含單一檔案，則應將其重新命名為「rewrite.rules」，同時別忘了調整在虛擬主機檔案中引用考該檔案的 Include 陳述式。

   * 然而，如果該資料夾包含多個虛擬主機特定檔案，則應將其內容複製至在虛擬主機檔案中引用這些檔案的 Include 陳述式中。

1. **檢查變數**

   1. 輸入目錄「conf.d/variables」。

   1. 請移除任何命名為「ams_default.vars」的檔案，也要記得在虛擬主機中移除引用了上述檔案的 Include 陳述式。

   1. 如果「conf.d/variables」目前包含單一檔案，則應將其重新命名為「custom.vars」，同時別忘了調整在虛擬主機檔案中引用該檔案的 Include 陳述式。

   1. 然而，如果該資料夾包含多個虛擬主機特定檔案，則應將其內容複製至在虛擬主機檔案中引用這些檔案的 Include 陳述式中。

1. **移除白名單**

   移除資料夾「conf.d/whitelists」，並在虛擬主機檔案中，移除引用該子資料夾中部分檔案的 Include 陳述式。

1. **取代任何已無法使用的變數**

   在所有虛擬主機檔案中：

   將「PUBLISH_DOCROOT」重新命名為「DOCROOT」
移除引用了名為「DISP_ID」、「PUBLISH_FORCE_SSL」或「PUBLISH_WHITELIST_ENABLED」之變數的區段

1. **執行驗證器以檢查狀態**

   使用以下的 httpd 子命令，在您的目錄中執行 Dispatcher 驗證器：

   `$ validator httpd`
如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

   如果您看見未列入白名單的 Apache 指示詞，請刪除它們。

1. **移除所有非發佈用的伺服器陣列**

   移除任何名稱包含「author」、「unhealthy」、「health」、「lc」或「flush」的伺服器陣列檔案。您也可以移除所有在「conf.dispatcher.d/available_farms」中未連結的伺服器陣列檔案。

1. **重新命名伺服器陣列檔案**

   所有在「conf.dispatcher.d/enabled_farms」中的伺服器陣列都必須重新命名，以符合模式「*.farm」。舉例來說，名為「customerX_farm.any」的伺服器陣列檔案應重新命名為「customerX.farm」。

1. **檢查快取**

   輸入目錄「conf.dispatcher.d/cache」。

   移除任何以「ams_」為首碼的檔案。

   如果「conf.dispatcher.d/cache」目前空白，請將檔案「conf.dispatcher.d/cache/rules.any」從標準 Dispatcher 設定複製至此資料夾。您可以在此 SDK 的「src」資料夾中找到標準 Dispatcher 設定。同時，別忘了調整在伺服器陣列檔案中引用「ams_*_cache.any」規則檔的 $include 陳述式。

   如果「conf.dispatcher.d/cache」目前包含尾碼為「_cache.any」的單一檔案，則應將其重新命名為「rules.any」，同時別忘了調整在伺服器陣列檔案中引用該檔案的 $include 陳述式。

   然而，如果該資料夾包含多個有該模式的伺服器陣列特定檔案，則應將其內容複製至在伺服器陣列檔案中引用這些檔案的 $include 陳述式中。

   移除任何尾碼為「_invalidate_allowed.an」的檔案。

   將檔案「conf.dispatcher.d/cache/default_invalidate_any」從預設 Dispatcher 設定複製至該位置。

   在每個伺服器陣列檔案中，移除「cache/allowedClients」區段中的任何內容，並取代為：

   $include &quot;../cache/default_invalidate.any&quot;

1. **檢查用戶端標頭**

   輸入目錄「conf.dispatcher.d/clientheaders」。

   移除任何以「ams_」為首碼的檔案。

   如果「conf.dispatcher.d/clientheaders」目前包含尾碼為「_clientheaders.any」的單一檔案，則應將其重新命名為「clientheaders.any」，同時別忘了調整在伺服器陣列檔案中引用該檔案的 $include 陳述式。

   然而，如果該資料夾包含多個有該模式的伺服器陣列特定檔案，則應將其內容複製至在伺服器陣列檔案中引用這些檔案的 $include 陳述式中。

   將檔案「conf.dispatcher/clientheaders/default_clientheaders.any」從預設 Dispatcher 設定複製至該位置。

   在每個伺服器陣列檔案中，取代任何如下所示的「clientheader include」陳述式：

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   以及以下陳述式：

   `$include "../clientheaders/default_clientheaders.any"`

1. **檢查篩選器**

   * 輸入目錄「conf.dispatcher.d/filters」。

   * 移除任何以「ams_」為首碼的檔案。

   * 如果「conf.dispatcher.d/filters」目前包含單一檔案，則應將其重新命名為「filters.any」，同時別忘了調整在伺服器陣列檔案中引用該檔案的 $include 陳述式。

   * 然而，如果該資料夾包含多個有該模式的伺服器陣列特定檔案，則應將其內容複製至在伺服器陣列檔案中引用這些檔案的 $include 陳述式中。

   * 將檔案「conf.dispatcher/filters/default_filters.any」從預設 Dispatcher 設定複製至該位置。

   * 在每個伺服器陣列檔案中，取代任何如下所示的 filter include 陳述式：

   * $Include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`
以及以下陳述式：

      `$include "../filters/default_filters.any"`

1. **檢查轉譯**

   * 輸入目錄「conf.dispatcher.d/renders」。

   * 移除該資料夾中的所有檔案。

   * 將檔案「conf.dispatcher.d/renders/default_renders.any」從預設 Dispatcher 設定複製至該位置。

   * 在每個伺服器陣列檔案中，移除「renders」區段中的任何內容，並取代為：

      `$include "../renders/default_renders.any"`

1. **檢查虛擬主機**

   * 重新命名 `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` 目錄並進入其中。

   * 移除任何以「`ams_`」為首碼的檔案。

   * 如果「conf.dispatcher.d/virtualhosts」目前包含單一檔案，則應將其重新命名為「 virtualhosts.any」，同時別忘了調整在伺服器陣列檔案中引用該檔案的 $include 陳述式。

   * 然而，如果該資料夾包含多個有該模式的伺服器陣列特定檔案，則應將其內容複製至在伺服器陣列檔案中引用這些檔案的 $include 陳述式中。

   * 將檔案「conf.dispatcher/virtualhosts/default_virtualhosts.any」從預設 Dispatcher 設定複製至該位置。

   * 在每個伺服器陣列檔案中，取代任何如下所示的 filter include 陳述式：

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
以及以下陳述式：

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **執行驗證器以檢查狀態**

   * 使用以下的 dispatcher 子命令，在您的目錄中執行 Dispatcher 驗證器：

      `$ validator dispatcher`

   * 如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

   * 如果您看見有關未定義變數「`PUBLISH_DOCROOT`」的錯誤，請將其重新命名為「`DOCROOT`」。

   * 如果看見其他錯誤，請參考驗證器工具文件的疑難排解章節。

## 使用本機部署 {#testing-config-local-deployment} 測試您的設定

>[!IMPORTANT]
>
>使用本機部署測試設定時，需要安裝 Docker。

使用 Dispatcher SDK 中的指令碼 `docker_run.sh`，即可測試您的設定是否不包含任何僅顯示在部署中的其他錯誤：

1. 使用以下驗證器產生部署資訊：

   `validator full -d out`
如此一來，即可驗證所有設定並產生部署資訊。

1. 使用該部署資訊在 Docker 映像中啟動 Dispatcher

   在您的 macOS 電腦上執行 AEM 發佈伺服器，並在連接埠 4503 上接聽後，即可在該伺服器前端執行 Dispatcher，如下所示：

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   如此一來將啟動容器，並在本機連接埠 8080 上公開 Apache。

## 使用您的新 Dispatcher 設定 {#using-dispatcher-config}

如果驗證器不再回報任何問題，且 Docker 容器啟動時未出現任何失敗情況或警告，即可將您的設定移至 Git 存放庫的 D`ispatcher/src` 子目錄。