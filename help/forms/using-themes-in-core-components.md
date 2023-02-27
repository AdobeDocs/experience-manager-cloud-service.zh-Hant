---
title: 建立和使用主題
description: 您可以使用主題來使用核心元件，使用樣式化並為適用性表單提供視覺識別。 您可以在任意數量的適用性Forms中共用主題。
source-git-commit: 0205ffeabcb422ad70fd9439a1af246f438c52d5
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---


# 適用性Forms的主題（核心元件） {#themes-for-af-using-core-components}

您可以使用核心元件建立並套用主題，使最適化表單變得樣式。 主題包含元件和面板的樣式詳細資料。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 應用主題時，指定的樣式會反映在相應的元件上。 主題可獨立管理，不需參考適用性表單。

當您 [建立最適化表單](/help/forms/creating-adaptive-form.md) 使用核心元件時，現成主題會顯示在 **樣式** 標籤。 依預設，僅 **畫布** 主題。

>[!NOTE]
>
>不應將適用性表單主題與 [最適化表單範本。](/help/forms/template-editor.md) 適用性表單主題僅包含適用性表單的樣式資訊。 最適化表單範本可定義表單結構和初始內容，並包含主題，以便建立新的 [最適化表單。](/help/forms/creating-adaptive-form.md)

## 使用核心元件在適用性Forms中使用畫布主題 {#using-theme-in-adaptive-form}

將主題套用至適用性表單的步驟如下：

1. 登入您的AEM Forms製作例項。

1. 點選 **Adobe Experience Manager** > **Forms** > **Forms與檔案**.

1. 按一下 **建立** > **適用性Forms**. 建立最適化表單的精靈隨即開啟。

1. 在 **來源** 標籤。

   >[!NOTE]
   >
   > 當您建立具有核心元件的適用性表單時，您會在「樣式」標籤下看到畫布主題。 這是目前唯一可用的立即可用主題。 但您可以根據自己的喜好改變主題，並借由設定前端管道來儲存主題以供日後使用。

1. 在 **樣式** 標籤。
1. 按一下&#x200B;**建立**。

最適化表單主題是「最適化表單」範本的一部分，用於在建立最適化表單時定義樣式。

## 自訂主題 {#customizing-theme}

若要自訂主題，

* [在Cloud Manager中設定管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* 使用 [貢獻者角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* 您應該有 [Git基本知識](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) 和Cloud ServiceGit存放庫。

若要自訂畫布主題：
1. [複製畫布主題](#1-download-canvas-theme-download-canvas-theme)
1. [了解主題的結構](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [在package.json和package_lock.json中變更名稱](#changename-packagelock-packagelockjson)
1. [建立 ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [啟動本地代理伺服器](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [自訂主題](#customize-the-theme-customizing-theme)
1. [提交更改](#6-committing-the-changes-committing-the-changes)
1. [部署管道](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1.複製畫布主題 {#download-canvas-theme}

開啟命令提示字元並執行下列命令以複製畫布主題：

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> 「表單建立精靈」的「樣式」索引標籤會顯示與package.json檔案中相同的主題名稱。

### 2.了解主題的結構 {#structure-of-canvas-theme}

適用性表單主題是包含CSS、JavaScript和靜態資源的套件，這些資源定義表單的樣式並符合適用性表單主題的結構。 適用性表單主題具有以下前端專案的典型結構：

* `src/components`:AEM核心元件專用的JavaScript和CSS檔案
* `src/resources`:靜態檔案，例如圖示、標誌和字型
* `src/site`:套用至整個AEM Sites頁面的JavaScript和CSS檔案
* `src/theme.ts`:JavaScript和CSS主題的主要入口點
* `src\theme.scss`:套用至整個主題的JavaScript和CSS檔案

此 `src/components` 資料夾中有專供所有AEM核心元件（例如按鈕、核取方塊、容器、頁尾等）使用的JavaScript和CSS檔案。 您可以編輯AEM元件專用的CSS檔案，以設定按鈕或核取方塊的樣式。

![編輯主題](/help/forms/assets/theme_structure.png)

若要自訂主題，您可以啟動本機Proxy伺服器，以根據實際AEM內容即時查看主題自訂。

### 4.變更畫布主題的package.json和package_lock.json中的名稱 {#changename-packagelock-packagelockjson}

更新 `package.json` 和 `package_lock.json` 檔案。

>[!NOTE]
>
> 名稱不應具有 `@aemforms` 標籤。 簡單文字應為使用者提供的名稱。

![畫布主題圖片](/help/forms/assets/changename_canvastheme.png)

### 3.在主題資料夾中建立.env檔案 {#creating-env-file-theme-folder}

建立 `.env` 檔案，並新增下列參數：

* **AEM url**
AEM_URL=https://[author-instance]

* **AEM網站名稱**
AEM_ADAPTIVE_FORM=Form_name

* **AEM代理埠**
AEM_PROXY_PORT=7000


![畫布主題結構](/help/forms/assets/env-file-canvas-theme.png)

### 4.啟動本地代理伺服器 {#starting-a-local-proxy-server}

1. 從命令列，導覽至本機電腦上主題的根目錄。
1. 執行 `npm install` npm會擷取相依性並安裝專案。
1. 執行 `npm run live` 代理伺服器啟動。

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. 點選或按一下 **本機登入（僅限管理工作）** 並使用AEM管理員提供給您的proxy使用者憑證登入。

   ![在本機登入](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * 建立本機使用者以在本機登入。 為主題設計人員提供貢獻者角色。
   > * 如果您將AEM URL指定為 `http://localhost:[port]/` 在 `.env` 檔案，系統會直接將您重新導向至瀏覽器。


1. 登入後，請變更瀏覽器中的URL，以指向AEM管理員提供給您的範例內容的路徑。

   * 例如，如果提供的路徑是 `/content/formname.html?wcmmode=disabled`，請將URL變更為 `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![代理範例內容](/help/forms/assets/sample_af.png)

導覽至適用性表單，查看套用至適用性表單的畫布主題。

### 5.自訂主題 {#customize-theme}

1. 在編輯器中，開啟檔案 `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > 您可以編輯 `site/_variables.scss` 檔案。

1. 編輯 `font colour` to `red`.

   ![編輯主題](/help/forms/assets/edit_theme.png)

   **設定不同AEM元件的樣式**

   您可以在編輯器中變更適用性表單的CSS檔案，以設定其不同元件的樣式。 「畫布主題」資料夾中，每個適用性表單核心元件有不同的CSS資料夾。

   ![核心元件](/help/forms/assets/theme-component.png)

   若要在主題編輯器中指定特定元件的樣式，您可以在主題資料夾中編輯CSS。 例如，如果要更改文本框欄位的邊框顏色，請在編輯器中開啟CSS檔案並更改其邊框顏色。

   ![編輯文本框CSS](/help/forms/assets/edit_color_textbox.png)

1. 儲存檔案時，代理伺服器會透過該行識別變更 `[Browsersync] File event [change]`.

   ![代理瀏覽器同步](/help/forms/assets/browser_sync.png)

1. 切換回本機代理伺服器的瀏覽器後，變更會立即顯示。

   ![更改AF主題](/help/forms/assets/edit_theme_af.png)

主題設計器預覽本地代理伺服器中的更改並根據不同AEM元件的要求定制主題。

將變更提交至AEM Git存放庫前，您必須先存取 [Git存放庫資訊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 6.提交更改 {#committing-the-changes}

變更主題並使用本機Proxy伺服器進行測試後，請將變更提交至AEM FormsCloud Service的Git存放庫。 它可讓您的FormsCloud Service環境中提供自訂主題，供適用性Forms作者使用。

在提交變更至AEM FormsCloud Service的Git存放庫前，您必須先在本機電腦上複製存放庫。 複製儲存庫：

1. 按一下 **[!UICONTROL 儲存庫]** 選項。

   ![建立新主題存放庫](/help/forms/assets/createrepo_canvastheme.png)

1. 按一下 **[!UICONTROL 添加儲存庫]** 和指定 **儲存庫名稱** 在 **添加儲存庫** 對話框。 按一下「**[!UICONTROL 儲存]**」。

   ![新增畫布主題存放庫](/help/forms/assets/addcanvasthemerepo.png)

1. 按一下 **[!UICONTROL 複製儲存庫URL]** 複製已建立存放庫的URL。

   ![畫布主題URL](/help/forms/assets/copyurl_canvastheme.png)

1. 開啟命令提示字元，然後複製上述建立的雲端存放庫。

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. 使用類似於的命令，將您正在編輯的主題儲存庫檔案移至雲端儲存庫
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
例如，使用此命令 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. 在雲儲存庫的目錄中，使用以下命令提交您移入的主題檔案。

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. 自訂項目會推送至Git存放庫。

   ![提交的更改](/help/forms/assets/cmd_git_push.png)

您的自訂內容現在可安全地儲存在Git存放庫。


### 7.運行前端管道 {#deploy-pipeline}

1. 建立前端管道以部署自訂主題。 學習 [如何建立一條前線管道，以部署定制主題](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. 執行已建立的前端管道，以在 **[!UICONTROL 樣式]** 「適用性表單建立」精靈的索引標籤。

>[!NOTE]
>
>未來若您在畫布主題資料夾中進行任何修改，則需要再次重新執行上述管道。 因此，必須記住管道的名稱。

## 自訂主題的範例 {#example-to-customize-a-theme}

1. 登入您的AEM Forms製作例項。
1. 開啟使用核心元件建立的適用性表單。
1. 使用命令提示符啟動本地代理伺服器，然後按一下 **本機登入（僅限管理工作）**.
1. 登入後，系統會將您重新導向至瀏覽器，並查看套用的主題。
1. 下載 [畫布主題](https://github.com/adobe/aem-forms-theme-canvas) 並解壓縮下載的zip資料夾。
1. 在您偏好的編輯器中開啟解壓縮的zip資料夾。
1. 建立 `.env` 檔案，然後新增參數： **AEM URL**, **AEM_ADAPTIVE_FORM** 和 **AEM_PROXY_PORT**.
1. 在「畫布」主題資料夾中開啟文字方塊的CSS檔案，並變更其邊框顏色以顯示 `red` 顏色並儲存變更。
1. 再次重新開啟瀏覽器，您會看到變更會立即反映在最適化表單中。
1. 將畫布主題資料夾移至複製的存放庫。
1. 提交更改並運行前端管道。

管道執行後，主題即可在樣式標籤下使用。

## 最佳實務 {#best-practices}

* **避免資產出現在其他主題**

   編輯主題時，您可以瀏覽並新增其他主題的資產（例如影像）。 例如，您正在編輯頁面的背景。 例如，當您選取 **[!UICONTROL 頁面]** ![編輯按鈕](assets/edit-button.png)> **[!UICONTROL 背景]** > **[!UICONTROL 新增]** > **[!UICONTROL 影像]**，您會看到一個對話方塊，可讓您瀏覽和新增其他主題中的影像。

   如果從另一個主題新增資產，而移動或刪除另一個主題，您可能會面臨目前主題的問題。 建議您避免瀏覽及新增其他主題中的資產。

* **變更容器面板版面寬度**

   不建議變更容器面板配置寬度。 當您指定容器面板的寬度時，它會變成靜態，且不會適應不同的顯示。

* **使用表單編輯器或主題編輯器處理頁首和頁尾**

   如果要使用字型樣式、背景和透明度等樣式選項來設定頁眉和頁腳的樣式，請使用主題編輯器。
如果您想要提供標誌影像、頁首中的公司名稱、頁尾中的版權資訊等資訊，請使用表單編輯器選項。
