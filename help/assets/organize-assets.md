---
title: 組織您的數位資產
description: 使用Experience Manager組織您的數位資產、影像、檔案、資料夾等。
contentOwner: AG
feature: Asset Management, Search
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 3%

---

# 組織您的數位資產 {#organize-digital-assets}

擷取Microsoft® Office和PDF檔案的所有數位資產、中繼資料和內容，並供搜尋。 搜尋可針對資產進行精密的篩選，並完全尊重正確的權限。 數位資產管理的中繼資料將詳細說明中繼資料。

[!DNL Experience Manager Assets] 支援多種組織內容的方式。 您可以使用資料夾以階層方式組織資料夾，或以無序、隨選的方式組織資料夾，例如標籤。 使用者可以在DAM資產編輯器中編輯標籤，其中會顯示子資產、轉譯和中繼資料。

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a new folder.
1. In the menu, click **[!UICONTROL Create]**. Select **[!UICONTROL New Folder]**.
1. In the **[!UICONTROL Title]** field, provide a folder name. By default, DAM uses the title that you provided as the folder name. Once the folder is created, you can override the default and specify another folder name.
1. Click **[!UICONTROL Create]**. Your folder is displayed in the digital assets folder.

## Add CUG properties to folders {#add-cug-properties-to-folders}

You can limit who can access certain folders in Assets by making the folder part of a closed user group (CUG). To make a folder part of a CUG:

1. In Assets, right-click the folder you want to add closed user group properties for and select **Properties**.  
1. Click the **CUG** tab.
1. Select the **Enabled** check box to make the folder and its assets available only to a closed user group.  
1. Browse to the login page, if there is one, to add that information. Add admitted groups by clicking **Add item**. If necessary, add the realm. Click **OK** to save your changes.

## Use tags to organize assets {#use-tags-to-organize-assets}

You can use folders or tags or both to organize assets. Adding tags to assets makes them more easy to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## 在資料夾中組織資產 {#organize-using-folders}

組織資產的最基本方式是將資產儲存在資料夾中。 它類似於在本地檔案系統中組織資料夾中的檔案。 有關如何建立和管理資料夾的詳細資訊，請參見 [管理資產](manage-digital-assets.md). 如何命名檔案和資料夾、如何排列子資料夾，以及如何處理這些資料夾內的檔案，都會對這些資產的處理方式產生重大影響。 透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料實務，您可以充份運用數位資產存放庫。

* 數位資產存放庫通常會持續成長。 因此，在內容建立週期的早期將元資料的使用、資料夾結構和檔案命名正規化非常重要。
* 僅使用資料夾來為數位資產強加一致的儲存結構。 此一致性有助於您的流程，並更妥善地管理資產。 例如，放置在下列類型資料夾中的資產可協助您分隔資產：

   * **開發資料夾**:包含您目前使用的數位資產。
   * **用戶端資料夾**:包含根據用戶端或專案名稱的數位資產。
   * **主資料夾**:包含原始數位資產。
   * **轉譯資料夾**:包含原始數位資產的轉譯和復本。
   * **檔案大小資料夾**:包含以小型、中型或大型檔案大小為基礎的數位資產。
   * **中繼資料夾**:包含已準備好在您網站上上線發佈的數位資產。
   * **MIME類型資料夾**:包含MIME類型（如影像、檔案和多媒體）專屬的數位資產。
   * **封存資料夾**:包含已淘汰的數位資產。
   * **日期資料夾**:包含以建立日期或上次修改日期為基礎的數位資產。

* 建立不可能變更的資料夾目錄，以便任何自訂或自動化都能繼續運作。 例如，指派的處理設定檔可繼續運作。
* 如果資產已發佈，則您使用 [!DNL Experience Manager] 將資產移至其他資料夾，然後從新位置重新發佈。 原始已發佈資產位置仍可與新重新發佈的資產一起使用。 然而，原始發佈的資產是 *遺失* to [!DNL Experience Manager] 無法取消發佈。 因此，最佳作法是先取消發佈資產，然後將其移至其他資料夾。

## 使用標籤組織資產 {#use-tags-to-organize-assets}

將標籤新增至資產可讓您在搜尋期間更輕鬆擷取、使用搜尋結果建立集合、提升某些資產的搜尋排名，以及套用Adobe Sensei的AI演算法以進行資產探索。

[!DNL Adobe Experience Manager Assets] 使用自學算法來建立描述性很強的標籤，只需按幾下即可找到正確的資產。 智慧標籤使用Adobe Sensei、人工智慧和機器學習框架，可通過培訓來識別和應用標準標籤和特定於業務的標籤到影像。 智慧標籤也可以識別內容、個別字詞或片語，並自動將描述性標籤套用至資產。

新增標籤至資產的步驟如下：

1. 登入 [!DNL Experience Manager Assets].
1. 按一下 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**，選取資產並按一下 **[!UICONTROL 屬性]** 來開啟資產屬性。
1. 在 **[!UICONTROL 基本]** ，按一下 **[!UICONTROL 標籤]** 中繼資料。 隨即開啟彈出窗口。
1. 在中，從現有標籤搜尋或選取適當的標籤 `cq-tags`. 您可以指派多個標籤給資產。

   您可以根據 **[!UICONTROL 名稱]** （字母順序）, **[!UICONTROL 已建立]** 日期，或 **[!UICONTROL 已修改]** 日期。 在下圖中，標籤結構會根據 **[!UICONTROL 名稱]**.

   ![新增標籤](assets/add-tags-to-asset.png)

1. 按一下 **儲存** 更新資產中繼資料變更。

如需詳細資訊，請參閱下列文章：

* [編輯資產中繼資料](meta-edit.md)
* [資產中的智慧標籤](smart-tags.md)
* [新增標籤述詞至搜尋面板](/help/assets/search-facets.md/#adding-a-tags-predicate)

## 組織為集合 {#organize-as-collections}

將資產集合放在 [!DNL Experience Manager Assets]，您可以簡化在使用者之間建立、編輯和共用資產的能力。 根據您使用方式建立數種集合類型，包括包含靜態參考清單的資產、資料夾和集合的集合，以及根據搜尋准則提取資產的集合。 您可以使用不同位置的資產建立集合，並與具有不同存取、檢視及編輯權限層級的多個使用者共用集合。

如需詳細資訊，請參閱 [管理集合](manage-collections.md)


## 使用設定檔來組織資產 {#organize-to-use-profiles}

處理設定檔包含 [!DNL Assets] 處理命令，此命令會套用至上傳至預先定義之資料夾的資產。 設定檔可用來自動處理資料夾或新上傳資產的內容。 您可以使用設定檔來更妥善地組織資產。

標準化中繼資料的使用、檔案命名和資料夾結構，可確保隨著數位資產池的成長，您可以更精確且一致地將處理設定檔套用至資料夾。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [Assets支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連線資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [使用資產微服務和處理設定檔](asset-microservices-configure-and-use.md)
>* [中繼資料設定檔](metadata-profiles.md)
>* [視訊設定檔](/help/assets/dynamic-media/video-profiles.md)
>* [Dynamic Media影像設定檔](/help/assets/dynamic-media/image-profiles.md)


