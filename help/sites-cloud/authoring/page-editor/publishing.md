---
title: 使用頁面編輯器發佈內容
description: 瞭解頁面編輯器如何發佈內容。
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5871e04d3bd78bdd8df55d42e7619c98ea3f38ca
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# 使用網站編輯器發佈內容 {#publishing}

瞭解頁面編輯器如何發佈內容。

## 從頁面編輯器發佈 {#publishing-from-the-page-editor}

如果您在[頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)中編輯頁面，可以直接從編輯器發佈該頁面。

1. 選取&#x200B;**頁面資訊**&#x200B;圖示以開啟功能表，然後選取&#x200B;**發佈頁面**&#x200B;選項。

   ![透過頁面選項發佈頁面](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 視頁面是否有需要發佈的參照而定：

   * 如果沒有要發佈的引用，則會直接發佈頁面。
   * 如果頁面含有需要發佈的參考，這些參考會列在&#x200B;**發佈**&#x200B;精靈中，您可以在其中執行下列任一操作：
      * 指定您要與頁面一起發佈的資產或標籤等，然後使用&#x200B;**發佈**&#x200B;來完成程式。
      * 使用&#x200B;**取消**&#x200B;中止動作。

   ![使用頁面](/help/sites-cloud/authoring/assets/publishing-references.png)發佈參考

1. 選取&#x200B;**發佈**&#x200B;會將頁面復寫至發佈環境。 在頁面編輯器中，會顯示確認發佈動作的資訊橫幅。

   ![發佈狀態資訊橫幅](/help/sites-cloud/authoring/assets/publishing-info.png)

   在主控台中檢視相同頁面時，會顯示更新的發佈狀態。

   在網站主控台的資料行檢視中![頁面發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>從頁面編輯器發佈是簡單的發佈，也就是說，只會發佈選取的頁面，而不會發佈任何子頁面。

>[!NOTE]
>
>無法發佈編輯器中由[別名](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced)存取的頁面。 編輯器中的發佈選項僅適用於透過實際路徑存取的頁面。

## 從頁面編輯器取消發佈 {#unpublishing}

使用頁面編輯器編輯頁面時，如果您要取消發佈該頁面，請在&#x200B;**頁面資訊**&#x200B;選單中選取&#x200B;**取消發佈頁面**，就像您[發佈頁面](#publishing-from-the-editor)一樣。

>[!NOTE]
>
>無法取消發佈編輯器中由[別名](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced)存取的頁面。 編輯器中的發佈選項僅適用於透過實際路徑存取的頁面。

## 從網站主控台發佈與取消發佈 {#publishing-sites-console}

您也可以從Sites主控台](/help/sites-cloud/authoring/sites-console/publishing-pages.md)發佈[，當您想要發佈多個內容頁面，或排程發佈或取消發佈時，這會很有用。
