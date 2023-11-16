---
title: 如何在Adaptive Forms中建立和使用主題？
description: 您可以使用主題來設定樣式，並使用核心元件來將視覺身分提供給最適化表單。 您可以在任何數量的最適化Forms中共用主題。
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '2677'
ht-degree: 4%

---

# Adaptive Forms中的主題 {#themes-for-af-using-core-components}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html) |
| AEM as a Cloud Service  | 本文章 |

您可以建立並套用主題來設定最適化表單的樣式。 主題包含元件和面板的樣式詳細資訊。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。套用主題時，指定的樣式會反映在對應的元件上。主題是獨立管理，不需參照最適化表單，且可在多個最適化Forms中重複使用。

## 可用主題

Forms (如Cloud Service所提供)下列核心元件型最適化Forms的主題：

* [畫布主題](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND主題](https://github.com/adobe/aem-forms-theme-wknd)
* [畫架佈景主題](https://github.com/adobe/aem-forms-theme-easel)

## 瞭解主題的結構

主題是一個套件，其中包含定義最適化Forms樣式的CSS檔案、JavaScript檔案和資源（如圖示）。 最適化表單主題會依循特定組織，包含下列元件：

* `src/theme.scss`：此資料夾包含對整個主題有廣泛影響的CSS檔案。 它是定義和管理佈景主題樣式和行為的集中位置。 透過編輯此檔案，您可以進行在整個主題中普遍套用的變更，這會影響最適化Forms和AEM Sites頁面的外觀和功能。

* `src/site`：此資料夾包含套用至整個AEM網站頁面的CSS檔案。 這些檔案包含程式碼和樣式，會影響AEM網站頁面的整體功能和版面。 此處所做的任何修改會反映在您的網站的所有頁面中。 [何時使用？]

* `src/components`：此資料夾中的CSS檔案是針對個別AEM核心元件所設計。 元件的每個專用資料夾都包含 `.scss` 在最適化表單中設定該特定元件樣式的檔案。 例如，/src/components/accordion/_accordion.scss檔案包含Adaptive Forms摺疊式功能表元件的樣式資訊。

  ![最適化表單式主題結構](/help/forms/assets/theme_structure.png)

* `src/resources`：此資料夾包含靜態檔案，例如圖示、標誌和字型。 這些資源用於增強主題的視覺元素和整體設計。

## 建立主題

Forms如Cloud Service所提供，以下是核心元件型最適化Forms的主題。

* [畫布主題](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND主題](https://github.com/adobe/aem-forms-theme-wknd)
* [畫架佈景主題](https://github.com/adobe/aem-forms-theme-easel)

您可以 [自訂任何這些主題以建立新主題](#customize-a-theme-core-components).

![佈景主題自訂的工作流程](/help/forms/assets/workflow-of-customization-of-theme.png)

## 自訂主題 {#customize-a-theme-core-components}

自訂主題是指修改及個人化主題外觀的程式。 自訂主題時，您可以變更其設計元素、版面、顏色、印刷樣式，有時也會變更基礎程式碼。 它可讓您為網站或應用程式建立獨一無二且量身打造的外觀，同時維持主題提供的基本結構和功能。

### 先決條件 {#prerequisites-to-customize}

* 熟悉 [在Cloud Manager中設定管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline) 並且擁有有關如何設定管道的基本知識，可幫助您有效地管理和部署您的主題自訂。
* 瞭解如何 [設定具有貢獻者角色的使用者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html). 瞭解如何使用投稿人角色設定使用者，可讓您授與佈景主題自訂的必要許可權。
* 安裝最新版本的 [Apache Maven。](https://maven.apache.org/download.cgi) Apache Maven是常用於Java™專案的組建自動化工具。 安裝最新版本可確保您擁有佈景主題自訂的必要相依性。
* 安裝純文字編輯器。 例如，Microsoft® Visual Studio Code。 使用純文字編輯器(例如Microsoft® Visual Studio Code)可提供方便使用的環境，用於編輯和修改佈景主題檔案。

### 設定您的環境

* [啟用最適化Forms核心元件](/help/forms/enable-adaptive-forms-core-components.md)  適合您的本機開發和Cloud Service環境。
* 設定 [前端部署管道](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html) 適合您的Cloud Service環境。 或者，您可以稍後設定管道，讓您在設定部署管道之前，靈活地排定測試的優先順序並調整主題。

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

瞭解先決條件並設定開發環境後，您就可以開始根據特定需求自訂主題。

### 自訂主題 {#steps-to-customize-a-theme-core-components}

自訂主題是多步驟的過程。 若要自訂主題，請依照列出的順序執行步驟：

1. [原地複製主題](#download-a-theme-core-components)
1. [設定佈景主題的名稱](#set-name-of-theme)
1. [自訂主題](#customize-the-theme)
1. [測試主題](#test-the-theme)
1. [部署主題](#deploy-the-theme)

檔案中提供的範例是根據 **畫布** 佈景主題，但請務必注意，您可以複製任何佈景主題，並使用相同的指示加以自訂。 這些指示適用於任何主題，可讓您根據特定需求修改主題。

#### 1.原地複製主題 {#download-a-theme-core-components}

若要複製以核心元件為基礎的最適化Forms主題，請選擇下列其中一種主題：

* [畫布主題](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND主題](https://github.com/adobe/aem-forms-theme-wknd)
* [畫架佈景主題](https://github.com/adobe/aem-forms-theme-easel)

若要複製主題，請執行下列指示：

1. 在本機開發環境中開啟命令提示字元或終端機視窗。

1. 執行 `git clone` 複製佈景主題的命令。

   ```
      git clone [Path of Git Repository of the theme]
   ```

   取代 [主題的Git存放庫路徑] 和主題的對應Git存放庫的實際URL

   例如，若要複製畫布主題，請執行下列命令：

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   成功執行命令後，您的電腦上便可在下列位置取得主題的本機復本：  `aem-forms-theme-canvas` 資料夾。


#### 2.設定佈景主題的名稱 {#set-name-of-theme}

1. 以純文字編輯器開啟主題資料夾。 例如，若要開啟 `aem-forms-theme-canvas` Visual Studio程式碼編輯器中的資料夾。

1. 導覽至 `aem-forms-theme-canvas` 檔案夾。

1. 執行以下命令：

   ```
         code .
   ```

   ![以純文字編輯器開啟主題資料夾](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   資料夾會在Visual Studio Code中開啟。

1. 閇啟 `package.json` 檔案進行編輯。

1. 設定 `name` 和 `description` 屬性。

   name屬性用於唯一識別主題，例如&quot;aem-forms-wknd-theme&quot;，並顯示在 **樣式** 標籤之 **表單建立精靈**. description屬性提供有關主題的其他詳細資訊，包括其用途和設計適用的情境。 您也可以指定主題的版本、說明和授權。

1. 儲存並關閉檔案。

![畫布布主題名稱變更影像](/help/forms/assets/changename_canvastheme.png)


#### 3.自訂主題 {#customize-the-theme}

您可以使用佈景主題的全域變數來自訂個別元件或進行佈景主題層級變更。 對全域變數所做的任何變更都會影響所有個別元件。 例如，您可以使用全域變數來變更最適化表單所有元件的邊框顏色，並使用明亮的填色顏色來設定使用按鈕元件的CTA （行動號召）：

* [設定主題層級樣式](#theme-customization-global-level)

* [設定元件層級樣式](#component-based-customization)

##### 設定主題層級樣式{#theme-customization-global-level}

此 `variable.scss` 檔案包含佈景主題的全域變數。 透過更新這些變數，您可以在主題層級進行樣式相關的變更。 若要套用佈景主題層級樣式，請依照下列步驟進行：

1. 閇啟 `<your-theme-sources>/src/site/_variables.scss` 檔案進行編輯。
1. 變更任何屬性的值。 例如，預設的錯誤顏色為 `red`. 若要變更錯誤顏色 `red` 至 `blue`，變更的顏色十六進位代碼 `$errorvariable`. 例如，`$error: #196ee5`。
1. 儲存並關閉檔案。

   ![編輯主題](/help/forms/assets/edit_theme.png)

同樣地，您可以使用 `variable.scss` 檔案來設定字型系列和型別、佈景主題和字型顏色、字型大小、佈景主題間距、錯誤圖示、佈景主題框線樣式，以及其他可影響多個最適化表單元件的變數。

##### 設定元件層級樣式 {#component-based-customization}

您也可以變更特定最適化表單核心元件的字型、顏色、大小和其他CSS屬性。 例如按鈕、核取方塊、容器、頁尾等。 您可以編輯特定元件的CSS檔案來設定按鈕或核取方塊的樣式，使其與貴組織的樣式一致。 若要自訂元件的樣式：

1. 開啟檔案 `<your-theme-sources>/src/components/<component>/<component.scss>` 以進行編輯。 例如，若要變更按鈕元件的字型顏色，請開啟 `<your-theme-sources>/src/components/button/button.scss`，檔案。
1. 根據您的需求變更任何的值。 例如，若要將滑鼠懸停時按鈕元件的顏色變更為 `green`，變更 `color: $white` 中的屬性 `cmp-adaptiveform-button__widget:hover` 類別至十六進位程式碼 `#12B453` 或任何其他陰影 `green`. 最終程式碼如下所示：

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. 儲存並關閉檔案。

   ![編輯文字方塊CSS](/help/forms/assets/edit_color_textbox.png)

   >
   >
   > 在主題和元件層級同時定義樣式時，在元件層級定義的樣式會優先執行。

#### 4.測試自訂主題 {#test-the-theme}

若要預覽和測試本機環境中的變更，並根據不同AEM元件的需求自訂主題，請執行以下步驟：

* 4.1 [設定本機環境以進行測試](#rename-env-file-theme-folder)
* 4.2 [使用本機環境測試主題](#start-a-local-proxy-server)

##### 4.1.設定本機環境以進行測試 {#rename-env-file-theme-folder}

1. 以純文字編輯器開啟主題資料夾。 例如，開啟 `aem-forms-theme-canvas` Visual Studio程式碼編輯器中的資料夾。
1. 重新命名 `env_template` 檔案到 `.env` 檔案並新增下列引數：

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例如，表單的URL為 `http://localhost:4502/editor.html/content/forms/af/contactusform.html`. 因此，的值：

   * AEM_URL = `http://localhost:4502/`
   * AEM_ADAPTIVE_FORM = `contactusform`

1. 儲存檔案。

   ![畫布布主題結構](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2使用本機環境測試主題 {#start-a-local-proxy-server}

1. 導覽至主題資料夾的根目錄。 在此案例中，主題資料夾名稱為 `aem-forms-theme-canvas`.
1. 開啟命令提示或終端機。
1. 執行 `npm install` 以安裝相依性。
1. 執行 `npm run live` 以在本機瀏覽器中預覽具有更新主題的表單。

   >[!NOTE]
   >
   > 如果在執行 `npm run live` 指令，在之前執行以下指令 `npm run live` 命令：
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

這是熱門部署。 因此，無論您何時進行變更並儲存 `_variables.scss` 和 `button.scss` 檔案時，伺服器會自動挑選變更並預覽最新輸出。 直線 `[Browsersync] File event [change]` 表示伺服器已辨識出最新的變更，而且正在部署本機環境的變更。

![Proxy browsersync](/help/forms/assets/browser_sync.png)

在遵循主題層級和元件層級提供的範例進行主題自訂後，最適化表單的錯誤訊息將變更為 `blue` 顏色，而按鈕元件的標籤顏色會變更為 `green` 游標停留時。

**預覽主題層級樣式**

![範例：錯誤顏色設定為藍色](/help/forms/assets/theme-level-changes.png)

**預覽元件層級樣式**

![範例：將游標停留顏色設定為綠色](/help/forms/assets/button-customization.png)

###### 測試Cloud Service環境中託管的表單主題

您也可以測試AEM Formsas a Cloud Service執行個體上託管的最適化表單主題。 若要使用雲端例項上託管的Adaptive Forms來設定和設定本機環境以測試主題，請執行以下步驟：

1. 以純文字編輯器開啟主題資料夾。 例如，開啟 `aem-forms-theme-canvas` Visual Studio程式碼編輯器中的資料夾。
1. 重新命名 `env_template` 檔案到 `.env` 檔案並新增下列引數：

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例如，雲端環境中的表單URL為 `https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html`. 因此，的值：

   * AEM_URL = `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM_ADAPTIVE_FORM = `contactusform`
1. 儲存檔案。
1. 建立本機使用者。

   >[!NOTE]
   >
   > 若要建立本機使用者：
   >
   > * 前往 **[!UICONTROL AEM首頁]** > **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]** .
   > * 確定使用者是 `forms-users` 群組。

1. 導覽至主題資料夾的根目錄。 在此案例中，主題資料夾名稱為 `aem-forms-theme-canvas`.
1. 執行 `npm run live` 系統會將您重新導向至本機瀏覽器。
1. 按一下 `SIGN IN LOCALLY (ADMIN TASKS ONLY)` 並使用本機使用者的憑證登入。

您可以預覽含有最新變更的最適化表單。 一旦您滿意在主題資料夾中完成的修改，請使用前端管道將主題部署到AEM Cloud Service環境。

#### 5.部署主題 {#deploy-the-theme}

若要使用前端管道將主題部署到Cloud Service環境：

* 5.1 [建立主題的存放庫](#create-a-new-theme-repo)
* 5.2 [將變更推送至存放庫](#committing-the-changes)
* 5.3 [執行前端管道](#run-a-frontend-pipeline)

##### 5.1建立主題的存放庫{#create-a-new-theme-repo}

您需要存放庫才能部署主題。 登入您的 [AEM Cloud Manager存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) 並為您的主題新增存放庫。

1. 按一下「 」，建立主題的新存放庫 **[!UICONTROL 存放庫]** > **[!UICONTROL 新增存放庫]**.

   ![建立新的主題存放庫](/help/forms/assets/createrepo_canvastheme.png)


1. 指定 **存放庫名稱** 在 **新增存放庫** 對話方塊。 例如，提供的名稱是 `custom-canvas-theme-repo`.
1. 按一下「**[!UICONTROL 儲存]**」。

   ![新增畫布主題存放庫](/help/forms/assets/addcanvasthemerepo.png)

1. 按一下 **[!UICONTROL 複製存放庫URL]** 複製存放庫的URL。

   ![畫布主題URL](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   > * 您可以將單一存放庫用於多個主題。
   > * 要部署不同的主題，您必須建立單獨的前端管道。
   >* 例如，您可以使用相同的存放庫，如 `custom-canvas-theme-repo`，用於畫布布主題、WKND主題和畫盤主題。 但是，要部署主題，您需要建立單獨的前端管道。 使用相應的前端管道部署特定主題的未來自訂。

##### 5.2.將變更推送至存放庫 {#committing-the-changes}

現在，將變更推送到AEM FormsCloud Service的主題存放庫。.

1. 導覽至主題資料夾的根目錄。  在此案例中，主題資料夾名稱為 `aem-forms-theme-canvas`.
1. 開啟命令提示或終端機。
1. 以列出的順序執行以下命令：

   ```
   git remote add [alias-name-for-repository] [URL of repository]
   git add .
   git commit
   git push [name-for-createdrepository]
   ```

   例如：

   ```
   git remote add canvascloudthemerepo https://git.cloudmanager.adobe.com/stage-aemformsdev/customcanvastheme/
   git add .
   git commit
   git push canvascloudthemerepo 
   ```

   ![變更已認可](/help/forms/assets/cmd_git_push.png)



##### 5.3執行前端管道 {#run-a-frontend-pipeline}

使用部署主題 [前端管道。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html)。若要部署佈景主題，請執行下列步驟：

1. 登入您的AEM Cloud Manager存放庫。
1. 按一下 **[!UICONTROL 新增]** 按鈕來自 **[!UICONTROL 管道]** 區段。
1. 選取 **[!UICONTROL 新增非生產管道]** 或 **[!UICONTROL 新增生產管道]** 根據Cloud Service環境而定。 例如，此處 **[!UICONTROL 新增生產管道]** 已選取選項。
1. 在 **[!UICONTROL 新增生產管道]** 對話方塊作為 **[!UICONTROL 設定]** 步驟，指定管道的名稱。 例如，管道的名稱為 `customcanvastheme`.
1. 按一下&#x200B;**[!UICONTROL 「繼續」]**。
1. 選取 **[!UICONTROL 目標部署]** > **[!UICONTROL 前端計畫碼]** 選項，在 **[!UICONTROL 原始碼]** 步驟。
1. 選取 **[!UICONTROL 存放庫]** 和 **[!UICONTROL Git分支]** 具有您最新變更的值。 例如，此處選取的存放庫名稱為 `custom-canvas-theme-repo` Git分支為 `main`.
1. 選取 **[!UICONTROL 程式碼位置]** 作為 `/`，如果您的變更位於根資料夾中。
1. 按一下「**[!UICONTROL 儲存]**」。
   ![建立前端管道](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   管道設定完成後，會更新行動號召卡。

1. 以滑鼠右鍵按一下已建立的管線。
1. 按一下 **[!UICONTROL 執行]** .

   ![執行管道](/help/forms/assets/canvas-theme-run-pipeline.png)

建置完成後，主題即可在製作例項上使用。 它會顯示在 **[!UICONTROL 樣式]** 索引標籤建立新最適化表單時，使用最適化表單建立精靈中的這個索引標籤。

![樣式標籤下可用的自訂主題](/help/forms/assets/custom-theme-style-tab.png)

## 將主題套用至最適化表單 {#using-theme-in-adaptive-form}

將主題套用至最適化表單的步驟如下：

1. 登入您的AEM Forms作者執行個體。

1. 點選 **Adobe Experience Manager** > **Forms** > **Forms與檔案**.

1. 按一下 **建立** > **最適化Forms**. 建立最適化表單的精靈隨即開啟。

1. 選取中的核心元件範本 **來源** 標籤。
1. 選取中的主題 **樣式** 標籤。
1. 按一下&#x200B;**建立**。

最適化表單主題用於最適化表單範本的一部分，以便在建立最適化表單時定義樣式。

## 最佳做法 {#best-practices}

* **避免使用其他主題的資產**

  編輯主題時，您可以瀏覽並從其他主題新增資產（例如影像）。 例如，您正在編輯頁面的背景。 例如，當您選取 **[!UICONTROL 頁面]** ![編輯按鈕](assets/edit-button.png)> **[!UICONTROL 背景]** > **[!UICONTROL 新增]** > **[!UICONTROL 影像]**，您會看到一個對話方塊，可讓您瀏覽並新增其他主題中的影像。

  如果從其他主題新增資產，且移動或刪除了其他主題，您可能會遇到目前主題的問題。 建議您避免瀏覽和從其他主題新增資產。

* **變更容器面板配置寬度**

  不建議變更容器面板配置寬度。 當您指定容器面板的寬度時，其會變成靜態，且無法適應不同的顯示。

* **使用表單編輯器或主題編輯器來處理頁首和頁尾**

  如果要使用字型樣式、背景和透明度等樣式選項來設定頁首和頁尾的樣式，請使用主題編輯器。
如果您想在頁尾中提供標誌影像、公司名稱和版權資訊等資訊，請使用表單編輯器選項。

## 常見問題 {#faq}

**問：** 在全域和元件層級的主題資料夾中進行自訂時，哪個自訂專案優先？

**Ans：** 在全域和元件層級進行自訂時，優先採用元件層級的自訂。

<!--

## See next

* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/responsive-layout.md)
* [Generate Document of Record for Adaptive Forms (Core Components](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Create an Adaptive Forms with Repeatable sections](/help/forms/create-forms-repeatable-sections.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)


>[!MORELIKETHIS]
>
>* [Enable Adaptive Forms Core Components on AEM Forms as a Cloud Service and local development environment](/help/forms/enable-adaptive-forms-core-components.md)

-->


## 另請參閱 {#see-also}

{{see-also}}
* [設定不同熒幕大小和裝置型別的表單版面](/help/sites-cloud/authoring/features/responsive-layout.md)
* [產生最適化Forms的記錄檔案（核心元件）](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [建立具有可重複區段的最適化Forms](/help/forms/create-forms-repeatable-sections.md)
* [範例主題範本和表單資料模型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
* [在 AEM Forms as a Cloud Service 和本機開發環境中啟用最適化表單核心元件](/help/forms/enable-adaptive-forms-core-components.md)
