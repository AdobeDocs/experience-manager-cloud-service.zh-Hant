---
title: 如何設定重新導向頁面？
description: 了解如何將使用者重新導向至表單作者建立表單時可設定的網頁。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 設定重新導向頁面 {#configuring-redirect-page}

表單作者可為每個表單設定一個頁面，在提交表單後，表單使用者會重新導向至該頁面。

1. 在編輯模式中，選取元件，然後按一下 ![欄位層級](assets/select_parent_icon.svg) > **[!UICONTROL 適用性表單容器]**，然後按一下 ![cppr](assets/configure-icon.svg).

1. 在側欄中，按一下 **[!UICONTROL 提交]**.

1. 提供下方重新導向頁面的URL **[!UICONTROL 重新導向URL/路徑]** 在 **[!UICONTROL 提交]** 區段。
1. （可選）在「提交操作」下，對於「提交到REST」端點操作，您可以配置要傳遞到重定向頁的參數。

   ![重新導向頁面設定](assets/redirect-url.png)

   重新導向頁面設定

表單作者可使用傳遞至感謝頁面的下列參數。 對於所有可用的提交操作， `status` 和 `owner` 會傳遞參數。 除了這兩個參數外，還會為下列提交動作傳遞一些其他參數：

* **[!UICONTROL 提交到REST端點]**:系統會傳遞為欄位內與參數對應新增的參數。 `status` 和 `owner` 參數不會在此提交動作中傳遞。 如需詳細資訊，請參閱 [配置提交到REST端點提交操作](configuring-submit-actions.md).
