---
title: Dynatrace
description: 瞭解如何搭配AEMas a Cloud Service使用Dynatrace
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: a234f2a00c51bcb23b0c52feac9971259d26b8c3
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe功能可讓您使用Dynatrace在企業部署過程中監控AEMas a Cloud Service，找出任何潛在問題的原因，並視需要採取行動加以修正。

有了Dynatrace，您就可以順暢地觀察所有AEM應用程式。 Dynatrace可自動偵測您的AEM應用程式，並將其從網站到容器再到雲端服務的相依性視覺化，讓您全面掌握一般使用者體驗。 結合所有階層的端對端追蹤及「即時使用者監控」，將您的AEM內容導向體驗提升到全新的境界，不會出現空白或盲點。 如果有任何異常狀況發生，Dynatrace會使用Davis AI引擎即時診斷它們，並在客戶受到影響之前將根源歸結為程式碼中斷，藉此將平均修復時間縮到最短。

若要進一步瞭解Dynatrace，請參閱 [AdobeAEM Cloud Service整合](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![AEM作者和發佈者績效量度](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## 將Dynatrace與AEMas a Cloud Service整合 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatrace客戶可透過客戶支援票證請求連線，藉此監控其AEM環境。

連線要求所需的詳細資訊如下：

| **欄位** | **說明** |
|---|---|
| Dynatrace環境URL | 您的Dynatrace環境URL。<br><br>對於Dynatrace SaaS客戶，格式為 `https://<your-environment-id>.live.dynatrace.com`.<br><br>若為Dynatrace管理的客戶，格式為 `https://<your-managed-url>/e/<environmentId>` |
| Dynatrace環境ID | 您的Dynatrace環境ID。 請參閱 [取得Dynatrace環境資訊](#get-dynatrace-env-info) 以瞭解如何取得此內容。 |
| Dynatrace環境權杖 | 您的Dynatrace環境權杖。 請參閱 [取得Dynatrace環境資訊](#get-dynatrace-env-info) 以瞭解如何取得此內容。<br><br>這應視為秘密，因此請使用適當的安全實務。 例如，密碼可在網站中加以保護，例如 **zerobin.net**，客戶支援票證可參考以及密碼。 |
| Dynatrace API存取權杖 | Dynatrace環境的API存取Token。  請參閱 [建立Dynatrace API存取權杖](#create-dynatrace-access-token) 以瞭解如何建立此專案。<br><br>這應視為秘密，因此請使用適當的安全實務。 例如，密碼可在網站中加以保護，例如 **zerobin.net**，客戶支援票證可參考以及密碼。<br><br>注意：只有Dynatrace Managed才需要此專案。 |
| Dynatrace ActiveGate連線埠 | AEM整合應連線至您的Dynatrace ActiveGate連線埠。<br><br>注意：只有Dynatrace Managed才需要此專案。 |
| Dynatrace ActiveGate網路區域 | 您的 [Dynatrace ActiveGate網路區域](https://docs.dynatrace.com/docs/manage/network-zones) 在資料中心與網路區域間有效傳送AEM監控資料。<br><br>注意：Dynatrace ActiveGate網路區域是選用的。 |
| AEM環境ID | Dynatrace要監控的AEM環境ID。 |

>[!NOTE]
>
>Dynatrace整合後，資料將不再傳輸至其他APM工具，例如New Relic （若先前已啟用）。


## 建立Dynatrace API存取權杖 {#create-dynatrace-access-token}

1. 登入您的Dynatrace環境。
1. 在Dynatrace功能表中，前往「管理>存取權杖」 。
1. 選取「產生新Token」。
1. 定義權杖名稱。

1. 選用：設定到期日。 請務必在到期前產生新Token。
1. 將權杖範圍設定為PaaS整合 — 安裝程式下載
1. 選取「產生Token」。
1. 複製產生的存取權杖並將其儲存在安全位置。


## 取得Dynatrace環境資訊 {#get-dynatrace-env-info}

1. 對您的Dynatrace環境執行以下API請求：

`curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"`

取代\&lt;environmenturl> 搭配您的Dynatrace環境URL和\&lt;accesstoken> 以及您建立的API存取Token。

1. 複製\&lt;environmentid> 和\&lt;environmenttoken> 並將它們儲存在安全的地方。

```
{
   "tenantUUID": "<environmentId>",
   "tenantToken": "<environmentToken>",
   "communicationEndpoints": [
   ... 
   ],
   "formattedCommunicationEndpoints": "<endpoints>" 
}
```


