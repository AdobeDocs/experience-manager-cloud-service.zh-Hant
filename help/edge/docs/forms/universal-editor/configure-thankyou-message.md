---
title: 如何設定重新導向頁面或感謝訊息？
description: 瞭解使用者如何顯示感謝訊息或重新導向至表單作者在建立表單時可設定的網頁。
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
source-git-commit: 87650caea6eb907093f0f327f1dbc19641098e4a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 設定重新導向或感謝訊息

在使用通用編輯器建立的表單中，表單作者可以設定使用者提交表單後會發生什麼情況。 您可以顯示感謝訊息，或使用「編輯表單屬性」擴充功能中的「提交」索引標籤，將使用者重新導向至特定網頁。

您可以使用&#x200B;**AEM表單屬性**&#x200B;擴充功能的&#x200B;**提交**&#x200B;索引標籤，為在Universal Editor中建立的表單設定「感謝您」訊息或重新導向URL。

## 先決條件

您可以使用&#x200B;**編輯表單屬性**&#x200B;擴充功能的&#x200B;**提交**&#x200B;索引標籤，為在Universal Editor中建立的表單設定提交動作。

![表單屬性圖示](/help/forms/assets/ue-form-properties-icon.png)

![通用編輯器表單屬性](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> * 如果您在通用編輯器介面中看不到&#x200B;**表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
> * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。

## 如何設定重新導向或感謝訊息？

在提交表單時，您可以將使用者重新導向至其他網頁或顯示訊息。

若要設定重新導向頁面或感謝訊息：

1. 開啟最適化表單進行編輯。
2. 開啟內容樹狀結構並選取&#x200B;**[!UICONTROL 參考線容器]**。
3. 按一下最適化表單容器屬性![最適化表單容器屬性](/help/forms/assets/configure-icon.svg)圖示。 用來設定資料模型的最適化表單容器對話方塊隨即開啟。
4. 開啟&#x200B;**[!UICONTROL 提交]**&#x200B;標籤。 會顯示設定重新導向頁面或訊息的選項：

   ![指南容器的[提交]對話方塊以設定重新導向頁面或訊息](/help/forms/assets/adaptive-forms-core-components-redirect-page-or-thank-you-message.png)

**設定重新導向URL**

* 若要設定重新導向URL，請在[送出]選項中選取&#x200B;**[!UICONTROL 重新導向至URL選項]**，並提供絕對位址、重新導向URL或AEM Sites頁面的相對路徑。

![重新導向](/help/edge/docs/forms/universal-editor/assets/redirect-ue.png)

**設定感謝訊息**

* 若要設定自訂或感謝訊息，請選取&#x200B;**[!UICONTROL 顯示訊息]**&#x200B;選項，並在[訊息內容]方塊中提供訊息。 它是RTF文字方塊，您可以使用全熒幕選項來檢視所有可用的RTF專案。

![感謝您](/help/edge/docs/forms/universal-editor/assets/thankyou-ue.png)

表單作者可為每個表單設定頁面，表單使用者在提交表單後會重新導向至該頁面。
