---
title: 快速發佈至AEM和Dynamic Media
description: Assets檢視中的快速發佈可讓您同時或分別將資產發佈至AEM和Dynamic Media。 您可以選取資產和資料夾，然後選擇發佈至Dynamic Media或AEM。
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 2%

---

# 發佈資產至 AEM 和 Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

Experience Manager Assets可讓您使用Assets檢視快速將資產發佈到Experience Manager和Dynamic Media。 這可確保您管理資產，然後使用[Assets檢視發佈資產，而不需切換至管理員檢視](/help/assets/overview.md##persona-based-experiences)。

Experience Manager Assets檢視可讓您彈性地同時將資產發佈至AEM和/或Dynamic Media。 您可以在上傳、瀏覽和搜尋資產時發佈資產。 本文會詳細說明這些發佈資產的選項。

## 開始之前 {#before-you-begin}

設定這些設定以檢視AEM和Dynamic Media的發佈選項：

* 若要檢視Dynamic Media的發佈選項，請使用「管理員」檢視來設定下列設定：

   * [建立Dynamic Media雲端設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)。
   * 在資料夾層級設定Dynamic Media發佈模式。 您也可以在建立Dynamic Media雲端設定時進行這些設定。 若要覆寫資料夾層級的這些設定，請參閱[在Dynamic Media中設定資料夾層級的選擇性發佈](/help/assets/dynamic-media/selective-publishing.md)。

* 若要檢視AEM的發佈選項，您必須為環境設定AEM發佈端點。

## 上傳時發佈Assets {#piblish-assets-during-upload}

將資產上傳至資料夾時，您可以將資產發佈至AEM和Dynamic Media。 顯示的發佈選項取決於資產上傳所在資料夾的Dynamic Media發佈模式設定。 Dynamic Media發佈模式可設為：

* **啟動時：**&#x200B;將資產上傳至此資料夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。

* **立即：**&#x200B;將資產上傳至此資料夾時，系統會將這些資產擷取至Experience Manager，並立即提供URL/Embed。
* **選擇性發佈：** Assets已發佈至您選擇的Experience Manager或Dynamic Media，以便在公共網域中傳送。

### Dynamic Media發佈模式設定為（啟動時） {#dynamic-media-publish-mode-set-to-upon-activation}

若要在資產上傳至Dynamic Media發佈模式設定為&#x200B;**啟動時**&#x200B;的資料夾時發佈資產：

1. 按一下「**新增Assets**」>「**瀏覽**」>「**瀏覽檔案**」以瀏覽至適當的資料夾以上傳資產。 **發佈選項**&#x200B;區段會將&#x200B;**DM發佈模式**&#x200B;顯示為&#x200B;**啟動時**。
   ![啟動時上傳影像](/help/assets/assets/upload-uactivation.svg)
2. 選取&#x200B;**發佈至AEM和Dynamic Media**&#x200B;並按一下&#x200B;**上傳**。 資產會同時發佈至AEM和Dynamic Media。 若要檢視這些資產的更新發佈狀態，請參閱[檢查發佈狀態](#check-publish-status)。

### Dynamic Media發佈模式設為立即 {#dynamic-media-publish-mode-set-to-immediate}

若要在資產上傳至Dynamic Media發佈模式設定為&#x200B;**立即**&#x200B;的資料夾時發佈資產：

1. 按一下「**新增Assets**」>「**瀏覽**」>「**瀏覽檔案**」以瀏覽至適當的資料夾以上傳資產。 **發佈選項**&#x200B;區段會將&#x200B;**DM發佈模式**&#x200B;顯示為&#x200B;**立即**。
   ![檔案上傳影像 — 立即模式](/help/assets/assets/resized-image-pdf-svg-new.svg)


   由於Dynamic Media發佈模式為&#x200B;**立即**，當您按一下&#x200B;**上傳**&#x200B;時，已上傳的資產會自動發佈至Dynamic Media。

2. 選取&#x200B;**發佈至AEM**&#x200B;以將上傳的資產發佈至AEM，然後按一下「上傳」。

   如果您選取&#x200B;**發佈至AEM**，資產會發佈至AEM和Dynamic Media，否則資產會發佈至Dynamic Media。

   若要檢視這些資產的更新發佈狀態，請參閱[檢查發佈狀態](#check-publish-status)。

### Dynamic Media發佈模式設為選擇性發佈 {#dynamic-media-publish-mode-set-to-selective-publish}

若要在Dynamic Media發佈模式設為&#x200B;**選擇性發佈**&#x200B;的資料夾中，於上傳期間發佈資產：

1. 按一下「**新增Assets**」>「**瀏覽**」>「**瀏覽檔案**」以瀏覽至適當的資料夾以上傳資產。 **發佈選項**&#x200B;區段會將&#x200B;**DM發佈模式**&#x200B;顯示為&#x200B;**選擇性發佈**。
   ![上傳影像選擇性筆畫模式](/help/assets/assets/upload-selective.svg)

2. 根據您的需求，選取&#x200B;**發佈至AEM**、**發佈至Dynamic Media**&#x200B;或兩者，然後按一下&#x200B;**上傳**。

   資產會根據您的選擇發佈至AEM和Dynamic Media。

   若要檢視這些資產的更新發佈狀態，請參閱[檢查發佈狀態](#check-publish-status)。

## 使用資產瀏覽頁面發佈資產 {#publish-assets-using-asset-browse-page}

若要使用資產瀏覽頁面發佈資產：

1. 按一下左窗格中可用的&#x200B;**Assets管理**&#x200B;區段中的&#x200B;**Assets**。
2. 選取一或多個您需要發佈的資產或資料夾，然後按一下[發佈]。****
3. 選取&#x200B;**AEM**，然後按一下&#x200B;**發佈**，將資產發佈到AEM和Dynamic Media。
   ![資產瀏覽](/help/assets/assets/browse-uactivation-immediate.svg)
您無法發佈Dynamic Media發佈模式設為**選擇性發佈的資料夾。**所有其他選取的資料夾或資產在選取AEM後會發佈至AEM和Dynamic Media。
   ![資產瀏覽](/help/assets/assets/browse-selective123.svg)

## 使用搜尋結果頁面發佈資產 {#publish-assets-using-search-results-page}

若要使用資產搜尋結果頁面發佈資產：

1. 在搜尋列中指定條件，然後按一下搜尋圖示以檢視結果。
2. 選取您需要發佈的資產，然後按一下&#x200B;**發佈。**
3. 根據您的需求選取AEM、Dynamic Media或兩者，然後按一下&#x200B;**發佈。**
   ![搜尋影像](/help/assets/assets/search-mode.svg)
在搜尋結果頁面上發佈到Dynamic Media的選項取決於在存放庫中可使用該資產的資料夾上設定的Dynamic Media發佈模式。

   >[!NOTE]
   >
   >如果您選取資料夾並從搜尋結果頁面按一下「**發佈**」，則Experience Manager Assets會顯示將資產發佈到AEM的選項，而不管資料夾的Dynamic Media發佈模式設定為何，都會顯示將資產發佈到Dynamic Media的選項。

## 檢查發佈狀態 {#check-publish-status}

若要檢查資產或資料夾的已發佈狀態：

1. 按一下左窗格中可用的&#x200B;**[!UICONTROL Assets管理]**&#x200B;區段中的&#x200B;**[!UICONTROL Assets]**。
2. 使用檢視切換器切換至清單檢視。 您可以檢視資產屬性，例如AEM發佈、Dynamic Media發佈、標題、大小、維度等。\
   如果未發佈資產或資料夾，資料行&#x200B;**AEM Publish**&#x200B;和&#x200B;**Dynamic Media Publish**&#x200B;的狀態會顯示為&#x200B;**不適用。**
   ![檢查發佈狀態1](/help/assets/assets/check-publish-status1.png)
如果您無法在清單檢視中檢視AEM發佈和Dynamic Media發佈欄：
   1. 按一下![設定](/help/assets/assets/settings-icon.svg)，然後從&#x200B;**可設定的資料行**&#x200B;對話方塊中選取&#x200B;**AEM發佈**&#x200B;和&#x200B;**Dynamic Media發佈**&#x200B;資料行。
   2. 按一下&#x200B;**確認。** Experience Manager Assets將選取的欄新增至清單檢視。

      ![檢查發佈狀態2](/help/assets/assets/check-publish-status2.png)

您也可以選取資產並按一下[詳細資料]，以檢查資產發佈狀態。****&#x200B;詳細資料可在右窗格中的&#x200B;**發佈**&#x200B;區段中取得。 **發佈**&#x200B;區段會列出資產發佈至Dynamic Media和AEM的日期。 如果您需要檢視資產發佈的時間，可以導覽至清單檢視並檢視這些詳細資訊。

![檢查發佈狀態3](/help/assets/assets/check-publish-status3.png)

## 限制 {#limitations}

將資產發佈至AEM和Dynamic Media時，下列功能暫時不在範圍內：

* 從資產詳細資訊頁面將資產發佈到AEM和Dynamic Media。
* 使用「快速發佈」精靈將資產發佈的端點視覺化。
* 在快速發佈精靈中新增或刪除更多資產。
* 檢視已發佈資產的頁面。
* 可在資產層級複製或貼上Dynamic Media URL （如果資產已發佈至Dynamic Media）。
* 可在發佈至AEM時發佈參考（資產、標籤等）。
* 可在檔案夾層級覆寫Dynamic Media同步處理狀態。
* 可在檔案夾層級覆寫Dynamic Media發佈模式
* 尚不支援管理發布。
