---
title: 製作和發佈概念
description: 瞭解使用AEM、作者、預覽和發佈環境在AEM中編寫的概念。
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---


# 製作和發佈概念 {#authoring-publishing}

對於內容作者，AEM as a Cloud Service安裝在其最基本的層級可視為三個主要層級

* 作者階層
* 預覽層
* Publish階層

這些階層可互動，讓您在網站上提供內容，讓訪客能夠存取。 基本的工作流程為：

1. 內容作者會使用作者層級建立其內容。
1. 內容作者可使用預覽層級讓檢閱者預覽其內容。
1. 內容可供公眾使用後，作者將使用發佈層級發佈內容。

內容可以是許多不同的型別，包括頁面、資產和出版物。 根據作者的決定，可以略過預覽內容。

![作者、發行者和Dispatcher的圖表](assets/author-publish.jpg)

如需AEM as a Cloud Service技術架構的詳細資訊，請參閱檔案[Adobe Experience Manager as a Cloud Service架構簡介](/help/overview/architecture.md)。

{{edge-delivery-authoring}}

## 製作內容 {#author-environment}

製作層級的製作環境提供簡單易用的圖形使用者介面來建立內容。 它要求作者使用指派有適當存取許可權的帳戶登入。

根據您設定執行個體和個人存取許可權的方式，您可以對內容執行許多工作，包括（其中包括）：

* 產生新內容或編輯頁面上的現有內容
* 使用預先定義的範本來建立內容頁面
* 建立、編輯和管理您的資產和集合
* 移動、複製和刪除內容頁面和資產。
* 發佈（或取消發佈）頁面和資產。

此外，還有一些管理任務可協助您管理內容：

* 控制變更管理方式的工作流程，例如在發佈前強制執行稽核
* 協調個別任務的專案

AEM也可從製作環境進行管理。

請參閱檔案[製作快速入門手冊](/help/sites-cloud/authoring/quick-start.md)，瞭解製作程式的概觀。

## 預覽內容 {#previewing-content}

AEM也提供預覽服務，可讓開發人員和內容作者在網站到達發佈環境並公開使用之前預覽網站的最終體驗。

如需詳細資訊，請參閱檔案[預覽內容](/help/sites-cloud/authoring/sites-console/previewing-content.md)。

## Publish環境 {#publish-environment}

準備就緒後，您的網站內容會發佈至發佈層級的發佈環境。 在此處，根據內容範本的外觀，目標對象可以存取網站頁面。

請參閱檔案[發佈頁面](/help/sites-cloud/authoring/sites-console/publishing-pages.md)，以取得有關發佈和取消發佈頁面的詳細資訊。

## Dispatcher {#dispatcher}

為了最佳化網站訪客的效能，**[Dispatcher](/help/implementing/dispatcher/overview.md)**&#x200B;針對發佈和預覽層級實作負載平衡和快取。
