---
title: Digital Rights Management [!DNL Assets]
description: 了解如何在 [!DNL Experience Manager] as a [!DNL Cloud Service]中管理授權資產的資產到期狀態和資訊。
contentOwner: AG
feature: 資產管理，DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 7%

---

# Digital Rights Management資產 {#digital-rights-management-in-assets}

數位資產通常與指定使用條款和持續時間的授權相關聯。 因為[!DNL Adobe Experience Manager Assets]已與[!DNL Experience Manager]平台完全整合，因此您可以有效管理資產到期資訊和資產狀態。 您也可以將授權資訊與資產建立關聯。

## 資產過期 {#asset-expiration}

資產到期是強制執行資產授權要求的有效方式。 它可確保已發佈的資產在過期時未發佈，以免發生任何違反授權的情況。 沒有管理員權限的使用者無法編輯、複製、移動、發佈和下載過期的資產。

您可以在下列位置檢視資產的到期狀態：

* **卡片檢視**:對於過期的資產，卡片上的標幟會指出其已過期。
* **清單檢視**:對於過期的資產，「狀 **** 態」欄會顯示「過 **** 期」橫幅。
* **時間表**:您可以在時間軸中檢視資產的到期狀態。選取資產，然後選擇「時間軸」。
* **參考邊欄**:您也可以在「參考」邊欄中檢視資產的到期 **** 狀態。它可管理複合資產與參考的子資產、集合和專案之間的資產到期狀態和關係。

1. 導覽至您要檢視其參考網頁和複合資產的資產。
1. 選取資產，然後按一下[!DNL Experience Manager]標誌。
1. 從菜單中選擇&#x200B;**[!UICONTROL 引用]**。
1. 對於過期的資產，「參考」邊欄會在頂端顯示到期狀態&#x200B;**[!UICONTROL 資產已到期]**。 如果資產已過期的子資產，「參考」邊欄會顯示狀態&#x200B;**[!UICONTROL 資產已過期的子資產]**。

### 搜尋過期的資產 {#search-expired-assets}

您可以在「搜尋」面板中搜尋過期的資產，包括過期的子資產。

1. 在[!DNL Assets]控制台中，按一下工具列中的&#x200B;**[!UICONTROL 搜尋]**&#x200B;以顯示[!DNL Experience Manager]搜尋方塊。

1. 在Omnisearch框中，選擇`Enter`鍵以顯示搜索結果頁。

1. 按一下GlobalNav表徵圖以顯示「搜索」面板。

1. 按一下/點選「 **[!UICONTROL 到期狀態]** 」選項以展開它。

1. 選擇&#x200B;**[!UICONTROL Expired]**。 過期的資產會顯示在搜尋結果中。

當您選擇&#x200B;**[!UICONTROL Expired]**&#x200B;選項時，[!DNL Assets]主控台只會顯示複合資產參照的過期資產和子資產。 參考過期子資產的複合資產，不會在子資產過期後立即顯示。 而是會在[!DNL Experience Manager]偵測到它們在下次排程器執行時參考過期的子資產後顯示。

如果您將已發佈資產的到期日修改為早於目前排程器週期的日期，排程仍會在下次執行時將此資產偵測為過期資產，並據以反映狀態。 不同時區的使用者會以不同方式顯示資產的到期日。

此外，如果故障或錯誤使調度程式無法檢測當前週期中的過期資產，則調度程式將在下一個週期中重新檢查這些資產並檢測其過期狀態。

若要啟用[!DNL Assets]主控台以顯示參考的複合資產以及過期的子資產，請在[!DNL Experience Manager] Configuration Manager中設定&#x200B;**[!UICONTROL Adobe CQ DAM Expiry Notification]**&#x200B;工作流程。

1. 開啟[!DNL Experience Manager] Configuration Manager。
1. 選擇&#x200B;**[!UICONTROL Adobe CQ DAM過期通知]**。 依預設，會選取&#x200B;**[!UICONTROL 以時間為基礎的排程器]**，排程工作以在特定時間檢查資產是否已過期子資產。 作業完成後，過期的子資產和參考資產的資產會在搜尋結果中顯示為過期。

1. 要定期運行作業，請清除「基於時 **[!UICONTROL 間的調度程式規則]** 」欄位，並在「定期調度程式」欄位中以秒為單 **[!UICONTROL 位修改時間]** 。例如，示例表達式&#39;0 0 0 &amp;ast;&amp;ast;?&#39;會在00小時觸發工作。

<!-- 1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to AEM Assets) receives an email when the asset expires. See how to configure email notification for additional details around configuring email notifications at the overall AEM level.
-->

1. 在&#x200B;**[!UICONTROL 秒為的前通知欄位中]**，指定當您要接收到有關到期的通知時，資產到期前的秒數。 如果您是管理員或資產建立者，您會在資產到期前收到訊息，通知您資產將在指定時間後到期。

   資產過期後，您會收到確認到期的其他通知。 此外，已過期的資產會停用。

1. 按一下「**[!UICONTROL 儲存]**」。

## 資產狀態 {#asset-states}

[!DNL Assets]控制台可顯示資產的各種狀態。 根據特定資產的目前狀態，其卡片檢視會顯示描述其狀態的標籤，例如「已到期」、「已發佈」、「已核准」、「已拒絕」等。

1. 在[!DNL Assets]使用者介面中，選取資產。

1. 從工具列按一下「**[!UICONTROL 發佈]**」。 如果您在工具列上未看到&#x200B;**Publish**，請按一下工具列上的&#x200B;**[!UICONTROL More]**，然後找出&#x200B;**[!UICONTROL Publish]**&#x200B;選項。

1. 從菜單中選擇&#x200B;**[!UICONTROL Publish]**，然後關閉確認對話框。
1. 退出選擇模式。 資產的發佈狀態會顯示在卡片檢視中資產縮圖的底部。 在清單檢視中，「已發佈」欄會顯示資產發佈的時間。

1. 若要顯示其資產詳細資訊頁面，請在[!DNL Assets]介面中選取資產，然後按一下&#x200B;**[!UICONTROL 屬性]**。

1. 在[!UICONTROL Advanced]標籤中，從&#x200B;**[!UICONTROL Expires]**&#x200B;欄位設定資產的到期日。

1. 按一下「**[!UICONTROL 儲存]**」，然後按一下「**[!UICONTROL 關閉]**」以顯示資產主控台。
1. 資產的發佈狀態會在卡片檢視中資產縮圖底部指出過期狀態。 在清單檢視中，資產的狀態會顯示為&#x200B;**[!UICONTROL Expired]**。

1. 在[!DNL Assets]控制台中，選擇資料夾並在資料夾上建立審閱任務。
1. 複查和批准/拒絕複查任務中的資產，然後按一下&#x200B;**[!UICONTROL 完成]**。
1. 導航至建立審閱任務的資料夾。 您核准/拒絕的資產狀態會顯示在卡片檢視的底部。 在清單檢視中，核准和到期狀態會顯示在適當的欄中。

1. 若要根據資產的狀態來搜尋資產，請按一下「**[!UICONTROL 搜尋]**」以顯示Omnisearch列。

1. 選擇`Return`並按一下[!DNL Experience Manager]以顯示搜索面板。
1. 在搜尋面板中，按一下&#x200B;**[!UICONTROL 發佈狀態]**&#x200B;並選取&#x200B;**[!UICONTROL Published]**&#x200B;以在[!DNL Assets]中搜尋已發佈的資產。

1. 按一下「**[!UICONTROL 核准狀態]**」 ，然後按一下適當的選項以搜尋已核准或已拒絕的資產。

1. 若要根據資產的到期狀態來搜尋資產，請在「搜尋」面 **[!UICONTROL 板中選取「到期狀態]** 」，然後選擇適當的選項。

1. 您也可以根據各種搜尋刻面下的狀態組合來搜尋資產。 例如，您可以在搜尋Facet中選取適當的選項，以搜尋已在審核任務中核准且尚未過期的已發佈資產。

## [!DNL Assets]中的Digital Rights Management {#digital-rights-management-in-assets-1}

此功能可強制您接受授權合約，之後您才能從[!DNL Adobe Experience Manager Assets]下載授權資產。

如果您選取受保護的資產，然後按一下「下載」****，系統會將您重新導向至授權頁面，以接受授權合約。 如果您不接受許可協定，則&#x200B;**[!UICONTROL Download]**&#x200B;選項不可用。

如果選取項目包含多個受保護的資產，請一次選取一個資產、接受授權合約，然後繼續下載資產。

若符合以下任一條件，即視為資產受保護：

* 資產中繼資料屬性`xmpRights:WebStatement`指向包含資產授權合約之頁面的路徑。
* 資產中繼資料屬性`adobe_dam:restrictions`的值是指定授權協定的原始HTML。

>[!NOTE]
>
>[!DNL Experience Manager]舊版中用於儲存許可證的位置`/etc/dam/drm/licences`已過時。
>
>如果建立或修改許可證頁，或將其連接到以前的[!DNL Experience Manager]版本，則Adobe建議將它們儲存在`/apps/settings/dam/drm/licenses`或`/conf/*/settings/dam/drm/licenses`下。

### 下載受DRM保護的資產 {#downloading-drm-assets}

1. 在卡片檢視中，選取您要下載的資產，然後按一下&#x200B;**[!UICONTROL 下載]**。
1. 在「版 **[!UICONTROL 權管理]** 」頁面中，從清單中選取您要下載的資產。
1. 在[!UICONTROL 許可證]窗格中，選擇&#x200B;**[!UICONTROL 同意]**。 資產旁會出現核取記號。 按一下&#x200B;**[!UICONTROL Download]**&#x200B;選項。

   >[!NOTE]
   >
   >只有當您選擇同意受保護資產的授權合約時，才會啟用&#x200B;**[!UICONTROL 下載]**&#x200B;選項。 不過，如果您的選擇同時包含受保護和未受保護的資產，則窗格中只會列出受保護的資產，並啟用&#x200B;**[!UICONTROL Download]**&#x200B;選項以下載未受保護的資產。 若要同時接受多個受保護資產的授權合約，請從清單中選取資產，然後選擇「同 **[!UICONTROL 意」]**。

1. 在對話方塊中，按一下&#x200B;**[!UICONTROL Download]**&#x200B;以下載資產或其轉譯。
