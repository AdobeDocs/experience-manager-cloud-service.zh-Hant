---
title: 發佈 AEM Forms Edge Delivery Services Form
description: 發佈 AEM Forms Edge Delivery Services Form
feature: Edge Delivery Services
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
source-git-commit: b32e04dec83992ebfcea7874932a5ab77a1eaa70
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 92%

---

# 發佈您的表單

一旦您準備好與客戶分享表單以收集或提交資料，您只需發佈表單並供客戶隨時使用即可。

![檔案式撰寫生態系統](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## 必要條件 

* 您的AEM專案是根據 [AEM Forms範本](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) 或 [已將最適化Forms區塊新增至您現有的AEM專案](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)
* 您的表單已經過全面測試並可供使用。
* 您的[試算表已設定](/help/edge/docs/forms/submit-forms.md)可接受資料。


## 發佈您的表單

+++ 1. 發佈您的試算表

1. 開啟 Microsoft SharePoint 或 Google Drive 帳戶，然後導覽至您的 AEM Edge Delivery 專案目錄。

1. 開啟包含您表單的試算表。例如， `enquiry`表單 Microsoft Excel 工作簿。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽工作表。

   ![使用 AEM Sidekick 來預覽工作表](/help/edge/assets/preview-form.png)

   成功完成預覽作業後，試算表內容將轉換為 JSON 格式。然後，預覽頁面以結構化表格格式呈現該內容。例如，附圖說明「查詢」表單的內容。

   ![表單預覽 JSON 格式](/help/edge/assets/forms-preview-json-format.png)

1. 使用 AEM Sidekick 來發佈工作表。確保擷取發佈 URL，因為這是在下個區段中呈現表單必要的項目。URL 格式如下：


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>`是指 GitHub 存放庫的分支。
   * `<repository>`表示您的 GitHub 存放庫。
   * `<owner>`是指託管 GitHub 存放庫的 GitHub 帳戶使用者名稱。

   例如，如果您的專案存放庫名為 “portal” (位於帳戶 “wkndforms” 下面)，並且您使用的是「主要」分支，則 URL 如下所示：

   `https://main--portal--wkndforms.hlx.page/enquiry.json`

+++

+++ 2. 新增表單至您的網頁

將`<form>.json`新增至網頁以方便客戶互動，讓表單填寫者能夠輕鬆填寫並提交表單。


若要新增表單至您的網頁：

1. 存取您的 Microsoft SharePoint 或 Google Drive 帳戶並導覽到您的 `[AEM Edge Delivery project directory]`。

1. 開啟要嵌入表單的文件檔案。例如，您可以開啟 `index.docx` 檔案，或建立一個新文件。

1. 確定文件中要插入表單的所要區段，然後導覽至該區段。

1. 新增名為 &#39;Form&#39; 的區塊至檔案中，類似於下面提供的範例。

   | 表單 |
   |---|
   | [https://main--wefinance--wkndforms.hlx.live/enquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json) |

   ![將名為&#39;Form&#39;的區塊新增至檔案](/help/edge/assets/enquiry-doc-to-embed-form.png)

   此區塊是用作嵌入表單的暫留位置。在該區塊的第二行中，新增 `<form>.json` 檔案的 URL 作為超連結。

   >[!IMPORTANT]
   >
   >
   > 確保 URL 的格式為超連接，而不是顯示為純文字。

   使用預覽 URL (.page URL) 進行開發或測試，或使用發佈 URL (.live) 進行生產。以下是帶有預覽和發佈 URL 的範例：

   **預覽URL**
| 表單 | |—| | [https://main--wefinance--wkndforms.hlx.page/enquiry.json](https://main--wefinance--wkndforms.hlx.page/enquiry.json)  |


   **發佈URL**
| 表單 | |—| | [https://main--wefinance--wkndforms.hlx.live/enquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json)  |

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽網頁。頁面現在會顯示表單。例如，這是以[查詢試算表](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0)為主的表單：


   ![EDS Forms 範本](/help/edge/assets/eds-form.png)

1. 使用 AEM Sidekick 來發佈表單。現在，您的客戶可以填寫表格並提交。

+++

## 疑難排解

+++ 無法向表單提交資料

如果您遇到類似以下訊息的錯誤，則表示試算表尚未設定為[接受提交的](/help/edge/docs/forms/submit-forms.md)資料。

![在表單提交時的錯誤](/help/edge/assets/form-error.png)

+++


## 另請參閱

{{see-more-forms-eds}}
