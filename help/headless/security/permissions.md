---
title: Headless 內容的權限考量事項
description: 了解使用 Adobe Experience Manager 進行 Headless 實作時涉及的不同權限和 ACL 考量事項。了解編寫和發佈環境所需的不同角色和可能權限層級。
feature: Content Fragments,GraphQL API
exl-id: 3fbee755-2fa4-471b-83fc-3f4bf056267a
source-git-commit: 526520a8d9d217d0861a7283b10f7b89dffaf9d5
workflow-type: ht
source-wordcount: '841'
ht-degree: 100%

---

# Headless 內容的權限考量事項

進行 Headless 實作時，應該處理幾個安全和權限方面的問題。權限和角色可以根據 AEM 環境：**作者**&#x200B;或&#x200B;**發佈**&#x200B;進行廣泛的考量。每個環境都包含不同的角色和不同的需求。

## 編寫服務考量事項

編寫服務是內部使用者建立、管理和發佈內容的地方。權限取決於管理內容的不同角色。

### 在群組層級的權限

作為最佳做法，應在 AEM 的群組上設定權限。也稱為本機群組，這些群組可以在 AEM 編寫環境中管理。

管理群組成員身份最簡單方法是使用 Adobe Identity Management System (IMS) 群組，並將 [IMS 群組指派到本機 AEM 群組](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hant#managing-permissions-in-aem)。

![Admin Console 權限流程](assets/admin-console-aem-group-permissions.png)

概略來說，該流程是：

1. 使用 [Admin Console](https://adminconsole.adobe.com/) 將 IMS 使用者新增到新的或現有的 IMS 使用者群組
1. 使用者登入時，IMS 群組會與 AEM 同步。
1. 將 IMS 群組指派到 AEM 群組。
1. 在 AEM 群組設定權限。
1. 當使用者登入 AEM 並透過 IMS 進行驗證時，他們將繼承 AEM 群組的權限。

>[!TIP]
>
> 說明如何管理 IMS 和 AEM 使用者和群組的詳細影片逐步解說位於[此處](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html)。

若要管理 AEM **群組**，請導覽至&#x200B;**工具** > **安全性** > **群組**。

若要管理 AEM 群組權限，請導覽至&#x200B;**工具** > **安全性** > **權限**。

### DAM 使用者

在這種情況下，「DAM」是指數位資產管裡。**DAM 使用者**&#x200B;是可立即使用的 AEM 群組，可用於管理數位資產和內容片段的「日常」使用者。此群組提供相關權限可讓使用者&#x200B;**檢視**、**新增**、**更新**、**刪除**&#x200B;以及&#x200B;**發佈**&#x200B;片段內容和 AEM Assets 中的所有其他檔案。

如果使用 IMS 來管理群組成員資格，請將適當的 IMS 群組新增為 **DAM 使用者**&#x200B;群組的成員。IMS 群組的成員在登入 AEM 環境時會繼承 DAM 使用者群組的權限。

#### 自訂 DAM 使用者群組

最好不要直接修改可立即使用群組的權限。相反地，您也可以根據 **DAM 使用者**&#x200B;群組權限建立您自己的群組，並進一步限制 AEM Assets 內不同&#x200B;**資料夾**&#x200B;的存取權。

如需更精細的權限，請使用 AEM 中的&#x200B;**權限**&#x200B;主控台，並將路徑從 `/content/dam`更新為更具體的路徑，即 `/content/dam/mycontentfragments`。

可能需要授予此群組使用者建立和編輯而非刪除內容片段的權限。若要查看和指派編輯權限而非刪除權限，請參閱[內容片段 - 刪除考量事項](/help/sites-cloud/administering/content-fragments/delete-considerations.md)。

### 模型編輯器

修改&#x200B;**內容片段模型**&#x200B;的能力應交給管理員或具有較高權限的一&#x200B;**小組**&#x200B;使用者。修改內容片段模型會對下游產生很多影響。

>[!CAUTION]
>
>修改內容片段模型會改變 Headless 應用程式所依賴的基礎 GraphQL API。

如果您想要建立一個可以管理內容片段模型但沒有完全管理員存取權的群組，可以建立具有以下存取控制項目的群組：

| 路徑 | 權限 | 權限 |
|-----| -------------| ---------|
| `/conf` | **允許** | `jcr:read` |
| `/conf/<config-name>/settings/dam/cfm` | **允許** | `rep:write`, `crx:replicate` |

## 發佈服務權限

發佈服務被視為「即時環境」，通常是 GraphQL API 取用者互動的對象。內容在編寫服務經編輯和核准後，將發佈到發佈服務。然後， Headless 應用程式透過 GraphQL API 從發佈服務取用經核准的內容。

依預設，透過 AEM 發佈服務的 GraphQL 端點公開的內容，每個人都可存取，包括未經驗證的使用者。

### 內容權限

透過 AEM GraphQL API 公開的內容可以使用在資產資料夾上設定的[封閉使用者群組 (CUG) ](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html) 來進行限制，其在指定哪些 AEM 使用者群組 (及其成員) 可以存取資產資料夾的內容。

資產 CUG 透過以下方式運作：

* 首先，拒絕資料夾和子資料夾的所有存取
* 然後，允許 CUG 清單中的所有 AEM 使用者群組擁有資料夾和子資料夾的讀取權限

在內含透過 GraphQL API 公開之內容的資產資料夾上，可以設定 CUG。AEM Publish 資產資料夾的存取權應透過使用者群組控制，而非直接由使用者控制。建立 (或重複使用) AEM 使用者群組，該群組會授予內含 GraphQL API 公開之內容的資產資料夾存取權。

#### 選擇驗證配置{#publish-permissions-users}

[AEM Headless SDK](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) 支援兩種驗證類型：

* [權杖型驗證](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)，使用與單一技術帳戶綁定的服務認證。
* 採用 AEM 使用者的基本驗證。

### 存取 GraphQL API

提供[適當驗證認證](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client)給 AEM Publish 服務 GraphQL API 端點的 HTTP 要求，其包含認證被授權可讀取的內容和能以匿名方式存取的內容。GraphQL API 的其他取用者無法讀取受 CUG 保護之資料夾中的內容。
