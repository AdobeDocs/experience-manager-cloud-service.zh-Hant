---
title: 如何建立最適化表單的自訂提交動作？
description: 了解如何為適用性Forms建立自訂提交動作，以在將資料提交至rest端點、儲存至資料存放區及執行其他自訂功能之前，先延遲提交及處理資料。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 77131cc2-9cb1-4a00-bbc4-65b1a66e76f5
source-git-commit: 391a9482cc6ed97984693c21b41910fdd32ff25d
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 0%

---

# 建立適用性Forms的自訂提交動作 {#writing-custom-submit-action-for-adaptive-forms}

適用性表單提供多個立即可用的提交動作(OOTB)。 「提交動作」會指定要對透過適用性表單收集的資料執行的動作詳細資訊。 例如，在電子郵件上傳送資料。

您可以建立自訂的「提交動作」，以新增未包含在 [立即提交動作](configuring-submit-actions.md) 或未透過單一OOTB提交動作提供支援。 例如，將資料提交至工作流程、將資料儲存在資料儲存區、傳送電子郵件通知給提交表單的人員，以及透過單一「提交動作」傳送電子郵件給負責處理已提交表單以進行核准和拒絕的人員。

## XML資料格式 {#xml-data-format}

XML資料會使用 **`jcr:data`** 要求參數。 提交動作可存取參數以處理資料。 以下代碼描述XML資料的格式。 綁定到表單模型的欄位將顯示在 **`afBoundData`** 區段。 未綁定的欄位顯示在 `afUnoundData`區段。 <!--For more information about the format of the `data.xml` file, see [Introduction to prepopulating Adaptive Form fields](prepopulate-adaptive-form-fields.md).-->

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### 動作欄位 {#action-fields}

「提交動作」可新增隱藏的輸入欄位(使用HTML [輸入](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) 標籤)轉換為轉譯的表單HTML。 這些隱藏欄位可包含處理表單提交時所需的值。 提交表單時，這些欄位值會作為請求參數發回，「提交操作」可在提交處理期間使用這些參數。 輸入欄位稱為動作欄位。

例如，也擷取填寫表單所花時間的「提交動作」可以新增隱藏的輸入欄位 `startTime` 和 `endTime`.

指令碼可提供 `startTime` 和 `endTime` 表單轉譯時和表單提交前的欄位。 提交操作指令碼 `post.jsp` 之後，您就可以使用請求參數存取這些欄位，並計算填寫表單所需的總時間。

### 檔案附件 {#file-attachments}

「提交操作」還可以使用使用「檔案附件」元件上傳的檔案附件。 提交動作指令碼可使用sling存取這些檔案 [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). 此 [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) API的方法有助於識別要求參數是檔案還是表單欄位。 您可以反覆查看提交動作中的請求參數，以識別檔案附件參數。

下列范常式式碼可識別請求中的檔案附件。 接下來，會使用 [取得API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). 最後，它使用資料建立文檔對象並將其附加到清單中。

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

將檔案附加至適用性表單時，伺服器會在適用性表單提交後驗證檔案附件，並在下列情況下傳回錯誤訊息：

* 檔案附件包含以(.)開頭的檔案名 字元，包含\ / :* ? &quot; &lt; > | ;% $個字元，或包含為Windows作業系統保留的特殊檔案名，如 `nul`, `prn`, `con`, `lpt`，或 `com`.

* 檔案附件的大小為0位元組。

* 檔案附件的格式未定義於 [支援的檔案類型](https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text) 區段（在適用性表單中設定檔案附件元件時）。

### 前進路徑和重新導向URL {#forward-path-and-redirect-url}

執行所需操作後，提交servlet將請求轉發到轉發路徑。 動作會使用setForwardPath API來設定指南提交Servlet中的前進路徑。

如果動作未提供轉送路徑，則提交servlet會使用重新導向URL來重新導向瀏覽器。 作者會使用「適用性表單編輯」對話方塊中的「感謝頁面」設定來設定重新導向URL。 您也可以透過提交動作或指南提交servlet中的setRedirectUrl API來設定重新導向URL。 您也可以使用指南提交servlet中的setRedirectParameters API來設定傳送至重新導向URL的要求參數。

>[!NOTE]
>
>作者提供重新導向URL（使用感謝頁面設定）。 [OOTB提交操作](configuring-submit-actions.md) 使用「重新導向URL」，從正向路徑參考的資源重新導向瀏覽器。
>
>您可以撰寫自訂的「提交動作」，將請求轉送至資源或servlet。 Adobe建議執行正向路徑資源處理的指令碼在處理完成時，將要求重新導向至重新導向URL。

## 提交動作 {#submit-action}

提交動作是sling:Folder，包含下列項目：

* **addfields.jsp**:此指令碼提供在轉譯期間新增至HTML檔案的動作欄位。 使用此指令碼，在post.POST.jsp指令碼中添加提交期間所需的隱藏輸入參數。
* **dialog.xml**:此指令碼類似於CQ元件對話方塊。 提供作者自訂的設定資訊。 當您選擇「提交動作」時，這些欄位會顯示在「適用性表單編輯」對話方塊的「提交動作」標籤中。
* **post.POST.jsp**:Submit servlet會使用您提交的資料以及前幾節中的其他資料來呼叫此指令碼。 在此頁面中提及執行動作即表示執行post.POST.jsp指令碼。 若要向適用性Forms註冊「提交動作」以在適用性表單編輯對話方塊中顯示，請將這些屬性新增至Sling:Folder:

   * **guideComponentType** 類型字串和值 **fd/af/components/guidesubmittype**
   * **guideDataModel** 類型，指定適用「提交動作」的適用性表單類型。 <!--**xfa** is supported for XFA-based Adaptive Forms while -->**xd** 支援XSD型適用性Forms。 **基本** 不使用XDP或XSD的適用性Forms支援。 若要在多種類型的適用性Forms上顯示動作，請新增對應的字串。 以逗號分隔每個字串。 例如，若要讓動作在上顯示 <!--XFA- and -->以XSD為基礎的適用性Forms，請將值指定為 <!--**xfa** and--> **xd**.

   * **jcr:description** 類型。 此屬性的值顯示在「適用性表單編輯」對話框的「提交操作」頁簽的「提交操作」清單中。 OOTB動作會顯示在CRX存放庫的位置 **/libs/fd/af/components/guidesubmittype**.

   * **submitService** 類型。 如需詳細資訊，請參閱 [排程自訂動作的最適化表單提交](#schedule-adaptive-form-submission).

## 建立自訂提交動作 {#creating-a-custom-submit-action}

執行下列步驟以建立自訂的提交動作，將資料儲存在CRX存放庫中，然後傳送電子郵件給您。 適用性表單包含將資料儲存在CRX存放庫的OOTB提交動作存放區內容（已淘汰）。 此外，AEM也提供 [郵件](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/mailer/package-summary.html) 可用於傳送電子郵件的API。 使用Mail API之前，請透過系統主控台設定Day CQ Mail服務。 您可以重複使用「儲存內容（已廢止）」動作，將資料儲存在存放庫中。 「儲存內容（已廢止）」動作可在CRX存放庫的/libs/fd/af/components/guidesubmittype/store位置取得。

1. 在URL https://登入CRXDE Lite&lt;server>:&lt;port>/crx/de/index.jsp。 在/apps/custom_submit_action資料夾中，使用屬性sling:Folder和name store_and_mail建立節點。 建立custom_submit_action資料夾（如果尚未存在）。

   ![螢幕擷圖，說明使用屬性sling:Folder建立節點的方式](assets/step1.png)

1. **提供必填的設定欄位。**

   添加儲存操作所需的配置。 複製 **cq:dialog** 儲存操作節點，從/libs/fd/af/components/guidesubmittype/store指向/apps/custom_submit_action/store_and_email的操作資料夾。

   ![螢幕截圖顯示對話框節點複製到操作資料夾](assets/step2.png)

1. **提供設定欄位以提示作者進行電子郵件設定。**

   適用性表單也提供「電子郵件」動作，可傳送電子郵件給使用者。 根據您的需求自訂此動作。 導覽至/libs/fd/af/components/guidesubmittype/email/dialog。 將cq:dialog節點內的節點複製到提交動作(/apps/custom_submit_action/store_and_email/dialog)的cq:dialog節點。

   ![自訂電子郵件動作](assets/step3.png)

1. **讓動作可在「最適化表單編輯」對話方塊中使用。**

   在store_and_email節點中新增下列屬性：

   * **guideComponentType** 類型 **字串** 和值 **fd/af/components/guidesubmittype**

   * **guideDataModel** 類型 **字串** 和值 **<!--xfa, -->xsd，基本**

   * **jcr:description** 類型 **字串** 和值 **儲存和電子郵件動作**

   * **submitService** 類型 **字串** 和值 **儲存和電子郵件**. 如需詳細資訊，請參閱 [排程自訂動作的最適化表單提交](#schedule-adaptive-form-submission).

1. 開啟任何適用性表單。 按一下 **編輯** 按鈕 **開始** 開啟 **編輯** 對話方塊。 新動作會顯示在 **提交操作** 標籤。 選取 **儲存和電子郵件動作** 顯示在對話框節點中添加的配置。

   ![提交操作配置對話框](assets/store_and_email_submit_action_dialog.jpg)

1. **使用操作完成任務。**

   將post.POST.jsp指令碼新增至動作。 (/apps/custom_submit_action/store_and_mail/)。

   執行OOTB儲存動作(post.POST.jsp指令碼)。 使用 [FormsHelper.runAction](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction-java.lang.String-java.lang.String-org.apache.sling.api.resource.Resource-org.apache.sling.api.SlingHttpServletRequest-org.apache.sling.api.SlingHttpServletResponse-)(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse))CQ在您的程式碼中提供的API，用以執行「儲存」動作。 在JSP檔案中添加以下代碼：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   若要傳送電子郵件，程式碼會從設定讀取收件者的電子郵件地址。 若要擷取動作指令碼中的設定值，請使用下列程式碼讀取目前資源的屬性。 同樣地，您也可以讀取其他組態檔。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最後，使用CQ Mail API來傳送電子郵件。 使用 [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) 類以建立電子郵件對象，如下所示：

   >[!NOTE]
   >
   >確保JSP檔案的名稱為post.POST.jsp。

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   在適用性表單中選取動作。 動作會傳送電子郵件並儲存資料。

## 對自定義提交操作使用submitService屬性 {#submitservice-property}

當您設定自訂提交動作時，包括 `submitService` 屬性，表單會觸發 [FormSubmitActionService](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/service/FormSubmitActionService.html) 提交時。 此 `FormSubmitActionService` 使用 `getServiceName` 擷取 `submitService` 屬性。 根據 `submitService` 屬性，則服務會叫用適當的提交方法。 納入 `FormSubmitActionService` 上傳至的自訂套件組合 [!DNL AEM Forms] 伺服器。

新增 `submitService` 字串類型的屬性 `sling:Folder` 自訂提交動作啟用 [!DNL Adobe Sign] （適用於適用性表單）。 您可以選取 **[!UICONTROL 啟用Adobe Sign]** 選項 **[!UICONTROL 電子簽名]** 區段(僅限在 `submitService` 自訂提交動作的屬性。

<!--As a result of setting an appropriate value for the `submitService` property and enabling [!DNL Adobe Sign], you can schedule the submission of an Adaptive Form to ensure that all configured signers have taken an action on the form. [!DNL Adobe Sign] Configuration Service keeps polling [!DNL Adobe Sign] server at regular intervals to verify the status of signatures. If all the signers complete signing the form, the Submit Action service is started and the form is submitted.-->


![提交服務屬性](assets/submit-service-property.png)

<!-- You can't do comments within comments, so I changed comment tags to <start-comment> <end-comment> -->

<!--
## Workflow for a Submit Action {#workflow-for-a-submit-action}

The flowchart depicts the workflow for a Submit Action that is triggered when you click the **[!UICONTROL Submit]** button in an Adaptive Form. The files in the File Attachment component are uploaded to the server, and the form data is updated with the URLs of the uploaded files. Within the client, the data is stored in the JSON format. The client sends an Ajax request to an internal servlet that massages the data you specified and returns it in the XML format. The client collates this data with action fields. It submits the data to the final servlet (Guide Submit servlet) through a Form Submit Action. Then, the servlet forwards the control to the Submit Action. The Submit Action can forward the request to a different sling resource or redirect the browser to another URL.

![Flowchart depicting the workflow for Submit Action](assets/diagram1.png)

### XML data format {#xml-data-format}

The XML data is sent to the servlet using the **`jcr:data`** request parameter. Submit Actions can access the parameter to process the data. The following code describes the format of the XML data. The fields that are bound to the Form model appear in the **`afBoundData`** section. Unbound fields appear in the `afUnoundData`section. For more information about the format of the `data.xml` file, see [Introduction to prepopulating Adaptive Form fields](prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<start comment> xml corresponding to the Form Model /XML Schema <end comment>
<start comment> </afBoundData> <end comment>
</afData>
```

### Action fields {#action-fields}

A Submit Action can add hidden input fields (using the HTML [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) tag) to the rendered form HTML. These hidden fields can contain values that it needs while processing form submission. When submitting the form, these field values are posted back as request parameters that the Submit Action can use during submission handling. The input fields are called action fields.

For example, a Submit Action that also captures the time taken to fill a form can add the hidden input fields `startTime` and `endTime`.

A script can supply the values of the `startTime` and `endTime` fields when the form renders and before form submission, respectively. The Submit Action script `post.jsp` can then access these fields using request parameters and compute the total time required to fill the form.

### File attachments {#file-attachments}

Submit Actions can also use the file attachments you upload using the File Attachment component. Submit Action scripts can access these files using the sling [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). The [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) method of the API helps identify whether the request parameter is a file or a form field. You can iterate over the Request parameters in a Submit Action to identify File Attachment parameters.

The following sample code identifies the file attachments in the request. Next, it reads the data into the file using the [Get API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Finally, it creates a Document object using the data and appends it to a list.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### Forward path and Redirect URL {#forward-path-and-redirect-url}

After performing the required action, the Submit servlet forwards the request to the forward path. An action uses the setForwardPath API to set the forward path in the Guide Submit servlet.

If the action doesn't provide a forward path, the Submit servlet redirects the browser using the Redirect URL. The author configures the Redirect URL using the Thank You Page configuration in the Adaptive Form Edit dialog. You can also configure the Redirect URL through the Submit Action or the setRedirectUrl API in the Guide Submit servlet. You can also configure the Request parameters sent to the Redirect URL using the setRedirectParameters API in the Guide Submit servlet.

>[!NOTE]
>
>An author provides the Redirect URL (using the Thank You Page Configuration). [OOTB Submit Actions](configuring-submit-actions.md) use the Redirect URL to redirect the browser from the resource that the forward path references.
>
>You can write a custom Submit Action that forwards a request to a resource or servlet. Adobe recommends that the script that performs resource handling for the forward path redirect the request to the Redirect URL when the processing completes.

## Submit Action {#submit-action}

A Submit Action is a sling:Folder that includes the following:

* **addfields.jsp**: This script provides the action fields that are added to the HTML file during rendition. Use this script to add hidden input parameters required during submission in the post.POST.jsp script.
* **dialog.xml**: This script is similar to the CQ Component dialog. It provides configuration information that the author customizes. The fields are displayed in the Submit Actions Tab in the Adaptive Form Edit dialog when you select the Submit Action.
* **post.POST.jsp**: The Submit servlet calls this script with the data that you submit and the additional data in the previous sections. Any mention of running an action in this page implies running the post.POST.jsp script. To register the Submit Action with the Adaptive Forms to display in the Adaptive Form Edit dialog, add these properties to the sling:Folder:

    * **guideComponentType** of type String and value **fd/af/components/guidesubmittype**
    * **guideDataModel** of type String that specifies the type of Adaptive Form for which the Submit Action is applicable. **xfa** is supported for XFA-based Adaptive Forms while **xsd** is supported for XSD-based Adaptive Forms. **basic** is supported for Adaptive Forms that do not use XDP or XSD. To display the action on multiple types of Adaptive Forms, add the corresponding strings. Separate each string by a comma. For example, to make an action visible on XFA- and XSD-based Adaptive Forms, specify the values **xfa** and **xsd** respectively.

    * **jcr:description** of type String. The value of this property is displayed in the Submit Action list in the Submit Actions Tab of the Adaptive Form Edit dialog. The OOTB actions are present in the CRX repository at the location **/libs/fd/af/components/guidesubmittype**.

## Creating a custom Submit Action {#creating-a-custom-submit-action}

Perform the following steps to create a custom Submit Action that saves the data in the CRX repository and then sends you an email. The Adaptive Form contains the OOTB Submit Action Store Content (deprecated) that saves the data in the CRX repository. In addition, CQ provides a [Mail](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/mailer/package-summary.html) API that can be used to send emails. Before using the Mail API, configure the Day CQ Mail service through the system console. You can reuse the Store Content (deprecated) action to store the data in the repository. The Store Content (deprecated) action is available at the location /libs/fd/af/components/guidesubmittype/store in the CRX repository.

1. Log in to CRXDE Lite at the URL https://&lt;server&gt;:&lt;port&gt;/crx/de/index.jsp. Create a node with the property sling:Folder and name store_and_mail in the /apps/custom_submit_action folder. Create the custom_submit_action folder if it doesn't exist already.

   ![Screenshot depicting the creation of a node with the property sling:Folder](assets/step1.png)

1. **Provide the mandatory configuration fields.**

   Add the configuration the Store action requires. Copy the **cq:dialog** node of the Store action from /libs/fd/af/components/guidesubmittype/store to the action folder at /apps/custom_submit_action/store_and_email.

   ![Screenshot showing the copying of the dialog node to the action folder](assets/step2.png)

1. **Provide configuration fields to prompt the author for email configuration.**

   The Adaptive Form also provides an Email action that sends emails to users. Customize this action based on your requirements. Navigate to /libs/fd/af/components/guidesubmittype/email/dialog. Copy the nodes within the cq:dialog node to cq:dialog node of your Submit Action (/apps/custom_submit_action/store_and_email/dialog).

   ![Customizing the email action](assets/step3.png)

1. **Make the action available in the Adaptive Form Edit dialog.**

   Add the following properties in the store_and_email node:

    * **guideComponentType** of type **String** and value **fd/af/components/guidesubmittype**

    * **guideDataModel** of type **String** and value **xfa, xsd, basic**

    * **jcr:description** of type **String** and value **Store and Email Action**

1. Open any Adaptive Form. Click the **Edit** button next to **Start** to open the **Edit** dialog of the Adaptive Form container. The new action is displayed in the **Submit Actions** Tab. Selecting the **Store and Email Action** displays the configuration added in the dialog node.

   ![Submit Action configuration dialog](assets/store_and_email_submit_action_dialog.jpg)

1. **Use the action to complete a task.**

   Add the post.POST.jsp script to your action. (/apps/custom_submit_action/store_and_mail/).

   Run the OOTB Store action (post.POST.jsp script). Use the [FormsHelper.runAction](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction-java.lang.String-java.lang.String-org.apache.sling.api.resource.Resource-org.apache.sling.api.SlingHttpServletRequest-org.apache.sling.api.SlingHttpServletResponse-(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse)) API that CQ provides in your code to run the Store action. Add the following code in your JSP file:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   To send the email, the code reads the recipient's email address from the configuration. To fetch the configuration value in the action's script, read the properties of the current resource using the following code. Similarly you can read the other configuration files.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Finally, use the CQ Mail API to send the email. Use the [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) class to create the Email Object as depicted below:

   >[!NOTE]
   >
   >Ensure that the JSP file has the name post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Select the action in the Adaptive Form. The action sends an email and stores the data. 

-->
