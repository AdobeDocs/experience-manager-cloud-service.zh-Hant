---
title: 如何在最適化Forms中建置和使用主題？
description: 您可以使用主題來設定樣式，並使用核心元件來將視覺身分提供給最適化表單。 您可以在任何數量的最適化Forms中共用主題。
keywords: 表單產生器主題，最適化表單樣式化核心元件，表單主題產生器，樣式最適化表單，自訂主題，建立表單主題
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: c0e0a700e85563ff65c703d5d20e6d6c1ff0651c
workflow-type: tm+mt
source-wordcount: '2897'
ht-degree: 4%

---

# 使用主題來設定以核心元件為基礎的最適化Forms的樣式{#themes-for-af-using-core-components}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html) |
| AEM as a Cloud Service  | 本文章 |

您可以建立並套用主題來設定最適化表單的樣式。 主題包含元件和面板的樣式詳細資訊。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。套用主題時，指定的樣式會反映在對應的元件上。主題是獨立管理，不需參照最適化表單，且可在多個最適化Forms中重複使用。

在本文中，我們瞭解如何使用主題來設計核心元件型最適化Forms的自訂外觀。

## 設定核心元件樣式的可用主題

Forms如Cloud Service所提供，以下是核心元件型最適化Forms的下列主題：

* [畫布主題](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 主題](https://github.com/adobe/aem-forms-theme-wknd)
* [畫架佈景主題](https://github.com/adobe/aem-forms-theme-easel)

## 瞭解主題結構

主題是包含樣式元件的套件，例如CSS檔案、JavaScript檔案和定義最適化Forms樣式的資源（如圖示）。 最適化表單主題會依循特定組織，包含下列元件：

* `src/theme.scss`：此資料夾包含對整個主題有廣泛影響的CSS檔案。 它是定義和管理佈景主題樣式和行為的集中位置。 透過編輯此檔案，您可以進行在整個主題中普遍套用的變更，這會影響最適化Forms和AEM Sites頁面的外觀和功能。

* `src/site`：此資料夾包含套用至整個AEM網站頁面的CSS檔案。 這些檔案包含程式碼和樣式，會影響AEM網站頁面的整體功能和版面。 此處所做的任何修改會反映在您的網站的所有頁面中。 [何時使用？]

* `src/components`：此資料夾中的CSS檔案是針對個別AEM核心元件所設計。 元件的每個專用資料夾都包含一個`.scss`檔案，該檔案會在最適化表單中設定該特定元件的樣式。 例如，/src/components/accordion/_accordion.scss檔案包含Adaptive Forms摺疊式功能表元件的樣式資訊。

  ![以最適化表單為基礎的主題結構](/help/forms/assets/theme_structure.png)

* `src/resources`：此資料夾包含靜態檔案，例如圖示、標誌和字型。 這些資源用於增強主題的視覺元素和整體設計。

## 建立主題

Forms如Cloud Service所提供，以下列出核心元件型最適化Forms的最適化表單樣式主題。

* [畫布主題](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 主題](https://github.com/adobe/aem-forms-theme-wknd)
* [畫架佈景主題](https://github.com/adobe/aem-forms-theme-easel)

您可以[自訂任何這些主題以建立新的主題](#customize-a-theme-core-components)。

![佈景主題自訂的工作流程](/help/forms/assets/workflow-of-customization-of-theme.png)

## 自訂主題 {#customize-a-theme-core-components}

自訂主題是指修改、樣式化和個人化主題外觀的程式。 自訂主題時，您可以變更其設計元素、版面、顏色、印刷樣式，有時也會變更基礎程式碼。 它可讓您為網站或應用程式建立獨一無二且量身打造的外觀，同時維持主題提供的基本結構和功能。

### 先決條件 {#prerequisites-to-customize}

* 熟悉[在Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)中設定管道，並瞭解如何設定管道的基本知識，可協助您有效率地管理和部署您的主題自訂。
* 瞭解如何[設定具有貢獻者角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html)的使用者。 瞭解如何使用投稿人角色設定使用者，可讓您授與佈景主題自訂的必要許可權。
* 安裝最新版的[Apache Maven](https://maven.apache.org/download.cgi)。 Apache Maven是常用於Java™專案的組建自動化工具。 安裝最新版本可確保您擁有佈景主題自訂的必要相依性。
* 安裝純文字編輯器。 例如，Microsoft® Visual Studio Code。 使用純文字編輯器(例如Microsoft® Visual Studio Code)可提供方便使用的環境，用於編輯和修改佈景主題檔案。

### 設定您的環境

* 安裝最新的Far，為AEM Cloud Service環境啟用最適化Forms核心元件。
* 為您的Cloud Service環境設定[前端部署管道](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html)。 或者，您可以稍後設定管道，讓您在設定部署管道之前，靈活地排定測試的優先順序並調整主題。

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

瞭解先決條件並設定開發環境後，您就可以開始根據特定需求自訂主題或設定主題樣式。

### 自訂主題 {#steps-to-customize-a-theme-core-components}

自訂主題是多步驟的過程。 若要自訂主題，請依照列出的順序執行步驟：

1. [複製佈景主題](#download-a-theme-core-components)
1. [設定佈景主題的名稱](#set-name-of-theme)
1. [自訂主題](#customize-the-theme)
1. [測試主題](#test-the-theme)
1. [部署主題](#deploy-the-theme)

檔案中提供的範例是以&#x200B;**畫布**&#x200B;主題為基礎，但請務必注意，您可以使用相同的指示複製任何主題並加以自訂。 這些指示適用於任何主題，可讓您根據特定需求修改主題。

讓我們從使用主題為您的核心元件型最適化Forms建立品牌體驗的程式開始？

#### 1.原地複製主題 {#download-a-theme-core-components}

若要複製以核心元件為基礎的最適化Forms主題，請選擇下列其中一種主題：

* [畫布主題](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 主題](https://github.com/adobe/aem-forms-theme-wknd)
* [畫架佈景主題](https://github.com/adobe/aem-forms-theme-easel)

若要複製主題，請執行下列指示：

1. 在本機開發環境中開啟命令提示字元或終端機視窗。

1. 執行`git clone`命令以複製主題。

   ```
      git clone [Path of Git Repository of the theme]
   ```

   將主題[的Git存放庫的]路徑取代為主題對應的Git存放庫的實際URL

   例如，若要複製畫布主題，請執行下列命令：

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   成功執行命令後，您的電腦在`aem-forms-theme-canvas`資料夾中有可用的主題本機復本。


#### 2.設定佈景主題的名稱 {#set-name-of-theme}

1. 在IDE中開啟主題資料夾。 例如，在Visual Studio程式碼編輯器中開啟`aem-forms-theme-canvas`資料夾。

1. 導覽至 `aem-forms-theme-canvas` 檔案夾。

1. 執行以下命令：

   ```
      code .
   ```

   ![以純文字編輯器開啟主題資料夾](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   資料夾會在Visual Studio Code中開啟。

1. 開啟 `package.json` 檔案進行編輯。

1. 設定`name`和`version`屬性的值。

   ![畫布布主題名稱變更影像](/help/forms/assets/changename_canvastheme.png)

   >[!NOTE]
   >
   > * 名稱屬性用來唯一識別主題，而指定的名稱會顯示在&#x200B;**表單建立精靈**&#x200B;的&#x200B;**樣式**&#x200B;索引標籤中。
   > * 您可以選擇根據您的選擇為您的主題選取名稱，例如`mytheme`或`customtheme`。 不過，在此案例中，我們已指定名稱為`aem-forms-wknd-theme`。

1. 開啟 `package-lock.json` 檔案進行編輯。
1. 設定`name`和`version`屬性的值。 請確定`name`.json檔案中的`version`與`Package-lock`屬性值符合`Package.json`檔案中的值。

   ![畫布布主題名稱變更影像](/help/forms/assets/changename_canvastheme-package-lock.png)

1. （選擇性）開啟`ReadMe`檔案進行編輯並更新佈景主題的名稱。

   ![畫布布主題名稱變更影像](/help/forms/assets/changename_canvastheme-readme-file.png)

1. 儲存並關閉檔案。

**設定主題名稱時的考量事項**

* 必須從`@aemforms`檔案和`Package.json`檔案中的主題名稱移除`Package-lock.json`。 如果您無法從自訂主題名稱中移除`@aemforms`，這會導致在主題部署期間前端管道失敗。
* 建議更新`version`檔案和`Package.json`檔案中的主題`Package-lock.json`，以準確反映主題隨時間的變更和增強功能。
* 如需有關使用方式、安裝指示和其他相關詳細資訊的重要資訊，建議更新`ReadMe`檔案中的主題名稱。

#### 3.自訂主題 {#customize-the-theme}

您可以使用佈景主題的全域變數來自訂個別元件或進行佈景主題層級變更。 對全域變數所做的任何變更都會影響所有個別元件。 例如，您可以使用全域變數來變更最適化表單所有元件的邊框顏色，並使用明亮的填色顏色來設定CTA (Call to action)使用按鈕元件：

* [設定主題層級樣式](#theme-customization-global-level)

* [設定元件層級樣式](#component-based-customization)

##### 設定主題層級樣式{#theme-customization-global-level}

`variable.scss`檔案包含佈景主題的全域變數。 透過更新這些變數，您可以在主題層級進行樣式相關的變更。 若要套用佈景主題層級樣式，請依照下列步驟進行：

1. 開啟 `<your-theme-sources>/src/site/_variables.scss` 檔案進行編輯。
1. 變更任何屬性的值。 例如，預設的錯誤色彩為`red`。 若要將錯誤顏色從`red`變更為`blue`，請變更`$errorvariable`的顏色十六進位代碼。 例如，`$error: #196ee5`。
1. 儲存並關閉檔案。

   ![編輯主題](/help/forms/assets/edit_theme.png)

同樣地，您可以使用`variable.scss`檔案來設定字型系列與型別、佈景主題與字型顏色、字型大小、佈景主題間距、錯誤圖示、佈景主題框線樣式，以及其他影響多個最適化表單元件的變數。

##### 設定元件層級樣式 {#component-based-customization}

您也可以變更特定最適化表單核心元件的字型、顏色、大小和其他CSS屬性。 例如，按鈕、核取方塊、容器、頁尾等。 您可以編輯特定元件的CSS檔案來設定按鈕或核取方塊的樣式，使其與貴組織的樣式一致。 若要自訂元件的樣式：

1. 開啟檔案`<your-theme-sources>/src/components/<component>/<component.scss>`進行編輯。 例如，若要變更按鈕元件的字型顏色，請開啟`<your-theme-sources>/src/components/button/button.scss`，檔案。
1. 根據您的需求變更任何的值。 例如，若要將滑鼠懸停時按鈕元件的顏色變更為`green`，請將`color: $white`類別中`cmp-adaptiveform-button__widget:hover`屬性的值變更為十六進位代碼`#12B453`或其他任何`green`陰影。 最終程式碼如下所示：

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. 儲存並關閉檔案。

   ![編輯文字方塊CSS](/help/forms/assets/edit_color_textbox.png)

   >[!NOTE]
   >
   > 在主題和元件層級同時定義樣式時，在元件層級定義的樣式會優先執行。

#### 4.測試自訂主題 {#test-the-theme}

若要預覽和測試本機環境中的變更，以及根據不同AEM元件的需求自訂主題，請執行以下步驟：

* 4.1 [設定本機環境以進行測試](#rename-env-file-theme-folder)
* 4.2 [使用本機環境測試主題](#start-a-local-proxy-server)

##### 4.1.設定本機環境以進行測試 {#rename-env-file-theme-folder}

1. 在IDE中開啟主題資料夾。 例如，在Visual Studio程式碼編輯器中開啟`aem-forms-theme-canvas`資料夾。
1. 將`env_template`檔案重新命名為主題資料夾中的`.env`檔案，並新增下列引數：

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例如，表單的URL是`http://localhost:4502/editor.html/content/forms/af/contactusform.html`。 因此，的值：

   * AEM_URL = `http://localhost:4502/`
   * AEM_ADAPTIVE_FORM = `contactusform`

1. 儲存檔案。

   ![畫布布主題結構](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2使用本機環境測試主題 {#start-a-local-proxy-server}

1. 導覽至主題資料夾的根目錄。 在此案例中，主題資料夾名稱為`aem-forms-theme-canvas`。
1. 開啟命令提示或終端機。
1. 執行`npm install`以安裝相依性。
1. 執行`npm run live`以在本機瀏覽器中預覽具有更新主題的表單。

   >[!NOTE]
   >
   > 如果在執行`npm run live`命令期間發生錯誤，請在`npm run live`命令之前執行以下命令：
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

這是熱門部署。 因此，每當您進行任何變更並儲存`_variables.scss`和`button.scss`檔案時，伺服器就會自動挑選變更並預覽最新輸出。 行`[Browsersync] File event [change]`表示伺服器已辨識到最新的變更，而且正在部署本機環境中的變更。

![Proxy browsersync](/help/forms/assets/browser_sync.png)

在主題層級和主題自訂的元件層級遵循設定最適化表單（核心元件）樣式的範例後，最適化表單的錯誤訊息將變更為`blue`顏色，而按鈕元件的標籤顏色在暫留時變更為`green`。

**正在預覽佈景主題層級樣式**

![範例：錯誤顏色設定為藍色](/help/forms/assets/theme-level-changes.png)

**正在預覽元件層級樣式**

![範例：暫留色彩設定為綠色](/help/forms/assets/button-customization.png)

自訂主題有助於根據組織需求，設計核心元件型最適化Forms的自訂外觀。

###### 測試Cloud Service環境中託管的表單主題

您也可以測試在AEM Forms as a Cloud Service執行個體上託管的最適化表單主題。 若要使用雲端例項上託管的Adaptive Forms來設定和設定本機環境以測試主題，請執行以下步驟：

1. 在IDE中開啟主題資料夾。 例如，在Visual Studio程式碼編輯器中開啟`aem-forms-theme-canvas`資料夾。
1. 將`env_template`檔案重新命名為`.env`檔案，並新增下列引數：

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例如，在雲端環境的表單URL是`https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html`。 因此，的值：

   * AEM_URL = `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM_ADAPTIVE_FORM = `contactusform`
1. 儲存檔案。
1. 建立本機使用者。

   >[!NOTE]
   >
   > 若要建立本機使用者：
   >
   > * 移至&#x200B;**[!UICONTROL AEM首頁]** > **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]** 。
   > * 確定使用者是`forms-users`群組的成員。

1. 導覽至主題資料夾的根目錄。 在此案例中，主題資料夾名稱為`aem-forms-theme-canvas`。
1. 執行`npm run live`，系統會將您重新導向至本機瀏覽器。
1. 按一下`SIGN IN LOCALLY (ADMIN TASKS ONLY)`並使用本機使用者的認證登入。

您可以預覽含有最新變更的最適化表單。 一旦您滿意在主題資料夾中完成的修改，請使用前端管道將主題部署到AEM Cloud Service環境。

#### 5.部署主題 {#deploy-the-theme}

若要使用前端管道將主題部署到Cloud Service環境：

* 5.1 [建立佈景主題的存放庫](#create-a-new-theme-repo)
* 5.2 [將變更推送到存放庫](#committing-the-changes)
* 5.3 [執行前端管道](#run-a-frontend-pipeline)

##### 5.1建立主題的存放庫{#create-a-new-theme-repo}

您需要存放庫才能部署主題。 登入您的[AEM Cloud Manager存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)，並為您的主題新增存放庫。

1. 按一下&#x200B;**[!UICONTROL 存放庫]** > **[!UICONTROL 新增存放庫]**，為主題建立新的存放庫。

   ![建立新的主題存放庫](/help/forms/assets/createrepo_canvastheme.png)


1. 在&#x200B;**新增存放庫**&#x200B;對話方塊中指定&#x200B;**存放庫名稱**。 例如，提供的名稱是`custom-canvas-theme-repo`。
1. 按一下&#x200B;**[!UICONTROL 儲存]**。

   ![新增畫布布主題存放庫](/help/forms/assets/addcanvasthemerepo.png)

1. 按一下&#x200B;**[!UICONTROL 複製存放庫URL]**&#x200B;以複製存放庫URL。

   ![畫布布主題URL](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   >* 您可以將單一存放庫用於多個主題。
   >* 要部署不同的主題，您必須建立單獨的前端管道。
   >* 例如，您可以使用相同的存放庫作為畫布主題、WKND主題和畫盤主題的`custom-canvas-theme-repo`。 但是，要部署主題，您需要建立單獨的前端管道。 使用相應的前端管道部署特定主題的未來自訂。

##### 5.2.將變更推送至存放庫 {#committing-the-changes}

現在，將變更推送到AEM Forms Cloud Service的主題存放庫。

1. 導覽至主題資料夾的根目錄。  在此案例中，主題資料夾名稱為`aem-forms-theme-canvas`。
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

   ![已提交變更](/help/forms/assets/cmd_git_push.png)



##### 5.3執行前端管道 {#run-a-frontend-pipeline}

使用[前端管道](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html)部署主題。 若要部署佈景主題，請執行下列步驟：

1. 登入您的AEM Cloud Manager存放庫。
1. 按一下&#x200B;**[!UICONTROL 管道]**&#x200B;區段中的&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕。
1. 根據Cloud Service環境選取&#x200B;**[!UICONTROL 新增非生產管道]**&#x200B;或&#x200B;**[!UICONTROL 新增生產管道]**。 例如，此處已選取&#x200B;**[!UICONTROL 新增生產管道]**&#x200B;選項。
1. 在&#x200B;**[!UICONTROL 新增生產管道]**&#x200B;對話方塊中，作為&#x200B;**[!UICONTROL 設定]**&#x200B;步驟的一部分，請指定管道的名稱。 例如，管道的名稱為`customcanvastheme`。
1. 按一下「**[!UICONTROL 繼續]**」。
1. 選取&#x200B;**[!UICONTROL 目標部署]** > **[!UICONTROL 前端計畫碼]**&#x200B;選項，在
**[!UICONTROL Source程式碼]**&#x200B;步驟。
1. 選取包含您最新變更的&#x200B;**[!UICONTROL 存放庫]**&#x200B;和&#x200B;**[!UICONTROL Git分支]**&#x200B;值。 例如，此處選取的存放庫名稱為`custom-canvas-theme-repo`，而Git分支為`main`。
1. 如果您的變更出現在根資料夾中，請選取&#x200B;**[!UICONTROL 程式碼位置]**&#x200B;作為`/`。
1. 按一下&#x200B;**[!UICONTROL 儲存]**。
   ![建立前端管道](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   管道設定完成後，call-to-action卡會更新。

   >[!NOTE]
   >
   > 為確保您的前端管道在Cloud Manager中不會失敗，[請將Node.js版本設定為20](#set-the-nodejs-vesrion-to-20)。

1. 以滑鼠右鍵按一下已建立的管線。
1. 按一下「**[!UICONTROL 執行]**」。

   ![執行管道](/help/forms/assets/canvas-theme-run-pipeline.png)

建置完成後，主題即可在製作例項上使用。 建立最適化表單時，它出現在最適化表單建立精靈的&#x200B;**[!UICONTROL 樣式]**&#x200B;標籤下。

樣式標籤![下有](/help/forms/assets/custom-theme-style-tab.png)個可用的自訂主題

自訂主題有助於建立核心元件型Adaptive Forms的品牌體驗。

## 將主題套用至最適化表單 {#using-theme-in-adaptive-form}

將主題套用至最適化表單的步驟如下：

1. 登入您的AEM Forms作者執行個體。

1. 選取「**Adobe Experience Manager** > **表單** > **表單與文件**」。

1. 按一下&#x200B;**建立** > **最適化Forms**。 建立最適化表單的精靈隨即開啟。

1. 在&#x200B;**Source**&#x200B;索引標籤中選取核心元件範本。
1. 在&#x200B;**樣式**&#x200B;索引標籤中選取主題。
1. 按一下「**建立**」。

最適化表單主題用於最適化表單範本的一部分，以便在建立最適化表單時定義樣式。

## 將Node.js版本設為20

若要使用管道設定將Node.js版本設為20：

1. 前往&#x200B;**管道**&#x200B;區段並找到您的前端管道。
2. 在管道的右側，按一下三點選單&#x200B;**⋯**，然後從下拉式清單中選取&#x200B;**檢視/編輯變數**。
3. 在&#x200B;**變陣列態**&#x200B;對話方塊中，請依照下列方式填寫欄位：
   * **名稱** - NODE_VERSION
   * **值** - 20
   * **步驟已套用** — 建置
   * **型別** — 變數
4. 按一下[儲存]以套用組態。**&#x200B;**

![管道設定](/help/forms/assets/pipeline-config.png)

## 最佳做法 {#best-practices}

* **從另一個主題中避免資產**

  編輯主題時，您可以瀏覽並從其他主題新增資產（例如影像）。 例如，您正在編輯頁面的背景。 例如，當您選取&#x200B;**[!UICONTROL 頁面]** ![編輯按鈕](assets/edit-button.png)> **[!UICONTROL 背景]** > **[!UICONTROL 新增]** > **[!UICONTROL 影像]**&#x200B;時，您會看到一個對話方塊，可讓您瀏覽並新增其他主題中的影像。

  如果從其他主題新增資產，且移動或刪除了其他主題，您可能會遇到目前主題的問題。 建議您避免瀏覽和從其他主題新增資產。

* **變更容器面板配置寬度**

  不建議變更容器面板配置寬度。 當您指定容器面板的寬度時，其會變成靜態，且無法適應不同的顯示。

## 常見問題 {#faq}

**問：**&#x200B;在全域和元件層級的主題資料夾中進行自訂時，哪一個自訂優先？

**Ans：**&#x200B;當在全域層級和元件層級進行自訂時，元件層級的自訂優先執行。

<!--

## See next

* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Generate Document of Record for Adaptive Forms (Core Components](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Create an Adaptive Forms with Repeatable sections](/help/forms/create-forms-repeatable-sections.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)

-->


## 另請參閱 {#see-also}

{{see-also}}

* [設定不同熒幕大小和裝置型別的表單版面](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [產生最適化Forms的記錄檔案（核心元件）](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [建立具有可重複區段的最適化Forms](/help/forms/create-forms-repeatable-sections.md)
* [範例主題範本和表單資料模型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
