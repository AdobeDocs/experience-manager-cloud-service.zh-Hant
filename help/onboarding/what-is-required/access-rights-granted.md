---
title: 授予的訪問權限——需要什麼
description: 授予的訪問權限——需要什麼
translation-type: tm+mt
source-git-commit: 8259bf4e7f2004d76fd985ec7ad7c416b6f8d491
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 9%

---


# 授予的存取權限 {#access-rights-granted}

Adobe將在AdobeIdentity Management系統(IMS)中為您的公司建立&#x200B;**組織**&#x200B;識別碼，以便管理您的所有使用者及其權限。 每位使用者必須是本組織的成員，且將獲得[!UICONTROL Experience Cloud]服務的存取權，必須擁有自己的&#x200B;**Adobe ID**。

## 用戶身份類型{#user-identity-types}

若要開始使用Adobe ID，請造訪[管理Adobe身份類型](https://helpx.adobe.com/enterprise/using/identity.html)，以取得如何使用其中一種可用身份類型取得Adobe ID的詳細說明。

## 用戶和角色{#users-and-roles}

在Adobe為您的公司建立組織後，您指定的管理員即會新增為該組織的第一名成員。系統預設會授予管理員權限，並指派 [!UICONTROL AEM Managed Services]**Product**，以及一或多個 [!UICONTROL Cloud Manager] Product Profiles **** Chould。

1. 一旦系統管理員授予您Cloud Manager的存取權，您就會收到一封電子郵件，將您帶往Cloud Manager登入頁面，也可透過[Adobe Experience Cloud](https://my.cloudmanager.adobe.com/)存取。

1. 在Cloud Manager的登陸頁面上，按一下「管理存取權」。****

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

1. 按一下「管理存取權&#x200B;**」後，您會導覽至「** Admin Console **」，您可從此處管理Cloud Manager的使用者角色或權限。**

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin1.png)

   在Admin Console中，您可以執行SysAdmin任務，例如：
   * [管理角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-roles)
   * [管理對作者實例的訪問](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-access-aem)

      >[!NOTE]
      >請造訪[使用者與角色](#users-roles)一節，以進一步瞭解Cloud Manager中的使用者與角色定義。

授予這些權限後，管理員現在會設定單一登入(使用Adobe ID)來存取[!UICONTROL Experience Cloud]服務、登入您的雲端環境AEM，以及使用[!UICONTROL Cloud Manager]。

[!UICONTROL Cloud Manager]中的許多功能需要特定權限才能運作。

[!UICONTROL Cloud ] Manager目前為控制特定功能可用性的使用者定義四個角色：

* 企業負責人
* 計畫經理
* 部署管理員
* 開發人員

>[!CAUTION]
>若要使用[!UICONTROL Cloud Manager]，您必須將Adobe ID和Adobe Experience Manager作為Cloud Service產品上下文。

### 角色定義{#role-definitions}

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

### 整合產品設定檔{#integration-product-profile}

除了上述外，Cloud Manager還將自動建立名為「整合-Cloud Service」的產品設定檔。 此產品設定檔用於Adobe Experience Manager與其他Adobe產品的整合。 此產品配置檔案&#x200B;**必須**&#x200B;不能刪除。 如果您意外刪除了此配置式，則需要手動重新建立。 此配置檔案&#x200B;**的「顯示名稱」必須**&#x200B;為`CM_CS_DEFAULT`。

