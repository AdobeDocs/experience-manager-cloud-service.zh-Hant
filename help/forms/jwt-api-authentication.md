---
title: 如何設定JWT （JSON Web權杖）驗證？
description: 瞭解如何為Adobe Experience Manager Forms as a Cloud Service設定JWT （JSON Web權杖）驗證
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
source-git-commit: 43b648eb3984867fda35ee04de10b78dd836b481
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 3%

---


# JWT （JSON Web權杖）伺服器對伺服器驗證

AEM Forms中的JWT伺服器對伺服器驗證，尤其是與AEM as a Cloud Service的伺服器端整合，涉及與AEM服務安全互動的特定程式。 AEM Developer Console支援JWT伺服器對伺服器驗證。

## 先決條件

開始之前，請確定符合下列必要條件：

* 確保您有權存取您使用環境專屬的[Adobe Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html)。
* 指派[系統管理員或開發人員角色以存取Adobe Cloud Manager](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-manager/content/requirements/access-rights)。

## 如何使用JWT憑證產生存取權杖？

請依照下列步驟操作，以示範如何從JWT憑證產生存取權杖。

1. **Adobe Cloud Manager**

   1. 登入您的[Cloud Manager帳戶](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html)。
   2. 在您選取的程式上，按一下&#x200B;**[!UICONTROL 程式概述]**。

      ![Cloud Manager帳戶](/help/forms/assets/jwt-cloud-manager-landing.png)

   3. 在您的程式中，按一下三點功能表，然後選取&#x200B;**[!UICONTROL Developer Console]**。

      ![開發人員控制台](/help/forms/assets/jwt-developer-console.png)

2. **AEM Developer Console**
   1. 登入AEM Developer Console
   2. 按一下位於上方功能表列上的&#x200B;**[!UICONTROL 整合]**。

      ![整合](/help/forms/assets/jwt-integrations.png)

   3. 按一下&#x200B;**[!UICONTROL 建立新的技術帳戶]**&#x200B;的選項。

      ![建立新的技術帳戶](/help/forms/assets/jwt-creae-new-tech-account.png)

   在您按一下建立新的技術帳戶後，就會產生存取權杖（例如使用者端ID和使用者端密碼）所需的資訊，以及其他技術帳戶資訊，包括私密金鑰、公開金鑰、到期日等。

   ![JWT認證](/help/forms/assets/jwt-credentials.png)


3. **產生並儲存認證**

   1. 記錄API認證

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

4. **產生存取權杖**

   使用cURL命令以程式設計方式產生權杖：

   **必要的認證：**

   * 用戶端 ID
   * 用戶端密碼
   * 範圍（通常： `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`）

   **權杖端點：**

   ```
   https://ims-na1.adobelogin.com/ims/token/v3
   ```

   **範例要求(cURL)：**

   ```bash
   curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
   -H 'Content-Type: application/x-www-form-urlencoded' \
   -d 'grant_type=client_credentials' \
   -d 'client_id=<YOUR_CLIENT_ID>' \
   -d 'client_secret=<YOUR_CLIENT_SECRET>' \
   -d 'scope=AdobeID,openid,read_organizations'
   ```

   **回應：**

   ```json
   {
   "access_token": "eyJhbGciOiJSUz...",
   "token_type": "bearer",
   "expires_in": 86399
   }
   ```


>[!NOTE]
>
> 若要進一步瞭解服務認證，以及如何使用Adobe IMS API產生存取權杖，[請按一下這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials)。

您現在可以使用產生的存取Token針對開發、預備或生產環境進行API呼叫。

## 相關文章

瞭解如何設定同步（隨選）和非同步（批次） Forms Communications API的環境：

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="同步API" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="同步API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms Communications API — 同步">AEM Forms Communications API — 同步</a>
                    </p>
                    <p class="is-size-6">瞭解如何設定同步（隨選） Forms Communications API的環境，以便立即產生或處理檔案。 </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解更多</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms Communications API — 非同步" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="非同步API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="非同步API">AEM Forms Communications API — 非同步（批次）</a>
                    </p>
                    <p class="is-size-6">瞭解如何為非同步（批次） Forms Communications API設定環境，以排程方式產生或處理多個檔案。</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解更多</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


>[!MORELIKETHIS]
>
>* [AEM Forms as a Cloud Service通訊簡介](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* 最適化AEM Forms和通訊API的[Forms as a Cloud Service架構](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通訊處理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通訊處理 — 批次API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Forms Communications API — 教學課程](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)