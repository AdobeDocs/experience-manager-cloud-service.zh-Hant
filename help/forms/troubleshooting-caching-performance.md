---
title: '快取效能疑難解答  '
seo-title: Troubleshooting caching performance
description: '快取效能疑難解答  '
seo-description: Troubleshooting caching performance
contentOwner: khsingh
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 快取效能 {#caching-performance}

在Cloud Service環境中配置或使用自適應Forms快取時，可能會遇到以下一些問題：

## 某些包含影像或視頻的自適應Forms不會自動從Dispatcher快取無效 {#images-videos-not-invalidated}

您可以從資產瀏覽器選擇影像或視頻並將其添加到自適應表單。 在「資產」編輯器中編輯這些影像時，包含此類影像的自適應表單的快取版本不會失效。 「自適應」表單繼續顯示較舊的影像。

要解決此問題，在發佈影像和視頻後，明確取消發佈並發佈引用這些資產的自適應Forms。

## 某些包含內容片段或體驗片段的自適應Forms不會自動從Dispatcher快取中失效 {#content-fragments-experience-fragments-not-invalidated}

可以將內容片段或體驗片段添加到自適應表單中。 當這些片段被獨立編輯和發佈時，包含這些片段的自適應表單的快取版本不會失效。 自適應表單繼續顯示舊片段。

要解決此問題，在發佈更新的內容片段或經驗片段後，明確取消發佈和發佈使用這些資產的自適應Forms。

## 只快取AdaptiveForms的第一個實例 {#only-first-instance-cached}

當自適應表單URL不包含任何本地化資訊，並且啟用了配置管理器中的「使用瀏覽器區域設定」選項時，將提供自適應表單的本地化版本，並基於第一個請求（請求瀏覽器區域設定）快取自適應表單實例並將其發送給每個後續用戶。

請執行以下步驟來解決問題：

1. 開啟Experience Manager項目。
1. 開啟 `dispatcher/scr/conf.d/rewrites/rewrite.rules` 的子菜單。
1. 開啟 `conf.d/httpd-dispatcher.conf` 或配置為在運行時載入的任何其他配置檔案。
1. 將以下代碼添加到檔案並保存。 它是一個示例代碼，可根據您的環境修改它。

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

## 300秒後CDN快取停止工作 {#cdn-caching-stops-working-after-300-seconds}

CDN快取在300秒後停止工作，所有對CDN上快取的請求都重定向到Dispatcher。

要解決此問題，請將帳齡標題設定為0:

1. 在以下位置建立檔案 `src\conf.d\available_vhosts`

1. 將以下內容添加到檔案中以設定年齡頭

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. 保存並關閉檔案。
1. 修改軟連結 `src\conf.d\enabled_vhosts\default.vhost` 指向新檔案。
