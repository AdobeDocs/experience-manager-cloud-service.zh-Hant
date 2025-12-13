---
title: 如何預填自適應表單欄位？
description: 使用現有資料預先填寫最適化表單的欄位，使用者可以使用其社交設定檔登入，預先填寫表單中的基本資訊。
topic-tags: develop
feature: Adaptive Forms, Foundation Components
exl-id: e2a87233-a0d5-48f0-b883-915fe56f105f
role: User, Developer
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2044'
ht-degree: 2%

---

# 預填最適化表單欄位{#prefill-adaptive-form-fields}

>[!NOTE]
>
> Adobe建議針對[建立新的Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)或[將Adaptive Forms新增至AEM Sites頁面](/help/forms/creating-adaptive-form-core-components.md)，使用現代且可擴充的資料擷取[核心元件](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文說明使用基礎元件製作最適化Forms的舊方法。

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html) |
| AEM as a Cloud Service  | 本文章 |

## 簡介 {#introduction}

您可以使用現有資料預先填寫最適化表單的欄位。 當使用者開啟表單時，這些欄位的值將被預填。 若要在調適型表單中預先填入資料，請遵循預先填入調適型Forms資料結構的格式，將使用者資料填入為預先填入XML/JSON。

## 適用性和使用案例

### 保險

## AEM Forms可以預先填入保險應用程式資料嗎？

可以。AEM Forms支援使用後端資料來源預先填寫表單欄位，讓保險公司可重複使用現有的客戶或保單資料，並減少手動輸入次數。

## 預填資料的結構 {#the-prefill-structure}

調適型表單可以混合有已繫結和未繫結的欄位。 繫結欄位是從「內容尋找器」標籤拖曳的欄位，在欄位編輯對話方塊中包含非空白的`bindRef`屬性值。 未繫結欄位是從Sidekick的元件瀏覽器直接拖曳，並具有空的`bindRef`值。

您可以預先填寫最適化表單的繫結和未繫結欄位。 預填資料包含afBoundData和afUnBoundData區段，以預填調適型表單的繫結和未繫結欄位。 `afBoundData`區段包含繫結欄位和面板的預填資料。 此資料必須符合關聯的表單模型結構描述：

- 針對使用[XFA表單範本](#xfa-based-af)的最適化Forms，請使用與XFA範本的資料結構描述相容的預填XML。
- 針對使用[XML結構描述](#xml-schema-af)的最適化Forms，請使用符合XML結構描述結構的預填XML。
- 針對使用[JSON結構描述](#json-schema-based-adaptive-forms)的最適化Forms，請使用符合JSON結構描述的預先填入JSON。
- 針對使用FDM架構的最適化Forms，請使用符合FDM架構的預填JSON。
- 對於具有[無表單模型](#adaptive-form-with-no-form-model)的最適化Forms，沒有繫結資料。 每個欄位都是未繫結的欄位，並使用未繫結的XML預先填入。

### 預填XML結構範例 {#sample-prefill-xml-structure}

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

### 預填JSON結構範例 {#sample-prefill-json-structure}

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

對於具有相同bindref的繫結欄位或具有相同名稱的未繫結欄位，所有欄位都會填入XML標籤或JSON物件中指定的資料。 例如，表單中的兩個欄位對應到預填資料中的名稱`textbox`。 在執行階段，如果第一個文字方塊欄位包含「A」，則第二個文字方塊會自動填入「A」。 此連結稱為自適應表單欄位的即時連結。

### 使用XFA表單範本的最適化表單 {#xfa-based-af}

針對XFA型Adaptive Forms預先填入XML和已提交的XML的結構如下：

- **預填XML結構**：XFA型最適化表單的預填XML必須符合XFA表單範本的資料結構描述。 若要預填未繫結欄位，請將預填XML結構包裝成`/afData/afBoundData`標籤。

- **已提交的XML結構**：當未使用預填XML時，已提交的XML包含`afData`包裝函式標籤中繫結和未繫結欄位的資料。 如果使用預填XML，則提交的XML具有與預填XML相同的結構。 如果預填XML以`afData`根標籤開頭，則輸出XML也具有相同的格式。 如果預填XML沒有`afData/afBoundData`包裝函式，而是直接從結構描述根標籤（如`employeeData`）開始，則提交的XML也會從`employeeData`標籤開始。

Prefill-Submit-Data-ContentPackage.zip

[取得檔案](assets/prefill-submit-data-contentpackage.zip)
包含預填資料和已提交資料的範例

### 以XML結構描述為基礎的最適化Forms  {#xml-schema-af}

根據XML結構描述的最適化Forms的預填XML和已提交的XML結構如下：

- **預填XML結構**：預填XML必須符合關聯的XML結構描述。 若要預填未繫結欄位，請將預填XML結構包裝在/afData/afBoundData標籤中。
- **已送出的XML結構**：如果未使用預填XML，則送出的XML會包含`afData`包裝函式標籤中繫結和未繫結欄位的資料。 如果使用預填XML，則提交的XML具有與預填XML相同的結構。 如果預填XML以`afData`根標籤開頭，則輸出XML的格式會相同。 如果預填XML沒有`afData/afBoundData`包裝函式，而是直接從結構描述根標籤（如`employeeData`）開始，則提交的XML也會以`employeeData`標籤開始。

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

對於模型為XML結構描述的欄位，資料會預先填入`afBoundData`標籤，如下面的範例XML所示。 它可用來預先填寫包含一或多個未繫結文字欄位的最適化表單。

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
>建議不要在繫結面板(具有非空白`bindRef`且已透過從Sidekick或「資料來源」索引標籤拖曳元件而建立的面板)中使用未繫結欄位。 這可能會導致這些未繫結欄位的資料遺失。 此外，建議整個表單中的欄位名稱必須是唯一的，尤其是未繫結的欄位。

#### 不含afData和afBoundData包裝函式的範例 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### JSON結構描述型最適化Forms {#json-schema-based-adaptive-forms}

針對根據JSON結構描述的最適化Forms，以下說明預填JSON和已提交JSON的結構。 如需詳細資訊，請參閱[使用JSON結構描述建立最適化Forms](adaptive-form-json-schema-form-model.md)。

- **預填JSON結構**：預填JSON必須符合關聯的JSON結構描述。 如果您也想要預先填入未繫結欄位，可以選擇將其包裝到/afData/afBoundData物件中。
- **已提交的JSON結構**：如果未使用預填JSON，則已提交的JSON會包含afData包裝函式標籤中繫結和未繫結欄位的資料。 如果使用預填JSON，則提交的JSON將與預填JSON具有相同的結構。 如果預填JSON以afData根物件開頭，則輸出JSON會具有相同的格式。 如果預填JSON沒有afData/afBoundData包裝函式，而是直接從結構描述根物件（例如使用者）開始，則提交的JSON也會從使用者物件開始。

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

對於使用JSON結構描述模型的欄位，資料會預先填入afBoundData物件，如下面的範例JSON所示。 它可用來預先填寫包含一或多個未繫結文字欄位的最適化表單。 以下是具有`afData/afBoundData`包裝函式的資料範例：

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

以下是沒有`afData/afBoundData`包裝函式的範例：

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
> 不建議在繫結面板(具有非空白bindRef的面板，這些面板是從Sidekick或「資料來源」索引標籤拖曳元件而建立的)中使用未繫結欄位，因為這可能會造成未繫結欄位的資料遺失。**** 建議在表單中設定唯一的欄位名稱，尤其是未繫結欄位。
>

### 無表單模型的最適化表單 {#adaptive-form-with-no-form-model}

針對沒有表單模型的最適化Forms，所有欄位的資料都在`<data>`的`<afUnboundData> tag`標籤下。

此外，請注意下列事項：

針對針對各種欄位提交的使用者資料所產生的XML標籤，是使用欄位名稱產生的。 因此，欄位名稱必須是唯一的。

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

## 設定預填服務 {#configuring-prefill-service-using-configuration-manager}

使用`alloweddataFileLocations`預設預填服務組態&#x200B;**的**&#x200B;屬性來設定資料檔的位置，或資料檔位置的regex （規則運算式）。

下列JSON檔案顯示範例：

```JSON
  {
  "alloweddataFileLocations": "`file:///C:/Users/public/Document/Prefill/.*`"
  }
```

若要設定組態的值，請[使用AEM SDK產生OSGi組態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hant#generating-osgi-configurations-using-the-aem-sdk-quickstart)並[將組態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant#deployment-process)部署至您的Cloud Service執行個體。

>[!NOTE]
>
> - 預設情況下，所有型別的調適型Forms （XSD、XDP、JSON、FDM以及無表單模型型）都允許透過crx檔案進行預填。 只有JSON和XML檔案才允許預填。
> - crx通訊協定會負責預先填入的資料安全性，因此預設允許。 透過其他通訊協定使用通用regex預先填寫可能會造成漏洞。 在設定中，指定用於保護資料的安全URL設定。

## 可重複面板的奇怪情況 {#the-curious-case-of-repeatable-panels}

通常，繫結（表單結構描述）和未繫結欄位會以相同的最適化表單編寫，但如果繫結是可重複的，則有下列幾個例外：

- 使用XFA表單範本、XSD、JSON結構描述或FDM結構描述的適用性Forms不支援未繫結的可重複面板。
- 請勿在已繫結的可重複面板中使用未繫結欄位。

>[!NOTE]
>
> 根據經驗，如果繫結和未繫結欄位在使用者在未繫結欄位中填充的資料中相交，請勿將其混合。 如果可能的話，您應該修改結構描述或XFA表單範本，並為未繫結欄位新增專案，這樣它也會變成繫結，而且其資料可以像提交資料中的其他欄位一樣使用。

## 預填使用者資料的支援通訊協定 {#supported-protocols-for-prefilling-user-data}

使用有效的規則運算式設定時，可透過下列通訊協定，以預填資料格式預填調適型Forms的使用者資料：

### crx://通訊協定 {#the-crx-protocol}

```javascript
http
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

指定的節點必須具有名為`jcr:data`的屬性並儲存資料。

### file://通訊協定  {#the-file-protocol-nbsp}

```javascript
https://`servername`/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

參照的檔案必須在相同的伺服器上。

### https://通訊協定 {#the-http-protocol}

```javascript
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://servername/somesamplexmlfile.xml
```

### service://通訊協定 {#the-service-protocol}

```javascript
https://`servername`/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

- SERVICE_NAME是指OSGI預填服務的名稱。 請參閱[建立並執行預填服務](prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)。
- 識別碼會參照OSGI預填服務擷取預填資料所需的任何中繼資料。 登入使用者的識別碼是可使用的中繼資料範例。

>[!NOTE]
>
> 不支援傳遞驗證引數。

### 在slingRequest中設定資料屬性 {#setting-data-attribute-in-slingrequest}

您也可以在`data`中設定`slingRequest`屬性，其中`data`屬性是包含XML或JSON的字串，如下列範常式式碼所示（範例為XML）：

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

您可以撰寫包含所有資料的簡單XML或JSON字串，並在slingRequest中進行設定。 您可以在轉譯器JSP中針對任何元件輕鬆完成這項操作，您想要將元件加入可設定slingRequest資料屬性的頁面中。

例如，您想要為具有特定標題型別的頁面使用特定設計的位置。 若要達成此目的，您可以撰寫自己的`header.jsp`，將其包含在頁面元件中並設定`data`屬性。

另一個很好的範例是使用案例，您想要在透過Facebook、Twitter或LinkedIn等社交帳戶登入時預先填入資料。 在此情況下，您可以在`header.jsp`中加入簡單的JSP，它會從使用者帳戶擷取資料並設定資料引數。

預填頁面component.zip

[取得檔案](assets/prefill-page-component.zip)
頁面元件中的prefill.jsp範例

## [!DNL AEM Forms]自訂預填服務 {#aem-forms-custom-prefill-service}

您可以針對持續從預先定義的來源讀取資料的情況，使用自訂預填服務。 預填服務會從定義的資料來源讀取資料，並使用預填資料檔案的內容預填調適型表單的欄位。 它還有助於您將預填的資料與最適化表單永久建立關聯。

### 建立並執行預填服務 {#create-and-run-a-prefill-service}

預填服務是一項OSGi服務，會透過OSGi套件組合封裝。 您建立OSGi套件組合，將其上傳並安裝至[!DNL AEM Forms]套件組合。 開始建立套件組合之前：

- [下載 [!DNL AEM Forms] 使用者端SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)
- 下載範本套件

- 將資料（預填資料）檔案放入crx存放庫中。 您可以將檔案放置在crx-repository的\contents資料夾中的任何位置。

[取得檔案](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 建立預填服務 {#create-a-prefill-service}

樣版封裝（範例預填服務封裝）包含[!DNL AEM Forms]預填服務的範例實作。 在程式碼編輯器中開啟樣板套件。 例如，在Eclipse中開啟範本專案進行編輯。 在程式碼編輯器中開啟樣板套件後，請執行以下步驟來建立服務。

1. 開啟src\main\java\com\adobe\test\Prefill.java檔案進行編輯。
1. 在程式碼中，設定值：

   - `nodePath:`指向crx存放庫位置的節點路徑變數包含資料（預填）檔案的路徑。 例如， /content/prefilldata.xml
   - `label:` label引數指定服務的顯示名稱。 例如，預設預填服務

1. 儲存並關閉`Prefill.java`檔案。
1. 將`AEM Forms Client SDK`套件新增至樣版專案的建置路徑。
1. 編譯專案並為該套件組合建立.jar。

#### 啟動並使用預填服務 {#start-and-use-the-prefill-service}

若要啟動預填服務，請將JAR檔案上傳到[!DNL AEM Forms] Web主控台，然後啟動服務。 現在，服務開始出現在最適化Forms編輯器中。 若要將預填服務關聯至調適型表單：

1. 在Forms編輯器中開啟最適化表單，然後開啟表單容器的「屬性」面板。
1. 在「屬性」主控台中，瀏覽至[!DNL AEM Forms]容器>基本>預填服務。
1. 選取預設預填服務，然後按一下&#x200B;**[!UICONTROL 儲存]**。 此服務與表單相關聯。

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