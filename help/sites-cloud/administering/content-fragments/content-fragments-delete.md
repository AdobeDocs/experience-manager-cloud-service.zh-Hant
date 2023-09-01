---
title: 內容片段 - 刪除考量事項
description: 在AEM中定義內容片段刪除原則之前，請檢閱這些重要考量。 內容片段是傳送Headless內容的強大工具，必須仔細考慮刪除這些片段的影響。
feature: Content Fragments
role: User
hide: true
index: false
hidefromtoc: true
exl-id: f6698dd8-3e2a-44ac-b00f-df578aa85ffe
source-git-commit: 5ce5746026c5683e79cdc1c9dc96804756321cdb
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 10%

---

# 內容片段 - 刪除考量事項 {#content-fragments-delete-considerations}

<!--
hide: yes
index: no
hidefromtoc: yes
-->

在AEM中定義內容片段刪除原則之前，請檢閱這些重要考量。 內容片段是傳送Headless內容的強大工具，必須仔細考慮刪除這些片段的影響。

## 許可權 — 刪除或不刪除 {#permissions-delete-or-not-delete}

刪除內容的功能非常強大，但可能比較敏感，許多行業都需要限制和控制這些許可權的分配方式。

關於刪除許可權，內容片段必須考量為兩個層級：

1. **作為單一實體的內容片段。**

   * **使用案例**：需要編輯/更新內容片段的使用者 —  **並刪除整個片段**.
   * **許可權**：您可透過「使用者」及/或「群組管理」指派「刪除」許可權。 <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **構成內容片段的多個子實體；例如，變化、子節點。**

   內容片段編輯器的基本操作需要可以刪除此類暫時性子元素。 例如，操控變數時；編輯中繼資料或管理關聯內容時，也可以。

   * **使用案例**：需要編輯/更新內容片段的使用者 —  **不允許刪除整個片段**.
   * **許可權**：請參閱 [僅編輯器功能所需的許可權](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>當使用者沒有任何刪除許可權時，內容片段編輯器會運作 *唯讀* 模式。 <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>另請參閱如何在AEM中稽核使用者管理作業。 <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## 僅編輯器功能所需的許可權 {#permissions-required-for-editor-functionality-only}

對於需要編輯/更新內容片段而不允許他們刪除整個片段的使用者 ****，必須指派特定權限，因為內容片段編輯器的基本操作要求可以刪除暫時的子元素。

例如，操控變數時；編輯中繼資料或管理關聯內容時，也可以。

>[!NOTE]
>
>編輯/更新內容片段所需的刪除許可權包含在透過使用者和/或群組管理指派的刪除許可權中。 <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

編輯/更新片段所需的許可權需要套用至包含內容片段的節點或適當的父節點（在下的任何層級）。 `/content/dam`)。 當指派給此類父節點時，許可權會套用至該分支內的所有節點。

例如，將儲存所有內容片段的資料夾，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>設定許可權： `/content/dam` 也是可能的，因為所有內容片段都儲存在這裡。
>
>不過，此動作會將相同的刪除許可權套用至 *全部* 其他資產型別。

允許特定使用者和/或群組編輯/更新內容片段的先決條件許可權為：

>[!NOTE]
>
>此清單顯示所需的所有許可權，而不只是刪除許可權。

* 對於內容片段節點或資料夾：

   * `jcr:addChildNodes`、`jcr:modifyProperties`

* 對於 `jcr:content`所有內容片段的節點：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes`

* 適用於以下所有節點 `jcr:content` 所有內容片段的：

   * `jcr:addChildNodes`， `jcr:modifyProperties` 和 `jcr:removeChildNodes`， `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
