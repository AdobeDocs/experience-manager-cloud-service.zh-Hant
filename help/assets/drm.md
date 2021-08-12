---
title: Digital Rights Management [!DNL Assets]
description: 了解如何在 [!DNL Experience Manager] as a [!DNL Cloud Service]中管理授權資產的資產到期狀態和資訊。
contentOwner: AG
feature: 資產管理，DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: f993148a9f678cfdaf0693e4964f02b9163cf2ff
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 2%

---

# Digital Rights Management數位資產 {#digital-rights-management-in-assets}

數位資產通常與指定使用條款和持續時間的授權相關聯。 使用[!DNL Experience Manager]平台，您可以有效管理資產到期資訊和授權資訊。

## 資產過期 {#asset-expiration}

若要強制執行資產的授權要求，請使用資產到期資訊。 到期資訊可確保已發佈的資產在到期時取消發佈，從而防止違反許可證。 沒有管理員權限的使用者無法編輯、複製、移動、發佈和下載過期的資產。

您可以在下列位置檢視資產的到期狀態：

* **卡片檢視**:對於過期的資產，卡片上的標幟會指出其已過期。
* **清單檢視**:對於過期的資產，「狀態」 **** 欄會顯示「過期 **** 橫幅」。
* **時間表**:您可以在時間軸中檢視資產的到期狀態。選取資產，然後選擇「時間軸」。
* **參考邊欄**:您也可以在「參考」邊欄中檢視資產的到期 **** 狀態。它可管理複合資產與參考的子資產、集合和專案之間的資產到期狀態和關係。

若要檢視參考網頁和資產的複合資產，請執行下列步驟：

1. 導覽至資產，選取資產，然後按一下![左側邊欄內容參考圖示](assets/do-not-localize/content-rail-icon.png)。 左側邊欄隨即開啟。
1. 從左側邊欄選取&#x200B;**[!UICONTROL 參考]**。
1. 對於過期的資產，[!UICONTROL References]會將到期狀態顯示為&#x200B;**[!UICONTROL Asset is Expired]**。 如果資產已過期的子資產，[!UICONTROL 參考]邊欄會顯示狀態&#x200B;**[!UICONTROL 資產已過期的子資產]**。

### 搜尋過期的資產 {#search-expired-assets}

若要搜尋過期的資產（包括過期的子資產），請執行下列步驟：

1. 在[!DNL Assets]控制台中，按一下工具欄中的&#x200B;**[!UICONTROL 搜索]**，然後按`Enter`。

1. 按一下GlobalNav表徵圖並選擇&#x200B;**[!UICONTROL Expiry Status]**&#x200B;選項。

1. 選擇&#x200B;**[!UICONTROL Expired]**。 搜尋結果會顯示過期的資產。

當您選擇&#x200B;**[!UICONTROL Expired]**&#x200B;選項時，[!DNL Assets]主控台只會顯示複合資產參照的過期資產和子資產。 參考過期子資產的複合資產，不會在子資產過期後立即顯示。 而是會在[!DNL Experience Manager]偵測到它們在下次排程器執行時參考過期的子資產後顯示。

您可以將已發佈資產的到期日修改為早於目前排程器週期的日期。 不過，排程在下次執行時仍會偵測到這類資產是否為過期資產，且[!DNL Experience Manager]會反映其報表中的狀態。 不同時區的使用者會以不同方式顯示資產的到期日。

此外，如果錯誤使排程器無法偵測目前週期中的過期資產，則排程器會在下一個週期中重新檢查這些資產，並偵測其過期狀態。

若要啟用[!DNL Assets]主控台以顯示參考的複合資產以及過期的子資產，請在[!DNL Experience Manager]中設定&#x200B;**[!UICONTROL Adobe CQ DAM Expiry Notification]**&#x200B;工作流程。 以時間為基礎的排程器會排程工作，以在特定時間檢查資產是否已過期的子資產。 作業完成後，過期的子資產和參考資產的資產會在搜尋結果中顯示為過期。

1. 存取與您環境相關聯的[!DNL Cloud Manager] Git存放庫。
1. 提交儲存庫中名為`com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json`的檔案，其中包含以下內容。

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. 按照[如何在 [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md)中配置OSGi的說明操作。

您可以使用下列屬性來設定排程器：

* 屬性`cq.dam.expiry.notification.scheduler.istimebased`的`true`值啟動調度程式。 *屬性`cq.dam.expiry.notification.scheduler.timebased.rule`的值是定義時間的規則運算式。 上述範例會在00小時起始排程器作業。
* 如果`send_email`設為`true`，資產建立者（將特定資產上傳至[!DNL Assets]的人員）會在資產過期時收到電子郵件。
* 排程器的一個迭代中過期的資產數上限是屬性`asset_expired_limit`的值。
* 要定期運行作業，請將屬性`cq.dam.expiry.notification.scheduler.istimebased`的值設定為`false`，並以秒為單位設定屬性`cq.dam.expiry.notification.scheduler.period.rule`的值。

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1.  For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## 資產狀態 {#asset-states}

[!DNL Assets]控制台可顯示資產的各種狀態。 根據特定資產的目前狀態，其卡片檢視會顯示描述其狀態的標籤，例如「已到期」、「已發佈」、「已核准」、「已拒絕」等。

1. 在[!DNL Assets]使用者介面中，選取資產。

1. 從工具欄中選擇&#x200B;**[!UICONTROL 發佈]**。 如果您在工具列中未看到[!UICONTROL Publish]選項，請按一下工具列上的&#x200B;**[!UICONTROL More]** ，然後找到&#x200B;**[!UICONTROL Publish]**&#x200B;選項。

1. 從菜單中選擇&#x200B;**[!UICONTROL Publish]**，然後關閉確認對話框。

1. 退出選擇模式。 資產的發佈狀態會顯示在卡片檢視中資產縮圖的底部。 在清單檢視中，「已發佈」欄會顯示資產發佈的時間。

1. 若要顯示其資產詳細資訊頁面，請在[!DNL Assets]介面中選取資產，然後按一下&#x200B;**[!UICONTROL 屬性]**。

1. 在[!UICONTROL Advanced]標籤中，從&#x200B;**[!UICONTROL Expires]**&#x200B;欄位設定資產的到期日。

1. 按一下「**[!UICONTROL 儲存]**」，然後按一下「**[!UICONTROL 關閉]**」以顯示資產主控台。

1. 資產的發佈狀態會在卡片檢視中資產縮圖底部指出過期狀態。 在清單檢視中，資產的狀態會顯示為&#x200B;**[!UICONTROL Expired]**。

1. 在[!DNL Assets]控制台中，選擇資料夾並在資料夾上建立審閱任務。

1. 複查和批准/拒絕複查任務中的資產，然後按一下&#x200B;**[!UICONTROL 完成]**。

1. 導航至建立審閱任務的資料夾。 您核准/拒絕的資產狀態會顯示在卡片檢視的底部。 在清單檢視中，核准和到期狀態會顯示在適當的欄中。

1. 若要根據資產的狀態來搜尋資產，請按一下「**[!UICONTROL 搜尋]**」以顯示搜尋列。

1. 選擇`Return`並按一下[!DNL Experience Manager]。

1. 在搜尋面板中，按一下&#x200B;**[!UICONTROL 發佈狀態]**&#x200B;並選取&#x200B;**[!UICONTROL Published]**&#x200B;以在[!DNL Assets]中搜尋已發佈的資產。

1. 若要搜尋已核准或已拒絕的資產，請選取「**[!UICONTROL 核准狀態]**」並選取適當的選項。

1. 若要根據資產的到期狀態來搜尋資產，請在搜尋面板中選取「**[!UICONTROL 到期狀態]**」 ，然後選取適當的選項。

1. 您也可以根據各種搜尋刻面下的狀態組合來搜尋資產。 例如，您可以搜尋在審核任務中核准且未過期的已發佈資產。 若要搜尋此類資產，請在搜尋刻面中選取適當的選項。

## [!DNL Assets]中的Digital Rights Management {#digital-rights-management-in-assets-1}

在您可以從[!DNL Assets]下載授權資產之前，DRM功能會強制接受授權合約。

如果您選取受保護的資產，然後按一下「下載」****，系統會將您重新導向至授權頁面，以接受授權合約。 如果您不接受許可協定，則&#x200B;**[!UICONTROL Download]**&#x200B;選項不可用。

如果選取項目包含多個受保護的資產，請一次選取一個資產、接受授權合約，然後繼續下載資產。

若符合以下任一條件，即視為資產受保護：

* 資產中繼資料屬性`xmpRights:WebStatement`指向包含資產授權合約之頁面的路徑。
* 資產中繼資料屬性`adobe_dam:restrictions`的值是指定授權協定的原始HTML。

>[!NOTE]
>
>位置`/etc/dam/drm/licences`用於儲存早期版本[!DNL Experience Manager]中的許可證。 該位置現在已過時。 如果您建立或修改授權頁面，或連接先前[!DNL Experience Manager]版本的頁面，Adobe建議您將這類資產儲存在`/apps/settings/dam/drm/licenses`或`/conf/*/settings/dam/drm/licenses`位置。

### 下載受DRM保護的資產 {#downloading-drm-assets}

1. 在卡片檢視中，選取您要下載的資產，然後選取&#x200B;**[!UICONTROL Download]**。
1. 在「版 **[!UICONTROL 權管理]** 」頁面中，從清單中選取您要下載的資產。
1. 在[!UICONTROL 許可證]窗格中，選擇&#x200B;**[!UICONTROL 同意]**。 資產旁會出現核取記號。 選擇&#x200B;**[!UICONTROL Download]**&#x200B;選項。

   >[!NOTE]
   >
   >只有當您選擇同意受保護資產的授權合約時，才會啟用&#x200B;**[!UICONTROL 下載]**&#x200B;選項。 不過，如果您的選擇同時包含受保護和未受保護的資產，則窗格中只會列出受保護的資產，並且&#x200B;**[!UICONTROL Download]**&#x200B;選項可用於下載未受保護的資產。 若要同時接受多個受保護資產的授權合約，請從清單中選取資產，然後選擇「同 **[!UICONTROL 意」]**。

1. 若要下載資產或其轉譯，請在對話方塊中選取「**[!UICONTROL 下載]**」 。
