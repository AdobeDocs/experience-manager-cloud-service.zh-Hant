---
title: 如何配置重定向頁？
description: 瞭解如何將用戶重定向到表單作者在建立表單時可以配置的網頁。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 配置重定向頁 {#configuring-redirect-page}

表單作者可以為每個表單配置一個頁面，在提交表單後，表單用戶將重定向到該頁面。

1. 在編輯模式下，選擇一個元件，然後按一下 ![欄位級](assets/select_parent_icon.svg) > **[!UICONTROL 自適應窗體容器]**，然後按一下 ![招商](assets/configure-icon.svg)。

1. 在提要欄中，按一下 **[!UICONTROL 提交]**。

1. 在下面提供重定向頁的URL **[!UICONTROL 重定向URL/路徑]** 的 **[!UICONTROL 提交]** 的子菜單。
1. （可選）在「提交操作」下，對於「提交至REST」終結點操作，可以配置要傳遞到重定向頁的參數。

   ![重定向頁面配置](assets/redirect-url.png)

   重定向頁面配置

表單作者可以使用傳遞到「感謝」頁的以下參數。 對於所有可用的提交操作， `status` 和 `owner` 傳遞參數。 除了這兩個參數外，還為以下「提交操作」傳遞了一些附加參數：

* **[!UICONTROL 提交到REST終結點]**:將傳遞為欄位內映射添加的參數。 `status` 和 `owner` 未在此提交操作中傳遞參數。 有關詳細資訊，請參見 [配置提交到REST終結點提交操作](configuring-submit-actions.md)。
