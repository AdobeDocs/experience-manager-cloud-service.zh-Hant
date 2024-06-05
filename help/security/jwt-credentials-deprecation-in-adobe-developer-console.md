---
title: Adobe Developer Console 中的 JWT 憑證已被取代
description: 了解 Adobe Developer Console 中已取代 JWT 憑證對 AEM 的影響。
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
feature: Security
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 93%

---

# Adobe Developer Console 中的 JWT 憑證已被取代 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 客戶應參考[本文](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console)，了解更多資訊。

Adobe 客戶使用 [Adobe Developer Console](https://developer.adobe.com/console) 來產生可存取各種 API 的憑證。客戶可以選擇各種憑證類型，包括 OAuth 伺服器到伺服器和單頁應用程式。其中一種憑證類型 (服務帳戶 (JWT) 憑證) 已被已取代，取而代之的是 OAuth 伺服器到伺服器憑證。2024 年 6 月 3 日或之後無法建立新的服務帳戶 (JWT) 憑證，現有的 JWT 憑證自 2025 年 1 月 27 日起將無法再使用。您可以[閱讀已取代項目的資訊](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文說明 AEM as a Cloud Service 應如何處理已取代項目的其他背景資訊。

主要要點是，AEM 現在支援 AEM as a Cloud Service 全新的 OAuth 伺服器對伺服器認證。您可能已收到一封電子郵件，提供移轉JWT憑證的說明，此移轉現在可以完成。

以下區段列出客戶必須 (或在某些情況下不得) 將其服務帳戶 (JWT) 認證取代為 OAuth 伺服器對伺服器認證的情境，目前 AEM 支援這些情境。[了解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)移轉認證。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (請注意名稱中的 **AEM**，其與 **Adobe** Developer Console 並不相同) 提供了一個公用程式來產生用於伺服器到伺服器 API 的 [JWT 權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。這些憑證並未被取代，可以繼續使用。

## 將 AEM 與其他 Adobe 解決方案整合 {#integrating-aem-with-other-adobe-solutions}

**動作**：移轉您的設定，因為 AEM 現在支援 OAuth 認證。

**相關 AEM 版本**：AEM as a Cloud Service

AEM 客戶使用 AEM 來設定所有與許多其他 Adobe 解決方案的整合。例如 Adobe Target、Adobe Analytics 等。

有關如何執行以下操作的詳細資訊，請參閱「[為 AEM as a Cloud Service 設定 IMS 整合](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md)」：

* 使用 OAuth 認證建立設定
* 將之前使用 JWT 認證建立的設定，移轉成使用 OAuth 認證

## Cloud Manager API {#cloud-manager-apis}

**動作**：將您的JWT憑證移轉至Cloud Manager現在支援的OAuth憑證。

**相關 AEM 版本**：AEM as a Cloud Service

客戶可建立 Adobe Developer Console 專案，以便叫用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。在已過時的 JWT 憑證於 2025 年 1 月到期之前，應將 Adobe Developer 專案中的憑證應移轉到 OAuth 伺服器到伺服器憑證類型。

## 自動產生的專案 {#autogen-projects}

**動作**：請勿移轉，因為 Adobe 將代表您進行移轉。

**相關 AEM 版本**：AEM as a Cloud Service。

當 Cloud Manager 佈建 AEM as a Cloud Service 環境時，它會自動產生具有 JWT 憑證的 Adobe Developer Console 專案。該專案會標記為唯讀，如以下螢幕截圖所示。客戶不能也不應嘗試將這些專案移轉到 OAuth 伺服器對伺服器認證。相反地，Adobe 會在認證無法繼續使用之前自行移轉這些專案。

![自動產生的專案](/help/security/assets/jwt-deprecation-autogen-projects.png)
