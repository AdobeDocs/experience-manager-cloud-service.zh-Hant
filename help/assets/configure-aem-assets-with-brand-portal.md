---
title: 使用品牌入口網站將AEM資產設定為雲端服務
description: 使用 Brand Portal 設定 AEM Assets.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 5da0d4cc8c6d8781dd7cce8bbbde207568a6d10b
workflow-type: tm+mt
source-wordcount: '1647'
ht-degree: 14%

---


# 將AEM Assets設定為具有品牌入口網站{#configure-aem-assets-with-brand-portal}的雲端服務

設定Adobe Experience Manager Assets Brand Portal可讓您將Adobe Experience Manager Assets中經過核准的品牌資產發佈為雲端服務例項至品牌入口網站，並將其分發給品牌入口網站使用者。

**設定工作流程**

AEM Assets as a Cloud Service是透過Adobe Developer Console設定品牌入口網站，該網站會購買Adobe Identity Management Services(IMS)帳戶代號以授權品牌入口網站租戶。 這需要AEM Assets和Adobe Developer Console中的設定。

1. 在AEM Assets中，建立IMS帳戶並產生公開金鑰（憑證）。
1. 在Adobe Developer Console中，為您的品牌入口網站租用戶（組織）建立專案。
1. 在專案下，使用公開金鑰來設定API，以建立服務帳戶連線。
1. 取得服務帳戶認證和JSON Web Token(JWT)裝載資訊。
1. 在AEM Assets中，使用服務帳戶認證和JWT裝載來設定IMS帳戶。
1. 在AEM Assets中，使用IMS帳戶和品牌入口端端點（組織URL）來設定品牌入口網站雲端服務。
1. 將資產從AEM Assets發佈至品牌入口網站，以測試您的設定。

>[!NOTE]
>
>AEM Assets做為Cloud Service例項時，只能設定一個Brand Portal租用戶。

## 必備條件 {#prerequisites}

您需要下列項目才能使用 Brand Portal 設定 AEM Assets：

* 以雲端服務實例啟動並執行AEM Assets
* 品牌入口網站租用戶URL
* 對品牌入口網站的IMS組織具有系統管理員權限的使用者

## 建立設定 {#create-new-configuration}

在指定的序列中執行下列步驟，以設定具有品牌入口網站的AEM資產。

1. [取得公開憑證](#public-certificate)
1. [建立服務帳戶(JWT)連接](#createnewintegration)
1. [設定IMS帳戶](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)
1. [測試設定](#test-configuration)

### 建立 IMS 設定 {#create-ims-configuration}

IMS設定會以Brand Portal租用戶的雲端服務例項驗證您的AEM資產。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [設定IMS帳戶](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開金鑰（憑證）會在Adobe Developer Console上驗證您的個人檔案。

1. 登入AEM Assets。
1. 從&#x200B;**工具**&#x200B;面板，導覽至&#x200B;**[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**。
1. 在「Adobe IMS設定」頁面中，按一下「**[!UICONTROL 建立]**」。 它會重新導向至&#x200B;**[!UICONTROL Adobe IMS技術帳戶設定]**&#x200B;頁面。 預設情況下，**Certificate**&#x200B;頁籤開啟。
1. 在&#x200B;**[!UICONTROL 雲端解決方案]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL Adobe品牌入口網站]**。
1. 選擇「建立新證書」複選框，並為公鑰指定&#x200B;**[!UICONTROL 別名]**。 ****&#x200B;別名用作公共密鑰的名稱。
1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。然後，按一下&#x200B;**[!UICONTROL OK]**&#x200B;以生成公鑰。

   ![建立憑證](assets/ims-config2.png)

1. 按一下「下載公開金鑰」圖示，並將公開金鑰(.crt)檔案儲存在您的電腦上。****

   公開金鑰稍後將用於為您的品牌入口網站租用戶設定API，並在Adobe Developer Console中產生服務帳戶認證。

   ![下載憑證](assets/ims-config3.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**Account**&#x200B;標籤中，會建立Adobe IMS帳戶，此帳戶需要Adobe Developer Console中產生的服務帳戶認證。 暫時保持此頁面開啟。

   在Adobe Developer Console[中開啟新標籤並建立服務帳戶(JWT)連線，以取得用於設定IMS帳戶的認證和JWT裝載。](#createnewintegration)

### 建立服務帳戶(JWT)連接{#createnewintegration}

在Adobe Developer Console中，專案和API是在品牌入口網站租用戶（組織）層級設定。 配置API會建立服務帳戶(JWT)連接。 有兩種方法可用來設定API：產生金鑰對（私用和公開金鑰）或上傳公開金鑰。 若要使用品牌入口網站設定AEM資產，您必須在AEM資產中產生公開金鑰（憑證），並透過上傳公開金鑰在Adobe Developer Console中建立認證。 在AEM資產中設定IMS帳戶時，需要這些認證。 在設定IMS帳戶後，您就可以在AEM Assets中設定品牌入口網站雲端服務。

執行以下步驟以生成服務帳戶憑據和JWT裝載：

1. 以IMS組織（品牌入口網站租用戶）的系統管理員權限登入Adobe Developer Console。 預設URL為[https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   >[!NOTE]
   >
   >請確定您已從右上角的下拉式（組織）清單中選取正確的IMS組織（品牌入口網站租用戶）。

1. 按一下&#x200B;**[!UICONTROL 建立新項目]**。 系統會為您的組織建立空白專案，其名稱由系統產生。

   按一下&#x200B;**[!UICONTROL 編輯項目]**&#x200B;以更新&#x200B;**[!UICONTROL 項目標題]**&#x200B;和&#x200B;**[!UICONTROL 說明]**，然後按一下&#x200B;**[!UICONTROL 保存]**。

1. 在&#x200B;**[!UICONTROL Project overview]**&#x200B;標籤中，按一下&#x200B;**[!UICONTROL Add API]**。

1. 在&#x200B;**[!UICONTROL 新增API視窗]**&#x200B;中，選取&#x200B;**[!UICONTROL AEM品牌入口網站]**，然後按一下&#x200B;**[!UICONTROL Next]**。

   請確定您擁有AEM品牌入口網站服務的存取權。

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

您現在可以使用用戶端ID（API金鑰）、用戶端密碼和JWT裝載至[，在AEM資產中設定IMS帳戶](#create-ims-account-configuration)。

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

1. 從&#x200B;**工具**&#x200B;面板，導覽至&#x200B;**[!UICONTROL 雲端服務]** > **[!UICONTROL AEM品牌入口網站]**。

1. 在「品牌入口網站設定」頁面中，按一下「建立&#x200B;**[!UICONTROL 」。]**

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選擇您在[設定IMS帳戶](#create-ims-account-configuration)時建立的IMS設定。

   在&#x200B;**[!UICONTROL 服務URL]**&#x200B;欄位中，指定您的品牌入口網站租用戶（組織）URL。

   ![](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。雲端設定此時已建立。

   您的AEM Assets as a Cloud Service例項現在已設定品牌入口網站租用戶。

### 測試設定 {#test-configuration}

執行以下步驟以驗證配置：

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

1. 若要驗證AEM Assets作為雲端服務與品牌入口網站的連線，請按一下&#x200B;**[!UICONTROL Test Connection]**&#x200B;圖示。

   ![](assets/test-bpconfig4.png)

   出現一條消息，表示&#x200B;*測試包已成功交付*。

   >[!NOTE]
   >
   >請避免停用發佈代理程式，因為可能導致在佇列中執行的資產發佈失敗。

您現在可以：

* [從 AEM Assets 發佈資產到 Brand Portal](publish-to-brand-portal.md)
* [從 AEM Assets 發佈資料夾到 Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [從 AEM Assets 發佈集合到 Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [將預設集、結構和 Facet 發佈至 Brand Portal](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

如需詳細資訊，請參閱[品牌入口網站檔案](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/home.html)。

## 發佈記錄檔 {#distribution-logs}

您可以監視資產發佈工作流程的散發代理記錄檔。

例如，我們已將資產從AEM Assets發佈至品牌入口網站，以驗證設定。

1. 按照[測試配置](#test-configuration)部分中顯示的步驟（從1到4），導航到分發代理頁面。
1. 按一下&#x200B;**[!UICONTROL 日誌]**&#x200B;查看處理和錯誤日誌。

   ![](assets/test-bpconfig5.png)

分發代理已生成以下日誌：

* 資訊：這是系統生成的日誌，在成功配置分發代理時觸發。
* DSTRQ1（請求1）:測試連線時的觸發器。

發佈資產時，會產生下列請求和回應記錄檔：

**發佈代理程式請求**：

* DSTRQ2 (請求 2)：觸發資產發佈請求。
* DSTRQ3（請求3）:系統會觸發另一個請求，以發佈AEM Assets檔案夾（資產存在其中）並複製品牌入口網站中的檔案夾。

**發佈代理程式回應**：

* queue-bpdistributionagent0 (DSTRQ2)：資產已發佈至 Brand Portal。
* queue-bpdistributionagent0(DSTRQ3):系統會複製品牌入口網站中的「AEM資產」檔案夾（包含資產）。

在上述範例中，系統會觸發其他請求和回應。系統無法在品牌入口網站中找到父資料夾（新增路徑），因為資產是第一次發佈，因此會觸發額外請求，在發佈資產的品牌入口網站中建立同名的父資料夾。

>[!NOTE]
>
>當父資料夾不存在於品牌入口網站中或已在AEM Assets中修改時，會產生其他請求。

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
