---
title: 內容片段 - 刪除考量事項
description: 在中定義內容片段刪除策略之前，請查看這些重要注意事項AEM。 內容片段是提供無頭內容的強大工具，刪除它們的含義必須仔細考慮。
source-git-commit: a06024b4d4b6e5e750ed4c1e27f55283513b78a2
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 10%

---

# 內容片段 - 刪除考量事項 {#content-fragments-delete-considerations}

在中定義內容片段刪除策略之前，請查看這些重要注意事項AEM。 內容片段是提供無頭內容的強大工具，刪除它們的含義必須仔細考慮。

## 權限 — 刪除或不刪除 {#permissions-delete-or-not-delete}

刪除內容的能力非常強大，但可能是敏感的，許多行業需要限制和控制這些權限的分配方式。

關於刪除權限，必須在兩個級別考慮內容片段：

1. **內容片段作為單個實體。**

   * **用例**:需要編輯/更新內容片段的用戶 —  **並刪除整個片段**。
   * **權限**:可以通過「用戶和/或組管理」來分配「刪除」權限。 <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **構成內容片段的多個子實體；例如，變體，子節點。**

   內容片段編輯器的基本操作要求可以刪除此類臨時子元素。 例如，在操縱變體時；編輯元資料或管理關聯內容時。

   * **用例**:需要編輯/更新內容片段的用戶 —  **不允許刪除整個片段**。
   * **權限**:請參閱 [僅編輯器功能所需的權限](#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>當用戶沒有任何「刪除」權限時，內容片段編輯器將在 *只讀* 的子菜單。 <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>另請參閱中的「如何審核用戶管理操AEM作」。 <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## 僅編輯器功能所需的權限 {#permissions-required-for-editor-functionality-only}

對於需要編輯/更新內容片段而不允許他們刪除整個片段的使用者 ****，必須指派特定權限，因為內容片段編輯器的基本操作要求可以刪除暫時的子元素。

例如，在操縱變體時；編輯元資料或管理關聯內容時。

>[!NOTE]
>
>編輯/更新內容片段所需的刪除權限包含在通過「用戶」和/或「組管理」分配的「刪除」權限中。 <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

編輯/更新片段所需的權限需要應用於包含內容片段的節點或相應的父節點（位於以下任何級別） `/content/dam`)。 當分配給這樣的父節點時，權限將應用於該分支中的所有節點。

例如，將保存所有內容片段的資料夾，如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>設定權限 `/content/dam` 也是可能的，因為所有內容片段都儲存在這裡。
>
>但是，此操作將相同的刪除權限應用於 *全部* 其他資產類型。

允許特定用戶和/或組編輯/更新內容片段的權限先決條件是：

>[!NOTE]
>
>此清單顯示所需的所有權限，而不僅顯示刪除權限。

* 對於「內容片段」節點或資料夾：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 對於 `jcr:content`所有內容片段的節點：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes`

* 適用於以下所有節點 `jcr:content` 所有內容片段：

   * `jcr:addChildNodes`。 `jcr:modifyProperties` 和 `jcr:removeChildNodes`。 `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
