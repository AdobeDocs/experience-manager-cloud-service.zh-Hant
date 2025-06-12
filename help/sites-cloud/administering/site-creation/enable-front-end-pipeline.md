---
title: 啟用前端管道
description: 瞭解如何啟用現有網站的前端管道，以使用網站主題，更快地自訂您的網站。
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 啟用前端管道 {#enable-front-end-pipeline}

{{traditional-aem}}

瞭解如何啟用現有網站的前端管道，以使用網站主題，更快地自訂您的網站。

## 概觀 {#overview}

前端管道是一種機制，可根據[網站主題](site-themes.md)和[網站範本](site-templates.md)，快速部署您網站的前端程式碼。

此管道僅處理前端計畫碼，這使得部署過程比完整棧疊部署更快。 它可讓前端開發人員輕鬆自訂您的網站，而不需要瞭解AEM。

根據網站範本的網站預設可以使用前端管道。 本檔案說明如何調整現有網站以利用前端管道。

>[!TIP]
>
>如果您不熟悉前端管道以及如何使用它和網站範本來快速部署網站，請參閱[快速網站建立歷程](/help/journey-sites/quick-site/overview.md)以取得簡介。

AEM可將您的網站設定為載入使用前端管道部署的主題，即使您的網站不是使用網站範本和主題建立的，方法是將其分層到現有使用者端資料庫上。

## 技術細節 {#technical-details}

當您啟動網站的前端管道時，AEM會對您的網站結構做出以下變更。

* 網站的所有頁面都包含一個額外的CSS和JS檔案，您可以透過專用的Cloud Manager前端管道部署更新來修改這些檔案。
* 新增的CSS和JS檔案最初是空的。 不過，您可以下載「主題來源」資料夾，以設定透過管道部署CSS和JS程式碼更新所需的資料夾結構。
* 只有開發人員可以復原變更，方法是刪除此作業在`/conf/<site-name>/sling:configs`下方建立的`SiteConfig`和`HtmlPageItemsConfig`節點。

>[!NOTE]
>
>此動作不會自動將網站的現有使用者端程式庫轉換為使用前端管線。 將這些來源從使用者端程式庫資料夾移至前端管道資料夾是一項需要前端開發人員手動執行的任務。

## 要求 {#requirements}

AEM可以自動調整您的現有網站以使用前端管道。 若要執行此工作流程，您的網站必須使用[v2或更新版本的核心元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/wcm-components/page)的頁面元件。

## 啟用前端管道 {#enabling}

{{add-cm-allowlist-frontend-pipeline}}

使用[網站邊欄](site-rail.md)從Sites主控台啟用您的網站。

1. 登入AEM並透過&#x200B;**全域導覽** > **網站**&#x200B;瀏覽您的網站。
1. 在主控台中選取您的網站。 選取網站的根目錄，而非任何子頁面。
1. 選取您的網站後，請開啟左側的[邊欄選取器](/help/sites-cloud/authoring/basic-handling.md#rail-selector)，然後選擇&#x200B;**網站**。
1. 在&#x200B;**站台**&#x200B;邊欄中，按一下&#x200B;**啟用前端管道**&#x200B;按鈕。

   ![啟用前端管道](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM會提示您確認已進行變更的概述。 確認並調整您的網站。

現在，您的網站已準備好使用前端管道。 若要深入瞭解前端管道和管理您的網站主題，請參閱：

* [使用網站邊欄管理您的網站主題](site-rail.md)
* [快速網站建立歷程](/help/journey-sites/quick-site/overview.md) — 此檔案歷程為您提供使用前端管道和快速網站建立工具來快速部署網站的程式從頭到尾的概觀。
* [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) — 本檔案說明完整棧疊和Web層管道內容中的前端管道。

## 前端管道和自訂網域 {#custom-domains}

前端管道可與[Cloud Manager的自訂網域功能](/help/implementing/cloud-manager/custom-domain-names/introduction.md)搭配使用，但將這兩項功能搭配使用時，請注意下列需求。

### 靜態前端檔案 {#static-files}

依預設，透過Front-End Pipeline部署的靜態前端資產，會從Adobe預先定義的靜態網域提供服務。

如果您需要前端資產的自訂網域，可以在發佈層上安裝自訂網域，並設定Dispatcher將特定路徑（例如`/static/`）路由到Adobe的靜態託管位置。 此方法需要更新您的[Dispatcher規則](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-dispatcher/using/dispatcher)，才能正確轉送及快取靜態資產的請求。

設定自訂網域和Dispatcher後，您可以設定AEM以從靜態網域提供前端資產。

### 設定 {#configuration}

如[技術詳細資料](#technical-details)區段中所述，啟用網站的前端管道功能會在`/conf/<site-name>/sling:configs`下建立`SiteConfig`和`HtmlPageItemsConfig`節點。

如果您想要將Cloud Manager的自訂網域功能用於您的網站，並搭配前端管道用於狀態資產，則必須將其他屬性新增到這些節點。

1. 設定網站`SiteConfig`中的`customFrontendPrefix`屬性。
   1. 導覽至 `/conf/<site-name>/sling:configs/com.adobe.aem.wcm.site.manager.config.SiteConfig`。
   1. 新增或更新屬性`customFrontendPrefix = "https://your-custom-domain.com/static/"`。
1. 這會以自訂網域更新`HtmlPageItemsConfig`的`prefixPath`值。
   1. 導覽至 `/conf/<site-name>/sling:configs/com.adobe.cq.wcm.core.components.config.HtmlPageItemsConfig`。
   1. 驗證`prefixPath`是否反映您的自訂網域，例如`prefixPath = "https://your-custom-domain.com/static/<hash>/..."`。
   * 您也可以視需要手動覆寫此值。
1. 驗證您的設定。
   1. 部署後，請檢查頁面是否正確參考自訂網域中的主題成品。
   1. 開啟瀏覽器的開發人員工具，並檢查`theme.css`和`theme.js`檔案路徑，確認它們是否從正確的網域載入。

接著網站的頁面會參照該更新URL中的主題人工因素。 然後Dispatcher會將這些資源的請求路由到靜態網域。

## 前端開發人員的最佳作法 {#best-practices}

如果您需要在透過前端管道部署之前在本機開發和測試前端資產，請考慮以下方法：

* 使用[網站主題產生器的Proxy模式](https://github.com/adobe/aem-site-theme-builder?tab=readme-ov-file#proxy)，在本機覆寫主題成品以進行測試。
* 從本機開發伺服器手動提供您的佈景主題檔案，並更新`HtmlPageItemsConfig`中的`prefixPath`以符合本機伺服器位址。
* 請確保在測試期間已停用瀏覽器快取以檢視即時更新。

如需本機前端開發的詳細資訊，請參閱[網站主題產生器檔案。](https://github.com/adobe/aem-site-theme-builder)
