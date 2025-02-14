---
title: 按一下即可在Cloud Manager中建立Edge Delivery網站
description: 了解如何透過點擊按鈕在 Cloud Manager 中快速建立 Edge Delivery 網站。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 71%

---


# 關於在Cloud Manager中按一下即可建立Edge Delivery網站 {#about-one-click-edge-delivery-site}

一鍵式 Edge Delivery Service (EDS) 旨在自動完成 Cloud Manager 中 Edge Delivery 網站的上線和部署。只需按一下按鈕即可，大幅簡化了流程。按一下即可佈建所需的基礎結構，與 GitHub 整合以進行版本控制，並在 Google Drive 中設定您的文件和資產儲存體。

這種自動化有助於減少設定初始網站所需的手動工作。這可確保無縫的工作流程和可擴縮性，並在管理 Edge 內容方面提高團隊的效能。

## 重要概念 {#key-concepts}

按一下建立Edge Delivery網站時的主要概念。

| 重要概念 | 描述 |
| --- | --- |
| 自動化 Edge 部署 | <ul><li>使用者可以立即建立和設定Edge Delivery網站。</li><li>透過使用Cloud Manager與CI/CD工作流程的整合，它減少或消除了手動上線流程的需求。</li><li>與Cloud Manager整合，提供順暢的CI/CD工作流程。</li></ul> |
| 與 Cloud Manager 的整合 | <ul><li>使用 Cloud Manager 的使用者介面來觸發一鍵式 Edge Delivery 流程。</li><li>提供對自動存放庫建立和部署的存取。</li></ul> |
| 根據 GitHub 的版本控制 | <ul><li>使用預先定義的 boilerplate 範本在組織內建立 GitHub 存放庫以標準化部署。</li><li>與 AEM Bot 連結以進行內容更新。</li></ul> |
| 文件和資產儲存體整合 | <ul><li>產生用於儲存體的 Google Drive 資料夾。<li>在存放庫上安裝 AEM Code Sync 應用程式，以確保無縫進行同步和部署。</li></li><li>可讓多位共同作業人員輕鬆管理文件。</li></ul> |
| 安全性和可擴縮性 | <ul><li>確保遵循企業安全性標準的規範。</li><li>支援不同 Cloud Manager 租用戶下的多個 Edge Delivery 網站。</li></ul> |



## 按一下即可在Cloud Manager中建立Edge Delivery網站 {#one-click-edge-delivery-site}

若要按一下即可建立Adobe Edge Delivery網站，您的組織必須擁有可用的Edge Delivery Services授權。 此授權是Adobe Experience Manager (AEM)的一部分，是在Cloud Manager中建立Edge Delivery Services的必要許可權。

就權限而言，您必須是「業務負責人」角色的成員或已獲授予適當的權限，才能在 Cloud Manager 中新增或編輯程式。此存取等級可讓您管理 Edge Delivery Services 與程式的整合。

另請參閱 [Cloud Manager 的 Edge Delivery Services 簡介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

是否必須先建立適當的 AEM BOT 設定才能實現自動內容更新？TRUE？ FALSE？

**若要在Cloud Manager中按一下即可建立Edge Delivery網站：**

1. 在 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的程式。
1. 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。
1. 在左側功能表中的「**服務**」標頭下方，按一下 ![網頁頁面圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)「**Edge Delivery 網站**」。
1. 在 Edge Delivery 頁面的「**Edge Delivery 待辦事項清單**」對話方塊中，按一下「**完成必要條件**」群組方塊中的「**佈建**」。
1. 在「**佈建 Edge Delivery 網站**」對話方塊的「**專案名稱**」文字欄位中，輸入您的網站名稱，然後按一下「**佈建**」。
螢幕頂端中央附近會出現快顯通知，讓您知道 Edge Delivery 網站佈建已開始。
佈建完成且您的網站通過驗證後，網站名稱隨即出現在 Edge Delivery 頁面的 **Edge Delivery 網站**&#x200B;區域中。

### 探索新建立的Edge Delivery網站


1. 按一下網站名稱右側的 Git 存放庫連結。

發佈。

按一下網站名稱，

進行一些變更，然後發佈

在預覽中檢視頁面，然後變更 URL 以檢視即時版本。

新增共同作業人員。


## 預覽一鍵式Edge Delivery網站

## 發佈一鍵式Edge Delivery網站





## 新增共同作業人員至一鍵式Edge Delivery網站


































這些增強功能旨在提高自動化、簡化設定流程，並增強 Edge Delivery Services 使用者的共同作業。 <!-- CMGR-59362 -->

![按一下即可建立Edge Delivery網站](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![佈建 Edge Delivery 網站對話框](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)