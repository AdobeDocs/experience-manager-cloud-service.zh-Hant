---
title: 如何設定重新導向頁面？
description: 瞭解如何將使用者重新導向至表單作者可在建立表單時設定的網頁。
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 6%

---

# 設定重新導向頁面 {#configuring-redirect-page}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-redirect-page.html) |
| AEM as a Cloud Service  | 本文章 |

表單作者可為每個表單設定頁面，表單使用者在提交表單後會重新導向至該頁面。

1. 在編輯模式中，選取元件，然後按一下![欄位層級](assets/select_parent_icon.svg) > **[!UICONTROL 最適化表單容器]**，然後按一下![cmppr](assets/configure-icon.svg)。

1. 在側邊欄中，按一下&#x200B;**[!UICONTROL 提交]**。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;區段的&#x200B;**[!UICONTROL 重新導向URL/路徑]**&#x200B;下提供重新導向頁面的URL。
1. 您可以選擇在提交動作底下，針對提交至REST端點動作，設定要傳遞至重新導向頁面的引數。

   ![重新導向頁面設定](assets/redirect-url.png)

   重新導向頁面設定

表單作者可使用以下傳遞至「感謝您」頁面的引數。 針對所有可用的提交動作，會傳遞`status`和`owner`引數。 除了這兩個引數以外，系統還會為下列提交動作傳遞一些其他引數：

* **[!UICONTROL 提交至REST端點]**：傳遞為欄位內引數對應新增的引數。 此提交動作中未傳遞`status`和`owner`引數。 如需詳細資訊，請參閱[設定提交至REST端點提交動作](configuring-submit-actions.md)。

>[!MORELIKETHIS]
>
>* [設定重新導向頁面或感謝訊息](/help/forms/configure-redirect-page-or-thank-you-message.md)
