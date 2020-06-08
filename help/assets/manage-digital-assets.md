---
title: 在Experience Manager中管理您的數位資產
description: 瞭解各種資產管理和編輯方法。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d4b4b5fbbd07851485d216b502c66037cccef134
workflow-type: tm+mt
source-wordcount: '4419'
ht-degree: 12%

---


# Manage assets {#manage-assets}

本文說明如何在Adobe Experience Manager Assets中管理和編輯資產。 若要管理內容片段，請參 [閱內容片段](content-fragments/content-fragments.md) 。

## 建立資料夾 {#creating-folders}

組織資產集合（例如，所有影像）時， `Nature` 您可以建立資料夾以將資產保持在一起。 您可以使用資料夾來分類和組織您的資產。 AEM Assets不需要您在檔案夾中組織資產，以提高工作效率。

>[!NOTE]
>
>* 共用至Marketing Cloud時不 `sling:OrderedFolder`支援共用類型的「資產」檔案夾。 如果要共用資料夾，在建立資料夾時不 [!UICONTROL 要選擇] 「有序」。
>* Experience Manager不允許將 `subassets` Word用作資料夾的名稱。 它是為節點保留的關鍵字，其中包含複合資產的子資產


1. 導覽至您要建立新資料夾的數位資產檔案夾。 在功能表中，按一下「 **[!UICONTROL 建立]**」。 選擇「 **[!UICONTROL 新建資料夾]**」。
1. 在「標 **[!UICONTROL 題]** 」欄位中，提供檔案夾名稱。 依預設，DAM會使用您提供的標題作為檔案夾名稱。 建立資料夾後，您可以覆寫預設資料夾，並指定另一個資料夾名稱。
1. 按一下&#x200B;**[!UICONTROL 建立]**。您的資料夾會顯示在數位資產資料夾中。

不支援下列（以空格分隔的）字元清單：

* 資產檔案名稱不能包含下列任何字元： `* / : [ \\ ] | # % { } ? &`
* 資產檔案夾名稱不能包含下列任何字元： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Upload assets {#uploading-assets}

請參 [閱將數位資產新增至Experience Manager](add-assets.md)。

## 偵測重複資產 {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

如果DAM用戶上載儲存庫中已存在的一個或多個資產，則 [!DNL Experience Manager] 會檢測複製並通知用戶。 重複偵測預設會停用，因為它可能會根據儲存庫大小和上傳的資產數量，對效能產生影響。 若要啟用此功能，請設 [!UICONTROL 定Adobe AEM Cloud Asset Duplication Detector]。 了 [解如何進行OSGi配置](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html)。 複製檢測基於儲存在的唯 `dam:sha1` 一值 `jcr:content/metadata/dam:sha1`。 這表示即使檔案名稱不同，也會偵測到重複資產。

![偵測重複資產OSGi組態](assets/duplicate-detection.png)

啟用後，Experience Manager會將重複資產的通知傳送至收件匣。 它是多重複項的匯總結果。 使用者可以選擇根據結果移除資產。

![重複資產的收件匣通知](assets/duplicate-detect-inbox-notification.png)

## 預覽資產 {#previewing-assets}

若要預覽資產，請依照下列步驟進行。

1. 從「資產」使用者介面，導覽至您要預覽的資產所在的位置。
1. 點選所要的資產以將其開啟。

1. 在預覽模式中，支援的影像類型(使用互 [動式編輯](/help/assets/file-format-support.md) )可使用縮放選項。

   若要縮放資產，請點選／按一 `+` 下（或點選／按一下資產上的放大鏡）。 若要縮小，請點選／按一下 `-`。 當您放大時，可以透過平移來仔細檢視影像的任何區域。 重設縮放箭頭會將您帶回原始檢視。

   點選 **[!UICONTROL 「重設]** 」，將檢視重設為原始大小。

## 編輯屬性 {#editing-properties}

1. 導覽至您要編輯其中繼資料的資產所在位置。

1. 選取資產，然後點選／按一下工 **[!UICONTROL 具列中的]** 「屬性」以檢視資產屬性。 或者，選擇資 **[!UICONTROL 產卡上]** 「屬性」的快速動作。

   ![properties_quickaction](assets/properties_quickaction.png)

1. 在「屬 [!UICONTROL 性] 」頁面中，編輯各標籤下的中繼資料屬性。 例如，在「基 **[!UICONTROL 本]** 」標籤下，編輯標題、說明等。

   >[!NOTE]
   >
   >「屬性」頁面 [!UICONTROL 的版面配置] ，以及可用的中繼資料屬性，取決於基礎的中繼資料結構。 要瞭解如何修改「屬性」頁的 [!UICONTROL 佈局] ，請參 [閱元資料結構](/help/assets/metadata-schemas.md)。

1. 若要排程啟動資產的特定日期/時間，請使用「準時」欄位旁的日 **[!UICONTROL 期選擇器]** 。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 若要在特定持續時間後停用資產，請從「關閉時間」欄位旁的日期選擇器選擇停 **[!UICONTROL 用日期]** /時間。 停用日期應晚於資產的啟用日期。 在「關 [!UICONTROL 閉時間]」後，資產及其轉譯無法透過「資產」網頁介面或HTTP API使用。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在「標 **[!UICONTROL 記]** 」欄位中，選取一或多個標籤。 若要新增自訂標籤，請在方塊中輸入標籤名稱，然後按Enter鍵。 新標籤會儲存在AEM中。

   YouTube需要「標籤」才能發佈，並有YouTube的連結（如果找到適當的連結）。

   >[!NOTE]
   >
   >要建立標籤，您必須在CRX儲存庫的路 `/content/cq:tags/default` 徑上具有寫權限。

1. 若要檢視資產的使用情況統計資料，請按一下／點選「 **[!UICONTROL 前瞻分析]** 」標籤。

   使用統計資料包括：

   * 檢視或下載資產的次數
   * 使用資產的通道／裝置
   * 最近使用資產的創意解決方案

   如需詳細資訊，請參 [閱資產分析](assets-insights.md)。

1. 點選／按一下「 **[!UICONTROL 儲存並關閉]**」。

1. 導覽至「資產」使用者介面。 編輯的中繼資料屬性（包括標題、說明和標籤）會顯示在資產卡片的「卡片」檢視中，以及「清單」檢視中相關欄下。

## 複製資產 {#copying-assets}

複製資產或資料夾時，會複製整個資產或資料夾及其內容結構。 複製的資產或資料夾會在目標位置複製。 來源位置的資產不會變更。

不會結轉資產特定副本的少數屬性。 例如：

* 資產ID、建立日期和時間，以及版本和版本記錄。 有些屬性由屬性、 `jcr:uuid`和 `jcr:created`指示 `cq:name`。

* 每個資產及其每個轉譯的建立時間和參考路徑都是唯一的。

保留其他屬性和元資料資訊。 複製資產時不會建立部分復本。

1. 從「資產」UI中，選取一或多個資產，然後點選／按一下工具列 **[!UICONTROL 中的]** 「複製」圖示。 或者，從資 **[!UICONTROL 產卡]** 中選擇 ![Copy](assets/copy_icon.png) _copy_icon快速操作。

   >[!NOTE]
   >
   >如果您使用「復 [!UICONTROL 制] 」快速動作，一次只能複製一個資產。

1. 導覽至您要複製資產的位置。

   >[!NOTE]
   >
   >如果您在相同位置複製資產，AEM會自動產生名稱的變更。 例如，如果您複製標題為「資產」的 `Square`資產，AEM會自動產生其復本的標題 `Square1`。

1. 按一下工 **[!UICONTROL 具列中]** 的「貼上資產」圖示。 資產會複製到此位置。

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >「貼 **[!UICONTROL 上]** 」圖示可在工具列中使用，直到貼上作業完成為止。

### 移動或重新命名資產 {#moving-or-renaming-assets}

1. 導覽至您要移動的資產所在的位置。

1. 選取資產，然後點選／按一下工 **[!UICONTROL 具列中的]**![「移動」圖示](assets/move_icon.png) 。

1. 在「移動資產」精靈中，執行下列其中一項作業：

   * 指定資產移動後的名稱。 然後點選／按一 **[!UICONTROL 下]** 「下一步」繼續。

   * 點選／按一 **[!UICONTROL 下「取消]** 」以停止程式。
   >[!NOTE]
   >
   >* 如果新位置沒有同名的資產，您可以指定該資產的相同名稱。 但是，如果您將資產移至同名資產所在的位置，則應使用不同的名稱。 如果您使用相同的名稱，系統會自動產生名稱的變化。 例如，如果您的資產名稱為Square，系統會為其副本產生名稱Square1。
   >* 重新命名時，檔案名稱中不允許空格。


1. 在「選 **[!UICONTROL 擇目標]** 」對話框中，執行下列操作之一：

   * 導覽至資產的新位置，然後點選／按「下一 **[!UICONTROL 步]** 」繼續。

   * 點選／按一 **[!UICONTROL 下「上]** 」，返回「重新 **[!UICONTROL 命名]** 」畫面。

1. 如果要移動的資產有任何參照頁面、資產或系列，則「選擇目標」標籤旁 **[!UICONTROL 會顯示]** 「調整參 **[!UICONTROL 考」標籤]** 。

   在「調整參照」( **[!UICONTROL Adjust References)螢幕中執行下列操作之一]** :

   * 指定要根據新詳細資料調整的參照，然後點選／按一下「移 **[!UICONTROL 動]** 」繼續。

   * 從「調 **[!UICONTROL 整」欄]** ，選取／取消選取資產參照。
   * 點選／按一 **[!UICONTROL 下「上]** 」，返回「 **[!UICONTROL 選取目標]** 」畫面。

   * 點選／按一 **[!UICONTROL 下「取消]** 」以停止移動作業。

   如果您不更新參照，則參照會繼續指向資產的先前路徑。 如果您調整參照，它們會更新為新資產路徑。

### 管理轉譯 {#managing-renditions}

1. 您可以新增或移除資產的轉譯，但原始的轉譯除外。 導覽至您要新增或移除轉譯的資產位置。

1. 點選／按一下資產以開啟其資產頁面。

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 點選／按一下GlobalNav圖示，然後從清單中選 **[!UICONTROL 取]** 「轉譯」。

   ![renditions_menu](assets/renditions_menu.png)

1. 在「轉 **[!UICONTROL 譯]** 」面板中，檢視為資產產生的轉譯清單。

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >依預設，AEM Assets不會在預覽模式中顯示資產的原始轉譯。 如果您是管理員，可以使用覆蓋來設定AEM Assets，以在預覽模式中顯示原始轉譯。

1. 選取要檢視或刪除轉譯的轉譯。

   **刪除轉譯**

   從「轉譯」面板選取轉 **[!UICONTROL 譯]** ，然後點選／按一下工具列中的「 **[!UICONTROL 刪除轉譯]** 」圖示。 資產處理完成後，無法大量刪除轉譯。 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自 [!DNL Experience Manager] 訂以刪除特定轉譯或刪除資產，然後重新上傳已刪除的資產。

   ![delete_rendition圖示](assets/delete_renditionicon.png)

   **上傳新轉譯**

   導覽至資產的資產詳細資訊頁面，然後點選/按一下工具列中的「新增轉譯 **** 」圖示，以上傳資產的新轉譯。

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >如果您從「轉譯」面板選取轉譯 **** ，工具列會變更上下文，並僅顯示與轉譯相關的動作。不會顯示「上傳轉譯」圖示等選項。若要在工具列中檢視這些選項，請導覽至資產的詳細資訊頁面。

   您可以設定要顯示在影像或視訊資產詳細資料頁面的轉譯尺寸。 AEM Assets會根據您指定的維度，顯示具有精確或最接近的維度的轉譯。

   若要在資產詳細資料層級設定影像的轉譯尺寸，請覆蓋節 `renditionpicker` 點(`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`)並設定width屬性的值。設定屬性大 **[!UICONTROL 小 (長) (KB]** )以取代寬度，以根據影像大小自訂資產詳細資料頁面上的轉譯。對於基於大小的定製，如果匹配的 `preferOriginal` 格式副本的大小大於原始格式副本的大小，則屬性會為原始格式副本指定首選項。

   同樣地，您也可以透過覆蓋來自訂「注釋」頁面影像 `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`。

   ![chlimage_1-222](assets/chlimage_1-222.png)

   若要設定視訊資產的轉譯維度，請導覽至CRX `videopicker` 儲存庫中位於位置的節 `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`點、覆蓋節點，然後編輯適當的屬性。

   >[!NOTE]
   >
   >只有採用HTML5相容視訊格式的瀏覽器才支援視訊註解。 此外，視瀏覽器而定，支援不同的視訊格式。

## Delete assets {#delete-assets}

若要解析或移除其他頁面的傳入參照，請先更新相關參照，再刪除資產。

此外，使用覆蓋停用強制刪除按鈕，以禁止使用者刪除參照的資產並留下中斷的連結。

1. 瀏覽至您要刪除的資產所在的位置。

1. 選取資產，然後點選／按一下工具 **[!UICONTROL 列中的]** 「刪除」圖示。

   ![delete_icon](assets/delete_icon.png)

1. 在確認對話方塊中，按一下：

   * **[!UICONTROL 取消]** ，停止動作
   * **[!UICONTROL 刪除]**&#x200B;來確認動作：

      * 如果資產沒有參考，則會刪除資產。
      * 如果資產有參考，則會出現錯誤訊息通知您 **已參考一或多個資產。**&#x200B;您可以選取&#x200B;**[!UICONTROL 強制刪除]**&#x200B;或&#x200B;**[!UICONTROL 取消]**。

   >[!NOTE]
   >
   >您需要dam/asset的刪除權限才能刪除資產。 如果您只有修改權限，則只能編輯資產中繼資料並新增附註至資產。 不過，您無法刪除資產或其中繼資料。

   >[!NOTE]
   >
   >若要解析或移除其他頁面的傳入參照，請先更新相關參照，再刪除資產。
   >
   >
   >此外，使用覆蓋停用強制刪除按鈕，以禁止使用者刪除參照的資產並留下中斷的連結。

## 下載資產 {#download-assets}

See [Download assets from AEM](/help/assets/download-assets-from-aem.md).

## Publish assets {#publish-assets}

<!--
>[!NOTE]
>
>For more information specific to Dynamic Media, see [Publishing Dynamic Media Assets.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
-->

1. 導覽至您要發佈的資產／資料夾的位置。

1. 從資產卡 **[!UICONTROL 中選取「發佈]** 」快速動作，或選取資產，然後點選/按一下工具列中的「 **[!UICONTROL 快速發佈]** 」圖示。
1. 如果資產引用其他資產，其引用將列在嚮導中。 只會顯示自上次發佈／未發佈後未發佈或已修改的參照。 選擇要發佈的參照。

   ![chlimage_1-225](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >如果您要發佈的檔案夾包含空白檔案夾，則不會發佈空白檔案夾。

1. 點選／按一 **[!UICONTROL 下「發佈]** 」以確認資產的啟動。

>[!CAUTION]
>
>如果您發佈正在處理的資產，則只會發佈原始內容。 缺少轉譯。 等待處理完成，然後在處理完成後發佈或重新發佈資產。

## 取消發佈資產 {#unpublishing-assets}

1. 導覽至您要從發佈環境（解除發佈）移除的資產／資產檔案夾的位置。

1. 選取要解除發佈的資產／資料夾，然後點選／按一下工具列 **[!UICONTROL 中的「管理出版物]** 」圖示。

   ![manage_publication](assets/manage_publication.png)

1. 從清單 **[!UICONTROL 中選取]** 「取消發佈」動作。

   ![unpublish_action](assets/unpublish_action.png)

1. 若要稍後解除發佈資產，請選取「 **[!UICONTROL 稍後解除發佈]**」，然後選取要解除發佈資產的日期。
1. 排程資產在發佈環境中無法使用的日期。
1. 如果資產參考其他資產，請選擇您要取消發佈的參考。 點選／按一下「 **[!UICONTROL 解除發佈]**」。
1. 在確認對話方塊中，點選／按一下：

   * **[!UICONTROL 取消]** ，停止動作
   * **[!UICONTROL 取消發佈]** ，以確認資產在指定日期已取消發佈（在發佈環境中不再可用）。

   >[!NOTE]
   >
   >解除發佈複雜資產時，請僅解除發佈資產。 請避免取消發佈參照，因為其他已發佈資產可能會參照這些參照。

## Closed user group {#closed-user-group}

已關閉的使用者群組(CUG)可用來限制對從AEM發佈的特定資產資料夾的存取權。 如果為資料夾建立CUG，則對資料夾（包括資料夾資產和子資料夾）的訪問僅限分配的成員或組。 若要存取資料夾，他們必須使用其安全憑證登入。

CUG是限制存取您資產的額外方式。 您也可以設定資料夾的登入頁面。

1. 從「資產」使用者介面選取資料夾，然後點選／按一下工具列中的「屬性」圖示以顯示屬性頁面。
1. 在「權 **[!UICONTROL 限]** 」標籤中，在「已關閉的使用者群組」 **[!UICONTROL 下新增成員或群組]**。

   ![add_user](assets/add_user.png)

1. 若要在使用者存取資料夾時顯示登入畫面，請選取「啟 **[!UICONTROL 用]** 」選項。 然後，在AEM中選取登入頁面的路徑，並儲存變更。

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >如果您未指定登入頁面的路徑，AEM會在發佈例項中顯示預設登入頁面。

1. 發佈資料夾，然後嘗試從發佈例項存取資料夾。 隨即顯示登入畫面。
1. 如果您是CUG成員，請輸入您的安全憑據。 資料夾會在AEM驗證您後顯示。

## 搜尋資產 {#search-assets}

搜尋資產是數位資產管理系統的核心使用，不論是供創意人員進一步使用、由商業使用者和行銷人員強穩管理資產，或由DAM管理員管理。

如需簡單、進階和自訂搜尋，以發現和使用最適當的資產，請參閱「AEM [中的搜尋資產」](/help/assets/search-assets.md)。

## Quick actions {#quick-actions}

一次只有一個資產的快速動作圖示可用。視您的裝置而定，執行下列動作以顯示快速動作圖示：

* 觸控裝置： 輕觸並按住。 例如，在iPad上，您可以點選並按住資產，以便顯示快速動作。
* 非觸控裝置： 暫留指標。 例如，在案頭裝置上，如果您將指標暫留在資產縮圖上，就會顯示快速動作列。

## 編輯影像 {#editing-images}

AEM Assets介面中的編輯工具可讓您對影像資產執行小型編輯工作。 您可以裁切、旋轉、翻轉和執行其他影像編輯工作。 您也可以將影像地圖新增至資產。

>[!NOTE]
>
>對於某些元件，全屏模式還提供其他選項。

1. 執行下列任一項作業，以在編輯模式中開啟資產：

   * 選取資產，然後按一下／點選工具列 **[!UICONTROL 中的]** 「編輯」圖示。
   * 點選／按一 **[!UICONTROL 下]** 「卡片」檢視中資產上顯示的「編輯」圖示。
   * 在資產頁面中，點選／按一下工具 **[!UICONTROL 列中的]** 「編輯」圖示。

   ![edit_icon](assets/edit_icon.png)

1. 若要裁切影像，請點選／按一下「裁切 **」圖** 示。

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. 從清單中選取所需的選項。裁切區域會根據您選擇的選項出現在影像上。「自 **由手形** 」選項可讓您裁切影像，而不受任何外觀比例限制。

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. 選取要裁切的區域，並調整影像上的大小或位置。
1. 使用「 **完成** 」圖示（右上角）裁切影像。 按一下「完 **成** 」圖示也會觸發轉譯的重新產生。

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. 使用右 **上角的** 「復原」和「 **** 重做」圖示，分別回復至未裁切的影像或保留已裁切的影像。

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. 點選／按一下適當的「旋轉」圖示，以順時針或逆時針旋轉影像。

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. 點選／按一下適當的「反向」圖示，以水準或垂直反向影像。

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. 點選／按一下「 **完成** 」圖示以儲存變更。

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>BMP、GIF、PNG和JPEG檔案格式支援影像編輯。

<!-- You can also add image maps using the image editor. For details, see [Adding Image Maps](/help/assets/image-maps.md). -->

>[!NOTE]
>
>要編輯TXT檔案，請從配置管 **理器中設定Day CQ Link Externalizer** 。

## 時間軸 {#timeline}

時間軸可讓您檢視所選項目的各種事件，例如資產的作用中工作流程、註解／註解、活動記錄檔和版本。

![為資產圖排序時間軸](assets/sort_timeline.gif)*條目： 排序資產的時間軸項目*

>[!NOTE]
>
>在「系 [列」控制台](/help/assets/manage-collections.md#navigate-the-collections-console),「全 **[!UICONTROL 部顯示]** 」清單提供僅檢視注釋和工作流程的選項。 此外，時間軸只會針對控制台中列出的頂層系列顯示。 如果您在任何系列中導覽，則不會顯示它。

>[!NOTE]
>
>時間軸包含數 [個特定於內容片段的選項](content-fragments/content-fragments.md)。

## 備註 {#annotating}

註解是影像或視訊中新增的註解或說明註解。 註解可讓行銷人員協作並留下有關資產的意見回應。

只有採用HTML5相容視訊格式的瀏覽器才支援視訊註解。 AEM Assets支援的視訊格式取決於瀏覽器。

>[!NOTE]
>
>對於「內容片段」, [會在片段編輯器中建立註解](content-fragments/content-fragments.md)。

1. 導覽至您要新增附註的資產位置。
1. 點選／按一 **[!UICONTROL 下]** 下列其中一項的「註解」圖示：

   * [快速動作](#quick-actions)
   * 在選取資產或導覽至資產頁面後，從工具列

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. 在時間軸底部的 **[!UICONTROL 「注釋]** 」方塊中新增注釋。或者，在影像上標籤一個區域，並在「添加註釋」( **[!UICONTROL Add Annotation]** )對話框中添加註釋。

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>對於非管理員使用者，只有當使用者具有CRXDE中的「讀取」權限時，才會顯 `/home` 示建議。

![chlimage_1-235](assets/chlimage_1-235.png)

1. 添加註釋後，按一下「 **[!UICONTROL 添加]** 」(Add)保存注釋。 註解通知會傳送給Aaron。

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >您可以在儲存多個註解之前，先加入這些註解。

1. 點選／按一 **[!UICONTROL 下「關閉]** 」(Close)以退出「注釋」模式。
1. 若要檢視通知，請使用Aaron MacDonald的認證登入AEM Assets，然後按一下「 **[!UICONTROL Notifications]** 」圖示以檢視通知。

   >[!NOTE]
   >
   >您也可以將註解新增至視訊資產。 在為視訊加上註解時，播放器會暫停，讓您在影格上加上註解。 如需詳細資訊，請參 [閱「管理視訊資產](manage-video-assets.md)」。

1. 若要選擇不同的顏色以便區分使用者，請按一下／點選「描述檔」圖示，然後按一下／點選「我的偏 **[!UICONTROL 好設定」]**。

   ![chlimage_1-237](assets/chlimage_1-237.png)

   在「注釋顏色」( **[!UICONTROL Annotation Color)框中指定所要的顏色]** ，然後按一下/點選「 **[!UICONTROL 接受」(Accept]**)。

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>您也可以新增註解至系列。 不過，如果系列包含子系列，您只能將註解／留言新增至父系列。 子系列無法使用「註解」選項。

### 查看保存的注釋 {#viewing-saved-annotations}

1. 要查看資產的已保存批注，請定位至資產的位置並開啟資產的資產頁。

1. 點選／按一下GlobalNav圖示，然後從清 **[!UICONTROL 單中選擇]** 「時間軸」。

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. 從時間軸 **[!UICONTROL 的「顯示全部]** 」清單中，選取「注 **[!UICONTROL 釋]** 」以根據註解來篩選結果。

   ![chlimage_1-240](assets/chlimage_1-240.png)

   在「時間軸」面板中點選／按 **[!UICONTROL 一下注釋]** ，以檢視影像上的對應註解。

   ![chlimage_1-241](assets/chlimage_1-241.png)

   點選／按一 **[!UICONTROL 下「刪除]**」，以刪除特定留言。

### 列印註解 {#printing-annotations}

如果資產有註解或已經受審核工作流程，您可以將資產連同註解列印為PDF檔案，以便離線審核。

您也可以選擇僅打印注釋或查看狀態。

要打印注釋和查看狀態，請點選／按一下「 **[!UICONTROL Print]** （打印）」表徵圖，然後按照嚮導中的說明操作。 只有當資 **[!UICONTROL 產至少指派了一個註解或審閱狀態時，「列印]** 」圖示才會出現在工具列中。

1. 從「資產」使用者介面，開啟資產的預覽頁面。
1. 執行下列任一項作業：

   * 要打印所有注釋和審閱狀態，請跳過步驟3並直接轉到步驟4。
   * 若要列印特定的註解和檢閱狀態，請開啟 [時間軸](/help/assets/manage-digital-assets.md#timeline) ，然後移至步驟3。

1. 要打印特定注釋，請從時間軸中選擇注釋。

   ![chlimage_1-242](assets/chlimage_1-242.png)

   要僅打印審閱狀態，請從時間軸中選擇它。

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Tap/click the **[!UICONTROL Print]** icon from the toolbar.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. 從「列印」對話方塊中，選擇您要在PDF上顯示註解／審閱狀態的位置。 例如，如果您希望註解／狀態列印在包含已列印影像之頁面的右上角，請使用左上 **角設定** 。 預設會選取它。

   ![chlimage_1-245](assets/chlimage_1-245.png)

   您可以根據要在打印的PDF中顯示注釋/狀態的位置選擇其他設定。如果您希望註解/狀態顯示在與印刷資產不同的頁面中，請選擇「下 **[!UICONTROL 一頁」]**。

   >[!NOTE]
   >
   >冗長的註解可能無法在PDF檔案中正確呈現。 為獲得最佳演算效果，Adobe建議您將註解限制在50字以內。

1. 點選/按一下「 **[!UICONTROL 列印]**」。根據您在步驟2中選擇的選項，產生的PDF會在指定位置顯示註解/狀態。例如，如果您選擇使用左上角設定打印注釋和審閱狀態 **** ，則生成的輸出類似於此處所示的PDF檔案。

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. 使用右上角的選項下載或列印PDF。

   ![chlimage_1-247](assets/chlimage_1-247.png)

   要修改渲染的PDF檔案的外觀，例如注釋和狀態的字型顏色、大小和樣式、背景顏色，請從「配置管理器」(Configuration Manager)開啟「注釋 **[!UICONTROL PDF」(]** Annotation PDF)配置，並修改所需的選項。 例如，要更改批准狀態的顯示顏色，請修改相應欄位中的顏色代碼。 有關更改批注的字型顏色的資訊，請參 [閱注釋](/help/assets/manage-digital-assets.md#annotating)。

   ![chlimage_1-248](assets/chlimage_1-248.png)

   返回轉譯的PDF檔案並重新整理它。 重新整理的PDF會反映您所做的變更。

## 資產版本控制 {#asset-versioning}

版本設定會建立數位資產在特定時間點的快照。版本修訂功能有助於將資產還原為先前的狀態。 例如，如果您想要還原對資產所做的變更，請還原未編輯的資產版本。

以下是您建立版本的案例：

* 您可以修改不同應用程式中的影像，並上傳至AEM Assets。 會建立影像版本，以免覆寫原始影像。
* 您可以編輯資產的中繼資料。
* 您使用AEM案頭應用程式來結帳現有資產並儲存變更。 每次儲存資產時，都會建立新版本。

您也可以透過工作流程啟用自動版本修訂。 當您為資產建立版本時，中繼資料和轉譯會與版本一起儲存。 轉譯是相同影像的替代格式，例如已上傳JPEG檔案的PNG轉譯。

版本控制功能可讓您執行下列動作：

* 建立資產版本。
* 檢視資產的目前修訂。
* 將資產還原為舊版。

1. 導覽至您要建立版本的資產所在位置，點選／按一下該位置以開啟其資產頁面。

1. 點選／按一下GlobalNav圖示，然後從選單 **[!UICONTROL 選擇]** 「時間軸」。

   ![時間軸](assets/timeline.png)

1. 點選／按一 **[!UICONTROL 下底部的]** 「動作（箭頭）」圖示，以檢視可對資產執行的可用動作。

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. 點選／按一 **[!UICONTROL 下「另存為版本]** 」以建立資產的版本。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 新增標籤和註解，然後按一下「 **[!UICONTROL 建立]** 」以建立版本。 或者，點選／按一 **下「取消** 」以退出作業。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 若要檢視新版本，請從資產詳細資 **[!UICONTROL 訊頁面或資產UI開啟時間軸中的「顯示全部]** 」清單，然後選擇「版 **[!UICONTROL 本」]**。為資產建立的所有版本都會列在時間軸標籤下。您可以按一下下拉箭頭並從清單中選取「版本」，篩選清單以顯 **[!UICONTROL 示「版本]** 」。

   ![versions_option](assets/versions_option.png)

1. 為資產選取特定版本以進行預覽，或讓資產顯示在資產UI中。

   ![select_version](assets/select_version.png)

1. 新增版本的標籤和註解，以回復至資產UI中的特定版本。

   ![save_version](assets/save_version.png)

1. 若要產生版本的預覽，請點選/按一下「預 **[!UICONTROL 覽版本」]**。
1. 若要在資產UI中顯示此版本，請選取「 **[!UICONTROL 回復至此版本」]**。
1. 若要比較兩個版本，請前往資產的資產頁面，點選／按一下要與目前版本比較的版本。

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. 從時間軸中，選取您要比較的版本，並將滑桿拖曳至左側，將此版本重疊在目前版本上並進行比較。

   ![compare_versions](assets/compare_versions.png)

### 在資產上啟動工作流程 {#starting-a-workflow-on-an-asset}

1. 導覽至您要啟動工作流程的資產所在位置，然後點選／按一下資產以開啟資產頁面。
1. 點選／按一下GlobalNav圖示，然後從選單中選 **[!UICONTROL 擇]** 「時間軸」以顯示時間軸。

   ![timeline-1](assets/timeline-1.png)

1. 點選／按一 **[!UICONTROL 下底部的]** 「動作（箭頭）」圖示，以開啟資產可用的動作清單。

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. 點選／按一 **[!UICONTROL 下清單中的「開始工作流程]** 」。

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. （可選）指定工作流的標題，可用來參考工作流實例。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 點選/按一 **[!UICONTROL 下「開始]** 」，然後點選/按一下對話 **[!UICONTROL 方塊中的「繼續]** 」以進行確認。工作流程的每個步驟都會以事件的形式顯示在時間軸中。

   ![chlimage_1-256](assets/chlimage_1-256.png)

## 集合 {#collections}

系列是一組已訂購的資產。 使用系列在使用者之間共用資產。

* 系列可以包含不同位置的資產，因為它們只包含這些資產的參考。 每個系列都會維護資產的參考完整性。
* 您可以與擁有不同權限層級的多位使用者共用系列，包括編輯、檢視等。

如需系列 [管理的詳細資訊](/help/assets/manage-collections.md) ，請參閱管理系列。
