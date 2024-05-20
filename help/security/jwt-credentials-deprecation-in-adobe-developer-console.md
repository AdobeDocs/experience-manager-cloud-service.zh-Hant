---
title: Adobe Developer Console 中的 JWT 憑證已被取代
description: 了解 Adobe Developer Console 中已取代 JWT 憑證對 AEM 的影響。
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: b6e26ecaa73aaee37b6b824426dc0cd65d459502
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 62%

---

# Adobe Developer Console 中的 JWT 憑證已被取代 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 客戶應參考[本文](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console)，了解更多資訊。

Adobe 客戶使用 [Adobe Developer Console](https://developer.adobe.com/console) 來產生可存取各種 API 的憑證。客戶可以選擇各種憑證類型，包括 OAuth 伺服器到伺服器和單頁應用程式。其中一種憑證類型 (服務帳戶 (JWT) 憑證) 已被已取代，取而代之的是 OAuth 伺服器到伺服器憑證。2024 年 6 月 3 日或之後無法建立新的服務帳戶 (JWT) 憑證，現有的 JWT 憑證自 2025 年 1 月 27 日起將無法再使用。您可以[閱讀已取代項目的資訊](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文說明 AEM as a Cloud Service 應如何處理已取代項目的其他背景資訊。

主要成果是AEM現在支援AEMas a Cloud Service的新OAuth伺服器對伺服器認證。 您可能已收到一封電子郵件，提供移轉JWT憑證的說明，此移轉現在可以完成。

以下各節列出客戶必須（或在某些情況下不得）以OAuth伺服器對伺服器憑證取代其服務帳戶(JWT)憑證，現在AEM已支援這些憑證的案例。 [瞭解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) 以移轉認證。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (請注意名稱中的 **AEM**，其與 **Adobe** Developer Console 並不相同) 提供了一個公用程式來產生用於伺服器到伺服器 API 的 [JWT 權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。這些憑證並未被取代，可以繼續使用。

## 將 AEM 與其他 Adobe 解決方案整合 {#integrating-aem-with-other-adobe-solutions}

**動作**：移轉您的設定，因為AEM現在支援OAuth認證。

**相關 AEM 版本**：AEM as a Cloud Service

AEM客戶可使用AEM來設定與許多其他Adobe解決方案的整合。 例如，Adobe Target、Adobe Analytics和其他。

另請參閱 [為AEMas a Cloud Service設定IMS整合](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) 操作方式的詳細資訊：

* 使用OAuth憑證建立設定
* 移轉使用JWT認證建立的設定以使用OAuth認證

## Cloud Manager API {#cloud-manager-apis}

**動作**：確認這些憑證可何時從JWT移轉至OAuth憑證。

**相關 AEM 版本**：AEM as a Cloud Service

客戶可建立 Adobe Developer Console 專案，以便叫用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。在已過時的 JWT 憑證於 2025 年 1 月到期之前，應將 Adobe Developer 專案中的憑證應移轉到 OAuth 伺服器到伺服器憑證類型。

## 自動產生的專案 {#autogen-projects}

**動作**：請勿移轉，因為 Adob&#x200B;&#x200B;e 將代表您進行移轉。

**相關 AEM 版本**：AEM as a Cloud Service。

當 Cloud Manager 佈建 AEM as a Cloud Service 環境時，它會自動產生具有 JWT 憑證的 Adobe Developer Console 專案。該專案會標記為唯讀，如以下螢幕截圖所示。客戶不能也不應嘗試將這些專案移轉至OAuth伺服器對伺服器認證。 Adobe將會自行移轉這些專案，以免認證再使用。

![自動產生的專案](/help/security/assets/jwt-deprecation-autogen-projects.png)
