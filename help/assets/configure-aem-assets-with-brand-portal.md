---
title: 使用 Brand Portal 設定 AEM Assets 雲端服務
description: 使用 Brand Portal 設定 AEM Assets 雲端服務。
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 00e37e9493bc3dde8a4d83c562a889a67587ada0
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 80%

---


# 使用 Brand Portal 設定 AEM Assets {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager (AEM) Assets 是透過 Adobe I/O 以 Brand Portal 設定，這種方式會取得 IMS Token 來使 Brand Portal 租用戶獲得授權。

## 必備條件 {#prerequisites}

您需要下列項目才能使用 Brand Portal 設定 AEM Assets：

* 已開始運作的 AEM Assets 雲端例項。
* Brand Portal 租用戶 URL。
* 在 Brand Portal 租用戶的 IMS 組織具有系統管理員權限的使用者。

**請連絡客戶服務** ，以取得進一步的查詢。

## 建立設定 {#create-new-configuration}

您可以在Adobe I/O上建立設定，以使用品牌入口網站來設定您的AEM Assets雲端例項。

請以所列順序執行以下步驟：
1. [取得公開憑證](#public-certificate)
1. [建立 Adobe I/O 整合項目](#createnewintegration)
1. [建立 IMS 帳戶設定](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)
1. [測試設定](#test-configuration)

### 建立 IMS 設定 {#create-ims-configuration}

IMS 設定會以 AEM Assets 作者例項驗證您的 Brand Portal 租用戶。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [建立 IMS 帳戶設定](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開憑證可讓您在 Adobe I/O 上驗證設定檔。

1. 登入 AEM Assets 雲端例項。

1. From **tool** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![Adobe IMS 帳戶設定 UI](assets/ims-configuration1.png)

1. Adobe IMS 設定頁面隨即開啟。

   按一下&#x200B;**[!UICONTROL 建立]**。

   It will take you to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page.

1. 依預設，**憑證**&#x200B;標籤會開啟。

   在&#x200B;**雲端解決方案**&#x200B;中，選取 **[!UICONTROL Adobe Brand Portal]**。

1. Mark the check box **[!UICONTROL Create new certificate]** and specify an **alias** for the certificate. 別名的作用是對話方塊的名稱。

1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。對話方塊隨即顯示。按一下&#x200B;**[!UICONTROL 確定]**&#x200B;即可產生公開憑證。

   ![建立憑證](assets/ims-config2.png)

1. 按一下&#x200B;**[!UICONTROL 下載公開金鑰]**，並將 *AEM-Adobe-IMS.crt* 憑證檔案儲存在電腦上。憑證檔案可用於[建立 Adobe I/O 整合項目](#createnewintegration)。

   ![下載憑證](assets/ims-config3.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   您會在&#x200B;**帳戶**&#x200B;標籤中建立 Adobe IMS 帳戶，但需要整合詳細資訊才能完成。暫時保持此頁面開啟。

   開啟新標籤並[建立 Adobe I/O 整合項目](#createnewintegration)，以便取得 IMS 帳戶設定的整合詳細資訊。

### 建立 Adobe I/O 整合項目 {#createnewintegration}

Adobe I/O 整合項目會產生 API 金鑰、用戶端密碼，以及設定 IMS 帳戶設定所需的裝載 (JWT)。

1. 以 Brand Portal 租用戶在 IMS 組織的系統管理員權限登入 Adobe I/O 控制台。

   預設 URL：[https://console.adobe.io/](https://console.adobe.io/)

1. 按一下&#x200B;**[!UICONTROL 建立整合項目]**。

1. 選取&#x200B;**[!UICONTROL 存取 API]**，然後按一下&#x200B;**[!UICONTROL 繼續]**。

   ![建立新整合項目](assets/create-new-integration1.png)

1. 建立新整合項目的頁面隨即開啟。

   從下拉式清單中選取您的組織。

   在 **[!UICONTROL Experience Cloud]** 中選取 **[!UICONTROL AEM Brand Portal]**，然後按一下&#x200B;**[!UICONTROL 繼續]**。

   如果您已停用「Brand Portal」選項，請確認您已在 **[!UICONTROL Adobe 服務]**&#x200B;選項上方的下拉式方塊中選取正確的組織。如果您不清楚自己的組織為何，請聯絡您的管理員。

   ![建立整合項目](assets/create-new-integration2.png)

1. 指定整合項目的名稱和說明。按一下&#x200B;**[!UICONTROL 從電腦選取檔案]**，並上傳在[取得公開憑證](#public-certificate)區段中下載的 `AEM-Adobe-IMS.crt` 檔案 。

1. 選取組織的設定檔。

   或者，選取預設設定檔 **[!UICONTROL Assets Brand Portal]**，然後按一下&#x200B;**[!UICONTROL 建立整合項目]**。整合項目隨即建立。

1. 按一下&#x200B;**[!UICONTROL 繼續前往整合詳細資訊]**，以便檢視整合資訊。

   複製 **[!UICONTROL API 金鑰]**

   按一下&#x200B;**[!UICONTROL 擷取用戶端密碼]**&#x200B;並複製用戶端密碼金鑰。

   ![整合項目的 API 金鑰、用戶端密碼和裝載資訊](assets/create-new-integration3.png)

1. 導覽至 **[!UICONTROL JWT]** 標籤，並複製 **[!UICONTROL JWT 裝載]**。

   API 金鑰、用戶端密碼金鑰和 JWT 裝載資訊將用來建立 IMS 帳戶設定。

### 建立 IMS 帳戶設定 {#create-ims-account-configuration}

請確認您已執行下列步驟：

* [取得公開憑證](#public-certificate)
* [建立 Adobe I/O 整合項目](#createnewintegration)

**建立 IMS 帳戶設定的步驟：**

1. 開啟 IMS 設定頁面&#x200B;**[!UICONTROL 帳戶]**&#x200B;標籤。在[取得公開憑證](#public-certificate)這一節的結尾，您已保持此頁面開啟。

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在&#x200B;**[!UICONTROL 授權伺服器]**，輸入 URL：[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   貼上您在[建立 Adobe I/O 整合項目](#createnewintegration)結尾複製的 API 金鑰、用戶端密碼和 JWT 裝載。

   按一下&#x200B;**[!UICONTROL 建立]**。

   整合項目隨即建立。

   ![IMS 帳戶設定](assets/create-new-integration6.png)


1. 選取 IMS 設定，然後按一下&#x200B;**[!UICONTROL 檢查健康狀態]**。對話方塊隨即顯示。

   按一下&#x200B;**[!UICONTROL 檢查]**。成功連線時，*已成功擷取 Token* 訊息就會顯示。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一個IMS設定。 請勿建立多個 IMS 組態。
>
>確保IMS配置通過健康檢查。 如果配置未通過健康檢查，則無效。 您必須刪除它並建立新的有效設定。



### 設定雲端服務 {#configure-the-cloud-service}

執行下列步驟以建立 Brand Portal 雲端服務設定：

1. 登入 AEM Assets 雲端例項。

1. From **tool** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

   「Brand Portal 設定」頁面隨即開啟。

1. 按一下&#x200B;**[!UICONTROL 建立]**。

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選取您在[建立 IMS 帳戶設定](#create-ims-account-configuration)步驟中建立的 IMS 設定。

   在&#x200B;**[!UICONTROL 服務 URL]**&#x200B;中，輸入您的 Brand Portal 租用戶 URL。

   ![](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。雲端設定此時已建立。您的 AEM Assets 雲端例項現在已經以 Brand Portal 租用戶完成設定。

### 測試設定 {#test-configuration}

1. 登入 AEM Assets 雲端例項。

1. From **tool** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

   ![](assets/test-bpconfig1.png)

1. 「發佈」頁面隨即開啟。

   Brand Portal 發佈代理程式 `bpdistributionagent0` 會建立在&#x200B;**[!UICONTROL 發佈至 Brand Portal]** 下。

   按一下&#x200B;**[!UICONTROL 發佈至 Brand Portal]**。

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >依預設，系統會為 Brand Portal 租用戶建立一個發佈代理程式。

1. 發佈代理程式頁面隨即開啟。依預設，填入發佈佇列的&#x200B;**[!UICONTROL 狀態]**&#x200B;標籤此時會開啟。

   發佈代理程式包含兩個佇列：
   * **processing-queue**: 將資產分發至品牌入口網站。

   * **error-queue**: 對於分發失敗的資產。
   >[!NOTE]
   >
   >建議您檢閱失敗，並定期清 **除錯誤佇列** 。

   ![](assets/test-bpconfig3.png)

1. 若要驗證 AEM Assets 和 Brand Portal 之間的連線，請按一下&#x200B;**[!UICONTROL 測試連線]**。

   ![](assets/test-bpconfig4.png)

   頁面底部會顯示訊息，指出您的測試封裝已成功傳送。

   >[!NOTE]
   >
   >請避免停用發佈代理程式，因為可能導致在佇列中執行的資產發佈失敗。


您的 AEM Assets 雲端例項已成功以 Brand Portal 完成設定，您現在可以：

* [從 AEM Assets 發佈資產到 Brand Portal](publish-to-brand-portal.md)
* [從 AEM Assets 發佈資料夾到 Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [從 AEM Assets 發佈集合到 Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)

除了上述操作，您也可以從 AEM Assets 將中繼資料結構、影像預設集、搜尋 Facet 和標籤發佈至 Brand Portal。

* [將預設集、結構和 Facet 發佈至 Brand Portal](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


如需詳細資訊，請參閱 [Brand Portal 文件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/home.html)。


## 發佈記錄檔 {#distribution-logs}

您可以檢查記錄檔瞭解發佈代理程式所執行動作的詳細資訊。

舉例來說，我們已從 AEM Assets 發佈資產到 Brand Portal，以便驗證設定。

1. Follow the steps (Step 1 - 4) as shown in **[!UICONTROL Test Connection]** and navigate to the distribution agent page.

1. 按一下&#x200B;**[!UICONTROL 記錄檔]**&#x200B;以檢視發佈記錄檔。您可在此查看處理和錯誤記錄。

   ![](assets/test-bpconfig5.png)

發佈代理程式會產生以下記錄檔：

* 資訊： 這是系統生成的日誌，在成功配置時觸發，用於啟用分發代理。
* DSTRQ1（請求1）: 測試連線時的觸發器。

發佈資產時，會產生下列請求和回應記錄檔：

**發佈代理程式請求**：
* DSTRQ2 (請求 2)：觸發資產發佈請求。
* DSTRQ3（請求3）: 系統會觸發另一個請求來發佈資產所在的資料夾，並複製品牌入口網站中的資料夾。

**發佈代理程式回應**：
* queue-bpdistributionagent0 (DSTRQ2)：資產已發佈至 Brand Portal。
* queue-bpdistributionagent0 (DSTRQ3)：系統會複製含有 Brand Portal 中的資產的資料夾。

在上述範例中，會觸發額外的請求和回應。 系統無法在品牌入口網站中找到父資料夾（亦即新增路徑），因為資產是首次發佈，因此會觸發在發佈資產的品牌入口網站中建立同名父資料夾的額外請求。

>[!NOTE]
>
>如果父資料夾不存在上述例子的 Brand Portal 中，或父資料夾已在 AEM Assets 中經過修改，系統會產生其他請求。



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
