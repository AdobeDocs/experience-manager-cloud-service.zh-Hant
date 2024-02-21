---
title: 使用檔案式撰寫功能，為AEM Forms Edge Delivery Service建立表單
description: 製作完美的表單，快速！ ⚡ AEM Forms Edge Delivery + doc-based authoring =速度飛快、適合SEO使用的表單，適合更快樂的使用者和搜尋引擎。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f2752673dcaa0762bb55719cee23765aa8ecde96
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# 使用檔案式撰寫功能，為AEM Forms Edge Delivery Service建立表單

在當今的數位時代，建立好用的表單對於任何組織都至關重要。 AEM Forms Edge Delivery的檔案式撰寫功能可讓您使用熟悉的工具(如Word或Google檔案)建立表單。這些表單會直接將資料提交至Microsoft Excel或Google Sheets檔案，讓您能夠使用生氣勃勃的生態系統以及強大的API (如Google Sheets、Microsoft Excel和Microsoft Sharepoint)，以輕鬆處理提交的資料或啟動現有的業務工作流程。

本指南會逐步引導您瞭解：

* 準備試算表：瞭解如何設定Excel或Google工作表檔案以進行資料收集，以及在其中新增表單欄位。
* 傳送資料至您的工作表：瞭解如何使用POST請求傳送資料至您的工作表。
* 發佈表單：將表單整合至AEM Sites頁面，或發佈為獨立頁面。

無論您是新手還是專業人士，本指南都能讓您建立使用者喜愛的精美、功能性的表單。 讓我們解放建立有效率的表單 — 現在就開始吧！

## 開始之前

`WIP`

## 準備您的試算表以接收資料

1. 在Microsoft OneDrive或Google Drive的AEM Edge Delivery專案目錄下，隨處建立Microsoft Excel活頁簿或Google工作表。 本檔案使用名為的Google工作表 `contact-us.xlsx`，位於Adobe Experience Manager (AEM)專案的根目錄。

1. 請確定針對您的專案設定的AEM使用者(例如helix@adobe.com)擁有工作表的編輯許可權。

1. 開啟您建立的活頁簿，並將預設工作表名稱變更為「傳入」。

   >[!NOTE]
   >
   > 如果「傳入」工作表不存在，AEM將不會傳送任何資料到此活頁簿。

1. 在Sidekick中預覽工作表。

   >[!NOTE]
   >
   >即使您之前已預覽過工作表，您也必須在第一次建立「傳入」工作表之後再次預覽它。

1. 新增符合您輸入資料的標題以準備工作表。 下列範例會顯示「聯絡我們」表單的欄位：

   ![聯絡人表單的欄位](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   您可以手動進行此操作，或使用AEM管理服務中表單路由的POST請求。 管理員服務將檢查POST內文中的資料，並產生所需的適當標題、表格和工作表，以有效擷取資料並充分利用Forms服務。

   若要瞭解如何設定POST要求的格式，以設定您的工作表，請參閱 [管理API檔案](https://www.hlx.live/docs/admin.html#tag/form). 此外，請考量下列提供的範例：

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

雖然Admin服務建議設定您的工作表，但如果您偏好手動建立標題，請參閱檔案 [手動設定Forms工作表](https://www.hlx.live/docs/manual-forms-sheet-setup).

將POST請求提交至Admin Service後，您會在活頁簿中看到下列變更：

* 名為「shared-default」的新工作表會新增至Excel活頁簿或Google工作表。 當對工作表發出GET請求時，會擷取「shared-default」工作表中存在的資料。 此工作表是最佳位置，可讓您使用試算表公式來摘要傳入的資料，因此有助於在其他情境中消耗。

  「shared-default」工作表在任何情況下都不應包含您不想公開存取的任何個人識別資訊或敏感資料。

* 名為「slack」的工作表會新增至Excel活頁簿或Google工作表。 在此工作表中，每當新資料內嵌至試算表時，您都可以為指定的Slack頻道設定自動通知。 目前，AEM僅支援AEM工程Slack組織和Adobe企業支援組織的通知。

   1. 若要設定Slack通知，請輸入Slack工作區的「teamId」以及「頻道名稱」或「ID」。 您也可以向Slack-bot （使用偵錯命令）詢問「teamId」和「channel ID」。 建議改用「管道ID」而非「管道名稱」，因為這樣可在重新命名管道前使用。

      >[!NOTE]
      >
      > 較舊的表單沒有「teamId」欄。 「teamId」包含在頻道欄中，以「#」或「/」分隔。

   1. 輸入您想要的任何標題，並在欄位底下輸入您要在Slack通知中看到的欄位名稱。 每個標題應以逗號分隔（例如名稱、電子郵件）。

工作表現在已設定為可接收資料，而您可以使用hlx.page、hlx.live或您的生產網域直接傳送POST請求給工作表。


## 傳送資料至您的工作表 {#send-data-to-your-sheet}

工作表設定為接收資料後，您可以使用hlx.page、hlx.live或您的生產網域直接將POST請求傳送給工作表，以傳送資料。

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL的副檔名不應為.json。 您必須發佈工作表，POST作業才能在.live或生產網域上運作。

### 為EDS Forms格式化資料

有幾種不同的方式可以格式化POST本文中的表單資料。

* 名稱：值配對的陣列：

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
  
* 具有索引鍵：值配對的物件

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

* `x-www-form-urlencoded` 內文(`content-type` 標題必須設為 `application/x-www-form-urlencoded`) &#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



