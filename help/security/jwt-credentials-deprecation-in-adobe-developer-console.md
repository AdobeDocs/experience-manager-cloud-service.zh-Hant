---
title: Adobe Developer Console 中的 JWT 憑證已被取代
description: 了解 Adobe Developer Console 中已取代 JWT 憑證對 AEM 的影響
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: 484ad9721b1b9da95cf3966f139c0f11ff6ea473
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 71%

---

# Adobe Developer Console 中的 JWT 憑證已被取代 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 客戶應參考[本文](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html)，了解更多資訊。

Adobe 客戶使用 [Adobe Developer Console](https://developer.adobe.com/console) 來產生可存取各種 API 的憑證。客戶可以選擇各種憑證類型，包括 OAuth 伺服器到伺服器和單頁應用程式。其中一種憑證類型 (服務帳戶 (JWT) 憑證) 已被已取代，取而代之的是 OAuth 伺服器到伺服器憑證。2024年6月3日或之後無法建立新的服務帳戶(JWT)憑證，且現有的JWT憑證在2025年1月27日或之後將無法運作。 您可以[閱讀已取代項目的資訊](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文說明 AEM as a Cloud Service 應如何處理已取代項目的其他背景資訊。

目前的主要要點是 AEM 功能尚未支援新的 OAuth 伺服器到伺服器憑證。即將提供支援 — 透過AEMas a Cloud Service的AEM版本於2024年4月底提供。 您可能已收到說明移轉 JWT 憑證的電子郵件，但請放心，您可以而且應該推遲憑證移轉，直到 AEM 支援新的 OAuth 伺服器到伺服器憑證類型。

以下各節列出客戶必須（或在某些情況下不得）以OAuth伺服器對伺服器憑證取代其服務帳戶(JWT)憑證的案例，一旦AEM在4月底支援這些憑證即可。 [了解](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)將來更換憑證的方法。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (請注意名稱中的 **AEM**，其與 **Adobe** Developer Console 並不相同) 提供了一個公用程式來產生用於伺服器到伺服器 API 的 [JWT 權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。這些憑證並未被取代，可以繼續使用。


## 將 AEM 與其他 Adobe 解決方案整合 {#integrating-aem-with-other-adobe-solutions}

**動作**：等候移轉，直到2024年4月下旬AEM支援時（屆時將會更新本文）

**相關 AEM 版本**：AEM as a Cloud Service

AEM 客戶使用 AEM Author UI 設定所有與其他 Adobe 解決方案的整合。例如，Adobe Target、Adobe Analytics、Adobe Launch、AFCS 等。

![將 AEM 與其他解決方案整合](/help/security/assets/jwt-deprecation.png)

例如，以下是設定與 Adobe Target 整合的[說明](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=zh-Hant)。中的API金鑰 [在AEM中完成IMS設定](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) 四月底的AEM支援這些認證後，區段應該移轉至OAuth伺服器對伺服器認證型別。 這些指示將會在4月下旬更新，以幫助您套用新的OAuth伺服器對伺服器認證。

## Cloud Manager API {#cloud-manager-apis}

**動作**：請等候移轉，直到2024年4月下旬AEM支援後（屆時將會更新本文）。

**相關 AEM 版本**：AEM as a Cloud Service

客戶可建立 Adobe Developer Console 專案，以便叫用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。AEM 和 Cloud Manager 支援憑證後，Adobe Developer 專案中的憑證應移轉到 OAuth 伺服器到伺服器憑證類型。

## 自動產生的專案 {#autogen-projects}

**動作**：請勿移轉，因為 Adobe 將代您進行移轉。

**相關 AEM 版本**：AEM as a Cloud Service。

當 Cloud Manager 佈建 AEM as a Cloud Service 環境時，它會自動產生具有 JWT 憑證的 Adobe Developer Console 專案。該專案會標記為唯讀，如以下螢幕截圖所示。客戶不能也不應該嘗試將這些專案移轉到 OAuth 伺服器到伺服器憑證; Adobe 會在憑證失效前自行移轉這些專案。

![自動產生的專案](/help/security/assets/jwt-deprecation-autogen-projects.png)
