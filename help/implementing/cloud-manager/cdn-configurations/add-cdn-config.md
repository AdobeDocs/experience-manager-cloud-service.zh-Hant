---
title: 新增CDN設定
description: 瞭解如何為Edge Delivery網站或Cloud Manager環境新增CDN設定。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: e57a6ceb2482e61acabe928da0f539d26989985c
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 8%

---


# 新增CDN設定 {#add-cdn}

必須完成新增CDN設定才能使用SSL設定網域。

>
>
>對於Adobe管理的CDN，使用DV憑證時，只允許具有ACME驗證的網站。

**若要新增CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下&#x200B;**CDN組態**。

1. 在「CDN設定」頁面的右上角附近，按一下「**新增**」。

   ![設定CDN對話方塊](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. 在&#x200B;**設定CDN**&#x200B;對話方塊中，提供必要資訊。

   * 從&#x200B;**Origin**&#x200B;下拉式清單中，執行下列任一項作業：
      * **網站：**&#x200B;選取Edge Delivery Services網站。
      * **環境：**&#x200B;選取Cloud Service環境。
         * **階層：**&#x200B;為選取的環境選取&#x200B;**Publish**&#x200B;或&#x200B;**預覽**&#x200B;網頁階層。
   * 選取您的CDN型別： **Adobe管理的CDN**&#x200B;或&#x200B;**其他CDN提供者**。
   * 選取網域。
   * 選取SSL憑證。 只有在您選取&#x200B;**Adobe管理的CDN**&#x200B;作為您的CDN型別時才需要。

1. 按一下「**儲存**」。




