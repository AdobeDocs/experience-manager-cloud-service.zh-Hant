---
title: 如何將 Adobe Sign 與 AEM Forms 整合？
description: 了解如何設定  [!DNL AEM Forms] as a Cloud Service 的 Adobe Sign？
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 75%

---

# 將 [!DNL Adobe Sign] 與 [!DNL AEM Forms] as a Cloud Service 整合  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 可啟用最適化表單的電子簽名工作流程。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在標準 [!DNL Adobe Sign] 和最適化表單情境下，用戶會填寫最適化表單來申請服務。例如，信用卡申請表和市民福利表單。用戶申請、提交和簽署申請表單時，此表單會被傳送給服務提供者，以進一步動作。服務提供者便會審查申請並使用 [!DNL Adobe Sign] 標記已核准申請。若要啟用相似的電子簽名工作流程，您可以將 [!DNL Adobe Sign] 與 [!DNL AEM Forms] 整合。

若要使用 [!DNL Adobe Sign] 和 [!DNL AEM Forms]，請設定 AEM Cloud Services 中的 [!DNL Adobe Sign]：

## 必備條件 {#prerequisites}

您需要以下項目才能將 [!DNL Adobe Sign] 與 [!DNL AEM Forms] 整合：

* 主要 [Adobe Sign 開發人員帳戶](https://acrobat.adobe.com/us/en/sign/developer-form.html).
* [Adobe Sign API 應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* [!DNL Adobe Sign] API 應用程式的認證 (用戶端 ID 和用戶端密碼)。
* 使用製作和發佈執行個體的[同一密碼編譯金鑰](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#make-sure-you-properly-replicate-encryption-keys-when-needed)。
* (僅適用於政府機關身分證件驗證) [啟用適用於政府機關身分證件驗證的驗證方法](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport)。

## 設定 [!DNL Adobe Sign] 和 [!DNL AEM Forms] {#configure-adobe-sign-with-aem-forms}

已具備下列先決條件後，請執行以下步驟，以在作者執行個體上設定 [!DNL Adobe Sign] 和 [!DNL AEM Forms]。

1. 在AEM Forms作者實例上，導航到 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL 常規]** > **[!UICONTROL 配置瀏覽器]**。
1. 在 **[!UICONTROL 配置瀏覽器]** 頁面，點擊 **[!UICONTROL 建立]**。
1. 在 **[!UICONTROL 建立配置]** 對話框，指定 **[!UICONTROL 標題]** 對於配置，啟用 **[!UICONTROL 雲配置]**，然後點擊 **[!UICONTROL 建立]**。 這樣便會建立儲存 Cloud Services 的設定容器。請確保資料夾名稱未含任何空格。
1. 導航到 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** 並開啟在上一步中建立的配置容器。

   >[!NOTE]
   >
   >建立自適應表單時，在 **[!UICONTROL 配置容器]** 的子菜單。

1. 在配置頁上，點擊 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign]配置在AEM Forms。
1. 在 **[!UICONTROL 常規]** 頁籤 **[!UICONTROL 建立Adobe Sign配置]** 頁，指定 **[!UICONTROL 名稱]** ，然後點擊 **[!UICONTROL 下一個]**。 您可以選擇指定 **[!UICONTROL 標題]** 並瀏覽以選擇 **[!UICONTROL 縮略圖]** 的子菜單。

1. 將您目前瀏覽器視窗中的 URL 複製到筆記本。在後續步驟中，需要使用此 URL 設定 [!DNL Adobe Sign] 應用程式和 [!DNL AEM Forms]。

1. 設定 [!DNL Adobe Sign] 應用程式的 OAuth 設定：

   1. 開啟瀏覽器視窗並登入您的 [!DNL Adobe Sign] 開發人員帳戶。
   1. 選擇為 [!DNL AEM Forms]，然後點擊 **[!UICONTROL 為應用程式配置OAuth]**。
   1. 在 **[!UICONTROL 重定向URL]** 框中，添加上一步中複製的URL，然後按一下 **[!UICONTROL 保存]**。
   1. 為 [!DNL Adobe Sign] 應用程式，按一下 **[!UICONTROL 保存]**。
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   如需設定 [!DNL Adobe Sign] 應用程式的 OAuth 設定並取得金鑰的逐步資訊，請參閱「[設定應用程式的 OAuth 設定](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)」開發人員文件。

   ![OAuth Config](assets/oauthconfig_new.png)

1. 返回 **[!UICONTROL 建立Adobe Sign配置]** 的子菜單。 在 **[!UICONTROL 設定]** 頁籤 **[!UICONTROL OAuth URL]** 欄位中提到預設URL。 URL 的格式是：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 是指預設的資料庫分片。您可以修改資料庫分片的值。確保[!DNL Adobe Sign] Cloud Configurations 指向[正確的分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   如果您建立 Adobe Experience Manager 功能或元件的另一個 [!DNL Adobe Sign] 設定請確保所有 [!DNL Adobe Sign] Cloud Configurations 都指向相同分片。

1. 指定 **[!UICONTROL 客戶端ID]** （也稱為應用程式ID）和 **[!UICONTROL 客戶端密碼]**。 使用您在上一步建立的 Adobe Sign 應用程式的用戶端 ID 和用戶端密碼。

1. 選擇 **[!UICONTROL 為附件啟用Adobe Sign]** 選項，將附加到自適應窗體的檔案附加到相應的 [!DNL Adobe Sign] 文檔已發送以進行簽名。

1. 點擊 **[!UICONTROL 連接到Adobe Sign]**。 出現認證提示時，請提供在建立 [!DNL Adobe Sign] 應用程式時使用的帳戶使用者名稱和密碼。當要求確認訪問 `your developer account`，按一下 **[!UICONTROL 允許訪問]**。 如果認證正確且您允許 [!DNL AEM Forms] 存取您的 [!DNL Adobe Sign] 開發人員帳戶，則會出現與以下訊息相似的成功訊息。

   ![Adobe Sign 雲端設定成功](assets/adobe-sign-cloud-configuration-success.png)

1. 點擊 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] 配置。

1. 選擇配置並按一下 **[!UICONTROL 發佈]**，選擇配置，然後按一下 **[!UICONTROL 發佈]**。 這會將設定複寫至對應的發佈環境。

1. 請對您的開發人員、中繼及生產執行個體 (無論是哪個) 重複上述步驟，以完成您環境的設定 [!DNL Adobe Sign] with [!DNL AEM Forms]。

現在您可以 [新增 Adobe Sign 欄位至最適化表單](working-with-adobe-sign.md)。請確保您將用於 Cloud Service 的設定容器新增至 [!DNL Adobe Sign] 啟用的所有最適化表單。您可從最適化表單的屬性指定設定容器。

## (僅適用於 AEM 工作流程) 設定 [!DNL Adobe Sign] 排程器以同步簽名狀態 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

當您使用 [!DNL Adobe Sign] 工作流程步驟在最適化表單上簽名時，視工作流程設定步驟而定，此表單可以在簽名者之間逐一傳遞，或同時傳送給所有簽名者。啟用 [!DNL Adobe Sign] 的最適化表單只會在所有簽名者完成簽名程序後提交給 Experience Manager Forms 伺服器。

[!DNL Adobe Sign] 排程器服務預設為每 24 小時檢查 (輪詢) 簽名者回應。您可以為您的環境變更預設間隔。

若要變更預設間隔，請為 **Adobe Sign Configuration Service** 的 **sign.status.exp** 屬性指定 [cron 運算式](https://en.wikipedia.org/wiki/Cron#CRON_expression)。

例如，若要在每日午夜 12 點執行設定服務，請設定 **Adobe Sign Configuration Service** 的 **sign.status.exp** 屬性，以指定 `0 0 0 1/1 * ? *`。下列 JSON 檔案會顯示每日在午夜 12 點執行設定服務的範例：

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## 相關文章 {#related-articles}

* [在最適化表單中使用 Adobe Sign in](working-with-adobe-sign.md)

* [搭配最適化表單使用 Adobe Sign 的最佳做法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
