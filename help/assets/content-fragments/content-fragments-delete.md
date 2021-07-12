---
title: 內容片段 - 刪除考量事項
description: 在AEM中定義內容片段刪除原則前，請先檢閱這些重要考量事項。 內容片段是傳遞無頭內容的強大工具，刪除這些片段的含意必須謹慎考量。
feature: 內容片段
role: User
exl-id: 69c08f2f-4d51-4aea-957e-ee81c4604377
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 10%

---

# 內容片段 - 刪除考量事項 {#content-fragments-delete-considerations}

在AEM中定義內容片段刪除原則前，請先檢閱這些重要考量事項。 內容片段是傳遞無頭內容的強大工具，刪除這些片段的含意必須謹慎考量。

## 權限 — 刪除或不刪除 {#permissions-delete-or-not-delete}

刪除內容的能力強大，但可能很敏感，許多行業需要限制和控制這些權限的分配方式。

關於刪除權限，內容片段必須在兩個層級考量：

1. **內容片段為單一實體。**

   * **使用案例**:需要編輯/更新內容片段 — 並刪 **除整個片段的使用者**。
   * **權限**:可透過「使用者」和/或「群組管理」來指派「刪除」權限。  <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **組成內容片段的多個子實體；例如，變異、子節點。**

   內容片段編輯器的基本操作要求可以刪除這種暫時的子元素。 例如，在操縱變異時；編輯中繼資料或管理相關內容時，也會一併啟用。

   * **使用案例**:需要編輯/更新內容片段的使用者， **不允許刪除整個片段**。
   * **權限**:請參 [閱僅編輯器功能所需的權限](#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>當使用者沒有任何刪除權限時，內容片段編輯器會以&#x200B;*唯讀*&#x200B;模式運作。<!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>另請參閱如何在AEM中審核用戶管理操作。 <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## 僅編輯器功能所需的權限 {#permissions-required-for-editor-functionality-only}

對於需要編輯/更新內容片段而不允許他們刪除整個片段的使用者 ****，必須指派特定權限，因為內容片段編輯器的基本操作要求可以刪除暫時的子元素。

例如，在操縱變異時；編輯中繼資料或管理相關內容時，也會一併啟用。

>[!NOTE]
>
>編輯/更新內容片段所需的刪除權限，會包含在透過「使用者」和/或「群組管理」指派的「刪除」權限中。<!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

編輯/更新片段所需的權限需要套用至包含內容片段的節點，或適當的父節點（位於`/content/dam`下的任何層級）。 當指派給此父節點時，權限會套用至該分支內的所有節點。

例如，會保留所有內容片段的資料夾，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>也可以設定`/content/dam`的權限，因為所有內容片段都儲存在此處。
>
>不過，此動作也會將相同的刪除權限套用至&#x200B;*all*&#x200B;其他資產類型。

允許特定使用者和/或群組編輯/更新內容片段的權限先決條件為：

>[!NOTE]
>
>此清單顯示所需的所有權限，而不只是刪除權限。

* 對於內容片段節點或資料夾：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 對於所有內容片段的`jcr:content`節點：

   * `jcr:addChildNodes`,  `jcr:modifyProperties` 和  `jcr:removeChildNodes`

* 對於所有內容片段`jcr:content`下的所有節點：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes`,  `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
