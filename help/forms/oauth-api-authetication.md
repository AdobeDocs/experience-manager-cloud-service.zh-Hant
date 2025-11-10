---
title: 如何設定OAuth伺服器對伺服器驗證？
description: 瞭解如何為Adobe Experience Manager Forms as a Cloud Service設定OAuth伺服器對伺服器驗證
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromToC: true
index: false
source-git-commit: 69704ca8de41c655b59ce6652a4a43b788ba75ec
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---


# OAuth伺服器對伺服器驗證 — 建議使用

OAuth伺服器對伺服器驗證允許以權杖為基礎的安全存取AEM Forms Communications API，而不需要使用者互動。 此方法適用於需要以程式設計方式驗證的自動化系統、後端服務和整合。

## 先決條件

開始之前，請確定符合下列必要條件：

* 確保您有權存取您使用環境專屬的[Adobe Developer Console](https://developer.adobe.com/console)。
* 在Adobe Admin Console中指派系統管理員或開發人員角色，以啟用Adobe Developer Console的存取權。

## 如何使用OAuth伺服器對伺服器驗證產生存取權杖？

請依照下列步驟操作，以說明如何從Adobe Developer主控台產生存取Token，並透過OAuth伺服器對伺服器驗證發出第一個API呼叫。


1. 導覽至[Adobe Developer Console](https://developer.adobe.com/console)
2. 使用您的Adobe ID登入

3. 建立新專案或導覽至您現有的專案

   **若要建立新專案：**

   1. 在&#x200B;**快速入門**&#x200B;區段中，按一下&#x200B;**建立新專案**
   2. 使用預設名稱建立新專案

      ![建立ADC專案](/help/forms/assets/adc-home.png)

   3. 按一下右上角的&#x200B;**編輯專案**

      ![編輯專案](/help/forms/assets/adc-edit-project.png)

   4. 提供有意義的名稱（例如「formsproject」）
   5. 按一下「**儲存**」

      ![編輯專案名稱](/help/forms/assets/adc-edit-projectname.png)


   **若要導覽至您現有的專案：**

   1. 從Adobe Developer Console按一下&#x200B;**所有專案**

      ![搜尋專案](/help/forms/assets/search-adc-project.png)

   2. 找到您的專案，然後按一下以開啟。

      ![尋找專案](/help/forms/assets/locate-adc-project.png)


      >[!NOTE]
      >
      > 您可以按一下&#x200B;**新增至專案** > **API**，將API和驗證方法新增至您現有的專案\
      > ![新增API至現有的專案](/help/forms/assets/add-api-existing-project.png)
      > 若要新增API和驗證方法，請針對現有專案執行以下所述的相同步驟。

4. 根據您的需求新增不同的AEM Forms Communications API。

   **A。針對Document Services API**

   1. 按一下&#x200B;**新增API**

      ![新增API](/help/forms/assets/adc-add-api.png)

   2. 選取&#x200B;**Forms通訊API**
      1. 在&#x200B;_新增API_&#x200B;對話方塊中，依&#x200B;**Experience Cloud**&#x200B;篩選
      2. 選取&#x200B;**「Forms通訊API」**

         ![新增Forms通訊API](/help/forms/assets/adc-add-forms-api.png)


   3. 選取&#x200B;**OAuth伺服器對伺服器**&#x200B;驗證方法

      ![選取驗證方法](/help/forms/assets/adc-add-authentication-method.png)


   **B。適用於Adaptive Forms Runtime API**

   1. **按一下[新增API]**
在您的專案中，按一下&#x200B;**新增API**&#x200B;按鈕

      ![新增API](/help/forms/assets/adc-add-api.png)

   2. **選取AEM Forms傳遞和執行階段API**
      1. 在&#x200B;_新增API_&#x200B;對話方塊中，依&#x200B;**Experience Cloud**&#x200B;篩選
      2. 選取&#x200B;**「AEM Forms傳遞和執行階段API」**
      3. 按一下「**下一步**」。

   3. **驗證方法**
選取&#x200B;**OAuth伺服器對伺服器**&#x200B;驗證方法。


      ![選取驗證方法](/help/forms/assets/adc-add-authentication-method.png)

5. **新增產品設定檔**：

   1. 根據所需的存取層級選取適當的&#x200B;**產品設定檔**：

      | 存取型別 | 產品設定檔 |
      |------------------|----------------------|
      | 唯讀存取權 | `AEM Users - author - Program XXX - Environment XXX` |
      | 讀取/寫入存取權 | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
      | 完整管理存取權 | `AEM Administrators - author - Program XXX - Environment XXX` |

   2. 選取符合作者服務URL (**)的**&#x200B;產品設定檔`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`。 例如：選取`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`。

   3. 按一下&#x200B;**「儲存已設定的 API」**。API和產品描述檔已新增到您的專案

      ![選取專案組態](/help/forms/assets/adc-add-product-profile.png)

6. 產生並儲存認證

   1. 在Adobe Developer Console中導覽至您的專案
   2. 按一下&#x200B;**OAuth伺服器對伺服器**&#x200B;認證
   3. 檢視&#x200B;**認證詳細資料**&#x200B;區段

      ![檢視認證](/help/forms/assets/adc-view-credential.png)

   4. 記錄API認證

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

7. 產生存取權杖

   **A。測試**

   在Adobe Developer Console中手動產生存取權杖：

   1. **瀏覽至您的專案**
      1. 在Adobe Developer Console中，開啟您的專案
      2. 按一下&#x200B;**OAuth伺服器對伺服器**

   2. **產生存取權杖**
      1. 按一下專案API區段中的&#x200B;**「產生存取權杖」**&#x200B;按鈕
      2. 複製產生的存取權杖

      ![產生存取權杖](/help/forms/assets/adc-access-token.png)

      >[!NOTE]
      >
      > 存取權杖僅對&#x200B;**24小時**&#x200B;有效

   **B。用於生產**

   使用Adobe IMS API以程式設計方式產生代號：

   **必要的認證：**

   * 用戶端 ID
   * 用戶端密碼
   * 範圍（通常： `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`）

   **權杖端點：**

   ```
   https://ims-na1.adobelogin.com/ims/token/v3
   ```

   **範例要求(curl)：**

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

您現在可以使用產生的存取Token針對開發、預備或生產環境進行API呼叫。

>[!NOTE]
>
> 若要進一步瞭解OAuth伺服器對伺服器實作，以產生存取權杖並進行API呼叫，[按一下這裡](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)。

## 後續步驟

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


