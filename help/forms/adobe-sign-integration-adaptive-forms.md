---
title: 如何整合Adobe Sign與AEM Forms?
description: 了解如何為 [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# 整合 [!DNL Adobe Sign] with [!DNL AEM Forms] as a Cloud Service  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 啟用適用性Forms的電子簽名工作流程。 電子簽名改進了處理法律、銷售、工資、人力資源管理等許多領域的文檔的工作流。

在 [!DNL Adobe Sign] 和適用性Forms案例，使用者會填入適用性表單以申請服務。 例如，信用卡申請和公民福利表。 當用戶填寫、提交和簽名申請表時，該表單被發送給服務提供商，以便採取進一步的行動。 服務提供商審核應用程式和使用 [!DNL Adobe Sign] 標籤已批准的應用程式。 若要啟用類似的電子簽名工作流程，您可以整合 [!DNL Adobe Sign] with [!DNL AEM Forms].

使用 [!DNL Adobe Sign] with [!DNL AEM Forms]，設定 [!DNL Adobe Sign] 在AEM雲端服務中：

## 必備條件 {#prerequisites}

您需要下列項目才能整合 [!DNL Adobe Sign] with [!DNL AEM Forms]:

* 活動 [Adobe Sign開發人員帳戶](https://acrobat.adobe.com/us/en/sign/developer-form.html).
* 安 [Adobe Sign API應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* 的憑證（用戶端ID和用戶端密碼） [!DNL Adobe Sign] API應用程式。
* 使用 [完全加密密鑰](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#make-sure-you-properly-replicate-encryption-keys-when-needed) 用於製作和發佈例項。
* （僅適用於政府ID型驗證） [啟用驗證方法](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) 用於政府ID驗證。

## 設定 [!DNL Adobe Sign] with [!DNL AEM Forms] {#configure-adobe-sign-with-aem-forms}

準備就緒後，請執行下列步驟以設定 [!DNL Adobe Sign] with [!DNL AEM Forms] 在Author例項上。

1. 在AEM Forms作者例項上，導覽至 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 配置瀏覽器]**.
1. 在 **[!UICONTROL 配置瀏覽器]** 頁面，點選 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立配置]** 對話框，指定 **[!UICONTROL 標題]** 若為設定，請啟用 **[!UICONTROL 雲端設定]**，然後點選 **[!UICONTROL 建立]**. 它會建立設定容器以儲存Cloud Services。 確保資料夾名稱不包含任何空格。
1. 導覽至 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** 並開啟您在上一步驟中建立的設定容器。

   >[!NOTE]
   >
   >建立適用性表單時，請在 **[!UICONTROL 組態容器]** 欄位。

1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign]設定(在AEM Forms中)。
1. 在 **[!UICONTROL 一般]** 的 **[!UICONTROL 建立Adobe Sign設定]** 頁面，指定 **[!UICONTROL 名稱]** ，然後點選 **[!UICONTROL 下一個]**. 您可以選擇指定 **[!UICONTROL 標題]** 並瀏覽以選取 **[!UICONTROL 縮圖]** ，以取得設定。

1. 將您目前瀏覽器視窗中的URL複製到記事本。 必須有URL才能設定 [!DNL Adobe Sign] 應用程式 [!DNL AEM Forms] 的URL。

1. 配置 [!DNL Adobe Sign] 應用程式：

   1. 開啟瀏覽器視窗並登入您的 [!DNL Adobe Sign] 開發人員帳戶。
   1. 選擇為配置的應用程式 [!DNL AEM Forms]，然後點選 **[!UICONTROL 為應用程式配置OAuth]**.
   1. 在 **[!UICONTROL 重新導向URL]** 框中，添加在上一步中複製的URL，然後按一下 **[!UICONTROL 儲存]**.
   1. 為啟用下列OAuth設定 [!DNL Adobe Sign] 應用程式和按一下 **[!UICONTROL 儲存]**.
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   如需設定 [!DNL Adobe Sign] 應用程式和取得索引鍵，請參閱 [配置應用程式的oAuth設定](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) 開發人員檔案。

   ![OAuth設定](assets/oauthconfig_new.png)

1. 返回 **[!UICONTROL 建立Adobe Sign設定]** 頁面。 在 **[!UICONTROL 設定]** 標籤 **[!UICONTROL OAuth URL]** 欄位提及預設URL。 URL的格式為：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 表示預設資料庫共用。 您可以修改資料庫共用的值。 確保 [!DNL Adobe Sign] 雲端設定指向 [正確分配](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   如果您建立其他 [!DNL Adobe Sign] Adobe Experience Manager功能或元件的設定，請確定 [!DNL Adobe Sign] 雲配置指向相同的分區。

1. 指定 **[!UICONTROL 用戶端ID]** （亦稱為應用程式ID）和 **[!UICONTROL 用戶端密碼]**. 使用您在上一步建立之Adobe Sign應用程式的用戶端ID和用戶端密碼。

1. 選取 **[!UICONTROL 啟用Adobe Sign以取得附件]** 將附加至適用性表單的檔案附加至對應 [!DNL Adobe Sign] 要簽名的文檔。

1. 點選 **[!UICONTROL 連線至Adobe Sign]**. 提示輸入憑證時，請提供建立時使用之帳戶的使用者名稱和密碼 [!DNL Adobe Sign] 應用程式。 當要求確認 `your developer account`，按一下 **[!UICONTROL 允許存取]**. 如果憑證正確，且您允許 [!DNL AEM Forms] 訪問 [!DNL Adobe Sign] 開發人員帳戶中顯示類似下列的成功訊息。

   ![Adobe Sign雲端設定成功](assets/adobe-sign-cloud-configuration-success.png)

1. 點選 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] 設定。

1. 選取設定，然後按一下 **[!UICONTROL 發佈]**，選取設定，然後按一下 **[!UICONTROL 發佈]**. 它會將配置複製到相應的發佈環境。

1. 在您的開發人員、預備和生產執行個體（以左側為準）上重複上述所有步驟，以完成設定 [!DNL Adobe Sign] with [!DNL AEM Forms] 為您的環境。

現在，你可以 [將Adobe Sign欄位新增至最適化表單](working-with-adobe-sign.md). 請確定您將用於Cloud Service的設定容器新增至所有已啟用的適用性Forms [!DNL Adobe Sign]. 您可以從最適化表單的屬性中指定設定容器。

## (僅限AEM工作流程)設定 [!DNL Adobe Sign] 同步簽名狀態的調度程式 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

使用 [!DNL Adobe Sign] 簽署最適化表單的工作流程步驟，表單可逐一傳遞給簽署者，或根據工作流程步驟的設定同時傳送給所有簽署者。 [!DNL Adobe Sign] 啟用的Adaptive Forms只有在所有簽署者完成簽署程式後，才會提交至Experience Manager Forms伺服器。

依預設， [!DNL Adobe Sign] 排程器服務每24小時會檢查（輪詢）簽署者回應。 您可以變更環境的預設間隔。

若要變更預設間隔，請指定 [cron表達](https://en.wikipedia.org/wiki/Cron#CRON_expression) 針對 **sign.status.exp** 屬性 **Adobe Sign設定服務** 設定。

例如，若要每天00:00 am執行設定服務，請設定 **sign.status.exp** 屬性 **Adobe Sign設定服務** 指定的配置 `0 0 0 1/1 * ? *`. 下列JSON檔案顯示每日00:00 am運行配置服務的示例：

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

若要設定的值， [使用AEM SDK產生OSGi設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，和 [部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) 至您的Cloud Service例項。

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## 相關文章 {#related-articles}

* [在適用性表單中使用Adobe Sign](working-with-adobe-sign.md)

* [將Adobe Sign與最適化Forms搭配使用的最佳作法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
