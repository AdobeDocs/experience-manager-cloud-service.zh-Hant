---
title: 管理收藏集
description: 集合是Experience Manager Assets檢視中的一組資產。 使用收藏集在使用者之間共用資產。
exl-id: 33c889f5-c989-4772-9591-db62f50e5c80
source-git-commit: d198b3f0c7d8469a376ba7a3e95e57c84f835dbb
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 89%

---

# 管理收藏集 {#manage-collections}

>[!CONTEXTUALHELP]
>id="assets_collections"
>title="管理收藏集"
>abstract="收藏集是 Assets 檢視中的一組資產、檔案夾或其他集合。使用收藏集在使用者之間共用資產。和檔案夾不同，收藏集可包含來自不同位置的資產。您可以和使用者共用多個收藏集。每個收藏集都包含資產的參考資料。資產的參考完整性會跨越收藏集來維護。"

收藏集是Adobe Experience Manager資產檢視中的一組資產、資料夾或其他收藏集。 使用收藏集在使用者之間共用資產。

和檔案夾不同，收藏集可包含來自不同位置的資產。

<!--
You can share collections with various users that are assigned different levels of privileges, including viewing, editing, and so on.
-->

您可以和使用者共用多個收藏集。每個收藏集都包含資產的參考資料。資產的參考完整性會跨越收藏集來維護。

![收藏集](assets/collections.png)

您可以執行下列任務以管理和使用收藏集：

* [建立收藏集](#create-collection)

* [將資產新增至收藏集](#add-assets-to-collection)

* [從收藏集移除資產](#remove-assets-from-collection)

* [建立智慧型集合](#create-smart-collection)

* [編輯智慧型集合](#edit-smart-collection)

* [檢視和編輯收藏集中繼資料](#view-edit-collection-metadata)

* [共用收藏集的連結](#share-collection-links)

* [下載收藏集](#download-collection)

* [刪除收藏集](#delete-collection)

## 建立收藏集 {#create-collection}

若要建立收藏集：

1. 請按一下左側邊欄中的&#x200B;**[!UICONTROL 收藏集]**，然後按一下&#x200B;**[!UICONTROL 建立收藏集]**。

1. 指定收藏集的標題和說明 (選用)。

1. 如果需要建立私有集合或公共集合，請選擇。 公共集合可用於查看和編輯所有用戶。 但是，具有管理員權限的建立者和用戶可以使用專用集合。

1. 按一下以&#x200B;**[!UICONTROL 建立]**&#x200B;下一個色標。

![建立收藏集](assets/create-collection.png)

<!--
   
   for viewing and editing only to users with the appropriate [permissions](#manage-collection-access).

-->

## 將資產新增至收藏集 {#add-assets-to-collection}

若要將資產新增至收藏集：

1. 按一下左側邊欄中的&#x200B;**[!UICONTROL 資產]**，然後選取您需要新增到收藏集的資產。

1. 按一下&#x200B;**[!UICONTROL 新增至收藏集]**。

1. 在[!UICONTROL 收藏集]對話框中，選取收藏集以新增所選取的資產。

1. 按一下&#x200B;**[!UICONTROL 新增]**，以將資產新增到所選取的收藏集。

## 從收藏集移除資產 {#remove-assets-from-collection}

若要從收藏集移除資產：

1. 請按一下左側邊欄中的&#x200B;**[!UICONTROL 收藏集]**，以檢視收藏集清單。

1. 按一下收藏集，然後選取您需要從收藏集移除的項目。

1. 按一下&#x200B;**[!UICONTROL 移除]**。

## 管理智慧型集合 {#manage-smart-collection}

將搜尋結果另存為 Smart Collection 以動態更新收藏集內容。 如果新增到「資產」檢視存放庫的資產符合建立Smart Collection時定義的搜尋條件，則開啟Smart Collection時，Smart Collection的內容會自動更新。

### 建立智慧型集合 {#create-smart-collection}

若要建立 Smart Collection：

1. 按一下 **[!UICONTROL 篩選]** 和[定義搜索標準](search-assets-view.md#refine-search-results)。

1. 按一下 **[!UICONTROL 另存為]** ，然後選擇 **[!UICONTROL Smart Collection]**。

   ![建立智慧型集合](assets/create-smart-collection.png)

1. 在 [!UICONTROL 建立 Smart Collection] 的子選單。

1. 選擇 **[!UICONTROL 公共集合]** 的子選單。 選擇 **[!UICONTROL 私有集合]** 如果需要一組有限的用戶才能訪問集合。

1. 按一下 **[!UICONTROL 建立]**&#x200B;建立 Smart Collection。

### 編輯智慧型集合 {#edit-smart-collection}

若要編輯智慧型集合：

1. 按一下左邊欄中的&#x200B;**[!UICONTROL 集合]**，然後按兩下您要編輯集合的名稱。

1. 按一下&#x200B;**[!UICONTROL 編輯智慧型集合]**。

1. 在「[!UICONTROL 編輯智慧型集合篩選器]」對話方塊中，更新智慧型集合的[搜尋條件](search-assets-view.md#refine-search-results)。

1. 按一下「**[!UICONTROL 儲存]**」。

<!--

## Manage access to a Private collection {#manage-collection-access}

The permission management for collections function in the same manner as folders in [!DNL Assets view]. Administrators can manage the access levels for collections available in the repository. As an administrator, you can create user groups and assign permissions to those groups to manage access levels. You can also delegate the permission management privileges to user groups at the collection-level.

For more information, see [Manage permissions for folders and collections](manage-permissions.md).

-->

<!--

## Search a collection {#search-collections}

Click **[!UICONTROL Collections]** in the left rail and use the Search box to specify a text as the criteria to search for a collection. [!DNL Assets view] uses the specified text to search collection names, metadata including tags defined for a collection and returns appropriate results.

>[!NOTE]
>
>Assets view performs search in collections available at the root level. It does not perform search in assets and folders available in collections.

-->

## 檢視和編輯收藏集中繼資料 {#view-edit-collection-metadata}

收藏集中繼資料包含有關收藏集的資料，例如標題和說明。

若要檢視和編輯收藏集中繼資料：

1. 請按一下左側邊欄中的&#x200B;**[!UICONTROL 收藏集]**，選一個收藏集，然後按一下&#x200B;**[!UICONTROL 詳細資訊]**。
1. 使用&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤來檢視收藏集中繼資料。
1. 修改中繼資料欄位 (如有必要)。您可以修改[!UICONTROL 標題]和[!UICONTROL 說明]欄位。

![收藏集中繼資料](assets/collection-metadata.png)

## 共用收藏集的連結 {#share-collection-links}

[!DNL Assets view] 可讓您產生連結，並和無法存取 [!DNL Assets view] 應用程式的外部利益關係人共用收藏集和收藏集中的資產。您可以定義連結的到期日，然後使用您喜歡的通訊方式 (如電子郵件或簡訊服務) 與他人共用。連結的收件者可預覽和下載資產。

![共用資產連結](assets/share-link-collections.png)

如需有關如何與外部利益關係人共用收藏集連結的詳細資訊，請參閱 [共用資產連結](/help/assets/share-links-for-assets-view.md).

## 下載收藏集 {#download-collection}

若要下載收藏集：

1. 按一下左側邊欄中的&#x200B;**[!UICONTROL 收藏集]**。

1. 選取您需要下載的收藏集，然後按一下&#x200B;**[!UICONTROL 下載]**。

1. 在[!UICONTROL 下載資產]對話框中，按一下&#x200B;**[!UICONTROL 確定]**。

收藏集會下載成您本機電腦的 .ZIP 檔案。

## 刪除收藏集 {#delete-collection}

若要刪除收藏集：

1. 按一下左側邊欄中的&#x200B;**[!UICONTROL 收藏集]**。

1. 選取您需要刪除的收藏集。

1. 按一下&#x200B;**[!UICONTROL 刪除]**。

## 後續步驟 {#next-steps}

* 使用資產檢視使用者介面所提供的[!UICONTROL 意見回饋]選項提供產品意見回饋

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)

* 聯絡[客戶服務](https://experienceleague.adobe.com/?support-solution=General#support)
