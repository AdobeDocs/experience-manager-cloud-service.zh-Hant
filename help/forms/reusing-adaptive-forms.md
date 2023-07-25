---
title: 重複使用最適化表單的中繼資料屬性
seo-title: Reuse metadata properties of an Adaptive Form
description: 您可以重複使用現有的最適化表單來建立新的最適化Forms。
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: ca0c9f102488c38dbe8c969b54be7404748cbc00
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---

# 重複使用最適化表單的中繼資料屬性 {#reusing-adaptive-forms}

<span class="preview"> Adobe建議使用現代化且可擴充的資料擷取 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 的 [建立新的Adaptive Forms](/help/forms/creating-adaptive-form-core-components.md) 或 [將最適化Forms新增至AEM Sites頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). 這些元件代表最適化Forms建立工作取得重大進展，可確保提供令人驚歎的使用者體驗。 本文說明使用基礎元件製作最適化Forms的舊方法。 </span>


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/reusing-adaptive-forms.html) |
| AEM as a Cloud Service  | 本文 |

如果您想要使用現有最適化表單的某些屬性來產生新表單，您只需使用複製 — 貼上功能即可。 此外，您還可以在所需的資料夾路徑貼上新的調適型表單。 會複製所有中繼資料屬性，並複製XFA和XSD型最適化Forms的XFA和XSD。

>[!NOTE]
>
>不會複製狀態和稽核詳細資料。 例如，若您的調適型表單已發佈，而您複製表單時，貼上的調適型表單會處於未發佈狀態。 同樣地，如果正在稽核複製的資產，貼上的資產不會處於相同的稽核中。

## 複製最適化表單 {#copy-an-adaptive-form}

使用下列其中一種方法複製調適型表單：

1. 按一下複製 ![aem6forms_copy](assets/aem6forms_copy.png) 圖示加以檢視。

   >[!NOTE]
   >
   >快速動作是在滑鼠懸停時顯示在縮圖上的動作專案。

1. 選取最適化表單。 不同檢視的選取程式不同。

   如果您在卡片檢視中，請按一下選取專案以移至選取模式 ![aem6forms_check-circle](assets/aem6forms_check-circle.png) 圖示並按一下您要複製的所有最適化Forms。

   如果您在清單檢視中，請按一下所有最適化Forms的核取方塊以選取它們。

   >[!NOTE]
   >
   >所有選取的資產都必須是最適化Forms，因為只有Adaptive Forms支援複製貼上功能，而且所有選取的資產都必須存在於相同的資料夾中。

   選取資產後，按一下副本 ![aem6forms_copy](assets/aem6forms_copy.png) 圖示出現在工具列上，用來複製選取的最適化表單。

## 貼上最適化表單 {#paste-an-adaptive-form}

按一下複製動作會自動退出選取模式並進行貼上 ![貼上](assets/Smock_Paste_18_N.svg) 圖示可見。 現在前往所需的資料夾路徑，然後按一下貼上 ![貼上](assets/Smock_Paste_18_N.svg) 圖示貼上複製的最適化表單。

如果您貼上同一個資料夾，或是另一個具有相同節點名稱的檔案（儲存於CRX存放庫中）存在於這個目標資料夾中，則會將1附加至尾碼(例如，myaf會變成myaf1，而如果myaf1存在於相同位置，myaf會變成myaf2。 所有其他屬性仍維持與原始最適化表單相同。

按一下貼上之後 ![貼上](assets/Smock_Paste_18_N.svg) 圖示中，則會再次隱藏。 您一次只能貼上一次。 若要再次建立相同資產的復本，請再次複製。

## 變更新最適化表單的內容 {#change-contents-of-new-adaptive-form}

已貼上的最適化Forms內容可以使用以下方法變更，以使其與複製的表單不同：

1. **變更中繼資料屬性：**

   您可以變更最適化表單的中繼資料屬性，例如標題和說明。 如需有關中繼資料屬性及其變更方式的詳細資訊，請參閱 [管理表單中繼資料](manage-form-metadata.md)

1. **變更XFA/XSD型最適化Forms的XFA/XSD：**

   您可以變更最適化Forms中使用的XFA/XSD。 若要瞭解如何變更這些最適化Forms，請參閱 [管理表單中繼資料](manage-form-metadata.md)

1. **重新發佈:**

   貼上的資產與複製的資產不同。 您可以將它發佈為新資產，以供一般使用者使用。 若要瞭解如何發佈資產， <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
