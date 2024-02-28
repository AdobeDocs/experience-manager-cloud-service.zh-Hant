---
title: 使用文件型製作為 AEM Forms Edge Delivery Service 建立表單
description: 快速製作完美表單！⚡ AEM Forms Edge Delivery + 文件型製作 = 驚人的速度和 SEO 友善表單，讓使用者更滿意且適用於搜尋引擎。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f2752673dcaa0762bb55719cee23765aa8ecde96
workflow-type: ht
source-wordcount: '889'
ht-degree: 100%

---


# 使用文件型製作為 AEM Forms Edge Delivery Service 建立表單

身處今日數位時代，任何組織都需要建立對使用者友善的表單。AEM Forms Edge Delivery 的文件型製作功能讓您使用 Word 或 Google Docs 等熟悉的工具來建立表單。這些表單可直接提交資料至 Microsoft Excel 或 Google Sheets 檔案，讓您能夠使用由 Google Sheets、Microsoft Excel 和 Microsoft Sharepoint 等強大 API 建構的活躍生態系統，以便輕鬆處理提交的資料或啟動現有的業務工作流程。

本指南將引導您：

* 準備試用表：了解如何設定 Excel 或 Google Sheets 檔案，以便收集資料並在其中新增表單欄位。
* 將資料傳到工作表：了解使用 POST 請求將資料傳送到工作表。
* 發佈表單：將表單整合至您的 AEM Sites 頁面，或將其發佈為獨立頁面。

無論您是新手或專業人士，本指南都可以幫助您建立使用者喜愛的美觀、實用表單。讓我們盡情建立有效表單 - 現在就開始！

## 開始之前

`WIP`

## 準備試算表並接受資料

1. 在 Microsoft OneDrive 或 Google Drive 上的 AEM Edge Delivery 專案目錄下，在任何位置建立 Microsoft Excel 活頁簿或 Google Sheet。本文件會使用名為`contact-us.xlsx`的 Google Sheet，位於 Adob&#x200B;&#x200B;e Experience Manager (AEM) 專案的根目錄。

1. 確保為您專案設定的 AEM 使用者 (例如 helix@adobe.com) 擁有工作表的編輯權限。

1. 開啟您建立的活頁簿並將預設工作表的名稱變更為「傳入」。

   >[!NOTE]
   >
   > 如果「傳入」工作表不存在，AEM 不會向此活頁簿傳送任何資料。

1. 在 Sidekick 中預覽工作表。

   >[!NOTE]
   >
   >即使以前已預覽過該工作表，在第一次建立「傳入」工作表後也必須再次預覽。

1. 新增與您要輸入資料相符的標題來準備工作表。以下範例顯示「聯絡我們」表單的欄位：

   ![聯絡我們表單的欄位](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   您可以手動執行此操作，也可以使用 AEM Admin 服務中表單路徑的 POST 請求來執行此操作。這項管理服務將檢查 POST 內文中的資料，並產生有效擷取資料並充分利用 Forms 服務所需的適當標題、表格和工作表。

   若要了解如何制訂用來設定工作表的 POST 請求格式，請參閱「[Admin API 文件](https://www.hlx.live/docs/admin.html#tag/form)」。此外，請看一下下面提供的範例：

   **請求**

   ```JSON
   POST 'https://admin.hlx.page/form/{owner}/{repo}/{branch}/contact-us.json' \
   --header 'Content-Type: application/json' \
   --data '{
       "data": {
           "Email": "john@wknd.com",
           "Name": "John",
           "Subject": "Regarding Product Inquiry",
           "Message": "I have some questions about your products.",
           "Phone": "123-456-7890",
           "Company": "Adobe Inc.",
           "Country": "United States",
           "PreferredContactMethod": "Email",
           "SubscribeToNewsletter": true
       }
   }'
   ```

   **回應**

   ```JSON
   HTTP/2 200 
   content-type: application/json
   x-invocation-id: 1b3bd30a-8cfb-4f85-a662-4b1f7cf367c5
   cache-control: no-store, private, must-revalidate
   accept-ranges: bytes
   date: Sat, 10 Feb 2024 09:26:48 GMT
   via: 1.1 varnish
   x-served-by: cache-del21736-DEL
   x-cache: MISS
   x-cache-hits: 0
   x-timer: S1707557205.094883,VS0,VE3799
   strict-transport-security: max-age=31557600
   content-length: 138
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country","PreferredContactMethod","SubscribeToNewsletter"]}%
   ```

   您可以使用 curl 或 Postman 等工具來執行此 POST 請求，如下所示：

   ```JSON
   curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
       --header 'Content-Type: application/json' \
       --data '{
           "data": {
               "Email": "john@wknd.com",
               "Name": "John",
               "Subject": "Regarding Product Inquiry",
               "Message": "I have some questions about your products.",
               "Phone": "123-456-7890",
               "Company": "Wknd Inc.",
               "Country": "United States",
               "PreferredContactMethod": "Email",
               "SubscribeToNewsletter": true
       }
   }'
   ```

上述 POST 請求提供了範例資料，包括表單欄位及其個別的範例值。Admin 服務會使用此資料來設定表單。

雖然 Admin 服務&#x200B;&#x200B;建議設定您的工作表，但如果您喜歡手動建立標題，請參閱名為「[手動表單設定](https://www.hlx.live/docs/manual-forms-sheet-setup)」的文件。

向 Admin 服務提交 POST 請求後，您將在活頁簿中觀察到以下變動：

* 名為「共用預設」的新工作表將會新增到您的 Excel 活頁簿或 Google Sheet 中。在向工作表發出 GET 請求時，系統將擷取「共用預設」工作表中出現的資料。此工作表是使用試算表公式總結傳入資料的最佳位置，使其有利於在其他情況下使用。

  在任何情況下，「共用預設」工作表都不應包含您不願意開放存取的任何個人識別資料或敏感資料。

* 名為「slack」的工作表會新增至您的 Excel 活頁簿或 Google Sheet 中。在此工作表中，當系統擷取新資料至試算表中時，您可以為指定的 Slack 頻道設定自動通知。目前，AEM 僅支援向 AEM Engineering Slack 組織和 Adob&#x200B;&#x200B;e Enterprise 支援組織發送通知。

   1. 若要設定 Slack 通知，請輸入 Slack 工作區的「teamId」和「頻道名稱」或「ID」。您也可以向 Slack 機器人 (使用 debug 指令) 要求「teamId」和「頻道 ID」。最好使用「頻道 ID」而不是「頻道名稱」，因為這樣可以在頻道重新命名後繼續存在。

      >[!NOTE]
      >
      > 舊的表單沒有「teamId」欄。「teamId」會包含在頻道欄中，並且以「#」或「/」分隔。

   1. 輸入您想要的任何標題，然後在欄位下輸入您想要在 Slack 通知中看到的欄位名稱。每個標題應以逗號分隔 (例如姓名、電子郵件)。

此工作表現已設定為接受資料，您可以使用 hlx.page、hlx.live 或您的生產網域直接向其發送 POST 請求。


## 將資料傳送到您的工作表 {#send-data-to-your-sheet}

將工作表設定為接受資料後，您可以使用 hlx.page、hlx.live 或您的生產網域直接向其發送 POST 請求以傳送資料。

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL 不應有 .json 副檔案名稱。您必須發佈 POST 操作的工作表才能在 .live 或生產網域上運作。

### 為 EDS Forms 的資料格式化

您可使用幾種不同法來格式化 POST 內文中的表單資料。

* name:value 配對組陣列：

  ```JSON
  {
    "data": [
      { "name": "name", "value": "Clark Kent" },
      { "name": "email", "value": "superman@example.com" },
      { "name": "subject", "value": "Regarding Product Inquiry" },
      { "name": "message", "value": "I have some questions about your products." },
      { "name": "phone", "value": "123-456-7890" },
      { "name": "company", "value": "Example Inc." },
      { "name": "country", "value": "United States" },
      { "name": "preferred_contact_method", "value": "Email" },
      { "name": "newsletter_subscribe", "value": true }
    ]
  }
  ```

  例如

  ```JSON
      curl -s -i -X POST 'https://main--portal--wkndforms.hlx.page/contact-us' \
          --header 'Content-Type: application/json' \
          --data '{
          "data": [
              { "name": "name", "value": "Clark Kent" },
              { "name": "email", "value": "superman@example.com" },
              { "name": "subject", "value": "Regarding Product Inquiry" },
              { "name": "message", "value": "I have some questions about your products." },
              { "name": "phone", "value": "123-456-7890" },
              { "name": "company", "value": "Example Inc." },
              { "name": "country", "value": "United States" },
              { "name": "preferred_contact_method", "value": "Email" },
              { "name": "newsletter_subscribe", "value": true }
              ]
          }'
  
* 具備 key:value 配對組的物件

  ```JSON
      {
        "data": {
          "name": "Jessica Jones",
          "email": "jj@example.com",
          "subject": "Regarding Product Inquiry",
          "message": "I have some questions about your products.",
          "phone": "123-456-7890",
          "company": "Example Inc.",
          "country": "United States",
          "preferred_contact_method": "Email",
          "newsletter_subscribe": true
        }
      }
  ```

* `x-www-form-urlencoded` 內文 (`content-type` 標題必須設定為 `application/x-www-form-urlencoded`)
&#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



