---
title: 如何配置資料源？
description: Experience Manager Forms資料整合允許您配置和連接到不同的資料源。 瞭解如何將REST風格的Web服務、基於SOAP的Web服務和OData服務配置為資料源，並使用它們建立表單資料模型。
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: ac525d2500177229221a5d6f79d2a8feeefe3f06
workflow-type: tm+mt
source-wordcount: '2195'
ht-degree: 2%

---

# 設定資料來源 {#configure-data-sources}

![資料整合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 資料整合允許您配置和連接到不同的資料源。 支援開箱即用的以下類型：

* 關係資料庫 — MySQL [!DNL Microsoft SQL Server]。 [!DNL IBM DB2], [!DNL Oracle RDBMS]
* REST風格的Web服務
* 基於SOAP的Web服務
* OData服務（4.0版）
* Microsoft®動力學
* SalesForce
* Microsoft® AzureBlob儲存

資料整合支援OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)。 [客戶端憑據](https://oauth.net/2/grant-types/client-credentials/))、基本身份驗證和API密鑰身份驗證類型開箱即用，並允許實施訪問Web服務的自定義身份驗證。 而RESTful、基於SOAP和OData服務是在 [!DNL Experience Manager] as a Cloud Service、關係資料庫的JDBC和關係資料庫的連接器 [!DNL Experience Manager] 在中配置用戶配置檔案 [!DNL Experience Manager] web控制台。

## 配置關係資料庫 {#configure-relational-database}

### 必備條件

在使用 [!DNL Experience Manager] Web控制台配置，必須：
* [通過雲管理器API啟用高級網路](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)，因為預設情況下禁用埠。
* [在Maven中添加JDBC驅動程式依賴項](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies)。


### 配置關係資料庫的步驟

可以使用 [!DNL Experience Manager] Web控制台配置。 請執行下列動作：

1. 轉到 [!DNL Experience Manager] Web控制台 `https://server:host/system/console/configMgr`。
1. 定位 **[!UICONTROL 日公共JDBC連接池]** 配置。 按一下以在編輯模式下開啟配置。

   ![JDBC連接器池](/help/forms/assets/jdbc_connector.png)

1. 在「配置」對話框中，指定要配置的資料庫的詳細資訊，如：

   * JDBC驅動程式的Java™類名
   * JDBC連接URI
   * 用於建立與JDBC驅動程式連接的用戶名和密碼
   * 在 **[!UICONTROL 驗證查詢]** 欄位以驗證來自池的連接。 查詢必須至少返回一行。 根據您的資料庫，指定以下選項之一：
      * 選擇1（MySQL和MS SQL）
      * 從雙(Oracle)中選擇1
   * 資料源的名稱

   用於配置關係資料庫的示例字串：

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > 參考 [使用JDBC DataSourcePool的SQL連接](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) 的子菜單。

1. 點擊 **[!UICONTROL 保存]** 的子菜單。

現在，您可以將配置的關係資料庫與表單資料模型一起使用。

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

## 為雲服務配置配置資料夾 {#cloud-folder}

配置RESTful、SOAP和OData服務的雲服務需要配置雲服務資料夾。

中的所有雲服務配置 [!DNL Experience Manager] 併入 `/conf` 資料夾 [!DNL Experience Manager] 儲存庫。 預設情況下， `conf` 資料夾包含 `global` 建立雲服務配置的資料夾。 但是，您必須為雲配置手動啟用它。 您也可以在 `conf` 建立和組織雲服務配置。

要為雲服務配置配置資料夾：

1. 轉到 **[!UICONTROL 工具>常規>配置瀏覽器]**。
   * 查看 [配置瀏覽器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) 的子菜單。
1. 執行以下操作以啟用雲配置的全局資料夾，或跳過此步驟為雲服務配置建立和配置另一個資料夾。

   1. 在 **[!UICONTROL 配置瀏覽器]**，選擇 `global` 資料夾和點擊 **[!UICONTROL 屬性]**。

   1. 在 **[!UICONTROL 配置屬性]** 對話框，啟用 **[!UICONTROL 雲配置]**。

   1. 點擊 **[!UICONTROL 保存並關閉]** 以保存配置並退出對話框。

1. 在 **[!UICONTROL 配置瀏覽器]**&#x200B;按一下 **[!UICONTROL 建立]**。
1. 在 **[!UICONTROL 建立配置]** 對話框，指定資料夾的標題，並啟用 **[!UICONTROL 雲配置]**。
1. 點擊 **[!UICONTROL 建立]** 建立為雲服務配置啟用的資料夾。

## 配置REST風格的Web服務 {#configure-restful-web-services}

可使用 [Swagger規格](https://swagger.io/specification/v2/) JSON或YAML格式 [!DNL Swagger] 定義檔案。 在中配置REST風格的Web服務 [!DNL Experience Manager] as a Cloud Service，確保您 [!DNL Swagger] 檔案([Swagger 2.0版](https://swagger.io/specification/v2/))或 [!DNL Swagger] 檔案([Swagger 3.0版](https://swagger.io/specification/v3/))或檔案所在的URL。

### 為Open API規範2.0版配置REST風格的服務 {#configure-restful-services-open-api-2.0}

1. 轉到 **[!UICONTROL 工具>Cloud Services>資料源]**。 點擊以選擇要在其中建立雲配置的資料夾。

   請參閱 [為雲服務配置配置資料夾](configure-data-sources.md#cloud-folder) 有關為雲服務配置建立和配置資料夾的資訊。

1. 點擊 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**。 指定配置的名稱和標題（可選），選擇 **[!UICONTROL REST風格服務]** 從 **[!UICONTROL 服務類型]** 下拉，（可選）瀏覽並選擇配置的縮略圖，然後點擊 **[!UICONTROL 下一個]**。
1. 為RESTful服務指定以下詳細資訊：

   * 從中選擇URL或檔案 [!UICONTROL 斯瓦格源] ，並相應地指定 [!DNL Swagger URL] 到[!DNL  Swagger] 定義檔案或上載 [!DNL Swagger] 檔案。
   * 基於[!DNL  Swagger] 源輸入。以下欄位預填充了值：

      * 方案：REST API使用的傳輸協定。 下拉清單中顯示的方案類型數取決於在 [!DNL Swagger] 源。
      * 主機：為REST API提供服務的主機的域名或IP地址。 這是一個強制欄位。
      * 基本路徑：所有API路徑的URL前置詞。 它是一個可選欄位。\
         如有必要，請編輯這些欄位的預填充值。
   * 選擇身份驗證類型 — 無，OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)。 [客戶端憑據](https://oauth.net/2/grant-types/client-credentials/))、基本身份驗證、API密鑰或自定義身份驗證 — 訪問REST風格的服務，並相應地提供身份驗證的詳細資訊。

   如果選擇 **[!UICONTROL API密鑰]** 作為驗證類型，指定API密鑰的值。 API密鑰可以作為請求頭或查詢參數發送。 從 **[!UICONTROL 位置]** 下拉清單，並在 **[!UICONTROL 參數名稱]** 欄位。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 點擊 **[!UICONTROL 建立]** 為REST風格服務建立雲配置。

### 為Open API規範3.0版配置REST風格的服務 {#configure-restful-services-open-api-3.0}

1. 轉到 **[!UICONTROL 工具>Cloud Services>資料源]**。 點擊以選擇要在其中建立雲配置的資料夾。

   請參閱 [為雲服務配置配置資料夾](configure-data-sources.md#cloud-folder) 有關為雲服務配置建立和配置資料夾的資訊。

1. 點擊 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**。 指定配置的名稱和標題（可選），選擇 **[!UICONTROL REST風格服務]** 從 **[!UICONTROL 服務類型]** 下拉，（可選）瀏覽並選擇配置的縮略圖，然後點擊 **[!UICONTROL 下一個]**。
1. 為RESTful服務指定以下詳細資訊：

   * 從中選擇URL或檔案 [!UICONTROL 斯瓦格源] ，並相應地指定 [!DNL Swagger 3.0 URL] 到[!DNL  Swagger] 定義檔案或上載 [!DNL Swagger] 檔案。
   * 基於[!DNL  Swagger] 源輸入，顯示與目標伺服器的連接資訊。
   * 選擇身份驗證類型 — 無，OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)。 [客戶端憑據](https://oauth.net/2/grant-types/client-credentials/))、基本身份驗證、API密鑰或自定義身份驗證 — 訪問REST風格的服務，並相應地提供身份驗證的詳細資訊。

   如果選擇 **[!UICONTROL API密鑰]** 作為驗證類型，指定API密鑰的值。 API密鑰可以作為請求頭或查詢參數發送。 從 **[!UICONTROL 位置]** 下拉清單，並在 **[!UICONTROL 參數名稱]** 欄位。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 點擊 **[!UICONTROL 建立]** 為REST風格服務建立雲配置。

REST風格的服務Open API規範3.0版不支援的一些操作包括：
* 回調
* 一個/任意
* 遠程引用
* 連結
* 針對單個操作的不同MIME類型的不同請求主體

您可以參考 [OpenAPI 3.0規範](https://swagger.io/specification/v3/) 的上界。

### 表單資料模型HTTP客戶端配置以優化效能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 當與REST風格的Web服務整合為資料源時，將形成資料模型，包括用於效能優化的HTTP客戶端配置。

設定以下屬性 **[!UICONTROL REST資料源的表單資料模型HTTP客戶端配置]** 用於指定規則運算式的配置：

* 使用 `http.connection.max.per.route` 屬性，用於設定表單資料模型和REST風格的Web服務之間允許的最大連接數。 預設值為20個連接。

* 使用 `http.connection.max` 屬性，指定每個路由允許的最大連接數。 預設值為40個連接。

* 使用 `http.connection.keep.alive.duration` 屬性，指定持續HTTP連接保持活動的持續時間。 預設值為15秒。

* 使用 `http.connection.timeout` 屬性，指定持續時間 [!DNL Experience Manager Forms] 伺服器等待連接建立。 預設值為10秒。

* 使用 `http.socket.timeout` 屬性，指定兩個資料包之間不活動的最大時間段。 預設值為30秒。

以下JSON檔案顯示示例：


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

1. 點擊 **[!UICONTROL REST資料源的表單資料模型HTTP客戶端配置]**。

1. 在 [!UICONTROL REST資料源的表單資料模型HTTP客戶端配置] 對話框：

   * 指定表單資料模型和REST風格Web服務之間允許的最大連接數 **[!UICONTROL 連接限制總數]** 的子菜單。 預設值為20個連接。

   * 指定中每個路由允許的最大連接數 **[!UICONTROL 每個路由的連接限制]** 的子菜單。 預設值為兩個連接。

   * 指定持續HTTP連接保持活動的持續時間， **[!UICONTROL 保持活力]** 的子菜單。 預設值為15秒。

   * 指定持續時間， [!DNL Experience Manager Forms] 伺服器等待建立連接，在 **[!UICONTROL 連接超時]** 的子菜單。 預設值為10秒。

   * 指定中兩個資料包之間不活動的最大時間段 **[!UICONTROL 套接字超時]** 的子菜單。 預設值為30秒。

## 配置SOAP Web服務 {#configure-soap-web-services}

使用 [Web服務描述語言(WSDL)規範](https://www.w3.org/TR/wsdl)。 [!DNL Experience Manager Forms] 不支援RPC樣式WSDL模型。

在中配置基於SOAP的Web服務 [!DNL Experience Manager] as a Cloud Service，確保您有Web服務的WSDL URL，並執行以下操作：

1. 轉到 **[!UICONTROL 工具>Cloud Services>資料源]**。 點擊以選擇要在其中建立雲配置的資料夾。

   請參閱 [為雲服務配置配置資料夾](configure-data-sources.md#cloud-folder) 有關為雲服務配置建立和配置資料夾的資訊。

1. 點擊 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**。 指定配置的名稱和標題（可選），選擇 **[!UICONTROL SOAP Web服務]** 從 **[!UICONTROL 服務類型]** 下拉，（可選）瀏覽並選擇配置的縮略圖，然後點擊 **[!UICONTROL 下一個]**。
1. 為SOAP Web服務指定以下內容：

   * Web服務的WSDL URL。
   * 服務端點. 在此欄位中指定值以覆蓋WSDL中提及的服務端點。
   * 選擇身份驗證類型 — 無，OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)。 [客戶端憑據](https://oauth.net/2/grant-types/client-credentials/))、基本身份驗證或自定義身份驗證 — 訪問SOAP服務，並相應地提供身份驗證的詳細資訊。

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 點擊 **[!UICONTROL 建立]** 為SOAP web服務建立雲配置。

### 在SOAP Web服務WSDL中啟用導入語句 {#enable-import-statements}

可以指定規則運算式，該規則運算式用作SOAP Web服務WSDL中允許作為導入語句的絕對URL的篩選器。 預設情況下，此欄位中沒有值。 因此， [!DNL Experience Manager] 阻止WSDL中提供的所有導入語句。 如果指定 `.*` 作為該欄位的值， [!DNL Experience Manager] 允許所有導入語句。

設定 `importAllowlistPattern` 屬性 **[!UICONTROL 表單資料模型SOAP Web服務導入允許清單]** 用於指定規則運算式的配置。 以下JSON檔案顯示示例：


```json
{
  "importAllowlistPattern": ".*"
}
```


若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。

## 配置OData服務 {#config-odata}

OData服務由其服務根URL標識。 在中配置OData服務 [!DNL Experience Manager] as a Cloud Service，確保您有服務的根URL，並執行以下操作：

>[!NOTE]
>
> 表單資料模型支援 [OData版本4](https://www.odata.org/documentation/)。
>有關配置的逐步指南 [!DNL Microsoft® Dynamics 365]，聯機或本地，請參閱 [[!DNL Microsoft® Dynamics] OData配置](ms-dynamics-odata-configuration.md)。

1. 轉到 **[!UICONTROL 工具>Cloud Services>資料源]**。 點擊以選擇要在其中建立雲配置的資料夾。

   請參閱 [為雲服務配置配置資料夾](#cloud-folder) 有關為雲服務配置建立和配置資料夾的資訊。

1. 點擊 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**。 指定配置的名稱和標題（可選），選擇 **[!UICONTROL OData服務]** 從 **[!UICONTROL 服務類型]** 下拉，（可選）瀏覽並選擇配置的縮略圖，然後點擊 **[!UICONTROL 下一個]**。
1. 為OData服務指定以下詳細資訊：

   * 要配置的OData服務的服務根URL。
   * 選擇身份驗證類型 — 無，OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)。 [客戶端憑據](https://oauth.net/2/grant-types/client-credentials/))、基本身份驗證、API密鑰或自定義身份驗證 — 訪問OData服務，並相應地提供身份驗證的詳細資訊。

   如果選擇 **[!UICONTROL API密鑰]** 作為驗證類型，指定API密鑰的值。 API密鑰可以作為請求頭或查詢參數發送。 從 **[!UICONTROL 位置]** 下拉清單，並在 **[!UICONTROL 參數名稱]** 欄位。

   >[!NOTE]
   必須選擇OAuth 2.0身份驗證類型才能連接 [!DNL Microsoft® Dynamics] 使用OData終結點作為服務根的服務。

1. 點擊 **[!UICONTROL 建立]** 為OData服務建立雲配置。

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## 後續步驟 {#next-steps}

您已配置資料源。 接下來，您可以建立表單資料模型，或者如果已經建立了沒有資料源的表單資料模型，則可以將其與您配置的資料源關聯。 請參閱 [建立表單資料模型](create-form-data-models.md) 的雙曲餘切值。
