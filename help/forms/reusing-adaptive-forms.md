---
title: 重複使用最適化表單的中繼資料屬性
seo-title: Reuse metadata properties of an Adaptive Form
description: 您可以重複使用現有的適用性表單來建立新的適用性Forms。
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 重複使用最適化表單的中繼資料屬性 {#reusing-adaptive-forms}

如果您想要使用現有適用性表單的某些屬性來產生新屬性，您只需使用複製貼上功能即可。 此外，您可以將新的適用性表單貼到所需的資料夾路徑。 會複製所有中繼資料屬性，並複製XFA和XSD型適用性Forms的XFA和XSD。

>[!NOTE]
>
>不會複製狀態和審閱詳細資訊。 例如，如果您的適用性表單已發佈，而您複製了該表單，則貼上的適用性表單會處於未發佈狀態。 同樣地，如果複製的資產正在審閱中，貼上的資產不在同一次審閱中。

## 複製最適化表單 {#copy-an-adaptive-form}

使用下列其中一種方法複製最適化表單：

1. 按一下複製 ![aem6forms_copy](assets/aem6forms_copy.png) 表徵圖。

   >[!NOTE]
   >
   >快速動作是滑鼠暫留時在縮圖上顯示的動作項目。

1. 選取「最適化表單」。 不同視圖的選擇過程不同。

   如果您處於卡片檢視中，請按一下選取項目，以前往選取模式 ![aem6forms_check-circle](assets/aem6forms_check-circle.png) 圖示，然後按一下您要複製的所有適用性Forms。

   如果您處於清單檢視中，請按一下所有適用性Forms的核取方塊以選取。

   >[!NOTE]
   >
   >所有選取的資產都必須為適用性Forms，因為僅適用性Forms支援複製貼上功能，且所有選取的資產都必須顯示在相同的資料夾中。

   選取資產後，按一下復本 ![aem6forms_copy](assets/aem6forms_copy.png) 圖示來複製所選的最適化表單。

## 貼上最適化表單 {#paste-an-adaptive-form}

按一下複製動作會自動退出選取模式並進行貼上 ![貼上](assets/Smock_Paste_18_N.svg) 表徵圖。 現在，前往所需的資料夾路徑，然後按一下貼上 ![貼上](assets/Smock_Paste_18_N.svg) 圖示來貼上複製的最適化表單。

如果您貼入相同資料夾，或此目標資料夾中存在另一個節點名稱相同（與CRX儲存庫儲存）的檔案，則1會附加到尾碼(例如，myaf會變成myaf1，而如果myaf1存在於相同位置，myaf會變成myaf2。 所有其他屬性仍與原始適用性表單相同。

按一下貼上後 ![貼上](assets/Smock_Paste_18_N.svg) 表徵圖，它將再次被隱藏。 一次您只能貼上一次。 若要再次建立相同資產的復本，請再次複製。

## 變更新適用性表單的內容 {#change-contents-of-new-adaptive-form}

您可以使用下列方法來變更貼上的適用性Forms的內容，使其與複製的表單不同：

1. **更改元資料屬性：**

   您可以變更適用性表單的中繼資料屬性，例如標題和說明。 如需中繼資料屬性的詳細資訊，以及如何變更，請參閱 [管理表單中繼資料](manage-form-metadata.md)

1. **針對XFA/XSD型適用性Forms變更XFA/XSD:**

   您可以變更適用性Forms中使用的XFA/XSD。 若要了解如何變更這些適用性Forms，請參閱 [管理表單中繼資料](manage-form-metadata.md)

1. **重新發佈:**

   貼上的資產與複製的資產不同。 您可以將其發佈為新資產，以供使用者使用。 若要了解如何發佈資產， <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
