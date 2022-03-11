---
title: 無頭內容的權限考慮事項
description: 瞭解與Adobe Experience Manager一起實施無頭項的不同權限和ACL注意事項。 瞭解「作者」和「發佈」環境所需的不同角色和潛在權限級別。
feature: Content Fragments,GraphQL API
exl-id: 3fbee755-2fa4-471b-83fc-3f4bf056267a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# 無頭內容的權限考慮事項

通過無頭實施，有幾個安全和權限領域需要解決。 權限和角色可以根據環境進行廣AEM泛考慮 **作者** 或 **發佈**。 每個環境都包含不同的角色和不同的需求。

## 作者服務注意事項

作者服務是內部用戶建立、管理和發佈內容的位置。 權限圍繞管理內容的不同角色。

### 在組級別管理權限

最佳做法是，應在中的「組」上設定權AEM限。 這些組也稱為本地組，可以在作者環境中AEM進行管理。

管理組成員資格的最簡單方法是使用AdobeIdentity Management系統(IMS)組並分配 [IMS組到本地AEM組](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=en#managing-permissions-in-aem)。

![管理控制台權限流](assets/admin-console-aem-group-permissions.png)

從高度講，這一過程是：

1. 使用 [Admin Console](https://adminconsole.adobe.com/)
1. IMS組與用戶登錄時AEM同步。
1. 將IMS組分配AEM給組。
1. 設定組AEM權限。
1. 當用戶登錄並通AEM過IMS進行身份驗證時，他們將繼承組的權AEM限。

>[!TIP]
>
> 可以找到管理IMS和用戶AEM和組的詳細視頻漫遊 [這裡](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html)。

管理 **組** 中AEM，導航 **工具** > **安全** > **組**。

要管理中的組權限，請導AEM航至 **工具** > **安全** > **權限**。

### DAM用戶

在此背景下，「DAM」代表數字資產管理。 的 **DAM用戶** 是現成的組，可用AEM於管理數字資產和內容片段的「日常」用戶。 此組向 **視圖**。 **添加**。 **更新**。 **刪除**, **發佈** 內容片段和AEM Assets中的所有其他檔案。

如果將IMS用於組成員身份，則添加適當的IMS組作為 **DAM用戶** 組。 登錄到環境時，IMS組的成員將繼承DAM用戶組的權AEM限。

#### 自定義DAM用戶組

最好不要直接修改出廠設定組的權限。 相反，您也可以建立自己的組，這些組建在 **DAM用戶** 組權限，並進一步限制對不同權限的訪問 **資料夾** 在AEM Assets。

要獲得更細的權限，請使用 **權限** 控制台AEM中並更新路徑 `/content/dam` 到更具體的路徑，即 `/content/dam/mycontentfragments`。

最好給這組用戶授予建立和編輯內容片段而不是刪除的權限。 要查看和分配編輯權限，但不要刪除，請參閱 [內容片段 — 刪除注意事項](/help/assets/content-fragments/content-fragments-delete.md)。

### 模型編輯器

修改能力 **內容片段模型** 應留給管理員或 **小群** 具有提升權限的用戶。 修改內容片段模型具有許多下游效果。

>[!CAUTION]
>
>對內容片段模型的修改會改變無頭應用程式所依賴的基礎GraphQL API。

如果您希望建立一個管理內容片段模型但沒有完全管理員訪問權限的組，則可以建立具有以下訪問控制項的組：

| 路徑 | 權限 | 權限 |
|-----| -------------| ---------|
| `/conf` | **允許** | `jcr:read` |
| `/conf/<config-name>/settings/dam/cfm` | **允許** | `rep:write`, `crx:replicate` |

## 發佈服務權限

「發佈」服務被視為「即時」環境，通常是GraphQL API使用者與之交互的環境。 內容在作者服務上編輯和批准後，將發佈到發佈服務。 然後，無頭應用程式通過GraphQL API從發佈服務中使用批准的內容。

預設情況下，通過AEM發佈服務的GraphQL終結點公開的內容可供所有人訪問，包括未經身份驗證的用戶。

### 內容權限

通過GraphQL APIAEM公開的內容可以使用 [已關閉用戶組(CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html) 在「資產」資料夾上設定，該資料夾AEM指定哪些用戶組（及其成員）可以訪問「資產」資料夾的內容。

資產CUG的工作方式：

* 首先，拒絕對資料夾和子資料夾的所有訪問
* 然後，允許對CUG清單中列出的所AEM有用戶組的資料夾和子資料夾進行讀取訪問

可以在包含通過GraphQL API公開的內容的資產資料夾上設定CUG。 AEM發佈上對資產資料夾的訪問應通過用戶組控制，而不是直接通過用戶。 建立（或重新使用）AEM用戶組，該用戶組授予對包含由GraphQL API公開的內容的資產資料夾的訪問權限。

#### 選擇驗證方案{#publish-permissions-users}

的 [無AEM頭SDK](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) 支援兩種身份驗證：

* [基於令牌的身份驗證](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 使用綁定到單個技術帳戶的服務憑據。
* 使用用戶進行基AEM本驗證。

### 訪問GraphQL API

提供 [適當的身份驗證憑據](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) 到AEM發佈服務的GraphQL API端點，包括憑據被授權讀取的內容以及可匿名訪問的內容。 GraphQL API的其他使用者無法讀取受CUG保護的資料夾中的內容。
