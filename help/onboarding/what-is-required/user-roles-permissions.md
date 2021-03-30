---
title: 使用者角色和權限
description: 本頁說明使用者角色和權限。 請依照本頁瞭解如何新增使用者並指派他們至Cloud Manager角色。
translation-type: tm+mt
source-git-commit: f09b688db23024d59f39b53766060b6f3b14e564
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 7%

---


# 用戶角色和權限{#user-roles-permissions}

Adobe將在AdobeIdentity Management系統(IMS)中為您的公司建立&#x200B;**組織**&#x200B;識別碼，以便管理您的所有使用者及其權限。 每位使用者必須是本組織的成員，且將獲得[!UICONTROL Experience Cloud]服務的存取權，必須擁有自己的&#x200B;**Adobe ID**。

## 使用者角色 {#user-roles}

Cloud Manager中的許多功能需要特定權限才能運作。

Cloud Manager目前為控制特定功能可用性的用戶定義四個角色：

* 企業負責人
* 部署管理員
* 計畫經理
* 開發人員

>[!NOTE]
>Admin Console中的「開發人員」角色與[!UICONTROL Cloud Manager]中的「開發人員」角色無關。

下表匯總了角色：

| [!UICONTROL Cloud ] Manager角色 | 說明 |
|--- |--- |
| 企業負責人 | 負責定義KPI、批准生產部署及覆寫重要的3層故障。 |
| 計畫經理 | 使用[!UICONTROL Cloud Manager]執行團隊設定、檢閱狀態及檢視KPI。 可以批准重要的3層故障。 |
| 部署管理員 | 管理部署操作。 使用[!UICONTROL Cloud Manager]執行階段／生產部署。 可編輯CI/CD管線。 可以批准重要的3層故障。 可以訪問Git儲存庫。 |
| 開發人員 | 開發並測試自訂的應用程式碼。 主要使用[!UICONTROL Cloud Manager]來檢視狀態。 可以訪問Git儲存庫以進行代碼提交。 |
| 內容作者 | 通常不與[!UICONTROL Cloud Manager]互動。 可以使用[!UICONTROL Cloud Manager]程式切換器(已從[!UICONTROL Experience Cloud]導航)訪問AEM。 |

### 整合產品設定檔{#integration-product-profile}

除了上述外，Cloud Manager還將自動建立名為「整合-Cloud Service」的產品設定檔。 此產品設定檔用於Adobe Experience Manager與其他Adobe產品的整合。 此產品配置檔案&#x200B;**必須**&#x200B;不能刪除。 如果您意外刪除了此配置式，則需要手動重新建立。 此配置檔案&#x200B;**的「顯示名稱」必須**&#x200B;為`CM_CS_DEFAULT`。


## 與角色定義{#permissions}關聯的權限

[!UICONTROL Cloud Manager 已預先設定角色，賦予適當權限。]例如，開發人員會開發程式碼，並具有將程式碼推送至&#x200B;**Git Repository**&#x200B;的權限。 或者，企業擁有者擁有不同的權限，可讓他們定義關鍵績效指標(KPI)並批准部署。


每個角色都具有與每個角色關聯的特定權限。 下表匯總了角色，列出了可用的函式，以及可執行該函式的角色。

| 權限 | 說明 | 企業負責人 | 部署管理員 | 計畫經理 | 開發人員 |
|--- |--- |--- |--- |--- |--- |
| 添加程式 | 新增計畫。 | x |  |  |  |
| 建立環境 | 建立Prod+Stage、Dev、環境。 | x | x |  |  |
| 更新環境 | 更新Prod+Stage、Dev、環境。 | x | x |  |  |
| 刪除環境 | 刪除非prod、開發、環境。 | x | x |  |  |
| 管線設定 | 設定或編輯管線。 |  | x |  |  |
| 管線執行 | 啟動管線。 | x | x |  |  |
| 管線執行 | 拒絕／批准重要的3層故障。 | x | x | x |  |
| 管線執行 | 提供GoLive批准。 | x | x | x |  |
| 管線執行 | 排程生產部署。 | x | x | x |  |
| 管線刪除 | 允許刪除管線。 |  | x |  |  |
| 執行取消 | 取消當前執行。 |  | x |  |  |
| 產生個人存取Token | 存取Git。 |  | x |  | x |