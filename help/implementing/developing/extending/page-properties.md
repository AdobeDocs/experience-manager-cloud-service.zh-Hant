---
title: 自訂頁面屬性的檢視
description: 了解作者如何檢視和編輯頁面屬性。
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 92%

---

# 自訂頁面屬性的檢視{#customizing-views-of-page-properties}

每個頁面都有一組使用者可以檢視和編輯的[屬性](/help/sites-cloud/authoring/sites-console/page-properties.md)。有些是建立頁面 (建立檢視) 時的要求，其他的則可在稍後階段再檢視和編輯 (編輯檢視)。這些頁面屬性由適當頁面元件的對話框 (`cq:dialog`) 定義和提供。

每個頁面屬性的預設狀態為：

* 隱藏在建立檢視中 (例如，**建立頁面**&#x200B;精靈)

* 在編輯檢視 (例如，**檢視屬性**) 中提供

如果需要任何變更，則必須特別設定欄位。這會使用適當的節點屬性完成：

* 頁面屬性會在建立檢視 (例如，**建立頁面**&#x200B;精靈) 中提供：

   * 名稱：`cq:showOnCreate`
   * 類型：`Boolean`

* 頁面屬性會在編輯檢視 (例如&#x200B;**檢視**/**編輯****屬性**&#x200B;選項) 中提供：

   * 名稱：`cq:hideOnEdit`
   * 類型：`Boolean`

>[!TIP]
>
>如需自訂頁面屬性的指南，請參閱「[擴充頁面屬性教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=zh-Hant)」。

## 設定您的頁面屬性 {#configuring-your-page-properties}

設定頁面元件的對話框並套用適當的節點屬性，還可以設定可用的欄位。

例如，預設情況下，[**建立頁面**&#x200B;精靈](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page)會顯示在&#x200B;**更多標題和說明**&#x200B;下面分組的欄位。若要隱藏這些，您可以設定：

1. 在 `/apps` 下面建立您的頁面元件。
1. 針對頁面元件的 `basic` 區段建立覆寫 (使用由 [Sling 資源合併](/help/implementing/developing/introduction/sling-resource-merger.md)所提供的&#x200B;*對話框差異*)；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. 在 `basic` 上設定 `path` 屬性，以指向基本索引標籤的覆寫 (另請參閱下一個步驟)。例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在相對應的路徑建立 `basic` - `moretitles` 區段的覆寫；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 套用適當的節點屬性：

   * **名稱**：`cq:showOnCreate`
   * **類型**：`Boolean`
   * **值**：`false`

   「**更多標題和說明**」區段即不會再顯示在「**建立頁面**」精靈中。

>[!NOTE]
>
>設定要與即時副本一起使用的頁面屬性時，請參閱[擴充多網站管理員](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties)以取得詳細資訊。

## 頁面屬性的設定範例 {#sample-configuration-of-page-properties}

本範例會示範 [Sling 資源合併](/help/implementing/developing/introduction/sling-resource-merger.md)的對話框差異技術，包括 [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties) 的使用。還會說明 `cq:showOnCreate` 和 `cq:hideOnEdit` 兩者的使用。

您可以在[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)上找到此頁面的程式碼。
