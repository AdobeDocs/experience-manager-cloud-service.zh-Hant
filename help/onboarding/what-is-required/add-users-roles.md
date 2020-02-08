---
title: 新增使用者和角色——必要項目
description: 新增使用者和角色——必要項目
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# 新增使用者和角色——必要項目 {#add-users-roles}


Cloud Manager中的許 [!UICONTROL 多功能] ，都需要特定的權限才能運作。 例如，僅允許某些用戶為程式設定關鍵績效指標(KPI)。 這些權限在邏輯上分組為角色。

[!UICONTROL Cloud Manager] （雲管理器）目前為控制特定功能可用性的用戶定義四個角色：

* 企業負責人
* 計畫經理
* 部署管理員
* 開發人員

>[!CAUTION]
>
>若要使 [!UICONTROL 用Cloud Manager]，您必須擁有Adobe ID和Adobe Managed services產品內容。

## 角色定義 {#role-definitions}

>[!NOTE]
>
>Admin console中的「開發人員角色」與 [!UICONTROL Cloud Manager中的「開發人員」角色無關]。

下表匯總了角色：

| [!UICONTROL Cloud Manager] Roles | 說明 |
|--- |--- |
| 企業負責人 | 負責定義KPI、批准生產部署及覆寫重要的3層故障。 |
| 計畫經理 | 使用 [!UICONTROL Cloud Manager] ，執行團隊設定、檢閱狀態及檢視KPI。 可以批准重要的3層故障。 |
| 部署管理員 | 管理部署操作。 使用 [!UICONTROL Cloud Manager] 執行舞台／生產部署。 可編輯CI/CD管線。 可以批准重要的3層故障。 可以訪問Git儲存庫。 |
| 開發人員 | 開發並測試自訂的應用程式碼。 主要使 [!UICONTROL 用Cloud Manager] 來檢視狀態。 可以訪問Git儲存庫以進行代碼提交。 |
| 內容作者 | 通常不與 [!UICONTROL Cloud Manager互動]。 可能會 [!UICONTROL 使用Cloud Manager] Program Switcher(在從 [!UICONTROL Experience Cloud]瀏覽後)存取AEM。 |

## 使用Admin console建立設定檔 {#using-admin-console-to-create-a-profile}

您可從Adobe Admin console為 [!UICONTROL Cloud Manager] 管理角色。 將使用者新增至Admin console的「 [!UICONTROL Cloud Manager] Product Profile」（雲端管理員產品設定檔），以提供特定角色成員資格。

您可以在Adobe Admin console中將使用者新增至 [!UICONTROL Cloud Manager] **Product Profile** ，以指派特定角色會籍。Adobe Admin console是管理整個組織中Adobe權益的集中位置。 若要進一步瞭解Adobe Admin Console，請參閱 [Admin Console的檔案](https://helpx.adobe.com/enterprise/using/admin-console.html)。

>[!NOTE]
>
>若要存取管理控制台並設定您的團隊（使用者和角色），請開啟瀏覽器並造訪 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

為了為 [!UICONTROL Cloud Manager] （客戶組織中的管理員）使用者提供適當的角色型權限，必須在 **AEM Managed Services** Product Context下建立新的產品設定檔。

若要為 [!UICONTROL Cloud Manager] （雲端管理員）使用者提供適當的角色型權限，您必須在與四個 [!UICONTROL Cloud Manager] （雲端管理員）角色對應的「 [!UICONTROL AEM Managed Services] Product Context」（AEM Managed Services產品內容）下建立四個新的產品設定檔：

* 企業負責人
* 部署管理員
* 開發人員
* 計畫經理

您可以使用 [Admin Console](https://adminconsole.adobe.com/) for [!UICONTROL Cloud Manager]，建立或新增使用者／群組至這些產品設定檔，如下圖所示：

1. 登入管理控制台，然後按一下「 **新增描述檔** 」以新增描述檔。

1. 填寫欄位以設定 [!UICONTROL Cloud Manager的新角色]。

   輸入 **描述檔名**、 **顯示名稱** ，以建立新的描述檔。 此外，您也可以為描述 **檔選取「權限群組** 」。

   按一下「 **完成** 」(Done)以完成配置檔案建立步驟。

   >[!NOTE]
   >
   >建立這些產品設定檔時，「顯 **示名稱** 」必須是 [!UICONTROL Cloud Manager定義的技術值] （請參閱下表）。 The **Profile Name** can be anything, buth foun commuse, it is recommended to use the values in *Recommended Profile Name* column below. 若要這麼做，在建立產品描述檔時，請取消勾選「與描述檔名 **稱相同** 」，並指定對應的值為 **「顯示名稱」**。

   | **角色** | **顯示名稱（必要）** | **建議的描述檔名稱** |
   |---|---|---|
   | 企業負責人 | CM_BUSINESS_OWNER_ROLE_PROFILE | [!UICONTROL Cloud Manager] —— 業務擁有者角色 |
   | 部署管理員 | CM_DEPLOYMENT_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] —— 部署管理員角色 |
   | 開發人員 | CM_DEVELOPER_ROLE_PROFILE | [!UICONTROL Cloud Manager] —— 開發人員角色 |
   | 計畫經理 | CM_PROGRAM_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] —— 計畫經理角色 |

1. 在您建立產品設定檔後，就可以將使用者（或群組）新增至產品設定檔。


