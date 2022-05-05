---
title: 組織您的數位資產
description: 使用Experience Manager組織您的數字資產、影像、檔案、資料夾等。
contentOwner: AG
feature: Asset Management, Search
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 333a0b0f6e0937a5ac6dc1a697c773f7bada45cc
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 1%

---

# 組織您的數位資產 {#organize-digital-assets}

Microsoft®辦公室和PDF文檔的所有數字資產、元資料和內容都被提取並可搜索。 搜索允許對資產進行複雜的篩選，並完全尊重適當的權限。 元資料在數字資產管理中的元資料中作了詳細介紹。

[!DNL Experience Manager Assets] 支援多種組織內容的方法。 可以使用資料夾以分層方式組織它們，或者可以按無序、即席的方式組織它們，例如標籤。 用戶可以在顯示子組、格式副本和元資料的DAM資產編輯器中編輯標籤。

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

組織資產的最基本方法是將資產保存在資料夾中。 它類似於組織本地檔案系統中資料夾中的檔案。 有關如何建立和管理資料夾的詳細資訊，請參見 [管理資產](manage-digital-assets.md)。 如何命名檔案和資料夾、如何排列子資料夾以及如何處理這些資料夾中的檔案都會對處理這些資產的方式產生重大影響。 通過使用一致且適當的檔案和資料夾命名策略以及良好的元資料做法，您可以充分利用數字資產儲存庫。

* 通常，您的數字資產儲存庫總在增長。 因此，在內容建立週期的早期就對元資料的使用、資料夾結構和檔案命名進行規範非常重要。
* 僅使用資料夾為您的數字資產強加一致的儲存結構。 此一致性有助於您的流程並更好地管理資產。 例如，放置在以下類型的資料夾中的資產可以幫助您隔離資產：

   * **開發資料夾**:包含您當前正在處理的數字資產。
   * **客戶端資料夾**:包含基於客戶端或項目名稱的數字資產。
   * **主資料夾**:包含原始的源數字資產。
   * **格式副本資料夾**:包含原始源數字資產的格式副本和副本。
   * **檔案大小資料夾**:包含基於小、中或大檔案大小的數字資產。
   * **暫存資料夾**:包含已準備好在您的網站上即時發佈的數字資產。
   * **MIME類型資料夾**:包含特定於MIME類型的數字資產，如影像、文檔和多媒體。
   * **存檔資料夾**:包含已停用的數字資產。
   * **基於日期的資料夾**:包含基於建立日期或上次修改日期的數字資產。

* 建立不太可能更改的資料夾目錄，以便任何自定義或自動化都繼續工作。 例如，已分配的處理配置檔案繼續工作。
* 如果已發佈資產，則使用 [!DNL Experience Manager] 將資源移動到另一個資料夾，並從其新位置重新發佈。 原始發佈的資產位置與新重新發佈的資產一起仍然可用。 但是，原始發佈的資產是 *失* 至 [!DNL Experience Manager] 不能不發表。 因此，作為最佳做法，首先取消發佈資產，然後將其移動到其他資料夾。

## 使用標籤組織資產 {#use-tags-to-organize-assets}

向資產添加標籤使它們在搜索過程中更容易檢索，使用搜索結果建立集合，提高某些資產的搜索排名，並將Adobe Sensei的AI算法應用於資產發現。

[!DNL Adobe Experience Manager Assets] 使用自學習算法建立高度描述性的標籤，使您只需按一下幾下即可找到合適的資產。 智慧標籤使用Adobe Sensei、人工智慧和機器學習框架，可訓練其識別和應用標準標籤和特定於業務的標籤到影像。 智慧標籤還可以識別內容、單個詞或短語，並自動將描述性標籤應用於資產。

以下是向資產添加標籤的步驟：

1. 登錄到 [!DNL Experience Manager Assets]。
1. 按一下 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**，選擇資產並按一下 **[!UICONTROL 屬性]** 開啟資產屬性。
1. 在 **[!UICONTROL 基本]** 的子菜單。 **[!UICONTROL 標籤]** 元資料。 將開啟一個彈出窗口。
1. 從中的現有標籤中搜索或選擇相應的標籤 `cq-tags`。 您可以為資產分配多個標籤。

   您可以根據 **[!UICONTROL 名稱]** （按字母順序排列）, **[!UICONTROL 已建立]** 日期或 **[!UICONTROL 已修改]** 日期。 在下圖中，標籤結構根據 **[!UICONTROL 名稱]**。

   ![添加標籤](assets/add-tags-to-asset.png)

1. 按一下 **保存** 更新資產元資料更改。

有關詳細資訊，請參閱以下文章：

* [編輯資產元資料](meta-edit.md)
* [資產中的智慧標籤](smart-tags.md)
* [將標籤謂詞添加到搜索面板](/help/assets/search-facets.md/#adding-a-tags-predicate)

## 組織為集合 {#organize-as-collections}

將資產收集 [!DNL Experience Manager Assets]，您可以簡化用戶之間建立、編輯和共用資產的功能。 根據使用方式建立多種類型的集合，包括包含資產、資料夾和集合的靜態引用清單的集合，以及根據搜索標準納入資產的集合。 您可以使用不同位置的資產建立集合，並與具有不同訪問、查看和編輯權限級別的多個用戶共用這些集合。

有關詳細資訊，請參見 [管理集合](manage-collections.md)


## 使用配置檔案來組織您的資產 {#organize-to-use-profiles}

處理配置檔案包含 [!DNL Assets] 正在處理適用於上載到預定義資料夾的資產的命令。 配置檔案用於自動處理資料夾或新上載的資產的內容。 您可以使用配置檔案來更好地組織資產。

標準化元資料使用、檔案命名和資料夾結構可確保隨著數字資產池的增長，您可以以更高的精確度和一致性將處理配置檔案應用於資料夾。

>[!MORELIKETHIS]
>
>* [使用資產微服務和處理配置檔案](asset-microservices-configure-and-use.md)
>* [中繼資料設定檔](metadata-profiles.md)
>* [視頻配置檔案](/help/assets/dynamic-media/video-profiles.md)
>* [Dynamic Media影像配置檔案](/help/assets/dynamic-media/image-profiles.md)


