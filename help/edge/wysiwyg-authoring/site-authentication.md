---
title: 設定網站驗證以進行內容製作
description: 瞭解AEM Live如何支援權杖式驗證，以及如何設定AEM以搭配WYSIWYG製作使用驗證。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 6d28b831fb902173bb5fbadd4aa2a52ba58e0a3b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 2%

---


# 設定網站驗證以進行內容製作 {#site-authentication}

瞭解AEM Live如何支援權杖式驗證，以及如何設定AEM以搭配WYSIWYG製作使用驗證。

## 概觀 {#overview}

AEM Live支援權杖型驗證。 網站驗證通常會同時套用至預覽和發佈網站，但也可以設定為只個別保護任一網站。

>[!NOTE]
>
>如果您選擇啟用網站驗證，您也必須在AEM編寫環境中進行設定

## 要求 {#requirements}

若要設定網站驗證以搭配內容製作使用，您必須先完成下列工作：

* 本檔案假設您已根據[使用Edge Delivery Services進行WYSIWYG編寫的開發人員快速入門手冊，為您的專案建立網站。](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* 您必須已[啟用專案的重新導向功能。](/help/edge/wysiwyg-authoring/repoless.md)

## 設定網站驗證 {#configure-authentication}

如需有關如何設定網站驗證的詳細資訊，請參閱檔案[設定網站驗證](https://www.aem.live/docs/authentication-setup-site)。

設定驗證時，請注意下列資訊：

* 技術帳戶的ID
* 您的網站驗證Token

需要這些專案才能完成AEM編寫環境的網站驗證設定。

## 設定製作環境 {#authoring-environment}

設定網站驗證後，您就可以在AEM編寫環境中啟用它。

1. 登入AEM作者執行個體並移至&#x200B;**工具** -> **雲端服務** -> **Edge Delivery Services設定**，然後選取為您的網站自動建立的設定，並點選或按一下工具列中的&#x200B;**屬性**。
1. 在&#x200B;**Edge Delivery Services設定**&#x200B;視窗中，選取&#x200B;**驗證**&#x200B;索引標籤，並提供下列值，您在設定網站驗證時已記錄這些值。

   * **技術帳戶ID**
   * **網站驗證Token**

   ![Edge Delivery Services設定](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. 點選或按一下「**儲存並關閉**」。
