---
title: 建立和使用主題
description: 您可以使用主題來使用核心元件對自適應表單進行風格化和提供視覺標識。 您可以在任意數量的自適應Forms中共用主題。
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---

# 適應性Forms主題（核心元件） {#themes-for-af-using-core-components}

您可以建立和應用主題，以使用核心元件設計自適應表單的樣式。 主題包含元件和面板的樣式詳細資訊。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 應用主題時，指定的樣式會反映在相應的元件上。 主題是獨立管理的，而不引用自適應表單。

當你 [建立自適應窗體](/help/forms/creating-adaptive-form.md) 使用核心元件時，「現成」主題顯示在 **樣式** 頁籤。 預設情況下，僅 **畫布** 的雙曲餘切值。

>[!NOTE]
>
>不應將自適應表單主題與 [自適應表單模板。](/help/forms/template-editor.md) 「自適應表單」主題僅包含「自適應表單」的樣式資訊。 自適應表單模板定義表單結構和初始內容並包含主題，以允許建立新的表單 [自適應窗體。](/help/forms/creating-adaptive-form.md)

## 使用核心元件在自適應Forms中使用Canvas主題 {#using-theme-in-adaptive-form}

將主題應用於自適應表單的步驟包括：

1. 登錄到您的AEM Forms作者實例。

1. 點擊 **Adobe Experience Manager** > **Forms** > **Forms和文檔**。

1. 按一下 **建立** > **自適應Forms**。 將開啟用於建立「自適應表單」的嚮導。

1. 在 **源** 頁籤。

   >[!NOTE]
   >
   > 建立具有核心元件的自適應表單時，將在「樣式」頁籤下看到「畫布」主題。 這是目前唯一可用的現成主題。 但是，您可以根據自己的喜好更改主題，並通過設定前端管道將其保存以備將來使用。

1. 在 **樣式** 頁籤。
1. 按一下&#x200B;**建立**。

「自適應表單」主題用作「自適應表單」模板的一部分，用於在建立「自適應表單」時定義樣式。

## 自定義主題 {#customizing-theme}

要自定義主題，

* [在Cloud Manager中設定管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* 使用 [貢獻者角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html)。
* 你應該有 [Git的基本知識](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) 和Cloud ServiceGit儲存庫。

要自定義畫布主題：
1. [克隆畫布主題](#1-download-canvas-theme-download-canvas-theme)
1. [瞭解主題的結構](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [更改package.json和package_lock.json中的名稱](#changename-packagelock-packagelockjson)
1. [建立 ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [啟動本地代理伺服器](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [自定義主題](#customize-the-theme-customizing-theme)
1. [提交更改](#6-committing-the-changes-committing-the-changes)
1. [部署管道](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1。克隆畫布主題 {#download-canvas-theme}

開啟命令提示符並運行以下命令以克隆畫布主題：

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> 「建立表單嚮導」的「樣式」頁籤顯示的主題名稱與package.json檔案中的主題名稱相同。

### 2.瞭解主題的結構 {#structure-of-canvas-theme}

自適應表單主題是包含CSS、JavaScript和靜態資源的包，這些資源定義表單的樣式並遵循自適應表單主題的結構。 自適應表單主題具有以下前端項目的典型結構：

* `src/components`:特定於核心元件的JavaScript和AEMCSS檔案
* `src/resources`:靜態檔案，如表徵圖、徽標和字型
* `src/site`:應用於整個AEM Sites頁的JavaScript和CSS檔案
* `src/theme.ts`:JavaScript和CSS主題的主要入口點
* `src\theme.scss`:適用於整個主題的JavaScript和CSS檔案

的 `src/components` 資料夾具有特定於所有核心元件(如按鈕、復AEM選框、容器、頁腳等)的JavaScript和CSS檔案。 可以通過編輯特定於元件的CSS檔案來設定按鈕或復AEM選框樣式。

![編輯主題](/help/forms/assets/theme_structure.png)

要自定義主題，可以啟動本地代理伺服器以根據實際內容即時查看主AEM題自定義。

### 3.更改畫布主題的package.json和package_lock.json中的名稱 {#changename-packagelock-packagelockjson}

在中更新畫布主題的名稱和版本 `package.json` 和 `package_lock.json` 的子菜單。

>[!NOTE]
>
> 名稱不應 `@aemforms` 標籤。 它應該是簡單文本，作為用戶提供的名稱。

![畫布主題圖片](/help/forms/assets/changename_canvastheme.png)

### 4.在主題資料夾中建立.env檔案 {#creating-env-file-theme-folder}

建立 `.env` 檔案，並添加以下參數：

* **AEMurl**
AEM_URL=https://[作者實例]

* **AEM站點名稱**
AEM_ADAPTIVE_FORM=表單名稱

* **AEM代理埠**
AEM_PROXY_PORT=7000


![畫布主題結構](/help/forms/assets/env-file-canvas-theme.png)

### 5.啟動本地代理伺服器 {#starting-a-local-proxy-server}

1. 從命令行導航到本地電腦上主題的根。
1. 執行 `npm install` npm檢索依賴項並安裝項目。
1. 執行 `npm run live` 代理伺服器啟動。

   ![npm運行即時](/help/forms/assets/theme_proxy.png)


1. 點擊或按一下 **本地登錄（僅限管理任務）** 並使用管理員提供給您的代理用戶憑據登AEM錄。

   ![本地登錄](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * 建立本地用戶以本地登錄。 為主題設計器提供參與者角色。
   > * 如果將AEMURL指定為 `http://localhost:[port]/` 的 `.env` 檔案，您將直接重定向到瀏覽器。


1. 登錄後，請更改瀏覽器中的URL以指向管理員提供給您的示例內AEM容的路徑。

   * 例如，如果提供的路徑是 `/content/formname.html?wcmmode=disabled`，將URL更改為 `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![代理樣本內容](/help/forms/assets/sample_af.png)

導航到自適應表單以查看應用於自適應表單的畫布主題。

### 6。自定義主題 {#customize-theme}

1. 在編輯器中，開啟檔案 `<your-theme-sources>/src/site/_variables.scss`。

   >[!NOTE]
   >
   > 通過編輯 `site/_variables.scss` 的子菜單。

1. 編輯 `font colour` 至 `red`。

   ![編輯主題](/help/forms/assets/edit_theme.png)

   **設定不同組AEM件的樣式**

   通過在編輯器中更改Adaptive Form的CSS檔案，可以對其不同元件進行樣式化。 Canvas Theme資料夾中每個Adaptive Form核心元件有不同的CSS資料夾。

   ![核心部件](/help/forms/assets/theme-component.png)

   要在主題編輯器中指定特定元件的樣式，可以在主題資料夾中編輯CSS。 例如，如果要更改文本框欄位的邊框顏色，請在編輯器中開啟CSS檔案並更改其邊框顏色。

   ![編輯文本框CSS](/help/forms/assets/edit_color_textbox.png)

1. 保存檔案時，代理伺服器通過線路識別更改 `[Browsersync] File event [change]`。

   ![代理瀏覽器同步](/help/forms/assets/browser_sync.png)

1. 切換回本地代理伺服器的瀏覽器後，更改立即可見。

   ![更改AF主題](/help/forms/assets/edit_theme_af.png)

主題設計器預覽本地代理伺服器中的更改，並根據不同元件的要求定制主AEM題。

在將更改提交到AEMGit儲存庫之前，您需要訪問 [Git儲存庫資訊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)。

### 7。提交更改 {#committing-the-changes}

對主題進行更改並使用本地代理伺服器對其進行測試後，將更改提交到您的AEM FormsCloud Service的Git儲存庫。 它使自定義主題可在您的FormsCloud Service環境中提供，供適應性Forms作者使用。

在將更改提交到AEM FormsCloud Service的Git儲存庫之前，您需要在本地電腦上克隆該儲存庫。 要克隆儲存庫，請執行以下操作：

1. 通過按一下 **[!UICONTROL 儲存庫]** 的雙曲餘切值。

   ![新建主題回購](/help/forms/assets/createrepo_canvastheme.png)

1. 按一下 **[!UICONTROL 添加儲存庫]** 並指定 **儲存庫名稱** 的 **添加儲存庫** 對話框。 按一下「**[!UICONTROL 儲存]**」。

   ![添加畫布主題回購](/help/forms/assets/addcanvasthemerepo.png)

1. 按一下 **[!UICONTROL 複製儲存庫URL]** 複製已建立儲存庫的URL。

   ![畫布主題URL](/help/forms/assets/copyurl_canvastheme.png)

1. 開啟命令提示符並克隆上面建立的雲儲存庫。

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. 使用類似於
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
例如，使用此命令 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. 在雲儲存庫的目錄中，使用以下命令提交已移入的主題檔案。

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. 將自定義項推送到Git儲存庫。

   ![提交的更改](/help/forms/assets/cmd_git_push.png)

您的自定義內容現在安全地儲存在Git儲存庫中。


### 8.運行前端管線 {#deploy-pipeline}

1. 建立前端管道以部署自定義主題。 學習 [如何設定前線管道以部署自定義主題](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)。
1. 運行建立的前端管道以在 **[!UICONTROL 樣式]** 頁籤。

>[!NOTE]
>
>將來，如果在「畫布」主題資料夾中進行任何修改，則需要重新運行上述管道。 因此，必須記住管線的名稱。

## 自定義主題的示例 {#example-to-customize-a-theme}

1. 登錄到您的AEM Forms作者實例。
1. 開啟使用核心元件建立的自適應表單。
1. 使用命令提示符啟動本地代理伺服器，然後按一下 **本地登錄（僅限管理任務）**。
1. 登錄後，您將被重定向到瀏覽器並查看應用的主題。
1. 下載 [畫布主題](https://github.com/adobe/aem-forms-theme-canvas) 並解壓縮下載的zip資料夾。
1. 在首選編輯器中開啟解壓縮的zip資料夾。
1. 建立 `.env` 檔案，並添加參數： **URLAEM**。 **AEM_ADAPTIVE_FORM** 和 **AEM代理埠**。
1. 開啟「畫布」主題資料夾中文本框的CSS檔案，並更改其邊框顏色 `red` 顏色並保存更改。
1. 再次重新開啟瀏覽器，您會看到這些更改會立即反映在自適應表單中。
1. 將畫布主題資料夾移到克隆的儲存庫中。
1. 提交更改並運行前端管線。

管線執行後，「樣式」(Style)頁籤下將顯示主題。

## 最佳做法 {#best-practices}

* **避免資產來自其他主題**

   編輯主題時，可以瀏覽和添加來自其他主題的資源（如影像）。 例如，您正在編輯頁面的背景。 例如，當您選擇 **[!UICONTROL 頁面]** ![編輯按鈕](assets/edit-button.png)> **[!UICONTROL 背景]** > **[!UICONTROL 添加]** > **[!UICONTROL 影像]**，您將看到一個對話框，該對話框允許您瀏覽和添加其他主題中的影像。

   如果從另一個主題添加資產，並且移動或刪除了另一個主題，則您可能會面臨當前主題的問題。 建議您避免瀏覽和添加來自其他主題的資產。

* **更改容器面板佈局寬度**

   不建議更改容器面板佈局寬度。 指定容器面板的寬度時，它將變為靜態，不適應不同的顯示。

* **使用表單編輯器或主題編輯器處理頁眉和頁腳**

   如果要使用樣式選項（如字型樣式、背景和透明度）對頁眉和頁腳進行樣式化，請使用主題編輯器。
如果要提供徽標影像、頁眉中的公司名稱和頁腳中的版權資訊等資訊，請使用表單編輯器選項。
