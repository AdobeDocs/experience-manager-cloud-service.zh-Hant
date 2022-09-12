---
title: 製作概念
description: AEM中的製作概念
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 2%

---

# 製作概念 {#authoring-concepts}

AEM安裝通常至少包含兩個環境：

* 作者
* 發佈

這些互動可讓您將內容提供至您的網站，讓您的訪客可以存取。

製作環境提供建立、更新和檢閱此內容的機制，之後才會實際發佈內容：

* 作者會建立並檢閱內容。 內容可以是許多不同的類型，例如頁面、資產、出版物等。
* 此內容會在某個時間點發佈至您的網站。

![作者、發佈者和Dispatcher的圖表](/help/sites-cloud/authoring/assets/author-publish.png)

在製作環境中，AEM的功能可透過AEM製作UI使用。 針對發佈環境，您可設計供使用者使用之介面的完整外觀與風格。

## 製作環境 {#author-environment}

作者的工作方式為 **作者環境**. 這為建立內容提供了一個易於使用的介面(圖形用戶介面（GUI或UI）)。 它需要作者使用已指派適當存取權限的帳戶登入。

>[!NOTE]
>
>您的帳戶需要適當的存取權來建立、編輯或發佈內容。

根據您的執行個體和您的個人存取權限的設定方式，您可以對您的內容執行許多工作，包括：

* 在頁面上產生新內容或編輯現有內容
* 使用預先定義的範本建立新內容頁面
* 建立、編輯及管理資產和集合
* 移動、複製和刪除內容頁面、資產等
* 發佈（或取消發佈）頁面、資產等。

此外，還有一些管理任務可幫助您管理內容：

* 控制如何管理變更的工作流程，例如在發佈前強制執行審核
* 協調個別工作的專案

>[!NOTE]
>
>AEM也可從製作環境中管理。

## 發佈環境 {#publish-environment}

準備就緒後，您網站的內容會發佈至 **發佈環境**. 在此，網站的頁面會根據設計介面的外觀與風格提供給預定對象使用。

如需發佈和取消發佈頁面的詳細資訊，請參閱本檔案 [發佈頁面。](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

若要最佳化網站訪客的效能，請 **[dispatcher](/help/implementing/dispatcher/overview.md)** 實作負載平衡和快取。
