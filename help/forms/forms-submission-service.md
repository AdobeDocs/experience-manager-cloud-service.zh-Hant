---
Title: How to use forms submission service for submitting forms?
Description: Learn how to use forms submission service for submitting forms.
Keywords: Use form submission service, Submit form using form submission service
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: 37b20a97942f381b46ce36a6a3f72ac019bba5b7
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 9%

---

# 使用Edge Delivery Services Forms的Forms提交服務

<span class="preview">您可以透過搶先體驗方案使用這項功能。若要請求存取權，請使用您的官方地址發送電子郵件至 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，郵件內容須包含您的 GitHub 組織名稱和存放庫名稱。例如，若存放庫 URL 為 https://github.com/adobe/abc,，則組織名稱為 adobe，存放庫名稱為 abc。</span>

Forms提交服務可讓您將表單提交的資料儲存在任何試算表中(例如OneDrive、SharePoint或Google Sheets)，讓您在自己的試算表平台中輕鬆存取和管理表單資料。

![Forms提交服務](/help/forms/assets/form-submission-service.png)

## 使用Forms提交服務的優勢

搭配試算表使用Forms提交服務的一些優點包括：

* **直接整合**：您可以設定表單，將資料直接提交至指定的試算表，而不需要手動資料傳輸。
* **資料結構**：設定提交時，您可以將表單欄位對應至對應的試算表欄，以儲存有序的資料。
* **存取控制**：您可以利用現有的許可權，根據選擇的試算表服務，控制誰可以存取及修改提交的表單資料。

## 必要條件

以下是使用Forms提交服務的先決條件：

* 請確定您的AEM專案具有最新最適化表單區塊。
* 確認您的Git存放庫已新增至允許清單，以使用Forms提交服務。 請使用您的GitHub組織名稱和存放庫名稱[mailto:aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，將這些組織名稱和存放庫名稱新增至允許清單，以便使用Forms提交服務。

## 設定Forms提交服務

建立以最適化AEM區塊設定的新Forms專案。 請參閱[快速入門 — 開發人員教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial)文章，瞭解如何建立新的AEM專案。 更新專案中的`fstab.yaml`檔案。 將現有的參考取代為您與`forms@adobe.com`共用的資料夾路徑。

您可以[手動設定Forms提交服務](#configuring-the-forms-submission-service-manually)或[使用API設定Forms提交服務](#configuring-the-forms-submission-service-using-api)。

### 手動設定Forms提交服務

![表單提交服務的工作流程](/help/forms/assets/forms-submission-service-workflow.png)

#### 1.使用表單定義建立表單

使用Google Sheets或Microsoft Excel製作表單。 若要瞭解如何使用Microsoft Excel或Google Sheets中的表單定義來建立表單，[請按一下這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)。

以下熒幕擷圖顯示用來建立表單的表單定義：

![表單定義](/help/forms/assets/form-submission-definition.png)

>[!IMPORTANT]
>
>**用來製作表單的工作表有命名限制。工作表名稱僅限使用 `helix-default` 和 `shared-aem`。**

#### 2.啟用試算表以接受資料。

建立並預覽表單後，請啟用對應的試算表以開始接收資料。 新增工作表做為`incoming`。 您可以[手動啟用試算表以接受資料](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/submit-forms#manually-enable-the-spreadsheet-to-accept-data)。

![傳入工作表](/help/forms/assets/form-submission-incoming-sheet.png)

>[!WARNING]
>
> 如果`incoming`工作表不存在，AEM將不會傳送任何資料到此活頁簿。

#### 3.共用試算表並產生連結。

若要將試算表共用至`forms@adobe.com`帳戶並產生連結，請執行下列步驟：

1. 在Excel或Google工作表中，按一下右上角的&#x200B;**共用**&#x200B;按鈕。
1. 新增`forms@adobe.com`帳戶並
按一下眼睛圖示，選取&#x200B;**編輯**&#x200B;存取權，然後按一下&#x200B;**傳送**。

   ![共用傳入工作表](/help/forms/assets/form-submission-share-incoming.png)

1. 若要複製試算表連結，請按一下右上角的&#x200B;**共用**&#x200B;按鈕，並選取&#x200B;**複製連結**。

   ![複製傳入工作表的連結](/help/forms/assets/form-submission-copy-link.png)

#### 4.在表單定義中連結試算表

若要使用Forms Sheets或Microsoft Excel設定Google提交服務，請執行以下步驟：

1. 開啟包含表單定義的試算表。
1. 在對應&#x200B;**提交**&#x200B;欄位的列中，將複製的試算表連結貼到&#x200B;**動作**&#x200B;欄。

   ![連結試算表](/help/forms/assets/form-submission-sheet-linking.png)

1. 使用[AEM Sidekick](https://www.aem.live/docs/sidekick)搭配更新的表單提交服務來預覽及發佈工作表。

>[!NOTE]
>
> 您可以參考[試算表](/help/forms/assets/spreadsheet.xlsx)以使用Forms提交服務。

### 使用API設定Forms提交服務

您也可以傳送&#x200B;**POST**&#x200B;要求至表單，以更新含有資料的`incoming`工作表。

>[!NOTE]
>
> * 如果`incoming`工作表不存在，AEM將不會傳送任何資料到此活頁簿。
> * 與Adobe Experience Manager共用`incoming`工作表`forms@adobe.com`並授與編輯存取權。
> * 在Sidekick中預覽並發佈`incoming`工作表。

若要瞭解如何格式化POST要求以設定工作表，請參閱[API檔案](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)。 您可以查看下方提供的範例：

您可以使用curl或Postman之類的工具來執行此POST要求，如下所示。

* **使用Postman**：

例如，取代後在Postman中傳送以下請求：
* `{id}`與您的表單ID
* `site or repository`搭配您的GitHub存放庫或網站名稱
* 使用您的GitHub使用者名稱`organization`

  ```json
  POST 'https://forms.adobe.com/adobe/forms/af/submit/{id}' \
  --header 'Content-Type: application/json' \
  --header 'x-adobe-routing: tier=live,bucket=main--[site/repository]--[organization]' \
  --data '{
      "data": {
          "startDate": "2025-01-10",
          "endDate": "2025-01-25",
          "destination": "Australia",
          "class": "First Class",
          "budget": "2000",
          "amount": "1000000",
          "name": "Mary",
          "age": "35",
          "subscribe": null,
          "email": "mary@gmail.com"
              }
          }'
  ```

按一下Postman中的&#x200B;**傳送**&#x200B;按鈕會傳回`201 Created`回應，而`incoming`工作表會以提交的資料更新。

![郵遞員熒幕](/help/forms/assets/postman-api.png)

* **使用Curl命令**：

例如，取代後，在終端機或命令提示字元中執行以下命令：
* `{id}`與您的表單ID
* `site or repository`搭配您的GitHub存放庫或網站名稱
* 使用您的GitHub使用者名稱`organization`


>[!BEGINTABS]
>[!TAB 適用於macOS 的]

    &grave;&grave;json
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; \
     — 標頭&grave;Content-Type： application/json&quot; \
     — 標頭&grave;x-adobe-routing： tier=live，bucket=main—[site/repository]—[organization]&quot; \
     — 資料&grave;&lbrace;
    `data`： &lbrace;
    &grave;startDate&quot;： &quot;2025-01-10&quot;，
    &grave;endDate&quot;： &quot;2025-01-25&quot;，
    &grave;destination&quot;澳洲」，
    「class」：「First Class」，
    「budget」：「2000」，
    「amount」：「1000000」，
    「name」：「Joe」，
    「age」：「35」，
    「subscribe」： null，
    「email」：「mary@gmail.com」
    &rbrace;
    &rbrace;&#39;
    
    」&#39;

>[!TAB 適用於Windows作業系統的] 

    &grave;&grave;json
    
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; ^
     — 標頭&quot;Content-Type： application/json&quot; ^
     — 標頭&quot;x-adobe-routing： tier=live，bucket=main—[site/repository]—[organization]&quot; ^
     — 資料&quot;{\&quot;data\&quot;： {\&quot;startDate\&quot;： \&quot;2025-01-10\&quot;， \&quot;endDate\&quot;： \&quot;2025-015\&quot;： \&quot;Destinstination\&quot; australia\&quot;， \&quot;class\&quot;： \&quot;First Class\&quot;， \&quot;budget\&quot;： \&quot;2000\&quot;， \&quot;amount\&quot;： \&quot;1000000\&quot;， \&quot;name\&quot;： \&quot;Joe\&quot;， \&quot;age\&quot;： \&quot;35\&quot;， \&quot;subscribe\&quot;： null， \&quot;email\&quot;： \&quot;mary@gmail.com\&quot;}}&quot;
    
    &quot;&#39;

>[!ENDTABS]

上述POST要求會使用以下回應來更新`incoming`工作表：

```json
    < HTTP/1.1 201 Created
    < Connection: keep-alive
    < Content-Length: 0
    < X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
    < X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
    < Accept-Ranges: bytes
    < Date: Fri, 10 Jan 2025 13:06:10 GMT
    < Via: 1.1 varnish
    < Access-Control-Allow-Origin: *
    < X-Served-By: cache-del21750-DEL
    < X-Cache: MISS
    < X-Cache-Hits: 0
    < X-Timer: S1736514370.704084,VS0,VE1234
```

以下畫面顯示使用API傳送資料所更新之`incoming`工作表的熒幕擷圖：

![已更新工作表](/help/forms/assets/updated-sheet.png)

## 另請參閱

{{see-more-forms-eds}}