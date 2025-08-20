---
title: 提交表單後顯示自訂感謝訊息
description: 了解如何設定 Forms 區塊的感謝頁面和重新導向，以最佳化使用者體驗並簡化使用者歷程。
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '557'
ht-degree: 100%

---

# 提交表單後顯示自訂感謝訊息

在使用者提交表單後，請務必透過感謝訊息提供順暢的體驗。不僅可以確認成功提交，還可以提高使用者滿意度並引導他們繼續之後的歷程。

- **感謝訊息**：感謝訊息是使用者體驗的重要基礎，一方面可加強品牌識別，另一方面可提供保證並傳達重要訊息。此頁面是對使用者行為的直接認可，讓他們產生一種完成後的滿足感。

- **重新導向**：重新導向可發揮關鍵作用，旨在引導使用者前往相關目的地、提高最佳參與度且最後達到更高轉換率。重新導向可無縫引導使用者進入下一步歷程，確保使用者得到流暢的導覽體驗。例如，在收集初始的詳細資料後，將使用者重新導向至付款頁面。

最適化表單區塊的預設行為是在提交時顯示以下的感謝訊息。成功提交表單後，該訊息將顯示在表單最上方。

![預設感謝訊息](/help/edge/assets/thank-you-message.png)

但是，您可以靈活地自訂這項體驗，以滿足您的特定需求。選項包括：    

- 提交表單後顯示自訂感謝訊息
- 提交後，將使用者重新導向至另一個頁面，以便進行後續動作

>[!NOTE]
>
> 您可以參考下方的[查詢試算表](/help/edge/docs/forms/assets/enquiry.xlsx)，根據您的要求自訂感謝訊息。

## 設定自訂感謝訊息

如果您想在成功提交表單後顯示個人化的感謝訊息，可以設定試算表以顯示該訊息。

請依照以下步驟為您的最適化表單區塊設定自訂感謝訊息：

1. 前往 Microsoft SharePoint 或 Google Workspace 的 Edge Deliver 專案資料夾，並開啟您的試算表。
1. 在試算表的 `submit` 欄位類型的 `value` 欄中新增自訂感謝訊息。

   ![自訂感謝訊息](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   例如，在 `submit` 欄位類型的 `value` 欄新增 `Submission Successful!` 訊息。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

   ![自訂感謝訊息](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## 提交後將使用者重新導向至另一個頁面

提交表單後將使用者重新導向至另一個頁面，可提供相關資訊、確認動作並引導使用者前往期望的結果頁面，藉此加強使用者體驗。例如，

- 使用者填寫購買表單後，他們將被重新導向至付款頁面，以安全方式完成交易。
- 提交活動或網路研討會的註冊表單後，使用者將被重新導向至顯示活動詳細資訊 (例如日期、時間和地點) 的確認頁面。

請按照以下步驟，將使用者重新導向到另一個頁面：

1. 前往 Microsoft SharePoint 或 Google Workspace 的 Edge Deliver 專案資料夾，並開啟您的試算表。
1. 將 URL 貼到試算表中 `submit` 欄位類型的 `value` 欄，以便在成功提交表單後重新導向使用者。
若要將頁面重新導向到其他頁面，請使用 [Edge Delivery 文件](https://www.aem.live/docs/)頁面 URL。

   ![感謝重新導向 URL](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

   ![重新導向感謝訊息](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

您也可以建立新文件檔案，並在 `submit` 欄位類型的 `value` 欄中新增其預覽 URL。

使用者提交表單後，請務必提供清楚的感謝訊息。這樣可以確認提交成功並提高使用者滿意度。

