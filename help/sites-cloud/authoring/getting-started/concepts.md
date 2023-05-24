---
title: 編寫概念
description: AEM中的製作概念
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: b407765438086bb2f7fb720fb7f1dd05699cb48f
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 4%

---

# 編寫概念 {#authoring-concepts}

AEM 安裝通常至少包含兩個環境：

* 作者
* 發佈

這些互動可讓您提供網站上的內容，以便您的訪客可以存取。

作者環境提供機制，可在實際發佈此內容之前建立、更新和檢閱此內容：

* 作者建立和檢閱內容。 內容可以是許多不同的型別，例如頁面、資產、出版物等。
* 此內容會在某個時間點發佈至您的網站。

![作者、發佈者和Dispatcher圖表](/help/sites-cloud/authoring/assets/author-publish.png)

在製作環境中，AEM的功能可透過AEM製作UI提供。 對於發佈環境，您可以設計可供使用者使用的介面的完整外觀。

## 作者環境 {#author-environment}

作者的工作方式稱為 **作者環境**. 這提供建立內容時易於使用的介面(圖形化使用者介面（GUI或UI）)。 它要求作者使用已指派適當存取許可權的帳戶登入。

>[!NOTE]
>
>您的帳戶需要適當的存取權才能建立、編輯或發佈內容。

根據您設定執行個體和個人存取許可權的方式，您可以對內容執行許多工作，包括（其中包括）：

* 在頁面上產生新內容或編輯現有內容
* 使用預先定義的範本來建立新內容頁面
* 建立、編輯和管理您的資產和集合
* 移動、複製和刪除內容頁面、資產等。
* 發佈（或取消發佈）頁面、資產等。

此外，還有一些管理任務可協助您管理內容：

* 控制變更管理方式的工作流程，例如在發佈前強制執行稽核
* 協調個別任務的專案

>[!NOTE]
>
>AEM也可從製作環境進行管理。

## 預覽內容 {#previewing-content}

AEM也提供Sites預覽服務，可讓開發人員和內容作者在網站到達發佈環境並公開使用之前，預覽網站的最終體驗。

另請參閱 [預覽內容](/help/sites-cloud/authoring/fundamentals/previewing-content.md) 以取得更多詳細資料。

## 發佈環境 {#publish-environment}

準備就緒後，您的網站內容會發佈至 **發佈環境**. 在此處，根據設計介面的外觀，目標受眾可以使用網站頁面。

如需發佈和取消發佈頁面的詳細資訊，請參閱檔案 [發佈頁面。](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

若要最佳化網站訪客的效能， **[dispatcher](/help/implementing/dispatcher/overview.md)** 實作負載平衡和快取。
