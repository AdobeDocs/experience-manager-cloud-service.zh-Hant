---
title: 內容片段——刪除考量事項
description: 內容片段——刪除考量事項
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# 內容片段——刪除考量事項{#content-fragments-delete-considerations}

## 權限——刪除或不刪除 {#permissions-delete-or-not-delete}

刪除內容的能力強大，但可能很敏感，許多產業需要限制和控制這些權限的分發方式。

有關刪除權限，內容片段必須考慮在兩個層級：

1. **內容片段為單一實體。**

   * **使用案例**:需要編輯／更新內容片段——並刪除整 **個片段的使用者**。
   * **權限**:「刪除」權限可透過「使用者」和／或「群組管理」來指派。 <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **構成內容片段的多個子實體；例如，變化，子節點。**

   內容片段編輯器的基本操作要求可以刪除這種瞬時子元素。 例如，在操縱變化時；編輯中繼資料或管理相關內容時也一樣。

   * **使用案例**:需要編輯／更新內容片段的使用者， **而不允許刪除整個片段**。
   * **權限**:請參閱僅限編輯器功能所需的權限。 <!-- See [Permissions Required for Editor Functionality Only](/help/assets/content-fragments-delete.md#permissions-required-for-editor-functionality-only). -->

>[!NOTE]
>
>當使用者沒有任何刪除權限時，內容片段編輯器會以唯讀 *模式運作* 。 <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>另請參閱How to Audit User Management Operations in AEM。 <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## 僅編輯器功能所需的權限 {#permissions-required-for-editor-functionality-only}

對於需要編輯／更新內容片段而不允許他們刪除整個片段的使用者 ****，必須指派特定權限，因為內容片段編輯器的基本操作要求可以刪除暫時的子元素。

例如，在操縱變化時；編輯中繼資料或管理相關內容時也一樣。

>[!NOTE]
>
>編輯／更新內容片段所需的刪除權限，會包含在透過「使用者」和／或「群組管理」指派的「刪除」權限中。 <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

編輯／更新片段所需的權限必須套用至包含內容片段的節點，或適當的父節點(在任何層級下 `/content/dam`)。 當指派給此類父節點時，權限將會套用至該分支中的所有節點。

例如，包含所有內容片段的資料夾，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>也可設定權 `/content/dam` 限，因為所有內容片段都儲存在這裡。
>
>不過，此動作也會將相同的刪除權 *限套用* 至所有其他資產類型。

允許特定使用者和／或群組編輯／更新內容片段的權限先決條件為：

>[!NOTE]
>
>此清單顯示所有所需權限，而不只是刪除權限。

* 對於「內容片段」節點或資料夾：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 對於所 `jcr:content`有內容片段的節點：

   * `jcr:addChildNodes`, `jcr:modifyProperties` &amp; `jcr:removeChildNodes`

* 對於所有內容片段 `jcr:content` 的下方所有節點：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 而 `jcr:removeChildNodes`且 `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
