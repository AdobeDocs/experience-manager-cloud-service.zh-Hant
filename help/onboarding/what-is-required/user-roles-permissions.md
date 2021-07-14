---
title: Cloud Manager角色
description: 本頁面說明使用者角色和權限。 請詳閱本頁，了解如何新增使用者並將其指派給Cloud Manager角色。
exl-id: d1689134-044a-4d96-97a2-cd09f735a680
source-git-commit: a0edbaf650fdfbc271a000ab4827a4c414321613
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 6%

---

# Cloud Manager角色 {#user-roles-permissions}

## 使用者角色 {#user-roles}

Cloud Manager的許多功能都需要特定權限才能運作，並根據指派的角色和權限，限制您在使用者介面中所執行的動作。 在某些情況下，如果您沒有採取動作的權限，則介面控制項會存在，但會停用。

如果有您要執行的動作，但無法執行，請檢查下面的[使用者角色和權限](#permissions)區段。 您可以聯絡系統管理員並請求您所需的角色，視您的目標而定。

Cloud Manager目前為使用者定義四個角色，這些角色可控制特定功能的可用性：

* 業務負責人
* 部署管理員
* 計畫經理
* 開發人員

>[!NOTE]
>Admin Console中的開發人員角色與[!UICONTROL Cloud Manager]中的開發人員角色無關。

## 檢視您的角色 {#view-roles}

若要在Cloud Manager中檢視您的角色，請登入Cloud Manager UI，選取右上角的設定檔圖示，然後選取&#x200B;**使用者角色**，如下圖所示。

>[!NOTE]
>請參閱[導覽至Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md)以進一步了解登入Cloud Manager的資訊。

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### 整合產品設定檔 {#integration-product-profile}

除了上述功能，Cloud Manager將自動建立名為「整合 — Cloud Service」的產品設定檔。 此產品設定檔用於整合Adobe Experience Manager與其他Adobe產品。 此產品配置檔案&#x200B;**必須**&#x200B;不能刪除。 如果您不小心刪除了此設定檔，則需要手動重新建立。 此配置檔案&#x200B;**的「顯示名稱」必須**&#x200B;為`CM_CS_DEFAULT`。


## 使用者角色和權限 {#permissions}

[!UICONTROL Cloud Manager 已預先設定角色，賦予適當權限。]例如，開發人員開發程式碼，並擁有將程式碼推送至Git存放庫的權限。 或者，業務擁有者擁有不同的權限，可讓他們新增和編輯程式、新增環境，以及核准部署。

每個角色都有與其相關聯的特定權限。 例如，如果您的角色為：

* ***業務擁有者***，則您擁有新增程式或編輯程式、新增或更新環境，以及執行任何管道的權限。

* ***部署管理器***，則您有權添加或更新環境，並運行任何管道。

* ***開發人員***，您便有權產生個人存取權杖以存取Git。

   >[!NOTE]
   > 可以將用戶分配給多個角色。 例如，將業務所有者和部署管理員角色分配給用戶時，會為其提供這些權限的組合或總和。


下表摘要了Cloud Manager中的角色及其相關權限。

| 權限 | 說明 | 業務負責人 | 部署管理員 | 計畫經理 | 開發人員 |
|--- |--- |--- |--- |--- |--- |
| 添加程式<br>編輯程式 | 新增方案。<br>編輯程式 — 添加或刪除解決方案或附加元件的 | x |  |  |  |
| 建立環境 | 建立Prod+Stage、Dev、Environments。 | x | x |  |  |
| 更新環境 | 更新Prod+Stage、Dev、Environments。 | x | x |  |  |
| 刪除開發環境 | 刪除開發環境。 | x | x |  |  |
| 管道設定 | 設定或編輯管道。 |  | x |  |  |
| 管道執行 | 啟動管道。 | x | x |  |  |
| 管道執行 | 拒絕/批准重要的3層故障。 | x | x | x |  |
| 管道執行 | 提供GoLive核准。 | x | x | x |  |
| 管道執行 | 排程生產部署。 | x | x | x |  |
| 管道刪除 | 允許刪除管道。 |  | x |  |  |
| 執行取消 | 取消當前執行。 |  | x |  |  |
| 產生個人存取權杖 | 存取Git。 |  | x |  | x |
