---
title: Adobe Developer Console 中的 JWT 憑證已被取代
description: 了解 Adobe Developer Console 中已取代 JWT 憑證對 AEM 的影響。
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
feature: Security
role: Admin
source-git-commit: d3c00c33925a23ad5b1080c1e864cfdb5a8d1c1b
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 63%

---

# Adobe Developer Console 中的 JWT 憑證已被取代 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 客戶應參考 [AEM 6.5 的類似文件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console)以了解更多資訊。

Adobe 客戶使用 [Adobe Developer Console](https://developer.adobe.com/console) 來產生可存取各種 API 的憑證。客戶可以選擇各種憑證類型，包括 OAuth 伺服器到伺服器和單頁應用程式。其中一種憑證類型 (服務帳戶 (JWT) 憑證) 已被已取代，取而代之的是 OAuth 伺服器到伺服器憑證。2024 年 6 月 3 日或之後無法建立新的服務帳戶 (JWT) 憑證，現有的 JWT 憑證自 2025 年 1 月 27 日起將無法再使用。您可以[閱讀已取代項目的資訊](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文說明 AEM as a Cloud Service 應如何處理已取代項目的其他背景資訊。

主要要點是，AEM 現在支援 AEM as a Cloud Service 全新的 OAuth 伺服器對伺服器認證。您可能已收到一封電子郵件，內含要求您移轉 JWT 認證的指示，而現在可以完成這項移轉作業。

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

**動作**：將 JWT 認證移轉到 Cloud Manager 現在支援的 OAuth 認證。

**相關 AEM 版本**：AEM as a Cloud Service

客戶可建立 Adobe Developer Console 專案，以便叫用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。在已過時的 JWT 憑證於 2025 年 1 月到期之前，應將 Adobe Developer 專案中的憑證應移轉到 OAuth 伺服器到伺服器憑證類型。

## 自動產生的專案 {#autogen-projects}

**動作**：請勿移轉，因為 Adobe 將代表您進行移轉。

**相關 AEM 版本**：AEM as a Cloud Service。

當 Cloud Manager 佈建 AEM as a Cloud Service 環境時，它會自動產生具有 JWT 憑證的 Adobe Developer Console 專案。該專案會標記為唯讀，如以下螢幕截圖所示。客戶不能也不應嘗試將這些專案移轉到 OAuth 伺服器對伺服器認證。相反地，Adobe 會在認證無法繼續使用之前自行移轉這些專案。

![自動產生的專案](/help/security/assets/jwt-deprecation-autogen-projects.png)

## 自動產生的專案常見問題集 {#autogen-projects-faqs}

本節針對AEM as a Cloud Service中自動產生專案的JWT憑證淘汰，提供最常見問題的解答。

**我要如何自動產生哪些專案？**
導覽至Adobe Developer Console | 專案區段。  AEM as a Cloud Service自動產生的專案會有含有「自動產生」識別碼的鎖定圖示。  自動產生的專案會遵循AEM-p#####-e####格式，且由技術帳戶使用者建立。

<img width="439" alt="影像" src="https://git.corp.adobe.com/storage/user/16149/files/6b20a8a3-3711-4741-8f2c-ec5e36fe97cc">


**如果我們自動產生的專案發生問題，該怎麼辦？**

連絡[Adobe客戶服務](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。

**我應該移轉自動產生的專案嗎？**

不需要採取任何動作，因為Adobe會針對具有AEM發行說17258（2024年8月）及更新的環境移轉代表您自動產生的。

**移轉自動產生的專案的時間表為何？**

Adobe將於2025年第1季開始分階段移轉方法，從開發環境開始。

**如果我們的AEM版本比AEM版本17258本（2024年8月）舊，我們的AEM as a Cloud Service執行個體會受到什麼影響？**

如果自動產生的專案整合在2025年6月前未移轉至OAuth，系統將停止運作。

若要確保順利轉換，客戶應立即連絡[Adobe客戶服務](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)，並開始更新至[最新AEM版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/release-notes/maintenance/latest)的程式。 這將提供充足的時間進行回歸測試，並允許Adobe有效管理專案的移轉。

**我可以升級至支援的OAuth版本而不升級我的AEM as a Cloud Service AEM版本嗎？**

否。若要確保順利轉換，客戶應立即連絡[Adobe客戶服務](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)，並開始更新至[最新AEM版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/release-notes/maintenance/latest)的程式。 這將提供充足的時間進行回歸測試，並允許Adobe有效管理專案的移轉。
