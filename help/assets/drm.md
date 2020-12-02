---
title: ' [!DNL Assets]中的數位版權管理'
description: '瞭解如何以雲端服務的形式管理授權資產的資產到期狀態和資訊。 [!DNL Experience Manager] '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 7%

---


# 資產的數位版權管理{#digital-rights-management-in-assets}

數位資產通常與指定使用條款和期限的授權相關聯。 由於[!DNL Adobe Experience Manager Assets]已與[!DNL Experience Manager]平台完全整合，因此您可以有效管理資產到期資訊和資產狀態。 您也可以將授權資訊與資產建立關聯。

## 資產到期日{#asset-expiration}

資產到期是強制執行資產授權要求的有效方式。 它可確保發佈的資產在過期時未發佈，避免任何授權違規的可能。 不具管理員權限的使用者無法編輯、複製、移動、發佈及下載過期的資產。

您可以在下列位置檢視資產的到期狀態：

* **卡片檢視**:對於過期的資產，卡片上的標幟會指出其已過期。
* **清單檢視**:對於過期資產，「狀 **** 態」欄會顯示「過 **** 期」橫幅。
* **時間軸**:您可以在時間軸中檢視資產的到期狀態。選取資產，然後選擇「時間軸」。
* **參考邊欄**:您也可以在「參考」欄中檢視資產的到期 **** 狀態。它可管理資產到期狀態以及複合資產與參考子資產、系列和專案之間的關係。

1. 導覽至您要檢視其參考網頁和複合資產的資產。
1. 選取資產，然後按一下[!DNL Experience Manager]標誌。
1. 從菜單中選擇&#x200B;**[!UICONTROL References]**。
1. 對於過期資產，「參考」邊欄會在上方顯示到期狀態&#x200B;**[!UICONTROL 資產已到期]**。 如果資產已過期子資產，「參考」邊欄會顯示狀態&#x200B;**[!UICONTROL 「資產已過期子資產」]**。

### 搜尋過期資產{#search-expired-assets}

您可以在「搜尋」面板中搜尋過期的資產，包括過期的子資產。

1. 在[!DNL Assets]控制台中，按一下工具欄中的&#x200B;**[!UICONTROL Search]**&#x200B;以顯示「Omnisearch」框。

1. 在「Omnisearch」（搜索）框中，按Enter鍵可顯示搜索結果頁。

1. 按一下GlobalNav圖示以顯示「搜尋」面板。

1. 按一下/點選「 **[!UICONTROL 到期狀態]** 」選項以展開它。

1. 選擇&#x200B;**[!UICONTROL 已過期]**。 過期的資產會顯示在搜尋結果中。

當您選擇&#x200B;**[!UICONTROL Expired]**&#x200B;選項時，[!DNL Assets]主控台只會顯示複合資產參考的已到期資產和子資產。 在子資產到期後，不會立即顯示參照已到期子資產的複合資產。 相反，它們會在[!DNL Experience Manager]偵測到它們在下次排程器執行時參考過期子資產後顯示。

如果您將已發佈資產的到期日修改為早於目前排程器週期的日期，則排程仍會在下次執行時將此資產偵測為已到期資產，並據以反映狀態。 不同時區的使用者會以不同方式顯示資產的到期日。

此外，如果故障或錯誤導致調度程式無法檢測當前週期中的過期資產，則調度程式會在下一個週期重新檢查這些資產並檢測其過期狀態。

若要啟用[!DNL Assets]主控台來顯示參照的複合資產以及過期的子資產，請在[!DNL Experience Manager] Configuration Manager中設定&#x200B;**[!UICONTROL Adobe CQ DAM Expiry Notification]**&#x200B;工作流程。

1. 開啟[!DNL Experience Manager]配置管理器。
1. 選擇&#x200B;**[!UICONTROL Adobe CQ DAM Expiry Notification]**。 預設情況下，選擇&#x200B;**[!UICONTROL 基於時間的調度程式]**，該調度程式將作業安排在特定時間檢查資產是否已過期子資產。 作業完成後，已過期子資產和參考資產的資產會在搜尋結果中顯示為過期。

1. 要定期運行作業，請清除「基於時 **[!UICONTROL 間的調度程式規則]** 」欄位，並在「定期調度程式」欄位中以秒為單 **[!UICONTROL 位修改時間]** 。例如，示例表達式&#39;0 0 0 &amp;ast;&amp;ast;?&#39;會在00小時觸發工作。

<!-- 1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to AEM Assets) receives an email when the asset expires. See how to configure email notification for additional details around configuring email notifications at the overall AEM level.
-->

1. 在&#x200B;**[!UICONTROL 以秒為單位的先前通知]**&#x200B;欄位中，指定當您要收到有關過期的通知時，資產到期前的秒數。 如果您是管理員或資產建立者，在資產到期前會收到訊息，通知您資產將在指定時間後到期。

   資產過期後，您會收到另一則確認到期的通知。 此外，過期的資產會停用。

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

## 資產狀態{#asset-states}

[!DNL Assets]主控台可顯示資產的各種狀態。 根據特定資產的目前狀態，其卡片檢視會顯示描述其狀態的標籤，例如「已到期」、「已發佈」、「已核准」、「已拒絕」等。

1. 在[!DNL Assets]使用者介面中，選取資產。

1. 從工具列按一下「**[!UICONTROL 發佈]**」。 如果您在工具列上未看到&#x200B;**Publish**，請按一下工具列上的&#x200B;**[!UICONTROL More]**，並找到&#x200B;**[!UICONTROL Publish]**&#x200B;選項。

1. 從菜單中選擇&#x200B;**[!UICONTROL Publish]**，然後關閉確認對話框。
1. 退出選擇模式。 資產的出版物狀態會顯示在卡片檢視中資產縮圖的底部。 在清單檢視中，「已發佈」欄會顯示資產發佈的時間。

1. 若要顯示其資產詳細資料頁面，請在[!DNL Assets]介面中選取資產，然後按一下「屬性」]**。**[!UICONTROL 

1. 在[!UICONTROL Advanced]標籤中，從&#x200B;**[!UICONTROL Expires]**&#x200B;欄位設定資產的到期日。

1. 按一下「儲存」，然後按一下「關閉」以顯示「資產」主控台。]********[!UICONTROL 
1. 資產的發佈狀態會指出卡片檢視中資產縮圖底部的過期狀態。 在清單檢視中，資產的狀態會顯示為&#x200B;**[!UICONTROL 已到期]**。

1. 在[!DNL Assets]控制台中，選擇一個資料夾並在該資料夾上建立查看任務。
1. 複查並批准／拒絕複查任務中的資產，然後按一下&#x200B;**[!UICONTROL 完成]**。
1. 導航至您為其建立審閱任務的資料夾。 您核准／拒絕的資產狀態會顯示在卡片檢視的底部。 在清單檢視中，核准和到期狀態會顯示在適當的欄中。

1. 若要根據資產狀態來搜尋資產，請按一下「搜尋&#x200B;****」以顯示Omnisearch列。

1. 按return並按一下[!DNL Experience Manager]以顯示搜索面板。
1. 在搜尋面板中，按一下「發佈狀態」並選取「已發佈」，以搜尋[!DNL Assets]中的已發佈資產。]****[!UICONTROL ****

1. 按一下「核准狀態」，然後按一下適當的選項以搜尋已核准或已拒絕的資產。****

1. 若要根據資產的到期狀態來搜尋資產，請在「搜尋」面 **[!UICONTROL 板中選取「到期狀態]** 」，然後選擇適當的選項。

1. 您也可以根據各種搜尋刻面下的狀態組合來搜尋資產。 例如，您可以在搜尋Facet中選取適當的選項，以搜尋已在審核工作中核准但尚未過期的已發佈資產。

## [!DNL Assets] {#digital-rights-management-in-assets-1}中的數位版權管理

此功能會強制您接受授權合約，您才能從[!DNL Adobe Experience Manager Assets]下載授權資產。

如果您選取受保護的資產，然後按一下「下載」，就會將您重新導向至授權頁面以接受授權合約。 ]****[!UICONTROL &#x200B;如果您不接受授權合約，則&#x200B;**[!UICONTROL Download]**&#x200B;選項不可用。

如果選擇包含多個受保護的資產，請一次選取一個資產、接受授權合約，然後繼續下載資產。

如果符合下列任一條件，資產即視為受保護：

* 資產中繼資料屬性`xmpRights:WebStatement`指向包含資產授權合約之頁面的路徑。
* 資產中繼資料屬性`adobe_dam:restrictions`的值是指定授權合約的原始HTML。

>[!NOTE]
>
>`/etc/dam/drm/licences`用於儲存[!DNL Experience Manager]舊版授權的位置已過時。
>
>如果您建立或修改授權頁面，或從先前的[!DNL Experience Manager]版本移植，Adobe建議您將它們儲存在`/apps/settings/dam/drm/licenses`或`/conf/*/settings/dam/drm/licenses`下。

### 下載受DRM保護的資產{#downloading-drm-assets}

1. 在資訊卡檢視中，選取您要下載的資產，然後按一下「下載」。****
1. 在「版 **[!UICONTROL 權管理]** 」頁面中，從清單中選取您要下載的資產。
1. 在[!UICONTROL 許可證]窗格中，選擇&#x200B;**[!UICONTROL 同意]**。 資產旁會出現核取標籤。 按一下&#x200B;**[!UICONTROL Download]**&#x200B;選項。

   >[!NOTE]
   >
   >**[!UICONTROL Download]**&#x200B;選項只有在您選擇同意受保護資產的授權合約時啟用。 不過，如果您的選擇同時包含受保護和未受保護的資產，則窗格中只會列出受保護的資產，並且會啟用「下載&#x200B;****」選項來下載未受保護的資產。 若要同時接受多個受保護資產的授權合約，請從清單中選取資產，然後選擇「同 **[!UICONTROL 意」]**。

1. 在對話方塊中，按一下「下載&#x200B;****」以下載資產或其轉譯。
