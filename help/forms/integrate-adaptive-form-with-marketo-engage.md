---
title: 如何使用表單精靈將Marketo Engage與AEM Forms整合？
description: 瞭解如何使用表單精靈整合Marketo Engage執行個體與AEM Forms。
keywords: 如何連結Marketo執行個體與表單？、將表單連線至Marketo、將表單與Marketo Engage整合、將調適型表單與Marketo執行個體整合。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 1fcba628-ffd8-416a-a8b5-76b35d4aabd4
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 4%

---

# 整合最適化表單與Marketo Engage

<span class="preview">此功能可在早期採用者方案下使用。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。</span>

![工作流程](/help/forms/assets/workflow-marketo-4.png)

建立雲端服務設定以將Marketo Engage與AEM Forms整合後，您可以設定最適化表單以與[Adobe Marketo Engage](https://experienceleague.adobe.com/zh-hant/docs/marketo/using/home)整合。

您可以使用表單精靈將Marketo Engage連線至調適型表單，透過引導您完成每個步驟來簡化設定程式。 其中包括選取範本、樣式和資料欄位，以及設定資料對應以確保您的表單在建立後可以與Marketo Engage通訊。 使用表單精靈，您也可以設定最適化表單，在提交時直接將資料提交至Adobe Marketo Engage。

## 設定表單之Marketo Engage資料來源的考量

設定表單的Marketo Engage資料來源時，請考量下列事項：

* 無法將Edge Delivery Services Forms與Marketo Engage連線。

## 連線Marketo Engage與表單的先決條件

連線Marketo Engage與表單的先決條件：

* 建立[雲端服務設定以整合Marketo Engage與表單](/help/forms/integrate-form-to-marketo-engage.md)。

## 如何設定新的最適化表單以與Marketo Engage整合？

>[!VIDEO](https://video.tv.adobe.com/v/3442867/marketo-aem-marketo-engage-engage-aem-forms)

<span>此影片僅適用於核心元件。 若為UE/Foundation元件，請參閱文章。</span>

>[!BEGINTABS]

>[!TAB 基礎元件]

若要根據Foundation元件設定新的最適化表單以與Marketo Engage整合，請執行以下步驟：

1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。

   ![選取Forms和檔案](/help/forms/assets/select-forms.png)

1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 自適應表單]**」。表單建立精靈隨即開啟。

   ![選取AF](/help/forms/assets/select-create-forms.png)

1. 在&#x200B;**[!UICONTROL Source]**&#x200B;索引標籤中，選取範本

   ![選取範本](/help/forms/assets/select-template-af1.png)

1. 從&#x200B;**[!UICONTROL 樣式]**，選取主題。

   ![選取主題](/help/forms/assets/select-form-theme-af1.png)
1. 在&#x200B;**[!UICONTROL 資料]**&#x200B;索引標籤中，選取資料模型做為&#x200B;**Marketo Engage**。
1. 從熒幕右窗格中顯示的下拉式清單中選取&#x200B;**[!UICONTROL 雲端設定]**。
依預設，關聯組態的所有欄位都會顯示。 此精靈可讓您透過使用核取方塊，選擇性地選擇應包含在調適型表單中的欄位。

   ![選取資料模型](/help/forms/assets/select-marketo-data-af1.png)

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;索引標籤中，選取提交動作作為&#x200B;**[!UICONTROL 提交至Marketo]**。

   當您選取資料模型為&#x200B;**Marketo Engage**&#x200B;時，則會自動選取提交動作為&#x200B;**提交至Marketo**。 您可以從&#x200B;**[!UICONTROL 提交]**&#x200B;索引標籤中選取不同的提交動作。 **[!UICONTROL 提交]**&#x200B;索引標籤會顯示所有可用的提交動作。

   ![提交至Marketo engage](/help/forms/assets/select-marketo-engage.png)

1. 選擇 **[!UICONTROL 建立]**。指定標題、名稱和位置以儲存最適化表單。

   ![建立表單](/help/forms/assets/create-marketo-form.png)

1. 選取「**[!UICONTROL 建立]**」。

最適化表單現在已設定為與Marketo Engage執行個體連線。 或者，您也可以編輯最適化表單屬性，以變更其相關聯的設定

>[!TAB 核心元件]

若要根據核心元件設定新的最適化表單以與Marketo Engage整合，請執行以下步驟：

1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。

   ![選取Forms和檔案](/help/forms/assets/select-forms.png)

1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 自適應表單]**」。表單建立精靈隨即開啟。

   ![選取AF](/help/forms/assets/select-create-forms.png)

1. 在&#x200B;**[!UICONTROL Source]**&#x200B;索引標籤中，選取範本

   ![選取範本](/help/forms/assets/select-template.png)

1. 從&#x200B;**[!UICONTROL 樣式]**，選取主題。

   ![選取主題](/help/forms/assets/select-form-theme.png)


1. 在&#x200B;**[!UICONTROL 資料]**&#x200B;索引標籤中，選取資料模型做為&#x200B;**Marketo Engage**。

1. 從熒幕右窗格中顯示的下拉式清單中選取&#x200B;**[!UICONTROL 雲端設定]**。
依預設，關聯組態的所有欄位都會顯示。 此精靈可讓您透過使用核取方塊，選擇性地選擇應包含在調適型表單中的欄位。

   ![選取資料模型](/help/forms/assets/select-marketo-data.png)

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;索引標籤中，選取提交動作作為&#x200B;**[!UICONTROL 提交至Marketo]**。

   當您選取資料模型為&#x200B;**Marketo Engage**&#x200B;時，則會自動選取提交動作為&#x200B;**提交至Marketo**。 您可以從&#x200B;**[!UICONTROL 提交]**&#x200B;索引標籤中選取不同的提交動作。 **[!UICONTROL 提交]**&#x200B;索引標籤會顯示所有可用的提交動作。

   ![提交至Marketo engage](/help/forms/assets/select-marketo-engage.png)

1. 選擇 **[!UICONTROL 建立]**。指定標題、名稱和位置以儲存最適化表單。

   ![建立表單](/help/forms/assets/create-marketo-form.png)

1. 選取「**[!UICONTROL 建立]**」。

最適化表單現在已設定為與Marketo Engage執行個體連線。 或者，您也可以編輯最適化表單屬性，以變更其相關聯的設定。

>[!TAB 通用編輯器]

若要設定在Universal Editor中編寫的新最適化表單以與Marketo Engage整合，請執行以下步驟：

1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。

   ![選取Forms和檔案](/help/forms/assets/select-forms.png)

1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 自適應表單]**」。表單建立精靈隨即開啟。

   ![選取AF](/help/forms/assets/select-create-forms.png)

1. 在&#x200B;**[!UICONTROL Source]**&#x200B;索引標籤中，選取範本

   ![選取範本](/help/forms/assets/select-template-ue.png)

1. 在&#x200B;**[!UICONTROL 資料]**&#x200B;索引標籤中，選取資料模型做為&#x200B;**Marketo Engage**。

1. 從熒幕右窗格中顯示的下拉式清單中選取&#x200B;**[!UICONTROL 雲端設定]**。
依預設，關聯組態的所有欄位都會顯示。 此精靈可讓您透過使用核取方塊，選擇性地選擇應包含在調適型表單中的欄位。

   ![選取資料模型](/help/forms/assets/select-marketo-data-ue.png)

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;索引標籤中，選取提交動作作為&#x200B;**[!UICONTROL 提交至Marketo]**。

   當您選取資料模型為&#x200B;**Marketo Engage**&#x200B;時，則會自動選取提交動作為&#x200B;**提交至Marketo**。 您可以從&#x200B;**[!UICONTROL 提交]**&#x200B;索引標籤中選取不同的提交動作。 **[!UICONTROL 提交]**&#x200B;索引標籤會顯示所有可用的提交動作。

   ![提交至Marketo engage](/help/forms/assets/select-marketo-engage-ue.png)

1. 選擇 **[!UICONTROL 建立]**。指定標題、名稱和位置以儲存最適化表單。

   ![建立表單](/help/forms/assets/create-marketo-form.png)

1. 選取「**[!UICONTROL 建立]**」。

最適化表單現在已設定為與Marketo Engage執行個體連線。 或者，您也可以編輯最適化表單屬性，以變更其相關聯的設定。

>[!ENDTABS]

## 常見問題集(FAQs)

**問：您可以變更已設定為與Marketo Engage結構描述連線的表單的提交動作嗎？**
**A：**&#x200B;依預設，當表單設定為與Marketo結構描述連線時，會選取&#x200B;**提交至Marketo Engage**&#x200B;動作。 不過，您可以視需要變更表單的提交動作。


**問：變更表單的聯結器會發生什麼事？**\
**A：**&#x200B;如果您變更表單的聯結器，現有的繫結就會變成無效。

**問：規則編輯器的Invoke Service中哪些作業可用於與Marketo Engage整合的表單？**\
**A：**&#x200B;在與Marketo Engage整合的表單的&#x200B;**叫用服務**&#x200B;中可用的三個現成作業是：

* 同步處理銷售機會
* 依ID取得銷售機會
* 依篩選器型別取得銷售機會

## 下一步

您也可以將最適化表單與[Munchkin資料庫](https://experienceleague.adobe.com/zh-hant/docs/marketo/using/product-docs/administration/setup/munchkin)連線，以追蹤造訪次數、點按次數和表單提交次數。

## 相關的文章

{{af-submit-action}}

## 另請參閱

{{marketo-engage-see-also}}
