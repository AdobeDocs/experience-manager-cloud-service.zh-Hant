---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: AEM Forms REST端點、提交至REST端點、將資料發佈至REST URL、設定REST端點動作
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
title: 如何設定最適化表單的提交動作？
role: User, Developer
exl-id: 58c63ba6-aec5-4961-a70a-265990ab9cc8
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 57%

---

# 為REST端點提交動作設定最適化表單

<span class="preview">使用設定指定REST端點的功能屬於早期採用者程式，僅適用於核心元件和Edge Delivery Services Forms。 您可以從您的正式電子郵件ID寫信到`aem-forms-ea@adobe.com`，以加入早期採用者計畫並請求存取該功能。</span>

使用&#x200B;**[!UICONTROL 提交至REST端點]**&#x200B;動作，將提交的資料發佈至REST URL。 該 URL 可以是內部伺服器 (呈現表單的伺服器) 或外部伺服器。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/aem-forms-submit-action.md)文章中進一步瞭解這些選項。

## 優點

為Adaptive Forms設定&#x200B;**[!UICONTROL 提交至REST端點]**&#x200B;提交動作的部分優點包括：

* 透過RESTful API，可緊密整合表單資料與外部系統和服務。
* 它提供處理最適化Forms資料提交作業的彈性，支援動態和複雜的資料結構。
* 它支援將表單欄位動態對應到REST端點URL中的引數，允許適應性和可自訂的資料提交。


## 設定提交至REST端點提交動作 {#steps-to-configure-submit-to-restendpoint-submit-action}

>[!BEGINTABS]

>[!TAB 基礎元件]

若要根據以基礎元件為基礎之最適化表單的Swagger Open API規格設定提交動作，請執行下列動作：

1. 開啟最適化表單以進行編輯，並導覽至最適化表單容器屬性的&#x200B;**[!UICONTROL 提交]**&#x200B;區段。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 提交至Rest端點]**。

   提交至Rest端點的![動作設定](/help/forms/assets/submit-action-restendpoint.png)

   若要將資料發佈到內部伺服器，請提供資源的路徑。資料會發佈到資源的路徑。例如 `/content/restEndPoint`。對於此類發佈請求，會使用提交請求的驗證資訊。
此選項可讓您直接輸入目標REST端點。
若要將資料發佈到外部伺服器，請提供 URL。URL 的格式是：`https://host:port/path_to_rest_end_point`。請確保設定以匿名方式處理 POST 要求的路徑。
   ![做為「感謝頁面」參數傳遞之欄位值的對應](assets/post-enabled-actionconfig.png)

   在上面的範例中，在 `textbox` 輸入的資訊是使用 `param1` 參數來擷取。使用 `param1` 發佈所擷取之資料的語法是：

   `String data=request.getParameter("param1");`

   同樣地，用於發佈 XML 資料和附件的參數是 `dataXml` 和 `attachments`。

   例如，您會在指令碼中使用這兩個參數將資料剖析到 REST 端點。您會使用以下語法來儲存和剖析資料：

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   在此範例中，`data`儲存XML資料，`att`儲存附件資料。
「**[!UICONTROL 提交到 REST 端點]**」提交動作會將表單中填寫的資料做為 HTTP GET 要求的一部分，提交到已設定的確認頁面。您可以新增要請求的欄位名稱。 要求的格式為：
   `{fieldName}={request parameter name}`

   如下圖所示，`param1` 和 `param2` 是做為參數傳遞，其值是從 **textbox** 和 **numericbox** 欄位複製做為下一個動作。

   ![設定 REST 端點提交動作](assets/action-config.png)

   您也可以「**[!UICONTROL 啟用 POST 要求]**」並提供用於發佈要求的 URL。若要將資料提交到託管表單的 AEM 伺服器，請使用對應至 AEM 伺服器根路徑的相對路徑。例如 `/content/forms/af/SampleForm.html`。若要將資料提交到任何其他伺服器，請使用絕對路徑。

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!TAB 核心元件]

若要根據以核心元件為基礎的最適化表單的Swagger Open API規格設定提交動作，請執行下列動作：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 提交至Rest端點]**。

   ![正在設定Rest端點](assets/rest-service-endpoint-config.png)

   若要將資料發佈到內部伺服器，請提供資源的路徑。資料會發佈到資源的路徑。例如 `/content/restEndPoint`。對於此類發佈要求，會使用提交要求的驗證資訊。

   您有兩個選項可指定REST端點：

   +++URL

   此選項可讓您直接輸入目標REST端點。
若要將資料發佈到外部伺服器，請提供 URL。URL 的格式是：`https://host:port/path_to_rest_end_point`。請確保設定以匿名方式處理 POST 要求的路徑。

   ![做為「感謝頁面」參數傳遞之欄位值的對應](assets/post-enabled-actionconfig.png)

   在上面的範例中，在 `textbox` 輸入的資訊是使用 `param1` 參數來擷取。使用 `param1` 發佈所擷取之資料的語法是：

   `String data=request.getParameter("param1");`

   同樣地，用於發佈 XML 資料和附件的參數是 `dataXml` 和 `attachments`。

   例如，您會在指令碼中使用這兩個參數將資料剖析到 REST 端點。您會使用以下語法來儲存和剖析資料：

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   在這個範例中，`data` 會儲存 XML 資料，而 `att` 會儲存附件資料。

   「**[!UICONTROL 提交到 REST 端點]**」提交動作會將表單中填寫的資料做為 HTTP GET 要求的一部分，提交到已設定的確認頁面。您可以新增要請求的欄位名稱。 要求的格式為：

   `{fieldName}={request parameter name}`

   如下圖所示，`param1` 和 `param2` 是做為參數傳遞，其值是從 **textbox** 和 **numericbox** 欄位複製做為下一個動作。

   ![設定 REST 端點提交動作](assets/action-config.png)

   您也可以「**[!UICONTROL 啟用 POST 要求]**」並提供用於發佈要求的 URL。若要將資料提交到託管表單的 AEM 伺服器，請使用對應至 AEM 伺服器根路徑的相對路徑。例如 `/content/forms/af/SampleForm.html`。若要將資料提交到任何其他伺服器，請使用絕對路徑。

   +++

   +++設定

   此選項可讓您新增透過AEM的設定瀏覽器管理的預先定義HTTP設定。 您可以選取為服務Rest端點驗證型別和內容型別建立的組態。 若要進一步瞭解驗證型別和內容型別，請造訪[設定資料來源](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint)

   +++

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!TAB 通用編輯器]

若要根據在Universal Editor中編寫的最適化表單的Swagger Open API規格設定提交動作，請執行下列動作：

1. 開啟最適化表單進行編輯。
1. 按一下編輯器上的&#x200B;**編輯表單屬性**&#x200B;擴充功能。
**表單屬性**&#x200B;對話方塊就會顯示。
   >[!NOTE]
   >
   > * 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
   > * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。
1. 按一下&#x200B;**提交**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 提交至Rest端點]**&#x200B;提交動作。

   若要將資料發佈到內部伺服器，請提供資源的路徑。資料會發佈到資源的路徑。例如 `/content/restEndPoint`。對於此類發佈要求，會使用提交要求的驗證資訊。

   您有兩個選項可指定REST端點：

   +++URL

   此選項可讓您直接輸入目標REST端點。
若要將資料發佈到外部伺服器，請提供 URL。URL 的格式是：`https://host:port/path_to_rest_end_point`。請確保設定以匿名方式處理 POST 要求的路徑。

   ![做為「感謝頁面」參數傳遞之欄位值的對應](assets/post-enabled-actionconfig.png)

   在上面的範例中，在 `textbox` 輸入的資訊是使用 `param1` 參數來擷取。使用 `param1` 發佈所擷取之資料的語法是：

   `String data=request.getParameter("param1");`

   同樣地，用於發佈 XML 資料和附件的參數是 `dataXml` 和 `attachments`。

   例如，您會在指令碼中使用這兩個參數將資料剖析到 REST 端點。您會使用以下語法來儲存和剖析資料：

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   在這個範例中，`data` 會儲存 XML 資料，而 `att` 會儲存附件資料。

   「**[!UICONTROL 提交到 REST 端點]**」提交動作會將表單中填寫的資料做為 HTTP GET 要求的一部分，提交到已設定的確認頁面。您可以新增要請求的欄位名稱。 要求的格式為：

   `{fieldName}={request parameter name}`

   如下圖所示，`param1` 和 `param2` 是做為參數傳遞，其值是從 **textbox** 和 **numericbox** 欄位複製做為下一個動作。

   ![設定 REST 端點提交動作](/help/forms/assets/submit-to-rest-endpoint-ue.png)

   您也可以「**[!UICONTROL 啟用 POST 要求]**」並提供用於發佈要求的 URL。若要將資料提交到託管表單的 AEM 伺服器，請使用對應至 AEM 伺服器根路徑的相對路徑。例如 `/content/forms/af/SampleForm.html`。若要將資料提交到任何其他伺服器，請使用絕對路徑。

   +++

   +++設定

   此選項可讓您新增透過AEM的設定瀏覽器管理的預先定義HTTP設定。 您可以選取為服務Rest端點驗證型別和內容型別建立的組態。 若要進一步瞭解驗證型別和內容型別，請造訪[設定資料來源](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint)

   +++

1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。

>[!ENDTABS]

<!-- ### Configure submit action based on Service Rest Endpoint {#config-service-endpoint-auth}



1. Open the Content browser, and select the **[!UICONTROL Guide Container]** component of your Adaptive Form.
2. Click the Guide Container properties ![Guide properties](/help/forms/assets/configure-icon.svg) icon. The Adaptive Form Container dialog box opens. 
3. Click the  **[!UICONTROL Submission]** tab. 
4. From the **[!UICONTROL Submit Action]** drop-down list, select **[!UICONTROL Submit to Rest endpoint]**.
5. Enable the POST request.
6. Specify the REST endpoint URL.
7. Select the Configuration you have created for your Service Rest Endpoint Authentication Type and the Content Types. To know more about Authentication Type and the Content Types, visit [configure data sources](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint).
    ![Configuring Rest Endpoint](assets/rest-service-endpoint-config.png)
8. Click Done. -->



## 最佳實務

* 將資料張貼至外部伺服器時，請確定URL是安全的，並設定以匿名方式處理POST要求的路徑，以保護敏感資訊。
* 若要將欄位做為 REST URL 的參數傳遞，所有欄位都必須具有不同的元素名稱，即使這些欄位位於不同面板上也是如此。

## 相關文章

{{af-submit-action}}
