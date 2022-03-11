---
title: 專案
description: 項目使您可以將資源分組到一個實體中，該實體的公共共用環境使管理項目變得容易
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
source-git-commit: 8ea043b4b6424d6922c41c143ca74fd25ac60cf8
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 11%

---

# 專案 {#projects}

項目允許您將資源分組到一個實體中。 通用的共用環境使管理項目變得輕鬆。 可以與項目關聯的資源類型稱為「AEM磁貼」。 磁貼可包括項目和團隊資訊、資產、工作流和其他類型的資訊，如中所述 [項目磁貼。](#project-tiles)

>[!CAUTION]
>
>對於項目中的用戶，在使用項目功能（如建立項目、建立任務/工作流、查看和管理團隊）時，要查看其他用戶/組，這些用戶需要具有對 `/home/users` 和 `/home/groups`。 實施此策略的最簡單方法是 **項目用戶** 組讀取訪問權限 `/home/users` 和 `/home/groups`。

作為用戶，可以執行以下操作：

* 建立項目
* 將內容和資產資料夾與項目關聯
* 刪除項目
* 從項目中刪除內容連結

請參閱以下附加主題：

* [管理專案](/help/sites-cloud/authoring/projects/managing.md)
* [使用任務](/help/sites-cloud/authoring/projects/tasks.md)
* [使用專案工作流程](/help/sites-cloud/authoring/projects/workflows.md)

## 項目控制台 {#projects-console}

項目控制台是您訪問和管理項目的位AEM置。

![項目控制台](/help/sites-cloud/authoring/assets/projects-console.png)

* 選擇 **時間軸** 然後是一個項目來查看其時間表。
* 按一下/點擊 **選擇** 的子菜單。
* 按一下 **建立** 的子菜單。
* **切換活動項目** 允許您在所有項目之間切換，只在活動的項目之間切換。
* **顯示統計資訊視圖** 用於查看有關任務完成的項目統計資訊。

## 項目磁貼 {#project-tiles}

使用「項目」，可以將不同類型的資訊與項目關聯。 這些稱為 **磁貼**。 本節將介紹每個磁貼及其包含的資訊類型。

您可以擁有與項目關聯的以下磁貼。 下面各節介紹了每項內容：

* 資產和資產收集
* 體驗
* 連結
* 項目資訊
* 團隊
* 著陸頁面
* 電子郵件
* 工作流程
* 啟動
* 任務

### 資產 {#assets}

在 **資產** 平鋪，可以收集用於特定項目的所有資產。

![資產磁貼](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

您直接在磁貼中上載資產。 此外，如果具有「Dynamic Media」附加模組，則可以建立映像集、旋轉集或混合媒體集。

![影像集](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### 資產收集 {#asset-collections}

與資產類似，您可以添加 [資產收集](/help/assets/manage-collections.md) 直接到你的項目。 在資產中定義收款。

![資產收集](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

按一下「新增系列」 **並從清單中選取適當的系列** ，即可新增系列。

### 體驗 {#experiences}

的 **體驗** 磁貼允許您向項目添加Mobile應用、網站或發佈。

![體驗](/help/sites-cloud/authoring/assets/project-experiences.png)

這些圖示會指出所呈現的體驗類型：網站、行動應用程式或出版物。通過點擊或點擊下垂的雪佛龍和敲擊來添加體驗 **添加體驗** 選擇經驗類型。

![添加體驗](/help/sites-cloud/authoring/assets/projects-add-experience.png)

選擇縮略圖的路徑，如果適用，更改體驗的縮略圖。 在 **體驗** 平鋪。

### 連結 {#links}

「連結」磁貼允許您將外部連結與項目關聯。

![連結](/help/sites-cloud/authoring/assets/project-links.png)

可以使用易於識別的名稱命名連結並更改縮略圖。

![添加連結](/help/sites-cloud/authoring/assets/projects-add-link.png)

### 專案資訊 {#project-info}

「項目資訊」磁貼提供有關項目的一般資訊，包括說明、項目狀態（無效或有效）、到期日和成員。 此外，還可以添加項目縮略圖，該縮略圖顯示在主「項目」頁面上。

![項目資訊](/help/sites-cloud/authoring/assets/project-info.png)

可以從此磁貼和「團隊」磁貼中分配和刪除團隊成員（或更改其角色）。

![將團隊成員添加到項目](/help/sites-cloud/authoring/assets/projects-add-team.png)

### 翻譯工作 {#translation-job}

「翻譯作業」磁貼是您開始翻譯的位置，也是您查看翻譯狀態的位置。 要設定翻譯，請參閱 [建立翻譯項目](/help/assets/translate-assets.md)。

![翻譯作業](/help/sites-cloud/authoring/assets/projects-translation-job.png)

按一下 **翻譯作業** 卡以查看翻譯工作流中的資產。 翻譯作業清單還顯示資產元資料和標籤的條目。 這些條目表示還翻譯了資產的元資料和標籤。

![翻譯作業詳細資訊](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### 團隊 {#team}

在此磁貼中，可以指定項目團隊的成員。 編輯時，可以輸入團隊成員的名稱並分配用戶角色。

![團隊磁貼](/help/sites-cloud/authoring/assets/projects-team-tile.png)

您可以添加和刪除團隊成員。 此外，您還可以編輯 [用戶角色](#user-roles-in-a-project) 分配給團隊成員。

![從清單添加團隊](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### 工作流程 {#workflows}

您可以指定項目以遵循某些工作流。 如果有工作流正在運行，則其狀態顯示在 **工作流** 在項目中平鋪。

![工作流程](/help/sites-cloud/authoring/assets/project-workflows.png)

您可以指定項目以遵循某些工作流。 根據您選擇的項目，您有不同的工作流可用。

這些內容在 [使用項目工作流。](/help/sites-cloud/authoring/projects/workflows.md)

### 啟動 {#launches}

「啟動」磁貼顯示已使用 [請求啟動工作流。](/help/sites-cloud/authoring/projects/workflows.md)

![啟動](/help/sites-cloud/authoring/assets/project-launches.png)

### 任務 {#tasks}

任務允許您監視任何與項目相關的任務（包括工作流）的狀態。 有關任務的詳細資訊，請參閱 [使用任務](/help/sites-cloud/authoring/projects/tasks.md)。

![任務](/help/sites-cloud/authoring/assets/projects-tasks.png)

## 項目模板 {#project-templates}

裝AEM有3個不同模板：

* 簡單項目 — 任何不適合其他類別的項目的參考示例（全部捕獲）。 它包括三個基本角色（所有者、編輯和觀察員）和四個工作流（項目批准、請求啟動、請求登錄頁和請求電子郵件）。
* 媒體項目 — 與媒體相關活動的參考示例項目。 它包括幾個與媒體相關的項目角色（攝影師、編輯、文案撰寫人、設計師、所有者和觀察者）。 它還可以請求複製工作流以請求和審閱文本。
* A [翻譯項目](/help/sites-cloud/administering/translation/overview.md)  — 用於管理與翻譯相關的活動的參考示例。 它包括三個基本角色（所有者、編輯和觀察員）。 它包括在「工作流」用戶介面中訪問的兩個工作流。

根據您選擇的模板，您有不同的選項可供您選擇，特別是有關用戶角色和工作流的選項。

## 項目中的用戶角色 {#user-roles-in-a-project}

不同的用戶角色在項目模板中設定，其使用原因有二：

1. 權限. 用戶角色分為以下三個類別之一：觀察者、編輯器、所有者。 例如，攝影師或文案撰寫人將具有與編輯者相同的權限。 權限決定用戶可以對項目中的內容執行什麼操作。
1. 工作流程. 工作流確定項目中為誰分配了任務。 任務可以與項目角色關聯。 例如，可以將任務分配給攝影師，以便所有具有攝影師角色的團隊成員都將獲得該任務。

所有項目都支援以下預設角色，以便您管理安全和控制權限：

| 角色 | 說明 | 權限 | 組成員身份 |
|---|---|---|---|
| 觀察者 | 此角色中的用戶可以查看項目詳細資訊，包括項目狀態。 | 項目的只讀權限 | `workflow-users` 群組 |
| 編輯者 | 此角色中的用戶可以上載和編輯項目的內容。 | 對項目、相關元資料和相關資產的讀寫訪問；上載鏡頭清單以及審核和批准資產的權限；對/etc/commerce寫權限；修改特定項目的權限 | 工作流用戶組 |
| 所有者 | 此角色中的用戶可以啟動項目。 所有者可以建立項目、在項目中啟動工作，還可以將批准的資產移到「生產」資料夾。 儘管項目中的所有其他任務也可由所有者查看和執行。 | 寫入權限 `/etc/commerce` | `dam-users` 組（能夠建立項目）項目 — 管理員組（能夠建立項目和移動資產） |

>[!NOTE]
>
>當您建立專案並將使用者新增至各種角色時，系統會自動建立與專案相關的群組，以管理相關的權限。例如，名為Myproject的專案會有三個群組 **Myproject Owners**、 **Myproject Editors**、 **Myproject Obsertors**。不過，如果刪除專案，這些群組不會自動刪除。管理員需要手動刪除「工具 **>安全** 性 **>** 群組 ****」。
