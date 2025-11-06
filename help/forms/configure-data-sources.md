---
title: 如何設定資料來源？
description: 瞭解如何將RESTful Web服務、SOAP式Web服務和OData服務設定為表單資料模型(FDM)的資料來源。
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 4%

---


# 設定資料來源 {#configure-data-sources}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/configure-data-sources.html) |
| AEM as a Cloud Service  | 本文章 |

![資料整合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms]資料整合可讓您設定並連線至不同的資料來源。 下列是支援的現成可用型別：

* 關聯式資料庫 — MySQL、[!DNL Microsoft® SQL Server]、[!DNL IBM® DB2®]、postgreSQL和[!DNL Oracle RDBMS]
* RESTful Web服務
* SOAP型網站服務
* OData服務（4.0版）
* Microsoft® Dynamics
* Salesforce
* Microsoft® Azure Blob儲存體

資料整合可支援OAuth2.0（[授權代碼](https://oauth.net/2/grant-types/authorization-code/)、[使用者端認證](https://oauth.net/2/grant-types/client-credentials/)）、基本驗證及API金鑰驗證型別，並且允許實作自訂驗證以存取Web服務。 在[!DNL Experience Manager] as a Cloud Service中設定RESTful、SOAP型和OData服務時，在[!DNL Experience Manager] Web主控台中設定關聯式資料庫的JDBC和[!DNL Experience Manager]使用者設定檔的聯結器。

## 設定關聯式資料庫 {#configure-relational-database}

### 先決條件

在使用[!DNL Experience Manager] Web主控台組態設定關聯式資料庫之前，必須：

* [透過Cloud Manager API啟用進階網路](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)，因為連線埠預設為停用。
* [在Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies)中新增JDBC驅動程式相依性。


### 設定關聯式資料庫的步驟

您可以使用[!DNL Experience Manager] Web主控台組態來設定關聯式資料庫。 請執行下列動作：

1. 移至[!DNL Experience Manager]的`https://server:host/system/console/configMgr`網頁主控台。
1. 找到&#x200B;**[!UICONTROL Day Commons JDBC連線集區]**&#x200B;組態。 選取以在編輯模式中開啟設定。

   ![JDBC聯結器集區](/help/forms/assets/jdbc_connector.png)

1. 在設定對話方塊中，指定您要設定的資料庫詳細資訊，例如：

   * JDBC驅動程式的Java™類別名稱
   * JDBC連線URI
   * 與JDBC驅動程式建立連線的使用者名稱和密碼
   * 在&#x200B;**[!UICONTROL 驗證查詢]**&#x200B;欄位中指定SQL SELECT查詢，以驗證集區的連線。 查詢至少必須傳回一列。 根據您的資料庫，指定下列其中一項：
      * 選取1 (MySQL和MS® SQL)
      * 選取1個(雙(Oracle)
   * 資料來源的名稱

   設定關聯式資料庫的範例字串：

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > 如需詳細資訊，請參閱使用JDBC DataSourcePool[的](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html)SQL連線。

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存組態。

現在，您可以將已設定的關聯式資料庫與表單資料模型(FDM)搭配使用。

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and select to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties are available for use in form data model (FDM). Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model (FDM) can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Select **[!UICONTROL Save]** to save the configuration. -->

## 設定雲端服務設定的資料夾 {#cloud-folder}

設定RESTful、SOAP和OData服務的雲端服務時，需要設定雲端服務資料夾。

[!DNL Experience Manager]中的所有雲端服務設定都已整合到`/conf`存放庫的[!DNL Experience Manager]資料夾中。 根據預設，`conf`資料夾包含您可以建立雲端服務設定的`global`資料夾。 不過，您必須手動為雲端設定啟用它。 您也可以在`conf`中建立其他資料夾，以建立並組織雲端服務設定。

若要設定雲端服務設定的資料夾：

1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   * 如需詳細資訊，請參閱[設定瀏覽器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html)檔案。
1. 請執行以下操作來啟用雲端設定的全域資料夾，或跳過此步驟來建立和設定雲端服務設定的另一個資料夾。

   1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;中，選取`global`資料夾並選取&#x200B;**[!UICONTROL 屬性]**。

   1. 在「**[!UICONTROL 設定屬性]**」對話框中，啟用&#x200B;**[!UICONTROL 雲端設定]**。

   1. 選取「**[!UICONTROL 儲存並關閉]**」，即可儲存設定並退出對話框。

1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;中，選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立設定]**&#x200B;對話方塊中，指定資料夾的標題，並啟用&#x200B;**[!UICONTROL 雲端設定]**。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立為雲端服務設定啟用的資料夾。

## 設定RESTful Web服務 {#configure-restful-web-services}

可在[定義檔或服務端點中使用JSON或YAML格式的](https://swagger.io/specification/v2/)Swagger規格[!DNL Swagger]來描述RESTful Web服務。

>[!NOTE]
> 若要在[!DNL Experience Manager] as a Cloud Service中設定RESTful Web服務，請確定您的檔案系統上有[!DNL Swagger]檔案（[Swagger 2.0](https://swagger.io/specification/v2/)版）或[!DNL Swagger]檔案（[Swagger 3.0](https://swagger.io/specification/v3/)版），或是裝載該檔案的URL。

### 為Open API規格2.0版設定RESTful服務 {#configure-restful-services-open-api-2.0}

1. 移至&#x200B;**[!UICONTROL 工具>雲端服務>資料來源]**。 選取以選取您要建立雲端設定的資料夾。

   請參閱[設定雲端服務設定的資料夾](configure-data-sources.md#cloud-folder)，以取得關於建立和設定雲端服務設定的資料夾的資訊。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料Source設定精靈]**。 指定設定的名稱及標題，從&#x200B;**[!UICONTROL 服務型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL RESTful服務]**，選擇性地瀏覽並選取設定的縮圖影像，然後選取&#x200B;**[!UICONTROL 下一步]**。
1. 指定RESTful服務的下列詳細資料：

   * 從[!UICONTROL Swagger Source]下拉式清單中選取URL或檔案，並相應地指定[!DNL Swagger URL]定義檔案的[!DNL &#x200B; Swagger]或從您的本機檔案系統上傳[!DNL Swagger]檔案。
   * 根據[!DNL &#x200B; Swagger] Source輸入，下列欄位已預先填入值：

      * 配置： REST API使用的傳輸通訊協定。 下拉式清單中顯示的配置型別數目，取決於[!DNL Swagger]來源中定義的配置。
      * 主機：提供REST API之主機的網域名稱或IP位址。 這是必填欄位。
      * 基本路徑：所有API路徑的URL首碼。 它是選用欄位。\
        如有需要，請編輯這些欄位的預先填入值。

   * 選取驗證型別 — 無、OAuth2.0（[授權碼](https://oauth.net/2/grant-types/authorization-code/)、[使用者端認證](https://oauth.net/2/grant-types/client-credentials/)）、基本驗證、API金鑰或自訂驗證 — 以存取RESTful服務，並相應地提供驗證的詳細資料。

   如果您選取&#x200B;**[!UICONTROL API金鑰]**&#x200B;作為驗證型別，請指定API金鑰的值。 API金鑰可作為請求標頭或查詢引數傳送。 從&#x200B;**[!UICONTROL 位置]**&#x200B;下拉式清單中選取其中一個選項，並相應地在&#x200B;**[!UICONTROL 引數名稱]**&#x200B;欄位中指定標頭名稱或查詢引數。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立RESTful服務的雲端設定。

### 為Open API規格3.0版設定RESTful服務 {#configure-restful-services-open-api-3.0}

1. 移至&#x200B;**[!UICONTROL 工具>雲端服務>資料來源]**。 選取以選取您要建立雲端設定的資料夾。

   請參閱[設定雲端服務設定的資料夾](configure-data-sources.md#cloud-folder)，以取得關於建立和設定雲端服務設定的資料夾的資訊。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料Source設定精靈]**。 指定設定的名稱及標題，從&#x200B;**[!UICONTROL 服務型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL RESTful服務]**，選擇性地瀏覽並選取設定的縮圖影像，然後選取&#x200B;**[!UICONTROL 下一步]**。
1. 指定RESTful服務的下列詳細資料：

   * 從[!UICONTROL Swagger Source]下拉式清單中選取URL或檔案，並相應地指定[!DNL Swagger 3.0 URL]定義檔案的[!DNL &#x200B; Swagger]或從您的本機檔案系統上傳[!DNL Swagger]檔案。
   * 根據[!DNL &#x200B; Swagger] Source輸入，會顯示與目標伺服器的連線資訊。
   * 選取驗證型別 — 無、OAuth2.0（[授權碼](https://oauth.net/2/grant-types/authorization-code/)、[使用者端認證](https://oauth.net/2/grant-types/client-credentials/)）、基本驗證、API金鑰或自訂驗證 — 以存取RESTful服務，並相應地提供驗證的詳細資料。

   如果您選取&#x200B;**[!UICONTROL API金鑰]**&#x200B;作為驗證型別，請指定API金鑰的值。 API金鑰可作為請求標頭或查詢引數傳送。 從&#x200B;**[!UICONTROL 位置]**&#x200B;下拉式清單中選取其中一個選項，並相應地在&#x200B;**[!UICONTROL 引數名稱]**&#x200B;欄位中指定標頭名稱或查詢引數。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立RESTful服務的雲端設定。

RESTful Services Open API Specification 3.0版不支援的作業包括：

* 回呼
* oneof/any of
* 遠端參考
* 連結
* 針對單一作業的不同MIME型別，有不同的要求內文

如需詳細資訊，請參閱[OpenAPI 3.0規格](https://swagger.io/specification/v3/)。

### 使用服務端點設定RESTful服務 {#configure-restful-services-service-endpoint}

<span class="preview"> Service Endpoint功能在Early Adopter Program之下，僅適用於核心元件。 您可以使用官方電子郵件 ID 寫信至 aem-forms-ea@adobe.com，以加入早期採用者計劃並要求存取該功能。</span>

1. 移至&#x200B;**[!UICONTROL 工具>雲端服務>資料來源]**。 選取以選取您要建立雲端設定的資料夾。

   請參閱[設定雲端服務設定的資料夾](configure-data-sources.md#cloud-folder)，以取得關於建立和設定雲端服務設定的資料夾的資訊。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料Source設定精靈]**。

1. 指定設定的名稱及標題，從&#x200B;**[!UICONTROL 服務型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL RESTful服務]**，選擇性地瀏覽並選取設定的縮圖影像，然後選取&#x200B;**[!UICONTROL 下一步]**。

1. 在下一個頁面，從&#x200B;**[!UICONTROL RESTful服務下拉式清單]**&#x200B;中選取&#x200B;**[!UICONTROL 服務端點]**。

   ![服務端點](/help/forms/assets/select-service-endpoint.png)

1. 指定&#x200B;**[!UICONTROL 服務端點URL]**。

   >[!NOTE]
   > 依預設，「方法型別」為POST。
1. 選取您要從下拉式清單中選擇的其中一個「內容型別」。 內容型別為多部分表單資料、JSON和URL編碼（索引鍵值配對）。
1. 現在，您可以從下拉式清單中選取任一驗證型別，例如OAuth 2.0、基本驗證、API金鑰、自訂驗證。
   ![服務端點驗證型別](/help/forms/assets/service-endpoint-authtype.png)
1. 按一下「建立」。

### 表單資料模型(FDM) HTTP使用者端設定可最佳化效能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms]在與RESTful Web服務整合時形成資料模型，因為資料來源包括用於效能最佳化的HTTP使用者端設定。

設定REST資料來源&#x200B;**[!UICONTROL 組態的]**&#x200B;表單資料模型HTTP使用者端組態的下列屬性，以指定規則運算式：

* 使用`http.connection.max.per.route`屬性設定表單資料模型(FDM)與RESTful Web服務之間允許的最大連線數目。 預設值為20個連線。

* 使用`http.connection.max`屬性指定每個路由允許的最大連線數目。 預設值為40個連線。

* 使用`http.connection.keep.alive.duration`屬性指定持續性HTTP連線持續運作的持續時間。 預設值為15秒。

* 使用`http.connection.timeout`屬性指定持續時間，[!DNL Experience Manager Forms]伺服器會等待建立連線。 預設值為10秒。

* 使用`http.socket.timeout`屬性指定兩個資料封包之間閒置的最長時間。 預設值為30秒。

下列JSON檔案顯示範例：


```json
{   
   "http.connection.keep.alive.duration":"15",   
   "http.connection.max.per.route":"20",   
   "http.connection.timeout":"10",   
   "http.socket.timeout":"30",   
   "http.connection.idle.connection.timeout":"15",   
   "http.connection.max":"40" 
} 
```

1. 選取REST資料來源&#x200B;**[!UICONTROL 的]**&#x200B;表單資料模型HTTP使用者端組態。

1. 在[!UICONTROL REST資料來源]的表單資料模型HTTP使用者端設定對話方塊中：

   * 在&#x200B;**[!UICONTROL 連線限制（共]**&#x200B;個欄位）中，指定表單資料模型(FDM)與RESTful Web服務之間允許的最大連線數目。 預設值為20個連線。

   * 在&#x200B;**[!UICONTROL 每個路由的連線限制]**&#x200B;欄位中，指定每個路由允許的最大連線數目。 預設值是兩個連線。

   * 在&#x200B;**[!UICONTROL 保持連線]**&#x200B;欄位中指定持續性HTTP連線持續運作的持續時間。 預設值為15秒。

   * 在[!DNL Experience Manager Forms]連線逾時&#x200B;**[!UICONTROL 欄位中指定]**&#x200B;伺服器等待連線建立的持續時間。 預設值為10秒。

   * 在&#x200B;**[!UICONTROL 通訊端逾時]**&#x200B;欄位中，指定兩個資料封包之間閒置的最長時間。 預設值為30秒。

## 設定SOAP網站服務 {#configure-soap-web-services}

以SOAP為基礎的Web服務是使用[Web服務描述語言(WSDL)規格](https://www.w3.org/TR/wsdl)來描述。 [!DNL Experience Manager Forms]不支援RPC樣式的WSDL模型。

若要在[!DNL Experience Manager] as a Cloud Service中設定SOAP式Web服務，請確定您擁有Web服務的WSDL URL，並執行下列動作：

1. 移至&#x200B;**[!UICONTROL 工具>雲端服務>資料來源]**。 選取以選取您要建立雲端設定的資料夾。

   請參閱[設定雲端服務設定的資料夾](configure-data-sources.md#cloud-folder)，以取得關於建立和設定雲端服務設定的資料夾的資訊。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料Source設定精靈]**。 指定設定的名稱及標題，從&#x200B;**[!UICONTROL 服務型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL SOAP Web服務]**，瀏覽並選取設定的縮圖影像，然後選取&#x200B;**[!UICONTROL 下一步]**。
1. 針對SOAP Web服務指定下列專案：

   * Web服務的WSDL URL。
   * 服務端點。 在此欄位中指定值，以覆寫WSDL中提及的服務端點。
   * 選取驗證型別 — None、OAuth2.0（[授權代碼](https://oauth.net/2/grant-types/authorization-code/)、[使用者端認證](https://oauth.net/2/grant-types/client-credentials/)）、Basic Authentication或Custom Authentication — 以存取SOAP服務，並相應地提供驗證的詳細資料。

     <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
     <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

     <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立SOAP Web服務的雲端設定。

### 啟用在SOAP網站服務WSDL中使用匯入陳述式 {#enable-import-statements}

您可以指定規則運算式，用來篩選在SOAP Web服務WSDL中允許做為匯入陳述式的絕對URL。 依預設，此欄位中沒有值。 因此，[!DNL Experience Manager]會封鎖WSDL中可用的所有匯入陳述式。 如果您在此欄位中指定`.*`為值，[!DNL Experience Manager]會允許所有匯入陳述式。

設定`importAllowlistPattern`表單資料模型SOAP Web服務匯入允許清單&#x200B;**[!UICONTROL 設定的]**&#x200B;屬性，以指定規則運算式。 下列JSON檔案顯示範例：

```json
{
  "importAllowlistPattern": ".*"
}
```

若要設定值，請[使用 AEM SDK 產生 OSGi 設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hant#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並[將設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant#deployment-process)您的 Cloud Service 執行個體。

## 設定OData服務 {#config-odata}

OData服務由其服務根URL識別。 若要在[!DNL Experience Manager] as a Cloud Service中設定OData服務，請確定您擁有該服務的服務根URL，並執行下列動作：

>[!NOTE]
>
> 表單資料模型(FDM)支援[OData 4](https://www.odata.org/documentation/)版。
>如需設定[!DNL Microsoft®® Dynamics 365] （線上或內部部署）的逐步指南，請參閱[[!DNL Microsoft® Dynamics] OData設定](ms-dynamics-odata-configuration.md)。

1. 移至&#x200B;**[!UICONTROL 工具>雲端服務>資料來源]**。 選取以選取您要建立雲端設定的資料夾。

   請參閱[設定雲端服務設定的資料夾](#cloud-folder)，以取得關於建立和設定雲端服務設定的資料夾的資訊。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料Source設定精靈]**。 指定組態的名稱與標題，從&#x200B;**[!UICONTROL 服務型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL OData服務]**，選擇性地瀏覽並選取組態的縮圖影像，然後選取&#x200B;**[!UICONTROL 下一步]**。
1. 指定OData服務的下列詳細資料：

   * 要設定之OData服務的服務根URL。
   * 選取驗證型別 — 無、OAuth2.0（[授權碼](https://oauth.net/2/grant-types/authorization-code/)、[使用者端認證](https://oauth.net/2/grant-types/client-credentials/)）、基本驗證、API金鑰或自訂驗證 — 以存取OData服務，並相應地提供驗證的詳細資料。

   如果您選取&#x200B;**[!UICONTROL API金鑰]**&#x200B;作為驗證型別，請指定API金鑰的值。 API金鑰可作為請求標頭或查詢引數傳送。 從&#x200B;**[!UICONTROL 位置]**&#x200B;下拉式清單中選取其中一個選項，並相應地在&#x200B;**[!UICONTROL 引數名稱]**&#x200B;欄位中指定標頭名稱或查詢引數。

   >[!NOTE]
   >
   >選取OAuth 2.0驗證型別，以使用OData端點作為服務根來連線至[!DNL Microsoft®® Dynamics]服務。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立OData服務的雲端設定。

<!--
## Configure Microsoft&reg; SharePoint List {#config-sharepoint-list}

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

To save data in a tabular form use, Microsoft&reg; SharePoint List. To configure a Microsoft SharePoint List in [!DNL Experience Manager] as a Cloud Service, do the following:

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft&reg; SharePoint]**.   
1. Select a **Configuration Container**. The configuration is stored in the selected Configuration Container. 
1. Click **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** from the drop-down list. The SharePoint configuration wizard appears.  
1. Specify the **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** and **[!UICONTROL OAuth URL]**. For information on how to retrieve Client ID, Client Secret, Tenant ID for OAuth URL, see [Microsoft&reg; Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
    * You can retrieve the `Client ID` and `Client Secret` of your app from the Microsoft&reg; Azure portal.
    * In the Microsoft&reg; Azure portal, add the Redirect URI as `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Replace `[author-instance]` with the URL of your Author instance.
    * Add the API permissions `offline_access` and `Sites.Manage.All` in the **Microsoft&reg; Graph** tab to provide read/write permissions. Add `AllSites.Manage` permission in the **Sharepoint** tab to interact remotely with SharePoint data.
    * Use OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` with the `tenant-id` of your app from the Microsoft&reg; Azure portal.

      >[!NOTE]
      >
      > The **client secret** field is mandatory or optional depends upon your Azure Active Directory application configuration. If your application is configured to use a client secret, it is mandatory to provide the client secret.

1. Click **[!UICONTROL Connect]**. On a successful connection, the `Connection Successful` message appears.
1. Select **[!UICONTROL SharePoint Site]** and **[!UICONTROL SharePoint List]** from the drop-down list.
1. Select **[!UICONTROL Create]** to create the cloud configuration for the Microsoft&reg; SharePointList.

-->

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model (FDM), both the data source and [!DNL Experience Manager] Server running Form Data Model (FDM) authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model (FDM) on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and select **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and select **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, select **[!UICONTROL Select Certificate File]**, upload the certificate, and select **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## 後續步驟 {#next-steps}

您已設定資料來源。 接下來，您可以建立表單資料模型(FDM)，或者，如果您已建立不含資料來源的表單資料模型(FDM)，則可以將其與您設定的資料來源建立關聯。 如需詳細資訊，請參閱[建立表單資料模型](create-form-data-models.md)。

<!--

>[!MORELIKETHIS]
>
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>*  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->