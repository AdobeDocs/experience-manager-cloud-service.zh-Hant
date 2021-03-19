---
title: '將AEM Assets配置為具有品牌門戶的a [!DNL Cloud Service] '
description: 使用 Brand Portal 設定 AEM Assets.
contentOwner: Vishabh Gupta
feature: 品牌入口網站
role: 管理員
translation-type: tm+mt
source-git-commit: 69c865dbc87ca021443e53b61440faca8fa3c4d4
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 9%

---


# 將AEM Assets配置為[!DNL Cloud Service]和品牌門戶{#configure-aem-assets-with-brand-portal}

設定Adobe Experience Manager資產品牌入口網站可讓您將Adobe Experience Manager資產的已核准品牌資產發佈為[!DNL Cloud Service]例項至品牌入口網站，並將其發佈至品牌入口網站使用者。

## 使用Cloud Manager {#activate-brand-portal}啟用品牌入口網站

Cloud Manager使用者會啟動AEM Assets的品牌入口網站作為[!DNL Cloud Service]例項。 啟動工作流程會在後端建立必要的設定（授權Token、IMS設定和品牌入口雲端服務），並反映Cloud Manager中品牌入口租戶的狀態。 啟用品牌入口網站可讓AEM Assets使用者將資產發佈至品牌入口網站，並將資產分發至品牌入口網站使用者。

**必備條件**

您需要下列項目才能將您AEM Assets的品牌入口網站啟動為[!DNL Cloud Service]實例：

* 以[!DNL Cloud Service]實例啟動並運行AEM Assets。
* 可存取Cloud Manager的使用者，已指派給Cloud Manager產品的設定檔。 如需詳細資訊，請參閱[存取Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#accessing-cloud-manager)。

>[!NOTE]
>
>[!DNL Cloud Service]實例的AEM Assets僅有權與一個品牌入口網站租用戶連接。 您可以將AEM Assets的多個環境（開發、生產和階段）當作[!DNL Cloud Service]實例，其中品牌入口網站在一個環境上啟動。

**啟動品牌入口網站的步驟**

您可以啟動品牌入口網站，同時將AEM Assets的環境建立為[!DNL Cloud Service]例項，或個別建立。 假設環境已建立，您現在必須啟動品牌入口網站。

1. 登入AdobeCloud Manager，並導覽至&#x200B;**[!UICONTROL Environments]**。

   **[!UICONTROL Environments]**&#x200B;頁面會顯示所有現有環境的清單。

1. 從清單中選擇環境（逐個）以查看環境詳細資訊。

   品牌門戶有權使用其中一個可用環境，並反映在&#x200B;**[!UICONTROL 環境資訊]**&#x200B;下。

   找到與品牌入口網站相關的環境後，按一下&#x200B;**[!UICONTROL 啟用品牌入口網站]**&#x200B;按鈕，開始啟動工作流程。

   ![啟動品牌入口網站](assets/create-environment4.png)

1. 啟動工作流程會在後端建立必要的組態時，啟動品牌入口網站租用戶只需幾分鐘。 啟用品牌入口網站租用戶後，狀態會變更為「已啟用」。

   ![檢視狀態](assets/create-environment5.png)


>[!NOTE]
>
>品牌入口網站必須在與AEM Assets相同的IMS組織上啟動為[!DNL Cloud Service]例項。
>
>如果您對IMS組織（組織1-現有）有現有的品牌入口網站雲端設定([使用Adobe開發人員主控台](#manual-configuration)手動設定)，而您的AEM Assets為[!DNL Cloud Service]例項，則會針對其他IMS組織（組織2-新）設定，從雲端管理員啟動品牌入口網站會將品牌入口網站IMS組織重設為`org2-new`。 雖然`org1-existing`上的手動設定雲端設定會顯示在AEM Assets作者例項中，但在從Cloud Manager啟動品牌入口網站後，將不再使用。
>
>如果現有的品牌入口網站雲端設定和[!DNL Cloud Service]例項的AEM Assets使用相同的IMS組織（組織1），您只需從Cloud Manager啟動品牌入口網站。

**另請參閱**:
* [將AEM Assets的用戶和角色添加為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html?lang=en#role-definitions)

* [在Cloud Manager中管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments)


**登入您的品牌入口網站租用戶**:

在Cloud Manager中啟動您的品牌入口網站租用戶後，您可以從Admin Console或直接使用租用戶URL登入品牌入口網站。

您的品牌入口網站租用戶的預設URL為：`https://<tenant-id>.brand-portal.adobe.com/`。

其中，租用戶ID為IMS組織。

如果您不確定品牌入口網站URL，請執行下列步驟：

1. 登入[Admin Console](http://adminconsole.adobe.com/)並導覽至&#x200B;**[!UICONTROL 產品]**。
1. 從左側導軌中，選擇&#x200B;**[!UICONTROL Adobe Experience Manager品牌入口網站——品牌入口網站]**。
1. 按一下&#x200B;**[!UICONTROL 前往品牌入口網站]**，直接在瀏覽器中開啟品牌入口網站。

   或者，從&#x200B;**[!UICONTROL 前往品牌入口網站]**&#x200B;連結複製品牌入口網站URL，並貼到您的瀏覽器中以開啟品牌入口網站介面。

   ![存取品牌入口網站](assets/access-bp-on-cloud.png)


**測試連線**

執行下列步驟以驗證您的AEM Assets作為[!DNL Cloud Service]實例與品牌入口網站租用戶之間的連接：

1. 登入AEM Assets。

1. 從&#x200B;**工具**&#x200B;面板，導航至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 分發]**。

   ![](assets/test-bpconfig1.png)

   在&#x200B;**[!UICONTROL 發佈到品牌門戶]**&#x200B;下建立品牌門戶分發代理(**[!UICONTROL bpdistributionagent0]**)。

   ![](assets/test-bpconfig2.png)


1. 按一下「發佈至品牌入口網站」，以開啟散發代理。****

   您可以在&#x200B;**[!UICONTROL Status]**&#x200B;標籤下看到分佈隊列。

   發佈代理程式包含兩個佇列：
   * **processing-queue**:將資產分發至品牌入口網站。

   * **error-queue**:對於分發失敗的資產。
   >[!NOTE]
   >
   >建議定期檢查故障並清除&#x200B;**error-queue**。

   ![](assets/test-bpconfig3.png)

1. 要驗證作為[!DNL Cloud Service]和品牌門戶的AEM Assets之間的連接，請按一下&#x200B;**[!UICONTROL 測試連接]**&#x200B;表徵圖。

   ![](assets/test-bpconfig4.png)

   出現一條消息，表示&#x200B;*測試包已成功交付*。

   >[!NOTE]
   >
   >請避免停用發佈代理程式，因為可能導致在佇列中執行的資產發佈失敗。

若要確認您的AEM Assets（[!DNL Cloud Service]實例）與品牌入口網站租用戶之間的連接，請從AEM Assets發佈資產至品牌入口網站。 如果連線成功，發佈的資產會顯示在品牌入口網站介面中。


您現在可以：

* [從 AEM Assets 發佈資產到 Brand Portal](publish-to-brand-portal.md)
* [從 AEM Assets 發佈資料夾到 Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [從 AEM Assets 發佈集合到 Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [將資產從品牌入口網站發佈至AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en) -品牌入口網站中的資產來源補充
* [將預設集、結構和 Facet 發佈至 Brand Portal](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

如需詳細資訊，請參閱[品牌入口網站檔案](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/home.html)。

**發佈記錄檔**

您可以監視資產發佈工作流程的散發代理記錄檔。

現在，讓我們將資產從AEM Assets發佈至品牌入口網站，並查看記錄檔。

1. 按照&#x200B;**測試連接**&#x200B;部分中顯示的步驟（從1到4），導航到分發代理頁面。
1. 按一下&#x200B;**[!UICONTROL 日誌]**&#x200B;查看處理和錯誤日誌。

   ![](assets/test-bpconfig5.png)

分發代理已生成以下日誌：

* 資訊：它是系統生成的日誌，在成功配置分發代理時觸發。
* DSTRQ1（請求1）:測試連線時的觸發器。

發佈資產時，會產生下列請求和回應記錄檔：

**發佈代理程式請求**：

* DSTRQ2 (請求 2)：觸發資產發佈請求。
* DSTRQ3（請求3）:系統會觸發另一個請求，以發佈AEM Assets資料夾（資產存在於其中）並複製品牌入口網站中的資料夾。

**發佈代理程式回應**：

* queue-bpdistributionagent0 (DSTRQ2)：資產已發佈至 Brand Portal。
* queue-bpdistributionagent0(DSTRQ3):系統會複製品牌入口網站中的AEM Assets資料夾（包含資產）。

在上述範例中，會觸發額外的請求和回應。 系統無法在品牌入口網站中找到父資料夾（新增路徑），因為資產是第一次發佈，因此會觸發額外請求，在發佈資產的品牌入口網站中建立同名的父資料夾。

>[!NOTE]
>
>當父資料夾不存在於Brand Portal中或已修改於AEM Assets時，會產生其他請求。

除了以[!DNL Cloud Service]啟動AEM Assets的品牌入口網站的自動化工作流程外，還有另一種方法可使用Adobe開發人員主控台手動將AEM Assets設定為[!DNL Cloud Service]品牌入口網站，這已不再建議使用。

>[!NOTE]
>
>如果您在啟動品牌入口網站租用戶時遇到任何問題，請連絡Adobe支援。

## 使用Adobe開發人員控制台{#manual-configuration}進行手動配置

下節說明如何使用Adobe開發人員主控台手動將AEM Assets設為[!DNL Cloud Service]品牌入口網站。

之前，AEM Assets是[!DNL Cloud Service]透過Adobe開發人員主控台手動設定品牌入口網站，該主控台會購買AdobeIdentity Management服務(IMS)帳戶代號以授權品牌入口網站租戶。 它需要在AEM Assets和Adobe開發人員主控台中進行配置。

1. 在AEM Assets，建立IMS帳戶並產生公開金鑰（憑證）。
1. 在Adobe開發人員主控台中，為您的品牌入口網站租用戶（組織）建立專案。
1. 在專案下，使用公開金鑰來設定API，以建立服務帳戶連線。
1. 取得服務帳戶認證和JSON Web Token(JWT)裝載資訊。
1. 在AEM Assets，使用服務帳戶憑證和JWT裝載來設定IMS帳戶。
1. 在AEM Assets，使用IMS帳戶和品牌入口端端點（組織URL）來設定品牌入口網站雲端服務。
1. 將資產從AEM Assets發佈至品牌入口網站，以測試您的設定。

>[!NOTE]
>
>作為[!DNL Cloud Service]實例的AEM Assets僅應配置一個品牌門戶租戶。

**必備條件**

您需要下列項目才能使用 Brand Portal 設定 AEM Assets：

* 啟動並運行AEM Assets作為[!DNL Cloud Service]實例
* 品牌入口網站租用戶URL
* 對品牌入口網站的IMS組織具有系統管理員權限的使用者

## 建立設定 {#create-new-configuration}

在指定的序列中執行下列步驟，以使用品牌入口網站配置AEM Assets。

1. [取得公開憑證](#public-certificate)
1. [建立服務帳戶(JWT)連接](#createnewintegration)
1. [設定IMS帳戶](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)

### 建立 IMS 設定 {#create-ims-configuration}

IMS設定會將您的AEM Assets驗證為品牌入口網站的[!DNL Cloud Service]實例。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [設定IMS帳戶](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開金鑰（憑證）會在Adobe開發人員主控台上驗證您的個人檔案。

1. 登入AEM Assets。
1. 從&#x200B;**工具**&#x200B;面板，瀏覽至&#x200B;**[!UICONTROL 安全]** > **[!UICONTROL AdobeIMS配置]**。
1. 在「AdobeIMS配置」頁中，按一下&#x200B;**[!UICONTROL 建立]**。 它將重定向至「**[!UICONTROL AdobeIMS技術帳戶配置]**」頁。 預設情況下，**Certificate**&#x200B;頁籤開啟。
1. 在&#x200B;**[!UICONTROL 雲端解決方案]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL Adobe品牌入口網站]**。
1. 選擇「建立新證書」複選框，並為公鑰指定&#x200B;**別名**。 ****&#x200B;別名用作公共密鑰的名稱。
1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。然後，按一下&#x200B;**[!UICONTROL OK]**&#x200B;以生成公鑰。

   ![建立憑證](assets/ims-config2.png)

1. 按一下&#x200B;**[!UICONTROL 下載公開密鑰]**&#x200B;表徵圖，並將公開密鑰(CRT)檔案保存在電腦上。

   公開金鑰稍後會用來為您的品牌入口網站租用戶設定API，並在Adobe開發人員主控台中產生服務帳戶認證。

   ![下載憑證](assets/ims-config3.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**Account**&#x200B;標籤中，建立AdobeIMS帳戶，此帳戶需要在Adobe開發人員主控台中產生的服務帳戶認證。 暫時保持此頁面開啟。

   開啟新標籤，並在Adobe開發人員主控台(Developer Console)中建立服務帳戶(JWT)連線，以取得用於設定IMS帳戶的認證和JWT裝載。[](#createnewintegration)

### 建立服務帳戶(JWT)連接{#createnewintegration}

在Adobe開發人員主控台中，專案和API是在品牌入口網站租用戶（組織）層級設定。 配置API會建立服務帳戶(JWT)連接。 有兩種方法可用來設定API：產生金鑰對（私用和公開金鑰）或上傳公開金鑰。 若要使用品牌入口網站來設定AEM Assets，您必須在AEM Assets產生公開金鑰（憑證），並上傳公開金鑰以在Adobe開發人員主控台中建立認證。 必須有這些認證才能在AEM Assets設定IMS帳戶。 一旦設定IMS帳戶後，您就可以在AEM Assets設定品牌入口網站雲端服務。

執行以下步驟以生成服務帳戶憑據和JWT裝載：

1. 以IMS組織（品牌入口租戶）的系統管理員權限登入Adobe開發人員主控台。 預設URL為[https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   >[!NOTE]
   >
   >請確定您已從右上角的下拉式（組織）清單中選取正確的IMS組織（品牌入口網站租用戶）。

1. 按一下&#x200B;**[!UICONTROL 建立新項目]**。 系統會為您的組織建立空白專案，其名稱由系統產生。

   按一下&#x200B;**[!UICONTROL 編輯項目]**&#x200B;以更新&#x200B;**[!UICONTROL 項目標題]**&#x200B;和&#x200B;**[!UICONTROL 說明]**，然後按一下&#x200B;**[!UICONTROL 保存]**。

1. 在&#x200B;**[!UICONTROL Project overview]**&#x200B;標籤中，按一下&#x200B;**[!UICONTROL Add API]**。

1. 在&#x200B;**[!UICONTROL 新增API視窗]**&#x200B;中，選擇&#x200B;**[!UICONTROL AEM品牌入口網站]**，然後按一下&#x200B;**[!UICONTROL Next]**。

   確保您擁有品牌入口網站AEM服務的存取權。

1. 在&#x200B;**[!UICONTROL 配置API]**&#x200B;窗口中，按一下&#x200B;**[!UICONTROL 上傳公開密鑰]**。 然後，按一下「**[!UICONTROL 選擇檔案]**」並上傳您在[獲取公共證書](#public-certificate)部分中下載的公開密鑰（.crt檔案）。

   按一下&#x200B;**[!UICONTROL 下一步]**。

   ![上傳公開金鑰](assets/service-account3.png)

1. 驗證公鑰，然後按一下&#x200B;**[!UICONTROL Next]**。

1. 選擇&#x200B;**[!UICONTROL Assets Brand Portal]**&#x200B;作為預設產品配置檔案，然後按一下&#x200B;**[!UICONTROL Save configured API]**。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![選擇產品設定檔](assets/service-account4.png)

1. 一旦設定API後，就會將您重新導向至API概觀頁面。 在&#x200B;**[!UICONTROL Credentials]**&#x200B;下的左側導航中，按一下&#x200B;**[!UICONTROL 服務帳戶(JWT)]**&#x200B;選項。

   >[!NOTE]
   >
   >您可以查看憑據並執行諸如生成JWT Token、複製憑據詳細資訊、檢索客戶機密碼等操作。

1. 從&#x200B;**[!UICONTROL 客戶端憑據]**&#x200B;頁籤複製&#x200B;**[!UICONTROL 客戶端ID]**。

   按一下「檢索客戶機密碼」**[!UICONTROL 並複製**[!UICONTROL &#x200B;客戶機密碼&#x200B;]**。]**

   ![服務帳戶認證](assets/service-account5.png)

1. 導航至「生成JWT ]**」頁籤並複製**[!UICONTROL  JWT Payload ]**資訊。**[!UICONTROL 

您現在可以使用用戶端ID（API金鑰）、用戶端密碼和JWT裝載至[，在AEM Assets設定IMS帳戶](#create-ims-account-configuration)。

<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.

-->

### 設定IMS帳戶{#create-ims-account-configuration}

請確認您已執行下列步驟：

* [取得公開憑證](#public-certificate)
* [建立服務帳戶(JWT)連接](#createnewintegration)

執行下列步驟以設定IMS帳戶。

1. 開啟IMS設定並導覽至&#x200B;**[!UICONTROL Account]**&#x200B;標籤。 在[取得公共憑證時，您會保持頁面開啟。](#public-certificate)

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在&#x200B;**[!UICONTROL 授權伺服器]**&#x200B;欄位中，指定URL:[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   在[建立服務帳戶(JWT)連線](#createnewintegration)時，在&#x200B;**[!UICONTROL API金鑰]**&#x200B;欄位、**[!UICONTROL 客戶機密碼]**&#x200B;和&#x200B;**[!UICONTROL Payload]**（JWT有效載荷）中指定您複製的用戶端ID。

   按一下&#x200B;**[!UICONTROL 建立]**。

   已設定IMS帳戶。

   ![IMS 帳戶設定](assets/create-new-integration6.png)


1. 選擇IMS帳戶配置，然後按一下&#x200B;**[!UICONTROL 檢查運行狀況]**。

   在對話框中按一下「**[!UICONTROL 檢查]**」。 成功配置時，將顯示一條消息，表示&#x200B;*Token已成功檢索*。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一個IMS設定。
>
>確保IMS配置通過健康檢查。 如果配置未通過健康檢查，則無效。 您必須刪除它並建立新的有效設定。

### 設定雲端服務 {#configure-the-cloud-service}

執行下列步驟以設定品牌入口網站雲端服務：

1. 登入AEM Assets。

1. 從&#x200B;**工具**&#x200B;面板，導覽至&#x200B;**[!UICONTROL Cloud Services]** > **[!UICONTROL 品AEM牌入口網站]**。

1. 在「品牌入口網站設定」頁面中，按一下「建立&#x200B;**[!UICONTROL 」。]**

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選擇您在[設定IMS帳戶](#create-ims-account-configuration)時建立的IMS設定。

   在&#x200B;**[!UICONTROL 服務URL]**&#x200B;欄位中，指定您的品牌入口網站租用戶（組織）URL。

   ![](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。雲端設定此時已建立。

   您的[!DNL Cloud Service]例項AEM Assets現在已設定為品牌入口網站租用戶。

您現在可以檢查散發代理並將資產發佈至品牌入口網站，以測試設定。

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Log in to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click on the **[!UICONTROL Test Connection]** icon.

   ![](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![](assets/test-bpconfig5.png)

The distribution agent has generated the following logs:

* INFO: This is a system-generated log that triggers on successful configuration of the distribution agent. 
* DSTRQ1 (Request 1): Triggers on test connection.

On publishing the asset, the following request and response logs are generated:

**Distribution agent request**:

* DSTRQ2 (Request 2): The asset publishing request is triggered.
* DSTRQ3 (Request 3): The system triggers another request to publish the AEM Assets folder (in which the asset exists) and replicates the folder in Brand Portal.

**Distribution agent response**:

* queue-bpdistributionagent0 (DSTRQ2): The asset is published to Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): The system replicates the AEM Assets folder (containing the asset) in Brand Portal.

In the above example, an additional request and response is triggered. The system could not find the parent folder (Add Path) in Brand Portal because the asset was published for the first time, therefore, it triggered an additional request to create a parent folder with the same name in Brand Portal where the asset is published.  

>[!NOTE]
>
>Additional request is generated in case the parent folder does not exist in Brand Portal or has been modified in AEM Assets. 
-->

<!--

## Additional information {#additional-information}

Go to `/system/console/slingmetrics` for statistics related to the distributed content:

1. **Counter metrics**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Time metrics**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`

-->

<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
-->
