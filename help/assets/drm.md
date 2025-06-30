---
title: ' [!DNL Assets]中的Digital Rights Management'
description: 瞭解如何在 [!DNL Experience Manager] as a [!DNL Cloud Service]中管理授權資產的資產到期狀態和資訊。
contentOwner: AG
feature: Asset Management,DRM
role: User, Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 6%

---

# 適用於數位資產的Digital Rights Management {#digital-rights-management-in-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/drm.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

數位資產通常與指定使用條款與時間的授權相關聯。 使用[!DNL Experience Manager]平台，您可以有效管理資產到期資訊和授權資訊。

## 資產有效期 {#asset-expiration}

若要強制執行資產的授權要求，請使用資產到期資訊。 到期資訊可確保已發佈的資產在到期時取消發佈，以防止授權違規。 沒有管理員許可權的使用者無法編輯、複製、移動、發佈和下載過期的資產。

您可以在下列位置檢視資產的到期狀態：

* **卡片檢視**：對於已到期的資產，卡片上的旗標會指出該資產已到期。
* **清單檢視**：針對已到期的資產，**[!UICONTROL 狀態]**&#x200B;欄會顯示&#x200B;**[!UICONTROL 已到期]**&#x200B;橫幅。
* **時間表**：您可以在時間表中檢視資產的到期狀態。 選取資產，然後選擇「時間軸」。
* **參考邊欄**：您也可以在&#x200B;**[!UICONTROL 參考]**&#x200B;邊欄中檢視資產的到期狀態。 它可管理資產到期狀態以及複合資產和參照的子資產、集合和專案之間的關係。

若要檢視資產的參照網頁和複合資產，請遵循下列步驟：

1. 導覽至該資產，選取該資產，然後按一下![左側邊欄內容參考圖示](assets/do-not-localize/content-rail-icon.png)。 左側邊欄隨即開啟。
1. 從左側邊欄選取&#x200B;**[!UICONTROL 參考]**。
1. 對於過期的資產，[!UICONTROL 參考]會顯示到期狀態，因為&#x200B;**[!UICONTROL 資產已過期]**。 如果資產具有過期的子資產，[!UICONTROL 參考]邊欄會顯示狀態&#x200B;**[!UICONTROL 資產具有過期的子Assets]**。

### 搜尋過期的資產 {#search-expired-assets}

若要搜尋過期的資產（包括過期的子資產），請遵循下列步驟：

1. 在[!DNL Assets]主控台中，按一下工具列中的&#x200B;**[!UICONTROL 搜尋]**，然後按`Enter`。

1. 按一下GlobalNav圖示並選取&#x200B;**[!UICONTROL 到期狀態]**&#x200B;選項。

1. 選取&#x200B;**[!UICONTROL 過期]**。 搜尋結果會顯示過期的資產。

當您選擇&#x200B;**[!UICONTROL 過期]**&#x200B;選項時，[!DNL Assets]主控台只會顯示複合資產所參考的過期資產和子資產。 參考過期子資產的複合資產不會在子資產過期後立即顯示。 而是在下次排程器執行時[!DNL Experience Manager]偵測到它們參照過期的子資產後，才會顯示。

您可以將已發佈資產的到期日修改為早於目前排程器週期的日期。 不過，排程在下次執行時仍會偵測到這類資產為已到期的資產，[!DNL Experience Manager]會在報表中反映狀態。 對於不同時區的使用者，資產到期日的顯示方式會有所不同。

此外，如果錯誤阻止排程器在目前週期中偵測到已到期的資產，排程器會在下一個週期中重新檢查這些資產，並偵測其已到期狀態。

若要啟用[!DNL Assets]主控台以顯示參照的複合資產以及過期的子資產，請在[!DNL Experience Manager]中設定&#x200B;**[!UICONTROL Adobe CQ DAM Expiry Notification]**&#x200B;工作流程。 基於時間的排程器會排程工作，以在特定時間檢查資產是否已過期子資產。 工作完成後，具有過期子資產和參考資產的資產會在搜尋結果中顯示為過期。

1. 存取與您的環境相關聯的[!DNL Cloud Manager] Git存放庫。
1. 提交儲存庫中名為`com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json`的檔案，該檔案包含下列內容。

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. 依照[的指示操作，如何在 [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md)中進行OSGi設定。

您可以使用以下屬性來設定排程器：

* 屬性`cq.dam.expiry.notification.scheduler.istimebased`的`true`值會啟動排程器。 *屬性`cq.dam.expiry.notification.scheduler.timebased.rule`的值是定義時間的規則運算式。 上述範例會在00小時起始排程器工作。
* 如果`send_email`設為`true`，則資產建立者（將特定資產上傳至[!DNL Assets]的人員）會在資產過期時收到電子郵件。
* 排程器一個反複專案中到期的資產數目上限是屬性`asset_expired_limit`的值。
* 若要定期執行工作，請將屬性`cq.dam.expiry.notification.scheduler.istimebased`的值設為`false`，並將屬性`cq.dam.expiry.notification.scheduler.period.rule`的值設為以秒為單位的時間。

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## 資產狀態 {#asset-states}

[!DNL Assets]主控台可顯示資產的各種狀態。 根據特定資產的目前狀態，其卡片檢視會顯示描述其狀態的標籤，例如，已過期、已發佈、已核准、已拒絕等。

1. 在[!DNL Assets]使用者介面中，選取資產。

1. 從工具列選取&#x200B;**[!UICONTROL 發佈]**。 如果您在工具列中看不到[!UICONTROL 發佈]選項，請按一下工具列上的&#x200B;**[!UICONTROL 更多]**，然後找到&#x200B;**[!UICONTROL 發佈]**&#x200B;選項。

1. 從功能表選擇&#x200B;**[!UICONTROL 發佈]**，然後關閉確認對話方塊。

1. 結束選取模式。 資產的發佈狀態會顯示在卡片檢視的資產縮圖底部。 在清單檢視中，「已發佈」欄會顯示資產的發佈時間。

1. 若要顯示其資產詳細資訊頁面，請在[!DNL Assets]介面中選取資產，然後按一下&#x200B;**[!UICONTROL 屬性]**。

1. 在[!UICONTROL 進階]索引標籤中，從&#x200B;**[!UICONTROL 過期]**&#x200B;欄位設定資產的到期日。

1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;以顯示資產主控台。

1. 資產的發佈狀態會指出卡片檢視中資產縮圖底部的過期狀態。 在清單檢視中，資產的狀態會顯示為&#x200B;**[!UICONTROL 已過期]**。

1. 在[!DNL Assets]主控台中，選取資料夾並在該資料夾上建立稽核工作。

1. 檢閱並核准/拒絕檢閱任務中的資產，然後按一下&#x200B;**[!UICONTROL 完成]**。

1. 導覽至您建立稽核任務的資料夾。 您核准/拒絕的資產狀態會顯示在卡片檢視的底部。 在清單檢視中，核准和到期狀態會顯示在適當的欄中。

1. 若要根據資產的狀態來搜尋資產，請按一下&#x200B;**[!UICONTROL 搜尋]**&#x200B;以顯示搜尋列。

1. 選取`Return`並按一下[!DNL Experience Manager]。

1. 在搜尋面板中，按一下&#x200B;**[!UICONTROL 發佈狀態]**&#x200B;並選取&#x200B;**[!UICONTROL 已發佈]**，以在[!DNL Assets]中搜尋已發佈的資產。

1. 若要搜尋已核准或已拒絕的資產，請選取&#x200B;**[!UICONTROL 核准狀態]**&#x200B;並選取適當的選項。

1. 若要根據資產的到期狀態來搜尋資產，請在搜尋面板中選取&#x200B;**[!UICONTROL 到期狀態]**，然後選取適當的選項。

1. 您也可以根據各種搜尋面向下的狀態組合來搜尋資產。 例如，您可以搜尋在稽核任務中核准且未過期的已發佈資產。 若要搜尋這類資產，請在搜尋Facet中選取適當的選項。

## [!DNL Assets]中的Digital Rights Management {#digital-rights-management-in-assets-1}

DRM功能會強制接受授權合約，然後才能從[!DNL Assets]下載授權資產。

如果您選取受保護的資產並按一下[下載]，系統會將您重新導向至授權頁面，讓您接受授權合約。 **&#x200B;**&#x200B;如果您不接受授權合約，將無法使用&#x200B;**[!UICONTROL 下載]**&#x200B;選項。

如果選取範圍包含多個受保護的資產，請一次選取一個資產、接受授權合約，然後繼續下載資產。

如果符合下列任一條件，資產即視為受保護：

* 資產中繼資料屬性`xmpRights:WebStatement`指向包含資產授權合約的頁面的路徑。
* 資產中繼資料屬性`adobe_dam:restrictions`的值是指定授權合約的原始HTML。

>[!NOTE]
>
>位置`/etc/dam/drm/licences`是用來儲存舊版[!DNL Experience Manager]的授權。 該位置現已棄用。 如果您建立或修改授權頁面，或移轉來自先前[!DNL Experience Manager]個版本的頁面，Adobe建議您將這些資產儲存在`/apps/settings/dam/drm/licenses`或`/conf/*/settings/dam/drm/licenses`位置。

### 下載受DRM保護的資產 {#downloading-drm-assets}

1. 在卡片檢視中，選取您要下載的資產，然後選取&#x200B;**[!UICONTROL 下載]**。
1. 在「版 **[!UICONTROL 權管理]** 」頁面中，從清單中選取您要下載的資產。
1. 在[!UICONTROL 授權]窗格中，選擇&#x200B;**[!UICONTROL 同意]**。 資產旁會出現核取標籤。 選取&#x200B;**[!UICONTROL 下載]**&#x200B;選項。

   >[!NOTE]
   >
   >**[!UICONTROL 下載]**&#x200B;選項只有在您選擇同意受保護資產的授權合約時才啟用。 但是，如果您的選擇同時包含受保護和未受保護的資產，則窗格中只會列出受保護的資產，且&#x200B;**[!UICONTROL 下載]**&#x200B;選項可用於下載未受保護的資產。 若要同時接受多個受保護資產的授權合約，請從清單中選取資產，然後選擇「同 **[!UICONTROL 意」]**。

1. 若要下載資產或其轉譯，請在對話方塊中選取&#x200B;**[!UICONTROL 下載]**。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
