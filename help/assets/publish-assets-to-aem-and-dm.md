---
title: 快速發佈至 [!DNL AEM and Dynamic Media]
description: 在 [!DNL Assets view] 中快速發佈可讓您將資產同時或個別發佈到 [!DNL AEM and Dynamic Media] 。 您可以選取資產和資料夾，並選擇發佈至 [!DNL Dynamic Media] 或 [!DNL AEM]。
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, [!DNL Dynamic Media]
role: User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# 將Assets發佈至[!DNL AEM and Dynamic Media]{#Publish-Assets-to-AEM-and-Dynamic-Media}

[!DNL Experience Manager Assets]可讓您使用[!DNL Experience Manager]快速將資產發佈到[!DNL Dynamic Media]和[!DNL Assets view]。 這可確保您管理資產，然後使用[[!DNL Assets view] 發佈資產，而不需切換至 [!DNL Admin view]](/help/assets/overview.md##persona-based-experiences)。

[!DNL Experience Manager Assets view]提供彈性功能，可同時將資產發佈至[!DNL AEM]或[!DNL Dynamic Media]，或兩者同時發佈。 您可以在上傳、瀏覽和搜尋資產時發佈資產。 本文會詳細說明這些發佈資產的選項。

## 開始之前 {#before-you-begin}

設定這些設定以檢視[!DNL AEM and Dynamic Media]的發佈選項：

* 若要檢視[!DNL Dynamic Media]的發佈選項，請使用「管理員」檢視來設定下列設定：

   * [建立 [!DNL Dynamic Media] 雲端設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)。
   * 在資料夾層級設定[!DNL Dynamic Media]發佈模式。 您也可以在建立[!DNL Dynamic Media]雲端組態時進行這些設定。 若要覆寫資料夾層級的這些設定，請參閱[在 [!DNL Dynamic Media]](/help/assets/dynamic-media/selective-publishing.md)中設定資料夾層級的選擇性發佈。

* 若要檢視[!DNL AEM]的發佈選項，您必須為環境設定[!DNL AEM]發佈端點。

## 上傳時發佈Assets {#piblish-assets-during-upload}

上傳資產至資料夾時，您可以將資產發佈至[!DNL AEM and Dynamic Media]。 顯示的發佈選項取決於資產上傳所在資料夾的[!DNL Dynamic Media]發佈模式設定。 [!DNL Dynamic Media]發佈模式可以設為：

* **[!UICONTROL 啟動時]：**&#x200B;將資產上傳至此資料夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。

* **[!UICONTROL 立即]：**&#x200B;將資產上傳至此資料夾時，系統會將該資產擷取至Experience Manager，並立即提供URL/內嵌。
* **[!UICONTROL 選擇性發佈]：** Assets已發佈至您選擇的[!DNL Experience Manager]或[!DNL Dynamic Media]，以便在公用網域中傳遞。

### [!UICONTROL Dynamic Media發佈模式]啟動時設定為 {#dynamic-media-publish-mode-set-to-upon-activation}

若要在資產上傳至[!DNL Dynamic Media Publish Mode]設定為&#x200B;**[!UICONTROL 啟動時]**&#x200B;的資料夾時發佈資產：

1. 按一下「**[!UICONTROL 新增Assets]**」>「**[!UICONTROL 瀏覽]**」>「**[!UICONTROL 瀏覽檔案]**」以瀏覽至適當的資料夾以上傳資產。 **[!UICONTROL 發佈選項]**&#x200B;區段會將&#x200B;**[!UICONTROL DM發佈模式]**&#x200B;顯示為&#x200B;**[!UICONTROL 啟動時]**。

   ![啟動時上傳影像](/help/assets/assets/upload-uactivation.svg)

1. 選取&#x200B;**[!UICONTROL 發佈至AEM和Dynamic Media]**&#x200B;並按一下&#x200B;**[!UICONTROL 上傳]**。 資產會同時發佈至[!DNL AEM and Dynamic Media]。 若要檢視這些資產的更新發佈狀態，請參閱[檢查發佈狀態](#check-publish-status)。

### [!UICONTROL Dynamic Media發佈模式]設定為[!UICONTROL 立即] {#dynamic-media-publish-mode-set-to-immediate}

若要在資產上傳至[!UICONTROL Dynamic Media發佈模式]設定為&#x200B;**[!UICONTROL 立即]**&#x200B;的資料夾時發佈資產：

1. 按一下「**[!UICONTROL 新增Assets]**」>「**[!UICONTROL 瀏覽]**」>「**[!UICONTROL 瀏覽檔案]**」以瀏覽至適當的資料夾以上傳資產。 **[!UICONTROL 發佈選項]**&#x200B;區段會將&#x200B;**[!UICONTROL DM發佈模式]**&#x200B;顯示為&#x200B;**[!UICONTROL 立即]**。

   ![檔案上傳影像 — 立即模式](/help/assets/assets/resized-image-pdf-svg-new.svg)

   由於[!UICONTROL Dynamic Media發佈模式]是&#x200B;**[!UICONTROL 立即]**，當您按一下[!DNL Dynamic Media]上傳&#x200B;**[!UICONTROL 時，已上傳的資產會自動發佈至]**。

1. 選取&#x200B;**發佈至AEM**&#x200B;以將上傳的資產發佈至[!DNL AEM]，然後按一下&#x200B;**[!UICONTROL 上傳]**。

   如果您選取&#x200B;**發佈至AEM**，資產會發佈至[!DNL AEM and Dynamic Media]，否則資產會發佈至[!DNL Dynamic Media]。

   若要檢視這些資產的更新發佈狀態，請參閱[檢查發佈狀態](#check-publish-status)。

### [!UICONTROL Dynamic Media發佈模式]設定為[!UICONTROL 選擇性發佈] {#dynamic-media-publish-mode-set-to-selective-publish}

若要在上傳至資料夾期間發佈資產，且[!UICONTROL Dynamic Media發佈模式]設定為&#x200B;**[!UICONTROL 選擇性發佈]**：

1. 按一下「**[!UICONTROL 新增Assets]**」>「**[!UICONTROL 瀏覽]**」>「**[!UICONTROL 瀏覽檔案]**」以瀏覽至適當的資料夾以上傳資產。 **[!UICONTROL 發佈選項]**&#x200B;區段會將&#x200B;**[!UICONTROL DM發佈模式]**&#x200B;顯示為&#x200B;**[!UICONTROL 選擇性發佈]**。

![上傳影像選擇性筆畫模式](/help/assets/assets/upload-selective.svg)

1. 根據您的需求，選取&#x200B;**[!UICONTROL 發佈至AEM]**、**[!UICONTROL 發佈至Dynamic Media]**&#x200B;或兩者，然後按一下&#x200B;**上傳**。

   資產會根據您的選擇發佈至[!DNL AEM and Dynamic Media]。

   若要檢視這些資產的更新發佈狀態，請參閱[檢查發佈狀態](#check-publish-status)。

## 使用資產瀏覽頁面發佈資產 {#publish-assets-using-asset-browse-page}

若要使用資產瀏覽頁面發佈資產：

1. 按一下左窗格中可用的&#x200B;**[!UICONTROL Assets管理]**&#x200B;區段中的&#x200B;**[!UICONTROL Assets]**。
1. 選取一或多個您需要發佈的資產或資料夾，然後按一下[發佈]。****
1. 選取&#x200B;**[!UICONTROL AEM]**&#x200B;並按一下&#x200B;**[!UICONTROL 發佈]**&#x200B;以將資產發佈到[!DNL AEM and Dynamic Media]。

   ![資產瀏覽](/help/assets/assets/browse-uactivation-immediate.svg)

   您無法發佈[!DNL Dynamic Media]發佈模式設為&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;的資料夾。 所有其他選取的資料夾或資產在選取[!DNL AEM and Dynamic Media]後會發佈至[!DNL AEM]。

   ![資產瀏覽](/help/assets/assets/browse-selective123.svg)

## 使用搜尋結果頁面發佈資產 {#publish-assets-using-search-results-page}

若要使用資產搜尋結果頁面發佈資產：

1. 在搜尋列中指定條件，然後按一下搜尋圖示以檢視結果。
1. 選取您需要發佈的資產，然後按一下&#x200B;**[!UICONTROL 發佈].**
1. 根據您的需求選取[!DNL AEM, Dynamic Media]或兩者，然後按一下&#x200B;**[!UICONTROL 發佈]**。

   ![搜尋影像](/help/assets/assets/search-mode.svg)

   在搜尋結果頁面上發佈到[!DNL Dynamic Media]的選項取決於在存放庫中可使用該資產的資料夾上設定的[!DNL Dynamic Media]發佈模式。

   >[!NOTE]
   >
   >如果您選取資料夾並從搜尋結果頁面按一下&#x200B;**[!UICONTROL 發佈]**，則[!DNL Experience Manager Assets]會顯示將資產發佈到[!DNL AEM]而非[!DNL Dynamic Media]的選項，無論資料夾的[!DNL Dynamic Media]發佈模式設定為何。

## 檢查發佈狀態 {#check-publish-status}

若要檢查資產或資料夾的已發佈狀態：

1. 按一下左窗格中可用的&#x200B;**[!UICONTROL Assets管理]**&#x200B;區段中的&#x200B;**[!UICONTROL Assets]**。
1. 使用檢視切換器切換至清單檢視。 您可以檢視資產屬性，例如[!UICONTROL AEM發佈]、[!UICONTROL Dynamic Media發佈]、[!UICONTROL 標題]、[!UICONTROL 大小]、[!UICONTROL 維度]等。

   如果未發佈資產或資料夾，資料行&#x200B;**[!UICONTROL AEM Publish]**&#x200B;和&#x200B;**[!UICONTROL Dynamic Media Publish]**&#x200B;的狀態會顯示為&#x200B;**[!UICONTROL N/A]**。

   ![檢查發佈狀態 1](/help/assets/assets/check-publish-status1.png)

   如果您無法在清單檢視中檢視[!DNL AEM]發佈和[!DNL Dynamic Media]發佈欄：

   1. 按一下![設定](/help/assets/assets/settings-icon.svg)，然後從&#x200B;**[!UICONTROL 可設定的資料行]**&#x200B;對話方塊中選取&#x200B;**[!UICONTROL AEM發佈]**&#x200B;和&#x200B;**[!UICONTROL Dynamic Media發佈]**&#x200B;資料行。
   1. 按一下&#x200B;**[!UICONTROL 確認]**。 [!DNL Experience Manager Assets]將選取的資料行新增至清單檢視。

      ![檢查發佈狀態2](/help/assets/assets/check-publish-status2.png)

您也可以選取資產並按一下&#x200B;**[!UICONTROL 詳細資料]**，以檢查資產發佈狀態。 這些詳細資料可在右窗格中的&#x200B;**[!UICONTROL 發佈]**&#x200B;區段中取得。 **[!UICONTROL 發佈]**&#x200B;區段會列出將資產發佈到[!DNL Dynamic Media]和[!DNL AEM]的日期。 如果您需要檢視資產發佈的時間，可以導覽至清單檢視並檢視這些詳細資訊。

![檢查發佈狀態3](/help/assets/assets/check-publish-status3.png)

## 限制 {#limitations}

將資產發佈至[!DNL AEM and Dynamic Media]時，下列功能暫時不在範圍內：

* 從[!DNL AEM and Dynamic Media]發佈資產到[!DNL Asset details page]。
* 使用「快速發佈」精靈將資產發佈的端點視覺化。
* 在快速發佈精靈中新增或刪除更多資產。
* 檢視已發佈資產的頁面。
* 可在資產層級複製或貼上[!DNL Dynamic Media] URL （如果資產已發佈至[!DNL Dynamic Media]）。
* 發佈至[!DNL AEM]時可發佈參考（資產、標籤等）。
* 能夠覆寫資料夾層級的[!DNL Dynamic Media]同步處理狀態。
* 能夠在資料夾層級覆寫[!DNL Dynamic Media]發佈模式
* 尚不支援管理發布。
