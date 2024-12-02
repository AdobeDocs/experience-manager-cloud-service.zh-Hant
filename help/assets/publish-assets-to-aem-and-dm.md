---
title: Publish快速移至AEM和Dynamic Media
description: Assets檢視中的快速Publish可讓您同時或分別將資產發佈至AEM和Dynamic Media。 您可以選取資產和資料夾，然後選擇發佈至Dynamic Media或AEM。
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: 8ab19fe82fc390d28d33b17222177fd8486c8fc7
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 2%

---

# 發佈資產至 AEM 和 Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Experience Manager Assets可讓您使用Assets檢視快速將資產發佈到Experience Manager和Dynamic Media。 這可確保您管理資產，然後使用[Assets檢視發佈資產，而不需切換至管理員檢視](/help/assets/overview.md##persona-based-experiences)。

Experience Manager Assets檢視可讓您靈活地將資產同時發佈至AEM或Dynamic Media （或兩者）。 您可以在上傳、瀏覽和搜尋資產時發佈資產。 本文會詳細說明這些發佈資產的選項。

## 開始之前 {#before-you-begin}

設定這些設定以檢視AEM和Dynamic Media的發佈選項：

* 若要檢視Dynamic Media的發佈選項，請使用「管理員」檢視來設定下列設定：

   * [建立Dynamic Media雲端設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)。
   * 在資料夾層級設定Dynamic Media Publish模式。 您也可以在建立Dynamic Media雲端設定時進行這些設定。 若要覆寫資料夾層級的這些設定，請參閱[在Dynamic Media的資料夾層級設定選擇性Publish ](/help/assets/dynamic-media/selective-publishing.md)。

* 若要檢視AEM的發佈選項，您必須為環境設定AEM發佈端點。

## 上傳期間的Publish Assets {#piblish-assets-during-upload}

將資產上傳至資料夾時，您可以將資產發佈至AEM和Dynamic Media。 顯示的發佈選項取決於在資產上傳到的資料夾上設定的Dynamic Media發佈模式。 Dynamic Media發佈模式可以設為：

* **啟動時：**&#x200B;將資產上傳至此資料夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。

* **立即：**&#x200B;將資產上傳至此資料夾時，系統會將這些資產擷取至Experience Manager，並立即提供URL/內嵌。
* **選擇性Publish：** Assets已發佈至您選擇的Experience Manager或Dynamic Media，以便在公用網域中傳送。

### Dynamic Media Publish模式設定為「啟動時」 {#dynamic-media-publish-mode-set-to-upon-activation}

若要在上傳至資料夾期間發佈資產，並將Dynamic Media Publish模式設定為&#x200B;**啟動時**：

1. 按一下「**新增Assets**」>「**瀏覽**」>「**瀏覽檔案**」以瀏覽至適當的資料夾以上傳資產。 **Publish選項**&#x200B;區段會將&#x200B;**DM Publish模式**&#x200B;顯示為&#x200B;**啟動時**。
   ![啟動時上傳影像](/help/assets/assets/upload-uactivation.svg)
2. 選取&#x200B;**Publish至AEM和Dynamic Media**，然後按一下&#x200B;**上傳**。 資產會同時發佈至AEM和Dynamic Media。 若要檢視這些資產的更新發佈狀態，請參閱[檢查Publish狀態](#check-publish-status)。

### Dynamic Media Publish模式設為「立即」 {#dynamic-media-publish-mode-set-to-immediate}

若要在上傳至資料夾期間發佈資產，且Dynamic Media Publish模式設定為&#x200B;**立即**：

1. 按一下「**新增Assets**」>「**瀏覽**」>「**瀏覽檔案**」以瀏覽至適當的資料夾以上傳資產。 Publish選項區段會將&#x200B;**DM Publish模式**&#x200B;顯示為&#x200B;**立即**。
   ![檔案上傳影像 — 立即模式](/help/assets/assets/resized-image-pdf-svg-new.svg)


   由於Dynamic Media Publish模式為&#x200B;**立即**，當您按一下&#x200B;**上傳**&#x200B;時，已上傳的資產會自動發佈至Dynamic Media。

2. 選取Publish以&#x200B;**AEM將已上傳的資產發佈至AEM**，然後按一下「上傳」。

   如果您選取&#x200B;**將Publish發佈至AEM**，資產會發佈至AEM和Dynamic Media，否則資產會發佈至Dynamic Media。

   若要檢視這些資產的更新發佈狀態，請參閱[檢查Publish狀態](#check-publish-status)。

### Dynamic Media Publish模式設為選擇性Publish {#dynamic-media-publish-mode-set-to-selective-publish}

若要在上傳至資料夾期間發佈資產，且Dynamic Media Publish模式設定為&#x200B;**選擇性Publish**：

1. 按一下「**新增Assets**」>「**瀏覽**」>「**瀏覽檔案**」以瀏覽至適當的資料夾以上傳資產。 Publish選項區段會將&#x200B;**DM Publish模式**&#x200B;顯示為&#x200B;**選擇性Publish**。
   ![上傳影像選擇性筆畫模式](/help/assets/assets/upload-selective.svg)

2. 根據您的需求，選取&#x200B;**Publish到AEM**、**Publish到Dynamic Media**&#x200B;或兩者，然後按一下&#x200B;**上傳**。

   資產會根據您的選擇發佈至AEM和Dynamic Media。

   若要檢視這些資產的更新發佈狀態，請參閱[檢查Publish狀態](#check-publish-status)。

## 使用資產瀏覽頁面的Publish資產 {#publish-assets-using-asset-browse-page}

若要使用資產瀏覽頁面發佈資產：

1. 按一下左窗格中可用的&#x200B;**Assets管理**&#x200B;區段中的&#x200B;**Assets**。
2. 選取一或多個您需要發佈的資產或資料夾，然後按一下&#x200B;**Publish**。
3. 選取&#x200B;**AEM**，然後按一下&#x200B;**Publish**，將資產發佈至AEM和Dynamic Media。
   ![資產瀏覽](/help/assets/assets/browse-uactivation-immediate.svg)
您無法發佈Dynamic Media Publish模式設為**選擇性發佈的資料夾。**選取AEM後，所有其他選取的資料夾或資產會發佈至AEM和Dynamic Media。
   ![資產瀏覽](/help/assets/assets/browse-selective123.svg)

## 使用搜尋結果頁面的Publish資產 {#publish-assets-using-search-results-page}

若要使用資產搜尋結果頁面發佈資產：

1. 在搜尋列中指定條件，然後按一下搜尋圖示以檢視結果。
2. 選取您需要發佈的資產，然後按一下&#x200B;**Publish。**
3. 根據您的需求選取AEM、Dynamic Media或兩者，然後按一下&#x200B;**Publish。**
   ![搜尋影像](/help/assets/assets/search-mode.svg)
在搜尋結果頁面上發佈至Dynamic Media的選項取決於在存放庫中可供資產使用的資料夾上設定的Dynamic Media Publish模式。

   >[!NOTE]
   >
   >如果您選取資料夾並從搜尋結果頁面按一下「**Publish**」，Experience Manager Assets會顯示將資產發佈至AEM而非Dynamic Media的選項，無論資料夾的Dynamic Media Publish模式設定為何。

## 檢查Publish狀態 {#check-publish-status}

若要檢查資產或資料夾的已發佈狀態：

1. 按一下左窗格中可用的&#x200B;**[!UICONTROL Assets管理]**&#x200B;區段中的&#x200B;**[!UICONTROL Assets]**。
2. 使用檢視切換器切換至清單檢視。 您可以檢視資產屬性，例如AEM發佈、Dynamic Media Publish、標題、大小、維度等。\
   如果未發佈資產或資料夾，資料行&#x200B;**AEM Publish**&#x200B;和&#x200B;**Dynamic Media Publish**&#x200B;的狀態會顯示為&#x200B;**不適用。**
   ![檢查發佈狀態1](/help/assets/assets/check-publish-status1.png)
如果您無法在清單檢視中檢視AEM Publish和Dynamic Media Publish欄：
   1. 按一下![設定](/help/assets/assets/settings-icon.svg)，然後從&#x200B;**可設定的資料行**&#x200B;對話方塊中選取&#x200B;**AEM Publish**&#x200B;和&#x200B;**Dynamic Media Publish**&#x200B;資料行。
   2. 按一下&#x200B;**確認。** Experience Manager Assets將選取的欄新增至清單檢視。

      ![檢查發佈狀態2](/help/assets/assets/check-publish-status2.png)

您也可以選取資產並按一下[詳細資料]，以檢查資產發佈狀態。****&#x200B;詳細資料可在右窗格的&#x200B;**Publish**&#x200B;區段中取得。 **Publish**&#x200B;區段會列出將資產發佈至Dynamic Media和AEM的日期。 如果您需要檢視資產發佈的時間，可以導覽至清單檢視並檢視這些詳細資訊。

![檢查發佈狀態3](/help/assets/assets/check-publish-status3.png)

## 限制 {#limitations}

將資產發佈到AEM和Dynamic Media時，下列功能暫時不在範圍內：

* 從資產詳細資訊頁面，將Publish資產轉移至AEM和Dynamic Media。
* 使用「快速Publish」精靈將資產發佈的端點視覺化。
* 在快速Publish精靈中新增或刪除更多資產。
* 檢視已發佈資產的頁面。
* 可在資產層級複製或貼上Dynamic Media URL (如果資產已發佈至Dynamic Media)。
* 可在發佈至AEM時發佈參考（資產、標籤等）。
* 能夠覆寫檔案夾層級的Dynamic Media同步狀態。
* 可在檔案夾層級覆寫Dynamic Media Publish模式
* 尚不支援管理發布。
