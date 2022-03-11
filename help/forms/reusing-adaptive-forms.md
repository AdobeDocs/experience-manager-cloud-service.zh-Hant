---
title: 重複使用最適化表單的中繼資料屬性
seo-title: Reuse metadata properties of an Adaptive Form
description: 您可以重用現有的自適應表單來建立新的自適應Forms。
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 2%

---

# 重複使用最適化表單的中繼資料屬性 {#reusing-adaptive-forms}

如果要使用現有自適應表單的某些屬性來生成新的屬性，則只需使用複製貼上功能即可。 此外，還可以將新的自適應表單貼上到所需資料夾路徑上。 複製所有元資料屬性，並複製基於XFA和XSD的自適應Forms的XFA和XSD。

>[!NOTE]
>
>不複製狀態和審閱詳細資訊。 例如，如果已發佈「自適應表單」，然後複製了它，則貼上的「自適應表單」處於未發佈狀態。 同樣，如果正在複查複製的資產，則貼上的資產不在同一審閱下。

## 複製自適應表單 {#copy-an-adaptive-form}

使用下列方法之一複製自適應表單：

1. 按一下「複製」 ![aem6forms_copy](assets/aem6forms_copy.png) 表徵圖。

   >[!NOTE]
   >
   >快速操作是滑鼠懸停時在縮略圖上顯示的操作項。

1. 選擇「自適應表單」。 不同視圖的選擇過程不同。

   如果處於卡視圖中，請通過按一下選擇進入選擇模式 ![aem6forms_check circle](assets/aem6forms_check-circle.png) 表徵圖，然後按一下要複製的所有自適應Forms。

   如果處於清單視圖中，請按一下所有自適應Forms的複選框以選中它們。

   >[!NOTE]
   >
   >所有選定的資產必須是自適應Forms，因為只支援自適應Forms的複製貼上功能，並且所有選定的資產必須位於同一資料夾中。

   選擇資產後，按一下副本 ![aem6forms_copy](assets/aem6forms_copy.png) 表徵圖，以複製選定的「自適應」窗體。

## 貼上自適應表單 {#paste-an-adaptive-form}

按一下複製操作會自動退出選擇模式並進行貼上 ![貼上](assets/Smock_Paste_18_N.svg) 表徵圖。 現在轉到所需的資料夾路徑，然後按一下貼上 ![貼上](assets/Smock_Paste_18_N.svg) 表徵圖，以貼上複製的「自適應」窗體。

如果貼上到同一資料夾或具有相同節點名稱（與其一起儲存在CRX儲存庫中）的其他檔案存在於此目標資料夾中，則1會附加到尾碼(例如，myaf變為myaf1，如果myaf1位於同一位置，則myaf變為myaf2。 所有其它屬性與原始「自適應表單」保持相同。

按一下貼上後 ![貼上](assets/Smock_Paste_18_N.svg) 表徵圖，它將再次隱藏。 一次只能貼上一次。 要再次建立同一資產的副本，請再次複製。

## 更改新自適應表單的內容 {#change-contents-of-new-adaptive-form}

可以使用以下方法更改貼上的自適應Forms的內容，使其與複製的表單不同：

1. **更改元資料屬性：**

   您可以更改自適應表單的元資料屬性，例如標題和說明。 有關元資料屬性以及如何更改這些屬性的詳細資訊，請參見 [管理表單元資料](manage-form-metadata.md)

1. **為基於XFA/XSD的自適應Forms更改XFA/XSD:**

   您可以更改在自適應Forms中使用的XFA/XSD。 要瞭解如何更改這些自適應Forms，請參見 [管理表單元資料](manage-form-metadata.md)

1. **重新發佈:**

   貼上的資產與複製的資產不同。 您可以將其作為新資產發佈，以使其可供最終用戶使用。 要知道如何發佈資產， <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
