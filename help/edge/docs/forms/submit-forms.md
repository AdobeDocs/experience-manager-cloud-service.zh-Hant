---
title: 準備您的試算表以接受資料
description: 使用試算表和表單區塊欄位，更快製作強大的表單！
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bd8c4fbfd7f740baa6abd7a91fb8d1dcdaff6c28
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 0%

---


# 準備您的試算表以接受資料

一旦您 [已建立和預覽表單](/help/edge/docs/forms/create-forms.md)，是時候啟用對應的試算表來開始接收資料了。

>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

若要啟用試算表：

1. 開啟具有表單的試算表，然後附加新工作表，將其重新命名為 `incoming`.

   >[!WARNING]
   >
   > 如果 `incoming` 工作表不存在，AEM不會將任何資料傳送至試算表。

1. 映象表單欄位名稱，值 `Name` 中的欄`shared-default` 工作表，到中的標題 `incoming` 工作表。

   中的每一個值 `Name` 的欄 `shared-default` 工作表（不包括提交按鈕）會作為頁首 `incoming` 工作表。 例如，請考慮下圖說明「contact-us」表單的標題：

   ![聯絡人表單的欄位](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. 使用sidekick預覽工作表。

   >[!NOTE]
   >
   >即使您之前已預覽過工作表，您仍必須在建立工作表之後再次預覽 `incoming` 第一次使用工作表。


將欄位名稱新增至 `incoming` 工作表，您的表單就準備好可以接受提交了。 您可以預覽表單，並使用表單將資料提交至工作表。

您也會在試算表中觀察到下列變更：

名為「Slack」的工作表會新增至Excel活頁簿或Google工作表。 在此工作表中，每當新資料內嵌至試算表時，您都可以為指定的Slack頻道設定自動通知。 目前，AEM僅支援AEM工程Slack組織和Adobe企業支援組織的通知。

1. 若要設定Slack通知，請輸入Slack工作區的「teamId」以及「頻道名稱」或「ID」。 您也可以向Slack-bot （使用偵錯命令）詢問「teamId」和「channel ID」。 建議改用「管道ID」而非「管道名稱」，因為這樣可在重新命名管道前使用。

   >[!NOTE]
   >
   > 較舊的表單沒有「teamId」欄。 「teamId」包含在頻道欄中，以「#」或「/」分隔。

1. 輸入任何您想要的標題，並在欄位底下輸入您要在Slack通知中看到的欄位名稱。 每個標題應以逗號分隔（例如名稱、電子郵件）。

   >[!WARNING]
   >
   >  「shared-default」工作表不應包含您不喜歡公開存取的任何個人識別資訊或敏感資料。


## （選用）使用Admin API啟用試算表以接受資料

您也可以傳送POST要求至表單，讓其接受資料並設定標題 `incoming` 工作表。 在收到POST請求後，此服務會分析請求內文，並自主產生資料擷取所需的必要標題和工作表。

若要使用Admin API讓試算表接受資料：


1. 開啟您已建立的活頁簿，並將預設工作表的名稱變更為 `incoming`.

   >[!WARNING]
   >
   > 如果 `incoming` 工作表不存在，AEM不會將任何資料傳送至此活頁簿。

1. 在Sidekick中預覽工作表。

   >[!NOTE]
   >
   >即使您之前已預覽過工作表，您仍必須在建立工作表之後再次預覽 `incoming` 第一次使用工作表。

1. 傳送POST請求以在中產生適當的標頭 `incoming` 工作表，然後新增 `shared-default` 頁面至您的試算表（如果尚未存在）。

   若要瞭解如何設定POST要求的格式，以設定您的工作表，請參閱 [管理API檔案](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). 您可以檢視以下提供的範例：

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

   上述POST請求提供範例資料，包括表單欄位及其各自的範例值。 管理員服務會使用此資料來設定表單。

   您的表單現在已啟用以接受資料。 您也會在試算表中觀察到下列變更：

名為「Slack」的工作表會新增至Excel活頁簿或Google工作表。 在此工作表中，每當新資料內嵌至試算表時，您都可以為指定的Slack頻道設定自動通知。 目前，AEM僅支援AEM工程Slack組織和Adobe企業支援組織的通知。

1. 若要設定Slack通知，請輸入Slack工作區的「teamId」以及「頻道名稱」或「ID」。 您也可以向Slack-bot （使用偵錯命令）詢問「teamId」和「channel ID」。 建議改用「管道ID」而非「管道名稱」，因為這樣可在重新命名管道前使用。

   >[!NOTE]
   >
   > 較舊的表單沒有「teamId」欄。 「teamId」包含在頻道欄中，以「#」或「/」分隔。

1. 輸入任何您想要的標題，並在欄位底下輸入您要在Slack通知中看到的欄位名稱。 每個標題應以逗號分隔（例如名稱、電子郵件）。


工作表現在已設定為可接收資料，您可以 [使用forms區塊預覽表單](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) 或 [使用POST請求](#use-admin-apis-to-send-data-to-your-sheet) 以開始傳送資料至工作表。

>[!WARNING]
>
>  「shared-default」工作表不應包含您不喜歡公開存取的任何個人識別資訊或敏感資料。

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