---
title: 快速發佈至AEM和Dynamic Media
description: 資產檢視中的快速發佈可讓您同時或個別將資產發佈到AEM和Dynamic Media。 您可以選取資產和資料夾，然後選擇發佈至Dynamic Media或AEM。
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
source-git-commit: 0891d58e10e8be746c0be5f55d554174567fcd64
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# 將資產發佈到AEM和Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

Experience Manager Assets可讓您使用「資產」檢視快速將資產發佈到Experience Manager和Dynamic Media。 這可確保您管理資產，然後使用發佈它們 [未切換至「管理員」檢視的「資產」檢視](/help/assets/overview.md##persona-based-experiences).

Experience Manager Assets檢視可讓您靈活地將資產同時發佈至AEM或Dynamic Media （或兩者）。 您可以在上傳、瀏覽和搜尋資產時發佈資產。 本文會詳細說明發佈資產的所有選項。

## 開始之前 {#before-you-begin}

設定這些設定以檢視AEM和Dynamic Media的發佈選項：

* 若要檢視Dynamic Media的發佈選項，請使用「管理員檢視」設定下列設定：

   * [建立Dynamic Media雲端設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * 在資料夾層級設定Dynamic Media發佈模式。 您也可以在建立Dynamic Media雲端設定時進行這些設定。 若要覆寫資料夾層級的這些設定，請參閱 [在Dynamic Media中設定資料夾層級的選取發佈](/help/assets/dynamic-media/selective-publishing.md).

* 若要檢視AEM的發佈選項，您必須為環境設定AEM發佈端點。

## 上傳時發佈資產 {#piblish-assets-during-upload}

將資產上傳至資料夾時，您可以將資產發佈至AEM和Dynamic Media。 顯示的發佈選項取決於資產上傳目的地資料夾上的Dynamic Media發佈模式設定。 Dynamic Media發佈模式可以設為：

* **啟動時：** 將資產上傳至此資料夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。

* **立即：** 將資產上傳至此資料夾時，系統會將這些資產擷取至Experience Manager，並立即提供URL/內嵌。
* **選擇性發佈：** 資產會發佈至您選擇的Experience Manager或Dynamic Media，以便在公共網域中傳送。

### Dynamic Media發佈模式設定為「啟動時」 {#dynamic-media-publish-mode-set-to-upon-activation}

若要在上傳至資料夾期間發佈資產，且Dynamic Media發佈模式設定為 **啟動時**：

1. 按一下 **新增資產** > **瀏覽** > **瀏覽檔案** 導覽至適當的資料夾以上傳資產。 此 **發佈選項** 區段顯示 **DM發佈模式** 作為 **啟動時**.
   ![啟動時上傳影像](/help/assets/assets/upload-upon-activation.png)
2. 選取 **發佈至AEM和Dynamic Media** 並按一下 **上傳**. 資產會同時發佈至AEM和Dynamic Media。 若要檢視這些資產的更新發佈狀態，請參閱 [檢查發佈狀態](#check-publish-status).

### Dynamic Media發佈模式設定為立即 {#dynamic-media-publish-mode-set-to-immediate}

若要在上傳至資料夾期間發佈資產，且Dynamic Media發佈模式設定為 **立即**：

1. 按一下 **新增資產** > **瀏覽** > **瀏覽檔案** 導覽至適當的資料夾以上傳資產。 「發佈選項」段落會顯示 **DM發佈模式** 作為 **立即**.
   ![檔案上傳影像 — 立即模式](/help/assets/assets/upload-immediate-mode.png)
由於Dynamic Media發佈模式為 **立即**，則上傳的資產會在您按一下時自動發佈至Dynamic Media **上傳**.

2. 選取發佈至 **要發佈的AEM** 已將資產上傳到AEM，然後按一下「上傳」。

   如果您選取 **發佈至AEM**，資產會發佈至AEM和Dynamic Media，否則資產會發佈至Dynamic Media。

   若要檢視這些資產的更新發佈狀態，請參閱 [檢查發佈狀態](#check-publish-status).

### Dynamic Media發佈模式設為選擇性發佈 {#dynamic-media-publish-mode-set-to-selective-publish}

若要在上傳至資料夾期間發佈資產，且Dynamic Media發佈模式設定為 **選擇性發佈**：

1. 按一下 **新增資產** > **瀏覽** > **瀏覽檔案** 導覽至適當的資料夾以上傳資產。 發佈選項區段會顯示 **DM發佈模式** 作為 **選擇性發佈**.
   ![上傳影像選擇性印刷模式](/help/assets/assets/upload-image-selective-publish-mode.png)

2. 選取 **發佈至AEM**， **發佈至Dynamic Media**，或根據您的需求選擇兩者，然後按一下 **上傳**.

   資產會根據您的選擇發佈至AEM和Dynamic Media。

   若要檢視這些資產的更新發佈狀態，請參閱 [檢查發佈狀態](#check-publish-status).

## 使用資產瀏覽頁面發佈資產 {#publish-assets-using-asset-browse-page}

若要使用資產瀏覽頁面發佈資產：

1. 按一下 **資產** 在 **資產管理** 區段可在左窗格中使用。
2. 選取您需要發佈的資產或資料夾，然後按一下 **發佈**.
3. 選取 **AEM** 並按一下 **發佈** 將資產發佈至AEM和Dynamic Media。
   ![資產瀏覽](/help/assets/assets/assets-browse-1.png)
您無法發佈Dynamic Media發佈模式設定為的資料夾 **選擇性發佈。** 所有其他選取的資料夾或資產在選取AEM後會發佈至AEM和Dynamic Media。
   ![資產瀏覽](/help/assets/assets/assets-browse-2.png)

## 使用搜尋結果頁面發佈資產 {#publish-assets-using-search-results-page}

若要使用資產搜尋結果頁面發佈資產：

1. 在搜尋列中指定條件，然後按一下搜尋圖示以檢視結果。
2. 選取您需要發佈的資產，然後按一下 **發佈。**
3. 根據您的需求選取AEM、Dynamic Media或兩者，然後按一下 **發佈。**
   ![搜尋影像](/help/assets/assets/search-image1.png)
在搜尋結果頁面上發佈至Dynamic Media的選項取決於在存放庫中可使用該資產的資料夾上設定的Dynamic Media發佈模式。

   >[!NOTE]
   >
   >如果您選取資料夾並按一下 **發佈** 從搜尋結果頁面，Experience Manager Assets會顯示將資產發佈到AEM而非Dynamic Media的選項，無論資料夾的Dynamic Media發佈模式設定為何。

## 檢查發佈狀態 {#check-publish-status}

若要檢查資產或資料夾的發佈狀態：

1. 按一下 **[!UICONTROL 資產]** 在 **[!UICONTROL 資產管理]** 區段可在左窗格中使用。
2. 使用檢視切換器切換至清單檢視。 您可以檢視資產屬性，例如AEM Publish、Dynamic Media Publish、標題、大小、維度等。\
   如果資產或資料夾未發佈，則狀態 **AEM發佈** 和 **Dynamic Media發佈** 欄會顯示為 **不適用**
   ![檢查發佈狀態1](/help/assets/assets/check-publish-status1.png)
如果您無法在清單檢視中檢視AEM Publish和Dynamic Media Publish欄：
   1. 按一下 ![設定](/help/assets/assets/settings-icon.svg) 並選取 **AEM發佈** 和 **Dynamic Media發佈** 欄來自 **可設定的欄** 對話方塊。
   2. 按一下 **確認。** Experience Manager Assets會將選取的欄新增至清單檢視。

      ![檢查發佈狀態2](/help/assets/assets/check-publish-status2.png)

您也可以選取資產並按一下，以檢查資產發佈狀態 **詳細資訊。** 詳細資訊可在以下連結中取得： **發佈** 區段可在右窗格中使用。 此 **發佈** 區段列出將資產發佈至Dynamic Media和AEM的日期。 如果您需要檢視資產發佈的時間，可以導覽至清單檢視並檢視這些詳細資訊。

![檢查發佈狀態3](/help/assets/assets/check-publish-status3.png)

## 限制 {#limitations}

將資產發佈到AEM和Dynamic Media時，下列功能暫時不在範圍內：

* 從資產詳細資訊頁面發佈資產到AEM和Dynamic Media。
* 使用「快速發佈」精靈將資產發佈的端點視覺化。
* 在快速發佈精靈中新增或刪除更多資產。
* 檢視已發佈資產的頁面。
* 可在資產層級複製或貼上Dynamic Media URL (如果資產已發佈至Dynamic Media)。
* 可在發佈至AEM時發佈參考（資產、標籤等）。
* 能夠覆寫檔案夾層級的Dynamic Media同步狀態。
* 可在檔案夾層級覆寫Dynamic Media發佈模式
* 尚不支援管理發布。
