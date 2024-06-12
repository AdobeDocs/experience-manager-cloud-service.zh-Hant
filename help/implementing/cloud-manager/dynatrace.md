---
title: Dynatrace
description: 瞭解如何搭配AEMas a Cloud Service使用Dynatrace
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: 8d5d8910a906e2adf17fa9c75f17634602c2e0b9
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe可讓您在企業部署過程中使用Dynatrace來監控AEMas a Cloud Service，找出任何潛在問題的原因，並視需要採取行動加以修正。

有了Dynatrace，您就可以順暢地觀察所有AEM應用程式。 Dynatrace可自動偵測您的AEM應用程式，並將其從網站到容器再到雲端服務的相依性視覺化，進而全面掌握一般使用者體驗。 與所有層級的端對端追蹤和即時監控相結合，將您的AEM內容導向體驗提升到全新境界，不會出現空白或盲點。 如果有任何異常狀況發生，Dynatrace會使用Davis AI引擎即時診斷它們，並在客戶受到影響之前將根源歸結為程式碼中斷，藉此將平均修復時間縮到最短。

若要進一步瞭解Dynatrace，請參閱 [AdobeAEM Cloud Service整合](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![AEM作者和發佈者績效量度](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## 將Dynatrace與AEMas a Cloud Service整合 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatrace客戶可透過客戶支援票證要求連線，藉此監控其AEM環境。

連線要求所需的詳細資訊如下：

| **欄位** | **說明** |
|---|---|
| [!DNL Dynatrace Environment URL] | 您的Dynatrace環境網址。<br><br>對於Dynatrace SaaS客戶，格式為 `https://<your-environment-id>.live.dynatrace.com`.<br><br>若為Dynatrace管理客戶，格式為 `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | 您的Dynatrace環境ID。 請參閱 [如何取得我的Dynatrace連線詳細資訊？](#how-do-i-get-my-dynatrace-connection-details) 以瞭解如何取得此內容。 |
| [!DNL Dynatrace Environment Token] | 您的Dynatrace環境權杖。 請參閱 [如何取得我的Dynatrace連線詳細資訊？](#how-do-i-get-my-dynatrace-connection-details) 以瞭解如何取得此內容。<br><br>這應視為秘密，因此請使用適當的安全實務。 例如，密碼可在網站中加以保護，例如 **zerobin.net**，客戶支援票證可參考以及密碼。 |
| [!DNL Dynatrace API access token] | 您Dynatrace環境的API存取Token。  請參閱 [建立Dynatrace API存取權杖](#create-dynatrace-access-token) 以瞭解如何建立此專案。<br><br>這應視為秘密，因此請使用適當的安全實務。 例如，密碼可在網站中加以保護，例如 **zerobin.net**，客戶支援票證可參考以及密碼。<br><br>注意：只有Dynatrace Managed才需要此專案。 |
| [!DNL Dynatrace ActiveGate Port] | AEM整合應連線至您的Dynatrace ActiveGate連線埠。<br><br>注意：只有Dynatrace Managed才需要此專案。 |
| [!DNL Dynatrace ActiveGate Network Zone] | 您的 [Dynatrace ActiveGate網路區域](https://docs.dynatrace.com/docs/manage/network-zones) 在資料中心與網路區域間有效傳送AEM監控資料。<br><br>注意：Dynatrace ActiveGate網路區域為選用。 |
| [!DNL AEM Environment ID(s)] | Dynatrace要監控的AEM環境ID。 |

>[!NOTE]
>
>Dynatrace整合後，資料將不再傳輸至其他APM工具，例如New Relic （若先前已啟用）。

## 常見問題集 {#faq}

### Dynatrace AEM監控需要哪個授權？ {#which-license-do-i-need-for-AEM-monitoring}

Dynatrace AEM監視需要Dynatrace授權。 Dynatrace AEM授權是根據 [Kubernetes容器的完整棧疊監視](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring). 系統會自動偵測受監視的AEM容器（製作者和發佈者服務）的記憶體大小。

每個AEM環境的Adobe部署規格為：

* 生產：平均4個容器，每個容器16 GB的記憶體
* 非生產：平均4個容器，每個8 GB記憶體

若要進一步瞭解Dynatrace授權，請參閱 [Dynatrace平台訂閱](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription).

### 如何取得我的Dynatrace連線詳細資訊？ {#how-do-i-get-my-dynatrace-connection-details}

1. 對您的Dynatrace環境執行以下API請求：

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   取代 `<environmentUrl>` 使用您的Dynatrace環境URL和 `<accessToken>` 以及您建立的API存取Token。

1. 複製 `<environmentId>` 和 `<environmentToken>` 並將它們儲存在安全的地方。

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### 建立Dynatrace API存取權杖 {#create-dynatrace-access-token}

1. 登入您的Dynatrace環境。
1. 前往 **[!DNL Access tokens]** 並選取 **[!DNL Generate new token]**.
1. 定義 [!DNL token name].
1. 將權杖範圍設為 **[!DNL PaaS integration - Installer download]**.
1. 選取 **[!DNL Generate token]**.
1. 複製產生的存取權杖並將其儲存在安全位置。





