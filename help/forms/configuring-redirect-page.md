---
title: 如何設定重新導向頁面？
description: 瞭解如何將使用者重新導向至表單作者可在建立表單時設定的網頁。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 0f8aed76af4d2640094a76f2805f73a0a619e33f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 6%

---

# 設定重新導向頁面 {#configuring-redirect-page}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-redirect-page.html) |
| AEM as a Cloud Service  | 本文章 |

表單作者可為每個表單設定頁面，表單使用者在提交表單後會重新導向至該頁面。

1. 在編輯模式中，選取元件，然後按一下 ![欄位層級](assets/select_parent_icon.svg) > **[!UICONTROL 最適化表單容器]**，然後按一下 ![cmppr](assets/configure-icon.svg).

1. 在側邊欄中，按一下 **[!UICONTROL 提交]**.

1. 在下方提供重新導向頁面的URL **[!UICONTROL 重新導向URL/路徑]** 在 **[!UICONTROL 提交]** 區段。
1. 您可以選擇在提交動作底下，針對提交至REST端點動作，設定要傳遞至重新導向頁面的引數。

   ![重新導向頁面設定](assets/redirect-url.png)

   重新導向頁面設定

表單作者可使用以下傳遞至「感謝您」頁面的引數。 針對所有可用的提交動作， `status` 和 `owner` 引數會傳遞。 除了這兩個引數以外，系統還會為下列提交動作傳遞一些其他引數：

* **[!UICONTROL 提交至REST端點]**：傳遞為欄位內與引數對應新增的引數。 `status` 和 `owner` 此提交動作中未傳遞引數。 如需詳細資訊，請參閱 [設定提交至REST端點提交動作](configuring-submit-actions.md).

>[!MORELIKETHIS]
>
>* [設定重新導向頁面或感謝訊息](/help/forms/configure-redirect-page-or-thank-you-message.md)
