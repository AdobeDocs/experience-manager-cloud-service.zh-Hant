---
title: 在Cloud Manager中建立Edge Delivery網站
description: 瞭解如何透過按一下按鈕在Cloud Manager中快速建立Edge Delivery網站。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1e4e07d2690bcbd44ffe994a571ffc0a8ae7eb50
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 30%

---


# 關於在Cloud Manager中建立Edge Delivery網站 {#about-one-click-edge-delivery-site}

建立Edge Delivery網站功能可協助您在Cloud Manager中自動上線和部署Edge Delivery網站。 只需按一下按鈕即可，大幅簡化了流程。按一下即可佈建所需的基礎結構，與 GitHub 整合以進行版本控制，並在 Google Drive 中設定您的文件和資產儲存體。

這種自動化有助於減少設定初始網站所需的手動工作。這可確保無縫的工作流程和可擴縮性，並在管理 Edge 內容方面提高團隊的效能。

## 重要概念 {#key-concepts}

按一下即可在Cloud Manager中建立Edge Delivery網站的主要概念。

| 重要概念 | 描述 |
| --- | --- |
| 自動化 Edge 部署 | <ul><li>使用者可即刻佈建和設定 Edge Delivery 網站。</li><li>透過使用Cloud Manager與CI/CD工作流程的整合，減少或免除手動上線流程。</li><li>已和 Cloud Manager 整合，實現無縫的 CI/CD 工作流程。</li></ul> |
| 與 Cloud Manager 的整合 | <ul><li>使用 Cloud Manager 的使用者介面來觸發一鍵式 Edge Delivery 流程。</li><li>提供自動存放庫建立和部署的存取權。</li></ul> |
| 根據 GitHub 的版本控制 | <ul><li>使用預先定義的 boilerplate 範本在組織內建立 GitHub 存放庫以標準化部署。</li><li>與 AEM Bot 連結以進行內容更新。</li></ul> |
| 文件和資產儲存體整合 | <ul><li>產生用於儲存體的 Google Drive 資料夾。<li>在存放庫上安裝 AEM Code Sync 應用程式，以確保無縫進行同步和部署。</li></li><li>共同作業人員可以輕鬆管理檔案。</li></ul> |
| 安全性和可擴縮性 | <ul><li>確保遵循企業安全性標準的規範。</li><li>支援不同Cloud Manager租使用者底下的多個Edge Delivery網站。</li></ul> |

<!-- >
## Practical use cases {#use-cases}

| Use case | Description |
| --- | --- |
| Website and application deployment | <ul><li>Automate the hosting and delivery of static or dynamic sites.</li><li>Ensure fast performance through edge caching. </li></ul> |
| API gateway and content delivery | <ul><li>Optimize API responses by caching data at the edge.</li><li>Reduce backend load and improved response times. </li></ul> |
| Real-time content updates | <ul><li>Instant deployment of new content across edge locations.</li><li>Support integration with automated content pipelines. </li></ul> |
| Edge computing workloads | <ul><li>Support serverless computing to process workloads closer to users.</li><li>Reduce latency and enhance performance. </li></ul> |
| Security and governance | <ul><li>Security is provided with integrated DDoS (Distributed Denial of Service) protection and WAF (Web Application Firewall) integration.</li><li>Ensure that content is delivered securely through TLS (Transport Security Layer) encryption. </li></ul> |
-->

## 在 Cloud Manager 中一鍵式建立 Edge Delivery 網站 {#one-click-edge-delivery-site}

若要按一下即可建立Adobe Edge Delivery網站，您的組織必須具備可用的Edge Delivery Services授權。 此授權屬於 Adob&#x200B;&#x200B;e Experience Manager (AEM) 的一部分，而且是在 Cloud Manager 中建立 Edge Delivery Services 所必需的。

就權限而言，您必須是「業務負責人」角色的成員或已獲授予適當的權限，才能在 Cloud Manager 中新增或編輯程式。此存取等級可讓您管理 Edge Delivery Services 與程式的整合。

另請參閱 [Cloud Manager 的 Edge Delivery Services 簡介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**若要在 Cloud Manager 中一鍵式建立 Edge Delivery 網站：**

1. 在 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的程式。
1. 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。
1. 在左側功能表的&#x200B;**方案**&#x200B;標題下，按一下&#x200B;**概觀**。
1. 在&#x200B;**計畫總覽**&#x200B;頁面上，按一下&#x200B;**Edge Delivery**&#x200B;標籤。
1. 在Edge Delivery頁面的&#x200B;**Edge Delivery待辦事項清單**&#x200B;對話方塊的&#x200B;**新增Edge Delivery網站**&#x200B;群組方塊中，按一下&#x200B;**立即建立網站**。
1. 在「**建立Edge Delivery網站**」對話方塊的「**專案名稱**」文字欄位中，輸入網站的名稱，然後按一下「**立即建立網站**」。

   快顯通知會出現在畫面中央附近，通知您Edge Delivery網站布建已開始。

當Cloud Manager完成網站布建和驗證時，**網站名稱** （您先前輸入的專案名稱）會顯示在Edge Delivery頁面的&#x200B;**Edge Delivery網站**&#x200B;清單方塊中。 此外，儲存區域URL左側會出現綠色核取記號。


### 探索一鍵建立的Edge Delivery網站 {#explore-one-click-ed-site}

1. 在 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的程式。
1. 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。
1. 在左側功能表的&#x200B;**方案**&#x200B;標題下，按一下&#x200B;**概觀**。
1. 在&#x200B;**計畫總覽**&#x200B;頁面上，按一下&#x200B;**Edge Delivery**&#x200B;標籤。
1. 在Edge Delivery頁面上，執行下列任一項作業：

   | 要探索的內容 | 步驟 |
   | --- | --- |
   | 網站的GitHub存放庫 | <ul><li>在&#x200B;**Edge Delivery網站**&#x200B;清單方塊的&#x200B;**存放庫**&#x200B;欄標題下，按一下您剛建立的網站URL。<br>您可能需要使用您的使用者名稱或電子郵件地址及密碼登入GitHub。</li> |
   | 發佈網站 | <ul><li> 在&#x200B;**Edge Delivery網站**&#x200B;清單方塊中，按一下網站名稱最右邊的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以開啟下拉式功能表。</li><li>在下拉式功能表中按一下![發佈檢查圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **發佈網站**。<br>會顯示快顯通知訊息，讓您知道已成功開始發佈網站。</li></ul> |
   | 預覽已發佈的網站 | <ul><li>在&#x200B;**Edge Delivery網站**&#x200B;清單方塊的&#x200B;**網站名稱**&#x200B;欄標題下，按一下您剛建立和發佈的網站URL。<br>在瀏覽器的URL位址列中，請注意，網站的URL結尾是`.page`，表示您看到網站預覽。</li><li>若要即時檢視網站，請在URL位址列中手動將`.page`變更為`.live`。</li></ul> |
   | 授予使用者存取Google Drive上內容存放庫的許可權 | <ul><li> 在&#x200B;**Edge Delivery網站**&#x200B;清單方塊中，按一下網站名稱最右邊的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以開啟下拉式功能表。</li><li>在下拉式功能表中按一下![使用者新增圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **取得內容存放庫的存取權**。</li><li>在&#x200B;**新增共同作業人員至您的網站**&#x200B;對話方塊中，輸入貢獻者的電子郵件地址，然後按一下![核取記號圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>視需要繼續新增投稿人電子郵件。</li><li>完成時，按一下&#x200B;**新增共同作業人員**。</li><li>若要與您的內容共同作業人員共用連結，請在&#x200B;**Collaboration成功新增**&#x200B;對話方塊中，按一下&#x200B;**確定**。</li><li>在Collaboration成功新增的對話方塊中，按一下![復製圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)以複製連結，並與您的共同作業人員共用。<br>共用連結前，請確認共同作業人員是以與其IMS帳戶相關聯的電子郵件地址登入。 如果無法取得IMS電子郵件帳戶，則必須使用新增為共同作業人員的電子郵件地址。 如此可確保共同作業人員能夠存取連結，並在Google Drive上檢視要編輯或更新之內容。</li><li>完成編輯後，按一下Cloud Manager中的&#x200B;**發佈網站**，如上所述。<br>或者，預覽所做的變更，如上所述。</li></ul> |
   | 授予使用者存取GitHub上基本存放庫的許可權 | <ul><li> 在&#x200B;**Edge Delivery網站**&#x200B;清單方塊中，按一下網站名稱最右邊的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以開啟下拉式功能表。</li><li>按一下下拉式功能表中的![程式碼圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **取得基本存放庫的存取權**。</li><li>在&#x200B;**存取您網站的基本存放庫**&#x200B;對話方塊中，輸入共同作業人員的GitHub使用者名稱，然後按一下![核取記號圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>視需要繼續新增GitHub使用者名稱。</li><li>完成時，按一下&#x200B;**新增共同作業人員**。</li>使用者必須授與存取權給自己的GitHub使用者名稱，才能檢視存放庫。 |


