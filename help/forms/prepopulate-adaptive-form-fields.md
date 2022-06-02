---
title: 預填充自適應表單域
seo-title: Prefill Adaptive Form fields
description: 使用現有資料預填充自適應表單的欄位。
seo-description: With Adaptive Forms, you users can prefill basic information in a form by logging in with their social profiles. This article describes how you can accomplish this.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
source-git-commit: 6b3c0abbbd7a5b3c9a3790937b933699389b0cd2
workflow-type: tm+mt
source-wordcount: '1948'
ht-degree: 1%

---


# 預填充自適應表單域{#prefill-adaptive-form-fields}

## 簡介 {#introduction}

可以使用現有資料預填自適應表單的欄位。 當用戶開啟表單時，這些欄位的值將預先填充。 要在自適應表單中預填充資料，請使用戶資料以符合自適應Forms預填充資料結構的格式可用作預填充XML/JSON。

## 預填充資料的結構 {#the-prefill-structure}

自適應表單可以具有綁定和未綁定欄位的混合。 綁定欄位是從「內容查找器」頁籤中拖動並包含非空的欄位 `bindRef` 欄位編輯對話框中的屬性值。 未綁定欄位直接從Sidekick的元件瀏覽器中拖動，並且為空 `bindRef` 值。

可以預填充自適應表單的綁定和未綁定欄位。 預填充資料包含afBoundData和afUnBoundData節，用於預填充自適應表單的綁定和未綁定欄位。 的 `afBoundData` 部分包含綁定欄位和面板的預填充資料。 此資料必須與關聯的表單模型架構相容：

- 對於自適應Forms，使用 [XFA表單模板](#xfa-based-af)，使用與XFA模板的資料架構相容的預填充XML。
- 適應Forms使用 [XML架構](#xml-schema-af)，使用與XML架構結構相容的預填充XML。
- 適應Forms使用 [JSON架構](#json-schema-based-adaptive-forms)，使用與JSON架構相容的預填充JSON。
- 對於使用FDM架構的Adaptive Forms，請使用與FDM架構相容的預填充JSON。
- 適應Forms [無表單模型](#adaptive-form-with-no-form-model)，沒有綁定資料。 每個欄位都是未綁定的欄位，並使用未綁定的XML預填充。

### 示例預填充XML結構 {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         .
         .
    </data>
  </afUnboundData>
</afData>
```

### 示例預填充JSON結構 {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

對於具有相同bindref或具有相同名稱的未綁定欄位，在XML標籤或JSON對象中指定的資料將填充到所有欄位中。 例如，表單中的兩個欄位映射到名稱 `textbox` 的雙曲餘切值。 在運行時，如果第一個文本框欄位包含「A」，則「A」將自動填充到第二個文本框中。 此連結稱為「自適應表單」欄位的即時連結。

### 使用XFA表單模板的自適應表單 {#xfa-based-af}

基於XFA的自適應Forms預填充XML和提交XML的結構如下：

- **預填充XML結構**:基於XFA的自適應表單的預填充XML必須與XFA表單模板的資料模式相容。 要預填充未綁定的欄位，請將預填充XML結構包裝到 `/afData/afBoundData` 標籤。

- **已提交的XML結構**:當未使用預填充XML時，提交的XML包含綁定欄位和未綁定欄位的資料 `afData` 包裝標籤。 如果使用預填充XML，則提交的XML與預填充XML的結構相同。 如果預填充XML以 `afData` 根標籤，輸出XML的格式也相同。 如果預填充XML沒有 `afData/afBoundData`包裝，而是直接從模式根標籤(如 `employeeData`，提交的XML也以 `employeeData` 標籤。

Prefill-Submit-Data-ContentPackage.zip

[獲取檔案](assets/prefill-submit-data-contentpackage.zip)
包含預填充資料和已提交資料的示例

### 基於XML模式的自適應Forms  {#xml-schema-af}

基於XML架構的自適應Forms預填充XML和提交XML的結構如下：

- **預填充XML結構**:預填充XML必須與關聯的XML架構相容。 要預填充未綁定的欄位，請將預填充XML結構包裝到/afData/afBoundData標籤中。
- **已提交的XML結構**:如果未使用預填充XML，則提交的XML包含中綁定和未綁定欄位的資料 `afData` 包裝標籤。 如果使用預填充XML，則提交的XML與預填充XML的結構相同。 如果預填充XML以 `afData` 根標籤，輸出XML的格式相同。 如果預填充XML沒有 `afData/afBoundData` 包裝，而是直接從模式根標籤(如 `employeeData`，提交的XML也以 `employeeData` 標籤。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">

    <xs:element name="sample" type="SampleType"/>

    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

對於模型為XML架構的欄位，資料將預填充到 `afBoundData` 標籤，如下面的示例XML中所示。 它可用於使用一個或多個未綁定文本欄位預填充自適應表單。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>建議不要在綁定面板（非空的面板）中使用未綁定欄位 `bindRef` 是通過從「邊」或「資料源」頁籤中拖動元件建立的)。 它可能導致這些未綁定欄位的資料丟失。 此外，建議在表單中欄位的名稱是唯一的，特別是對於未綁定欄位。

#### 沒有afData和afBoundData包裝的示例 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### 基於JSON架構的自適應Forms {#json-schema-based-adaptive-forms}

對於基於JSON架構的自適應Forms，下面介紹了預填充JSON和已提交JSON的結構。 有關詳細資訊，請參見 [使用JSON架構建立自適應Forms](adaptive-form-json-schema-form-model.md)。

- **預填充JSON結構**:預填充JSON必須與關聯的JSON架構相容。 或者，如果您也想預填充未綁定的欄位，可以將其包裝到/afData/afBoundData對象中。
- **已提交JSON結構**:如果未使用預填充JSON，則提交的JSON包含afData包裝標籤中綁定和未綁定欄位的資料。 如果使用預填充JSON，則提交的JSON與預填充JSON具有相同的結構。 如果預填充JSON以afData根對象開頭，則輸出JSON的格式相同。 如果預填充JSON沒有afData/afBoundData包裝，而是直接從架構根對象（如用戶）啟動，則提交的JSON也以用戶對象啟動。

```json
{
  "id": "https://some.site.somewhere/entry-schema#",
  "$schema": "https://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "address": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string"
        },
        "age": {
          "type": "integer"
        }
      }
    }
  }
}
```

對於使用JSON架構模型的欄位，資料將預填入afBoundData對象，如下面的示例JSON所示。 它可用於使用一個或多個未綁定文本欄位預填充自適應表單。 下面是資料的示例 `afData/afBoundData` 包裝：

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

下面是一個示例 `afData/afBoundData` 包裝：

```json
{
  "user": {
    "address": {
      "city": "Noida",
      "country": "India"
    }
  }
}
```

>[!NOTE]
>
> 在綁定面板中使用未綁定的欄位（通過從「邊」或「資料源」頁籤中拖動元件建立的具有非空bindRef的面板） **不** 建議，因為它可能導致未綁定欄位的資料丟失。 建議在窗體中具有唯一的欄位名，特別是對於未綁定的欄位。

### 無表單模型的自適應表單 {#adaptive-form-with-no-form-model}

對於沒有表單模型的自適應Forms，所有欄位的資料都位於 `<data>` 標籤 `<afUnboundData> tag`。

另請注意以下事項：

為各個欄位提交的用戶資料的XML標籤使用欄位的名稱生成。 因此，欄位名稱必須唯一。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## 配置預填充服務 {#configuring-prefill-service-using-configuration-manager}

使用 `alloweddataFileLocations` 屬性 **預設預填充服務配置** 設定資料檔案的位置或資料檔案位置的regex（規則運算式）。

以下JSON檔案顯示示例：

```JSON
  {
  "alloweddataFileLocations": "`file:///C:/Users/public/Document/Prefill/.*`"
  }
```

要設定配置值， [使用SDK生成OSGi配AEM置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) 和 [部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) 你的Cloud Service。

>[!NOTE]
>
> - 預設情況下，允許通過crx檔案為所有類型的自適應Forms（XSD、XDP、JSON、FDM和不基於表單模型）預填充。 僅JSON和XML檔案允許預填充。
> - crx協定負責預填充的資料安全，因此預設允許。 通過使用泛型regex的其他協定進行預填充可能會導致漏洞。 在配置中，指定用於保護資料的安全URL配置。


## 可重複面板的奇特案例 {#the-curious-case-of-repeatable-panels}

通常，綁定（表單架構）和未綁定欄位是在同一自適應表單中創作的，但在綁定是可重複的情況下，以下是少數例外：

- 對於使用XFA表單模板、XSD、JSON架構或FDM架構的Adaptive Forms，不支援未綁定的可重複面板。
- 請勿在綁定的可重複面板中使用未綁定欄位。

>[!NOTE]
>
> 作為經驗法則，如果綁定和未綁定欄位在未綁定欄位中被最終用戶填充的資料中交叉，則不要混合綁定和未綁定欄位。 如果可能，應修改架構或XFA表單模板並為未綁定欄位添加一個條目，以便它也會被綁定，並且其資料與已提交資料中的其他欄位一樣可用。

## 支援的預填充用戶資料的協定 {#supported-protocols-for-prefilling-user-data}

當配置有有效規則運算式時，可通過以下協定用預填充資料格式的用戶資料預填充自適應Forms:

### crx://協定 {#the-crx-protocol}

```javascript
http
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

指定的節點必須具有名為 `jcr:data` 保存資料。

### file://協定  {#the-file-protocol-nbsp}

```javascript
https://`servername`/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

引用的檔案必須位於同一伺服器上。

### https://協定 {#the-http-protocol}

```javascript
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://servername/somesamplexmlfile.xml
```

### service://協定 {#the-service-protocol}

```javascript
https://`servername`/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

- SERVICE_NAME指OSGI預填充服務的名稱。 參考 [建立並運行預填服務](prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)。
- IDENTIFIER指OSGI預填充服務獲取預填充資料所需的任何元資料。 登錄用戶的標識符是可以使用的元資料的示例。

>[!NOTE]
>
> 不支援傳遞身份驗證參數。

### 在slingRequest中設定資料屬性 {#setting-data-attribute-in-slingrequest}

也可以設定 `data` 屬性 `slingRequest`的子菜單。 `data` attribute是包含XML或JSON的字串，如下面的示例代碼所示(Example is for XML):

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

您可以編寫包含所有資料的簡單XML或JSON字串，並在slingRequest中設定它。 在渲染器JSP中，可以輕鬆完成對任何元件的這一操作，這些元件要包括在可以設定slingRequest資料屬性的頁中。

例如，您希望頁面具有特定類型的標題的特定設計。 為了達到這個目的，你可以自己寫 `header.jsp`，您可以在頁面元件中包括該元件並設定 `data` 屬性。

另一個好的示例是您希望通過Facebook、Twitter或LinkedIn等社交帳戶預填登錄資料的使用案例。 在這種情況下，可以在 `header.jsp`，它從用戶帳戶中提取資料並設定資料參數。

預填充頁元件.zip

[獲取檔案](assets/prefill-page-component.zip)
頁面元件中的prefill.jsp示例

## [!DNL AEM Forms] 自定義預填充服務 {#aem-forms-custom-prefill-service}

您可以對方案使用自定義預填充服務，在這些方案中，您經常從預定義的源中讀取資料。 預填充服務從定義的資料源讀取資料，並用預填充資料檔案的內容預填充自適應表單的欄位。 它還幫助您將預填資料與自適應表單永久關聯。

### 建立並運行預填服務 {#create-and-run-a-prefill-service}

預填充服務是OSGi服務，並通過OSGi捆綁包打包。 您可以建立OSGi捆綁包、上載並將其安裝到 [!DNL AEM Forms] 捆綁。 在開始建立捆綁包之前：

- [下載 [!DNL AEM Forms] 客戶端SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)
- 下載模板包

- 將資料（預填充資料）檔案放在crx-repository中。 可以將檔案放在crx-repository的\contents資料夾中的任何位置。

[取得檔案](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 建立預填服務 {#create-a-prefill-service}

模板包（示例預填充服務包）包含示例實現 [!DNL AEM Forms] 預填充服務。 在代碼編輯器中開啟模板包。 例如，在Eclipse中開啟模板項目進行編輯。 在代碼編輯器中開啟模板包後，請執行以下步驟建立服務。

1. 開啟src\main\java\com\adobe\test\Prefill.java檔案進行編輯。
1. 在代碼中，設定以下值：

   - `nodePath:` 指向crx-repository位置的節點路徑變數包含資料（預填充）檔案的路徑。 例如，/content/prefilldata.xml
   - `label:` 標籤參數指定服務的顯示名稱。 例如，預設預填充服務

1. 保存並關閉 `Prefill.java` 的子菜單。
1. 添加 `AEM Forms Client SDK` 包到模板項目的生成路徑。
1. 編譯項目並為捆綁包建立.jar。

#### 啟動和使用預填服務 {#start-and-use-the-prefill-service}

要啟動預填充服務，請將JAR檔案上載到 [!DNL AEM Forms] Web控制台，並激活服務。 現在，服務開始出現在自適應Forms編輯器中。 要將預填服務與自適應表單關聯，請執行以下操作：

1. 在Forms編輯器中開啟「自適應表單」，然後開啟「表單容器」的「屬性」面板。
1. 在「屬性」控制台中，導航至 [!DNL AEM Forms] 容器>基本>預填充服務。
1. 選擇預設預填充服務，然後按一下 **[!UICONTROL 保存]**。 服務與表單關聯。

<!-- ## Prepopulate data at client {#prefill-at-client}

When you prefill an Adaptive Form, the [!DNL AEM Forms] server merges data with an Adaptive Form and delivers the filled form to you. By default, the data merge action takes place at the server.

You can configure the [!DNL AEM Forms] server to perform the data merge action at the client instead of the server. It significantly reduces the time required to prefill and render Adaptive Forms. By default, the feature is disabled. You can enable it from the Configuration Manager or command line.

* To enable or disable from configuration manager:
  1. Open AEM Configuration Manager.
  1. Locate and open the Adaptive Form and Interactive Communication Web Channel Configuration
  1. Enable the Configuration.af.clientside.datamerge.enabled.name option
* To enable or disable from the command line:
  * To enable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  * To disable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   To take full advantage of the prepopulate data at client option, update your prefill service to return [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) and [CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) -->
