---
title: 新增使用者和角色——必要項目
description: 新增使用者和角色——必要項目
translation-type: tm+mt
source-git-commit: 2c21414edd6c3178d05c818d2bf57aa152b5956b
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 2%

---


# 新增使用者和角色 {#add-users-roles}


[!UICONTROL Cloud Manager]中的許多功能需要特定權限才能運作。

[!UICONTROL Cloud ] Manager目前為控制特定功能可用性的使用者定義四個角色：

* 企業負責人
* 計畫經理
* 部署管理員
* 開發人員

>[!CAUTION]
>
>若要使用[!UICONTROL Cloud Manager]，您必須將Adobe ID和Adobe Experience Manager作為Cloud Service產品上下文。

## 角色定義{#role-definitions}

>[!NOTE]
>
>Admin Console中的「開發人員」角色與[!UICONTROL Cloud Manager]中的「開發人員」角色無關。

下表匯總了角色：

| [!UICONTROL Cloud ] Manager角色 | 說明 |
|--- |--- |
| 企業負責人 | 負責定義KPI、批准生產部署及覆寫重要的3層故障。 |
| 計畫經理 | 使用[!UICONTROL Cloud Manager]執行團隊設定、檢閱狀態及檢視KPI。 可以批准重要的3層故障。 |
| 部署管理員 | 管理部署操作。 使用[!UICONTROL Cloud Manager]執行階段／生產部署。 可編輯CI/CD管線。 可以批准重要的3層故障。 可以訪問Git儲存庫。 |
| 開發人員 | 開發並測試自訂的應用程式碼。 主要使用[!UICONTROL Cloud Manager]來檢視狀態。 可以訪問Git儲存庫以進行代碼提交。 |
| 內容作者 | 通常不與[!UICONTROL Cloud Manager]互動。 可以使用[!UICONTROL Cloud Manager]程式切換器(已從[!UICONTROL Experience Cloud]導航)訪問AEM。 |

## 整合產品設定檔{#integration-product-profile}

除了上述外，Cloud Manager還將自動建立名為「整合-Cloud Service」的產品設定檔。 此產品設定檔用於Adobe Experience Manager與其他Adobe產品的整合。 此產品配置檔案&#x200B;**必須**&#x200B;不能刪除。 如果您意外刪除了此配置式，則需要手動重新建立。 此配置檔案&#x200B;**的「顯示名稱」必須**&#x200B;為`CM_CS_DEFAULT`。
