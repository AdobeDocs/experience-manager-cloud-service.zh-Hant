---
title: AEM Forms Edge Delivery Services快速入門 — 開發人員教學課程
description: 本教學課程可協助您啟動並執行新的Adobe Experience Manager Forms (AEM)專案。 10到20分鐘後，您就會建立自己的表格。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '1770'
ht-degree: 3%

---


# 快速入門 - 開發人員教學課程

身處今日數位時代，任何組織都需要建立對使用者友善的表單。AEM FormsEdge Delivery Services(EDS)可讓您使用熟悉的工具(如Google檔案和Microsoft Office)來建立表單。

這些表單可直接提交資料至 Microsoft Excel 或 Google Sheets 檔案，讓您能夠使用由 Google Sheets、Microsoft Excel 和 Microsoft Sharepoint 等強大 API 建構的活躍生態系統，以便輕鬆處理提交的資料或啟動現有的業務工作流程。

AEM Forms提供稱為最適化Forms區塊的區塊，可協助您輕鬆建立表單，以擷取及儲存擷取的資料。 您可以建立已預先配備最適化Forms區塊的新AEM專案，或將最適化Forms區塊新增到現有AEM專案。

此AEM Forms教學課程會引導您使用新的Adobe Experience Manager (AEM) Forms專案來建立、預覽和發佈您自己的自訂表單。 您還將瞭解如何將Adaptive Forms區塊新增至現有的AEM專案。

* **[建立預先配備最適化Forms區塊的新AEM專案](#create-a-new-eds-project-pre-equipped-with-adaptive-forms-block)**
* **[將最適化Forms區塊新增至現有的AEM專案](#add-adaptive-forms-block-to-an-existing-eds-project)**



## 先決條件

* 您有GitHub帳戶，並瞭解Git基本知識。
* 您有Google或Microsoft SharePoint帳戶。
* 您瞭解HTML、CSS和JavaScript的基本概念。
* 您已安裝Node/npm以進行本機開發。

**抬頭！** 本教學課程使用macOS、Chrome和Visual Studio Code。 雖然這些步驟可以適應其他設定，但熒幕擷取畫面和特定UI元素可能會因您選擇的作業系統、瀏覽器和程式碼編輯器而有所不同。


## 建立預先配備最適化Forms區塊的新AEM專案

AEM Forms樣板範本可讓您透過預先設定最適化Forms區塊的AEM專案快速入門。 這是遵循AEM最佳實務並直接開始建立您的表單的最快速、最簡單的方法。

### 開始使用AEM Forms範本存放庫範本

1. 為您的AEM專案建立Github存放庫。 若要建立存放庫：
   1. 前往 [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms樣板](/help/edge/assets/aem-forms-boilerplate.png)
   1. 按一下 **使用此範本** 選項並選取 **建立新的存放庫** 選項。 「建立新存放庫」畫面隨即開啟。

      ![使用AEM Forms範本建立新的存放庫](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. 在「建立新的存放庫」畫面上，選取 **所有者**，並指定 **存放庫名稱** . Adobe建議將存放庫設為 **公共**. 因此，請選取 **公共** 選項，然後按一下 **建立存放庫**.

   ![將存放庫設為公開](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. 在您的存放庫上安裝AEM程式碼同步GitHub應用程式。 若要安裝：
   1. 前往 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. 在「安裝AEM程式碼同步」畫面上，選取 **僅選取存放庫** 選項並選取您新建立的存放庫。 按一下「儲存」。

   ![將存放庫設為公開](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > 如果您正在使用具有IP篩選的Github Enterprise，您可以將下列IP新增至允許清單： 3.227.118.73

   恭喜！您有一個新網站在執行中 `https://<branch>--<repo>--<owner>.hlx.page/`.

   * `<branch>` 是指GitHub存放庫的分支。
   * `<repository>` 代表您的GitHub存放庫。
   * `<owner>` 是指代管GitHub存放庫的GitHub帳戶使用者名稱。

   例如，如果分支名稱為 `main`，存放庫為 `wefinance`，而擁有者為 `wkndforms`，網站將會在 [https://main--wefinance--wkndforms.hlx.page/](https://main--wefinance--wkndforms.hlx.page/).



### 連結您自己的內容來源

您新建立的Github存放庫指向 [儲存在Google Drive資料夾中的範例內容](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_). 此唯讀內容是您表單的絕佳起點。 您可以隨意將檔案複製到自己的Google Drive，並根據自己的需求進行自訂。

![Google Drive上的範例內容](/help/edge/assets/folder-with-sample-content.png)

若要將範例內容複製到您自己的內容資料夾，並將Github存放庫指向您自己的內容資料夾：

1. 在Google Drive或Microsoft SharePoint中建立專為AEM內容的新資料夾。 本檔案使用在Microsoft SharePoint上建立的資料夾。

1. 與Adobe Experience Manager使用者共用資料夾(helix@adobe.com)。

   ![使用「管理存取權」選項與AEM使用者 — SharePoint共用資料夾](/help/edge/assets/share-folder-with-aem-user.png)

   ![使用「管理存取權」選項與AEM使用者 — Google磁碟機共用資料夾](/help/edge/assets/share-google-drive-folder.png)


   確定您已向Adobe Experience Manager使用者提供資料夾的編輯許可權。

   ![與AEM使用者共用資料夾，提供編輯許可權 — SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png)

   ![與AEM使用者共用資料夾，提供編輯許可權 — Google Drive](/help/edge/assets/add-aem-user-google-folder.png)

1. 複製 [儲存在Google Drive資料夾中的範例內容](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_) 至您的資料夾。 若要複製：

   1. 一起下載檔案或下載個別檔案。

      ![下載範例內容](/help/edge/assets/download-sample-content.png)

      此 `index`， `nav`、和 `footer` 檔案會定義頁面的基本版面，且很少會在整個專案中變更。 這類檔案也具有與其他大多數內容檔案不同的特定結構。 透過檢查這些檔案，您將會瞭解AEM專案中內容的組織方式。


   1. 將這些檔案上傳至Microsoft SharePoint或Google Drive資料夾。

      ![Google Drive上的範例內容](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      請務必複製  `enquiry` 將範例內容中的工作表移至Google Drive或Microsoft SharePoint上的資料夾。 它包含範例表單的結構。

1. 現在您已設定內容資料夾，接下來該將其連結至您先前使用AEM Forms Boilerplate在GitHub上建立的專案。 若要連線：

   1. 前往您使用AEM Forms Boilerplate先前建立的GitHub存放庫。
   1. 開啟 `fstab.yaml` 以進行編輯。
   1. 以您與AEM使用者共用的資料夾路徑(helix@adobe.com)取代現有參照。

      ![Google Drive上的範例內容](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      如果您使用Microsoft SharePoint，資料夾路徑會使用以下格式：

      ```HTML
      https://<tenant>.sharepoint.com/sites/  <sp-site>/Shared%20Documents/<folder-name>
      ```

      例如，

      ```HTML
      https://adobe.sharepoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      如需在Microsoft SharePoint中使用管理檔案的詳細資訊，請參閱 [如何使用AdobeSharepoint](https://www.aem.live/docs/setup-customer-sharepoint).



   1. 提交更新的 `fsatb.yaml` 檔案，在您更新參考且一切看起來良好後。 如果您遇到任何建置問題，請參閱 [疑難排解GitHub建置問題](#troubleshooting-github-build-issues).



      ![認可更新的fsatab.yaml檔案](/help/edge/assets/commit-updated-fstab-yaml.png)

      這會將您的內容資料夾連線至您的網站。 更新參考後，您一開始可能會遇到「404 Not Found」錯誤。 這是因為您的內容尚未預覽。 下一節將說明如何開始編寫和預覽您的內容。

      ![認可更新的fsatab.yaml檔案](/help/edge/assets/aem-forms-project-folder-error.png)

### 預覽和發佈您的內容

完成最後一個步驟後，您的新內容來源並非空白，但在它升級至預覽或即時階段之前，您將無法在您的網站上看到它。 目前，這可能會造成404錯誤。

若要預覽未發佈的內容：

1. 安裝名為的Chrome擴充功能 [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![安裝AEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

   將擴充功能安裝至Chrome後，別忘了釘選擴充功能，這樣可讓您更輕鬆找到擴充功能。

   ![釘選AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. 若要設定Sidekick Chrome擴充功能，請前往您先前共用的Google Drive或Microsoft SharePoint資料夾，然後在瀏覽器工具列中的擴充功能圖示上按一下滑鼠右鍵，然後選取「 」 `Add this project`.

   ![AEM Sidekick — 新增專案](/help/edge/assets/aem-sidekick-add-a-project.png)

   只要已安裝擴充功能並新增專案，您就可以從Google Drive預覽和發佈內容。

1. 選取Microsoft SharePoint或Google Drive資料夾中的所有檔案。 您可以按住Ctrl鍵(Windows/Linux)或Cmd鍵(Mac)，同時按一下以選擇多個檔案。

   ![選取所有檔案](/help/edge/assets/select-all-files.png)

1. 按一下釘選至Chrome擴充功能列的AEM Sidekick圖示。 熒幕上會出現一個工具列。 您可以選擇預覽或發佈您的內容。

   如果您複製至 `index`， `nav`， `footer` 和 `enquiry` 檔案，所有這些檔案都是獨立的檔案，都有自己的預覽和發佈週期，因此請務必預覽（和發佈）所有這些檔案。

   預覽檔案時，新的瀏覽器標籤會顯示檔案。 若要預覽範例表單，請前往下列URL：


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.live
   ```

   * `<branch>` 是指GitHub存放庫的分支。
   * `<repository>` 代表您的GitHub存放庫。
   * `<owner>` 是指代管GitHub存放庫的GitHub帳戶使用者名稱。


   `https://<branch>--<repo>--<owner>.hlx.page/enquiry` URL。

   例如，如果您的專案存放庫命名為「wefinance」，它位於帳戶擁有者「wkandforms」下方，而您使用的是「主要」分支，則URL為：



   [https://main--wefinance--wkndforms.hlx.page](https://main--wefinance--wkndforms.hlx.page).

### 更新您的表單

1. 前往Microsoft SharePoint或Google Drive資料夾。

1. 開啟 `enquiry.xlsx` 以進行編輯。

   ![查詢表單](/help/edge/assets/enquiry-form-microsoft-sharepoint.png)

1. 將提交按鈕的標籤變更為 `Let's Chat`.

   ![查詢表單](/help/edge/assets/enquiry-form-microsoft-sharepoint.png)

1. 使用AEM Sidekick來預覽和發佈 `enquiry.xlsx` 檔案。

   ![查詢表單](/help/edge/assets/enquiry-form-preview-publish.png)

1. 若要預覽查詢表單，請前往下列URL：


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.page/enquiry
   ```

   提交按鈕的標籤會更新。 現在，填寫表單並按一下提交按鈕，您會遇到類似以下內容的錯誤，因為試算表並非 [設定為尚未接受資料](/help/edge/docs/forms/submit-forms.md).


### 開始開發樣式和功能


立即使用本機AEM開發環境執行作業：

1. 安裝AEM CLI： AEM CLI可簡化開發工作。 讓我們使用npm將其全域安裝：

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. 複製Github專案：使用下列命令從GitHub複製專案存放庫，取代 <owner> 與存放庫擁有者及 <repo> 存放庫名稱：

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. 啟動您的本機環境：導覽至您的專案目錄，並使用單一命令引發您的本機AEM執行個體：

   ```
   cd <repo>
   aem up
   ```

最適化Forms區塊 `blocks/form` 資料夾是您表單樣式和程式碼的遊樂場！ 編輯任一 `.css` 或 `.js` 此目錄中的檔案，您會看到變更立即反映在瀏覽器中。

準備好展示您的建立作業了嗎？ 使用Git來認可及推送您的變更。 這會更新可從這些URL存取的預覽和生產環境（將預留位置取代為您的專案詳細資料）：

預覽： `https://<branch>--<repo>--<owner>.hlx.page/`
生產： `https://<branch>--<repo>--<owner>.hlx.live/`
恭喜！ 您已成功設定本機開發環境並部署變更。



## 將最適化Forms區塊新增至您現有的AEM專案


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

如果您有現有的AEM專案，可以整合Adaptive Forms區塊至您目前的專案，以開始建立表單。 若要整合：

1. 將最適化Forms區塊存放庫： https://github.com/adobe-rnd/aem-boilerplate-forms複製至您的電腦。

1. 在下載的資料夾中，找到 `blocks/form` 資料夾。 複製此資料夾。 現在，導覽至您AEM專案的本機 `blocks` 並將複製的表單資料夾貼到這裡。

1. 在GitHub上提交這些變更並推送至您的AEM專案。


就是這樣！最適化Forms區塊現在是AEM專案的一部分。 您可以開始建立表單，並將表單新增至AEM頁面。


## 疑難排解GitHub建置問題

解決下列潛在問題，確保GitHub建置流程順暢：

* **解決模組路徑錯誤：**
如果您遇到「無法解析模組「&#39;../../scripts/lib-franklin.js&#39;」的路徑」錯誤，請導覽至 [EDS專案]/blocks/forms/form.js檔案。 將lib-franklin.js檔案取代為aem.js檔案，以更新匯入陳述式。

* **處理Linting錯誤：**
如果您遇到任何連結錯誤，可以略過這些錯誤。 開啟 [EDS專案]/package.json檔案並將「lint」指令碼從「lint」：「npm run lint：js &amp;&amp; npm run lint：css」修改為「lint」：「echo &#39;skipping linting for now&#39;」。 儲存檔案並將變更提交至您的GitHub專案。


## 另請參閱

* [使用Google工作表或Microsoft Excel建立表單](/help/edge/docs/forms/create-forms.md)
* [直接將表單提交至您的Microsoft Excel或Google工作表](/help/edge/docs/forms/submit-forms.md)
* [變更表單外觀](/help/edge/docs/forms/style-theme-forms.md)






