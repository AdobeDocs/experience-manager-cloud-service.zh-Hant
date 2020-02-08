---
title: 編寫概念
description: 在AEM中編寫概念
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# 編寫概念 {#authoring-concepts}

AEM安裝通常至少包含兩個環境：

* 作者
* 發佈

這些互動功能可讓您在網站上提供內容，讓您的訪客可以存取。

作者環境提供建立、更新和檢閱此內容的機制，然後再實際發佈：

* 作者會建立並檢閱內容。 內容可以是多種不同的類型，例如頁面、資產、出版品等。
* 此內容會在某個時候發佈至您的網站。

![作者、發佈者和調度員的圖表](/help/sites-cloud/authoring/assets/author-publish.png)

在作者環境中，AEM的功能可透過AEM的編寫UI取得。 針對發佈環境，您設計的整個介面外觀和感覺都提供給您的使用者。

>[!NOTE]
>
>AEM本身可用來發佈AEM檔案。

## 作者環境 {#author-environment}

作者的工作環境稱為作 **者環境**。 這為建立內容提供了易於使用的介面(圖形用戶介面（GUI或UI）)。 它要求作者使用已指派適當存取權限的帳戶登入。

>[!NOTE]
>
>您的帳戶需要適當的存取權，才能建立、編輯或發佈內容。

視您的例項和個人存取權限的設定而定，您可以對內容執行許多工作，包括：

* 產生新內容或編輯頁面上的現有內容
* 使用預先定義的範本建立新的內容頁面
* 建立、編輯和管理您的資產和系列
* 移動、複製和刪除內容頁面、資產等。
* 發佈（或取消發佈）頁面、資產等

此外，還有管理工作可協助您管理內容：

* 控制變更管理方式的工作流程，例如在發佈前強制審查
* 協調個別工作的專案

>[!NOTE]
>
>AEM也是從作者環境管理。

## 發佈環境 {#publish-environment}

準備就緒後，您網站的內容會發佈至發 **布環境**。 在這裡，網站的頁面會根據設計介面的外觀和感覺提供給預期的讀者。

如需有關發佈和取消發佈頁面的詳細資訊，請參閱檔案發 [布頁面。](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

為了最佳化網站訪客的效能，Dispatcher **[實作](/help/implementing/dispatcher/overview.md)**負載平衡和快取。
