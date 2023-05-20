---
title: 腳注支援
description: 腳注的RTE支援。
exl-id: f04dae84-daab-42f8-876f-02fe426f62be
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 腳注元件 {#footnotecomponent}

**[!UICONTROL 腳注]** 是頁面末尾顯示的額外資訊或注釋。 [!UICONTROL 腳注] 包含在您的文本中以數字作為上標的注釋。

腳注按頁面上顯示的順序按順序編號。 每個腳注都有一個唯一的編號作為上標，該編號與位於頁面底部的編號相對應。 編號旁邊將顯示補充資訊作為腳注說明。

![腳注說明](/help/forms/assets/footnote_description.png)


## 腳注的用法 {#usesoffootnotes}

* 有助於提供引文。
* 提供可中斷主資訊正常流的額外資訊。
* 提供家長資訊或版權權限。

在適應性Forms, [!UICONTROL 腳注] 用於顯示有關如何完成或使用表單的資訊。 有關如何建立自適應Forms的資訊，請參見 [建立自適應窗體](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html)。

## 自適應Forms {#using-footnote-adaptiveforms}

要在自適應Forms中添加腳注，請執行以下步驟：
1. 在中開啟自適應窗體 **編輯** 的子菜單。
1. 在元件瀏覽器中，拖放 **[!UICONTROL 文本]** 到「自適應」窗體。
1. 選擇 **[!UICONTROL 文本]** 添加的元件和點擊 ![招商](assets/configure-icon.svg) 編輯其屬性。

   ![自適應Forms](/help/forms/assets/footnote_rte.png)

1. 選擇要為其添加腳注說明的文本，然後按一下  ![星](/help/forms/assets/asterisk.svg) 按鈕 **[!UICONTROL 腳注]** 元件。

1. 按一下 ![檢查](/help/forms/assets/save_icon.svg) 的子菜單。

   >[!NOTE]
   >
   >* 腳注會自動編號，並以在「自適應表單」上建立的方式顯示。
   >* 如果有重複的腳注，則所有重複的腳注的計算相同。


1. 在元件瀏覽器中，拖放 **[!UICONTROL 腳注佔位符]** 到「自適應」窗體。
   >[!NOTE]
   >
   >* 在發佈實例中，腳注顯示在 **[!UICONTROL 腳注佔位符]** 元件被放置到「自適應窗體」上。
   >* 在不同的面板之間導航時，在 **[!UICONTROL 腳注佔位符]** 在導航面板中。


1. 保存屬性。

在運行時，數字將作為上標出現在文本中，其相應說明將出現在 **[!UICONTROL 腳注]** 在 [!UICONTROL 腳注佔位符] 的上界。 通過按一下腳注說明上的相應編號，可以直接導航到腳注說明 [!UICONTROL 腳注]。
