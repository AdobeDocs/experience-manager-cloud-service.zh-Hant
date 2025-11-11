---
title: 如何設定互動式通訊同步API？
description: 為Adobe Experience Manager Forms as a Cloud Service的互動式通訊同步API設定開發環境
role: Admin, Developer, User
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: cbf640e0c4643616638de96e9daa460cdcf2a4a5
workflow-type: tm+mt
source-wordcount: '2574'
ht-degree: 1%

---


# AEM Forms as a Cloud Service通訊同步API處理

本指南提供設定及使用AEM Forms Communications Synchronous API的完整指示。

瞭解如何使用OAuth伺服器對伺服器驗證來設定AEM as a Cloud Service環境、啟用API存取及叫用通訊API。

## 先決條件

若要設定執行和測試AEM Forms Communications API的環境，請確定您具備下列條件：

### 存取權和許可權

在開始設定Communications API之前，請確定您具有必要的存取許可權和許可權。

**使用者和角色許可權**

- 已在[https://account.adobe.com/](https://account.adobe.com/)建立Adobe ID
- 與您組織電子郵件相關聯的Adobe ID
- 已指派Adobe Managed Services產品內容
- 在Adobe Admin Console中指派的開發人員角色
- 在Adobe Developer Console中建立專案的許可權

>[!NOTE]
>
> 若要進一步瞭解指派角色和授與使用者存取權，請參閱文章[新增使用者和角色](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)。

**Cloud Manager存取權**

- [Cloud Manager](https://my.cloudmanager.adobe.com)的登入認證
- 存取以檢視和管理您的方案環境
- 建立和執行CI/CD管道的許可權
- 存取環境詳細資料和設定

**Git存放庫存取權**

- 存取Cloud Manager Git存放庫
- 用於複製和推送變更的Git憑證

### 開發工具

- **Node.js**&#x200B;以執行範例應用程式
- 最新版本的&#x200B;**Git**
- 存取&#x200B;**終端機/命令列**
- 用於編輯組態檔（VS程式碼、IntelliJ等）的&#x200B;**文字編輯器或IDE**
- 用於API測試的&#x200B;**Postman**&#x200B;或類似的工具

>[!NOTE]
>
> 這是每個環境的一次性流程，在繼續進行AEM Forms Communications API設定之前必須先完成。

現在，讓我們詳細瞭解每個步驟。

### 步驟1：更新AEM執行個體

若要更新AEM執行個體：

1. **登入Adobe Cloud Manager**
   1. 瀏覽至[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
   2. 使用您的Adobe ID登入

2. **瀏覽至計畫總覽**
   1. 從清單中選取您的計畫。 系統會將您重新導向至方案概觀頁面

3. **尋找環境詳細資料**
   1. 選取環境名稱旁的`ellipsis`(...)圖示，然後按一下&#x200B;**更新**
   2. 按一下&#x200B;**提交**&#x200B;按鈕，然後執行建議的完整棧疊管道。

      ![更新環境](/help/forms/assets/update-env.png)

### 步驟2：複製Git存放庫

複製Cloud Manager Git存放庫以管理您的API設定檔案。

1. **找到存放庫區段**
   1. 在&#x200B;**計畫總覽**&#x200B;頁面上，按一下&#x200B;**存放庫**&#x200B;索引標籤
   2. 找到存放庫名稱，然後按一下省略符號選單(...)
   3. 複製存放庫URL

      >[!NOTE]
      >
      > URL格式通常是`https://git.cloudmanager.adobe.com/<org>/<program>/`

2. 使用Git命令&#x200B;**複製**

   1. 開啟命令提示或終端機
   2. 執行`git clone`命令以複製Git存放庫。

      ```bash
      git clone [repository-url]
      ```

      >[!NOTE]
      >
      > 若要複製Git存放庫，請使用Adobe Cloud Manager提供的憑證。

      例如，若要複製Git存放庫，請執行以下命令：

      ```bash
      https://git.cloudmanager.adobe.com/formsinternal01/AEMFormsInternal-ReleaseSanity-p43162-uk59167/
      ```

      ![克隆Git存放庫](/help/forms/assets/repo-clone.png)


**Git存放庫整合選項**

Adobe Cloud Manager支援兩種存放庫選項：

- **直接使用Cloud Manager的Git存放庫**
   - 使用Cloud Manager的原生Git存放庫
   - 內建與管道的整合

- **與客戶管理的Git存放庫整合**
   - 連線您自己的Git存放庫（GitHub、GitLab、Bitbucket等）
   - 設定與Adobe Cloud Manager的同步

若要進一步瞭解如何整合Adobe Cloud Manager與Adobe Cloud Manager，請參閱[Git整合檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html)。

### 步驟3：存取AEM雲端服務環境和AEM Forms端點

存取您的AEM Cloud Service環境詳細資訊，以取得API設定所需的URL和識別碼。

1. **登入Adobe Cloud Manager**
   1. 瀏覽至[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
   2. 使用您的Adobe ID登入

2. **瀏覽至計畫總覽**
從清單中選取您的計畫。 系統會將您重新導向至方案概觀頁面

3. **存取及檢視AEM雲端服務環境**

   您可以使用以下兩個選項之一，檢視或存取AEM雲端服務環境詳細資訊：

   - **選項1：從概觀頁面**

      1. 在&#x200B;**計畫總覽**&#x200B;頁面
      2. 按一下左側功能表中的&#x200B;**「環境」**。  您可以檢視所有環境的清單

         ![檢視所有環境](/help/forms/assets/all-env.png)

      3. 按一下特定環境名稱以檢視詳細資訊

         ![選項1 — 環境詳細資料](/help/forms/assets/option1-env.png)

   - **選項2：來自環境區段**

      1. 在計畫總覽頁面
      2. 找到&#x200B;**環境**&#x200B;區段
      3. 按一下&#x200B;**「全部顯示」**&#x200B;以檢視所有環境
      4. 按一下環境旁的&#x200B;**省略符號選單(...)**
         ![選項1 — 環境詳細資料](/help/forms/assets/option2-env-details.png)
      5. 選取&#x200B;**「檢視詳細資料」**

         ![選項1 — 環境詳細資料](/help/forms/assets/option1-env.png)

4. **尋找您的AEM Forms端點**

   從&#x200B;**環境**&#x200B;詳細資訊頁面，請注意下列詳細資訊：

   **作者服務URL**

   - URL： `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`
   - 貯體：author-pXXXXX-eYYYY
範例： `https://author-p43162-e177398.adobeaemcloud.com`

   **發佈服務URL**

   - URL： `https://publish-pXXXXX-eYYYYY.adobeaemcloud.com`
   - 貯體：publish-pXXXXX-eYYYY
範例： `https://publish-author-p43162-e177398.adobeaemcloud.com`

>[!NOTE]
>
> 若要瞭解如何存取AEM雲端服務環境和AEM Forms端點，請參閱[管理環境檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html)。

### 步驟4： API存取設定

執行以下步驟來設定AEM Forms Communications API：

#### 4.1 Adobe Developer Console專案設定

1. **存取Adobe Developer Console**
   1. 導覽至[Adobe Developer Console](https://developer.adobe.com/console)
   2. 使用您的Adobe ID登入

2. **建立新專案**
   1. 在&#x200B;**快速入門**&#x200B;區段中，按一下&#x200B;**建立新專案**
   2. 使用預設名稱建立新專案

      ![建立ADC專案](/help/forms/assets/adc-home.png)

   3. 按一下右上角的&#x200B;**編輯專案**

      ![編輯專案](/help/forms/assets/adc-edit-project.png)

   4. 提供有意義的名稱（例如「formsproject」）
   5. 按一下「**儲存**」

      ![編輯專案名稱](/help/forms/assets/adc-edit-projectname.png)

#### 4.2新增Forms通訊API

您可以根據需求新增不同的AEM Forms Communications API。

**A。針對Document Services API**

1. 按一下&#x200B;**新增API**

   ![新增API](/help/forms/assets/adc-add-api.png)

2. 選取&#x200B;**Forms通訊API**
   1. 在&#x200B;_新增API_&#x200B;對話方塊中，依&#x200B;**Experience Cloud**&#x200B;篩選
   2. 選取&#x200B;**「Forms通訊API」**

   ![新增Forms通訊API](/help/forms/assets/adc-add-forms-api.png)


3. 選取&#x200B;**OAuth伺服器對伺服器**&#x200B;驗證方法

   ![選取驗證方法](/help/forms/assets/adc-add-authentication-method.png)

**B。適用於Forms執行階段API**

1. **按一下[新增API]**
   - 在您的專案中，按一下&#x200B;**新增API**&#x200B;按鈕

   ![新增API](/help/forms/assets/adc-add-api.png)

2. **選取AEM Forms傳遞和執行階段API**
   - 在&#x200B;_新增API_&#x200B;對話方塊中，依&#x200B;**Experience Cloud**&#x200B;篩選
   - 選取&#x200B;**「AEM Forms傳遞和執行階段API」**
   - 按一下「**下一步**」。

   ![新增執行階段API](/help/forms/assets/add-runtime-api.png)


3. **驗證方法**
   - 選取&#x200B;**OAuth伺服器對伺服器**&#x200B;驗證方法。


   ![選取驗證方法](/help/forms/assets/add-authentication-for-runtime-apis.png)

#### 4.3新增產品設定檔

請依照下列步驟新增產品設定檔：

1. 根據所需的存取層級選取適當的&#x200B;**產品設定檔**：

   | 存取型別 | 產品設定檔 |
   |------------------|----------------------|
   | 唯讀存取權 | `AEM Users - author - Program XXX - Environment XXX` |
   | 讀取/寫入存取權 | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
   | 完整管理存取權 | `AEM Administrators - author - Program XXX - Environment XXX` |

2. 選取符合作者服務URL (**)的**&#x200B;產品設定檔`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`。 例如：選取`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`。

3. 按一下&#x200B;**「儲存已設定的 API」**。API和產品描述檔已新增到您的專案

   ![選取專案組態](/help/forms/assets/adc-add-product-profile.png)

#### 4.4產生並儲存認證

1. **存取您的認證**

   1. 在Adobe Developer Console中導覽至您的專案
   2. 按一下&#x200B;**OAuth伺服器對伺服器**&#x200B;認證
   3. 檢視&#x200B;**認證詳細資料**&#x200B;區段

   ![檢視認證](/help/forms/assets/adc-view-credential.png)

2. **記錄API認證**

   ```text
   API Credentials:
   ================
   Client ID: <your_client_id>
   Client Secret: <your_client_secret>
   Technical Account ID: <tech_account_id>
   Organization ID: <org_id>
   Scopes: AdobeID,openid,read_organizations
   ```

#### 4.5存取Token產生

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
   > 存取權杖的有效期限為&#x200B;**24小時**

**B。用於生產**

使用Adobe IMS API以程式設計方式產生代號：

**必要的認證：**

- 用戶端 ID
- 用戶端密碼
- 範圍（通常： `AdobeID,openid,read_organizations`）

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

#### 4.6向AEM環境註冊使用者端ID

若要讓ADC專案的使用者端ID能夠與AEM執行個體通訊，您必須使用YAML設定檔案進行註冊，並透過設定管道進行部署。

1. **尋找或建立設定目錄**

   1. 導覽至複製的AEM專案存放庫，然後導覽至`config`資料夾
   2. 如果該檔案不存在，請在專案根層級建立：

   ```bash
   mkdir config
   ```

2. 在`api.yaml`目錄中建立名為`config`的新檔案：

   ```bash
   touch config/api.yaml
   ```

3. 在`api.yaml`檔案中新增下列程式碼：

   ```yaml
   kind: "API"
   version: "1"
   metadata:
   envTypes: ["dev"]  # or ["prod", "stage"] for production environments
   data:
   allowedClientIDs:
       author:
       - "<your_client_id>"
       publish:
       - "<your_client_id>"
       preview:
       - "<your_client_id>"
   ```

   以下說明組態引數：

   - **kind**：一律設為`"API"` （將此識別為API設定）
   - **版本**： API版本，通常是`"1"`或`"1.0"`
   - **envTypes**：套用此設定的環境型別陣列
      - `["dev"]` — 僅開發環境
      - `["stage"]` — 僅暫存環境
      - `["prod"]` — 僅生產環境
   - **allowedClientIDs**：允許使用者端ID存取您的AEM執行個體
      - **作者**：作者層的使用者端ID
      - **發佈**：發佈層級的使用者端ID
      - **預覽**：預覽層的使用者端ID

   例如，將`allowedClientIDs`新增為`6bc4589785e246eda29a545d3ca55980`，並將envTypes新增為`dev`：

   ![正在新增設定檔](/help/forms/assets/create-api-yaml-file.png)

4. **認可和推播變更**

   1. 導覽至您克隆的存放庫的根資料夾，然後執行下列命令：


   ```bash
       git add config/api.yaml
       git commit -m "Whitelist client id for api invocation"
       git push origin <your-branch>
   ```

   ![推播Git變更](/help/forms/assets/push-yaml-changes-in-git.png)


5. **安裝設定管道**

   1. **登入Cloud Manager**
      1. 瀏覽至[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
      2. 使用您的Adobe ID登入

   2. **瀏覽至您的程式**
從清單中選取您的方案，系統就會將您重新導向方案概觀頁面

   3. **找到管道卡**
      1. 在計畫總覽頁面上找到&#x200B;**管道**&#x200B;卡
      1. 按一下&#x200B;**「新增」**&#x200B;按鈕

   4. **選取管道型別**

      - **適用於開發環境**：選取&#x200B;**「新增非生產管道」**。 非生產管道適用於開發和測試環境

      - **針對生產環境**：選取&#x200B;**「新增生產管道」**。 生產管道需要其他核准

        >[!NOTE]
        >
        > 在這種情況下，請建立非生產管道，因為開發環境可供使用。

   5. **設定管道 — 設定索引標籤**

      在&#x200B;**組態**&#x200B;索引標籤中：

      a. **管線型別**
      - 選取&#x200B;**「部署管道」**

      b. **管道名稱**
      - 提供描述性名稱，例如，將管道命名為`api-config-pipieline`

      c. **部署觸發程式**
      - **手動**：僅在手動觸發時部署（建議用於初始設定）
      - **在Git變更上**：將變更推送至分支時自動部署

      d. **重要量度失敗行為**
      - **每次都詢問**：失敗時提示動作（預設）
      - **立即失敗**：在量度失敗時自動讓管道失敗
      - **立即繼續**：失敗仍繼續

      e.按一下&#x200B;**「繼續」**&#x200B;以繼續前往&#x200B;**Source程式碼**&#x200B;標籤

      ![設定管道](/help/forms/assets/add-config-pipeline.png)

   6. **設定Pipeline - Source程式碼標籤**

      在&#x200B;**Source程式碼**&#x200B;索引標籤中：

      a. **部署型別**
      - 選取&#x200B;**「目標部署」**

      b. **部署選項**
      - 選取&#x200B;**「設定」** （僅部署設定檔）。 它會告訴Cloud Manager這是設定部署。

      c. **選取合格的部署環境**
      - 選擇您要部署設定的環境。 在此案例中，它是`dev`環境。

      d. **定義Source程式碼詳細資料**

      - **存放庫**：選取包含您`api.yaml`檔案的存放庫。 例如，選取`AEMFormsInternal-ReleaseSanity-p43162-uk59167`存放庫。
      - **Git分支**：選取您的分支。 例如，在此案例中，我們的程式碼部署在`main`分支。
      - **程式碼位置**：輸入`config`目錄的路徑。 由於`api.yaml`位於根目錄的`config`資料夾中，所以請輸入`/config`

      e.按一下&#x200B;**「儲存」**&#x200B;以建立管道

      ![設定管道](/help/forms/assets/confirm-pipeline-1.png)

6. **部署組態**

   現在管道已建立，請部署您的`api.yaml`設定：

   1. 從管道總覽&#x200B;**&#x200B;**
      1. 在方案總覽頁面上，找到&#x200B;**管道**&#x200B;卡片
      2. 瀏覽至清單中新建立的設定管道。 例如，尋找您建立的管道名稱（例如「api-config-pipeline」）。 您可以檢視管道詳細資訊，包括狀態和上次執行。

   2. **開始部署**
      1. 按一下您的管道旁的&#x200B;**「建置」**&#x200B;按鈕（或播放圖示▶）
      2. 如果出現提示且管道執行開始，則確認部署

      ![執行管道](/help/forms/assets/run-config-pipeline.png)

   3. **驗證部署成功**
      - 等待管道完成。
         - 如果成功，狀態會變更為「成功」（綠色核取記號✓）。
         - 如果失敗，狀態會變更為「失敗」（紅十字✗）。 按一下&#x200B;**下載記錄檔**&#x200B;以檢視錯誤詳細資料。

           ![管道成功](/help/forms/assets/pipeline-suceess.png)

      現在，您可以開始測試Forms Communications API。 為了測試目的，您可以使用Postman、curl或任何其他REST使用者端來叫用API。

### 步驟5：API規格和測試

現在您的環境已設定完畢，您可以使用[Swagger UI](#a-using-swagger-ui-for-api-testing)或以程式設計方式開發NodeJS應用程式，以開始測試AEM Forms Communication API。

在此範例中，讓我們使用範本和XDP檔案，透過檔案服務API來產生PDF。

#### A.使用Swagger UI進行API測試

Swagger UI提供互動式介面來測試API，而不需撰寫程式碼。請使用&#x200B;**嘗試它**&#x200B;功能來叫用及測試[產生PDF](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) Document Service API。

1. 導覽至API檔案
   - Forms API： [Forms API參考](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
   - 檔案服務： [檔案服務API參考](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
在瀏覽器中，開啟[Document Services API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document)檔案。
2. 展開&#x200B;**Document Generation**&#x200B;區段並選取[從XDP或PDF範本產生可填寫的PDF表單，可選擇合併資料](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm)。
3. 在右窗格中，按一下&#x200B;**試用**。

   ![API的Swagger測試](/help/forms/assets/api-doc-generation.png)
4. 輸入下列值：

   | **節** | **引數** | **值** |
   |--------------|---------------|------------|
   | 貯體 | AEM執行個體 | 不含AEM網域名稱(`.adobeaemcloud.com`)的Adobe執行個體名稱例如，使用`p43162-e177398`做為貯體。 |
   | 安全性 | 持有人權杖 | 使用Adobe Developer Console專案的OAuth伺服器對伺服器認證中的存取權杖 |
   | 內文 | 範本 | 上傳XDP以產生PDF表單。 例如，您可以使用此[XDP](/help/forms/assets/ClosingForm.xdp)來產生PDF。 |
   | 內文 | 資料 | 選用的XML檔案，其中包含要與範本合併的資料，以產生預先填入的PDF表單。 例如，您可以使用此[XML](/help/forms/assets/ClosingForm.xml)來產生PDF。 |
   | 參數 | X-Adobe-Accept-Experimental | 1 |

5. 按一下&#x200B;**傳送**&#x200B;以叫用API

   ![傳送API](/help/forms/assets/api-send.png)

6. 檢查&#x200B;**回應**&#x200B;標籤中的回應：
   - 如果回應代碼為`200`，表示已成功建立PDF。
   - 如果回應代碼為`400`，表示要求引數無效或格式錯誤。
   - 如果回應代碼為`500`，表示存在內部伺服器錯誤。

   在此案例中，回應代碼為`200`，這表示已成功產生PDF：

   ![檢閱回應](/help/forms/assets/api-success.png)

   現在，您可以使用[下載](/help/forms/assets/create-pdf.pdf)按鈕下載&#x200B;**已建立的PDF**，並在PDF檢視器中檢視它：

   ![檢視PDF](/help/forms/assets/create-pdf.png)

>[!NOTE]
>
> 為了測試目的，您也可以使用[Postman](https://www.postman.com/)、[curl](https://curl.se/)或任何其他REST使用者端來叫用AEM API。

#### B.以程式設計方式開發NodeJS應用程式

開發Node.js應用程式，以使用&#x200B;**Document Services API**&#x200B;從&#x200B;**XDP**&#x200B;範本和&#x200B;**XML**&#x200B;資料檔產生可填寫的PDF表單

##### 先決條件

- 系統上已安裝的Node.js
- 作用中的AEM as a Cloud Service執行個體
- 來自Adobe Developer Console的API驗證持有人權杖
- 範例XDP檔案： [ClosingForm.xdp](/help/forms/assets/ClosingForm.xdp)
- 範例XML檔案： [ClosingForm.xml](/help/forms/assets/ClosingForm.xml)

若要開發Node.js應用程式，請遵循逐步開發步驟：

##### 步驟1：建立新的Node.js專案

開啟cmd/終端機並執行以下命令：

```bash
# Create a new directory
mkdir demo-nodejs-generate-pdf
cd demo-nodejs-generate-pdf

##### Initialize Node.js project
npm init -y
```

![建立新節點js專案](/help/forms/assets/api-1.png)

##### 步驟2：安裝必要的相依性

安裝&#x200B;**node-fetch**、**dotenv**&#x200B;和&#x200B;**form-data**&#x200B;程式庫，以分別發出HTTP要求、讀取環境變數及處理表單資料。

```bash
npm install node-fetch
npm install dotenv
npm install form-data
```

![安裝npm相依性](/help/forms/assets/api-2.png)

##### 步驟3：更新package.json

1. 開啟cmd/終端機並執行命令：

   ```bash
   code .
   ```

   ![在編輯器中開啟專案](/help/forms/assets/api-3.png)

   它會在程式碼編輯器中開啟專案。

2. 更新`package.json`檔案以將`type`新增至`module`。

   ```bash
   {
   "name": "demo-nodejs-generate-pdf",
   "version": "1.0.0",
   "type": "module",
   "main": "index.js",
   }
   ```

   ![更新封裝檔案](/help/forms/assets/api-4.png)

##### 步驟4：建立.env檔案

1. 在專案的根層級建立.env檔案
2. 新增下列設定，並將預留位置取代為ADC專案的OAuth伺服器對伺服器認證中的實際值。

   ```bash
   CLIENT_ID=<ADC Project OAuth Server-to-Server credential ClientID>
   CLIENT_SECRET=<ADC Project OAuth Server-to-Server credential Client Secret>
   SCOPES=<ADC Project OAuth Server-to-Server credential Scopes>
   ```

   ![建立環境檔案](/help/forms/assets/api-5.png)

   >[!NOTE]
   >
   > 您可以從Adobe Developer Console專案複製`CLIENT_ID`、`CLIENT_SECRET`和`SCOPES`。

##### 步驟5：建立src/index.js

1. 在專案的根層級建立`index.js`檔案
2. 新增下列程式碼，並以實際值取代預留位置：

```javascript
// Import the dotenv configuration to load environment variables from the .env file
import "dotenv/config";

// Import fetch for making HTTP requests
import fetch from "node-fetch";
import fs from "fs";
import FormData from "form-data";

// REPLACE THE FOLLOWING VALUE WITH YOUR OWN
const bucket = <bucket-value>; // Your AEM Cloud Service Bucket name
const xdpFilePath = <xdp-file>;
const xmlFilePath = <xml-file>;

// Load environment variables
const clientId = process.env.CLIENT_ID;
const clientSecret = process.env.CLIENT_SECRET;
const scopes = process.env.SCOPES;

// Adobe IMS endpoint for obtaining an access token
const adobeIMSV3TokenEndpointURL = "https://ims-na1.adobelogin.com/ims/token/v3";

// Function to get an access token
const getAccessToken = async () => {
    console.log("Getting access token from IMS...");

    const options = {
        method: "POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded",
        },
        body: `grant_type=client_credentials&client_id=${clientId}&client_secret=${clientSecret}&scope=${scopes}`,
    };

    const response = await fetch(adobeIMSV3TokenEndpointURL, options);
    const responseJSON = await response.json();

    console.log("Access token received.");
    return responseJSON.access_token;
};

// Function to generate PDF form from XDP and XML
const generatePDF = async () => {
    const accessToken = await getAccessToken();

    console.log("Generating PDF form from XDP and XML...");

    // Read XDP and XML files
    const xdpFile = fs.readFileSync(xdpFilePath);
    const xmlFile = fs.readFileSync(xmlFilePath);

    const url = `https://${bucket}.adobeaemcloud.com/adobe/document/generate/pdfform`;

    const formData = new FormData();
    formData.append("template", xdpFile, {
        filename: "form.xdp",
        contentType: "application/vnd.adobe.xdp+xml"
    });
    formData.append("data", xmlFile, {
        filename: "data.xml",
        contentType: "application/xml"
    });

    const response = await fetch(url, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${accessToken}`,
            "X-Api-Key": clientId,
            "X-Adobe-Accept-Experimental": "1",
            ...formData.getHeaders()
        },
        body: formData,
    });

    if (response.ok) {
        const arrayBuffer = await response.arrayBuffer();
        fs.writeFileSync("generatedForm.pdf", Buffer.from(arrayBuffer));
        console.log("✅ PDF form generated successfully (saved as generatedForm.pdf)");
    } else {
        console.error("❌ Failed to generate PDF. Status:", response.status);
        console.error(await response.text());
    }
};

// Run the PDF generation function
generatePDF();
```

![建立index.js](/help/forms/assets/api-6.png)

##### 步驟6：執行應用程式

```bash
node src/index.js
```

![執行應用程式](/help/forms/assets/api-7.png)

PDF是在`demo-nodejs-generate-pdf`資料夾中建立。 瀏覽至資料夾以尋找名為`generatedForm.pdf`的產生檔案。

![檢視建立的pdf](/help/forms/assets/api-8.png)

您可以開啟[產生的PDF](/help/forms/assets/create-pdf.png)進行檢視。

## 疑難排解

### 常見問題與可能原因

#### 問題1： 403禁止的錯誤

**症狀：**

- API要求傳回`403 Forbidden`
- 錯誤訊息： *拒絕存取*&#x200B;或&#x200B;*許可權不足*
- 即使使用有效的存取權杖也會發生

**可能的原因：**

- 連結至OAuth伺服器對伺服器認證的產品設定檔中的許可權不足
- AEM Author中的服務使用者群組缺少必要內容路徑上的必要許可權

#### 問題2： 401未授權錯誤

**症狀：**

- API要求傳回`401 Unauthorized`
- 錯誤訊息： *無效或過期的Token*

**可能的原因：**

- 存取權杖已過期（僅適用於24小時）
- 使用者端ID和使用者端密碼不正確或不相符
- API請求中缺少驗證標頭或驗證標頭格式錯誤

#### 問題3： 404 Not Found錯誤

**症狀：**

- API要求傳回`404 Not Found`
- 錯誤訊息：找不到&#x200B;*資源*&#x200B;或找不到&#x200B;*API端點*

**可能的原因：**

- 使用者端ID未在AEM執行個體的`api.yaml`設定中註冊
- 不正確的貯體引數(不符合AEM執行個體識別碼)
- 資源ID （表單或資產）無效或不存在

#### 問題4：無法使用伺服器對伺服器驗證選項

**症狀：**

- Adobe Developer Console中的OAuth伺服器對伺服器選項遺失或停用

**可能的原因：**

- 建立整合的使用者不會在關聯的產品設定檔中新增為&#x200B;**開發人員**

#### 問題5：管道部署失敗

**症狀：**

- 設定管道執行失敗
- 部署記錄檔顯示與`api.yaml`相關的錯誤

**可能的原因：**

- 無效的YAML語法（縮排、引號或陣列格式問題）
- `api.yaml`放置在不正確的目錄中
- 設定中的使用者端ID格式不正確或不正確


## 相關文章

若要瞭解如何設定批次環境（非同步API），請參閱[AEM Forms as a Cloud Service通訊批次處理](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)。
