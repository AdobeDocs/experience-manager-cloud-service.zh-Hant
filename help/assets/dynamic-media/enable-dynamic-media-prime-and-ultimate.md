---
title: 啟用 [!DNL Dynamic Media] Prime和Ultimate
description: 瞭解如何啟用 [!DNL Dynamic Media] Prime和Ultimate方案。
feature: Asset Management
role: User, Admin
exl-id: 0ee161f5-bf44-41f1-928e-c07574fd43cc
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---

# 啟用[!DNL Dynamic Media] Prime和Ultimate {#enable-dynamic-media-prime-and-ultimate}

[!DNL Adobe Experience Manager] as a Cloud Service可讓您存取[!DNL Dynamic Media] Prime和Ultimate產品，以簡化您的數位工作流程並最佳化內容管理。 請參閱[Dynamic Media Prime和Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md)，瞭解其優點以及兩者之間的主要差異。

本文提供端對端工作流程，以啟用[!DNL Dynamic Media]個Prime和Ultimate供應專案。

## 啟用[!DNL Dynamic Media] Ultimate {#enable-dynamic-media-ultimate}

若要啟用[!DNL Dynamic Media] Ultimate：

1. [啟動 [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)
1. [設定 [!DNL Dynamic Media] 解決方案](#configure-dynamic-media-solutions)
1. [建立並列出 [!DNL Dynamic Media] 公司](#create-and-list-dynamic-media-companies)
1. [在傳遞層](#configure-custom-domain-in-delivery-tier)中設定自訂網域

<!--
1. [Onboard API keys using the [!DNL AEM] [!DNL Dynamic Media] API card](#onboarding-api-keys)
-->

如果您需要啟用[!DNL Dynamic Media Prime]，請參閱[啟用 [!DNL Dynamic Media Prime]](#enable-dynamic-media-prime)中提供的快速連結。

### 啟動[!DNL Dynamic Media with OpenAPI] {#activate-dynamic-media-with-openapi}

具有OpenAPI功能的[!DNL Dynamic Media]將DAM置於敏捷且有效率的內容供應鏈生態系統的核心，以確保資產治理和交付。

啟用[!DNL Dynamic Media] Ultimate的程式中的第一個步驟，是為您的Cloud Service環境啟用[[!DNL Dynamic Media] 使用OpenAPI](/help/assets/dynamic-media-open-apis-overview.md)。

#### 準備開始使用 {#prerequisites}

在啟動啟動程式之前，請確定您符合下列需求：

1. [存取Cloud Manager](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。
1. [您的程式包含 [!DNL Dynamic Media] 解決方案](#configure-dynamic-media-solutions)。
1. 您有[!DNL Dynamic Media]個Prime或Ultimate授權。

#### 在您的Cloud Service環境中啟用[!DNL Dynamic Media with OpenAPI]功能 {#enable-dynamic-media-with-openapi-capabilites-in-your-CS-environment}

執行這些步驟以啟用雲端服務環境的[!DNL Dynamic Media with OpenAPI]：

1. [導覽至Cloud Manager UI](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。

1. [如果您沒有現有環境的存取權，請建立環境](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments)。

1. 在[環境]詳細資訊頁面上&#x200B;**[!UICONTROL 環境資訊]**&#x200B;區段的&#x200B;**[!UICONTROL 動態媒體]**&#x200B;列中，選取&#x200B;**[!UICONTROL 按一下以啟動]**。

   ![使用OpenAPI功能啟用Dynamic Media](/help/assets/assets/activate-adv-capabiliites-of-dm-openAPI.png)

1. 在確認對話方塊上按一下[啟動&#x200B;**&#x200B;**]以開始[!DNL Dynamic Media with OpenAPI]啟動程式。 成功啟用後，Cloud Manager會顯示下列狀態更新：
   1. **[!UICONTROL 環境階段]**： **[!UICONTROL 執行中]**
   1. ![DM已啟用](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media &#x200B;]**：**[!UICONTROL &#x200B; OpenAPI功能已啟用&#x200B;]**

      ![啟用成功](/help/assets/assets/activation-successful.png){width="700" align="left"}

#### 重試啟動 {#retry-activation}

如果啟用失敗，Cloud Manager會顯示下列狀態更新：

* **[!UICONTROL 環境階段]**： **[!UICONTROL DM with OpenAPI失敗]**
* ![DM已啟用](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media &#x200B;]**：**[!UICONTROL &#x200B;無法啟動OpenAPI功能&#x200B;]**

  ![重試啟動](/help/assets/assets/retry-dm-openapi-failed-activation.png){width="700" align="left"}

選取&#x200B;**[!UICONTROL 按一下以重試]**&#x200B;以重新啟動啟動。

或者，執行這些步驟以重新啟動啟動程式：

1. 瀏覽到列出所有環境的頁面。

1. 按一下環境列末尾的更多選項（![更多選項](/help/assets/assets/three-dots.svg)）。

1. 選取&#x200B;**[!UICONTROL 使用OpenAPI啟用重試DM]**&#x200B;以重新啟動啟用。

   ![從環境詳細資訊頁面重試啟動](/help/assets/assets/restart-activation-process-from-list-environment-page.png)

### 設定[!DNL Dynamic Media]解決方案 {#configure-dynamic-media-solutions}

設定[!UICONTROL Dynamic Media]解決方案，以在Cloud Manager中可用的現有或新環境中使用[Dynamic Media搭配OpenAPI](/help/assets/dynamic-media-open-apis-overview.md)的基本和進階功能。

#### 準備開始使用 {#prerequisites-to-configure-dynamic-media-solutions}

確定您有下列專案可設定[!UICONTROL Dynamic Media]解決方案：

1. [存取Cloud Manager](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。
1. 您有[!DNL Dynamic Media] Ultimate授權。

#### 設定[!DNL Dynamic Media]個解決方案以進行資產傳遞 {#configure-dynamic-media-solutions-for-asset-delivery}

執行以下步驟：

1. [建立新程式](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program)或瀏覽至現有的程式，然後按一下&#x200B;**[!UICONTROL 編輯]**。 **[!UICONTROL 為生產設定]**&#x200B;頁面顯示&#x200B;**[!UICONTROL 解決方案和附加元件]**&#x200B;標籤。

1. 選取&#x200B;**[!UICONTROL Assets]**、**[!UICONTROL Assets Prime]**、**[!UICONTROL Assets Ultimate]**&#x200B;或&#x200B;**[!UICONTROL 網站]**，將&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;解決方案新增至您的程式。

1. 選取&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;解決方案，然後按一下&#x200B;**[!UICONTROL 繼續]**，將&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;解決方案新增至您的程式。 此動作會重新啟動您的程式中的所有現有環境，並將[!DNL Dynamic Media]解決方案新增到其中。 此外，您在程式下建立的任何新環境都會自動取得[!DNL Dynamic Media]。

   ![已設定用於生產](/help/assets/assets/set-up-for-prod.png){width="500" align="left"}

請參閱[啟動 [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)以在您的環境中開始使用[!DNL Dynamic Media]與OpenAPI功能的功能。

### 建立並列出[!DNL Dynamic Media]公司 {#create-and-list-dynamic-media-companies}

在您的AEM雲端服務環境中建立並列出[!DNL Dynamic Media]公司，以便在您的AEM環境中管理設定。

#### 準備開始使用 {#prerequisites-to-create-and-list-dynamic-media-companies}

若要在您的IMS組織中檢視現有的公司（帳戶）或新增新的[!DNL Dynamic Media]公司（帳戶），您必須擁有：

1. [存取Cloud Manager](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。

1. 您有[!DNL Dynamic Media] Ultimate授權。

#### 在您的IMS組織中建立並列出[!DNL Dynamic Media]公司 {#create-and-list-dynamic-media-companies-in-your-ims-organisation}

執行這些步驟，建立和列出可在您的[!DNL AEM]環境中設定的新[!DNL Dynamic Media]公司（帳戶）：

1. 瀏覽至[Cloud Manager授權頁面](https://experience-stage.adobe.com/#/@ssahnichstage/cloud-manager/license)。

1. 按一下&#x200B;**[!UICONTROL 新增公司]**，會顯示&#x200B;**[!UICONTROL 建立Dynamic Media公司]**&#x200B;對話方塊。

1. 指定唯一的[!DNL Dynamic Media]公司名稱、選取公司地區並新增以逗號分隔的公司管理員電子郵件ID清單。

   ![建立Dynamic Media公司](/help/assets/assets/create-dynamic-media-company.png){width="500" align="left"}

1. 按一下[建立]&#x200B;**&#x200B;**&#x200B;開始建立您的公司。 此動作將新資料列新增至&#x200B;**[!UICONTROL [!DNL Dynamic Media]公司]**&#x200B;區段，並顯示&#x200B;**[!UICONTROL 正在設定]**&#x200B;為公司的&#x200B;**[!UICONTROL 狀態]**。

   ![已起始Dynamic Media公司建立](/help/assets/assets/dm-company-creation-initiated.png)

1. **選擇性：**&#x200B;按一下![資訊圖示](/help/assets/assets/info-icon-solid-black.svg)以檢視公司的詳細資料。 公司建立時，**[!UICONTROL 狀態]**&#x200B;會更新為&#x200B;**[!UICONTROL 就緒]**。

   ![Dynamic Media公司資訊](/help/assets/assets/dm-company-information.png)

1. 身為Dynamic Media系統管理員，請檢視您的信箱以取得歡迎電子郵件，其中包含在[!DNL AEM] Cloud Service環境中[設定 [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#architecture-diagram-of-dynamic-media)公司的步驟清單，以便開始使用。

   ![歡迎電子郵件](/help/assets/assets/welcome-email.png)

#### 重試公司建立 {#retry-company-creation}

如果[!DNL Dynamic Media]公司建立失敗，請根據失敗狀態執行以下步驟：

1. 如果&#x200B;**[!UICONTROL 狀態]**&#x200B;為「擱置中」，則請向客戶支援團隊提出問題以尋求解決方案。


   ![擱置狀態](/help/assets/assets/company-creation-pending-status.png){width="350" align="center"}



1. 如果&#x200B;**[!UICONTROL 狀態]**&#x200B;失敗，則根據失敗原因重試。

   ![失敗狀態](/help/assets/assets/company-creation-failure-status.png){width="380" align="center"}

### 可選：在傳遞層級中設定自訂網域 {#configure-custom-domain-in-delivery-tier}

雖然AEM as a Cloud Service隨附預設網域，但您可以視需求加以自訂。 使用Cloud Manager將自訂網域附加至傳遞層。

#### 準備開始使用 {#prerequisites-to-configure-custom-domain-in-delivery-tier}

在啟動設定程式之前，請確定您符合下列需求：

1. [存取Cloud Manager](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。
1. [已在您的環境中啟動 [!DNL Dynamic Media with OpenAPI] ](#activate-dynamic-media-with-openapi)。
1. 已啟用[!DNL Dynamic Media with OpenAPI]處於就緒狀態。
1. 用於傳遞層級的網域的EV或OV型別憑證。 如需詳細資訊，請參閱[ SSL憑證簡介](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates)。

#### 使用Cloud Manager在傳遞層級中設定自訂網域 {#configure-custom-domain-in-delivery-tier-using-cloud-manager}

在Cloud Manager中執行以下步驟，在傳送層級中設定自訂網域：

1. [新增客戶管理的SSL憑證](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert)。

1. [新增自訂網域名稱](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings)。

1. 瀏覽到環境詳細資訊頁面，並[新增CDN設定](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/domain-mappings/add-domain-mapping)。 新增設定時，請在&#x200B;**[!UICONTROL 設定CDN]**&#x200B;對話方塊的&#x200B;**[!UICONTROL 層]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 傳遞]**。

   ![設定CDN](/help/assets/assets/select-delivery-tier-in-configure-cdn-form.png)

   新增設定後，**[!UICONTROL CDN設定]**&#x200B;的&#x200B;**[!UICONTROL 狀態]**&#x200B;更新為&#x200B;**[!UICONTROL 已套用]**。

   ![設定CDN部署狀態](/help/assets/assets/cdn-configuration-deployment-status.png)

1. 按一下更多選項（![更多選項](/help/assets/assets/three-dots.svg)）並選取&#x200B;**[!UICONTROL 上線整備]**&#x200B;以顯示&#x200B;**[!UICONTROL 上線整備]**&#x200B;對話方塊。

   ![上線整備選項](/help/assets/assets/go-live-readiness-option.png)

1. 執行&#x200B;**[!UICONTROL 設定CNAME]**&#x200B;步驟以對DNS服務提供者之DNS記錄中的`cdn.adobeaemcloud.com` （CNAME記錄）進行對應。 此對應程式可確保將從自訂網域收到的請求重新導向至Adobe的CDN。

   ![上線整備對話方塊](/help/assets/assets/go-live-readiness-dialogbox.png){width="500" align="left"}

1. 按一下&#x200B;**[!UICONTROL 確定]**，**[!UICONTROL 狀態]**&#x200B;更新為&#x200B;**[!UICONTROL 已驗證]**。 自訂網域已準備好用於傳送URL。


   ![設定CDN](/help/assets/assets/cdn-configurations-varified.png)



<!--
### Onboard API keys {#onboarding-api-keys}

Create an API key to access [!DNL Dynamic Media] with OpenAPIs and the delivery tier backed Asset Selector.

#### Prepare yourself for API keys onboarding process {#prerequisites-for-onboarding-api-keys} 

To start the API keys onboarding process, ensure you have:

1. [Access to Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Activated [!DNL Dynamic Media with OpenAPI] in your environment](#activate-dynamic-media-with-openapi).
1. [Access to the Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#create-adobe-developer-console-adc-project).

#### Onboard the API keys using [!DNL AEM Dynamic Media] API card {#onboarding-api-keys-using-aem-dynamic-media-api-card}

Use the [Adobe Developer Console](https://developer.adobe.com/developer-console/) to onboard the API keys to:

1. [Access Dynamic Media APIs](#access-dynamic-media-apis)
1. [Access Delivery tier backed Asset Selector](#access-delivery-tier-backed-asset-selector)

#### Create an API key to access [!DNL Dynamic Media] with OpenAPIs {#access-dynamic-media-apis}

Execute the following steps to create an API key to access [!DNL Dynamic Media] with OpenAPIs:

1. Navigate to the **[!UICONTROL Admin Console]**. The Admin Console displays the **[!UICONTROL author]**, **[!UICONTROL delivery]** and **[!UICONTROL publish]** instances.
![instances on admin console](/help/assets/assets/delivery-instance-admin-console.png)
1. Select the **[!UICONTROL delivery]** instance to display the product profile with **[!UICONTROL AEM Dynamic Media enable API Services]** enabled by default. The product profile looks like this: **[!UICONTROL AEM Assets DM OpenAPI Users - delivery  - Program [ID Number] - Environment [ID Number]]**. 

   ![product profile on admin console](/help/assets/assets/admin-console-product-profile.png)

   >[!NOTE]
   >
   >This delivery instance is common for [!DNL Content Hub] and [!DNL Dynamic Media] with OpenAPI capabilities.

1. Navigate to the [Adobe Developer console](https://developer.adobe.com/console) and [create a new project](https://developer.adobe.com/dep/guides/dev-console/create-project/). See [Invoke OpenAPI-based AEM APIs for server to server authentication](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) to learn about creating a new project.
1. Select **[!UICONTROL AEM Dynamic Media API]** to access to the [!DNL Dynamic Media with OpenAPI capabilities] and click **[!UICONTROL Next]**.
![adobe developer console](/help/assets/assets/adobe-developer-console.png)
1. Select **[!UICONTROL Server-to-Server Authentication]** and click **[!UICONTROL Next]**. See [Server to Server authentication](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) to learn more about this authentication type.
![server-to-server-authentication](/help/assets/assets/server-to-server-authentication.png)
1. Select **[!UICONTROL OAuth Server-to-Server]**, specify a unique **[!UICONTROL Credential name]** and click **[!UICONTROL Next]**.
![oauth server to server credential](/help/assets/assets/oauth-server-server-and-credential-name.png)
1. Select your product profile (mentioned in step 2) to access the APIs using the environment's delivery endpoint and click **[!UICONTROL Save configured API]**.
![select product profile](/help/assets/assets/select-product-profile.png)
1. Select **[!UICONTROL AEM Dynamic Media API]**. Use the **[!UICONTROL OAuth Server-to-Server]** to fetch the **X-API-key** and access the token for the **authorization** header. 
![oauth server to server](/help/assets/assets/oauth-server-to-server-credentials.png)
Execute the below steps to use [Dynamic Media with OpenAPIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) using the **[!UICONTROL OAuth Server-to-Server]** credentials. 
    1. Copy the **[!UICONTROL API KEY (Client ID)]** and replace the `X-Api-Key` in the cURL.
    1. Click **[!UICONTROL Generate access token]** to generate an access token and replace `YOUR_JWT_HERE` with the token in the cURL.

The cURL looks like this:
```
headers: {
    'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    `},
```
See [Search Assets API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/search-assets-api#search-assets-api-header) for more information.

### Access Delivery tier backed Asset Selector {#access-delivery-tier-backed-asset-selector}

TBD: Wiki in progress..
-->

## 啟用[!DNL Dynamic Media] Prime {#enable-dynamic-media-prime}

若要啟用[!DNL Dynamic Media] Prime：

1. [使用OpenAPI啟動Dynamic Media](#activate-dynamic-media-with-openapi)
1. [選用：設定傳遞層](#configure-custom-domain-in-delivery-tier)中的自訂網域

<!--
1. [Onboard API keys using the AEM Dynamic Media API card](#onboarding-api-keys)
-->
