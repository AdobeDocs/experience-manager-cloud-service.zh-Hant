---
title: 從試算表到Forms — 掌握表單區塊欄位驗證
description: 使用試算表和表單區塊欄位，更快製作強大的表單！ 本指南可協助您建立EDS Forms區塊欄位的自訂驗證。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---


# 啟用您的表單以傳送資料

建立及預覽表單後，請啟用對應的工作表以接受資料。 若要開始接受資料，請設定試算表以包含符合您要收集之資料的標題。 新增至「shared-default」工作表的所有標題也應該出現在表格下的「incoming」工作表中。

下列範例會顯示「聯絡我們」表單的欄位：

![聯絡人表單的欄位](/help/edge/assets/contact-us-form-excel-sheet-fields.png)


完成此設定後，您的表單就準備好可以接受提交了。 您可以採用下列其中一種方法，讓試算表接受資料：

* [手動設定試算表以接受資料](#manually-configure-a-spreadsheet-to-receive-data)

* [使用Admin API啟用試算表以接受資料](#use-admin-apis-to-enable-a-spreadsheet-to-receive-data-use-admin-apis-to-enable-a-spreadsheet-to-recieve-data)

## 手動設定試算表以接受資料

若要手動設定試算表以接受資料：


1. 開啟您建立的活頁簿，並將預設工作表名稱變更為「傳入」。

   >[!WARNING]
   >
   > 如果「傳入」工作表不存在，AEM將不會傳送任何資料到此活頁簿。

1. 新增符合您輸入資料的標題以準備工作表。 下列範例會顯示「聯絡我們」表單的欄位：

   ![聯絡人表單的欄位](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. 在Sidekick中預覽工作表。

   >[!NOTE]
   >
   >即使您之前已預覽過工作表，您也必須在第一次建立「傳入」工作表之後再次預覽它。


## 使用Admin API啟用試算表以接受資料

您可以在AEM管理服務內起始表單路由的POST請求。 收到POST內文資料後，Admin服務會加以分析，並自主產生資料擷取所需的必要標題、表格和工作表，進而最佳化Forms服務的功能。

若要使用Admin API讓試算表接受資料：


1. 開啟您建立的活頁簿，並將預設工作表名稱變更為「傳入」。

   >[!WARNING]
   >
   > 如果「傳入」工作表不存在，AEM將不會傳送任何資料到此活頁簿。

1. 在Sidekick中預覽工作表。

   >[!NOTE]
   >
   >即使您之前已預覽過工作表，您也必須在第一次建立「傳入」工作表之後再次預覽它。

1. 新增符合您輸入資料的標題以準備工作表。

   若要這麼做，請傳送POST要求至AEM管理服務中的表單路由。 管理員服務會檢查POST內文中的資料，並產生所需的適當標題、表格和工作表，以有效擷取資料並充分利用Forms服務。

   若要瞭解如何設定POST要求的格式，以設定您的工作表，請參閱 [管理API檔案](https://www.hlx.live/docs/admin.html#tag/form). 此外，請檢視以下提供的範例：

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
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country",      "PreferredContactMethod","SubscribeToNewsletter"]}%
   ```

   您可以使用curl或Postman之類的工具來執行此POST請求，如下所示：

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

   前述的POST請求提供範例資料，包括表單欄位及其各自的範例值。 管理員服務會使用此資料來設定表單。

   將POST請求提交至Admin Service後，您會在活頁簿中觀察到下列變更：

* 名為「shared-default」的新工作表會新增至Excel活頁簿或Google工作表。 當對工作表發出GET請求時，會擷取「shared-default」工作表中存在的資料。 此工作表是最佳位置，可供您使用試算表公式來彙總傳入的資料，使其有利於在其他情境中消耗。

  「shared-default」工作表不應包含您不喜歡公開存取的任何個人識別資訊或敏感資料。

* 名為「Slack」的工作表會新增至Excel活頁簿或Google工作表。 在此工作表中，每當新資料內嵌至試算表時，您都可以為指定的Slack頻道設定自動通知。 目前，AEM僅支援AEM工程Slack組織和Adobe企業支援組織的通知。

   1. 若要設定Slack通知，請輸入Slack工作區的「teamId」以及「頻道名稱」或「ID」。 您也可以向Slack-bot （使用偵錯命令）詢問「teamId」和「channel ID」。 建議改用「管道ID」而非「管道名稱」，因為這樣可在重新命名管道前使用。

      >[!NOTE]
      >
      > 較舊的表單沒有「teamId」欄。 「teamId」包含在頻道欄中，以「#」或「/」分隔。

   1. 輸入任何您想要的標題，並在欄位底下輸入您要在Slack通知中看到的欄位名稱。 每個標題應以逗號分隔（例如名稱、電子郵件）。

工作表現在已設定為可接收資料，您可以 [使用forms區塊預覽表單](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) 或 [使用POST請求](#use-admin-apis-to-send-data-to-your-sheet) 以開始傳送資料至工作表。



## 傳送資料至您的工作表 {#send-data-to-your-sheet}

將工作表設定為接收資料後，您可以 [使用forms區塊預覽表單](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) 或 [使用管理API](#use-admin-apis-to-send-data-to-your-sheet) 以開始傳送資料至工作表。

### 使用管理API傳送資料至您的工作表

您可以使用hlx.page、hlx.live或您的生產網域直接將POST請求傳送至您的表單，以傳送資料。


```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL的副檔名不應為.json。 您必須發佈工作表才能進行POST作業 `.live` 或在生產網域上。

#### 格式化表單資料

有幾種不同的方式可以格式化POST本文中的表單資料。 您可以使用：

* 陣列 `name:value` 配對：

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
          { "name": "message", "value": "I have some questions about your        products." },
          { "name": "phone", "value": "123-456-7890" },
          { "name": "company", "value": "Example Inc." },
          { "name": "country", "value": "United States" },
          { "name": "preferred_contact_method", "value": "Email" },
          { "name": "newsletter_subscribe", "value": true }
      ]
  }'
  ```



* 物件，具有 `key:value` 配對：

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

  例如，

  ```JSON
  curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
  --header 'Content-Type: application/json' \
  --data '{
      "data": {
          "Email": "khushwant@wknd.com",
          "Name": "khushwant",
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

* URL已編碼(`x-www-form-urlencoded`)內文(含 `content-type` 標題設為 `application/x-www-form-urlencoded`)

  ```Shell
  'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'
  ```

  例如，

  ```Shell
  curl -s -i -X POST \
    -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
    https://main--portal--wkndforms.hlx.live/contact-us
  ```

接下來，您可以自訂感謝訊息， [設定感謝頁面](/help/edge/docs/forms/thank-you-page-form.md)，或 [設定重新導向](/help/edge/docs/forms/thank-you-page-form.md).

## 檢視更多

* [建立及預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單以傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈至網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [變更表單的主題和樣式](/help/edge/docs/forms/style-theme-forms.md)