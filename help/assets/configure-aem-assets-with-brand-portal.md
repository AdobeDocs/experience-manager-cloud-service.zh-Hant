---
title: 使用品牌入口網站設定AEM Assets雲端服務
description: 使用品牌入口網站設定AEM Assets雲端服務。
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: f57731e4ab30af1bfcd93a12b2cf80e63efdac79

---


# 使用品牌入口網站設定AEM資產 {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager(AEM)Assets是透過Adobe I/O以品牌入口網站設定，Adobe I/O會購買IMS Token以授權您的品牌入口網站租用戶。

## 必備條件 {#prerequisites}

您需要下列項目才能設定具有品牌入口網站的AEM資產：

* 啟動並執行AEM Assets雲端例項。
* 品牌入口網站租用戶URL。
* 對品牌入口網站的IMS組織具有系統管理員權限的使用者。

**請連絡支援** ，以取得進一步的查詢。

## Create configuration {#create-new-configuration}

您可以在Adobe I/O上建立新的設定，以使用品牌入口網站來設定您的AEM Assets雲端例項。

在所列順序中執行以下步驟：
1. [取得公開憑證](#public-certificate)
1. [建立Adobe I/O整合](#createnewintegration)
1. [建立IMS帳戶設定](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)
1. [測試設定](#test-configuration)

### 建立IMS設定 {#create-ims-configuration}

IMS設定會以AEM Assets作者例項驗證您的品牌入口網站租用戶。

IMS配置包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [建立IMS帳戶設定](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開憑證可讓您在Adobe I/O上驗證個人檔案。

1. 登入您的AEM Assets雲端例項

1. 從「 **Security** ![Tools](assets/tools.png) ( **[!UICONTROL 安全性工具)」面板，導覽至「]** Adobe IMS設定工具(Security **[!UICONTROL >]** Adobe IMS Configurations Tools)」。

   ![Adobe IMS帳戶設定UI](assets/ims-configuration1.png)

1. Adobe IMS設定頁面隨即開啟。

   按一下 **[!UICONTROL 建立]**。

   這會帶您前往 **[!UICONTROL Adobe IMS技術帳戶設定頁面]** 。

1. 依預設會開 **啟「認證** 」標籤。

   在 **Cloud Solution中**，選取 **[!UICONTROL Adobe品牌入口網站]**。

1. 標籤核取方 **[!UICONTROL 塊「建立新憑證]** 」並指 **定憑證的** 別名。 別名用作對話框的名稱。

1. 按一 **[!UICONTROL 下建立憑證]**。 將出現對話框。 按一下 **[!UICONTROL 確定]** ，生成公共證書。

   ![建立憑證](assets/ims-config2.png)

1. 按一 **[!UICONTROL 下「下載公開金鑰]** 」，並將 ** AEM-Adobe-IMS.crt憑證檔案儲存在您的電腦上。 憑證檔案用來 [建立Adobe I/O整合](#createnewintegration)。

   ![下載憑證](assets/ims-config3.png)

1. 按一 **[!UICONTROL 下「下一步]**」。

   在「帳 **戶** 」索引標籤中，您建立Adobe IMS帳戶，但您需要整合詳細資訊。 請立即開啟此頁面。

   開啟新標籤並建 [立Adobe I/O整合](#createnewintegration) ，以取得IMS帳戶設定的整合詳細資訊。

### 建立Adobe I/O整合 {#createnewintegration}

Adobe I/O整合會產生API金鑰、用戶端密碼和裝載(JWT)，這是設定IMS帳戶設定所需的。

1. 使用品牌入口網站租用戶之IMS組織的系統管理員權限登入Adobe I/O Console。

   預設URL: [https://console.adobe.io/](https://console.adobe.io/)

1. 按一 **[!UICONTROL 下建立整合]**。

1. 選取 **[!UICONTROL 存取API]**，然後按一下 **[!UICONTROL 繼續]**。

   ![建立新整合](assets/create-new-integration1.png)

1. 建立新的整合頁面隨即開啟。

   從下拉式清單中選擇您的組織。

   在 **[!UICONTROL Experience Cloud]**，選取 **[!UICONTROL AEM品牌入口網站]** ，然後按一下「 **[!UICONTROL 繼續]**」。

   如果您已停用「品牌入口網站」選項，請確定您已從 **[!UICONTROL Adobe服務選項上方的下拉式方塊中選取正確的組織]** 。 如果您不瞭解您的組織，請聯絡您的管理員。

   ![建立整合](assets/create-new-integration2.png)

1. 指定整合的名稱和說明。 按一 **[!UICONTROL 下「從電腦選取檔案」]** ，並上傳 `AEM-Adobe-IMS.crt` 在「取得公用憑證」區 [段中下載的檔案](#public-certificate) 。

1. 選擇組織的配置檔案。

   或者，選取預設的描述檔 **[!UICONTROL 資產品牌入口網站]** ，然後按 **[!UICONTROL 一下「建立整合」]**。 會建立整合。

1. 按一 **[!UICONTROL 下「繼續」以整合詳細資訊]** ，以檢視整合資訊。

   複製 **[!UICONTROL API金鑰]**

   按一 **[!UICONTROL 下「擷取用戶端密碼]** 」並複製用戶端密碼。

   ![整合的API金鑰、用戶端密碼和裝載資訊](assets/create-new-integration3.png)

1. 導航到 **[!UICONTROL JWT]** 頁籤，並複製 **[!UICONTROL JWT裝載]**。

   API金鑰、用戶端密碼金鑰和JWT裝載資訊將用來建立IMS帳戶設定。

### 建立IMS帳戶設定 {#create-ims-account-configuration}

請確定您已執行下列步驟：

* [取得公開憑證](#public-certificate)
* [建立Adobe I/O整合](#createnewintegration)

**建立IMS帳戶設定的步驟：**

1. 開啟「IMS設定」頁面的「帳 **[!UICONTROL 戶]** 」標籤。 您在「取得公開的憑證」一節的結尾處保 [持頁面開啟](#public-certificate)。

1. 指定 **[!UICONTROL IMS帳戶]** 的標題。

   在授 **[!UICONTROL 權伺服器]**，輸入URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   在「建立Adobe I/O」整合結束時貼上您已複製的API金鑰、用戶端密碼和JWT裝載 [](#createnewintegration)。

   按一下 **[!UICONTROL 建立]**。

   會建立整合。

   ![IMS帳戶設定](assets/create-new-integration6.png)


1. 選擇IMS設定，然後按一下「 **[!UICONTROL Check Health」(檢查健康]**)。 將出現一個對話框。

   按一下 **[!UICONTROL 檢查]**。 在成功連線時，會出 *現成功擷取的Token* 訊息。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>只建立一個有效的IMS設定。
>
> 確保配置正常。 如果配置不健康，請將其刪除並建立新的健康配置。


### 設定雲端服務 {#configure-the-cloud-service}

執行下列步驟以建立品牌入口網站雲端服務設定：

1. 登入您的AEM Assets雲端例項

1. 從「工 **具**![」面板，導覽至「雲端服務](assets/tools.png) >品 ********&#x200B;牌入口工具」。

   品牌入口網站設定頁面隨即開啟。

1. 按一下 **[!UICONTROL 建立]**。

1. 指定 **[!UICONTROL 配置的]** 「標題」。

   選取您在步驟中建立的IMS設定，建立 [IMS帳戶設定](#create-ims-account-configuration)。

   在「 **[!UICONTROL 服務URL]**」中，輸入您的品牌入口網站租用戶URL。

   ![](assets/create-cloud-service.png)

1. 按一 **[!UICONTROL 下儲存並關閉]**。 雲端設定已建立。 您的AEM Assets雲端例項現在已設定品牌入口網站租用戶。

### Test configuration {#test-configuration}

1. 登入您的AEM Assets雲端實例。

1. 從「 **Deployment** ![Tools](assets/tools.png)**[!UICONTROL 」面板，導覽至「Deployment]** Distribution **[!UICONTROL Tools]**> 」。

   ![](assets/test-bpconfig1.png)

1. 「散發」頁面隨即開啟。

   在「發佈至品牌入口網站」 `bpdistributionagent0` 下會建立 **[!UICONTROL 品牌入口網站分發代理]**。

   Click **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >依預設，會為品牌入口網站租用戶建立一個散發代理。

1. 此時會開啟散發代理頁面。 預設情況下，會打 **[!UICONTROL 開「狀態]** 」頁籤，該頁籤將填充分佈隊列。

   分發代理包含兩個隊列：
   * 將資產分發至品牌入口網站的處理佇列。
   * 發佈失敗之資產的錯誤佇列。
   ![](assets/test-bpconfig3.png)

1. 若要驗證AEM Assets和品牌入口網站之間的連線，請按一下「 **[!UICONTROL 測試連線」]**。

   ![](assets/test-bpconfig4.png)

   頁面底部會顯示訊息，指出您的測試套件已成功傳送。

   >[!NOTE]
   >
   >請避免停用散發代理，因為這可能導致資產的散發（在佇列中執行）失敗。


您的AEM Assets雲端例項已成功設定為品牌入口網站，您現在可以：

* [將資產從AEM Assets發佈至品牌入口網站](publish-to-brand-portal.md)
* [將資料夾從AEM Assets發佈至品牌入口網站](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [將系列從AEM Assets發佈至品牌入口網站](publish-to-brand-portal.md#publish-collections-to-brand-portal)

除了上述外，您也可以將中繼資料結構描述、影像預設集、搜尋刻面和標籤從AEM Assets發佈至品牌入口網站。

* [將預設集、結構描述和刻面發佈至品牌入口網站](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


如需詳細 [資訊，請參閱品牌入口網站](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) (Brand Portal)檔案。


## 散發記錄檔 {#distribution-logs}

您可以檢查日誌，瞭解有關對分發代理執行的操作的詳細資訊。

例如，我們已將資產從AEM Assets發佈至品牌入口網站，以驗證設定。

1. 請依照測試連線中顯示的步驟(步驟1 **[!UICONTROL 至]** 4)，並導覽至散發代理頁面。

1. 按一 **[!UICONTROL 下「記錄]** 」以檢視散發記錄檔。 您可在此處看到處理和錯誤記錄。

   ![](assets/test-bpconfig5.png)

Distribution Agent會生成以下日誌：

* 資訊：這是系統生成的日誌，在成功配置時觸發，用於啟用分發代理。
* DSTRQ1（請求1）:在測試連線上觸發。

發佈資產時，會產生下列請求和回應記錄：

**散發代理請求**:
* DSTRQ2（請求2）:會觸發資產發佈請求。
* DSTRQ3（請求3）:系統會觸發另一個請求，以發佈資產所在的檔案夾，並複製品牌入口網站中的檔案夾。

**散發代理回應**:
* queue-bpdistributionagent0(DSTRQ2):資產會發佈至品牌入口網站。
* queue-bpdistributionagent0(DSTRQ3):系統會複製品牌入口網站中包含資產的資料夾。

在上述範例中，會觸發額外的請求和回應。 系統無法在品牌入口網站中找到父資料夾（亦即新增路徑），因為資產是首次發佈，因此會觸發其他要求，在發佈資產的品牌入口網站中建立同名的父資料夾。

>[!NOTE]
>
>如果父資料夾不存在於品牌入口網站（在上例中），或父資料夾已在AEM Assets中修改，則會產生其他請求。


## 其他資訊 {#additional-information}

請至以 `/system/console/slingmetrics` 取得與散布內容相關的統計資料：

1. **計數器量度**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **時間量度**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
