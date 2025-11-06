---
title: 準備試算表並接受資料
description: 使用試算表和最適化表單區塊欄位更快地製作強大的表單！
feature: Edge Delivery Services
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 100%

---

# 設定您的 Google 表單或 Microsoft Excel 檔案以開始接受資料


[建立並預覽表單](/help/edge/docs/forms/create-forms.md)後，您即可啟用對應的試算表以開始接收資料。您可以

- [手動啟用試算表以接受資料](#manually-enable-the-spreadsheet-to-accept-data)
- [使用 Admin API 讓試算表接受資料](#use-admin-apis-to-enable-a-spreadsheet-to-accept-data)

![文件型製作生態系統](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)


<!--

>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

## 手動啟用試算表以接受資料

若要啟用試算表以接受資料

1. 開啟包含您表單的試算表並附加一個新工作表，將其重新命名為 `incoming`。例如，[查詢](/help/edge/assets/enquiry.xlsx)表單 Microsoft Excel 工作簿。

   >[!WARNING]
   >
   > 如果 `incoming` 工作表不存在，AEM 不會向試算表傳送任何資料。

1. 在此工作表中，插入一個名為 &quot;intake_form&quot; 的表。選取與表單欄位名稱相符所需的欄數。然後，在工具列中前往「插入 > 表格」，並按一下「確定」。

1. 將表格的名稱更改為 “intake_form”。在 Microsoft Excel 中，若要變更表格的名稱，請選取該表格並按一下「表格設計」。

1. 接下來，新增表單欄位名稱作為表格標題。為了確保這些欄位完全相同，您可以從 &quot;shared-aem&quot; 工作表中將其複製並貼上。在 &quot;shared-aem&quot; 工作表中，選取並複製 &quot;Name&quot; 欄下所列的表單 ID (提交欄位除外)。

1. 在「傳入」工作表中，選取「選擇性貼上 > 將列調換為欄」，以便將欄位 ID 複製為該新工作表中的欄標題。只保留需要擷取資料的欄位，其他可以忽略。

   `shared-aem` 工作表 `Name` 欄的每個值 (不包含提交按鈕) 可以成為  `incoming` 工作表的標題。例如，請參考下方說明 &quot;enquiry&quot; 表單標題的圖片：

   ![聯絡我們表單的欄位](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 延伸模組來預覽表單更新。您的工作表已準備好接受傳入的表單提交。

   >[!NOTE]
   >
   >即使以前已預覽過該工作表，在第一次建立 `incoming` 工作表後也必須再次預覽。


將欄位名稱新增至 `incoming` 工作表後，您的表單就可以接受提交了。您可以預覽表單並使用它向工作表提交資料。

將工作表設定為接收資料後，您即可[預覽表單](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) <!--or [use POST requests](#use-admin-apis-to-send-data-to-your-sheet)-->，以開始將資料傳送到工作表。

>[!WARNING]
>
>  &quot;shared-aem&quot; 工作表絕不會包括任何您不願意開放存取的個人可識別資料或敏感資料。


## 使用 Admin API 讓試算表接受資料

您也可以向表單傳送 POST 要求，使其能夠接受資料並設定 `incoming` 工作表的標題。收到 POST 要求後，服務會分析要求內文並自動產生資料擷取所需的基本標題和工作表。

若要使用 Admin API 讓試算表接受資料：


1. 開啟您建立的活頁簿並將預設工作表的名稱變更為 `incoming`。

   >[!WARNING]
   >
   > 如果 `incoming` 工作表不存在，AEM 不會向此活頁簿傳送任何資料。

1. 在 Sidekick 中預覽工作表。

   >[!NOTE]
   >
   >即使以前已預覽過該工作表，在第一次建立 `incoming` 工作表後也必須再次預覽。

1. 傳送 POST 要求以在 `incoming` 工作表中產生適當的標題，並將 `shared-default` 工作表新增至試算表 (如果尚未存在)。

   若要了解如何制訂用來設定工作表的 POST 要求格式，請參閱「[Admin API 文件](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile)」。您可以查看下方提供的範例：

   **要求**

   ```JSON
   POST 'https://admin.aem.page/form/{owner}/{repo}/{branch}/contact-us.json' \
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

   您可以使用 curl 或 Postman 等工具來執行此 POST 要求，如下所示：

   ```JSON
   curl -s -i -X POST 'https://admin.aem.page/form/wkndform/wefinance/main/contact-us.json' \
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

   上面提及的 POST 要求提供了範例資料，包括表單欄位及其個別的範例值。Admin 服務會使用此資料來設定表單。

   您的表單現在可以接受資料了。您也可以觀察到試算表有以下變化：

## 一旦啟用接受資料，工作表就會自動變更。

將工作表設定為接收資料後，您會在試算表中觀察到以下變更：

名為「Slack」的工作表會新增至您的 Excel 活頁簿或 Google Sheet 中。在此工作表中，當系統擷取新資料至試算表中時，您可以為指定的 Slack 頻道設定自動通知。目前，AEM 僅支援向 AEM Engineering Slack 組織和 Adob&#x200B;&#x200B;e Enterprise 支援組織發送通知。

1. 若要設定 Slack 通知，請輸入 Slack 工作區的「teamId」和「頻道名稱」或「ID」。您也可以向 Slack 機器人 (使用 debug 指令) 要求「teamId」和「頻道 ID」。最好使用「頻道 ID」而不是「頻道名稱」，因為這樣可以在頻道重新命名後繼續存在。

   >[!NOTE]
   >
   > 舊的表單沒有「teamId」欄。「teamId」會包含在頻道欄中，並且以「#」或「/」分隔。

1. 輸入您想要的任何標題，然後在欄位下輸入您想要在 Slack 通知中看到的欄位名稱。每個標題應以逗號分隔 (例如姓名、電子郵件)。

   >[!WARNING]
   >
   >  「共用預設」工作表絕不會包含您不願意開放存取的任何個人識別資料或敏感資料。



接下來，您可以[自訂感謝訊息](/help/edge/docs/forms/thank-you-page-form.md)。

