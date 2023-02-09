---
title: 腳注支援
description: 腳注的RTE支援。
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 腳注元件 {#footnotecomponent}

**[!UICONTROL 腳注]** 是出現在頁面結尾的額外資訊或附註。 [!UICONTROL 腳注] 包括在文本中以數字作為上標的注釋。

腳注會依其在頁面上的顯示順序排列編號。 每個腳注都有一個唯一編號作為上標，該編號與放在頁面底部的編號相對應。 數字旁邊顯示補充資訊作為腳注說明。

![腳注說明](/help/forms/assets/footnote_description.png)


## 腳注使用 {#usesoffootnotes}

* 有助於提供引用。
* 提供可中斷主資訊正常流的額外資訊。
* 提供括弧資訊或版權權限。

在適用性Forms中， [!UICONTROL 腳注] 用於顯示如何完成或使用表單的資訊。 如需如何建立最適化Forms的詳細資訊，請參閱 [建立最適化表單](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## 適用性Forms中的腳注 {#using-footnote-adaptiveforms}

若要在適用性Forms中新增腳注，請執行下列步驟：
1. 在中開啟最適化表單 **編輯** 模式。
1. 從元件瀏覽器中，拖放 **[!UICONTROL 文字]** 元件至適用性表單。
1. 選取 **[!UICONTROL 文字]** 您新增的元件，點選 ![cppr](assets/configure-icon.svg) 來編輯其屬性。

   ![適用性Forms中的腳注](/help/forms/assets/footnote_rte.png)

1. 選擇要為其添加腳注說明的文本，然後按一下  ![星星](/help/forms/assets/asterisk.svg) 按鈕 **[!UICONTROL 腳注]** 元件。

1. 按一下 ![check](/help/forms/assets/save_icon.svg) 以儲存變更和樣式。

   >[!NOTE]
   >
   >* 腳注會自動編號，並以在適用性表單中建立的方式顯示。
   >* 如果有重複的腳注，則所有重複的腳注的計算都相同。


1. 從元件瀏覽器中，拖放 **[!UICONTROL 腳注佔位符]** 元件至適用性表單。
   >[!NOTE]
   >
   >* 在發佈例項中，腳注顯示在 **[!UICONTROL 腳注佔位符]** 元件會放置到最適化表單上。
   >* 當您在不同面板之間導覽時，只有可見的腳注會出現在 **[!UICONTROL 腳注佔位符]** 即會顯示在導覽面板中。


1. 儲存屬性。

在運行時，數字將以上標形式顯示在文本上，其相應說明將顯示在 **[!UICONTROL 腳注]** 元件 [!UICONTROL 腳注佔位符] 會放置在最適化表單上。 您可以按一下腳注說明上對應的數字，直接導覽至腳注說明。 [!UICONTROL 腳注].