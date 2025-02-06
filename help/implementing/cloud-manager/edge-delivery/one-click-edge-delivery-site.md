---
title: 在Cloud Manager中布建Edge Delivery網站
description: 瞭解如何透過按一下按鈕在Cloud Manager中快速建立Edge Delivery網站。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ac110fb006ed377403bce52c961712e6e449be88
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 8%

---


# 關於在Cloud Manager中布建Edge Delivery網站 {#about-provision-edge-delivery-site}

一鍵式Edge Delivery服務(EDS)旨在自動化Cloud Manager中Edge Delivery網站的上線和部署。 它透過讓您按一下單一按鈕而大幅簡化程式。 按一下滑鼠即可布建必要的基礎架構、與GitHub整合以進行版本控制，以及在Google Drive中設定您的檔案和資產儲存空間。

此自動化功能有助於減少設定初始網站所需的人工作業。 它可確保順暢的工作流程、擴充能力，並提升團隊在邊緣管理內容的效能。

## 重要概念 {#key-concepts}

在您使用按一下Edge Delivery網站布建時的主要概念。

| 重要概念 | 說明 |
| --- | --- |
| 自動化Edge部署 | <ul><li>使用者可以立即布建及設定Edge Delivery網站。</li><li>使用Cloud Manager與CI/CD工作流程的整合，減少或免除手動上線流程的需求。</li><li>與Cloud Manager整合，提供順暢的CI/CD工作流程。</li></ul> |
| 與Cloud Manager整合 | <ul><li>使用Cloud Manager的使用者介面來觸發「一鍵式Edge Delivery」程式。</li><li>提供對自動化存放庫建立和部署的存取。</li></ul> |
| GitHub型版本控制 | <ul><li>使用預先定義的樣板範本，在組織內建立GitHub存放庫，將部署標準化。</li><li>AEM機器人內容更新的連結。</li></ul> |
| 檔案和資產儲存整合 | <ul><li>產生Google磁碟機資料夾以供儲存。<li>在存放庫上安裝AEM Code Sync應用程式，確保順暢的同步和部署。</li></li><li>允許多位共同作業人員輕鬆管理檔案。</li></ul> |
| 安全性與擴充性 | <ul><li>確保符合企業安全性標準。</li><li>支援不同Cloud Manager租使用者底下的多個Edge Delivery Sites。</li></ul> |



## 在Cloud Manager中布建Edge Delivery網站 {#provision-edge-delivery-site}

若要只需按一下即可布建Adobe Edge傳送網站，您的組織必須具備可用的Edge Delivery Services授權。 此授權是Adobe Experience Manager (AEM)的一部分，在Cloud Manager中布建Edge Delivery Services時是必要的。

在許可權方面，您必須是業務負責人角色的成員或已獲得適當的許可權，才能在Cloud Manager中新增或編輯計畫。 此存取層級可讓您管理Edge Delivery Services與程式中的整合。

另請參閱 [Cloud Manager 的 Edge Delivery Services 簡介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

自動內容更新必須先設定正確的AEM機器人設定？ 是真的嗎？ 假？

**若要在Cloud Manager中布建Edge Delivery網站：**

1. 在 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的程式。
1. 在頁面的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示左側功能表。
1. 在左側功能表的&#x200B;**服務**&#x200B;標題下，按一下![網頁圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery網站**。
1. 在Edge Delivery頁面的&#x200B;**Edge Delivery待辦事項清單**&#x200B;對話方塊的&#x200B;**完成必要條件**&#x200B;群組方塊中，按一下&#x200B;**布建**。
1. 在&#x200B;**布建Edge Delivery網站**&#x200B;對話方塊的&#x200B;**專案名稱**&#x200B;文字欄位中，輸入網站的名稱，然後按一下&#x200B;**布建**。
快顯通知會出現在畫面中央附近，通知您Edge Delivery網站布建已開始。
布建完成並驗證您的網站後，網站名稱會顯示在Edge Delivery頁面上的**Edge Delivery網站**&#x200B;區域中。

### 探索新布建的Edge Delivery網站




1. 按一下網站名稱右側的Git存放庫連結。

Publish。 按一下「網站名稱」，進行一些變更，然後發佈

在預覽中檢視頁面，然後變更URL以檢視即時版本。

新增共同作業人員。




## Publish與Edge Delivery網站



## 將共同作業人員新增至Edge Delivery網站


































這些增強功能旨在提高自動化、簡化設定流程，並增強 Edge Delivery Services 使用者的共同作業。 <!-- CMGR-59362 -->

請參閱「![佈建 Edge Delivery 網站](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)」。

![佈建 Edge Delivery 網站對話框](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)