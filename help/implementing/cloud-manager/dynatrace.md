---
title: Dynatrace
description: 瞭解如何搭配AEM as a Cloud Service使用Dynatrace
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: 498a58c89910f41e6b86c5429629ec9282028987
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe可讓您在企業部署過程中使用Dynatrace來監控AEM as a Cloud Service，找出任何潛在問題的原因，並視需要採取行動加以修正。

有了Dynatrace，您就可以順暢地觀察所有AEM應用程式。 Dynatrace會探索您的AEM應用程式並顯示其從網站到容器再到雲端服務的路徑，以顯示使用者體驗。 結合所有階層的端對端追蹤及「即時監控」，將您的AEM內容導向體驗提升到全新的境界，不會出現漏洞或盲點。 如果發生異常，Dynatrace會使用Davis AI引擎即時診斷它們。 它會在客戶受到影響之前將根本原因歸結為程式碼損壞，將平均修復時間降至最低。

若要深入瞭解Dynatrace，請參閱[Adobe AEM雲端服務整合](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/)。

![AEM作者和發佈者績效量度](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## 將Dynatrace與AEM as a Cloud Service整合 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatrace客戶可透過客戶支援票證要求連線，藉此監控其AEM環境。

連線要求所需的詳細資訊如下：

| **欄位** | **說明** |
|---|---|
| [!DNL Dynatrace Environment URL] | 您的Dynatrace環境網址。<br><br>Dynatrace SaaS客戶的格式為`https://<your-environment-id>.live.dynatrace.com`。<br><br>對於Dynatrace Managed客戶，格式為`https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | 您的Dynatrace環境ID。 請參閱[如何取得我的Dynatrace連線詳細資料？](#how-do-i-get-my-dynatrace-connection-details)如何取得。 |
| [!DNL Dynatrace Environment Token] | 您的Dynatrace環境權杖。 請參閱[如何取得我的Dynatrace連線詳細資料？](#how-do-i-get-my-dynatrace-connection-details)如何取得。<br><br>此Token應視為秘密，因此請使用適當的安全性實務。 例如，密碼可在網站（例如&#x200B;**zerobin.net**，客戶支援票證可參照此網站）中保護此密碼以及密碼。 |
| [!DNL Dynatrace API access token] | 您Dynatrace環境的API存取Token。 請參閱[建立Dynatrace API存取Token](#create-dynatrace-access-token)，瞭解如何建立它。<br><br>此Token應視為機密，因此請使用適當的安全性實務。 例如，密碼可保護網站（例如&#x200B;**zerobin.net**，客戶支援票證可參照該網站）中的密碼及密碼。<br> |
| [!DNL Dynatrace ActiveGate Port] | AEM整合應連線至您的Dynatrace ActiveGate連線埠。<br><br>只有Dynatrace Managed才需要此連線埠。 |
| [!DNL Dynatrace ActiveGate Network Zone] | 您的[Dynatrace ActiveGate網路區域](https://docs.dynatrace.com/docs/manage/network-zones)可在資料中心和網路區域間有效路由AEM監控資料。<br><br>注意： Dynatrace ActiveGate網路區域是選用的。 |
| [!DNL AEM Environment IDs] | 供Dynatrace監視的一或多個AEM環境ID。 |

>[!NOTE]
>
>Dynatrace整合後，資料將不再傳輸至其他APM工具，例如New Relic （若之前已啟用）。

## 常見問題 {#faq}

### Dynatrace AEM監控需要哪個授權？ {#which-license-do-i-need-for-AEM-monitoring}

Dynatrace AEM監控需要Dynatrace授權。 Dynatrace AEM授權是以Kubernetes容器的[完整棧疊監視](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring)為基礎。 系統會自動偵測受監視的AEM容器（作者和發佈者服務）的記憶體大小。

根據AEM環境，Adobe部署規格為：

* 生產：平均4個容器，每個容器16 GB的記憶體
* 非生產：平均4個容器，每個8 GB記憶體

若要深入瞭解Dynatrace授權，請參閱[Dynatrace平台訂閱](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription)。

### 如何取得我的Dynatrace連線詳細資訊？ {#how-do-i-get-my-dynatrace-connection-details}

1. 對您的Dynatrace環境執行以下API請求：

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   將`<environmentUrl>`取代為您的Dynatrace環境URL，並將`<accessToken>`取代為您建立的API存取權杖。

1. 從回應承載中複製`<environmentId>`和`<environmentToken>`，並將其儲存在安全的地方。

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### 建立Dynatrace API存取權杖 {#create-dynatrace-access-token}

1. 登入您的Dynatrace環境。
1. 移至&#x200B;**[!DNL Access tokens]**，然後按一下選項&#x200B;**[!DNL Generate new token]**。
1. 定義[!DNL token name]。
1. 將權杖範圍設定為&#x200B;**[!DNL PaaS integration - Installer download]**。
1. 選取&#x200B;**[!DNL Generate token]**。
1. 複製產生的存取權杖並將其儲存在安全位置。





