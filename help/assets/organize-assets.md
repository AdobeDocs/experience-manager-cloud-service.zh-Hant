---
title: 組織您的數位資產
description: 使用Experience Manager組織您的數位資產、影像、檔案、資料夾等。
contentOwner: AG
feature: Asset Management, Best Practices
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 6%

---

# 組織您的數位資產 {#organize-digital-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/organize-assets.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

Microsoft® Office和PDF檔案的所有數位資產、中繼資料和內容都會經過擷取，並可供搜尋。 搜尋可讓您對資產進行複雜的篩選，並完全遵循適當的許可權。 有關中繼資料的詳情，請參閱數位資產管理的中繼資料。

[!DNL Experience Manager Assets]支援多種組織內容的方式。 您可以使用資料夾以階層方式組織資料夾，也可以以無序、臨機方式組織資料夾，例如標籤。 使用者可以在DAM Asset Editor中編輯顯示子資產、轉譯和中繼資料的標籤。

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a folder.
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

You can use folders or tags or both to organize assets. Adding tags to assets makes them easier to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## 組織資料夾中的資產 {#organize-using-folders}

組織資產的最基本方式是將資產儲存在資料夾中。 這類似於在本機檔案系統的資料夾中組織檔案。 如需有關如何建立及管理資料夾的詳細資訊，請參閱[管理資產](manage-digital-assets.md)。 您如何命名檔案和資料夾、如何排列子資料夾，以及如何處理這些資料夾中的檔案，可能會對這些資產的處理方式產生重大影響。 透過使用一致且適當的檔案和資料夾命名策略，搭配良好的中繼資料做法，您可以充份運用數位資產存放庫。

* 通常您的數位資產存放庫永遠在成長。 因此，在內容建立週期早期將中繼資料使用、資料夾結構和檔案命名正規化非常重要。
* 僅使用資料夾為您的數位資產強制實施一致的儲存結構。 此一致性可協助您改善流程並管理資產。 例如，將資產放在以下型別的資料夾中可以幫助您隔離資產：

   * **開發資料夾**：包含您目前正在處理的數位資產。
   * **使用者端資料夾**：包含以使用者端或專案名稱為基礎的數位資產。
   * **主要資料夾**：包含原始的來源數位資產。
   * **轉譯資料夾**：包含原始來源數位資產的轉譯與復本。
   * **檔案大小資料夾**：包含以小型、中型或大型檔案大小為基礎的數位資產。
   * **中繼資料夾**：包含已準備好在您的網站上即時發佈的數位資產。
   * **MIME型別資料夾**：包含影像、檔案和多媒體MIME型別專屬的數位資產。
   * **封存資料夾**：包含淘汰的數位資產。
   * **以日期為基礎的資料夾**：包含以建立日期或上次修改日期為基礎的數位資產。

* 建立不太可能變更的資料夾目錄，讓任何自訂或自動化功能繼續運作。 例如，指派的處理設定檔可繼續運作。
* 如果資產已發佈，則您可使用[!DNL Experience Manager]將資產移動到另一個資料夾，並從其新位置重新發佈。 仍可隨新重新發佈的資產使用原始已發佈的資產位置。 然而，原始發佈的資產為&#x200B;*遺失*&#x200B;至[!DNL Experience Manager]，無法取消發佈。 因此，最佳實務是先取消發佈資產，然後將其移至其他資料夾。

## 使用標籤組織資產 {#use-tags-to-organize-assets}

將標籤新增至資產可讓他們更輕鬆地在搜尋期間擷取、使用搜尋結果建立集合、提升某些資產的搜尋排名，以及套用Adobe Sensei的AI演演算法以進行資產探索。

[!DNL Adobe Experience Manager Assets]會使用自我學習演演算法來建立高度描述性的標籤，讓您只需按幾下滑鼠即可找到正確的資產。 智慧標籤使用Adobe Sensei、人工智慧和機器學習架構，這些架構經過訓練可辨識標準標籤和業務特定標籤，並套用至影像。 智慧標籤也可以識別內容、個別字詞或片語，並自動將描述性標籤套用至資產。

以下是將標籤新增至資產的步驟：

1. 登入[!DNL Experience Manager Assets]。
1. 按一下&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**，選取資產並按一下&#x200B;**[!UICONTROL 屬性]**&#x200B;以開啟資產屬性。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;標籤中，按一下&#x200B;**[!UICONTROL 標籤]**&#x200B;中繼資料中的資料夾圖示。 隨即開啟快顯視窗。
1. 從`cq-tags`中的現有標籤中搜尋或選取適當的標籤。 您可以指派多個標籤給資產。

   您可以根據&#x200B;**[!UICONTROL Name]** （字母順序）、**[!UICONTROL 已建立]**&#x200B;日期或&#x200B;**[!UICONTROL 已修改]**&#x200B;日期，以遞增或遞減順序來排序標籤結構。 在下圖中，標籤結構是根據&#x200B;**[!UICONTROL Name]**&#x200B;依字母順序排序。

   ![新增標記](assets/add-tags-to-asset.png)

1. 按一下&#x200B;**儲存**&#x200B;以更新資產中繼資料變更。

如需詳細資訊，請參閱下列文章：

* [編輯資產中繼資料](meta-edit.md)
* [Assets中的智慧標籤](smart-tags.md)
* [將標籤述詞新增至搜尋面板](/help/assets/search-facets.md/#adding-a-tags-predicate)

## 組織為集合 {#organize-as-collections}

透過[!DNL Experience Manager Assets]中的資產集合，您可以簡化使用者之間建立、編輯和共用資產的能力。 根據您使用收藏集的方式建立多種收藏集型別，包括包含資產、資料夾和收藏集的靜態參考清單的收藏集，以及根據搜尋條件提取資產的收藏集。 您可以使用不同位置的資產建立集合，並與具有不同存取層級、檢視和編輯許可權的多個使用者共用它們。

如需詳細資訊，請參閱[管理集合](manage-collections.md)


## 使用設定檔來組織您的資產 {#organize-to-use-profiles}

處理設定檔包含[!DNL Assets]個處理命令，這些命令適用於上傳至預先定義資料夾的資產。 設定檔可用來自動處理資料夾內容或最新上傳的資產。 您可以使用設定檔更好地組織您的資產。

將中繼資料使用、檔案命名和檔案夾結構標準化，可確保隨著數位資產集區的成長，您可以更精確且一致地將處理設定檔套用至檔案夾。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [使用資產微服務和處理設定檔](asset-microservices-configure-and-use.md)
>* [中繼資料設定檔](metadata-profiles.md)
>* [視訊設定檔](/help/assets/dynamic-media/video-profiles.md)
>* [Dynamic Media影像設定檔](/help/assets/dynamic-media/image-profiles.md)

