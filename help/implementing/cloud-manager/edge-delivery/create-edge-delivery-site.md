---
title: 一鍵式建立您的第一個 Edge Delivery Site
description: 了解如何透過點按按鈕，在 Cloud Manager 中快速建立 Edge Delivery Site。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 100%

---

# 一鍵式建立您的第一個 Edge Delivery Site{#about-one-click-edge-delivery-site}

一鍵式建立您的第一個 Edge Delivery Site 之功能，目的為協助您在 Cloud Manager 中自動完成 Edge Delivery Sites 上線和部署的工作。只需按一下按鈕即可，大幅簡化了流程。按一下即可佈建所需的基礎結構，與 GitHub 整合以進行版本控制，並在 Google Drive 中設定您的文件和資產儲存體。

這種自動化有助於減少設定初始網站所需的手動工作。這可確保無縫的工作流程和可擴縮性，並在管理 Edge 內容方面提高團隊的效能。

<!-- Check out this quick 2-minute video for a step-by-step walkthrough on creating your first Edge Delivery site—no hassle, just one click.

>[!VIDEO](https://video.tv.adobe.com/v/3458975?quality=12&learn=on) -->



<!--
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

若要一鍵式建立 Adobe Edge Delivery 網站，貴組織必須擁有可用的 Edge Delivery Services 授權。此授權屬於 Adob&#x200B;&#x200B;e Experience Manager (AEM) 的一部分，而且是在 Cloud Manager 中建立 Edge Delivery Services 所必需的。

就權限而言，您必須是「業務負責人」角色的成員或已獲授予適當的權限，才能在 Cloud Manager 中新增或編輯程式。此存取等級可讓您管理 Edge Delivery Services 與程式的整合。

另請參閱 [Cloud Manager 的 Edge Delivery Services 簡介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**若要在 Cloud Manager 中一鍵式建立 Edge Delivery 網站：**

1. 在 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的程式。
1. 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。
1. 於左側選單中，在「**方案**」標題下，按一下「**概觀**」。
1. 在&#x200B;**方案概觀**&#x200B;頁面上，按一下「**Edge Delivery**」索引標籤。
1. 在 Edge Delivery 頁面的「**Edge Delivery 待辦事項清單**」對話框中，在「**新增 Edge Delivery 網站**」群組方塊中按一下「**立即建立網站**」。
1. 在「**建立 Edge Delivery 網站**」對話框的「**專案名稱**」文字欄位中，輸入您的網站名稱，然後按一下「**立即建立網站**」。

   螢幕頂端中央附近會出現快顯通知，讓您知道 Edge Delivery 網站佈建已開始。

當 Cloud Manager 完成網站佈建與驗證後，在 Edge Delivery 頁面上的 **Edge Delivery 網站**&#x200B;清單方塊中會出現該&#x200B;**網站名稱** (您先前輸入的專案名稱)。此外，存放庫 URL 的左側會出現一個綠色核取記號。


### 探索一鍵式建立的 Edge Delivery 網站 {#explore-one-click-ed-site}

1. 在 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的程式。
1. 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。
1. 於左側選單中，在「**方案**」標題下，按一下「**概觀**」。
1. 在&#x200B;**方案概觀**&#x200B;頁面上，按一下「**Edge Delivery**」索引標籤。
1. 在 Edge Delivery 頁面上，執行下列任一項操作：

   | 探索內容 | 步驟 |
   | --- | --- |
   | 網站的 GitHub 存放庫 | <ul><li>在 **Edge Delivery 網站**&#x200B;清單方塊中，在「**存放庫**」欄位標題下，按一下方才建立之網站的 URL。<br>您可能必須使用您的使用者名稱或電子郵件和密碼登入 GitHub。</li> |
   | 發佈網站 | <ul><li> 在 **Edge Delivery 網站**&#x200B;清單方塊中，按一下網站名稱最右端的「![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)」圖示開啟下拉式選單。</li><li>按一下下拉式選單中的「![發佈核取圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg)**發佈網站**」。<br>會出現快顯通知訊息，讓您知道網站的發佈已成功開始。</li></ul> |
   | 預覽已發佈的網站 | <ul><li>在 **Edge Delivery 網站**&#x200B;清單方塊，在「**網站名稱**」欄位標題下，按一下方才建立並發佈之網站的 URL。<br>在瀏覽器的 URL 網址列中，請注意到網站的 URL 以「`.page`」結尾，表示您查看的是該網站的預覽內容。</li><li>若要查看上線的網站，請在 URL 網址列中手動將「`.page`」變更為「`.live`」。</li></ul> |
   | 授予使用者存取 Google Drive 上內容存放庫的權限 | <ul><li> 在 **Edge Delivery 網站**&#x200B;清單方塊中，按一下網站名稱最右端的「![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)」圖示開啟下拉式選單。</li><li>在下拉式選單中按一下「![新增使用者圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg)**取得內容存放庫的存取權**」。</li><li>在「**將共同作業者新增至您的網站**」對話框中，輸入投稿人的電子郵件，然後按一下![核取記號圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>視需要繼續新增投稿人的電子郵件。</li><li>輸入完畢後，按一下「**新增共同作業者**」。</li><li>若要與內容共同作業者共用連結，請在「**成功新增共同作業**」對話框中按一下「**確定**」。</li><li>在「成功新增共同作業」對話框中，按一下![複製圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)來複製連結並與您的共同作業者共用。<br>在共用連結之前，請確認共同作業者使用與其 IMS 帳戶關聯的電子郵件登入。若他們的 IMS 電子郵件帳戶無法使用，則必須使用以共同作業者身分加入時所用的電子郵件。這樣做可以確保共同作業者能存取連結，並且看得到 Google Drive 上所要編輯或更新的內容。</li><li>編輯完畢後，如上所述，在 Cloud Manager 中按一下「**發佈網站**」。<br>或者，如上所述，預覽所做的變更。</li></ul> |
   | 授予使用者存取 GitHub 上基底存放庫的權限 | <ul><li> 在 **Edge Delivery 網站**&#x200B;清單方塊中，按一下網站名稱最右端的「![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)」圖示開啟下拉式選單。</li><li>在下拉式選單中按一下「![程式碼圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg)**取得基底存放庫的存取權**」。</li><li>在「**存取您網站的基底存放庫**」對話框中，輸入共同作業者的 GitHub 使用者名稱，然後按一下![核取記號圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>視需要繼續新增 GitHub 使用者名稱。</li><li>輸入完畢後，按一下「**新增共同作業者**」。</li>使用者必須將存取權授予自己的 GitHub 使用者名稱，才能檢視存放庫。 |
