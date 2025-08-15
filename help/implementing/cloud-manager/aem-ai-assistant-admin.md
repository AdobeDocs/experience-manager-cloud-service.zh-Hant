---
title: 在Adobe Experience Manager中設定AI助理
description: 瞭解如何使用Adobe Experience Manager中的Admin Console來設定人工智慧助理。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ab8fefe18e43c1fe937d0d16df65b6137fc8a292
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 3%

---

# 設定AEM AI助理 — 管理員設定 {#aem-ai-asst-admin-setup}

管理員必須先設定存取權、許可權和設定，組織內的使用者才能使用AEM AI Assistant的功能。 本文說明如何為貴組織啟用AI助理員、設定必要的認證及儲存組態變更。

**AEM AI Assistant組態程式概觀**

組態程式包含下列步驟：

1. 在Adobe Admin Console中建立新的產品設定檔。
1. 啟用「AI助理產品知識」許可權。
1. 建立或使用現有的使用者群組。
1. 將使用者新增至使用者群組。
1. 將產品設定檔指派給使用者群組。

**先決條件**

開始之前，請確定您已符合下列必要條件：

* 您在Adobe Admin Console中必須至少具有產品管理員許可權。
* 您瞭解組織的使用者管理結構。

## 1 — 在Adobe Admin Console中建立新的產品設定檔{#create-profile}

1. 依照[在Adobe Admin Console中建立新的產品設定檔](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile)中的詳細指示操作，找到Experience Platform檔案。

1. 建立新產品設定檔時，請使用以下範例來說明可用於AI助理的值。

   | 文字欄位 | 建議值 |
   | --- | --- |
   | 產品設定檔名稱 | `AEM AI Assistant` （或您偏好的描述性名稱） |
   | 顯示名稱（選擇性） | `AI Assistant` |
   | 說明 (選填) | `Product profile for managing AEM AI Assistant access` |
   | 通知 | 根據您組織的偏好設定進行設定 |




## 2 — 啟用「AI助理產品知識」許可權{#enable-permission}

指派自訂許可權給產品設定檔的程式遵循標準Adobe Cloud Manager自訂許可權工作流程。

參考文章： [將自訂許可權指派給新的產品設定檔](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. 在Admin Console中，按一下您新建立的產品設定檔名稱(`AEM AI Assistant`)

   ![螢幕擷圖](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. 若要檢視可編輯許可權的清單，請按一下&#x200B;**許可權**&#x200B;索引標籤。

1. 在表格清單中，找出`AI Assistant Product Knowledge`許可權。

   Admin Console中的![AI助理許可權索引標籤](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. 在許可權名稱的右側，按一下![鉛筆圖示或「編輯」圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)。

1. 在&#x200B;**編輯AI助理的許可權**&#x200B;頁面中，開啟&#x200B;**AI助理產品知識**&#x200B;切換開關。

   ![ AI助理產品知識切換選項的編輯許可權頁面](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. 在頁面的右下角，按一下[儲存]。**&#x200B;**

   您的產品設定檔現在已啟用AI助理產品知識許可權。


## 3 — 建立使用者群組（或使用現有的使用者群組）{#create-user-group}

1. 執行下列任一項作業：

>[!BEGINTABS]

>[!TAB 建立新的使用者群組]

1. 在Admin Console中，按一下&#x200B;**使用者** > **使用者群組**。

   ![使用者群組](/help/implementing/cloud-manager/assets/ai-assistant-user-groups.png)

1. 在&#x200B;**使用者群組**&#x200B;頁面中，按一下&#x200B;**新增使用者群組**。

   ![使用者群組頁面上的[新增使用者群組]按鈕](/help/implementing/cloud-manager/assets/ai-assistant-new-user-group.png)

1. 在&#x200B;**建立新的使用者群組**&#x200B;頁面中，提供下列資訊：

   | 選項 | 建議值 |
   | --- | --- |
   | 使用者群組名稱 | `AEM AI Assistant` （或您偏好的名稱） |
   | 說明 (選填) | `User group for managing AEM AI Assistant access` |

   ![建立新的使用者群組頁面](/help/implementing/cloud-manager/assets/ai-assistant-create-new-user-group.png)

1. 在頁面的右下角，按一下[儲存]。**&#x200B;**

>[!TAB 使用現有的使用者群組]

如果現有AEM使用者群組符合AI Assistant存取要求，您就可以使用該使用者群組，而不需要建立新群組。

>[!ENDTABS]

## 4 — 將使用者新增至使用者群組{#add-users}

1. 執行下列任一項作業：

>[!BEGINTABS]

>[!TAB 新增個別使用者]

1. 在&#x200B;**使用者群組**&#x200B;頁面的&#x200B;**群組名稱**&#x200B;表格中，按一下您新建立的使用者群組名稱或現有的使用者群組名稱。

   ![使用者群組頁面在表格中顯示AEM AI助理使用者群組名稱](/help/implementing/cloud-manager/assets/ai-assistant-user-group-name-in-table.png)

1. 在&#x200B;**AEM AI小幫手**&#x200B;的&#x200B;**使用者群組**&#x200B;頁面中，按一下&#x200B;**使用者**&#x200B;索引標籤，然後按一下&#x200B;**新增使用者**。

   ![AEM AI助理使用者群組頁面，顯示[使用者]索引標籤和[新增使用者]按鈕](/help/implementing/cloud-manager/assets/ai-assistant-add-users.png)

1. 在&#x200B;**新增使用者至此使用者群組**&#x200B;頁面上，搜尋並選取需要存取AEM AI助理的使用者。

   ![新增使用者至此使用者群組頁面](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. 在頁面的右下角，按一下[儲存]。**&#x200B;**

>[!TAB 大量新增使用者]

您可以在Admin Console中使用大量上傳功能。

1. 準備包含使用者資訊的CSV檔案。

1. 使用&#x200B;**透過CSV新增使用者**&#x200B;選項，以有效進行大量新增。

>[!ENDTABS]




## 5 — 將產品設定檔指派給使用者群組{#assign-product-profile}




