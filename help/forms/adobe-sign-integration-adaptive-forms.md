---
title: 如何將Adobe Acrobat Sign與AEM Forms整合？
description: 瞭解如何設定的Adobe Acrobat Sign [!DNL AEM Forms] as a Cloud Service？
feature: Adaptive Forms, Acrobat Sign
role: Admin, User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 2128dac489c270d296f86b56ae811556fb5fe87e
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 24%

---

# 連線 [!DNL AEM Forms] as a Cloud Service與 [!DNL Adobe Acrobat Sign] {#integrate-adobe-sign-with-aem-forms}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms.html#adobe-acrobat-sign-for-government) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Acrobat Sign] 啟用最適化Forms和AEM工作流程的電子簽章工作流程。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在標準 [!DNL Adobe Acrobat Sign] 和最適化表單情境下，用戶會填寫最適化表單來申請服務。例如，信用卡申請表和市民福利表單。用戶申請、提交和簽署申請表單時，此表單會被傳送給服務提供者，以進一步動作。服務提供者便會審查申請並使用 [!DNL Adobe Acrobat Sign] 標記已核准申請。AEM Forms同時支援適用於政府的Adobe Acrobat Sign和Adobe Acrobat Sign Solutions。 根據您的授權和需求，您可以將AEM Forms與以下任一解決方案整合或連線：

* [連結AEM Forms與Adobe Acrobat Sign](#adobe-sign)
* [連線適用於政府的AEM Forms與Adobe Acrobat Sign Solutions](#adobe-acrobat-sign-for-government)

## 連結AEM Forms與Adobe Acrobat Sign {#adobe-sign}

若要連線 **[!DNL AEM Forms]** 替換為 **[!DNL Adobe Acrobat Sign]**，設定「先決條件」區段中列出的軟體和帳戶，並在Forms的as a Cloud Service「製作」和「發佈」執行個體中設定Adobe Sign Cloud Service：

### 連線AEM Forms與Adobe Acrobat Sign的先決條件 {#prerequisites-for-adobe-sign}

您需要下列設定才能整合 [!DNL Adobe Acrobat Sign] 替換為 [!DNL AEM Forms]：

1. 作用中 [Adobe Acrobat Sign開發人員帳戶](https://acrobat.adobe.com/us/en/sign/developer-form.html).
1. 一個 [Adobe Acrobat Sign API應用計畫](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
1. [!DNL Adobe Acrobat Sign] API 應用程式的認證 (用戶端 ID 和用戶端密碼)。
1. （僅適用於政府機關身分證件驗證） [啟用驗證方法](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) 用於政府機關身分證件驗證。

### 連結AEM Forms製作和發佈執行個體與Adobe Acrobat Sign {#configure-adobe-sign-with-aem-forms}

已具備下列先決條件後，請執行以下步驟，以在作者執行個體上設定 [!DNL Adobe Acrobat Sign] 和 [!DNL AEM Forms]。

1. 在AEM Forms作者例項上，導覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**.
1. 在 **[!UICONTROL 設定瀏覽器]** 頁面，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定 **[!UICONTROL 標題]** 對於設定，啟用 **[!UICONTROL 雲端設定]**，並選取 **[!UICONTROL 建立]**. 這樣便會建立儲存 Cloud Services 的設定容器。請確保資料夾名稱未含任何空格。
1. 瀏覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** 然後開啟您在上一步中建立的設定容器。

   >[!NOTE]
   >
   >建立最適化表單時，請在 **[!UICONTROL 設定容器]** 欄位。

1. 在設定頁面上，選取 **[!UICONTROL 建立]** 以建立 [!DNL Adobe Acrobat Sign] AEM Forms中的設定。
1. 在 **[!UICONTROL 一般]** 的標籤 **[!UICONTROL 建立Adobe Acrobat Sign設定]** 頁面，指定 **[!UICONTROL 名稱]** ，然後選取 **[!UICONTROL 下一個]**. 您可以選擇指定 **[!UICONTROL 標題]** 並瀏覽以選取 **[!UICONTROL 縮圖]** 用於設定。

1. 現在您可以 **[!UICONTROL 選取解決方案]** 以選取 [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions](assets/adobe-sign-solution.png)

<!--

[create URL](#create-a-redirect-url-for-your-aem-instance)
 -->

1. 將目前瀏覽器視窗中顯示的URL複製到記事本並移除部分 `/ui#/aem` 從URL. 接著需要修改過的URL才能進行設定 [!DNL Adobe Acrobat Sign] 應用程式搭配 [!DNL AEM Forms]，在稍後的步驟中。 選取&#x200B;**[!UICONTROL 「下一步」]**。

1. 在 **[!UICONTROL 設定]** 標籤，
   * 此 **[!UICONTROL OAuth URL]** 欄位包含預設URL，其中包含Adobe Sign資料庫分片。 URL 的格式是：

     `https://<shard>/public/oauth/v2`

     例如：
     `https://secure.na1.echosign.com/public/oauth/v2`

   * 此 **[!UICONTROL 存取記號URL]** 欄位包含預設URL，其中包含Adobe Sign資料庫分片。 URL 的格式是：

     `https://<shard>/oauth/v2/token`

     例如：
     `https://api.na1.echosign.com/oauth/v2/token`

   其中：

   **na1** 是指預設的資料庫分片。您可以修改資料庫分片的值。確保[!DNL  Adobe Acrobat Sign] Cloud Configurations 指向[正確的分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   >[!NOTE]
   >
   >* 保留 **建立Adobe Acrobat Sign設定** 頁面開啟。 不要關閉它。 您可以擷取 **使用者端ID** 和 **使用者端密碼** 為設定OAuth設定後 [!DNL Adobe Acrobat Sign] 應用程式，如未來步驟所述。
   > * 登入Adobe Sign帳戶後，請導覽至 **[!UICONTROL ACROBAT SIGN API]** > **[!UICONTROL API資訊]** > **[!UICONTROL REST API方法檔案]** > **[!UICONTROL OAuth存取權杖]** 以存取與Adobe Sign OAuth URL和存取記號URL相關的資訊。

1. 設定 [!DNL Adobe Acrobat Sign] 應用程式的 OAuth 設定：

   1. 開啟瀏覽器視窗並登入您的 [!DNL Adobe Acrobat Sign] 開發人員帳戶。
   1. 選取為設定的應用程式 [!DNL AEM Forms]，並選取 **[!UICONTROL 設定應用程式的OAuth]**.
   1. 在 **[!UICONTROL 重新導向URL]** 方塊，新增在上一步驟中複製的URL （步驟8）並按一下 **[!UICONTROL 儲存]**.
   1. 為以下專案啟用範圍： [!DNL Adobe Acrobat Sign] 應用程式並按一下 **[!UICONTROL 儲存]**.

   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   如需設定 [!DNL Adobe Acrobat Sign] 應用程式的 OAuth 設定並取得金鑰的逐步資訊，請參閱「[設定應用程式的 OAuth 設定](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)」開發人員文件。

   ![OAuth Config](/help/forms/assets/oauthconfig-new.png)

1. 返回 **[!UICONTROL 建立Adobe Acrobat Sign設定]** 頁面。 在 **[!UICONTROL 設定]** 索引標籤中，指定[**[!UICONTROL 使用者端ID]** （也稱為應用程式ID）和 **[!UICONTROL 使用者端密碼]**]。 使用 [Adobe Acrobat Sign應用程式的使用者端ID和使用者端密碼](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 您在上一步中建立的。

1. 選取 **[!UICONTROL 為附件啟用Adobe Acrobat Sign]** 將最適化表單附加的檔案附加至對應 [!DNL Adobe Acrobat Sign] 檔案已傳送供簽署。

1. 選取 **[!UICONTROL 連線至Adobe Acrobat Sign]**. 在系統提示輸入認證時，請提供 **使用者名稱** 和 **密碼** 建立時所使用的帳戶 [!DNL Adobe Acrobat Sign] 應用程式。 在系統要求您確認時，請存取 `your developer account`，按一下 **[!UICONTROL 允許存取]**. 如果認證正確且您允許 [!DNL AEM Forms] 存取您的 [!DNL Adobe Acrobat Sign] 開發人員帳戶，則會出現與以下訊息相似的成功訊息。

   ![Adobe Acrobat Sign雲端設定成功](assets/adobe-sign-cloud-configuration-success.png)

1. 選取 **[!UICONTROL 建立]** 以建立 [!DNL Adobe Acrobat Sign] 設定。

1. 選取設定並按一下 **[!UICONTROL 發佈]**，選取設定，然後按一下 **[!UICONTROL 發佈]**. 這會將設定複寫至對應的發佈環境。

1. 請對您的開發人員、中繼及生產執行個體 (無論是哪個) 重複上述步驟，以完成您環境的設定 [!DNL Adobe Acrobat Sign] with [!DNL AEM Forms]。

現在，您可以 [使用將Adobe Acrobat Sign欄位新增至最適化表單](working-with-adobe-sign.md). 請確保您將用於 Cloud Service 的設定容器新增至 [!DNL Adobe Acrobat Sign] 啟用的所有最適化表單。您可從最適化表單的屬性指定設定容器。

>[!NOTE]
>
> 若要設定Adobe Sign沙箱，您可以依照中說明的相同設定步驟操作 [Adobe Sign](#adobe-sign).

#### 疑難排解 {#resolve-config-error}

當您連線時 [!DNL Adobe Acrobat Sign] 替換為 [!DNL AEM Forms] 並尋找錯誤 `Unable to authorize access because the client configuration is invalid: invalid_request` 如下圖所示。 請依照下列步驟解決此問題：

![設定錯誤](/help/forms/assets/config_error_sign.png)

1. 將目前瀏覽器視窗中顯示的URL複製到記事本並移除部分 `/ui#/aem` 從URL.
1. 開啟瀏覽器視窗並登入您的 [!DNL Adobe Acrobat Sign] 開發人員帳戶。
1. 選取為設定的應用程式 [!DNL AEM Forms]，並選取 **[!UICONTROL 設定應用程式的OAuth]**.
1. 在 **[!UICONTROL 重新導向URL]** 方塊，新增在上一步中複製的URL並按一下 **[!UICONTROL 儲存]**.

## 連線適用於政府的AEM Forms與Adobe Acrobat Sign Solutions {#adobe-acrobat-sign-for-government}

將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線是多步驟流程。 其中涉及：

* 為您的AEM執行個體建立重新導向URL
* 與適用於政府團隊的Adobe Sign解決方案共用重新導向URL和範圍
* 接收來自Adobe Sign團隊的認證
* 使用收到的憑證將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線

![Adobe Sign政府工作流程](/help/forms/assets/adobe-acrobat-sign-govt-workflow.png)


AEM Formsas a Cloud Service提供開發、預備和生產環境。 您可以開始將的開發環境與適用於政府的Adobe Acrobat Sign Solutions連線，並在稍後連線預備和生產環境。

### 開始之前 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

開始將AEM Forms與Adobe Acrobat Sign解決方案連線之前，請確定 [適用於政府的Adobe Acrobat Sign Solutions](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) 已布建帳戶。


### 連線適用於政府的AEM Formsas a Cloud Service與Adobe Acrobat Sign Solutions {#connect-adobe-acrobat-sign-for-government}

#### 為您的AEM執行個體建立重新導向URL

1. 在Formsas a Cloud Service作者例項上，導覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**.
1. 在 **[!UICONTROL 設定瀏覽器]** 頁面，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定 **[!UICONTROL 標題]** 對於設定，啟用 **[!UICONTROL 雲端設定]**，並選取 **[!UICONTROL 建立]**. 這樣便會建立儲存Cloud Service的設定容器。 請確保資料夾名稱未含任何空格。
1. 瀏覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** 然後開啟您在上一步中建立的設定容器。 建立最適化表單時，請在 **[!UICONTROL 設定容器]** 欄位。
1. 在設定頁面上，選取 **[!UICONTROL 建立]** 以建立 [!DNL Adobe Acrobat Sign] AEM Forms中的設定。
1. 將您目前瀏覽器視窗的URL複製到記事本並移除 `/ui#/aem` 從URL. 此URL稱為 `re-direct URL`.
在下一個區段中，您共用 `re-direct URL` 和 `Scopes` Adobe Sign團隊並要求認證（使用者端ID和使用者端密碼）。

#### 與Adobe Sign團隊共用重新導向URL和範圍並接收認證

適用於政府解決方案的Adobe Acrobat Sign團隊需要 `re-direct URL` 和要為您的Adobe Acrobat Sign應用程式啟用的特定範圍（如下所列），以產生認證（使用者端ID和使用者端密碼），讓您將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線。

共用 `scopes` （如下所列）和 `re-direct URL` 建立並記錄上一節的最後一步，並請您的Adobe Acrobat Sign政府解決方案代表([Adobe Professional Services團隊成員](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password))。

**_範圍_**

* [!DNL aggrement_read]
* [!DNL aggrement_write]
* [!DNL aggrement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

代表會產生認證並與您共用。 在下一節中，您會使用認證（使用者端ID和使用者端密碼）來連線AEM Forms和適用於政府的Adobe Acrobat Sign Solutions。

#### 使用收到的認證連線AEM Forms與適用於政府的Adobe Acrobat Sign Solutions

1. 開啟 `re-direct URL` 在您的瀏覽器中。 您已建立並記下 `re-direct URL` 的最後一個步驟 [在您的AEM執行個體上建立重新導向URL](#create-a-redirect-url-for-your-aem-instance) 區段。

1. 在 **[!UICONTROL 一般]** 的標籤 **[!UICONTROL 建立Adobe Sign設定]** 頁面，指定 **[!UICONTROL 名稱]** ，然後選取 **[!UICONTROL 下一個]**. 您可以選擇指定 **[!UICONTROL 標題]** 並瀏覽以選取 **[!UICONTROL 縮圖]** 用於設定。 按一下「**[!UICONTROL 下一步]**」。

1. 在 **[!UICONTROL 設定]** 的標籤 **[!UICONTROL 建立Adobe Sign設定]** 頁面，針對 **[!UICONTROL 選取解決方案]** 選項，選取 [!DNL Adobe Acrobat Sign Solutions for Government].


   ![適用於政府的Adobe Acrobat Sign Solutions](assets/adobe-sign-for-govt.png)

1. 在 **[!UICONTROL 電子郵件]** 已歸檔，請為政府帳戶指定與您的Adobe Acrobat Sign Solutions相關聯的電子郵件地址。

1. 在 **[!UICONTROL 設定]** 標籤，
   * 此 **[!UICONTROL OAuth URL]** 欄位包含預設URL，其中包含Adobe Sign資料庫分片。 URL 的格式是：

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     例如：
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * 此 **[!UICONTROL 存取記號URL]** 欄位包含預設URL，其中包含Adobe Sign資料庫分片。 URL 的格式是：

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     例如：
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   其中：

   **na1** 是指預設的資料庫分片。您可以修改資料庫分片的值。確保[!DNL  Adobe Acrobat Sign] Cloud Configurations 指向[正確的分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   >[!NOTE]
   >
   > * 登入Adobe Sign帳戶後，請導覽至 **[!UICONTROL ACROBAT SIGN API]** > **[!UICONTROL API資訊]** > **[!UICONTROL REST API方法檔案]** > **[!UICONTROL OAuth存取權杖]** 以存取與Adobe Sign oAuth URL和存取記號URL相關的資訊。

1. 使用Adobe Acrobat Sign為政府解決方案代表共用的認證([Adobe Professional Services團隊成員])，在前一節中為[**[!UICONTROL 使用者端ID]** 和 **[!UICONTROL 使用者端密碼]**]。

1. 選取 **[!UICONTROL 為附件啟用Adobe Acrobat Sign]** 將最適化表單附加的檔案附加至對應 [!DNL Adobe Acrobat Sign] 檔案已傳送供簽署。

1. 選取 **[!UICONTROL 連線至Adobe Sign]**. 出現認證提示時，請提供在建立 [!DNL Adobe Acrobat Sign] 應用程式時使用的帳戶使用者名稱和密碼。當系統要求確認存取時 `your developer account`，按一下 **[!UICONTROL 允許存取]**. 如果認證正確且您允許 [!DNL AEM Forms] 存取您的 [!DNL Adobe Acrobat Sign] 開發人員帳戶，則會出現與以下訊息相似的成功訊息。

   ![Adobe Acrobat Sign雲端設定成功](assets/adobe-sign-cloud-configuration-success.png)

   <!-- > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. -->

1. 選取 **[!UICONTROL 建立]** 以建立設定。

1. 選取設定並按一下 **[!UICONTROL 發佈]**，選取設定，然後按一下 **[!UICONTROL 發佈]**. 這會將設定復寫至對應的發佈環境。

1. 請對您的開發人員、中繼及生產執行個體 (無論是哪個) 重複上述步驟，以完成您環境的設定 [!DNL Adobe Acrobat Sign Solutions for Government] with [!DNL AEM Forms]。

現在，您可以 [在最適化表單中使用新增Adobe Acrobat Sign欄位](working-with-adobe-sign.md) 或 [AEM工作流程](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). 請確定您將用於Cloud Service設定的設定容器新增至啟用的所有最適化Forms [!DNL Adobe Acrobat Sign]. 您可從最適化表單的屬性指定設定容器。

## 設定 [!DNL Adobe Acrobat Sign] 同步簽名狀態的排程器 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

AEM Formsas a Cloud Service提供排程器服務，可依定義的間隔檢查簽署者的狀態。 設定排程器服務的情境：

* 如果您使用 [提交表單（在每個收件者完成簽署儀式後）](/help/forms/working-with-adobe-sign.md#select-adobe-sign-cloud-service-and-signing-order) 若要簽署檔案，表格只會在所有簽署者簽署表格後才提交。
* 如果您使用 [AEM工作流程中的登入步驟](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step) 若要簽署檔案，在繼續工作流程的下一個步驟之前，簽署步驟會等待所有簽署者簽署檔案。

[!DNL Adobe Acrobat Sign] 排程器服務預設為每 24 小時檢查 (輪詢) 簽名者回應。您可以為您的環境變更預設間隔。

若要變更預設間隔，請指定 [cron運算式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 針對 **sign.status.exp** 的屬性 **Adobe Acrobat Sign設定服務** 設定。

例如，若要在每天凌晨00:00執行設定服務，請設定 **sign.status.exp** 的屬性 **Adobe Acrobat Sign設定服務** 要指定的設定 `0 0 0 1/1 * ? *`. 下列 JSON 檔案會顯示每日在午夜 12 點執行設定服務的範例：

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。


>[!MORELIKETHIS]
>
>* [使用手寫簽名對表單進行電子簽章](/help/forms/signing-forms-using-scribble.md)
>* [搭配最適化Forms使用Adobe Acrobat Sign的最佳做法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)