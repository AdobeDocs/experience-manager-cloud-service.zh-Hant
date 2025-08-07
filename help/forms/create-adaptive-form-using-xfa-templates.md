---
title: 如何使用XFA表單範本，根據核心元件建立最適化表單？
description: 瞭解如何使用 [!DNL Experience Manager Forms] 使用XFA表單範本或XDP檔案來建立最適化表單。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: f3c9b798-8b20-4674-9b96-a3a0b143d947
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 13%

---

# 以 XFA Form 範本為基礎建立最適化表單 (核心元件)

<span class="preview">此功能可在早期採用者方案下使用。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。</span>

AEM as a Cloud Service讓使用者可選擇使用XFA (XML Forms Architecture)表單範本或`*.XDP` (XML Data Package)檔案，根據核心元件建立最適化Forms。 此功能可讓使用者將欄位從XFA表單範本或XDP檔案直接移轉至最適化Forms，以節省時間。

您可以重新利用您的XFA表單範本或XDP檔案表單範本，以根據核心元件建立最適化Forms。 若要重新調整用途，請上傳XFA表單範本或XDP檔案，並將其與調適型表單建立關聯。 在最適化表單製作期間，XFA表單範本或XDP檔案的元素可用於內容尋找器。 從「內容尋找器」中，您可以將表單範本元素拖放至表單上。

## 根據XFA表單範本或XDP檔案建立表單的優點

根據XFA表單範本或XDP檔案建立表單的優點如下：

* **省時**：您可以快速重複使用現有的XFA表單範本（XDP檔案），而不需要重新建立表單結構，在編寫過程中節省時間和精力。
* **輕鬆移轉**：如果您已使用XFA表單範本，此選項可讓您輕鬆移轉到Adaptive Forms，讓您發揮現代AEM核心元件的優點，而不會遺失現有的表單資料與邏輯。
* **改善的使用者體驗**：最適化Forms比XFA表單更具回應能力且可自訂。 透過轉換為最適化Forms，您可以確保跨不同裝置和熒幕大小獲得更方便使用的體驗。
* **增強型整合**：最適化Forms可與其他功能（例如工作流程、資料繫結和表單提交）更妥善整合，讓工作流程更順暢，整體表單管理也更好。

## 必要條件

您需要下列專案，才能使用XFA表單範本或XDP檔案，根據核心元件建立最適化表單：

* [為您的環境啟用最適化Forms核心元件](enable-adaptive-forms-core-components.md)。
* 建議熟悉下列領域：
   * 建立最適化表單
   * XFA (XML Forms架構)

## 如何使用XFA表單範本或XDP檔案建立最適化表單？

執行以下步驟，使用XFA或XDP表單範本建立最適化表單：

1. 登入您的[!DNL Experience Manager Forms]作者執行個體。
1. 在 Experience Manager 登入頁面上輸入您的認證。登入後，在左上角選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。

   ![Forms和檔案](/help/forms/assets/create-fdm.png)

1. 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 最適化Forms]**。

   ![建立最適化表單](/help/forms/assets/create-af.png)

   表單建立精靈隨即開啟。
1. 在&#x200B;**Source**&#x200B;索引標籤中，根據核心元件選取範本。

   ![選取範本](/help/forms/assets/select-template.png)

   當您選取範本時，會自動選取範本中指定的主題和提交動作，並啟用&#x200B;**[!UICONTROL 建立]**&#x200B;按鈕。

   ![選取主題](/help/forms/assets/select-form-theme.png)

1. 選擇 **[!UICONTROL 建立]**。會出現一個對話方塊，用於指定標題、名稱以及儲存最適化表單的位置。
1. 指定其標題、名稱和位置。
1. 選取「**[!UICONTROL 建立]**」。
   ![提供名稱和標題](/help/forms/assets/create-form.png)

   此時已建立最適化表單，並在最適化表單編輯器中開啟。編輯器會顯示範本中可用的內容。
1. 選取![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 開啟屬性]**。

   ![開啟屬性](/help/forms/assets/form-properties.png)

   此時會開啟「表單屬性」頁面。
1. 移至&#x200B;**[!UICONTROL 表單模型]**&#x200B;標籤，然後選擇&#x200B;**表單範本**。
1. 從下拉式清單中選取.xdp檔案。

   ![選取XDP檔案](/help/forms/assets/select-xdp-file.png)

   熒幕上會顯示警告對話方塊。 按一下[確定]****&#x200B;以繼續進行。

   ![警告對話方塊](/help/forms/assets/fdm-warning.png)

1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存屬性。

   >[!NOTE]
   >
   > 在表單&#x200B;**模型**&#x200B;索引標籤中選取&#x200B;**表單範本**&#x200B;後，無法變更。


此時已建立最適化表單，並在最適化表單編輯器中開啟。編輯器會顯示範本中可用的內容。根據最適化表單的型別，相關XFA表單範本中存在的表單元素會顯示在側邊欄中&#x200B;**[!UICONTROL 內容瀏覽器]**&#x200B;的&#x200B;**[!UICONTROL 資料模型物件]**&#x200B;索引標籤中。 您也可以拖放這些元素以建置自己的最適化表單。

>[!NOTE]
>
> 您可以使用新增欄位的面板工具列，停用XDP表單欄位的指令碼。 使用[視覺規則編輯器](/help/forms/rule-editor-core-components.md)為新增的欄位建立邏輯。

