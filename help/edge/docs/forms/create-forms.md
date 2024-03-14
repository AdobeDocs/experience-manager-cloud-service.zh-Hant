---
title: 開始使用 AEM Forms Edge Delivery Service。建立表單。
description: 快速製作完美表單！⚡ AEM Forms Edge Delivery 文件型製作 = 驚人的速度和 SEO 友善表單，讓使用者更滿意且適用於搜尋引擎。
feature: Edge Delivery Services
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: b32e04dec83992ebfcea7874932a5ab77a1eaa70
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 62%

---

# 使用最適化Forms區塊建立表單

>[!VIDEO](https://video.tv.adobe.com/v/3427881?quality=12&learn=on)

AEM Forms Edge Delivery提供稱為最適化Forms區塊的區塊，協助您輕鬆建立表單，以擷取及儲存擷取的資料。 您可以 [建立已預先設定最適化Forms區塊的新AEM專案](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) 或 [將最適化Forms區塊新增至現有的AEM專案](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project).

這些表單會直接將資料提交至Microsoft Excel或Google Sheets檔案，讓您能夠使用生動的生態系統以及Google Sheets、Microsoft Excel和Microsoft SharePoint的強大API，輕鬆處理提交的資料或啟動現有的業務工作流程。

![檔案式撰寫生態系統](/help/edge/assets/document-based-authoring-workflow-create-form.png)


## 先決條件

在開始之前，請確保您已完成以下步驟：

* 設定 [使用AEM Forms範本的AEM專案](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) 或 [已將最適化Forms區塊新增至您現有的AEM專案](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) 並複製本機電腦上對應的GitHub存放庫。
在本檔案中，您的Edge Delivery Services(EDS)專案的本機資料夾稱為 `[EDS Project repository]`.
* 確保您可以存取 Google Sheets 或 Microsoft SharePoint。若要將Microsoft SharePoint設定為您的內容來源，請參閱 [如何使用SharePoint](https://www.aem.live/docs/setup-customer-SharePoint).



## 建立表單

<!-- 

+++ Step 1: Add the Adaptive Forms Block to your Edge Delivery Services (EDS) project.

The Adaptive  empowers users to create forms for an Edge Delivery Service Site. However, this block isn't included in the default AEM boilerplate (used to create an Edge Delivery Services project). To seamlessly integrate the Adaptive Forms Block into your Edge Delivery Services project:

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

使用試算表可輕鬆地製作表單，而無需瀏覽複雜的流程。您可以定義組成表單結構的列和欄。 每一列代表個人 [表單欄位](/help/edge/docs/forms/form-components.md#available-components) 而欄標題則會定義對應的 [欄位屬性](/help/edge/docs/forms/form-components.md#components-properties).

例如，考慮以下試算表，其中的列是概述`enquiry`表單和欄標題是定義其屬性：

![查詢試算表](/help/edge/assets/enquiry-form-spreadsheet.png)

若要繼續建立表單：

1. 在 Microsoft SharePoint 或 Google Drive 上，存取您的 AEM Edge Delivery 專案資料夾。

1. 在 AEM Edge Delivery 專案目錄內的任意位置，建立 Microsoft Excel 活頁簿或 Google Sheet。例如，在 Google Drive 上的 AEM Edge Delivery 專案目錄中，建立一個名為 `enquiry` 的試算表。

   ![Google Drive上的範例內容](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

1. [根據為您專案指定的設定](https://www.aem.live/docs/setup-customer-SharePoint)，確保讓相關 AEM 使用者 (例如 `helix@adobe.com`) 共用工作表。授予使用者關於工作表的編輯權限。

1. 開啟建立的試算表並將預設工作表重新命名為「共享預設」。

   ![將預設試算表重新命名為「共用預設」](/help/edge/assets/rename-sheet-to-shared-default.png)

1. 若要新增表單欄位，請將列和欄標題插入「共用預設」工作表中。每列應該代表一個 [表單欄位](/help/edge/docs/forms/form-components.md#available-components)，且有定義對應欄[屬性](/help/edge/docs/forms/form-components.md#components-properties)的欄標題。


   為了快速開始，請考慮複製[查詢試算表](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0)內容至您的試算表中。複製內容後，請儲存試算表。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽工作表。

   ![使用 AEM Sidekick 來預覽工作表](/help/edge/assets/preview-form.png)

   預覽時，新的瀏覽器標籤會以 JSON 格式顯示工作表內容。確保要擷取預覽 URL，因為這是在下個區段中呈現表單必要的項目。URL 格式如下：


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form-path>/<form-file-name>.json
   ```

   * `<branch>`是指 GitHub 存放庫的分支。
   * `<repository>`表示您的 GitHub 存放庫。
   * `<owner>`是指託管 GitHub 存放庫的 GitHub 帳戶使用者名稱。

   例如，如果您的專案存放庫名為 “portal” (位於帳戶 “wkndforms” 下面)，並且您使用的是「主要」分支，則 URL 如下所示：

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ 步驟2：使用您的Edge Delivery Services(EDS)頁面預覽表單。


到目前為止，您已準備表單的結構。 現在，若要預覽表單：

1. 開啟 Microsoft SharePoint 或 Google Drive 帳戶，然後導覽至您的 AEM Edge Delivery 專案目錄。



1. 開啟檔案檔案（例如，索引檔案）以內嵌表單。 或者，您可以建立一個新文件。

1. 移至檔案中您想要新增表單的位置。

1. 建立表單區塊以轉譯表單。 選取「插入」>「表格」，然後建立一欄、兩清單格。 將表格命名為「Form」，並將預覽URL貼到第二列。 請確定URL的格式為超連結，而非純文字，如下圖所示：

   | 表單 |
   |---|
   | [https://main--wefinance--wkndforms.hlx.live/enquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json) |


   ![將Adaptive Forms區塊新增至您的網頁](/help/edge/assets/add-adaptive-forms-block.png)

   此區塊是用作嵌入表單的暫留位置。在該區塊的第二行中，新增 `<form>.json` 檔案的預覽 URL 作為超連結。

   >[!IMPORTANT]
   >
   >
   > 確保 URL 的格式為超連接，而不是顯示為純文字。


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽文件。頁面現在會顯示表單。例如，這是以[查詢試算表](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0)為主的表單：


   [![EDS Form 範本](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   現在，填寫表單並按一下提交按鈕，您會遇到類似於以下內容的錯誤，因為試算表尚未設定為接受資料。

   ![在表單提交時的錯誤](/help/edge/assets/form-error.png)

+++


## 下一步

[準備您的試算表](/help/edge/docs/forms/submit-forms.md) 以在提交表單後開始接受資料。


## 另請參閱

{{see-more-forms-eds}}
