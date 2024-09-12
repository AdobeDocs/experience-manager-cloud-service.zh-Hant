---
title: 新增CDN設定
description: 瞭解如何為Edge Delivery網站或Cloud Manager環境新增CDN設定。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: 70f99cfb2cd00278d9ebbb7972ef455af7a87a1b
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 7%

---


# 新增內容傳遞網路設定 {#add-cdn}

若要將網域與計畫內Adobe管理的CDN上的SSL憑證連結，您必須新增CDN （內容傳遞網路）設定。

對於Adobe管理的CDN，使用DV憑證時，只允許具有ACME驗證的網站。

>[!IMPORTANT]
>
>您[是否已新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)和[是否已分別新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)？ 如果沒有，則必須先完成這兩個工作才能新增CDN設定。

**若要新增CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在左側導覽面板的&#x200B;**服務**&#x200B;下方，按一下&#x200B;**CDN設定**。

1. 在「CDN設定」頁面的右上角附近，按一下「**新增**」。

   ![設定CDN對話方塊](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. 在&#x200B;**設定CDN**&#x200B;對話方塊的&#x200B;**來源**&#x200B;下拉式清單中，選取下列其中一項：

   | 來源 | 說明 |
   | --- | --- |
   | Sites | 選取Edge Delivery網站。 |
   | 環境 | 選取您要在AEM設定中鎖定的特定Cloud Service環境。<br>在&#x200B;**第**&#x200B;層下拉式清單中，選取下列其中一項：<br>·選取&#x200B;**Publish**，將目標設定為內容傳送給使用者的即時生產環境。<br>·針對您要在變更上線前測試的測試或非生產環境，選取&#x200B;**預覽**。 |

1. 選擇下列其中一項，以選取您的CDN型別：

   | CDN型別 | 說明 |
   | --- | --- |
   | Adobe 管理的 CDN | a.在&#x200B;**網域**&#x200B;下拉式清單中，選取您要使用的網域名稱。<br>下拉式清單中沒有已驗證的網域嗎？ 請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。<br>b。在「SSL憑證」下拉式清單中，選取您要使用的憑證。<br>下拉式清單中沒有可用的SSL憑證嗎？ 請參閱[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 |
   | 其他CDN提供者。 | 如果您使用自己的CDN提供者，而不是Adobe管理的CDN，請選取此選項。<br>在&#x200B;**網域**&#x200B;下拉式清單中，選取您要使用的網域名稱。<br>下拉式清單中沒有可用的SSL憑證嗎？ 請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 |

1. 按一下「**儲存**」。
