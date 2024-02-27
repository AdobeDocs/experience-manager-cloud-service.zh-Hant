---
title: Adobe Developer主控台中的JWT憑證淘汰
description: 瞭解Adobe Developer主控台中JWT憑證的過時對AEM的影響
source-git-commit: e02e38a5267188111f0392a0a5c7b73e6a4f22b5
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Adobe Developer主控台中的JWT憑證淘汰 {#jwt-credentials-deprecation-in-adobe-developer-console}

客戶使用的Adobe [Adobe Developer Console](https://developer.adobe.com/console) 以產生可存取各種API的認證。 客戶可選取從OAuth伺服器對伺服器到單頁應用程式等各種認證型別。 其中一種認證型別，服務帳戶(JWT)認證，已遭取代而採用OAuth伺服器對伺服器認證。 2024年5月1日或之後無法建立新的服務帳戶(JWT)憑證，且現有的JWT憑證在2025年1月1日或之後將無法運作。 您可以 [閱讀有關淘汰資訊](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

本文提供有關AEMas a Cloud Service和AEM 6.5客戶應如何處理棄用的其他內容。

目前的主要收穫是AEM功能尚未支援新的OAuth伺服器對伺服器認證。 即將提供支援 — 在2024年4月中旬，透過AEMas a Cloud Service的AEM版本，以及針對AEM 6.5安裝的特殊相容性套件（如果您執行最新的Service Pack 20或以下版本，Service Pack 21及更高版本會自動包含）。 您可能已收到一封電子郵件，提供移轉JWT認證的說明，但請放心，您可以且應該延遲認證移轉，直到AEM支援新的OAuth伺服器對伺服器認證型別為止。

以下各節列出客戶在4月中旬獲得AEM支援後，必須（或在某些情況下不得）使用OAuth伺服器對伺服器憑證取代其服務帳戶(JWT)憑證的案例。 [瞭解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) 以在未來取代認證。

>[!NOTE]
>
>此 [**AEM** 開發人員主控台](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (請注意 **AEM** 在名稱中，以將其與 **Adobe** 開發人員主控台)提供用來產生 [JWT權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 用於伺服器對伺服器API。 這些認證並未遭到淘汰，可繼續使用。


## 將AEM與其他Adobe解決方案整合 {#integrating-aem-with-other-adobe-solutions}

**動作**：等候移轉，直到2024年4月中旬之後AEM支援。

**相關AEM版本**：AEMas a Cloud Service和AdobeManaged Services （Service Pack 20及以下版本）。


AEM客戶可使用AEM作者UI來設定與所有其他Adobe解決方案的整合。 例如Adobe Target、Adobe Analytics、Adobe Launch、AFCS等。

![將AEM與其他解決方案整合](/help/security/assets/jwt-deprecation.png)

舉例來說，以下是 [指示](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=en) 以設定與Adobe Target的整合。 中的API金鑰 [在AEM中完成IMS設定](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) 一節應移轉至OAuth伺服器對伺服器認證型別，一旦AEM在4月中旬支援這些認證。 這些指示將會在4月中旬更新，以幫助您套用新的OAuth伺服器對伺服器認證。

## Cloud Manager API {#cloud-manager-apis}

**動作**：等候移轉，直到2024年4月中旬之後AEM支援。

**相關AEM版本**：AEMas a Cloud Service和AdobeManaged Services （Service Pack 20及以下版本）。

客戶建立Adobe Developer主控台專案，以便叫用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). 在AEM和Cloud Manager支援後，Adobe Developer專案中的憑證應該移轉至OAuth伺服器對伺服器憑證型別。

## 自動產生的專案 {#autogen-projects}

**動作**：請勿移轉，因為Adobe會代表您移轉。

**相關AEM版本**：僅限AEMas a Cloud Service。

Cloud Manager布建AEMas a Cloud Service環境時，會自動產生具有JWT憑證的Adobe Developer主控台專案。 此專案標示為唯讀，如下方熒幕擷圖所示。 客戶不能也不應嘗試將這些專案移轉至OAuth伺服器對伺服器認證；Adobe將會在認證不再可用之前自行移轉這些專案。

![自動產生的專案](/help/security/assets/jwt-deprecation-autogen-projects.png)

