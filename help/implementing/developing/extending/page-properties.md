---
title: 自訂頁面屬性檢視
description: 瞭解如何由作者檢視及編輯頁面屬性。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---


# 自訂頁面屬性檢視{#customizing-views-of-page-properties}

每個頁面都有一組 [屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 使用者可檢視和編輯的專案。 建立頁面（建立檢視）時需要某些專案，稍候可以檢視和編輯其他專案（編輯檢視）。 這些頁面屬性會透過對話方塊(`cq:dialog`)。

每個頁面屬性的預設狀態為：

* 在建立檢視中隱藏(例如， **建立頁面** 精靈)

* 可在編輯檢視中使用(例如， **檢視屬性**)

如果需要進行任何變更，則必須明確設定欄位。 這是使用適當的節點屬性來完成：

* 建立檢視中可用的頁面屬性(例如， **建立頁面** 精靈)：

   * 名稱: `cq:showOnCreate`
   * 類型: `Boolean`

* 編輯檢視中可用的頁面屬性，例如 **檢視**/**編輯**  **屬性** 選項：

   * 名稱: `cq:hideOnEdit`
   * 類型: `Boolean`

>[!TIP]
>
>請參閱 [擴充頁面屬性教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) 以取得自訂頁面屬性的指南。

## 設定頁面屬性 {#configuring-your-page-properties}

您也可以設定頁面元件的對話方塊並套用適當的節點屬性，以設定可用的欄位。

例如，預設情況下 [**建立頁面** 精靈](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) 顯示分組在下列位置的欄位： **更多標題和說明**. 若要隱藏這些設定，請執行下列動作：

1. 在下建立您的頁面元件 `/apps`.
1. 建立覆寫(使用 *對話方塊差異* 提供者： [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md))用於 `basic` 區段；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. 設定 `path` 屬性： `basic` 指向基本標籤的覆寫（也請參閱下一個步驟）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 建立覆寫 `basic` - `moretitles` 區段中的路徑，例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 套用適當的節點屬性：

   * **名稱**: `cq:showOnCreate`
   * **型別**： `Boolean`
   * **值**: `false`

   此 **更多標題和說明** 區段不會再顯示於 **建立頁面** 精靈。

>[!NOTE]
>
>設定要與即時副本一起使用的頁面屬性時，請參閱檔案 [擴充多站點管理員](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) 以取得更多詳細資料。

## 頁面屬性的設定範例 {#sample-configuration-of-page-properties}

這個範例示範對話方塊的diff技巧。 [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md) 包含使用 [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). 它也會說明兩者搭配使用 `cq:showOnCreate` 和 `cq:hideOnEdit`.

您可以在此頁面找到程式碼： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
