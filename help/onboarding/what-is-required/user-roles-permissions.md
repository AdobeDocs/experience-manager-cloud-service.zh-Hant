---
title: 使用者角色和權限
description: 本頁說明使用者角色和權限。 請依照本頁瞭解如何新增使用者並指派他們至Cloud Manager角色。
translation-type: tm+mt
source-git-commit: 683e660bace4bf2d21ab6b373c75f78e306f5206
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 8%

---


# 用戶角色和權限{#user-roles-permissions}

## 使用者角色 {#user-roles}

Cloud Manager中的許多功能需要特定權限才能運作。

Cloud Manager中的許多功能需要特定權限才能執行，並根據指派的角色和權限限制您在使用者介面中執行的動作。 在某些情況下，如果您沒有執行動作的權限，則介面控制項會存在，但會停用。

如果您有要執行但無法執行的動作，請勾選與角色定義](#permissions)相關的[權限。 根據您的目標，您可以聯絡系統管理員並請求所需的角色。

Cloud Manager目前為控制特定功能可用性的用戶定義四個角色：

* 企業負責人
* 部署管理員
* 計畫經理
* 開發人員

>[!NOTE]
>Admin Console中的「開發人員」角色與[!UICONTROL Cloud Manager]中的「開發人員」角色無關。

## 查看角色{#view-roles}

若要在Cloud Manager中檢視您的角色，請登入Cloud Manager UI，在右上角選取您的設定檔圖示，然後選取&#x200B;**使用者角色**，如下圖所示。

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### 整合產品設定檔{#integration-product-profile}

除了上述外，Cloud Manager還將自動建立名為「整合-Cloud Service」的產品設定檔。 此產品設定檔用於Adobe Experience Manager與其他Adobe產品的整合。 此產品配置檔案&#x200B;**必須**&#x200B;不能刪除。 如果您意外刪除了此配置式，則需要手動重新建立。 此配置檔案&#x200B;**的「顯示名稱」必須**&#x200B;為`CM_CS_DEFAULT`。


## 與角色定義{#permissions}關聯的權限

[!UICONTROL Cloud Manager 已預先設定角色，賦予適當權限。]例如，開發人員會開發程式碼，並具有將程式碼推送至&#x200B;**Git Repository**&#x200B;的權限。 或者，企業擁有者擁有不同的權限，可讓他們新增和編輯程式、新增環境及核准部署。

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