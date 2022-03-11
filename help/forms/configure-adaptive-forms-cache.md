---
title: 配置自適應Forms快取
seo-title: Configure Adaptive Forms cache
description: '自適應Forms快取專門為自適應Forms和文檔設計。 它快取自適應Forms和自適應文檔，以減少在客戶端上呈現自適應表單或文檔所需的時間。 '
seo-description: The Adaptive Forms cache is designed specifically for Adaptive Forms and documents. It caches Adaptive Forms and adaptive documents with the objective of reducing the time required to render an Adaptive Form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---


# 配置自適應Forms快取 {#configure-adaptive-forms-cache}

快取是縮短資料存取時間、減少延遲和提高輸入/輸出(I/O)速度的機制。 自適應Forms快取僅儲存自適應表單的HTML內容和JSON結構，而不保存任何預填資料。 它有助於減少在客戶端上呈現自適應表單所需的時間。 它專門為適應性Forms設計。

## 在作者和發佈實例上配置AdaptiveForms快取 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. 轉到AEMWeb控制台配置管理器 `https://[server]:[port]/system/console/configMgr`。
1. 按一下 **[!UICONTROL 自適應形式與交互通信Web通道配置]** 編輯其配置值。
1. 在 [!UICONTROL 編輯配置值] 對話框，指定實例的最大表單或文檔數AEM [!DNL Forms] 伺服器可以在 **[!UICONTROL 自適應Forms]** 的子菜單。 預設值為 100。

   >[!NOTE]
   >
   >要禁用快取，請將「自適應Forms數」欄位中的值設定為 **0**。 在禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

   ![AdaptiveFormsHTML快取的配置對話框](assets/cache-configuration-edit.png)

1. 按一下 **[!UICONTROL 保存]** 的子菜單。

您的環境配置為使用快取自適應Forms和相關資產。


## （可選）在調度程式處配置Adaptive Form快取 {#configure-the-cache}

您還可以在調度程式上配置Adaptive Form快取，以提高效能。

### 先決條件 {#pre-requisites}

* 啟用 [合併或預填充客戶端資料](prepopulate-adaptive-form-fields.md#prefill-at-client) 的雙曲餘切值。 它有助於合併預填充表單的每個實例的唯一資料。
* [為每個發佈實例啟用刷新代理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance)。 它有助於為自適應Forms獲得更好的快取效能。 刷新代理的預設URL為 `http://[server]:[port]]/etc/replication/agents.publish/flush.html`。

### 在調度程式上快取自適應Forms的注意事項 {#considerations}

* 使用AdaptiveForms快取時，使用 [!DNL Dispatcher] 快取自適應表單的客戶端庫（CSS和JavaScript）。
* 在開發自定義元件時，在用於開發的伺服器上保持禁用AdaptiveForms快取。
* 不快取沒有副檔名的URL。 例如，具有模式模式的URL`/content/forms/[folder-structure]/[form-name].html` 快取，快取忽略具有模式的URL `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`。 因此，使用帶擴展的URL來獲取快取的好處。
* 本地化自適應Forms的注意事項：
   * 使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求自適應表單的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * 使用瀏覽器區域設定禁用 <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->格式的URL `http://host:port/content/forms/af/<adaptivefName>.html`。
   * 使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`, **[!UICONTROL 使用瀏覽器區域設定]** 在「配置管理器」中，將提供「自適應表單」的非本地化版本。 非本地化語言是開發自適應表單時使用的語言。 不考慮為瀏覽器配置的區域設定（瀏覽器區域設定），並提供非本地化版本的「自適應表單」。
   * 使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`, **[!UICONTROL 使用瀏覽器區域設定]** 在「配置管理器」中，如果可用，則提供「自適應表單」的本地化版本。 本地化的「自適應表單」的語言基於為瀏覽器配置的區域設定（瀏覽器區域設定）。 它會導致 [僅快取自適應表單的第一個實例]。 要防止在實例上發生問題，請參閱 [故障排除](#only-first-insatnce-of-adptive-forms-is-cached)。

### 在調度程式處啟用快取

執行下列步驟以啟用和配置調度程式上的自適應Forms:

1. 開啟您環境的每個發佈實例的以下URL並配置複製代理：
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [將以下內容添加到dispatcher.any檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#automatically-invalidating-cached-files):

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

   添加以上內容時：

   * 在未發佈表單的更新版本之前，自適應表單仍保留在快取中。

   * 當發佈自適應表單中引用的較新版本的資源時，受影響的自適應Forms將自動失效。 引用資源的自動無效存在一些例外。 有關異常的解決方法，請參見 [故障排除](#troubleshooting) 的子菜單。
1. [添加以下rules dispatcher.any或自定義規則檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache)。 它不包括不支援快取的URL。 例如，交互通信。

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

1. [將以下參數添加到忽略URL參數清單](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

您的AEM環境配置為快取自適應Forms。 它快取所有類型的自適應Forms。 如果您要求在傳遞快取頁之前檢查用戶對頁的訪問權限，請參閱 [快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html)。

## 疑難排解 {#troubleshooting}

### 某些包含影像或視頻的自適應Forms不會自動從調度程式快取中無效 {#videos-or-images-not-auto-invalidated}

#### 問題 {#issue1}

當您通過資產瀏覽器選擇影像或視頻並將其添加到自適應表單，並且這些影像和視頻在資產編輯器中編輯時，包含此類影像的自適應Forms不會自動從調度程式快取中無效。

#### 解決方案 {#Solution1}

發佈影像和視頻後，顯式取消發佈和發佈引用這些資產的Adaptive Forms。

### 某些包含內容片段或經驗片段的自適應Forms不會自動從調度程式快取中無效 {#content-or-experience-fragment-not-auto-invalidated}

#### 問題 {#issue2}

當您向自適應表單中添加內容片段或體驗片段並且這些資產被獨立編輯和發佈時，自適應Forms將包含這些資產，這些資產不會自動從調度程式快取中失效。

#### 解決方案 {#Solution2}

在發佈更新的內容片段或經驗片段後，明確取消發佈和發佈使用這些資產的自適應Forms。

### 只快取自適應表單的第一個實例{#only-first-insatnce-of-adptive-forms-is-cached}

#### 問題 {#issue3}

當自適應表單URL沒有任何本地化資訊時， **[!UICONTROL 使用瀏覽器區域設定]** 在「配置管理器」中，提供「自適應表單」的本地化版本，並且只快取「自適應表單」的第一個實例並將其發送給每個後續用戶。

#### 解決方案 {#Solution3}

請執行以下步驟來解決問題：

1. 開啟conf.d/httpd-dispatcher.conf或配置為在運行時載入的任何其他配置檔案。

1. 將以下代碼添加到檔案並保存。 它是一個示例代碼，可根據您的環境修改它。

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
