---
title: 將AEM Assets設定為 [!DNL Cloud Service] 搭配Brand Portal
description: 使用 Brand Portal 設定 AEM Assets.
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution,Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: 54057d6b5563de3455dddb7866c7c93a3b0294ec
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 7%

---

# 透過 Brand Portal 設定 Experience Manager Assets {#configure-aem-assets-with-brand-portal}

設定Adobe Experience Manager Assets Brand Portal可讓您從Adobe Experience Manager Assets發佈核准的品牌資產，作為 [!DNL Cloud Service] 例項，並將其分發給Brand Portal使用者。

## 使用Cloud Manager啟用Brand Portal {#activate-brand-portal}

Cloud Manager使用者會為Experience Manager Assets as a [!DNL Cloud Service] 例項。 啟動工作流程會在後端建立必要的設定(授權Token、IMS設定和Brand Portal雲端服務)，並反映Cloud Manager中Brand Portal租用戶的狀態。 啟用Brand Portal可讓Experience Manager Assets使用者將資產發佈至Brand Portal，並分發給Brand Portal使用者。

**必備條件**

您需要下列項目，才能在您的Experience Manager Assets上啟用Brand Portal，作為 [!DNL Cloud Service] 例項：

* 正在運作的Experience Manager Assets as a [!DNL Cloud Service] 例項。
* 有權存取Cloud Manager的使用者，已指派給Cloud Manager產品的設定檔。 請參閱 [存取Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager) 以取得更多資訊。

>[!NOTE]
>
>Experience Manager Assets as a [!DNL Cloud Service] 與Brand Portal租用戶連線的例項。

**啟動Brand Portal的步驟**

您可以在為Experience Manager Assets as建立生產環境時啟用Brand Portal [!DNL Cloud Service] 例項，或個別。 假設環境已建立，您現在必須啟用Brand Portal。

1. 登入AdobeCloud Manager並導覽至 **[!UICONTROL 環境]**.

   此 **[!UICONTROL 環境]** 頁面會顯示所有現有環境的清單。

1. 從清單中選取環境（逐一）以檢視環境詳細資訊。

   Brand Portal有權使用其中一個可用環境，並反映於 **[!UICONTROL 環境資訊]**.

   找到與Brand Portal相關聯的環境後，按一下 **[!UICONTROL 啟用Brand Portal]** 按鈕，開始啟動工作流程。

   ![啟用Brand Portal](assets/create-environment4.png)

1. 啟動工作流程會在後端建立必要的設定時，啟動Brand Portal租用戶需要幾分鐘的時間。 啟動Brand Portal租用戶後，狀態會變更為「已啟動」。

   ![檢視狀態](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal必須在與Experience Manager Assets相同的IMS組織上啟動，如同 [!DNL Cloud Service] 例項。
>
>如果您有現有的Brand Portal雲端設定([使用Adobe Developer Console手動設定](#manual-configuration))(適用於IMS組織(org1-existing)，而您的Experience Manager Assets as a [!DNL Cloud Service] 例項已設定供其他IMS組織(org2-new)使用，從Cloud manager啟用Brand Portal會將Brand Portal IMS組織重設為 `org2-new`. 雖然在上手動設定雲端設定 `org1-existing` 會顯示在Experience Manager Assets製作例項中，但從Cloud Manager啟動Brand Portal後，將不再使用。
>
>如果現有的Brand Portal雲端設定和Experience Manager Assets as a [!DNL Cloud Service] 執行個體使用相同的IMS組織(org1)，您只需從Cloud Manager啟用Brand Portal即可。
>
>請勿修改任何自動產生的設定。

**另請參閱**:

* [在Experience Manager Assets as a Cloud Service中新增使用者和角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [在Cloud Manager中管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**登入Brand Portal租用戶**:

在Cloud Manager中啟用Brand Portal租用戶後，您可以從Admin Console或直接使用租用戶URL登入Brand Portal。

Brand Portal租用戶的預設URL為： `https://<tenant-id>.brand-portal.adobe.com/`.

其中，租用戶ID為IMS組織。

如果您不確定Brand Portal URL，請執行下列步驟：

1. 登入 [Admin Console](https://adminconsole.adobe.com/) 並導覽至 **[!UICONTROL 產品]**.
1. 從左側面板中，選取 **[!UICONTROL Adobe Experience Manager Brand Portal -Brand Portal]**.
1. 按一下 **[!UICONTROL 前往Brand Portal]** 直接在瀏覽器中開啟Brand Portal。

   或從 **[!UICONTROL 前往Brand Portal]** 連結並貼到您的瀏覽器中，以開啟Brand Portal介面。

   ![存取Brand Portal](assets/access-bp-on-cloud.png)


**測試連接**

執行下列步驟來驗證Experience Manager Assets與 [!DNL Cloud Service] 例項和Brand Portal租用戶：

1. 登入Experience Manager Assets。

1. 從 **工具** 面板，導覽至 **[!UICONTROL 部署]** > **[!UICONTROL 分發]**.

   ![](assets/test-bpconfig1.png)

   Brand Portal發佈代理(**[!UICONTROL bpdistributionagent0]**)建立於 **[!UICONTROL 發佈至Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. 按一下 **[!UICONTROL 發佈至Brand Portal]** 來開啟發佈代理程式。

   您可以在 **[!UICONTROL 狀態]** 標籤。

   發佈代理程式包含兩個佇列：
   * **處理佇列**:將資產分配給Brand Portal。

   * **error-queue**:針對發佈失敗的資產。
   >[!NOTE]
   >
   >建議您檢閱失敗，並清除 **error-queue** 定期。

   ![](assets/test-bpconfig3.png)

1. 驗證Experience Manager Assets與 [!DNL Cloud Service] 和Brand Portal，按一下 **[!UICONTROL 測試連線]** 表徵圖。

   ![](assets/test-bpconfig4.png)

   系統會顯示訊息，指出您的 *已成功傳遞測試包*.

   >[!NOTE]
   >
   >請避免停用發佈代理程式，因為可能導致在佇列中執行的資產發佈失敗。

驗證Experience Manager Assets與 [!DNL Cloud Service] 例項和Brand Portal租用戶，將資產從Experience Manager Assets發佈至Brand Portal。 如果連線成功，已發佈的資產會顯示在Brand Portal介面中。


您現在可以：

* [從Experience Manager Assets發佈資產至Brand Portal](publish-to-brand-portal.md)
* [將資料夾從Experience Manager Assets發佈至Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [從Experience Manager Assets發佈集合到Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [從Brand Portal發佈資產至Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) -Brand Portal的Asset Sourcing
* [將預設集、結構和 Facet 發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

請參閱 [Brand Portal檔案](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 以取得更多資訊。

**發佈記錄檔**

您可以監視資產發佈工作流程的發佈代理程式記錄檔。

現在讓我們將資產從Experience Manager Assets發佈至Brand Portal並查看日誌。

1. 請依照 **測試連接** 區段，並導覽至發佈代理程式頁面。
1. 按一下 **[!UICONTROL 記錄檔]** 檢視處理和錯誤記錄。

   ![](assets/test-bpconfig5.png)

發佈代理程式已產生下列記錄檔：

* 資訊：這是系統產生的記錄檔，會在成功設定發佈代理時觸發。
* DSTRQ1（請求1）:測試連線時觸發。

發佈資產時，會產生下列請求和回應記錄檔：

**發佈代理程式請求**：

* DSTRQ2 (請求 2)：觸發資產發佈請求。
* DSTRQ3（請求3）:系統會觸發另一個請求以發佈Experience Manager Assets資料夾（資產存在其中）並複製Brand Portal中的資料夾。

**發佈代理程式回應**：

* queue-bpdistributionagent0 (DSTRQ2)：資產已發佈至 Brand Portal。
* queue-bpdistributionagent0(DSTRQ3):系統會複製Brand Portal中的Experience Manager Assets資料夾（包含資產）。

在上述範例中，會觸發其他請求和回應。 系統在Brand Portal中找不到父資料夾（新增路徑），因為資產是首次發佈，因此會觸發其他請求，在發佈資產的Brand Portal中建立同名的父資料夾。

>[!NOTE]
>
>如果父資料夾不存在於Brand Portal中或已在Experience Manager Assets中修改，則會產生其他請求。

連同在Experience Manager Assets as a [!DNL Cloud Service]，則有其他方法可手動設定Experience Manager Assets as a [!DNL Cloud Service] 搭配Brand Portal使用Adobe Developer Console，我們不再建議使用。

>[!NOTE]
>
>如果您在啟用Brand Portal租用戶時遇到任何問題，請聯絡客戶支援。

## 使用Adobe Developer Console手動設定 {#manual-configuration}

以下章節說明如何手動將Experience Manager Assets設定為 [!DNL Cloud Service] 搭配Brand Portal使用Adobe Developer Console。

之前，Experience Manager Assets [!DNL Cloud Service] 是透過Adobe Developer Console以Brand Portal手動設定，其會擷取AdobeIdentity Management服務(IMS)帳戶代號，以授權Brand Portal租用戶。 這需要Experience Manager Assets和Adobe Developer Console中的設定。

1. 在Experience Manager Assets中，建立IMS帳戶並產生公開金鑰（憑證）。
1. 在Adobe Developer Console中，為您的Brand Portal租用戶（組織）建立專案。
1. 在專案下，使用公開金鑰設定API以建立服務帳戶連線。
1. 取得服務帳戶認證和JSON網頁代號(JWT)裝載資訊。
1. 在Experience Manager Assets中，使用服務帳戶憑證和JWT裝載來設定IMS帳戶。
1. 在Experience Manager Assets中，使用IMS帳戶和Brand Portal端點（組織URL）來設定Brand Portal雲端服務。
1. 將資產從Experience Manager Assets發佈至Brand Portal，以測試您的設定。

>[!NOTE]
>
>Experience Manager Assets as a [!DNL Cloud Service] 執行個體只能設定一個Brand Portal租用戶。

**必備條件**

您需要下列項目才能使用Brand Portal設定Experience Manager Assets:

* 正在運作的Experience Manager Assets as a [!DNL Cloud Service] 執行個體
* Brand Portal租用戶URL
* 在Brand Portal租用戶的IMS組織上具有系統管理員權限的使用者

## 建立設定 {#create-new-configuration}

以指定順序執行下列步驟，使用Brand Portal設定Experience Manager Assets。

1. [取得公開憑證](#public-certificate)
1. [建立服務帳戶(JWT)連線](#createnewintegration)
1. [設定IMS帳戶](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)

### 建立 IMS 設定 {#create-ims-configuration}

IMS設定會驗證您的Experience Manager Assets，作為 [!DNL Cloud Service] 例項(與Brand Portal租用戶)。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [設定IMS帳戶](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開金鑰（憑證）在Adobe Developer Console上驗證您的設定檔。

1. 登入Experience Manager Assets。
1. 從 **工具** 面板，導覽至 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**.
1. 在Adobe IMS設定頁面中，按一下 **[!UICONTROL 建立]**. 它會重新導向至 **[!UICONTROL Adobe IMS技術帳戶設定]** 頁面。 依預設， **憑證** 標籤。
1. 選擇 **[!UICONTROL AdobeBrand Portal]** 在 **[!UICONTROL 雲端解決方案]** 下拉式清單。
1. 選取 **[!UICONTROL 建立新憑證]** 核取方塊並指定 **別名** 公開金鑰。 別名用作公鑰的名稱。
1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。然後，按一下 **[!UICONTROL 確定]** 來產生公開金鑰。

   ![建立憑證](assets/ims-config2.png)

1. 按一下 **[!UICONTROL 下載公開金鑰]** 表徵圖並將公鑰(CRT)檔案保存在電腦上。

   公開金鑰稍後會用來設定Brand Portal租用戶的API，以及在Adobe Developer Console中產生服務帳戶憑證。

   ![下載憑證](assets/ims-config3.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   在 **帳戶** 標籤，系統會建立Adobe IMS帳戶，而此帳戶需要在Adobe Developer Console中產生的服務帳戶憑證。 暫時保持此頁面開啟。

   開啟新標籤，然後 [在Adobe Developer主控台中建立服務帳戶(JWT)連線](#createnewintegration) 取得用於設定IMS帳戶的憑證和JWT裝載。

### 建立服務帳戶(JWT)連線 {#createnewintegration}

在Adobe Developer Console中，專案和API是在Brand Portal租用戶（組織）層級設定。 設定API會建立服務帳戶(JWT)連線。 有兩種方法可用來設定API，方法是產生金鑰組（私密和公開金鑰）或上傳公開金鑰。 若要使用Brand Portal設定Experience Manager Assets，您必須在Experience Manager Assets中產生公開金鑰（憑證），並透過上傳公開金鑰在Adobe Developer Console中建立憑證。 您必須具備這些憑證才能在Experience Manager Assets中設定IMS帳戶。 設定IMS帳戶後，您就可以在Experience Manager Assets中設定Brand Portal雲端服務。

執行下列步驟以產生服務帳戶憑證和JWT裝載：

1. 以IMS組織(Brand Portal租用戶)的系統管理員權限登入Adobe Developer Console。 預設URL為 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >確認您已從右上角的下拉式清單（組織）中選取正確的IMS組織(Brand Portal租用戶)。

1. 按一下 **[!UICONTROL 建立新專案]**. 系統會為您的組織建立一個空白專案，其名稱為系統產生。

   按一下 **[!UICONTROL 編輯專案]** 更新 **[!UICONTROL 專案標題]** 和 **[!UICONTROL 說明]**，然後按一下 **[!UICONTROL 儲存]**.

1. 在 **[!UICONTROL 專案概述]** 按一下 **[!UICONTROL 新增API]**.

1. 在 **[!UICONTROL 新增API視窗]**，選取 **[!UICONTROL AEM Brand Portal]** 按一下 **[!UICONTROL 下一個]**.

   確保您擁有Experience ManagerBrand Portal服務的存取權。

1. 在 **[!UICONTROL 設定API]** 按一下 **[!UICONTROL 上傳您的公開金鑰]**. 然後，按一下 **[!UICONTROL 選取檔案]** 並上傳您在 [取得公開憑證](#public-certificate) 區段。

   按一下&#x200B;**[!UICONTROL 下一步]**。

   ![上傳公開金鑰](assets/service-account3.png)

1. 驗證公開金鑰並按一下 **[!UICONTROL 下一個]**.

1. 選擇 **[!UICONTROL Assets Brand Portal]** 作為預設產品設定檔，然後按一下 **[!UICONTROL 儲存已設定的API]**.

   ![選取產品設定檔](assets/service-account4.png)

1. 設定API後，系統會將您重新導向至API概觀頁面。 從下方的左側導覽 **[!UICONTROL 憑證]**，按一下 **[!UICONTROL 服務帳戶(JWT)]** 選項。

   >[!NOTE]
   >
   >您可以檢視憑證並執行下列動作：產生JWT代號、複製憑證詳細資訊、擷取用戶端密碼等。

1. 從 **[!UICONTROL 客戶端憑據]** 頁簽，複製 **[!UICONTROL 用戶端ID]**.

   按一下 **[!UICONTROL 擷取用戶端密碼]** 並複製 **[!UICONTROL 用戶密碼]**.

   ![服務帳戶憑據](assets/service-account5.png)

1. 導覽至 **[!UICONTROL 產生JWT]** 標籤並複製 **[!UICONTROL JWT裝載]** 資訊。

您現在可以將用戶端ID（API金鑰）、用戶端密碼和JWT裝載，用於 [設定IMS帳戶](#create-ims-account-configuration) 在Experience Manager Assets。

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

### 設定IMS帳戶 {#create-ims-account-configuration}

請確認您已執行下列步驟：

* [取得公開憑證](#public-certificate)
* [建立服務帳戶(JWT)連線](#createnewintegration)

執行下列步驟來設定IMS帳戶。

1. 開啟IMS設定並導覽至 **[!UICONTROL 帳戶]** 標籤。 您在 [取得公開憑證](#public-certificate).

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在 **[!UICONTROL 授權伺服器]** 欄位，指定URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   在 **[!UICONTROL API金鑰]** 欄位， **[!UICONTROL 用戶端密碼]**，和 **[!UICONTROL 裝載]** （JWT裝載），而您 [建立服務帳戶(JWT)連線](#createnewintegration).

   按一下&#x200B;**[!UICONTROL 建立]**。

   已設定IMS帳戶。

   ![IMS 帳戶設定](assets/create-new-integration6.png)


1. 選取IMS帳戶設定，然後按一下 **[!UICONTROL 檢查運行狀況]**.

   按一下 **[!UICONTROL 檢查]** 框中輸入URL。 成功設定時，畫面會顯示訊息，指出 *已成功檢索令牌*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一個IMS設定。
>
>確認IMS設定通過健康狀況檢查。 如果配置未通過運行狀況檢查，則無效。 您必須刪除它，然後建立新的有效配置。

### 設定雲端服務 {#configure-the-cloud-service}

執行下列步驟以設定Brand Portal雲端服務：

1. 登入Experience Manager Assets。

1. 從 **工具** 面板，導覽至 **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. 在Brand Portal設定頁面中，按一下 **[!UICONTROL 建立]**.

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選取您在 [設定IMS帳戶](#create-ims-account-configuration).

   在 **[!UICONTROL 服務URL]** 欄位中，指定您的Brand Portal租用戶（組織）URL。

   ![](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。雲端設定此時已建立。

   您的Experience Manager Assets as a [!DNL Cloud Service] 例項現在已以Brand Portal租用戶設定。

您現在可以檢查發佈代理程式並將資產發佈至Brand Portal，以測試設定。

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Login to AEM Assets.

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
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

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
