---
title: 新增網域對應
description: 瞭解如何為Edge Delivery網站或Cloud Manager環境新增網域對應。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: 4935fbf5f0eb10f2f17280fb32f07d99f69eb875
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 5%

---


# 關於新增網域對應 {#add-domain-mapping}

若要將網域與計畫內Adobe管理的CDN上的SSL憑證連結，您必須新增CDN （內容傳遞網路）設定。

若是Adobe管理的CDN，使用DV SSL憑證時，只允許使用ACME驗證的網站。

>[!IMPORTANT]
>
>您[是否已新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)和[是否已分別新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)？ 如果沒有，則必須先完成這兩個工作才能新增CDN設定。

另請參閱[Adobe Managed CDN](https://www.aem.live/docs/byo-cdn-adobe-managed)。

**若要新增網域對應：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 根據您的使用案例，執行下列任一項作業：

   | 使用案例 | 步驟 |
   | --- | --- |
   | 我要將CDN設定新增至Cloud Manager中的&#x200B;*現有*&#x200B;個Edge Delivery網站 | a.在左側功能表的&#x200B;**服務**&#x200B;下方，按一下![網頁圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery網站**。<br>b。在Edge Delivery表格中，在沒有相關網域的資料列結尾按一下![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。<br>c。按一下&#x200B;**設定CDN**。 |
   | 我想要在Cloud Manager中新增CDN設定 | a.在左側功能表的&#x200B;**服務**&#x200B;下方，按一下![社交網路圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **網域對應**。<br>b。在「網域對應」頁面的右上角附近，按一下「**新增**」。 |

1. 在「**將網域對應至CDN**」對話方塊中，選取下列CDN型別之一：

   * **Adobe Managed CDN （建議）** — 此設定使用Adobe Managed CDN。 其中包括自動化設定與管理，以及內建的安全性功能。
   * **其他CDN提供者** — 此組態使用自我管理的CDN提供者網路。

1. 請根據上一步驟中所選的CDN型別，執行下列動作：

   * **Adobe Managed CDN**

     ![已選取Adobe管理的CDN選項按鈕的「將網域對應至CDN」對話方塊](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-adobe-managed.png)

      1. 在&#x200B;**來源**&#x200B;下拉式清單中，選取下列其中一項：

         | 來源下拉式清單 | 說明 |
         | --- | --- |
         | Sites | 選取Edge Delivery網站。 |
         | 環境 | 選取您要在AEM設定中鎖定的特定Cloud Service環境。<br>在&#x200B;**層**&#x200B;下拉式清單中，選取下列其中一項：<br>·選取&#x200B;**發佈**，將內容傳送至使用者的即時生產環境作為目標。<br>·針對您要在變更上線前測試的測試或非生產環境，選取&#x200B;**預覽**。 |

      1. 在&#x200B;**網域**&#x200B;下拉式清單中，選取您要使用的網域名稱。<br>下拉式清單中沒有已驗證的網域嗎？ 請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

      1. 在&#x200B;**SSL憑證**&#x200B;下拉式清單中，選取您要使用的憑證。<br>下拉式清單中沒有可用的SSL憑證嗎？ 請參閱[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

      1. 按一下&#x200B;**儲存**。

   * **其他CDN提供者**

     ![已選取Adobe管理的CDN選項按鈕的「將網域對應至CDN」對話方塊](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-other-provider.png)

     使用列出的設定步驟，在CDN中套用必要的設定並確認對應。 另請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

      1. 按一下&#x200B;**我已設定我的CDN**。

   <!-- OLD IMAGE/UI (/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)-->

   <!-- In the **Domain** field, enter the customer-facing hostname you want to serve (for example, `www.example.com`) -->

1. Adobe建議您測試網域對應。

## 測試網域對應 {#test-domain-mapping}

您可以確認Adobe管理的CDN上有新的網域對應正在運作，而不需要等候公用DNS傳輸。

執行覆寫DNS解析並直接指向CDN邊緣的&#x200B;**curl**&#x200B;命令：

```bash
curl -svo /dev/null https://www.example.com \
--resolve www.example.com:443:151.101.3.10
```

* 將`www.example.com`取代為您的網域。
* IP位址`151.101.3.10`是可用來存取AEM Cloud Service的IP之一。 另請參閱[APEX記錄](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-apex-record)。

`--resolve`旗標會強制要求傳送至指定的IP，而且只有在您網域的憑證和路由正確安裝之後，才會傳回成功。

