---
title: '使用Brand Portal將AEM Assets設定為a [!DNL Cloud Service] '
description: 使用 Brand Portal 設定 AEM Assets.
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution,Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '2402'
ht-degree: 8%

---

# 使用Brand Portal將AEM Assets設定為[!DNL Cloud Service] {#configure-aem-assets-with-brand-portal}

設定Adobe Experience Manager Assets Brand Portal可讓您將已核准的品牌資產以[!DNL Cloud Service]例項的形式發佈至Brand Portal，並分發給Brand Portal使用者。

## 使用Cloud Manager啟用Brand Portal {#activate-brand-portal}

Cloud Manager使用者會為AEM Assets啟用Brand Portal作為[!DNL Cloud Service]例項。 啟動工作流程會在後端建立必要的設定(授權Token、IMS設定和Brand Portal雲端服務)，並反映Cloud Manager中Brand Portal租用戶的狀態。 啟用Brand Portal可讓AEM Assets使用者將資產發佈至Brand Portal，並分發給Brand Portal使用者。

**必備條件**

您需要下列項目，才能以[!DNL Cloud Service]例項形式在您的AEM Assets上啟用Brand Portal:

* 以[!DNL Cloud Service]例項形式啟動且執行的AEM Assets。
* 有權存取Cloud Manager的使用者，已指派給Cloud Manager產品的設定檔。 如需詳細資訊，請參閱[存取Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager) 。

>[!NOTE]
>
>作為[!DNL Cloud Service]例項的AEM Assets只有權與一個Brand Portal租用戶連線。 您的AEM Assets可以有多個環境（開發、生產和預備），作為[!DNL Cloud Service]例項，其中Brand Portal會在一個環境中啟動。

**啟動Brand Portal的步驟**

您可以在將AEM Assets建立為[!DNL Cloud Service]例項時啟用Brand Portal，或個別啟用。 假設環境已建立，您現在必須啟用Brand Portal。

1. 登入AdobeCloud Manager並導覽至&#x200B;**[!UICONTROL Environments]**。

   **[!UICONTROL 環境]**&#x200B;頁面會顯示所有現有環境的清單。

1. 從清單中選取環境（逐一）以檢視環境詳細資訊。

   Brand Portal有權使用其中一個可用環境，並會反映在&#x200B;**[!UICONTROL 環境資訊]**&#x200B;下。

   找到與Brand Portal相關聯的環境後，按一下&#x200B;**[!UICONTROL 啟動Brand Portal]**&#x200B;按鈕以開始啟動工作流程。

   ![啟用Brand Portal](assets/create-environment4.png)

1. 啟動工作流程會在後端建立必要的設定時，啟動Brand Portal租用戶需要幾分鐘的時間。 啟動Brand Portal租用戶後，狀態會變更為「已啟動」。

   ![檢視狀態](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal必須在與AEM Assets相同的IMS組織上啟動，如同[!DNL Cloud Service]例項。
>
>如果您有適用於IMS組織(org1-existing)的現有Brand Portal雲端設定([使用Adobe開發人員控制台](#manual-configuration)手動設定)，且您的AEM Assets為[!DNL Cloud Service]例項已針對其他IMS組織(org2-new)設定，則從Cloud manager啟用Brand Portal會將Brand Portal IMS組織重設為`org2-new`。 雖然在`org1-existing`上手動設定的雲端設定會顯示在AEM Assets製作例項中，但從Cloud Manager啟動Brand Portal後，將不再使用。
>
>如果現有的Brand Portal雲端設定和AEM Assets作為[!DNL Cloud Service]例項使用相同的IMS組織(org1)，您只需從Cloud Manager啟用Brand Portal即可。
>
>請勿修改任何自動產生的設定。

**另請參閱**:
* [在AEM Assets as a Cloud Service中新增使用者和角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [在Cloud Manager中管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**登入您的Brand Portal租用戶**:

在Cloud Manager中啟用Brand Portal租用戶後，您可以從Admin Console或直接使用租用戶URL登入Brand Portal。

Brand Portal租用戶的預設URL為：`https://<tenant-id>.brand-portal.adobe.com/`。

其中，租用戶ID為IMS組織。

如果您不確定Brand Portal URL，請執行下列步驟：

1. 登入[Admin Console](https://adminconsole.adobe.com/)並導覽至&#x200B;**[!UICONTROL Products]**。
1. 從左側邊欄，選取&#x200B;**[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**。
1. 按一下&#x200B;**[!UICONTROL 前往Brand Portal]**&#x200B;直接在瀏覽器中開啟Brand Portal。

   或從&#x200B;**[!UICONTROL 前往Brand Portal]**&#x200B;連結複製Brand Portal租用戶URL，並貼到您的瀏覽器以開啟Brand Portal介面。

   ![存取Brand Portal](assets/access-bp-on-cloud.png)


**測試連接**

執行下列步驟來驗證您作為[!DNL Cloud Service]例項的AEM Assets與Brand Portal租用戶之間的連線：

1. 登入AEM Assets。

1. 從&#x200B;**工具**&#x200B;面板，導覽至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 分發]**。

   ![](assets/test-bpconfig1.png)

   在&#x200B;**[!UICONTROL 發佈至Brand Portal]**&#x200B;下建立Brand Portal發佈代理程式(**[!UICONTROL bpdistributionagent0]**)。

   ![](assets/test-bpconfig2.png)


1. 按一下&#x200B;**[!UICONTROL 發佈至Brand Portal]**&#x200B;以開啟發佈代理程式。

   您可以在&#x200B;**[!UICONTROL Status]**&#x200B;標籤下看到分發隊列。

   發佈代理程式包含兩個佇列：
   * **processing-queue**:將資產分配給Brand Portal。

   * **error-queue**:針對發佈失敗的資產。
   >[!NOTE]
   >
   >建議定期檢查故障並清除&#x200B;**error-queue**。

   ![](assets/test-bpconfig3.png)

1. 若要驗證作為[!DNL Cloud Service]的AEM Assets與Brand Portal之間的連線，請按一下&#x200B;**[!UICONTROL 測試連線]**&#x200B;圖示。

   ![](assets/test-bpconfig4.png)

   出現一條消息，表明&#x200B;*測試包已成功傳送*。

   >[!NOTE]
   >
   >請避免停用發佈代理程式，因為可能導致在佇列中執行的資產發佈失敗。

若要驗證您作為[!DNL Cloud Service]例項的AEM Assets與Brand Portal租用戶之間的連線，請從AEM Assets發佈資產至Brand Portal。 如果連線成功，已發佈的資產會顯示在Brand Portal介面中。


您現在可以：

* [從 AEM Assets 發佈資產到 Brand Portal](publish-to-brand-portal.md)
* [從 AEM Assets 發佈資料夾到 Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [從 AEM Assets 發佈集合到 Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [從Brand Portal發佈資產至AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)  - Brand Portal中的Asset Sourcing
* [將預設集、結構和 Facet 發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

如需詳細資訊，請參閱[Brand Portal檔案](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)。

**發佈記錄檔**

您可以監視資產發佈工作流程的發佈代理程式記錄檔。

現在讓我們將資產從AEM Assets發佈至Brand Portal並查看日誌。

1. 請依照&#x200B;**測試連線**&#x200B;區段中所示步驟（從1到4）操作，並導覽至發佈代理程式頁面。
1. 按一下&#x200B;**[!UICONTROL 記錄]**&#x200B;以檢視處理和錯誤記錄。

   ![](assets/test-bpconfig5.png)

發佈代理程式已產生下列記錄檔：

* 資訊：這是系統產生的記錄檔，會在成功設定發佈代理時觸發。
* DSTRQ1（請求1）:測試連線時觸發。

發佈資產時，會產生下列請求和回應記錄檔：

**發佈代理程式請求**：

* DSTRQ2 (請求 2)：觸發資產發佈請求。
* DSTRQ3（請求3）:系統會觸發另一個請求以發佈AEM Assets資料夾（資產存在其中）並複製Brand Portal中的資料夾。

**發佈代理程式回應**：

* queue-bpdistributionagent0 (DSTRQ2)：資產已發佈至 Brand Portal。
* queue-bpdistributionagent0(DSTRQ3):系統會複製Brand Portal中的AEM Assets資料夾（包含資產）。

在上述範例中，會觸發其他請求和回應。 系統在Brand Portal中找不到父資料夾（新增路徑），因為資產是首次發佈，因此會觸發其他請求，在發佈資產的Brand Portal中建立同名的父資料夾。

>[!NOTE]
>
>如果父資料夾不存在於Brand Portal中或已在AEM Assets中修改，則會產生其他請求。

除了在AEM Assets上以[!DNL Cloud Service]啟動Brand Portal的自動化工作流程之外，還有其他方法可使用Adobe開發人員控制台（不建議再使用），以Brand Portal手動將AEM Assets設為[!DNL Cloud Service]。

>[!NOTE]
>
>如果您在啟用Brand Portal租用戶時遇到任何問題，請聯絡客戶支援。

## 使用Adobe開發人員控制台手動配置 {#manual-configuration}

以下章節說明如何使用「Adobe開發人員控制台」，以手動方式將AEM Assets設為[!DNL Cloud Service]搭配Brand Portal。

過去，AEM Assets as a [!DNL Cloud Service]是透過Brand Portal開發人員控制台手動設定，這會擷取AdobeIdentity Management服務(IMS)帳戶代號，以授權Brand Portal租用戶。 這需要在AEM Assets和Adobe開發人員控制台中進行設定。

1. 在AEM Assets中，建立IMS帳戶並產生公開金鑰（憑證）。
1. 在Adobe開發人員控制台中，為您的Brand Portal租用戶（組織）建立專案。
1. 在專案下，使用公開金鑰設定API以建立服務帳戶連線。
1. 取得服務帳戶認證和JSON網頁代號(JWT)裝載資訊。
1. 在AEM Assets中，使用服務帳戶憑證和JWT裝載來設定IMS帳戶。
1. 在AEM Assets中，使用IMS帳戶和Brand Portal端點（組織URL）來設定Brand Portal雲端服務。
1. 將資產從AEM Assets發佈至Brand Portal，以測試您的設定。

>[!NOTE]
>
>AEM Assets作為[!DNL Cloud Service]例項時，只能設定一個Brand Portal租用戶。

**必備條件**

您需要下列項目才能使用 Brand Portal 設定 AEM Assets：

* 啟動並執行AEM Assets作為[!DNL Cloud Service]例項
* Brand Portal租用戶URL
* 在Brand Portal租用戶的IMS組織上具有系統管理員權限的使用者

## 建立設定 {#create-new-configuration}

以指定順序執行下列步驟，使用Brand Portal設定AEM Assets。

1. [取得公開憑證](#public-certificate)
1. [建立服務帳戶(JWT)連線](#createnewintegration)
1. [設定IMS帳戶](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)

### 建立 IMS 設定 {#create-ims-configuration}

IMS設定會以Brand Portal租戶驗證您的AEM Assets作為[!DNL Cloud Service]例項。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [設定IMS帳戶](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開金鑰（憑證）會在Adobe開發人員控制台中驗證您的設定檔。

1. 登入AEM Assets。
1. 從&#x200B;**工具**&#x200B;面板，導覽至&#x200B;**[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**。
1. 在「Adobe IMS設定」頁面中，按一下「**[!UICONTROL 建立]**」。 它會重新導向至&#x200B;**[!UICONTROL Adobe IMS技術帳戶設定]**&#x200B;頁面。 依預設，會開啟&#x200B;**Certificate**&#x200B;標籤。
1. 在&#x200B;**[!UICONTROL 雲解決方案]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL AdobeBrand Portal]**。
1. 選中「建立新證書&#x200B;]**」複選框，並為公鑰指定**&#x200B;別名&#x200B;**。**[!UICONTROL &#x200B;別名用作公鑰的名稱。
1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。然後，按一下&#x200B;**[!UICONTROL OK]**&#x200B;以產生公開金鑰。

   ![建立憑證](assets/ims-config2.png)

1. 按一下&#x200B;**[!UICONTROL 下載公開密鑰]**&#x200B;表徵圖並將公開密鑰(CRT)檔案保存在電腦上。

   公開金鑰稍後會用來設定Brand Portal租用戶的API，以及在Adobe開發人員控制台中產生服務帳戶憑證。

   ![下載憑證](assets/ims-config3.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**帳戶**&#x200B;標籤中，建立Adobe IMS帳戶，此帳戶需要在Adobe開發人員控制台中產生的服務帳戶憑證。 暫時保持此頁面開啟。

   開啟新標籤，並在Adobe開發人員控制台](#createnewintegration)中建立服務帳戶(JWT)連線，以取得用於設定IMS帳戶的憑證和JWT裝載。[

### 建立服務帳戶(JWT)連線 {#createnewintegration}

在「Adobe開發人員控制台」中，專案和API是在Brand Portal租用戶（組織）層級設定。 設定API會建立服務帳戶(JWT)連線。 有兩種方法可用來設定API，方法是產生金鑰組（私密和公開金鑰）或上傳公開金鑰。 若要使用Brand Portal設定AEM Assets，您必須在AEM Assets中產生公開金鑰（憑證），並透過上傳公開金鑰在Adobe開發人員控制台中建立憑證。 您必須具備這些憑證才能在AEM Assets中設定IMS帳戶。 設定IMS帳戶後，您就可以在AEM Assets中設定Brand Portal雲端服務。

執行下列步驟以產生服務帳戶憑證和JWT裝載：

1. 以IMS組織(Brand Portal租用戶)的系統管理員權限登入Adobe開發人員控制台。 預設URL為[https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   >[!NOTE]
   >
   >確認您已從右上角的下拉式清單（組織）中選取正確的IMS組織(Brand Portal租用戶)。

1. 按一下「**[!UICONTROL 建立新項目]**」。 系統會為您的組織建立一個空白專案，其名稱為系統產生。

   按一下&#x200B;**[!UICONTROL 編輯項目]**&#x200B;以更新&#x200B;**[!UICONTROL 項目標題]**&#x200B;和&#x200B;**[!UICONTROL 說明]**，然後按一下&#x200B;**[!UICONTROL 保存]**。

1. 在&#x200B;**[!UICONTROL 專案概述]**&#x200B;標籤中，按一下&#x200B;**[!UICONTROL 新增API]**。

1. 在&#x200B;**[!UICONTROL 新增API視窗]**&#x200B;中，選取&#x200B;**[!UICONTROL AEM Brand Portal]**&#x200B;並按一下&#x200B;**[!UICONTROL 下一步]**。

   確定您擁有AEM Brand Portal服務的存取權。

1. 在&#x200B;**[!UICONTROL 設定API]**&#x200B;視窗中，按一下&#x200B;**[!UICONTROL 上傳公開金鑰]**。 然後，按一下&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;並上載您在[獲取公共證書](#public-certificate)部分下載的公鑰（.crt檔案）。

   按一下&#x200B;**[!UICONTROL 下一步]**。

   ![上傳公開金鑰](assets/service-account3.png)

1. 驗證公鑰，然後按一下&#x200B;**[!UICONTROL Next]**。

1. 選擇&#x200B;**[!UICONTROL Assets Brand Portal]**&#x200B;作為預設產品配置檔案，然後按一下&#x200B;**[!UICONTROL 保存配置的API]**。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![選取產品設定檔](assets/service-account4.png)

1. 設定API後，系統會將您重新導向至API概觀頁面。 在&#x200B;**[!UICONTROL Credentials]**&#x200B;下的左側導航中，按一下&#x200B;**[!UICONTROL 服務帳戶(JWT)]**&#x200B;選項。

   >[!NOTE]
   >
   >您可以檢視憑證並執行下列動作：產生JWT代號、複製憑證詳細資訊、擷取用戶端密碼等。

1. 從&#x200B;**[!UICONTROL 客戶端憑據]**&#x200B;頁簽，複製&#x200B;**[!UICONTROL 客戶端ID]**。

   按一下&#x200B;**[!UICONTROL 擷取用戶端密碼]**&#x200B;並複製&#x200B;**[!UICONTROL 用戶端密碼]**。

   ![服務帳戶憑據](assets/service-account5.png)

1. 導覽至&#x200B;**[!UICONTROL 產生JWT]**&#x200B;標籤，並複製&#x200B;**[!UICONTROL JWT裝載]**&#x200B;資訊。

您現在可以使用用戶端ID（API金鑰）、用戶端密碼，以及JWT裝載來[設定AEM Assets中的IMS帳戶](#create-ims-account-configuration)。

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

1. 開啟IMS設定，並導覽至&#x200B;**[!UICONTROL Account]**&#x200B;標籤。 在[取得公開憑證](#public-certificate)時，您已保持頁面開啟。

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在&#x200B;**[!UICONTROL 授權伺服器]**&#x200B;欄位中，指定URL:[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   在[建立服務帳戶(JWT)連線](#createnewintegration)時您複製的&#x200B;**[!UICONTROL API金鑰]**&#x200B;欄位、**[!UICONTROL 用戶端密碼]**&#x200B;和&#x200B;**[!UICONTROL 裝載]**（JWT裝載）中指定用戶端ID。

   按一下&#x200B;**[!UICONTROL 建立]**。

   已設定IMS帳戶。

   ![IMS 帳戶設定](assets/create-new-integration6.png)


1. 選取IMS帳戶設定，然後按一下「**[!UICONTROL 檢查健康狀況]**」。

   按一下對話框中的&#x200B;**[!UICONTROL Check]**。 成功配置時，將顯示一條消息，說明已成功檢索&#x200B;*令牌*。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一個IMS設定。
>
>確認IMS設定通過健康狀況檢查。 如果配置未通過運行狀況檢查，則無效。 您必須刪除它，然後建立新的有效配置。

### 設定雲端服務 {#configure-the-cloud-service}

執行下列步驟以設定Brand Portal雲端服務：

1. 登入AEM Assets。

1. 從&#x200B;**工具**&#x200B;面板，導覽至&#x200B;**[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**。

1. 在「Brand Portal設定」頁面中，按一下「**[!UICONTROL 建立]**」。

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選取您在[設定IMS帳戶](#create-ims-account-configuration)時建立的IMS設定。

   在&#x200B;**[!UICONTROL 服務URL]**&#x200B;欄位中，指定您的Brand Portal租用戶（組織）URL。

   ![](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。雲端設定此時已建立。

   您的AEM Assets as a [!DNL Cloud Service]例項現在已透過Brand Portal租用戶完成設定。

您現在可以檢查發佈代理程式並將資產發佈至Brand Portal，以測試設定。

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
