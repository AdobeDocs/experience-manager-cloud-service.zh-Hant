---
title: 如何將Adobe Acrobat Sign與AEM Forms整合？
description: 瞭解如何為 [!DNL AEM Forms] as a Cloud Service設定Adobe Acrobat Sign？
feature: Adaptive Forms, Acrobat Sign
role: Admin, User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 22%

---

# 連線[!DNL AEM Forms] as a Cloud Service與[!DNL Adobe Acrobat Sign] {#integrate-adobe-sign-with-aem-forms}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms.html?lang=zh-Hant#adobe-acrobat-sign-for-government) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Acrobat Sign]可啟用最適化Forms和AEM工作流程的電子簽章工作流程。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在標準 [!DNL Adobe Acrobat Sign] 和最適化表單情境下，用戶會填寫最適化表單來申請服務。例如，信用卡申請表和市民福利表單。用戶申請、提交和簽署申請表單時，此表單會被傳送給服務提供者，以進一步動作。服務提供者便會審查申請並使用 [!DNL Adobe Acrobat Sign] 標記已核准申請。AEM Forms同時支援適用於政府的Adobe Acrobat Sign和Adobe Acrobat Sign Solutions。 根據您的授權和需求，您可以將AEM Forms與以下任一解決方案整合或連線：

* [連結AEM Forms與Adobe Acrobat Sign](#adobe-sign)
* [連線適用於政府的AEM Forms與Adobe Acrobat Sign Solutions](#adobe-acrobat-sign-for-government)

## 連結AEM Forms與Adobe Acrobat Sign {#adobe-sign}

若要將&#x200B;**[!DNL AEM Forms]**&#x200B;與&#x200B;**[!DNL Adobe Acrobat Sign]**&#x200B;連線，請設定先決條件區段中列出的軟體和帳戶，並在您的Forms as a Cloud Service製作和發佈執行個體中設定Adobe Sign Cloud Service：

### 連線AEM Forms與Adobe Acrobat Sign的先決條件 {#prerequisites-for-adobe-sign}

您需要下列安裝程式才能將[!DNL Adobe Acrobat Sign]與[!DNL AEM Forms]整合：

1. 有效的[Adobe Acrobat Sign開發人員帳戶。](https://www.adobe.com/acrobat/business/developer-form.html)
1. [Adobe Acrobat Sign API應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
1. [!DNL Adobe Acrobat Sign] API 應用程式的認證 (用戶端 ID 和用戶端密碼)。
1. （僅適用於政府機關身分證件驗證） [為政府機關身分證件驗證啟用驗證方法](https://helpx.adobe.com/tw/sign/using/adobesign-authentication-government-id.html#AuditReport)。

### 連結AEM Forms製作和發佈執行個體與Adobe Acrobat Sign {#configure-adobe-sign-with-aem-forms}

已具備下列先決條件後，請執行以下步驟，以在作者執行個體上設定 [!DNL Adobe Acrobat Sign] 和 [!DNL AEM Forms]。

1. 在AEM Forms作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]** ![hammer](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**。
1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立設定]**&#x200B;對話方塊中，指定設定的&#x200B;**[!UICONTROL 標題]**、啟用&#x200B;**[!UICONTROL 雲端設定]**，並選取&#x200B;**[!UICONTROL 建立]**。 這樣便會建立儲存 Cloud Services 的設定容器。請確保資料夾名稱未含任何空格。
1. 瀏覽至&#x200B;**[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL Adobe Acrobat Sign]**，並開啟您在上一步中建立的設定容器。

   >[!NOTE]
   >
   >建立最適化表單時，請在&#x200B;**[!UICONTROL 設定容器]**&#x200B;欄位中指定容器名稱。

1. 在設定頁面上，選取「**[!UICONTROL 建立]**」以在AEM Forms中建立[!DNL Adobe Acrobat Sign]設定。
1. 在&#x200B;**[!UICONTROL 建立Adobe Acrobat Sign組態]**&#x200B;頁面的&#x200B;**[!UICONTROL 一般]**&#x200B;標籤中，指定組態的&#x200B;**[!UICONTROL 名稱]**，並選取&#x200B;**[!UICONTROL 下一步]**。 您可以選擇指定&#x200B;**[!UICONTROL 標題]**&#x200B;並瀏覽以選取設定的&#x200B;**[!UICONTROL 縮圖]**。

1. 現在您可以&#x200B;**[!UICONTROL 選取方案]**&#x200B;以選取[!DNL Adobe Acrobat Sign]。

   <!--![Adobe Acrobat Sign Solutions](assets/adobe-sign-solution.png)-->
   ![Adobe Acrobat Sign Solutions設定](assets/adobe-sign-solution-config.png)

<!--

[create URL](#create-a-redirect-url-for-your-aem-instance)
 -->

1. 將您目前瀏覽器視窗中顯示的URL複製到記事本，並從URL移除部分`/ui#/aem`。 在稍後步驟中，需要修改過的URL才能使用[!DNL Adobe Acrobat Sign]設定[!DNL AEM Forms]應用程式。 選取&#x200B;**[!UICONTROL 「下一步」]**。

1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中，
   * **[!UICONTROL OAuth URL]**&#x200B;欄位包含預設URL，其中包含Adobe Sign資料庫分片。 URL 的格式是：

     `https://<shard>/public/oauth/v2`

     例如：
     `https://secure.na1.echosign.com/public/oauth/v2`

   * **[!UICONTROL 存取權杖URL]**&#x200B;欄位包含預設URL，其中包含Adobe Sign資料庫分片。 URL 的格式是：

     `https://<shard>/oauth/v2/token`

     例如：
     `https://api.na1.echosign.com/oauth/v2/token`

   其中：

   **na1** 是指預設的資料庫分片。您可以修改資料庫分片的值。確保[!DNL &#x200B; Adobe Acrobat Sign] Cloud Configurations 指向[正確的分片](https://helpx.adobe.com/tw/sign/using/identify-account-shard.html)。

   >[!NOTE]
   >
   >* 保持&#x200B;**建立Adobe Acrobat Sign設定**&#x200B;頁面開啟。 不要關閉它。 在設定&#x200B;**應用程式的OAuth設定後，您可以擷取**&#x200B;使用者端識別碼&#x200B;**和**&#x200B;使用者端密碼[!DNL Adobe Acrobat Sign]，如即將進行的步驟所述。
   > * 登入您的Adobe Sign帳戶後，請瀏覽至&#x200B;**[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API資訊]** > **[!UICONTROL REST API方法檔案]** > **[!UICONTROL OAuth存取Token]**，以存取與Adobe Sign OAuth URL和存取權杖URL相關的資訊。

1. 設定 [!DNL Adobe Acrobat Sign] 應用程式的 OAuth 設定：

   1. 開啟瀏覽器視窗並登入您的 [!DNL Adobe Acrobat Sign] 開發人員帳戶。
   1. 選取為[!DNL AEM Forms]設定的應用程式，然後選取&#x200B;**[!UICONTROL 設定應用程式的OAuth]**。
   1. 在&#x200B;**[!UICONTROL 重新導向URL]**&#x200B;方塊中，新增在上一步驟中複製的URL （步驟8），然後按一下&#x200B;**[!UICONTROL 儲存]**。
   1. 為[!DNL Adobe Acrobat Sign]應用程式啟用下列範圍，然後按一下&#x200B;**[!UICONTROL 儲存]**。

   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   >[!NOTE]
   > 您可以直接從AEM UI將範圍修飾元從`self`變更為`account`，如步驟12中所述。

   如需設定 [!DNL Adobe Acrobat Sign] 應用程式的 OAuth 設定並取得金鑰的逐步資訊，請參閱「[設定應用程式的 OAuth 設定](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)」開發人員文件。

   ![OAuth Config](/help/forms/assets/oauthconfig-new.png)

1. 返回&#x200B;**[!UICONTROL 建立Adobe Acrobat Sign設定]**&#x200B;頁面。 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中，指定[**[!UICONTROL 使用者端識別碼]** （也稱為應用程式識別碼）和&#x200B;**[!UICONTROL 使用者端密碼]**]。 使用您在上一步建立的Adobe Acrobat Sign應用程式[的](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret)使用者端ID和使用者端密碼。

1. 在[!UICONTROL 授權範圍]區段中，您可以視需要將前置詞「self」或「account」新增至範圍，將範圍修改為「account」或「self」。
   ![授權範圍](/help/forms/assets/authorization-scope.png)

1. 選取&#x200B;**[!UICONTROL 為附件啟用Adobe Acrobat Sign]**&#x200B;選項，以將最適化表單附加的檔案附加至要簽名的對應[!DNL Adobe Acrobat Sign]檔案。

1. 選取&#x200B;**[!UICONTROL 連線至Adobe Acrobat Sign]**。 出現認證提示時，請提供建立&#x200B;**應用程式時所使用帳戶的**&#x200B;使用者名稱&#x200B;**和**&#x200B;密碼[!DNL Adobe Acrobat Sign]。 當要求確認時，請按一下`your developer account`的存取權，然後按一下&#x200B;**[!UICONTROL 允許存取權]**。 如果認證正確且您允許 [!DNL AEM Forms] 存取您的 [!DNL Adobe Acrobat Sign] 開發人員帳戶，則會出現與以下訊息相似的成功訊息。

   ![Adobe Acrobat Sign雲端設定成功](assets/adobe-sign-cloud-configuration-success.png)

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立[!DNL Adobe Acrobat Sign]組態。

1. 選取組態並按一下&#x200B;**[!UICONTROL 發佈]**，選取組態，然後按一下&#x200B;**[!UICONTROL 發佈]**。 這會將設定複寫至對應的發佈環境。

1. 請對您的開發人員、中繼及生產執行個體 (無論是哪個) 重複上述步驟，以完成您環境的設定 [!DNL Adobe Acrobat Sign] with [!DNL AEM Forms]。

現在您可以[使用新增Adobe Acrobat Sign欄位至最適化表單](working-with-adobe-sign.md)。 請確保您將用於 Cloud Service 的設定容器新增至 [!DNL Adobe Acrobat Sign] 啟用的所有最適化表單。您可從最適化表單的屬性指定設定容器。

>[!NOTE]
>
> 若要設定Adobe Sign沙箱，您可以依照[Adobe Sign](#adobe-sign)中說明的相同設定步驟操作。

#### 疑難排解 {#resolve-config-error}

當您連線[!DNL Adobe Acrobat Sign]與[!DNL AEM Forms]並尋找錯誤`Unable to authorize access because the client configuration is invalid: invalid_request`時，如下圖所示。 請依照下列步驟解決此問題：

![設定錯誤](/help/forms/assets/config_error_sign.png)

1. 將您目前瀏覽器視窗中顯示的URL複製到記事本，並從URL移除部分`/ui#/aem`。
1. 開啟瀏覽器視窗並登入您的 [!DNL Adobe Acrobat Sign] 開發人員帳戶。
1. 選取為[!DNL AEM Forms]設定的應用程式，然後選取&#x200B;**[!UICONTROL 設定應用程式的OAuth]**。
1. 在&#x200B;**[!UICONTROL 重新導向URL]**&#x200B;方塊中，新增先前步驟中複製的URL，然後按一下&#x200B;**[!UICONTROL 儲存]**。

## 連線適用於政府的AEM Forms與Adobe Acrobat Sign Solutions {#adobe-acrobat-sign-for-government}

將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線是多步驟流程。 其中涉及：

* 為您的AEM執行個體建立重新導向URL
* 與政府團隊的Adobe Sign解決方案共用重新導向URL和範圍
* 接收來自Adobe Sign團隊的認證
* 使用收到的憑證將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線

![Adobe Sign政府工作流程](/help/forms/assets/adobe-acrobat-sign-govt-workflow.png)


AEM Forms as a Cloud Service提供開發、預備和生產環境。 您可以開始將的開發環境與適用於政府的Adobe Acrobat Sign Solutions連線，並在稍後連線預備和生產環境。

### 開始之前 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

開始將AEM Forms與Adobe Acrobat Sign解決方案連線之前，請確定已布建您的[Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning)帳戶。


### 連線適用於政府的AEM Forms as a Cloud Service與Adobe Acrobat Sign Solutions {#connect-adobe-acrobat-sign-for-government}

#### 為您的AEM執行個體建立重新導向URL

1. 在Forms as a Cloud Service作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**。
1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立設定]**&#x200B;對話方塊中，指定設定的&#x200B;**[!UICONTROL 標題]**、啟用&#x200B;**[!UICONTROL 雲端設定]**，並選取&#x200B;**[!UICONTROL 建立]**。 這樣便會建立儲存Cloud Services的設定容器。 請確保資料夾名稱未含任何空格。
1. 瀏覽至&#x200B;**[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL Adobe Acrobat Sign]**，並開啟您在上一步中建立的設定容器。 建立最適化表單時，請在&#x200B;**[!UICONTROL 設定容器]**&#x200B;欄位中指定容器名稱。
1. 在設定頁面上，選取「**[!UICONTROL 建立]**」以在AEM Forms中建立[!DNL Adobe Acrobat Sign]設定。
1. 將您目前瀏覽器視窗的URL複製到記事本，並從URL中移除`/ui#/aem`。 此URL稱為`re-direct URL`。
在下一個區段中，您與Adobe Sign團隊共用`re-direct URL`和`Scopes`並請求認證（使用者端ID和使用者端密碼）。

#### 與Adobe Sign團隊共用重新導向URL和範圍並接收認證

適用於政府的Adobe Acrobat Sign解決方案團隊需要為您的Adobe Acrobat Sign應用程式（如下所列）啟用`re-direct URL`和某些範圍，才能產生認證（使用者端ID和使用者端密碼），讓您將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線。

與您的Adobe Acrobat Sign政府解決方案代表(`scopes`Adobe Professional Services團隊成員`re-direct URL`)共用[ （如下所列），以及建立並記下上一節的最後一步的](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password)。

**_領域_**

* [!DNL aggrement_read]
* [!DNL aggrement_write]
* [!DNL aggrement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

代表會產生認證並與您共用。 在下一節中，您會使用認證（使用者端ID和使用者端密碼）來連線AEM Forms和適用於政府的Adobe Acrobat Sign Solutions。

#### 使用收到的認證連線AEM Forms與適用於政府的Adobe Acrobat Sign Solutions

1. 在瀏覽器中開啟`re-direct URL`。 您在`re-direct URL`在您的AEM執行個體[區段上建立重新導向URL的最後一步中建立並記下](#create-a-redirect-url-for-your-aem-instance)。

1. 在&#x200B;**[!UICONTROL 建立Adobe Sign組態]**&#x200B;頁面的&#x200B;**[!UICONTROL 一般]**&#x200B;標籤中，指定組態的&#x200B;**[!UICONTROL 名稱]**，並選取&#x200B;**[!UICONTROL 下一步]**。 您可以選擇指定&#x200B;**[!UICONTROL 標題]**&#x200B;並瀏覽以選取設定的&#x200B;**[!UICONTROL 縮圖]**。 按一下「**[!UICONTROL 下一步]**」。

1. 在&#x200B;**[!UICONTROL 建立Adobe Sign組態]**&#x200B;頁面的&#x200B;**[!UICONTROL 設定]**&#x200B;標籤中，針對&#x200B;**[!UICONTROL 選取方案]**&#x200B;選項，選取[!DNL Adobe Acrobat Sign Solutions for Government]。


   政府用![Adobe Acrobat Sign Solutions](assets/adobe-sign-for-govt.png)

1. 在&#x200B;**[!UICONTROL 電子郵件]**&#x200B;欄位中，指定與您Adobe Acrobat Sign Solutions政府帳戶相關的電子郵件地址。

1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中，
   * **[!UICONTROL OAuth URL]**&#x200B;欄位包含預設URL，其中包含Adobe Sign資料庫分片。 URL 的格式是：

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     例如：
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * **[!UICONTROL 存取權杖URL]**&#x200B;欄位包含預設URL，其中包含Adobe Sign資料庫分片。 URL 的格式是：

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     例如：
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   其中：

   **na1** 是指預設的資料庫分片。您可以修改資料庫分片的值。確保[!DNL &#x200B; Adobe Acrobat Sign] Cloud Configurations 指向[正確的分片](https://helpx.adobe.com/tw/sign/using/identify-account-shard.html)。

   >[!NOTE]
   >
   > * 登入您的Adobe Sign帳戶後，請瀏覽至&#x200B;**[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API資訊]** > **[!UICONTROL REST API方法檔案]** > **[!UICONTROL OAuth存取Token]**，以存取與Adobe Sign oAuth URL和存取權杖URL相關的資訊。

1. 在上一節中，將Adobe Acrobat Sign為政府解決方案代表([Adobe Professional Services團隊成員])共用的認證用作[**[!UICONTROL 使用者端識別碼]**&#x200B;和&#x200B;**[!UICONTROL 使用者端密碼]**]。

1. 選取&#x200B;**[!UICONTROL 為附件啟用Adobe Acrobat Sign]**&#x200B;選項，以將最適化表單附加的檔案附加至要簽名的對應[!DNL Adobe Acrobat Sign]檔案。

1. 選取&#x200B;**[!UICONTROL 連線至Adobe Sign]**。 出現認證提示時，請提供在建立 [!DNL Adobe Acrobat Sign] 應用程式時使用的帳戶使用者名稱和密碼。當要求確認`your developer account`的存取時，請按一下&#x200B;**[!UICONTROL 允許存取]**。 如果認證正確且您允許 [!DNL AEM Forms] 存取您的 [!DNL Adobe Acrobat Sign] 開發人員帳戶，則會出現與以下訊息相似的成功訊息。

   ![Adobe Acrobat Sign雲端設定成功](assets/adobe-sign-cloud-configuration-success.png)

   <!-- 
      > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. 
      -->

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立組態。

1. 選取組態並按一下&#x200B;**[!UICONTROL 發佈]**，選取組態，然後按一下&#x200B;**[!UICONTROL 發佈]**。 這會將設定復寫至對應的發佈環境。

1. 請對您的開發人員、中繼及生產執行個體 (無論是哪個) 重複上述步驟，以完成您環境的設定 [!DNL Adobe Acrobat Sign Solutions for Government] with [!DNL AEM Forms]。

現在，您可以[在最適化表單中新增Adobe Acrobat Sign欄位](working-with-adobe-sign.md)或[AEM工作流程](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)。 請確定您將用於Cloud Service設定的設定容器新增至為[!DNL Adobe Acrobat Sign]啟用的所有最適化Forms。 您可從最適化表單的屬性指定設定容器。

## 設定[!DNL Adobe Acrobat Sign]排程器以同步處理簽署狀態 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

AEM Forms as a Cloud Service提供排程器服務，可依定義的間隔檢查簽署者的狀態。 設定排程器服務的情境：

* 如果您使用[提交表單（在每個收件者完成簽署儀式後）](/help/forms/working-with-adobe-sign.md#select-adobe-sign-cloud-service-and-signing-order)來簽署檔案，則表單只會在所有簽署者簽署表單後提交。
* 如果您使用AEM工作流程中的[簽署步驟](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step)來簽署檔案，則簽署步驟會等待所有簽署者簽署檔案，再繼續工作流程的下一個步驟。

[!DNL Adobe Acrobat Sign] 排程器服務預設為每 24 小時檢查 (輪詢) 簽名者回應。您可以為您的環境變更預設間隔。

若要變更預設間隔，請為[Adobe Acrobat Sign組態服務](https://en.wikipedia.org/wiki/Cron#CRON_expression)組態的&#x200B;**sign.status.exp**&#x200B;屬性指定&#x200B;**cron運算式**。

例如，若要在每日午夜12點執行組態服務，請設定:00Adobe Acrobat Sign Configuration Service **組態的** sign.status.exp **屬性，以指定**。 `0 0 0 1/1 * ? *`下列JSON檔案顯示每天凌晨00:00執行設定服務的範例：

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

若要設定值，請[使用 AEM SDK 產生 OSGi 設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hant#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並[將設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant#deployment-process)您的 Cloud Service 執行個體。

## 常見問題

* **問：我是否可以在iframe中轉譯Adobe Sign GovCloud簽章頁面？**
* **A：**&#x200B;是，您可以在iframe中轉譯Adobe Sign GovCloud簽章頁面。

>[!MORELIKETHIS]
>
>* [使用手寫簽名對表單進行電子簽章](/help/forms/signing-forms-using-scribble.md)
>* [搭配最適化Forms使用Adobe Acrobat Sign的最佳做法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
