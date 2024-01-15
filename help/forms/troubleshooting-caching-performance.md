---
title: 如何針對AEM Formsas a Cloud Service的快取相關問題進行疑難排解？
description: 疑難排解AEM Formsas a Cloud Service的快取相關問題。
contentOwner: khsingh
feature: Adaptive Forms, Troubleshooting
role: User
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 1%

---

# 快取效能 {#caching-performance}

在Cloud Service環境中設定或使用最適化Forms快取時，您可能會遇到下列一些問題：

## 某些包含影像或影片的最適化Forms不會從Dispatcher快取中自動失效 {#images-videos-not-invalidated}

您可以從資產瀏覽器選取影像或影片，並將其新增至最適化表單。 在資產編輯器中編輯這些影像時，包含這些影像的最適化表單的快取版本不會失效。 最適化表單會繼續顯示較舊的影像。

若要解決此問題，請在發佈影像和視訊後，明確取消發佈並發佈參照這些資產的最適化Forms。

## 某些包含內容片段或體驗片段的自適應Forms不會從Dispatcher快取中自動失效 {#content-fragments-experience-fragments-not-invalidated}

您可以將內容片段或體驗片段新增至最適化表單。 當這些片段被獨立編輯和發佈時，包含這些片段的快取版Adaptive Form不會失效。 最適化表單會繼續顯示較舊的片段。

若要解決此問題，請在發佈更新的內容片段或體驗片段後，明確取消發佈並發佈使用這些資產的Adaptive Forms。

## 僅快取Adaptive Forms的第一個執行個體 {#only-first-instance-cached}

當最適化表單URL不包含任何本地化資訊，且啟用Configuration Manager中的「使用瀏覽器地區設定」選項時，將會提供本地化版本的Adaptive Form，並根據第一個請求（請求瀏覽器地區設定）快取最適化表單的例項並傳送給每個後續使用者。

執行以下步驟以解決問題：

1. 開啟您的Experience Manager專案。
1. 開啟 `dispatcher/scr/conf.d/rewrites/rewrite.rules` 以進行編輯。
1. 開啟 `conf.d/httpd-dispatcher.conf` 或任何其他設定為在執行階段載入的組態檔。
1. 將下列程式碼新增至您的檔案並儲存。 此範常式式碼會加以修改以符合您的環境。

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two characters which most likely are the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## CDN快取在300秒後停止運作 {#cdn-caching-stops-working-after-300-seconds}

CDN快取在300秒後停止運作，所有對CDN上快取的請求都會重新導向到Dispatcher。

若要解決此問題，請將age標頭設為0：

1. 建立檔案於 `src\conf.d\available_vhosts`

1. 將以下內容新增到檔案以設定age標頭

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. 儲存並關閉檔案。
1. 修改以下專案的軟連結： `src\conf.d\enabled_vhosts\default.vhost` 以指向新檔案。
