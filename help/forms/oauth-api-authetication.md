---
title: 如何設定OAuth伺服器對伺服器驗證？
description: 瞭解如何為Adobe Experience Manager Forms as a Cloud Service設定OAuth伺服器對伺服器驗證
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: 6bd2e1698cceaf8fe47e19e0645d0782c916644a
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 3%

---


# OAuth伺服器對伺服器驗證

OAuth伺服器對伺服器驗證允許以權杖為基礎的安全存取AEM Forms Communications API，而不需要使用者互動。 Adobe Developer Console支援OAuth伺服器對伺服器驗證。

## 先決條件

開始之前，請確定符合下列必要條件：

* 確保您擁有[存取您使用環境專屬的Adobe Developer Console](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-manager/content/requirements/access-rights)的許可權。
* [在Adobe Admin Console中指派系統管理員或開發人員角色](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions)以啟用Adobe Developer Console的存取權。

## 如何使用OAuth伺服器對伺服器驗證產生存取權杖？

請依照下列步驟，從Adobe Developer主控台產生存取權杖，並透過OAuth伺服器對伺服器驗證發出第一個API呼叫。

### &#x200B;1. Adobe Developer Console專案設定

1. 導覽至[Adobe Developer Console](https://developer.adobe.com/console)
2. 使用您的Adobe ID登入

3. 建立新專案或導覽至您現有的專案

>[!BEGINTABS]

>[!TAB 若要建立新專案]

1. 在&#x200B;**快速入門**&#x200B;區段中，按一下&#x200B;**建立新專案**
2. 使用預設名稱建立新專案

   ![建立ADC專案](/help/forms/assets/adc-home.png)

3. 按一下右上角的&#x200B;**編輯專案**

   ![編輯專案](/help/forms/assets/adc-edit-project.png)

4. 提供有意義的名稱（例如「formsproject」）
5. 按一下「**儲存**」

   ![編輯專案名稱](/help/forms/assets/adc-edit-projectname.png)

>[!TAB 瀏覽至您現有的專案]

1. 從Adobe Developer Console按一下&#x200B;**所有專案**

   ![搜尋專案](/help/forms/assets/search-adc-project.png)

2. 找到您的專案，然後按一下以開啟。

   ![尋找專案](/help/forms/assets/locate-adc-project.png)

>[!ENDTABS]

### 2.新增Forms API

根據您想要做的以下工作新增Forms API：

* **AEM Forms Communications API**：需要產生、轉換、組合或保護檔案(PDF及相關格式)時使用。
* **Adaptive Forms Runtime API** — 在執行階段需要轉譯、提交或處理Adaptive Forms時使用。

>[!BEGINTABS]

>[!TAB 適用於AEM Forms Communications API的] 

1. 按一下&#x200B;**新增API**

   ![新增API](/help/forms/assets/adc-add-api.png)

2. 選取&#x200B;**Forms通訊API**
   1. 在&#x200B;_新增API_&#x200B;對話方塊中，依&#x200B;**Experience Cloud**&#x200B;篩選
   2. 選取&#x200B;**「Forms通訊API」**

      ![新增Forms通訊API](/help/forms/assets/adc-add-forms-api.png)

   3. 按一下「**下一步**」。
   4. 選取&#x200B;**OAuth伺服器對伺服器**&#x200B;驗證方法

      ![選取驗證方法](/help/forms/assets/adc-add-authentication-method.png)

>[!TAB 最適化Forms執行階段API的] 

1. **按一下[新增API]**

   ![新增API](/help/forms/assets/adc-add-api.png)

2. **選取AEM Forms傳遞和執行階段API**
   1. 在&#x200B;_新增API_&#x200B;對話方塊中，依&#x200B;**Experience Cloud**&#x200B;篩選
   2. 選取&#x200B;**「AEM Forms傳遞和執行階段API」**
      ![新增Forms通訊API](/help/forms/assets/adc-add-runtime-api.png)

   3. 按一下「**下一步**」。
   4. 選取&#x200B;**OAuth伺服器對伺服器**&#x200B;驗證方法。
      ![選取驗證方法](/help/forms/assets/adc-add-authentication-method.png)

>[!ENDTABS]

您也可以按一下&#x200B;**新增至專案** > **API**，將API和驗證方法新增至您現有的專案\
![新增API至現有的專案](/help/forms/assets/add-api-existing-project.png)

### 3.新增產品設定檔

產品設定檔提供存取AEM資源的憑證許可權（或授權）。

1. 選取符合您AEM執行個體URL (**)的**&#x200B;產品設定檔`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`。

   * **服務型別** — 指定與AEM執行個體關聯的服務或許可權

   * **環境型別** — 指定環境是用於作者或發佈服務

   * **方案XXX** — 識別Cloud Manager方案識別碼

   * **環境XXX** — 識別該程式中的特定環境ID

   >[!NOTE]
   >
   > 產品設定檔會繫結至特定的AEM執行個體（程式+環境）。 一律選擇符合執行個體URL的設定檔。

2. 按一下&#x200B;**「儲存已設定的 API」**。API和產品描述檔已新增到您的專案

   ![選取專案組態](/help/forms/assets/adc-add-product-profile.png)

### 4.產生並儲存認證

1. 在Adobe Developer Console中導覽至您的專案
2. 按一下&#x200B;**OAuth伺服器對伺服器**&#x200B;認證
3. 檢視&#x200B;**認證詳細資料**&#x200B;區段

   ![檢視認證](/help/forms/assets/adc-view-credential.png)

**記錄API認證**

```text
    API Credentials:
    ================
    Client ID: <your_client_id>
    Client Secret: <your_client_secret>
    Technical Account ID: <tech_account_id>
    Organization ID: <org_id>
    Scopes: AdobeID,openid,read_organizations
```

### 5.產生存取權杖

手動或以程式設計方式產生存取權杖：

>[!BEGINTABS]

>[!TAB 以進行測試]

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

>[!TAB 用於生產]

使用[Adobe IMS](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service) API以程式設計方式產生權杖：

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

>[!ENDTABS]

您現在可以使用產生的存取Token針對開發、預備或生產環境進行API呼叫。

>
>
> 若要進一步瞭解OAuth伺服器對伺服器實作，以產生存取權杖並進行API呼叫，[按一下這裡](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)。

## 最佳實務：管理開發、測試和生產的認證

* 請一律使用開發、測試和生產的個別認證。

* 將每個認證對應至正確的AEM環境URL。

* 安全地儲存秘密，並且絕不將其提交至原始檔控制。

* 追蹤存取權杖有效性，因為權杖僅在24小時內有效。

## 後續步驟

若要瞭解如何設定同步Forms通訊API的環境，請參閱[AEM Forms as a Cloud Service通訊同步處理](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)。


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


