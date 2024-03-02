---
title: AEM Forms Edge Delivery Service快速入門。 建立表單。
description: 快速製作完美表單！⚡ AEM Forms Edge Delivery 文件型製作 = 驚人的速度和 SEO 友善表單，讓使用者更滿意且適用於搜尋引擎。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 68b60d33e6ccfe27452cfea76603e4d7d29f0c6e
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 16%

---


# 使用最適化表單區塊建立表單

身處今日數位時代，任何組織都需要建立對使用者友善的表單。AEM Forms Edge Delivery 讓您可以使用 Word 或 Google Docs 等熟悉的工具來建立表單。

這些表單可直接提交資料至 Microsoft Excel 或 Google Sheets 檔案，讓您能夠使用由 Google Sheets、Microsoft Excel 和 Microsoft Sharepoint 等強大 API 建構的活躍生態系統，以便輕鬆處理提交的資料或啟動現有的業務工作流程。

![檔案式撰寫生態系統](/help/edge/assets/document-based-authoring.png)

AEM Forms Edge Delivery提供最適化表單區塊，協助您輕鬆建立表單，以擷取及儲存擷取的資料。 您可以在AEM EDS專案中加入最適化表單區塊，以開始建立表單。 讓我們開始吧：


## 先決條件

開始之前，請確定您已完成下列步驟：

* 使用AEM範本設定Edge Delivery Service (EDS) GitHub專案，並在本機電腦上複製對應的GitHub存放庫。 另請參閱 [開發人員教學課程](https://www.aem.live/developer/tutorial) 以取得詳細資訊。 在本檔案中，Edge Delivery Service (EDS)專案的本機資料夾稱為 `[EDS Project repository]` .
* 確保您有權存取Google工作表或Microsoft SharePoint。 若要將Microsoft SharePoint設定為您的內容來源，請參閱 [如何使用Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint)



## 建立表單

+++ 步驟1：將最適化表單區塊新增至您的邊緣交付服務(EDS)專案。

此Adaptive可讓使用者為Edge Delivery Service網站建立表單。 不過，此區塊不包含在預設的AEM樣板中（用來建立Edge Delivery Service專案）。 若要將最適化表單區塊無縫整合至您的Edge Delivery Service專案：

1. **複製最適化表單區塊存放庫**：原地複製 [最適化表單區塊存放庫](https://github.com/adobe/afb) 本機電腦上。 它包含在EDS網頁上轉譯表單的程式碼。 在本檔案中，您的Forms Block存放庫的本機資料夾稱為 `[Adaptive Form block repository]`.
1. **找到最適化表單區塊存放庫：** 存取 [最適化表單區塊存放庫]/blocks資料夾並複製 `form` 資料夾。
1. **將最適化表單區塊貼入您的EDS專案：**
導覽至 [EDS專案存放庫]/blocks/資料夾貼上表單資料夾。
1. **將變更提交至GitHub：** 將表單資料夾及其基礎檔案簽入至GitHub上的邊緣傳遞服務專案。

完成上述步驟後，最適化表單區塊已成功新增至GitHub上的邊緣傳遞服務(EDS)專案存放庫。 您現在可以建立表單並新增至EDS Sites頁面。


**疑難排解GitHub建置問題**

解決下列潛在問題，確保GitHub建置流程順暢：

* **解決模組路徑錯誤：**
如果您遇到「無法解析模組「&#39;../../scripts/lib-franklin.js&#39;」的路徑」錯誤，請導覽至 [EDS專案]/blocks/forms/form.js檔案。 將lib-franklin.js檔案取代為aem.js檔案，以更新匯入陳述式。

* **處理Linting錯誤：**
如果您遇到任何連結錯誤，可以略過這些錯誤。 開啟 [EDS專案]/package.json檔案並將「lint」指令碼從「lint」：「npm run lint：js &amp;&amp; npm run lint：css」修改為「lint」：「echo &#39;skipping linting for now&#39;」。 儲存檔案並將變更提交至您的GitHub專案。



+++

+++ 步驟2：使用Microsoft Excel或Google工作表製作表單。

您可以使用試算表輕鬆完成表單的製作作業，而不需透過複雜的程式進行瀏覽。 首先，您可以將列和欄標題新增至試算表，其中每一列代表一個表單欄位，而每一欄標題則定義對應欄位的屬性。

例如，考慮下列試算表，其中的列大綱欄位用於 `enquiry` 表單和欄標題定義其屬性：

![查詢試算表](/help/edge/assets/enquiry-form-spreadsheet.png)

若要繼續建立表單：

1. 在Microsoft SharePoint或Google Drive上存取AEM Edge Delivery專案資料夾。

1. 在AEM Edge Delivery專案目錄中的任何位置建立Microsoft Excel活頁簿或Google工作表。 例如，在 Google Drive 上的 AEM Edge Delivery 專案目錄中，建立一個名為 `enquiry` 的試算表。

1. 確定工作表已和適當的AEM使用者共用(例如 `helix@adobe.com`) [根據專案指定的設定](https://www.aem.live/docs/setup-customer-sharepoint). 授予使用者工作表編輯許可權。

1. 開啟建立的試算表，並將預設工作表重新命名為「shared-default」。

   ![將預設試算表重新命名為「共用預設」](/help/edge/assets/rename-sheet-to-shared-default.png)

1. 若要新增表單欄位，請在「shared-default」工作表中插入列和欄標題。 每一列應代表 [表單欄位](/help/edge/docs/forms/form-components.md)，欄標題定義對應欄位 [屬性](/help/edge/docs/forms/eds-form-field-properties).

   為了快速起步，請考慮複製 [查詢試算表](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0) 放入您的試算表中。 複製內容後，請儲存試算表。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽頁面。

   ![使用AEM Sidekick預覽工作表](/help/edge/assets/preview-form.png)

   預覽時，新的瀏覽器標籤會以JSON格式顯示工作表內容。 請務必擷取預覽URL，因為這是呈現下一節中的表單所需。 URL格式如下：


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` 是指GitHub存放庫的分支。
   * `<repository>` 代表您的GitHub存放庫。
   * `<owner>` 是指代管GitHub存放庫的GitHub帳戶使用者名稱。

   例如，如果您的專案存放庫命名為「入口網站」，它位在帳戶「wkandforms」底下，而您使用的是「主要」分支，則URL看起來如下所示：

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ 步驟3：使用Edge Delivery Service (EDS)頁面預覽表單。


到目前為止，您已將最適化表單區塊新增到您的EDS專案中，並準備好表單的結構。 現在，若要預覽表單：

1. **存取您的專案目錄：** 開啟Microsoft SharePoint或Google Drive帳戶，並導覽至AEM Edge Delivery專案目錄。

1. **將表單內嵌至檔案：** 開啟檔案檔案（例如，索引檔案）以內嵌表單。 或者，您也可以建立新檔案。

1. **導覽至所需位置：** 移至檔案中您想要新增表單的位置。

1. **新增最適化表單區塊：** 將名為&#39;Form&#39;的區塊插入檔案中，如下圖所示：

   | 表單 |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

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

[準備您的試算表](/help/edge/docs/forms/submit-forms.md) 以在表單提交時開始接受資料。



## 了解更多

* [表單元件](/help/edge/docs/forms/form-components.md)
* [表單欄位屬性](/help/edge/docs/forms/eds-form-field-properties)
* [建立並預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單來傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈到網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [改變主題和樣式風格](/help/edge/docs/forms/style-theme-forms.md)
