---
title: 發佈 AEM Forms Edge Delivery Services Form
description: 發佈 AEM Forms Edge Delivery Services Form
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 10%

---


# 發佈您的表單

準備好與您的客戶共用表單以進行資料收集或提交後，您就可以發佈表單，讓客戶隨時可以使用表單。

## 先決條件

* 此 [已在GitHub上為您的EDS專案啟用最適化表單區塊](/help/edge/docs/forms/create-forms.md).
* 您的表單已完整測試且可供使用。
* 您的 [試算表已設定](/help/edge/docs/forms/submit-forms.md) 以接受資料。

## 發佈您的表單

+++ 1.發佈您的試算表

1. 開啟Microsoft SharePoint或Google Drive帳戶，並導覽至AEM Edge Delivery專案目錄。

1. 開啟具有您的表單的試算表。 例如， `enquiry` 表單Microsoft Excel活頁簿。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽頁面。

   ![使用AEM Sidekick預覽工作表](/help/edge/assets/preview-form.png)

   成功完成預覽作業後，試算表內容會轉換為JSON格式。 預覽頁面接著會以結構化表格格式顯示此內容。 例如，隨附的影像會說明「查詢」表單的內容。

   ![Forms預覽JSON格式](/help/edge/assets/forms-preview-json-format.png)

1. 使用AEM Sidekick發佈工作表。 請務必擷取發佈URL，因為這是呈現下一區段中的表單所需。 URL格式如下：


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` 是指GitHub存放庫的分支。
   * `<repository>` 代表您的GitHub存放庫。
   * `<owner>` 是指代管GitHub存放庫的GitHub帳戶使用者名稱。

   例如，如果您的專案存放庫命名為「入口網站」，它位在帳戶「wkandforms」底下，而您使用的是「主要」分支，則URL看起來如下所示：

   `https://main--portal--wkndforms.hlx.page/enquiry.json`

+++

+++ 2.將表單新增至網頁

新增 `<form>.json` 以方便客戶互動，讓表單填寫者輕鬆填寫及提交表單。


若要將表單新增至網頁：

1. 存取您的Microsoft SharePoint或Google Drive帳戶，並導覽至 `[AEM Edge Delivery project directory]`.

1. 開啟您打算嵌入表單的檔案檔案。 例如，您可以開啟 `index.docx` 檔案，或建立新檔案。

1. 識別檔案中要插入表單的所需區段，並據此導覽至該區段。

1. 將名為「Form」的區塊新增至檔案，類似於以下提供的範例：

   | 表單 |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   此區塊可作為內嵌表單的預留位置。 在區塊的第二列中，新增 `<form>.json` 檔案做為超連結。

   >[!IMPORTANT]
   >
   >
   > 請確定URL的格式為超連結，而非顯示為純文字。

   將預覽URL (.page URL)用於開發或測試目的，或將發佈URL (.live)用於生產。 以下是預覽和發佈URL的範例：

   **預覽URL**
| 表單 | |—| | [https://main--portal--wkndforms.hlx.page/enquiry.json](https://main--portal--wkndforms.hlx.page/enquiry.json)  |


   **發佈URL**
| 表單 | |—| | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json)  |

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽網頁。 頁面現在會顯示表單。例如，以下是根據 [查詢試算表](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0)：


   [![EDS表單範例](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

1. 使用AEM Sidekick發佈表單。 現在，您的客戶可以填寫並提交表單。

+++

## 疑難排解

+++ 無法提交資料至表單

如果您遇到類似下列訊息的錯誤，表示試算表未設定為 [接受已提交的](/help/edge/docs/forms/submit-forms.md) 資料尚未完成。

![在表單提交時的錯誤](/help/edge/assets/form-error.png)

+++


## 了解更多

* [建立並預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單來傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈到網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [改變主題和樣式風格](/help/edge/docs/forms/style-theme-forms.md)
