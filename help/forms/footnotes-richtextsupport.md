---
title: 如何將註腳新增至最適化表單？
description: 在最適化表單中的註腳使用RTF編輯器(RTE) 。
exl-id: f04dae84-daab-42f8-876f-02fe426f62be
source-git-commit: 57e421a865b664c0adb7af93b33bd4b6b32049ab
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 13%

---

# 註腳元件 {#footnotecomponent}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/creating-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

**[!UICONTROL 註腳]** 是顯示在頁面結尾的額外資訊或備註位元。 [!UICONTROL 註腳] 包含以數字作為上標的文字所表示的註記。

註腳會依顯示於頁面上的順序編號。 每個註腳都有一個唯一數字做為上標，對應頁面底部的數字。 編號旁會顯示補充資訊作為註腳說明。

![註腳說明](/help/forms/assets/footnote_description.png)


## 使用註腳 {#usesoffootnotes}

* 協助提供引文。
* 提供可以中斷主要資訊正常流程的額外資訊。
* 提供括弧資訊或版權許可權。

在最適化Forms中， [!UICONTROL 註腳] 用於顯示有關如何完成或使用表單的資訊。 如需如何建立最適化Forms的相關資訊，請參閱 [建立最適化表單](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## 最適化Forms中的註腳 {#using-footnote-adaptiveforms}

若要在Adaptive Forms中新增註腳，請執行以下步驟：
1. 在中開啟最適化表單 **編輯** 模式。
1. 在元件瀏覽器中，拖放 **[!UICONTROL 文字]** 元件至最適化表單。
1. 選取 **[!UICONTROL 文字]** 您所新增並點選的元件 ![cmppr](assets/configure-icon.svg) 以編輯其屬性。

   ![最適化Forms中的註腳](/help/forms/assets/footnote_rte.png)

1. 選取您要新增註腳說明的文字，然後按一下  ![星形](/help/forms/assets/asterisk.svg) 設定樣式按鈕 **[!UICONTROL 註腳]** 元件。

1. 按一下 ![check](/help/forms/assets/save_icon.svg) 以儲存變更和樣式。

   >[!NOTE]
   >
   >* 註腳會自動編號，並以在最適化表單中建立的方式顯示。
   >* 如果有重複的註腳，則所有重複的註腳的編號相同。

1. 在元件瀏覽器中，拖放 **[!UICONTROL 註腳預留位置]** 元件至最適化表單。
   >[!NOTE]
   >
   >* 在發佈執行個體中，註腳會顯示在下列位置： **[!UICONTROL 註腳預留位置]** 元件會放置在調適型表單上。
   >* 當您在不同面板之間導覽時，只有可見的註腳會出現在 **[!UICONTROL 註腳預留位置]** 存在於已導覽面板中的物件。

1. 儲存屬性。

在執行階段，數字會以上標的形式顯示在文字上，其對應的說明會顯示在 **[!UICONTROL 註腳]** 元件在位置 [!UICONTROL 註腳預留位置] 會放置在最適化表單上。 您可以按一下「 」上對應的編號，直接導覽至註腳說明。 [!UICONTROL 註腳].


## 另請參閱 {#see-also}

{{see-also}}