---
title: 如何設定資料來源？
description: Experience Manager Forms資料整合可讓您設定並連線至不同的資料來源。 了解如何將RESTful Web服務、基於SOAP的Web服務和OData服務配置為資料源，並使用它們建立表單資料模型。
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: 983f1b815fd213863ddbcd83ac7e3f076c57d761
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 5%

---

# 設定資料來源 {#configure-data-sources}

![資料整合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 資料整合可讓您設定並連線至不同的資料來源。 支援的現成可用類型如下：

<!-- * Relational databases - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2], and [!DNL Oracle RDBMS] 
* [!DNL Experience Manager] user profile  -->
* RESTful Web服務
* 基於SOAP的Web服務
* OData服務（4.0版）
* Microsoft Dynamics
* SalesForce
* Microsoft Azure Blob儲存

資料整合支援OAuth2.0、基本驗證和API金鑰驗證類型，且可立即使用，並可實作自訂驗證以存取網站服務。 而RESTful、SOAP型和OData服務則配置在 [!DNL Experience Manager] as a Cloud Service <!--, JDBC for relational databases --> 和連接器 [!DNL Experience Manager] 使用者設定檔設定於 [!DNL Experience Manager] web主控台。

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] 不支援關係資料庫。

<!-- ## Configure relational database {#configure-relational-database}

You can configure relational databases using [!DNL Experience Manager] Web Console Configuration. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://server:host/system/console/configMgr`.
1. Look for **[!UICONTROL Apache Sling Connection Pooled DataSource]** configuration. Tap to open the configuration in edit mode.
1. In the configuration dialog, specify the details for the database you want to configure, such as:

    * Name of the data source
    * Data source service property that stores the data source name
    * Java class name for the JDBC driver
    * JDBC connection URI
    * Username and password to establish connection with the JDBC driver

   >[!NOTE]
   >
   >Ensure that you encrypt sensitive information like passwords before configuring the data source. To encrypt:
   >
   >    
   >    
   >    1. Go to https://'[server]:[port]'/system/console/crypto.
   >    1. In the **[!UICONTROL Plain Text]** field, specify the password or any string to encrypt and tap **[!UICONTROL Protect]**.
   >    
   >    
   >    
   >The encrypted text appears in the Protected Text field that you can specify in the configuration.

1. Enable **[!UICONTROL Test on Borrow]** or **[!UICONTROL Test on Return]** to specify that the objects are validated before being borrowed or returned from and to the pool, respectively.
1. Specify a SQL SELECT query in the **[!UICONTROL Validation Query]** field to validate connections from the pool. The query must return at least one row. Based on your database, specify one of the following:

    * SELECT 1 (MySQL and MS SQL) 
    * SELECT 1 from dual (Oracle)

1. Tap **[!UICONTROL Save]** to save the configuration. -->

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties will be available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Tap **[!UICONTROL Save]** to save the configuration. -->

## 配置雲端服務配置的資料夾 {#cloud-folder}

為RESTful、SOAP和OData服務配置雲服務時，需要配置雲服務資料夾。

中的所有雲端服務設定 [!DNL Experience Manager] 併入 `/conf` 資料夾 [!DNL Experience Manager] 存放庫。 依預設， `conf` 資料夾包含 `global` 可在其中建立雲端服務設定的資料夾。 不過，您必須為雲端設定手動啟用。 您也可以在 `conf` 來建立和組織雲端服務設定。

要配置雲端服務配置的資料夾：

1. 前往 **[!UICONTROL 工具>一般>設定瀏覽器]**.
   * 請參閱 [配置瀏覽器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) 檔案以取得詳細資訊。
1. 請執行下列操作以啟用雲配置的全局資料夾，或跳過此步驟以建立和配置雲服務配置的其他資料夾。

   1. 在 **[!UICONTROL 配置瀏覽器]**，請選取 `global` 資料夾和點選 **[!UICONTROL 屬性]**.

   1. 在 **[!UICONTROL 配置屬性]** 對話框，啟用 **[!UICONTROL 雲端設定]**.

   1. 點選 **[!UICONTROL 儲存並關閉]** 以保存配置並退出對話框。

1. 在 **[!UICONTROL 配置瀏覽器]**，點選 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立配置]** 對話框，指定資料夾的標題並啟用 **[!UICONTROL 雲端設定]**.
1. 點選 **[!UICONTROL 建立]** 建立雲端服務設定啟用的資料夾。

## 配置RESTful Web服務 {#configure-restful-web-services}

RESTful Web服務可使用 [Swagger規格](https://swagger.io/specification/v2/) JSON或YAML格式 [!DNL Swagger] 定義檔案。 要配置RESTful Web服務，請在 [!DNL Experience Manager] as a Cloud Service，確保您擁有 [!DNL Swagger] 檔案([Swagger 2.0版](https://swagger.io/specification/v2/))，或托管檔案的URL。

請執行以下操作來配置RESTful服務：

1. 前往 **[!UICONTROL 工具>Cloud Services>資料來源]**. 點選以選取您要建立雲端設定的資料夾。

   請參閱 [配置雲端服務配置的資料夾](configure-data-sources.md#cloud-folder) 如需建立和設定雲端服務設定資料夾的相關資訊。

1. 點選 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**. 指定配置的名稱和（可選）標題，選擇 **[!UICONTROL RESTful服務]** 從 **[!UICONTROL 服務類型]** 下拉式清單，（可選）瀏覽並選取設定的縮圖影像，然後點選 **[!UICONTROL 下一個]**.
1. 為RESTful服務指定以下詳細資訊：

   * 從 [!UICONTROL Swagger源] 下拉式清單，並據此指定 [!DNL Swagger URL] 到[!DNL  Swagger] 定義檔案或上傳 [!DNL Swagger] 檔案。
   * 根據[!DNL  Swagger] 來源輸入中，下列欄位會預先填入值：

      * 方案：REST API使用的傳輸通訊協定。 下拉式清單中顯示的配置類型數目取決於 [!DNL Swagger] 來源。
      * 主機：提供REST API之主機的網域名稱或IP位址。 這是必填欄位。
      * 基本路徑：所有API路徑的URL首碼。 此為選用欄位。\
         如有必要，請編輯這些欄位的預先填入值。
   * 選取驗證類型（無、OAuth2.0、基本驗證、API密鑰或自訂驗證）以存取RESTful服務，並據此提供驗證的詳細資訊。

   如果您選取 **[!UICONTROL API金鑰]** 作為驗證類型，請指定API金鑰的值。 API金鑰可以以要求標題或查詢參數的形式傳送。 從 **[!UICONTROL 位置]** 下拉式清單中，並指定標題的名稱或 **[!UICONTROL 參數名稱]** 欄位。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 點選 **[!UICONTROL 建立]** 為RESTful服務建立雲配置。

### 表單資料模型HTTP用戶端設定，以最佳化效能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 表單資料模型與RESTful網站服務整合時，作為資料來源時包含HTTP用戶端設定，以達到效能最佳化。

設定下列屬性 **[!UICONTROL REST資料來源的表單資料模型HTTP用戶端設定]** 指定規則運算式的設定：

* 使用 `http.connection.max.per.route` 屬性，設定表單資料模型與RESTful Web服務之間允許的最大連接數。 預設值為20個連線。

* 使用 `http.connection.max` 屬性，指定每條路由允許的連接數上限。 預設值為40個連線。

* 使用 `http.connection.keep.alive.duration` 屬性，以指定持續HTTP連線保持運作的持續時間。 預設值為15秒。

* 使用 `http.connection.timeout` 屬性，指定持續時間 [!DNL Experience Manager Forms] 伺服器等待連接建立。 預設值為10秒。

* 使用 `http.socket.timeout` 屬性，指定兩個資料封包之間未活動的最長時段。 預設值為30秒。

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

若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。


執行下列步驟來設定表單資料模型HTTP用戶端：

1. 登入 [!DNL Experience Manager Forms] 以管理員身分撰寫執行個體，並前往 [!DNL Experience Manager] web控制台套件組合。 預設URL為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. 點選 **[!UICONTROL REST資料來源的表單資料模型HTTP用戶端設定]**.

1. 在 [!UICONTROL REST資料來源的表單資料模型HTTP用戶端設定] 對話框：

   * 指定表單資料模型與RESTful Web服務之間允許的最大連接數，位於 **[!UICONTROL 連線總數限制]** 欄位。 預設值為20個連線。

   * 指定 **[!UICONTROL 每個路由的連接限制]** 欄位。 預設值為2個連線。

   * 在 **[!UICONTROL 保持活力]** 欄位。 預設值為15秒。

   * 指定持續時間，其 [!DNL Experience Manager Forms] 伺服器會等待連線以建立，位於 **[!UICONTROL 連線逾時]** 欄位。 預設值為10秒。

   * 指定 **[!UICONTROL 通訊端逾時]** 欄位。 預設值為30秒。

## 配置SOAP Web服務 {#configure-soap-web-services}

描述基於SOAP的Web服務，使用 [網站服務描述語言(WSDL)規範](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] 不支援RPC樣式WSDL模型。

若要在 [!DNL Experience Manager] as a Cloud Service的是，請確保您具有Web服務的WSDL URL，並執行以下操作：

1. 前往 **[!UICONTROL 工具>Cloud Services>資料來源]**. 點選以選取您要建立雲端設定的資料夾。

   請參閱 [配置雲端服務配置的資料夾](configure-data-sources.md#cloud-folder) 如需建立和設定雲端服務設定資料夾的相關資訊。

1. 點選 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**. 指定配置的名稱和（可選）標題，選擇 **[!UICONTROL SOAP Web服務]** 從 **[!UICONTROL 服務類型]** 下拉式清單，（可選）瀏覽並選取設定的縮圖影像，然後點選 **[!UICONTROL 下一個]**.
1. 為SOAP Web服務指定以下內容：

   * Web服務的WSDL URL。
   * 服務端點. 在此欄位中指定一個值，以覆蓋WSDL中提及的服務端點。
   * 選取驗證類型（無、OAuth2.0、基本驗證或自訂驗證）以存取SOAP服務，並據此提供驗證的詳細資訊。

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 點選 **[!UICONTROL 建立]** 為SOAP Web服務建立雲配置。

### 啟用在SOAP Web服務WSDL中使用導入語句 {#enable-import-statements}

您可以指定規則運算式，作為絕對URL的篩選器，這些URL在SOAP網站服務WSDL中可作為匯入陳述式。 依預設，此欄位中沒有值。 因此， [!DNL Experience Manager] 阻止WSDL中可用的所有導入語句。 如果您指定 `.*` 作為此欄位中的值， [!DNL Experience Manager] 允許所有導入語句。

設定 `importAllowlistPattern` 屬性 **[!UICONTROL 表單資料模型SOAP網站服務匯入允許清單]** 設定來指定規則運算式。 下列JSON檔案顯示範例：

```json
{
  "importAllowlistPattern": ".*"
}
```

若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。

## 配置OData服務 {#config-odata}

OData服務由其服務根URL識別。 若要在 [!DNL Experience Manager] as a Cloud Service，請確定您有服務的服務根URL，並執行下列操作：

>[!NOTE]
>
> 表單資料模型支援 [OData第4版](https://www.odata.org/documentation/).
>設定的逐步指南 [!DNL Microsoft Dynamics 365]、線上或內部部署，請參閱 [[!DNL Microsoft Dynamics] OData配置](ms-dynamics-odata-configuration.md).

1. 前往 **[!UICONTROL 工具>Cloud Services>資料來源]**. 點選以選取您要建立雲端設定的資料夾。

   請參閱 [配置雲端服務配置的資料夾](#cloud-folder) 如需建立和設定雲端服務設定資料夾的相關資訊。

1. 點選 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**. 指定配置的名稱和（可選）標題，選擇 **[!UICONTROL OData服務]** 從 **[!UICONTROL 服務類型]** 下拉式清單，（可選）瀏覽並選取設定的縮圖影像，然後點選 **[!UICONTROL 下一個]**.
1. 指定OData服務的以下詳細資訊：

   * 要配置的OData服務的服務根URL。
   * 選取驗證類型（無、OAuth2.0、基本驗證、API金鑰或自訂驗證）以存取OData服務，並據此提供驗證的詳細資訊。

   如果您選取 **[!UICONTROL API金鑰]** 作為驗證類型，請指定API金鑰的值。 API金鑰可以以要求標題或查詢參數的形式傳送。 從 **[!UICONTROL 位置]** 下拉式清單中，並指定標題的名稱或 **[!UICONTROL 參數名稱]** 欄位。

   >[!NOTE]
   >
   >您必須選取OAuth 2.0驗證類型才能連線 [!DNL Microsoft Dynamics] 服務使用OData端點作為服務根。

1. 點選 **[!UICONTROL 建立]** 為OData服務建立雲配置。

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other’s identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## 後續步驟 {#next-steps}

您已設定資料來源。 接下來，您可以建立表單資料模型，或者如果您已經建立了沒有資料源的表單資料模型，則可以將其與剛配置的資料源關聯。 請參閱 [建立表單資料模型](create-form-data-models.md) 以取得詳細資訊。
