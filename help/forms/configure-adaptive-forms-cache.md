---
title: 什麼是調適型表單快取？ 以及如何快取AEM最適化表單？
description: 最適化Forms快取是專為最適化Forms和檔案所設計，其目標是減少轉譯最適化表單或檔案所需的時間。
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
source-git-commit: 5e02cf36112ce29cd3ebfd772623654328598bf2
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 1%

---


# 設定最適化Forms快取 {#configure-adaptive-forms-cache}

快取是一種可縮短資料存取時間、減少延遲以及改善輸入/輸出(I/O)速度的機制。 最適化Forms快取只會儲存最適化表單的HTML內容和JSON結構，不會儲存任何預先填入的資料。 它有助於減少在使用者端上轉譯調適型表單所需的時間。 這是專為最適化Forms所設計。

## 在製作和發佈執行個體上設定最適化Forms快取 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. 前往`https://[server]:[port]/system/console/configMgr`的AEM Web主控台組態管理員。
1. 按一下&#x200B;**[!UICONTROL 最適化表單和互動式通訊Web Channel設定]**&#x200B;以編輯其設定值。
1. 在[!UICONTROL 編輯設定值]對話方塊中，指定AEM [!DNL Forms Server]的執行個體可在&#x200B;**[!UICONTROL 最適化Forms數目]**&#x200B;欄位中快取的表單或檔案數目上限。 預設值為 100。

   >[!NOTE]
   >
   >若要停用快取，請將[最適化Forms數目]欄位中的值設定為&#x200B;**0**。 當您停用或變更快取設定時，快取會重設，所有表單和檔案都會從快取中移除。

   最適化FormsHTML快取的![設定對話方塊](assets/cache-configuration-edit.png)

1. 按一下[儲存]儲存組態。****

您的環境已設定為使用快取最適化Forms和相關資產。


## （可選）在Dispatcher設定最適化表單快取 {#configure-the-cache}

您也可以在Dispatcher設定最適化表單快取，以獲得額外的效能提升。

### 必要條件 {#pre-requisites}

* 啟用[在使用者端](prepopulate-adaptive-form-fields.md#prefill-at-client)合併或預填資料。 它有助於合併預填表單的每個例項的唯一資料。
* [為每個發佈執行個體啟用排清代理程式](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance)。 這有助於為最適化Forms獲得更好的快取效能。 排清代理程式的預設URL為`http://[server]:[port]]/etc/replication/agents.publish/flush.html`。

### 在Dispatcher上快取最適化Forms的考量事項 {#considerations}

* 使用最適化Forms快取時，請使用AEM [!DNL Dispatcher]來快取最適化表單的使用者端資料庫(CSS和JavaScript)。
* 開發自訂元件時，在用於開發的伺服器上，停用Adaptive Forms快取。
* 不會快取沒有副檔名的URL。 例如，快取模式為`/content/forms/[folder-structure]/[form-name].html`的URL，而快取會忽略模式為`/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`的URL。 因此，請使用具有擴充功能的URL，以獲得快取的優點。
* 本地化Adaptive Forms的考量事項：
   * 使用URL格式`http://host:port/content/forms/af/<afName>.<locale>.html`來要求最適化表單的本地化版本，而非`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * 針對格式為`http://host:port/content/forms/af/<adaptivefName>.html`的URL停用使用瀏覽器地區設定<!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->。
   * 當您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`，且組態管理員中的&#x200B;**[!UICONTROL 使用瀏覽器地區設定]**&#x200B;已停用時，會提供非當地語系化版本的調適型表單。 非當地語系化語言是開發最適化表單時使用的語言。 系統不會考量為瀏覽器設定的地區設定（瀏覽器地區設定），而是提供非當地語系化版本的調適型表單。
   * 當您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`，並且啟用Configuration Manager中的&#x200B;**[!UICONTROL 使用瀏覽器地區設定]**&#x200B;時，會提供當地語系化的最適化表單版本（如果有的話）。 當地語系化最適化表單的語言取決於瀏覽器設定的地區設定（瀏覽器地區設定）。 這會導致只快取[最適化表單]的第一個執行個體。 若要防止執行個體發生問題，請參閱[疑難排解](#only-first-insatnce-of-adptive-forms-is-cached)。

### 在Dispatcher啟用快取

執行以下列出的步驟，以便您可以在Dispatcher上啟用和設定快取最適化Forms：

1. 為環境的每個發佈執行個體開啟以下URL，並設定復寫代理程式：
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [將以下專案新增到您的dispatcher.any檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#automatically-invalidating-cached-files)：

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

   * 當最適化表單中參考的資源的較新版本發佈時，受影響的最適化表單會自動失效。 參考資源的自動失效有一些例外。 如需例外狀況的因應措施，請參閱[疑難排解](#troubleshooting)區段。
1. [新增以下規則dispatcher.any或自訂規則檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache)。 它會排除不支援快取的URL。 例如，互動式通訊。

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

您的AEM環境已設定為快取最適化Forms。 它會快取所有型別的調適型Forms。 如果您需要在傳遞快取頁面之前檢查頁面的使用者存取許可權，請參閱[快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html)。

## 疑難排解 {#troubleshooting}

### 有些包含影像或影片的最適化Forms不會從Dispatcher快取中自動失效 {#videos-or-images-not-auto-invalidated}

#### 問題 {#issue1}

當您透過資產瀏覽器選取影像或視訊並新增至最適化表單，且在Assets編輯器中編輯時，此類資產不會從Dispatcher快取中自動失效。

#### 解決方案 {#Solution1}

發佈影像和影片後，請明確取消發佈並發佈參照這些資產的最適化Forms。

### 某些包含內容片段或體驗片段的Adaptive Forms不會從Dispatcher快取中自動失效 {#content-or-experience-fragment-not-auto-invalidated}

#### 問題 {#issue2}

當您將內容片段或體驗片段新增到調適型表單並且這些資產經過獨立編輯和發佈時，包含此類資產的Adaptive Forms不會自動從Dispatcher快取中失效。

#### 解決方案 {#Solution2}

發佈更新的內容片段或體驗片段後，請明確取消發佈並發佈使用這些資產的Adaptive Forms。

### 僅快取最適化表單的第一個執行個體{#only-first-insatnce-of-adptive-forms-is-cached}

#### 問題 {#issue3}

當最適化表單URL沒有任何本地化資訊，且組態管理員中的&#x200B;**[!UICONTROL 使用瀏覽器地區設定]**&#x200B;已啟用時。 系統會提供當地語系化版本的最適化表單，且只快取最適化表單的第一個例項並傳送給每個後續使用者。

#### 解決方案 {#Solution3}

1. 開啟「conf.d/httpd-dispatcher.conf」或任何其他設定為在執行階段載入的組態檔。

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



>[!MORELIKETHIS]
>
>* [疑難排解AEM Formsas a Cloud Service的快取相關問題](/help/forms/troubleshooting-caching-performance.md)