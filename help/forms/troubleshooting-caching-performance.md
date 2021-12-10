---
title: '疑難排解快取效能  '
seo-title: Troubleshooting caching performance
description: '疑難排解快取效能  '
seo-description: Troubleshooting caching performance
contentOwner: khsingh
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 快取效能 {#caching-performance}

在Cloud Service環境中設定或使用適用性Forms快取時，您可能會遇到下列某些問題：

## 某些包含影像或視訊的適用性Forms不會從Dispatcher快取中自動失效 {#images-videos-not-invalidated}

您可以從資產瀏覽器選取影像或影片，並將其新增至最適化表單。 在「資產」編輯器中編輯這些影像時，包含這類影像的適用性表單快取版本不會失效。 適用性表單會繼續顯示舊影像。

若要解決此問題，發佈影像和影片後，請明確取消發佈並發佈參考這些資產的適用性Forms。

## 某些包含內容片段或體驗片段的適用性Forms不會從Dispatcher快取中自動失效 {#content-fragments-experience-fragments-not-invalidated}

您可以將內容片段或體驗片段新增至最適化表單。 獨立編輯和發佈這些片段時，包含這類片段的適用性表單快取版本不會失效。 適用性表單會繼續顯示舊的片段。

若要解決此問題，請在發佈更新的內容片段或體驗片段後，明確取消發佈並發佈使用這些資產的適用性Forms。

## 系統僅快取適用性Forms的第一個例項 {#only-first-instance-cached}

當適用性表單URL不含任何本地化資訊，且啟用設定管理器中的「使用瀏覽器地區」選項時，會提供適用性表單的本地化版本，並根據第一個請求（請求的瀏覽器地區）快取適用性表單的例項並傳送給後續的每位使用者。

執行下列步驟以解決問題：

1. 開啟您的Experience Manager專案。
1. 開啟 `dispatcher/scr/conf.d/rewrites/rewrite.rules` 編輯。
1. 開啟 `conf.d/httpd-dispatcher.conf` 或任何其他設定檔，以在執行階段載入。
1. 將下列程式碼新增至您的檔案並儲存。 此范常式式碼會加以修改，以符合您的環境。

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two character which most likely will be the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## CDN快取在300秒後停止運作 {#cdn-caching-stops-working-after-300-seconds}

CDN快取會在300秒後停止運作，而CDN上所有快取的請求會重新導向至Dispatcher。

若要解決此問題，請將頁首設為0:

1. 在建立檔案 `src\conf.d\available_vhosts`

1. 將下列內容新增至檔案以設定頁首

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. 儲存並關閉檔案。
1. 修改軟連結 `src\conf.d\enabled_vhosts\default.vhost` 指向新檔案。
