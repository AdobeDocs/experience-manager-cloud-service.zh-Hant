---
Title: How to configure Marketo Engage data for Adaptive Forms?
Description: Learn how to use Marketo Engage schema in Adaptive Forms.
Keywords: Use Marketo Engage data source in Adaptive Forms, How to connect a Marketo instance data source with form? , Connect a form to Marketo.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: dabf8029577c5fb6bb5eebdbf10d77f3d4d95a5d
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 4%

---

# 針對現有的最適化表單設定 Marketo Engage 資料來源

<span class="preview">此功能可在早期採用者方案下使用。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。</span>

![工作流程](/help/forms/assets/workflow-marketo-2.png)

建立雲端服務設定以整合Marketo Engage與現有AEM Forms後，您可以設定表單的資料來源。

設定資料整合可讓使用者連線至各種資料來源或結構描述。 與Marketo Engage資料來源整合，並跨不同表單使用，可簡化對該資料的操作。 若要探索最適化表單支援的現成可用資料來源，請參閱[設定資料來源](/help/forms/configure-data-sources.md)文章。

## 設定表單之Marketo Engage資料來源的考量

設定表單的Marketo Engage資料來源時，請考量下列事項：

* 無法將Edge Delivery Services Forms與Marketo Engage連線。

## 使用Marketo Engage表單資料來源的先決條件

搭配表單使用Marketo Engage資料來源的先決條件：

* 建立[雲端服務設定以整合Marketo Engage與表單](/help/forms/integrate-form-to-marketo-engage.md)。

## 如何為Marketo Engage資料來源設定現有的最適化表單？

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

<span>此影片僅適用於核心元件。 若為UE/Foundation元件，請參閱文章。</span>

>[!BEGINTABS]

>[!TAB 基礎元件]

若要使用Marketo Engage資料來源設定以基礎元件為基礎的最適化表單，請執行以下步驟：

1. 登入您的 [!DNL Experience Manager Forms] 作者實例。
1. 開啟最適化表單以進行編輯，並導覽至最適化表單容器屬性的&#x200B;**[!UICONTROL 資料模型]**&#x200B;區段，然後選取一個表單模型做為&#x200B;**聯結器**。
1. 從下拉式清單中選取&#x200B;**[!UICONTROL 聯結器]**。
1. 選取&#x200B;**[!UICONTROL 聯結器]**&#x200B;之後，您可以選取雲端設定。

   ![選取Marketo聯結器](/help/forms/assets/select-marketo-connector-af1.png){width=50%, height=50%}

   根據選取的Marketo Engage組態，表單元素會顯示在側邊欄中&#x200B;**[!UICONTROL 內容瀏覽器]**&#x200B;的&#x200B;**[!UICONTROL 資料模型物件]**&#x200B;索引標籤中。 您可以拖放這些元素來建置最適化表單。

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-af1.png){width=50%, height=50%}

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

或者，您也可以編輯最適化表單屬性，以變更其相關聯的設定。

最適化表單現在已使用連線的Marketo Engage例項的資料來源設定。 現在，請將其設定為傳送資料至Adobe Marketo Engage。

>[!TAB 核心元件]

若要使用Marketo Engage資料來源根據核心元件設定最適化表單，請執行以下步驟：

1. 登入您的 [!DNL Experience Manager Forms] 作者實例。

1. 開啟最適化表單進行編輯。
1. 開啟內容樹狀結構並選取&#x200B;**[!UICONTROL 參考線容器]**。
1. 按一下最適化表單容器屬性![最適化表單容器屬性](/help/forms/assets/configure-icon.svg)圖示。 可設定資料來源的最適化表單容器對話方塊隨即開啟。
1. 開啟&#x200B;**[!UICONTROL 資料模型]**&#x200B;標籤，並選取表單模型做為&#x200B;**聯結器**。
1. 從下拉式清單中選取&#x200B;**[!UICONTROL 聯結器]**。

1. 選取&#x200B;**[!UICONTROL 聯結器]**&#x200B;之後，您可以選取雲端設定。

   ![選取Marketo聯結器](/help/forms/assets/select-marketo-connector.png){width=50%, height=50%}

   根據選取的Marketo Engage組態，表單元素會顯示在側邊欄中&#x200B;**[!UICONTROL 內容瀏覽器]**&#x200B;的&#x200B;**[!UICONTROL 資料模型物件]**&#x200B;索引標籤中。 您可以拖放這些元素來建置最適化表單。

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source.png){width=50%, height=50%}

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

或者，您也可以編輯最適化表單屬性，以變更其相關聯的設定。

最適化表單現在已使用連線的Marketo Engage例項的資料來源設定。 現在，請將其設定為傳送資料至Adobe Marketo Engage。

>[!TAB 通用編輯器]

若要使用Marketo Engage資料來源設定在Universal Editor中編寫的最適化表單，請執行以下步驟：

1. 開啟表單的屬性以進行編輯。
1. 選取&#x200B;**[!UICONTROL 表單模型]**。
1. 從&#x200B;**表單模型**&#x200B;中選取&#x200B;**[!UICONTROL 聯結器]**。
1. 選取&#x200B;**[!UICONTROL 聯結器]**&#x200B;之後，您可以選取雲端設定。

   ![選取Marketo聯結器](/help/forms/assets/select-marketo-connector-ue.png)

1. 按一下「**[!UICONTROL 儲存並關閉]**」。

根據選取的Marketo Engage組態，表單元素會顯示在「屬性」面板中內容瀏覽器的&#x200B;**[!UICONTROL 資料來源]**&#x200B;索引標籤中。 您可以拖放這些元素來建置最適化表單。

![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-ue.png)

表單現在已使用連線的Marketo Engage執行個體的資料來源設定。 現在，請將其設定為傳送資料至Adobe Marketo Engage。

>[!ENDTABS]

## 常見問題集(FAQs)

**問：變更表單的聯結器會發生什麼事？**\
**A：**&#x200B;如果您變更表單的聯結器，現有的繫結就會變成無效。

**問：規則編輯器的Invoke Service中哪些作業可用於與Marketo Engage整合的表單？**\
**A：**&#x200B;在與Marketo Engage整合的表單的&#x200B;**叫用服務**&#x200B;中可用的三個現成作業是：
* 同步處理銷售機會
* 依ID取得銷售機會
* 依篩選器型別取得銷售機會

## 下一步

現在您已針對最適化Forms設定Marketo Engage資料來源。 接著，您可以[設定最適化表單，將資料傳送至Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)。

## 相關的文章

{{af-submit-action}}

## 另請參閱

{{marketo-engage-see-also}}
