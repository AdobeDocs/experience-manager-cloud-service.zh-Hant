---
title: 自訂網站主題
description: 了解網站主題的建立方式、如何自訂，以及如何使用即時AEM內容進行測試。
exl-id: b561bee0-3a64-4dd3-acb8-996f0ca5bfab
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# 自訂網站主題 {#customize-the-site-theme}

了解網站主題的建立方式、如何自訂，以及如何使用即時AEM內容進行測試。

## 迄今為止的故事 {#story-so-far}

在AEM快速網站建立歷程的上一份檔案中， [擷取Git存放庫存取資訊，](retrieve-access.md) 您了解前端開發人員使用者Cloud Manager如何存取git存放庫資訊，現在您應：

* 從高層次了解Cloud Manager是什麼。
* 已擷取您的認證以存取AEM Git，以便您提交自訂。

此部分的歷程會進行下一個步驟，並深入探討網站主題，並示範如何自訂，然後使用您擷取的存取憑證來提交這些自訂。

## 目標 {#objective}

本檔案說明如何建立AEM網站主題、如何自訂主題，以及如何使用即時AEM內容測試主題。 閱讀後，您應：

* 了解網站主題的基本結構及編輯方式。
* 請參閱如何透過本機Proxy，使用真實的AEM內容來測試您的主題自訂。
* 了解如何將變更提交至AEM Git存放庫。

## 負責角色 {#responsible-role}

此部分的歷程適用於前端開發人員。

## 了解主題結構 {#understand-theme}

將AEM管理員提供的主題解壓縮至您要編輯主題的位置，並在您偏好的編輯器中開啟該主題。

![編輯主題](assets/edit-theme.png)

主題是典型的前端項目。 結構中最重要的部分是：

* `src/main.ts`:JS和CSS主題的主要入口點
* `src/site`:套用至整個網站的JS和CSS檔案
* `src/components`:AEM元件專用的JS和CSS檔案
* `src/resources`:靜態檔案，例如圖示、標誌和字型

>[!TIP]
>
>若想進一步了解標準AEM網站主題，請參閱 [其他資源](#additional-resources) 部分。

熟悉主題專案的結構後，請啟動本機Proxy，以便根據實際AEM內容即時查看任何主題自訂。

## 啟動本地代理 {#starting-proxy}

1. 從命令列，導覽至本機電腦上主題的根目錄。
1. 執行 `npm install` npm會擷取相依性並安裝專案。

   ![npm安裝](assets/npm-install.png)

1. 執行 `npm run live` 代理伺服器啟動。

   ![npm run live](assets/npm-run-live.png)

1. 代理伺服器啟動時，會自動開啟瀏覽器以 `http://localhost:7001/`. 點選或按一下 **本機登入（僅限管理工作）** 並使用AEM管理員提供給您的proxy使用者憑證登入。

   ![在本機登入](assets/sign-in-locally.png)

1. 登入後，請變更瀏覽器中的URL，以指向AEM管理員提供給您的範例內容的路徑。

   * 例如，如果提供的路徑是 `/content/<your-site>/en/home.html?wcmmode=disabled`
   * 您可將URL變更為 `http://localhost:7001/content/<your-site>/en/home.html?wcmmode=disabled`

   ![代理範例內容](assets/proxied-sample-content.png)

您可以導覽網站以探索內容。 網站會從即時AEM例項中即時提取，以便您可以根據實際內容自訂主題。

## 自訂主題 {#customize-theme}

現在您可以開始自訂主題。 以下是簡單範例，說明如何透過Proxy即時查看變更。

1. 在編輯器中，開啟檔案 `<your-theme-sources>/src/site/_variables.scss`

   ![編輯主題](assets/edit-theme.png)

1. 編輯變數 `$color-background` 並將其設為白色以外的值。 在此範例中， `orange` 中所有規則的URL區段。

   ![已編輯的主題](assets/edited-theme.png)

1. 儲存檔案時，您會看到Proxy伺服器透過該行辨識變更 `[Browsersync] File event [change]`.

   ![代理瀏覽器同步](assets/proxy-browsersync.png)

1. 切換回代理伺服器的瀏覽器後，變更會立即顯示。

   ![橙色主題](assets/orange-theme.png)

您可以根據AEM管理員提供的需求，繼續自訂主題。

## 提交變更 {#committing-changes}

完成自訂後，您就可以將自訂項目提交至AEM Git存放庫。 首先，必須將存放庫複製到本機電腦。

1. 從命令列，導覽至您要複製存放庫的位置。
1. 執行命令 [先前從Cloud Manager擷取。](retrieve-access.md) 應類似於 `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`. 使用Git使用者名稱和密碼 [您在此歷程的前一部分擷取。](retrieve-access.md)

   ![複製存放庫](assets/clone-repo.png)

1. 使用類似的命令，將您正在編輯的主題專案移至複製的存放庫 `mv <site-theme-sources> <cloned-repo>`
1. 在複製的存放庫目錄中，提交您剛移入的主題檔案，並附上下列命令。

   ```text
   git add .
   git commit -m "Adding theme sources"
   git push
   ```

1. 自訂項目會推送至AEM Git存放庫。

   ![提交的更改](assets/changes-committed.png)

您的自訂內容現在可安全地儲存在AEM Git存放庫。

## 下一步 {#what-is-next}

現在您已完成AEM快速網站建立歷程的這一部分，您應：

* 了解網站主題的基本結構及編輯方式。
* 請參閱如何透過本機Proxy，使用真實的AEM內容來測試您的主題自訂。
* 了解如何將變更提交至AEM Git存放庫。

基於此知識，並透過接下來檢閱檔案，繼續建立AEM快速網站的歷程 [部署自定義主題，](deploy-theme.md) 您將在何處了解如何使用前端管道部署主題。

## 其他資源 {#additional-resources}

建議您透過檢閱檔案，繼續進行快速網站建立歷程的下一個階段 [部署自定義主題，](deploy-theme.md) 以下是一些額外的選用資源，可更深入探討本檔案中提及的一些概念，但您不需要這些資源即可繼續進行歷程。

* [AEM網站主題](https://github.com/adobe/aem-site-template-standard-theme-e2e)  — 這是AEM網站主題的GitHub存放庫。
* [npm](https://www.npmjs.com)  — 用來快速建立網站的AEM主題是以npm為基礎。
* [webpack](https://webpack.js.org)  — 用於快速建立網站的AEM主題依賴webpack。
