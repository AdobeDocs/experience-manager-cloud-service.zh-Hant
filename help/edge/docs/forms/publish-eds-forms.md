---
title: 發佈 AEM Forms Edge Delivery Services Form
description: 發佈 AEM Forms Edge Delivery Services Form
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 3b24d0cd4099e0b8eb48c977f460b25c168af220
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 19%

---


# 發佈您的表單

準備好與您的客戶共用表單以進行資料收集或提交後，您就可以發佈表單，讓客戶隨時可以使用表單。

## 先決條件

* 此 [已在Github上為您的EDS專案啟用表單區塊](/help/edge/docs/forms/create-forms.md).
* 您的表單已完整測試且可供使用。
* 您的 [試算表已設定](/help/edge/docs/forms/submit-forms.md) 以接受資料。

## 發佈您的表單

若要發佈表單：

1. 存取您的Microsoft SharePoint或Google Drive帳戶，並導覽至 `[AEM Edge Delivery project directory]`.

1. 開啟您打算嵌入表單的檔案檔案。 例如，您可以開啟索引檔案，或建立新檔案。

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

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽頁面。頁面現在會顯示表單。例如，以下是根據 [查詢試算表](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0)：


   [![EDS表單範例](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   現在，您的客戶可以填寫並提交表單。

## 疑難排解

+++ 無法提交資料至表單

如果您遇到類似下列訊息的錯誤，表示試算表尚未設定為接受提交的資料。

![在表單提交時的錯誤](/help/edge/assets/form-error.png)

+++


## 了解更多

* [建立並預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單來傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈到網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [改變主題和樣式風格](/help/edge/docs/forms/style-theme-forms.md)