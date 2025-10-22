---
title: 自訂網站主題
description: 了解如何建置網站主題、如何自訂網站主題，以及如何使用即時 AEM 內容測試網站主題。
exl-id: b561bee0-3a64-4dd3-acb8-996f0ca5bfab
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: noDisplay, noCatalog
source-git-commit: 8c4b34a77ef85869048fae254728c58cf0d99b66
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 100%

---


# 自訂網站主題 {#customize-the-site-theme}

{{traditional-aem}}

了解如何建置網站主題、如何自訂網站主題，以及如何使用即時 AEM 內容測試網站主題。

## 目前進度 {#story-so-far}

在 AEM 快速建立網站歷程的上一份文件「[擷取 Git 存放庫存取資訊](retrieve-access.md)」中，您已了解前端開發人員如何使用 Cloud Manager 來存取 Git 存放庫資訊，而您現在應該：

* 深入了解 Cloud Manager 是什麼。
* 已擷取您的認證來存取 AEM git，以便您可以提交自訂。

歷程的這個部分將進行下一步，深入研究網站主題並向您說明如何自訂主題，然後使用您擷取的存取認證提交這些自訂內容。

## 目標 {#objective}

本文件說明如何建置 AEM 網站主題、如何自訂網站主題，以及如何使用即時 AEM 內容測試網站主題。閱讀本文件後，您應該：

* 了解網站主題的基本結構以及如何編輯。
* 了解如何透過本機 Proxy 測試使用真實 AEM 內容的主題自訂內容。
* 了解如何將變更提交至 AEM Git 存放庫。

## 負責角色 {#responsible-role}

歷程的這個部分適用於前端開發人員。

## 了解主題結構 {#understand-theme}

將 AEM 管理員提供的主題擷取到您想要編輯主題的位置，並在您的偏好編輯器中將其開啟。

![編輯主題](assets/edit-theme.png)

您會發現主題是一個典型的前端專案。結構最重要的部分是：

* `src/main.ts`：JS &amp; CSS 主題的主要入口點
* `src/site`：套用至整個網站的 JS 和 CSS 檔案
* `src/components`：AEM 元件特定的 JS 和 CSS 檔案
* `src/resources`：圖示、標誌和字體等靜態檔案

>[!TIP]
>
>如果想了解有關標準 AEM 網站主題的更多資訊，請參閱本文件結尾處的「[其他資源](#additional-resources)」區段的 GitHub 連結。

待您熟悉主題專案的結構之後，請啟動本機 Proxy，便可以查看根據實際 AEM 內容的任何主題自訂內容。

## 啟動本機 Proxy {#starting-proxy}

1. 從命令列導航到本機電腦上主題的根目錄。
1. 執行 `npm install`，npm 便會擷取相依性然後安裝專案。

   ![npm install](assets/npm-install.png)

1. 執行 `npm run live` 然後 Proxy 伺服器便啟動。

   ![npm run live](assets/npm-run-live.png)

1. Proxy 伺服器啟動時，會自動開啟瀏覽器至 `http://localhost:7001/`。選取 **SIGN IN LOCALLY (ADMIN TASKS ONLY)** 並使用 AEM 管理員提供給您的 Proxy 使用者認證登入。

   ![本機登入](assets/sign-in-locally.png)

   >[!TIP]
   >
   >如果您沒有這些認證，請與您的管理員聯絡並參考此歷程中[「使用範本建立網站」文章的「設定 Proxy 使用者」區段](/help/journey-sites/quick-site/create-site.md#proxy-user)。

1. 登入後，將瀏覽器中的 URL 變更為指向 AEM 管理員提供給您的範例內容的路徑。

   * 例如，如果提供的路徑是 `/content/<your-site>/en/home.html?wcmmode=disabled`
   * 您將把 URL 變更為 `http://localhost:7001/content/<your-site>/en/home.html?wcmmode=disabled`

   ![由 Proxy 處理的範例內容](assets/proxied-sample-content.png)

您可以導覽網站以探索內容。網站是從即時 AEM 執行個體中即時提取的，所以您可以根據實際內容進行主題自訂。

## 自訂主題 {#customize-theme}

現在您可以開始自訂主題。以下是一個簡單的範例，說明如何透過 Proxy 即時查看變更。

1. 在編輯器中開啟檔案 `<your-theme-sources>/src/site/_variables.scss`

   ![編輯主題](assets/edit-theme.png)

1. 編輯變數 `$color-background` 並將其設為不是白色的值。這個例子使用 `orange`。

   ![已編輯的主題](assets/edited-theme.png)

1. 儲存檔案時，您會看到 Proxy 伺服器透過 `[Browsersync] File event [change]` 這一行識別出變更。

   ![Proxy browsersync](assets/proxy-browsersync.png)

1. 切換回 Proxy 伺服器的瀏覽器，立即可以看見變更。

   ![橘色主題](assets/orange-theme.png)

您可以根據 AEM 管理員提供給您的要求繼續自訂主題。

## 提交改變 {#committing-changes}

自訂完成後，您可以將它們提交到 AEM Git 存放庫。首先您必須將存放庫原地複製到本機電腦。

1. 從命令列導航到您想要原地複製存放庫的位置。
1. 執行您[之前從 Cloud Manager 擷取的](retrieve-access.md)命令。它應該類似於 `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`。使用[您在此歷程的前一部分擷取](retrieve-access.md)的 Git 使用者名稱和密碼。

   ![原地複製存放庫](assets/clone-repo.png)

1. 使用類似於 `mv <site-theme-sources> <cloned-repo>` 的命令，將您正在編輯的主題專案移至原地複製的存放庫中
1. 在原地複製的存放庫目錄中，使用以下指令提交您剛移入的主題檔案。

   ```text
   git add .
   git commit -m "Adding theme sources"
   git push
   ```

1. 自訂內容將推送到 AEM Git 存放庫。

   ![已提交變更](assets/changes-committed.png)

您的自訂內容現已安全地儲存在 AEM Git 存放庫中。

## 下一步 {#what-is-next}

現在您已完成 AEM 快速建立網站歷程的這個部分，您應該：

* 了解網站主題的基本結構以及如何編輯。
* 了解如何透過本機 Proxy 測試使用真實 AEM 內容的主題自訂內容。
* 了解如何將變更提交至 AEM Git 存放庫。

以此知識為基礎並接著檢閱文件「[部署您的自訂主題](deploy-theme.md)」，以繼續您的 AEM 快速建立網站歷程，您可在該文件中了解如何使用前端管道部署主題。

## 其他資源 {#additional-resources}

雖然建議您檢閱文件「[部署您的自訂主題](deploy-theme.md)」以繼續快速建立網站歷程的下一部分，但下列是一些其他選用資源，深入探究了本文件提到的一些概念，不過這些資源並非繼續該歷程的必要條件。

* [AEM 網站主題](https://github.com/adobe/aem-site-template-standard-theme-e2e)- 這是 AEM 網站主題的 GitHub 存放庫。
* [npm](https://www.npmjs.com) - 用於快速建立網站的 AEM 主題以 npm 為基礎。
* [webpack](https://webpack.js.org) - 用於快速建立網站的 AEM 主題以 webpack 為基礎。
