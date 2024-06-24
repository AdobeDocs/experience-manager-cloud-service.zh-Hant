---
title: 內容片段 - 刪除考量事項
description: 在AEM中定義內容片段刪除原則之前，請檢閱這些重要考量。 內容片段是傳送Headless內容的強大工具，必須仔細考慮刪除這些片段的影響。
feature: Content Fragments
role: User, Developer, Architect
exl-id: d1726bff-3aa8-4758-bee7-0cacea1f660a
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 刪除內容片段的注意事項 {#delete-considerations-content-fragments}

在AEM中定義內容片段的刪除政策之前，請檢閱這些重要考量。 內容片段是傳送Headless內容的強大工具，必須仔細考慮刪除這些片段的影響。

## 許可權 — 刪除或不刪除 {#permissions-delete-or-not-delete}

刪除內容的功能非常強大，但可能比較敏感，許多行業都需要限制和控制這些許可權的分配方式。

關於刪除許可權，內容片段必須考量為兩個層級：

1. **作為單一實體的內容片段。**

   * **使用案例**：必須編輯/更新內容片段的使用者 —  **並刪除整個片段**.
   * **許可權**：您可透過「使用者」及/或「群組管理」指派「刪除」許可權。

2. **構成內容片段的多個子實體；例如，變數、子節點。**

   內容片段編輯器的基本操作需要可以刪除這類暫時性子元素。 例如，操控變數時；編輯中繼資料或管理關聯內容時，也可以。

   * **使用案例**：必須編輯/更新內容片段的使用者 —  **不允許刪除整個片段**.
   * **許可權**：請參閱 [僅編輯器功能所需的許可權](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>另請參閱如何在AEM中稽核使用者管理作業。

## 僅編輯器功能所需的許可權 {#permissions-required-for-editor-functionality-only}

對於需要編輯/更新內容片段的使用者， **不允許他們刪除整個片段**，必須指派特定許可權，因為內容片段編輯器的基本操作要求可以刪除暫時性子元素。

例如，操控變數時；編輯中繼資料或管理關聯內容時，也可以。

>[!NOTE]
>
>編輯/更新內容片段所需的刪除許可權包含在透過使用者和/或群組管理指派的刪除許可權中。

編輯/更新片段所需的許可權必須套用至包含內容片段的節點或適當的父節點（在下的任何層級）。 `/content/dam`)。 當指派給此類父節點時，許可權會套用至該分支內的所有節點。

例如，用來存放所有內容片段的資料夾，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>設定許可權： `/content/dam` 也是可能的，因為所有內容片段都儲存在這裡。
>
>不過，此動作會將相同的刪除許可權套用至 *全部* 其他資產型別。

允許特定使用者和/或群組編輯/更新內容片段的先決條件是：

>[!NOTE]
>
>此清單顯示所需的所有許可權，而不只是刪除許可權。

* 對於內容片段節點或資料夾：

   * `jcr:addChildNodes`、`jcr:modifyProperties`

* 對於 `jcr:content`所有內容片段的節點：

   * `jcr:addChildNodes`， `jcr:modifyProperties`、和 `jcr:removeChildNodes`

* 適用於以下所有節點 `jcr:content` 所有內容片段的：

   * `jcr:addChildNodes`， `jcr:modifyProperties`、和 `jcr:removeChildNodes`， `jcr:removeNode`
