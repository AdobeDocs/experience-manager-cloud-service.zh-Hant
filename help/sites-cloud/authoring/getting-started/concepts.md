---
title: 製作概念
description: 創作概AEM念
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 2%

---

# 製作概念 {#authoring-concepts}

安AEM裝通常至少包括兩個環境：

* 作者
* 發佈

這些交互功能使您能夠在您的網站上提供內容，以便您的訪問者能夠訪問它。

作者環境提供了建立、更新和審閱此內容的機制，然後才能實際發佈它：

* 作者建立和審閱內容。 內容可以是多種不同類型的，如頁面、資產、出版物等。
* 此內容將在某個時候發佈到您的網站。

![作者、發佈者和調度員的圖表](/help/sites-cloud/authoring/assets/author-publish.png)

在作者環境中，通AEM過創作UI提AEM供功能。 對於發佈環境，您設計了提供給用戶的介面的整個外觀。

## 作者環境 {#author-environment}

作者的作品 **作者環境**。 這為建立內容提供了一個易於使用的介面(圖形用戶介面（GUI或UI）)。 它要求作者使用已分配了適當訪問權限的帳戶登錄。

>[!NOTE]
>
>您的帳戶需要相應的訪問權限才能建立、編輯或發佈內容。

根據您的實例和個人訪問權限的配置方式，您可以對內容執行許多任務，包括：

* 在頁面上生成新內容或編輯現有內容
* 使用預定義模板建立新內容頁
* 建立、編輯和管理資產和收集
* 移動、複製和刪除內容頁面、資產等
* 發佈（或取消發佈）頁面、資產等

此外，還有一些管理任務可幫助您管理內容：

* 控制更改管理方式的工作流，例如在發佈前強制執行審閱
* 協調單個任務的項目

>[!NOTE]
>
>也AEM由作者環境管理。

## 發佈環境 {#publish-environment}

準備好後，您的站點內容將發佈到 **發佈環境**。 此處，網站的頁面根據設計介面的外觀向目標受眾提供。

有關發佈和取消發佈頁面的詳細資訊，請參閱文檔 [正在發佈頁面。](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

為優化網站訪問者的效能， **[調度](/help/implementing/dispatcher/overview.md)** 實現負載平衡和快取。
