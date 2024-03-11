---
title: AEM Forms Edge Delivery Service快速入門。 建立表單。
description: 快速製作完美表單！⚡ AEM Forms Edge Delivery 文件型製作 = 驚人的速度和 SEO 友善表單，讓使用者更滿意且適用於搜尋引擎。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: 5cf8abe43987d145b302228877a38615f21ffd27
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 22%

---

# 使用最適化Forms區塊建立表單

AEM Forms Edge Delivery提供稱為最適化Forms區塊的區塊，協助您輕鬆建立表單，以擷取及儲存擷取的資料。 您可以 [建立預先配備最適化Forms區塊的新AEM專案](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-equipped-with-adaptive-forms-block) 或 [將最適化Forms區塊新增至現有的AEM專案](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project).

這些表單可直接提交資料至 Microsoft Excel 或 Google Sheets 檔案，讓您能夠使用由 Google Sheets、Microsoft Excel 和 Microsoft Sharepoint 等強大 API 建構的活躍生態系統，以便輕鬆處理提交的資料或啟動現有的業務工作流程。

![檔案式撰寫生態系統](/help/edge/assets/document-based-authoring-workflow-create-form.png)




## 先決條件

在開始之前，請確保您已完成以下步驟：

* 設定 [使用AEM Forms範本的AEM專案](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-equipped-with-adaptive-forms-block) 或 [已將最適化Forms區塊新增至您現有的AEM專案](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) 並複製本機電腦上對應的GitHub存放庫。
在本檔案中，您的Edge Delivery Services(EDS)專案的本機資料夾稱為 `[EDS Project repository]`.
* 確保您可以存取 Google Sheets 或 Microsoft SharePoint。若要將Microsoft SharePoint設定為您的內容來源，請參閱 [如何使用Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint).



## 建立表單

<!-- 

+++ Step 1: Add the Adaptive Forms Block to your Edge Delivery Services (EDS) project.

The Adaptive  empowers users to create forms for an Edge Delivery ServicesSite. However, this block isn't included in the default AEM boilerplate (used to create an Edge Delivery Services project). To seamlessly integrate the Adaptive Forms Block into your Edge Delivery Services project:

1. **Clone the Adaptive Forms Block repository**: Clone the [Adaptive Forms Block repository](https://github.com/adobe-rnd/form-block) on your local machine. It contains the code to render the form on an EDS webpage. In this document, the local folder of your Forms Block repository is referred as `[Adaptive Forms Block repository]`.
1. **Locate the Adaptive Forms Block Repository:** Access the [Adaptive Forms Block repository]/blocks/src folder and copy its content. 

1. on your local machine and copy the `form` folder. 
1. **Paste the Adaptive Forms Block's code into your EDS Project:**
Navigate to the [EDS Project repository]/blocks/ folder on your local machine and create a 'form' folder. Paste the `[Adaptive Forms Block repository]/blocks/src content`, copied in perevious step to the `[EDS Project repository]/blocks/form` folder.
1. **Commit Changes to GitHub:** Check in the `[EDS Project repository]/blocks/form` folder and its underlying files to your Edge Delivery Services project on GitHub.

After completing these steps, the Adaptive Forms Block is successfully added to your Edge Delivery Services (EDS) project repository on GitHub. You can now create and add forms to a EDS Sites page.
 

**Troubleshooting GitHub build issues**

Ensure a smooth GitHub build process by addressing potential issues:

* **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file.

* **Handle Linting Errors:**
    Should you come across any linting errors, you can bypass them. Open the [EDS Project]/package.json file and modify the "lint" script from "lint": "npm run lint:js && npm run lint:css" to "lint": "echo 'skipping linting for now'". Save the file and commit the changes to your GitHub project.

+++

-->

+++ 步驟 1：使用 Microsoft Excel 或 Google Sheet 製作表單。

您可以使用試算表輕鬆完成表單的製作作業，而不需透過複雜的程式進行瀏覽。 您可以定義組成表單結構的列和欄。 每一列代表個人 [表單欄位](/help/edge/docs/forms/form-components.md#available-components) 而欄標題則會定義對應的 [欄位屬性](/help/edge/docs/forms/form-components.md#components-properties).

例如，考慮下列試算表，其中的列大綱欄位用於 `enquiry` 表單和欄標題定義其屬性：

![查詢試算表](/help/edge/assets/enquiry-form-spreadsheet.png)

若要繼續建立表單：

1. 在Microsoft SharePoint或Google Drive上存取AEM Edge Delivery專案資料夾。

1. 在AEM Edge Delivery專案目錄中的任何位置建立Microsoft Excel活頁簿或Google工作表。 例如，在 Google Drive 上的 AEM Edge Delivery 專案目錄中，建立一個名為 `enquiry` 的試算表。

   ![Google Drive上的範例內容](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

1. 確定工作表已和適當的AEM使用者共用(例如 `helix@adobe.com`) [根據專案指定的設定](https://www.aem.live/docs/setup-customer-sharepoint). 授予使用者工作表編輯許可權。

1. 開啟建立的試算表，並將預設工作表重新命名為「shared-default」。

   ![將預設試算表重新命名為「共用預設」](/help/edge/assets/rename-sheet-to-shared-default.png)

1. 若要新增表單欄位，請在「shared-default」工作表中插入列和欄標題。 每一列應代表 [表單欄位](/help/edge/docs/forms/form-components.md#available-components)，欄標題定義對應欄位 [屬性](/help/edge/docs/forms/form-components.md#components-properties).


   為了快速起步，請考慮複製 [查詢試算表](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0) 放入您的試算表中。 複製內容後，請儲存試算表。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽頁面。

   ![使用AEM Sidekick預覽工作表](/help/edge/assets/preview-form.png)

   預覽時，新的瀏覽器標籤會以JSON格式顯示工作表內容。 請務必擷取預覽URL，因為這是呈現下一節中的表單所需。 URL格式如下：


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form-path>/<form-file-name>.json
   ```

   * `<branch>` 是指GitHub存放庫的分支。
   * `<repository>` 代表您的GitHub存放庫。
   * `<owner>` 是指代管GitHub存放庫的GitHub帳戶使用者名稱。

   例如，如果您的專案存放庫命名為「入口網站」，它位在帳戶「wkandforms」底下，而您使用的是「主要」分支，則URL看起來如下所示：

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ 步驟2：使用您的Edge Delivery Services(EDS)頁面預覽表單。


到目前為止，您已準備表單的結構。 現在，若要預覽表單：

1. 開啟Microsoft SharePoint或Google Drive帳戶，並導覽至AEM Edge Delivery專案目錄。



1. 開啟檔案檔案（例如，索引檔案）以內嵌表單。 或者，您也可以建立新檔案。

1. 移至檔案中您想要新增表單的位置。

1. 建立表單區塊以轉譯表單。 選取「插入」>「表格」，然後建立一欄、兩清單格。 將表格命名為「Form」，並將預覽URL貼到第二列。 請確定URL的格式為超連結，而非純文字，如下圖所示：

   | 表單 |
   |---|
   | [https://main--wefinance--wkndforms.hlx.live/enquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json) |


   ![將Adaptive Forms區塊新增至您的網頁](/help/edge/assets/add-adaptive-forms-block.png)

   此區塊可作為內嵌表單的預留位置。 在區塊的第二列中，新增您的預覽URL `<form>.json` 檔案做為超連結。

   >[!IMPORTANT]
   >
   >
   > 請確定URL的格式為超連結，而非顯示為純文字。


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽檔案。 頁面現在會顯示表單。例如，以下是根據 [查詢試算表](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0)：


   [![EDS表單範例](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   現在，填寫表單並按一下提交按鈕，您會遇到類似於以下內容的錯誤，因為試算表尚未設定為接受資料。

   ![在表單提交時的錯誤](/help/edge/assets/form-error.png)

+++


## 下一步

[準備您的試算表](/help/edge/docs/forms/submit-forms.md) 以在提交表單後開始接受資料。



