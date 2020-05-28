---
title: 將AMS轉換為Adobe Experience Manager做為雲端服務Dispatcher設定
description: 將AMS轉換為Adobe Experience Manager做為雲端服務Dispatcher設定
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---


# 將AMS轉換為Adobe Experience Manager(AEM)，做為雲端服務Dispatcher設定

## 簡介 {#introduction}

本節提供了有關如何轉換AMS配置的逐步說明。

>[!NOTE]
>它假定您的存檔具有與「管理Dispatcher配置」中所述的 [結構類似的結構](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)。

## 將AMS轉換為AEM做為雲端服務Dispatcher設定的步驟

1. **提取存檔並刪除最終的前置詞**

   將存檔解壓到資料夾，並確保立即子資料夾以conf 、 conf.d 、 conf.dispatcher.d和conf.modules.d開頭。 如果他們沒有，請在階層中向上移動。

1. **移除未儲存的子檔案夾和檔案**

   刪除子資料夾conf和conf.modules.d以及與conf.d/*.conf匹配的檔案。

1. **移除所有非發佈的虛擬主機**

1. **刪除任何虛擬主機檔案**

   在名稱中包含作者、不健康、健康、lc或刷新的conf.d/enabled_vhosts中。 conf.d/available_vhosts中未連結到的所有虛擬主機檔案也可以刪除。

1. 刪除或注釋不引用埠80的虛擬主機部分

   如果您的虛擬主機檔案中仍然有專門引用埠80以外的埠的部分，例如

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
移除或加上註解。 這些章節中的陳述式將不會被處理，但是，如果您保留這些陳述式，您最終可能仍會編輯這些陳述式，而不會產生任何效果，這會令人困惑。

1. **檢查重寫**

   * 輸入目錄conf.d/rewrites。

   * 刪除名為base_rewrite.rules和xforwarded_forcessl_rewrite.rules的任何檔案，並記得刪除引用它們的虛擬主機檔案中的「包括」語句。

   * 如果conf.d/rewrites現在包含單個檔案，則應將其更名為rewrite.rules，並且不要忘記在虛擬主機檔案中改寫引用該檔案的Include語句。

   * 但是，如果資料夾包含多個虛擬主機特定檔案，則其內容應複製到虛擬主機檔案中參照這些檔案的Include語句。

1. **檢查變數**

   1. 輸入目錄conf.d/variables。

   1. 刪除名為ams_default.vars的任何檔案，並記得在引用它們的虛擬主機檔案中刪除包括語句。

   1. 如果conf.d/variables現在包含單一檔案，則應將它重新命名為custom.vars，並且別忘了將Include陳述式改寫為虛擬主機檔案中該檔案的參考。

   1. 但是，如果資料夾包含多個虛擬主機特定檔案，則其內容應複製到虛擬主機檔案中參照這些檔案的Include語句。

1. **移除白名單**

   刪除資料夾conf.d/白名單，並刪除虛擬主機檔案中引用該子資料夾中某個檔案的「包括」語句。

1. **取代任何不再可用的變數**

   在所有虛擬主機檔案中：

   將PUBLISH_DOCROOT重新命名為DOCROTOR將參照名為DISP_ID、PUBLISH_FORCE_SSL或PUBLISH_WHITELIST_ENABLED的變數的區段移除

1. **運行驗證器以檢查狀態**

   使用httpd子命令在目錄中運行dispatcher validator:

   `$ validator httpd`
如果您發現遺失包含檔案的錯誤，請檢查您是否正確重新命名這些檔案。

   如果您看到未列入白名單的Apache指令，請將其刪除。

1. **移除所有非發佈農場**

   刪除conf.dispatcher.d/enabled_farms中名稱中包含author、invistic、health、lc或flush的任何場檔案。 conf.dispatcher.d/available_farms中未連結到的所有群檔案也可以刪除。

1. **更名群檔案**

   必須重新命名conf.dispatcher.d/enabled_farms中的所有場，以符合模式*.farm，因此，例如，名為customerX_farm.any的場檔案應重新命名customerX.farm。

1. **檢查快取**

   輸入目錄conf.dispatcher.d/cache。

   移除任何前置檔案ams_。

   如果conf.dispatcher.d/cache現在為空，請將檔案conf.dispatcher.d/cache/rules.any從標準調度器配置複製到此資料夾。 此SDK的檔案夾src中可找到標準分派器設定。 不要忘記調整引用場檔案中ams_*_cache.any規則檔案的$include語句。

   如果conf.dispatcher.d/cache現在包含帶有尾碼_cache.any的單一檔案，則應將其更名為rules.any，並且不要忘記改寫引用場檔案中該檔案的$include語句。

   但是，如果資料夾包含多個具有該模式的群特定檔案，則其內容應複製到群檔案中參照它們的$include語句。

   移除任何尾碼為_invalidate_allowed.any的檔案。

   將檔案conf.dispatcher.d/cache/default_invalidate_any從預設調度器配置複製到該位置。

   在每個群檔案中，刪除cache/allowedClients部分中的任何內容，並將其替換為：

   $include &quot;../cache/default_invalidate.any&quot;

1. **檢查用戶端標題**

   輸入目錄conf.dispatcher.d/clientheaders。

   移除任何前置檔案ams_。

   如果conf.dispatcher.d/clientheaders現在包含一個帶有尾碼_clientheaders.any的檔案，則應將其更名為clientheaders.any，並且不要忘記將引用該檔案的$include語句調整到場檔案中。

   但是，如果資料夾包含多個具有該模式的群特定檔案，則其內容應複製到群檔案中參照它們的$include語句。

   將檔案conf.dispatcher/clientheaders/default_clientheaders.any從預設的調度器配置複製到該位置。

   在每個群檔案中，替換任何clientheader包含如下所示的語句：

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   和聲明：

   `$include "../clientheaders/default_clientheaders.any"`

1. **檢查篩選**

   * 輸入目錄conf.dispatcher.d/filters。

   * 移除任何前置檔案ams_。

   * 如果conf.dispatcher.d/filters現在包含一個檔案，則應將其更名為filters.any，並且不要忘記將引用該檔案的$include語句調整到場檔案中。

   * 但是，如果資料夾包含多個具有該模式的群特定檔案，則其內容應複製到群檔案中參照它們的$include語句。

   * 將檔案conf.dispatcher/filters/default_filters.any從預設的調度器配置複製到該位置。

   * 在每個群檔案中，替換任何篩選器包含如下所示的語句：

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`with the statement:

      `$include "../filters/default_filters.any"`

1. **勾選轉譯**

   * 輸入目錄conf.dispatcher.d/renders。

   * 移除該資料夾中的所有檔案。

   * 將檔案conf.dispatcher.d/renders/default_renders.any從預設的調度器配置複製到該位置。

   * 在每個群檔案中，移除轉譯區段中的任何內容，並將其取代為：

      `$include "../renders/default_renders.any"`

1. **檢查虛擬主機**

   * 更名目 `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` 錄並輸入。

   * 移除任何前置詞的檔案 `ams_`。

   * 如果conf.dispatcher.d/virtualhosts現在包含一個檔案，則應將其更名為virtualhosts.any ，並且不要忘記將引用該檔案的$include語句調整到場檔案中。

   * 但是，如果資料夾包含多個具有該模式的群特定檔案，則其內容應複製到群檔案中參照它們的$include語句。

   * 將檔案conf.dispatcher/virtualhosts/default_virtualhosts.any從預設的調度器配置複製到該位置。

   * 在每個群檔案中，替換任何篩選器包含如下所示的語句：

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
和聲明：

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **運行驗證器以檢查狀態**

   * 使用dispatcher子命令在您的目錄中運行dispatcher validator:

      `$ validator dispatcher`

   * 如果您發現遺失包含檔案的錯誤，請檢查您是否正確重新命名這些檔案。

   * 如果您看到未定義變數的錯 `PUBLISH_DOCROOT`誤，請將它重新命名 `DOCROOT`。

   * 如需其他錯誤，請參閱驗證工具檔案的疑難排解一節。

## 使用本機部署測試您的組態 {#testing-config-local-deployment}

>[!IMPORTANT]
> 使用本機部署測試配置需要安裝Docker。

使用Dispatcher SDK `docker_run.sh` 中的指令碼，您可以測試您的設定是否不包含任何只會顯示在部署中的其他錯誤：

1. 使用驗證器生成部署資訊

   `validator full -d out`
這樣可驗證完整配置並生成部署資訊

1. 使用部署資訊在Docker映像中啟動調度程式

   當您的AEM發佈伺服器在您的macOS電腦上執行，並在連接埠4503上監聽時，您可以在該伺服器前面執行Dispatcher，如下所示：

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   這將啟動容器，並在本機埠8080上公開Apache。

## 使用您的新調度程式配置 {#using-dispatcher-config}

如果驗證器不再報告任何問題，而docker容器啟動時沒有出現任何故障或警告，您就可以將配置移動到git儲存庫的d`ispatcher/src` 子目錄。