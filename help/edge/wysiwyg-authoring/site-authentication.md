---
title: 設定內容製作的網站驗證
description: 了解 AEM Live 如何支援權杖型驗證，以及如何設定 AEM 針對所見即所得製作使用驗證。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: b2838da2-79c7-49b1-a101-15c21e80197e
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '324'
ht-degree: 100%

---

# 設定內容製作的網站驗證 {#site-authentication}

了解 AEM Live 如何支援權杖型驗證，以及如何設定 AEM 針對所見即所得製作使用驗證。

## 概觀 {#overview}

AEM Live 支援權杖型驗證。網站驗證通常適用於預覽和發佈網站，但也可以設定為僅單獨保護任一網站。

>[!NOTE]
>
>如果您選擇啟用網站驗證，則也必須在 AEM 製作環境中進行設定

## 要求 {#requirements}

若要設定與內容製作搭配使用的網站驗證，您必須先完成下列工作：

* 此文件假設您已根據[使用 Edge Delivery Services 進行所見即所得製作的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)，為專案建立網站。
* 您必須已經[為專案啟用無存放庫功能。](/help/edge/wysiwyg-authoring/repoless.md)

## 設定網站驗證 {#configure-authentication}

請參閱[設定網站驗證](https://www.aem.live/docs/authentication-setup-site)的文件，詳細了解如何設定網站驗證。

設定驗證時，請記下以下資訊：

* 技術帳號 ID
* 您的網站驗證權杖

若要完成 AEM 製作環境的網站驗證設定，必須具備這些項目。

## 設定製作環境 {#authoring-environment}

設定網站驗證後，您可以在 AEM 製作環境中啟用。

1. 登入 AEM 作者實例，並前往「**工具**」->「**雲端服務**」->「**Edge Delivery Services 設定**」，選取為您的網站自動建立的設定，然後點選或按一下工具列中的「**屬性**」。
1. 在「**Edge Delivery Services 設定**」視窗中，選取「**驗證**」索引標籤，提供您之前複製的&#x200B;**網站驗證權杖**。

   ![Edge Delivery Services 設定](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. 驗證&#x200B;**此技術帳戶 ID** 與您先前複製的相符。

   * 此欄位是唯讀且預先定義。
   * 單一 AEM 製作環境中所有網站的技術帳戶皆相同。

1. 點選或按一下「**儲存並關閉**」。
