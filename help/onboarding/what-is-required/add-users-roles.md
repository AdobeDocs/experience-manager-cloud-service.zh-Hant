---
title: 新增使用者和角色——必要項目
description: 新增使用者和角色——必要項目
translation-type: tm+mt
source-git-commit: 936e42f273b75f0ea7776c51f57af44ec9e6d96f

---


# 新增使用者和角色 {#add-users-roles}


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