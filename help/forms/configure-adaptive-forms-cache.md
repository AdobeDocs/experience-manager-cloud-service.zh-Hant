---
title: 設定最適化Forms快取
seo-title: Configure Adaptive Forms cache
description: 最適化Forms快取是專為最適化Forms和檔案所設計。 它會快取Adaptive Forms和Adaptive檔案，以減少在使用者端上轉譯Adaptive Form或檔案所需的時間。
seo-description: The Adaptive Forms cache is designed specifically for Adaptive Forms and documents. It caches Adaptive Forms and adaptive documents with the objective of reducing the time required to render an Adaptive Form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 1%

---


# 設定最適化Forms快取 {#configure-adaptive-forms-cache}

快取是一種可縮短資料存取時間、減少延遲以及改善輸入/輸出(I/O)速度的機制。 最適化Forms快取只會儲存最適化表單的HTML內容和JSON結構，不會儲存任何預先填入的資料。 它有助於減少在使用者端上轉譯最適化表單所需的時間。 它是專為Adaptive Forms設計的。

## 在製作和發佈執行個體上設定最適化Forms快取 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. 前往AEM Web主控台組態管理員，位於 `https://[server]:[port]/system/console/configMgr`.
1. 按一下 **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]** 以編輯其組態值。
1. 在 [!UICONTROL 編輯設定值] 對話方塊，指定AEM例項的表單或檔案數目上限 [!DNL Forms] 伺服器可以在以下位置快取： **[!UICONTROL 最適化Forms數量]** 欄位。 預設值為 100。

   >[!NOTE]
   >
   >若要停用快取，請將「最適化Forms數目」欄位中的值設為 **0**. 當您停用或變更快取設定時，快取會重設，所有表單和檔案都會從快取中移除。

   ![Adaptive FormsHTML快取的設定對話方塊](assets/cache-configuration-edit.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存設定。

您的環境已設定為使用快取Adaptive Forms和相關資產。


## （可選）在Dispatcher設定最適化表單快取 {#configure-the-cache}

您也可以在Dispatcher上設定最適化表單快取，以獲得額外的效能提升。

### 先決條件 {#pre-requisites}

* 啟用 [在使用者端合併或預填資料](prepopulate-adaptive-form-fields.md#prefill-at-client) 選項。 它有助於合併預填表單的每個例項的不重複資料。
* [為每個發佈執行個體啟用排清代理程式](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance). 它有助於取得Adaptive Forms的更佳快取效能。 排清代理程式的預設URL為 `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### 在Dispatcher上快取Adaptive Forms的考量事項 {#considerations}

* 使用最適化Forms快取時，請使用AEM [!DNL Dispatcher] 快取最適化表單的使用者端資料庫（CSS和JavaScript）。
* 開發自訂元件時，在用於開發的伺服器上，停用Adaptive Forms快取。
* 不會快取沒有副檔名的URL。 例如，具有模式模式的URL`/content/forms/[folder-structure]/[form-name].html` 快取，而且快取會忽略具有模式的URL `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. 因此，請使用具有擴充功能的URL，以享有快取的優點。
* 本地化Adaptive Forms的考量事項：
   * 使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求最適化表單的當地語系化版本，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * 停用使用瀏覽器地區設定 <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->格式為的URL `http://host:port/content/forms/af/<adaptivefName>.html`.
   * 當您使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`、和 **[!UICONTROL 使用瀏覽器地區設定]** 在configuration manager中，會停用非當地語系化版本的最適化表單。 非當地語系化語言是開發最適化表單時使用的語言。 系統不會考慮為瀏覽器設定的地區設定（瀏覽器地區設定），而是提供最適化表單的非當地語系化版本。
   * 當您使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`、和 **[!UICONTROL 使用瀏覽器地區設定]** 在Configuration Manager中，會啟用最適化表單的當地語系化版本（如果有的話）。 本地化的最適化表單的語言取決於為您的瀏覽器設定的地區設定（瀏覽器地區設定）。 這可能導致 [僅快取最適化表單的第一個例項]. 若要防止執行個體發生問題，請參閱 [疑難排解](#only-first-insatnce-of-adptive-forms-is-cached).

### 在Dispatcher上啟用快取

執行以下列出的步驟，在Dispatcher上啟用和設定快取Adaptive Forms：

1. 為環境的每個發佈執行個體開啟以下URL，並設定復寫代理程式：
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [將以下內容新增到您的dispatcher.any檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#automatically-invalidating-cached-files)：

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   當您新增上述專案時：

   * 最適化表單會保留在快取中，直到更新版本的表單未發佈為止。

   * 發佈最適化表單中參考的較新資源版本時，受影響的最適化Forms會自動失效。 參考資源的自動失效有一些例外。 如需例外的因應措施，請參閱 [疑難排解](#troubleshooting) 區段。
1. [新增以下rules dispatcher.any或自訂規則檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache). 它不包括不支援快取的URL。 例如，互動式通訊。

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [將下列引數新增至忽略URL引數清單](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters)：

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

您的AEM環境已設定為快取最適化Forms。 它會快取所有型別的Adaptive Forms。 如果您需要在傳遞快取頁面之前檢查頁面的使用者存取許可權，請參閱 [快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hant).

## 疑難排解 {#troubleshooting}

### 某些包含影像或影片的最適化Forms不會從Dispatcher快取中自動失效 {#videos-or-images-not-auto-invalidated}

#### 問題 {#issue1}

當您透過資產瀏覽器選擇影像或視訊並新增至最適化表單，且這些影像和視訊是在資產編輯器中編輯時，包含這類影像的Adaptive Forms不會自動從Dispatcher快取中失效。

#### 解決方案 {#Solution1}

發佈影像和影片後，請明確取消發佈並發佈參照這些資產的最適化Forms。

### 某些包含內容片段或體驗片段的Adaptive Forms不會從Dispatcher快取中自動失效 {#content-or-experience-fragment-not-auto-invalidated}

#### 問題 {#issue2}

當您將內容片段或體驗片段新增到調適型表單並且這些資產被獨立編輯和發佈時，包含此類資產的Adaptive Forms不會自動從Dispatcher快取中失效。

#### 解決方案 {#Solution2}

發佈更新的內容片段或體驗片段後，明確取消發佈並發佈使用這些資產的Adaptive Forms。

### 僅快取最適化表單的第一個執行個體{#only-first-insatnce-of-adptive-forms-is-cached}

#### 問題 {#issue3}

最適化表單URL沒有任何本地化資訊時，以及 **[!UICONTROL 使用瀏覽器地區設定]** 在configuration manager中啟用，會提供當地語系化版本的最適化表單，且只會快取最適化表單的第一個執行個體並傳送給每個後續使用者。

#### 解決方案 {#Solution3}

執行以下步驟以解決問題：

1. 開啟「conf.d/httpd-dispatcher.conf」或任何其他設定為在執行階段載入的設定檔。

1. 將下列程式碼新增至您的檔案並儲存。 此範常式式碼會加以修改以符合您的環境。

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two characters which most likely is the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
