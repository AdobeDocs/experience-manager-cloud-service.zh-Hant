---
title: 在Universal Editor中開始使用AEM Forms的Edge Delivery Services — 開發人員教學課程
description: 本教學課程可協助您啟動並執行新的 Adob​​e Experience Manager (AEM) Forms 專案。10到20分鐘後，您就會在Universal Editor中建立自己的Edge Delivery ServicesForms 。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 23%

---


# 使用Universal Editor (WYSIWYG)的AEM FormsEdge Delivery Services快速入門

在當今的數位時代，好記的表格是所有組織不可或缺的功能。 Edge Delivery Services Forms是使用通用編輯器建立的，該編輯器提供WYSIWYG （所見即所得）功能。 它提供現代、直覺式的介面，以進行有效的表單撰寫作業。

AEM Forms提供稱為最適化Forms區塊的區塊，可協助您輕鬆建立Edge Delivery Services Forms以擷取及儲存資料。 您可以[建立已預先設定最適化Forms區塊的新AEM專案](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)，或[將最適化Forms區塊新增至現有的AEM專案](#add-adaptive-forms-block-to-your-existing-aem-project)。

本教學課程會使用Universal Editor的WYSIWYG撰寫功能，引導您使用新的或現有的Adobe Experience Manager網站專案來建立、預覽及發佈自己的表單。


## 先決條件

* 您擁有 GitHub 帳戶，並且了解 Git 基本知識。
* 您擁有 Google 或 Microsoft SharePoint 帳戶。
* 您了解 HTML、CSS 和 JavaScript 的基本知識。
* 您已安裝 Node/npm 可進行本機開發。

## 建立一個預先設定最適化表單區塊的新 AEM 專案

AEM Forms 範本可協助您很快開始使用預先設定最適化表單區塊的 AEM 專案。這是遵循AEM最佳實務並直接開始建立您的表單的最快速、最簡單的方法。

### 開始使用 AEM Forms 範本的存放庫範本

1. 為您的 AEM 專案建立 GitHub 存放庫。若要建立存放庫：
   1. 前往 [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) 。

      ![AEM Forms 範本](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. 按一下&#x200B;**使用此範本**&#x200B;選項並選取&#x200B;**建立新存放庫**&#x200B;選項。

      ![使用 AEM Forms 範本建立新存放庫](/help/edge/docs/forms/assets/use-eds-form-template.png)

      **建立新存放庫**&#x200B;畫面會開啟。

   1. 在「**建立新存放庫**」畫面上，選取「**所有者**」，並指定「**存放庫名稱**」。 Adobe建議將存放庫設定為&#x200B;**公用**。 因此，選取「**公開**」選項，然後按一下「**建立存放庫**」。

      ![將存放庫設定為公開](/help/edge/docs/forms/assets/name-eds-repo.png)

1. 在您的存放庫上安裝 AEM Code Sync GitHub 應用程式。若要安裝：
   1. 前往 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new) 。
   1. 在&#x200B;**安裝AEM程式碼同步**&#x200B;畫面上，選取&#x200B;**僅選取存放庫**&#x200B;選項，並選取您新建立的存放庫。 按一下「**儲存**」。

   ![將存放庫設定為公開](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. 現在將您使用AEM Forms範本建立的GitHub存放庫連結至您的AEM專案製作環境。 若要連接：

   1. 前往您先前使用 AEM Forms 範本建立的 GitHub 存放庫。
   1. 開啟&#x200B;**fstab.yaml**&#x200B;檔案以進行編輯。

      ![開啟fstab.yaml檔案](/help/edge/docs/forms/assets/open-fstab.png)

   1. 編輯&#x200B;**fstab.yaml**檔案以更新專案的掛載點。 將URL取代為AEM as a Cloud Service編寫執行個體的URL。
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![編輯fstab.yaml檔案](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. 一旦您更新了參考且一切正常，請認可更新的&#x200B;**fstab.yaml**&#x200B;檔案。

      ![認可變更](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      如果您遇到任何建置問題，請參閱「[解決 GitHub 建置問題](#troubleshooting-github-build-issues)」。

### 建立新的AEM專案

現在您已擁有GitHub專案，您可以繼續前往AEM as a Cloud Service編寫執行個體建立和發佈新的AEM專案。
1. 若要建立新的AEM專案：

   1. 登入AEM as a Cloud Service編寫執行個體並選取&#x200B;**網站**。

      ![選取網站](/help/edge/assets/select-sites.png)

   1. 按一下&#x200B;**建立** > **從範本**&#x200B;建立網站。

      ![建立網站](/help/edge/docs/forms/assets/create-sites.png)

   1. 選取Edge Delivery Services網站範本，然後按一下&#x200B;**下一步**。

      ![select-site-template](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * 如果您的編寫執行個體無法使用「Edge Delivery Services網站」範本，請按一下「匯入」按鈕以上傳範本。
      > * 您可以從[GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)下載Edge Delivery Services網站範本。

   1. 輸入下列詳細資料以建立新的AEM專案：
      * **網站標題** - 為網站新增描述性標題。
      * **網站標題** — 使用您在上一步中定義的`site-name`。
      * **GitHub URL** - 使用您在上一個步驟中建立的 GitHub 專案的 URL。

      ![建立AEM網站](/help/edge/docs/forms/assets/create-aem-site.png)

   1. **建立網站**&#x200B;對話方塊出現，請按一下&#x200B;**確定**。

      ![按一下[確定]](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      幾分鐘內，您的新AEM專案就會建立。

   1. 導覽至您在Sites主控台中新建立的AEM專案，然後按一下&#x200B;**編輯**。
在此案例中，`index.html`頁面是用作插圖。

      ![編輯AEM網站](/help/edge/docs/forms/assets/edit-site.png)

      AEM專案會在Universal Editor的新標籤中開啟，以啟用WYSIWYG撰寫功能。 您現在可以編輯您的AEM專案。

      ![網站在通用編輯器中開啟](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. Publish您建立的AEM專案

   完成編輯AEM專案後，請將其發佈。 若要發佈：

   1. 在Sites主控台上，選取所有AEM專案頁面，然後按一下&#x200B;**快速Publish**。

      ![發佈AEM Sites專案](/help/edge/docs/forms/assets/publish-sites.png)

   1. **快速Publish**&#x200B;確認對話方塊出現，按一下&#x200B;**Publish**&#x200B;以開始發佈程式。

      ![快速Publish確認對話方塊](/help/edge/docs/forms/assets/quick-publish.png)

      或者，您也可以直接從通用編輯器使用者介面發佈AEM專案頁面。

      ![快速Publish確認對話方塊](/help/edge/docs/forms/assets/qui.png)

   恭喜！您有一個在  `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/` 上執行的新網站。

   * `<branch>`是指 GitHub 存放庫的分支。
   * `<repository>`表示您的 GitHub 存放庫。
   * `<owner>`是指託管 GitHub 存放庫的 GitHub 帳戶使用者名稱。
   * `<site-name>`參照您建立的網站名稱。

   例如，如果分支名稱為`main`，存放庫為`edsforms`，擁有者為`wkndforms`，而`site-name`為`eds-forms`，則網站將在`https://main--edsforms--wkndforms.aem.page/content/eds-forms/`啟動並執行

   >[!NOTE]
   >
   > * 若要檢視AEM專案的`index.html`頁面，請使用URL： `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * 若要檢視AEM專案的`index page`以外的頁面，請使用URL： `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

現在，您可以開始[建立表單並新增至您的AEM專案](#add-edge-delivery-services-forms-to-aem-project)。

## 將最適化Forms區塊新增至您現有的AEM專案

如果您有現有的 AEM 專案，則可以將最適化表單區塊整合至目前專案中並開始建立表單。

>[!NOTE]
>
>
> 此步驟適用於使用 [AEM 範本](https://github.com/adobe-rnd/aem-boilerplate-xwalk)建置的專案。如果您使用 [AEM Forms 範本](https://github.com/adobe-rnd/aem-boilerplate-forms)建立 AEM 專案，則可以省略此步驟。

若要整合：

1. 將最適化Forms區塊GitHub存放庫： [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)複製至您的電腦。
1. 在下載的資料夾中，找到`blocks/form`資料夾並複製此資料夾。
1. 將AEM專案GitHub存放庫複製到電腦。
1. 現在，請導覽至您本機AEM Project存放庫中的`blocks`資料夾，並將複製的表單資料夾貼到該處。
1. 在GitHub上提交這些變更並推送至您的AEM專案存放庫。

就是這樣！最適化Forms區塊現在是AEM專案的一部分。 您可以[開始建立表單並新增至您的AEM專案](#add-edge-delivery-services-forms-to-aem-site-project)。

## 使用WYSIWYG編寫AEM Forms

您可以在WYSIWYG編寫的通用編輯器中開啟AEM專案，編輯專案並新增最適化表單區段以在AEM專案頁面上包含Edge Delivery Services表單。

1. 將最適化表單區段新增到您的AEM專案頁面。 若要新增：
   1. 在網站主控台中導覽至您的AEM專案，然後按一下&#x200B;**編輯**。 「AEM專案」頁面會在通用編輯器中開啟以進行編輯。
在此案例中，`index.html`頁面是用作插圖。
   1. 開啟「內容」樹狀結構，並導覽至您要新增「最適化表單」區段的位置。
   1. 按一下「**[!UICONTROL 新增]**」圖示，然後從元件清單中選取&#x200B;**[!UICONTROL 最適化表單]**&#x200B;元件。

   ![內容樹狀結構](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   最適化表單區段會新增至指定位置。 您現在可以開始將表單元件新增至AEM專案頁面。

1. 將表單元件新增至新增的最適化表單區段。 若要新增表單元件：
   1. 導覽至內容樹狀結構中新增的最適化表單區段。

      ![已新增最適化表單區塊](/help/edge/docs/forms/assets/adative-form-block.png)


   1. 按一下&#x200B;**[!UICONTROL 新增]**&#x200B;圖示，然後從&#x200B;**最適化表單元件**&#x200B;清單新增所需元件。

      ![新增元件](/help/edge/docs/forms/assets/add-component.png)

      您也可以拖放所需的調適型Forms元件，因為Universal Editor提供直覺式的拖放功能。

   1. 選取新增的最適化表單元件，以使用&#x200B;**[!UICONTROL 屬性]**&#x200B;更新其屬性。

      ![開啟屬性](/help/edge/docs/forms/assets/component-properties.png)

      底下熒幕擷圖顯示使用WYSIWYG在AEM專案中編寫的表單：

      ![已新增表單](/help/edge/docs/forms/assets/added-form-aem-sites.png)

   >[!NOTE]
   >
   > 進行變更後，請務必再次發佈AEM專案頁面；否則，瀏覽器中不會顯示更新。

1. 重新發佈AEM專案頁面。

   1. 按一下&#x200B;**Publish**，在新增表單後再次發佈AEM專案頁面。

      ![發佈表單](/help/edge/docs/forms/assets/publish-form.png)

   1. **Publish**&#x200B;確認對話方塊會出現在熒幕上，請按一下&#x200B;**Publish**&#x200B;開始發佈。

      ![發佈表單1](/help/edge/docs/forms/assets/publish-form1.png)

      按一下&#x200B;**Publish**&#x200B;按鈕後，`Publish started successfully`訊息就會顯示。

      ![發佈表單2](/help/edge/docs/forms/assets/publish-form2.png)

   您現在可以在下列URL檢視含有新增Edge Delivery Services表單的AEM專案頁面：
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`。

   例如，如果分支名稱為`main`，存放庫為`edsforms`，擁有者為`wkndforms`，網站名稱為`eds-forms`，則URL會是：
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![索引頁面](/help/edge/docs/forms/assets/publish-index-page.png)

您可以編輯Adaptive Forms區塊中的`.css`和`.js`檔案，並[設定本機AEM開發環境](#set-up-local-aem-development-environment)，以便在瀏覽器中立即檢視變更，藉此設定Edge Delivery Services Forms的樣式。

## 設定本機AEM開發環境

您可以設定本機AEM開發環境，以便在本機開發自訂樣式和元件。 使用本機AEM開發環境執行作業：

1. **安裝AEM CLI**： AEM CLI可簡化開發工作。 讓我們使用 npm 進行全域安裝：

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **複製GitHub專案**：使用以下命令從GitHub複製AEM專案存放庫，取代 <owner> 存放庫所有者和 <repo> 存放庫名稱：

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **啟動您的本機環境**：瀏覽至您的專案目錄，並使用單一命令啟動您的本機AEM執行個體：

   ```
   cd <repo>
   aem up
   ```

您可以在最適化Forms區塊`blocks/form`資料夾中進行本機變更，以針對您的表單進行樣式和編碼！ 編輯此目錄中的`.css`或`.js`檔案，您會看到變更立即反映在瀏覽器中。

完成變更後，請使用Git命令來認可及推送變更。 這會更新您的預覽和生產環境，可在下列URL存取（將預留位置取代為您的專案詳細資料）：

預覽：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
生產：`https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## 疑難排解 GitHub 建置問題

解決潛在問題以確保 GitHub 建置過程順利進行：

* **處理 Linting 錯誤：**
如果您遇到任何 linting 錯誤，您可以略過不予處理。開啟 [EDS Project]/package.json 檔案並將 &quot;lint&quot; 指令碼從 `"lint": "npm run lint:js && npm run lint:css"` 修改為 `"lint": "echo 'skipping linting for now'"`。儲存檔案並將變更提交至您的 GitHub 專案。

<!-- * **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file. -->
