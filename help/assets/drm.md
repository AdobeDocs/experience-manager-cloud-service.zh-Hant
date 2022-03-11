---
title: Digital Rights Management [!DNL Assets]
description: 瞭解如何管理中的授權資產的資產到期狀態和資訊 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。
contentOwner: AG
feature: Asset Management,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: f993148a9f678cfdaf0693e4964f02b9163cf2ff
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 2%

---

# Digital Rights Management數字資產 {#digital-rights-management-in-assets}

數字資產通常與指定使用條款和持續時間的許可證相關聯。 使用 [!DNL Experience Manager] 平台，您可以高效地管理資產到期資訊和許可資訊。

## 資產到期 {#asset-expiration}

要強制執行資產的許可證要求，請使用資產到期資訊。 到期資訊確保發佈的資產在到期時被取消發佈，從而防止許可證違規。 沒有管理員權限的用戶無法編輯、複製、移動、發佈和下載過期資產。

您可以在以下位置查看資產的到期狀態：

* **卡視圖**:對於過期資產，卡上的標誌表示已過期。
* **清單視圖**:對於已到期資產， **[!UICONTROL 狀態]** 列顯示 **[!UICONTROL 已過期]** 橫幅。
* **時間軸**:您可以在時間軸中查看資產的到期狀態。 選擇資產，然後選擇時間軸。
* **參考導軌**:您還可以在 **[!UICONTROL 引用]** 鐵軌。 它管理複合資產與引用的子集、集合和項目之間的資產到期狀態和關係。

要查看資產的引用網頁和複合資產，請執行以下步驟：

1. 定位至資產，選擇資產，然後按一下 ![左欄內容引用表徵圖](assets/do-not-localize/content-rail-icon.png)。 左滑軌開啟。
1. 選擇 **[!UICONTROL 引用]** 左欄。
1. 對於已到期資產， [!UICONTROL 引用] 將到期狀態顯示為 **[!UICONTROL 資產已過期]**。 如果資產已過期子組， [!UICONTROL 引用] 滑軌顯示狀態 **[!UICONTROL 資產已到期子資產]**。

### 搜索過期資產 {#search-expired-assets}

要搜索已到期資產（包括已到期的子組），請執行以下步驟：

1. 在 [!DNL Assets] 控制台，按一下 **[!UICONTROL 搜索]** 按 `Enter`。

1. 按一下GlobalNav表徵圖並選擇 **[!UICONTROL 到期狀態]** 的雙曲餘切值。

1. 選擇 **[!UICONTROL 已過期]**。 搜索結果顯示過期的資產。

選擇 **[!UICONTROL 已過期]** 頁籤 [!DNL Assets] console僅顯示複合資產引用的過期資產和子組。 引用過期子集的複合資產在子集到期後不會立即顯示。 相反，它們在 [!DNL Experience Manager] 檢測它們在下次調度程式執行時引用過期的子集。

可以將已發佈資產的到期日期修改為早於當前計畫程式週期的日期。 但是，計畫在下次執行時仍將此類資產檢測為到期資產， [!DNL Experience Manager] 反映其報告中的狀態。 不同時區中的用戶不同地顯示資產的到期日期。

此外，如果錯誤阻止調度程式在當前週期中檢測到過期資產，則調度程式將在下一個週期中重新檢查這些資產並檢測其過期狀態。

啟用 [!DNL Assets] 控制台：顯示引用複合資產以及過期的子集，配置 **[!UICONTROL Adobe CQ大壩期終通知]** 工作流 [!DNL Experience Manager]。 基於時間的計畫程式將作業安排為在特定時間檢查資產是否已過期子集。 作業完成後，已過期子集和引用資產的資產在搜索結果中顯示為過期。

1. 訪問 [!DNL Cloud Manager] 與您的環境關聯的Git儲存庫。
1. 提交名為 `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` 的下界。

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. 按照 [如何在 [!DNL Experience Manager] 作為 [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md)。

可以使用以下屬性配置調度程式：

* A `true` 屬性的值 `cq.dam.expiry.notification.scheduler.istimebased` 啟動調度程式。 *財產價值 `cq.dam.expiry.notification.scheduler.timebased.rule` 是定義時間的規則運算式。 上例將在00小時啟動計畫程式作業。
* 如果 `send_email` 設定為 `true`，資產建立者（將特定資產上載到的人員） [!DNL Assets])在資產過期時收到電子郵件。
* 計畫程式的一個迭代中過期的最大資產數是屬性的值 `asset_expired_limit`。
* 要定期運行作業，請設定屬性的值 `cq.dam.expiry.notification.scheduler.istimebased` 如 `false` 並設定屬性的值 `cq.dam.expiry.notification.scheduler.period.rule` 以秒為單位。

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1.  For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## 資產狀態 {#asset-states}

的 [!DNL Assets] 控制台可顯示資產的各種狀態。 根據特定資產的當前狀態，其卡視圖將顯示描述其狀態的標籤，例如「已到期」、「已發佈」、「已批准」、「已拒絕」等。

1. 在 [!DNL Assets] 用戶介面，選擇資產。

1. 選擇 **[!UICONTROL 發佈]** 的子菜單。 如果你看不到 [!UICONTROL 發佈] 的 **[!UICONTROL 更多]** 在工具欄上，然後 **[!UICONTROL 發佈]** 的雙曲餘切值。

1. 選擇 **[!UICONTROL 發佈]** ，然後關閉確認對話框。

1. 退出選擇模式。 資產的發佈狀態顯示在卡視圖中資產縮略圖的底部。 在清單視圖中，「已發佈」列顯示資產發佈的時間。

1. 要顯示其資產詳細資訊頁面，請在 [!DNL Assets] 介面，選擇資產並按一下 **[!UICONTROL 屬性]**。

1. 在 [!UICONTROL 高級] 頁籤中，設定 **[!UICONTROL 過期]** 的子菜單。

1. 按一下 **[!UICONTROL 保存]** 然後按一下 **[!UICONTROL 關閉]** 顯示資產控制台。

1. 資產的發佈狀態在卡視圖中資產縮略圖底部指示過期狀態。 在清單視圖中，資產的狀態顯示為 **[!UICONTROL 已過期]**。

1. 在 [!DNL Assets] 控制台，選擇一個資料夾並在該資料夾上建立查看任務。

1. 審閱和批准/拒絕審閱任務中的資產，然後按一下 **[!UICONTROL 完成]**。

1. 導航到為其建立審閱任務的資料夾。 您批准/拒絕的資產的狀態顯示在卡視圖的底部。 在清單視圖中，審批和到期狀態將顯示在相應的列中。

1. 要根據資產的狀態搜索資產，請按一下 **[!UICONTROL 搜索]** 按鈕。

1. 選擇 `Return` 按一下 [!DNL Experience Manager]。

1. 在搜索面板中，按一下 **[!UICONTROL 發佈狀態]** 選擇 **[!UICONTROL 已發佈]** 要在中搜索已發佈的資產 [!DNL Assets]。

1. 要搜索已批准或已拒絕的資產，請選擇 **[!UICONTROL 審批狀態]** 並選擇相應的選項。

1. 要根據資產的到期狀態搜索資產，請選擇 **[!UICONTROL 到期狀態]** ，然後選擇相應的選項。

1. 您還可以根據各種搜索方面下的狀態組合來搜索資產。 例如，您可以搜索在複查任務中批准且未過期的已發佈資產。 要搜索此類資產，請在搜索方面中選擇相應的選項。

## Digital Rights Management [!DNL Assets] {#digital-rights-management-in-assets-1}

DRM功能強制您接受許可協定，然後您才能從下載許可資產 [!DNL Assets]。

如果選擇受保護的資產並按一下 **[!UICONTROL 下載]**，您將被重定向到許可證頁面以接受許可證協定。 如果您不接受許可協定， **[!UICONTROL 下載]** 頁籤

如果所選內容包含多個受保護資產，則一次選擇一個資產，接受許可協定，然後繼續下載該資產。

如滿足以下任一條件，則資產被視為受保護：

* 資產元資料屬性 `xmpRights:WebStatement` 指向包含資產的許可協定的頁面路徑。
* 資產元資料屬性的值 `adobe_dam:restrictions` 是指定許可協定的原始HTML。

>[!NOTE]
>
>位置 `/etc/dam/drm/licences` 用於將許可證儲存在 [!DNL Experience Manager]。 現在不建議使用該位置。 如果您建立或修改許可證頁，或將上一頁的頁埠 [!DNL Experience Manager] 版本，Adobe建議您將此類資產儲存在 `/apps/settings/dam/drm/licenses` 或 `/conf/*/settings/dam/drm/licenses` 位置。

### 下載受DRM保護的資產 {#downloading-drm-assets}

1. 在卡視圖中，選擇要下載的資產並選擇 **[!UICONTROL 下載]**。
1. 在「版 **[!UICONTROL 權管理]** 」頁面中，從清單中選取您要下載的資產。
1. 在 [!UICONTROL 許可證] 框，選擇 **[!UICONTROL 同意]**。 資產旁邊將顯示複選標籤。 選擇 **[!UICONTROL 下載]** 的雙曲餘切值。

   >[!NOTE]
   >
   >的 **[!UICONTROL 下載]** 選項僅在您選擇同意受保護資產的許可協定時啟用。 但是，如果您的選擇同時包含受保護和未受保護的資產，則窗格和 **[!UICONTROL 下載]** 選項可下載未受保護的資產。 若要同時接受多個受保護資產的授權合約，請從清單中選取資產，然後選擇「同 **[!UICONTROL 意」]**。

1. 要下載資產或其格式副本，請選擇 **[!UICONTROL 下載]** 的子菜單。
