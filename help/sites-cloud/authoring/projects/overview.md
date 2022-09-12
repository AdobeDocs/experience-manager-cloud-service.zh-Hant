---
title: 專案
description: 專案可讓您將資源分組為一個實體，其共同的共用環境可讓您輕鬆管理專案
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
source-git-commit: 8ea043b4b6424d6922c41c143ca74fd25ac60cf8
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 11%

---

# 專案 {#projects}

專案可讓您將資源分組為一個實體。 共用的共用環境讓您輕鬆管理專案。 您可與專案關聯的資源類型在AEM中以圖磚形式參照。 圖磚可包含專案和團隊資訊、資產、工作流程和其他類型的資訊，如 [專案圖磚。](#project-tiles)

>[!CAUTION]
>
>如果專案中的使用者在使用專案功能（例如建立專案、建立工作/工作流程、查看及管理團隊）時要查看其他使用者/群組，這些使用者必須擁有的讀取存取權 `/home/users` 和 `/home/groups`. 實作此項目最簡單的方式是提供 **專案 — 使用者** 群組讀取存取權 `/home/users` 和 `/home/groups`.

身為使用者，您可以執行下列動作：

* 建立專案
* 將內容和資產資料夾關聯至專案
* 刪除專案
* 從專案移除內容連結

請參閱下列其他主題：

* [管理專案](/help/sites-cloud/authoring/projects/managing.md)
* [使用任務](/help/sites-cloud/authoring/projects/tasks.md)
* [使用專案工作流程](/help/sites-cloud/authoring/projects/workflows.md)

## 專案主控台 {#projects-console}

專案主控台是您在AEM中存取及管理專案的位置。

![專案主控台](/help/sites-cloud/authoring/assets/projects-console.png)

* 選擇 **時間表** 然後是一個項目來查看時間表。
* 按一下/點選 **選擇** ，以進入選擇模式。
* 按一下 **建立** 來新增專案。
* **切換作用中的專案** 可讓您在所有專案和使用中專案之間切換。
* **顯示統計資訊視圖** 可讓您查看有關任務完成的項目統計資訊。

## 專案圖磚 {#project-tiles}

使用「專案」，可將不同類型的資訊與專案建立關聯。 這些稱為 **圖磚**. 本節將說明每個圖磚及其包含的資訊類型。

您可以有下列圖磚與您的專案相關聯。 以下各節將分別說明各項：

* 資產和資產集合
* 體驗
* 連結
* 專案資訊
* 團隊
* 著陸頁面
* 電子郵件
* 工作流程
* 啟動
* 任務

### Assets {#assets}

在 **資產** 圖磚，您可以收集用於特定專案的所有資產。

![資產圖磚](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

您直接在圖磚中上傳資產。 此外，如果您有Dynamic Media附加元件，也可以建立影像集、回轉集或混合媒體集。

![影像集](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### 資產集合 {#asset-collections}

與資產類似，您可以新增 [資產集合](/help/assets/manage-collections.md) 直接傳至您的專案。 您可以在資產中定義集合。

![資產集合](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

按一下「新增系列」 **並從清單中選取適當的系列** ，即可新增系列。

### 體驗 {#experiences}

此 **體驗** 圖磚可讓您新增行動應用程式、網站或出版物至專案。

![體驗](/help/sites-cloud/authoring/assets/project-experiences.png)

這些圖示會指出所呈現的體驗類型：網站、行動應用程式或出版物。點選或按一下向下>形並點選以新增體驗 **新增體驗** 和選取體驗類型。

![新增體驗](/help/sites-cloud/authoring/assets/projects-add-experience.png)

選取縮圖的路徑，並變更體驗的縮圖（若適用）。 體驗會分組在 **體驗** 方塊。

### 連結 {#links}

「連結」方塊可讓您將外部連結與專案建立關聯。

![連結](/help/sites-cloud/authoring/assets/project-links.png)

您可以使用易於識別的名稱來命名連結，並變更縮圖。

![新增連結](/help/sites-cloud/authoring/assets/projects-add-link.png)

### 專案資訊 {#project-info}

「項目資訊」(Project Information)表徵圖提供有關項目的一般資訊，包括說明、項目狀態（非活動或活動）、到期日和成員。 此外，您可以新增專案縮圖，該縮圖會顯示在主「專案」頁面上。

![專案資訊](/help/sites-cloud/authoring/assets/project-info.png)

可以從此表徵圖（或更改其角色）和「團隊」表徵圖中分配和刪除團隊成員。

![將團隊成員添加到項目](/help/sites-cloud/authoring/assets/projects-add-team.png)

### 翻譯工作 {#translation-job}

「翻譯工作」方塊是您開始翻譯的位置，也是您查看翻譯狀態的位置。 若要設定翻譯，請參閱 [建立翻譯專案](/help/assets/translate-assets.md).

![翻譯工作](/help/sites-cloud/authoring/assets/projects-translation-job.png)

按一下 **翻譯工作** 卡片以在翻譯工作流程中檢視資產。 翻譯工作清單也會顯示資產中繼資料和標籤的項目。 這些項目表示資產的中繼資料和標籤也會翻譯。

![翻譯工作詳細資料](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### 團隊 {#team}

在此圖磚中，您可以指定專案團隊的成員。 編輯時，您可以輸入團隊成員的名稱並分配用戶角色。

![團隊圖磚](/help/sites-cloud/authoring/assets/projects-team-tile.png)

您可以從團隊中添加和刪除團隊成員。 此外，您也可以編輯 [使用者角色](#user-roles-in-a-project) 已指派給團隊成員。

![從清單中添加團隊](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### 工作流程 {#workflows}

您可以指派專案以遵循特定工作流程。 如果有任何工作流程在執行中，其狀態會顯示在 **工作流程** 標題。

![工作流程](/help/sites-cloud/authoring/assets/project-workflows.png)

您可以指派專案以遵循特定工作流程。 視您選擇的專案而定，您有不同的可用工作流程。

這些說明於 [使用專案工作流程。](/help/sites-cloud/authoring/projects/workflows.md)

### 啟動 {#launches}

「啟動」方塊會顯示已透過 [請求啟動工作流程。](/help/sites-cloud/authoring/projects/workflows.md)

![啟動](/help/sites-cloud/authoring/assets/project-launches.png)

### 任務 {#tasks}

任務可讓您監視任何專案相關任務的狀態，包括工作流程。 有關任務的詳細說明，請訪問 [使用任務](/help/sites-cloud/authoring/projects/tasks.md).

![任務](/help/sites-cloud/authoring/assets/projects-tasks.png)

## 專案範本 {#project-templates}

AEM隨附三個不同的範本：

* 簡單專案 — 任何不符合其他類別（包羅永珍）的專案的參考範例。 它包含三個基本角色（擁有者、編輯者和觀察者）和四個工作流程（專案核准、請求啟動、請求登錄頁面和請求電子郵件）。
* 媒體專案 — 媒體相關活動的參考範例專案。 它包含數個與媒體相關的專案角色（攝影師、編輯、文案撰寫者、設計師、擁有者和觀察者）。 它也提供「請求複製」工作流程以請求和檢閱文字。
* A [翻譯專案](/help/sites-cloud/administering/translation/overview.md)  — 管理翻譯相關活動的參考範例。 它包含三個基本角色（擁有者、編輯和觀察者）。 它包含可在工作流程使用者介面中存取的兩個工作流程。

根據您選取的範本，您有不同的選項可供使用，尤其是使用者角色和工作流程。

## 專案中的使用者角色 {#user-roles-in-a-project}

不同的使用者角色會在專案範本中設定，其使用原因有二：

1. 權限. 使用者角色分為下列三個類別之一：觀察者、編輯者、擁有者。 例如，攝影師或文案撰寫者具有與編輯者相同的權限。 權限會決定使用者可以對專案中的內容執行什麼動作。
1. 工作流程. 工作流程會決定專案中指派工作的人員。 這些任務可以與項目角色相關聯。 例如，任務可以分配給Photogrepers，因此具有Photogrepher角色的所有團隊成員都將獲得該任務。

所有專案都支援下列預設角色，可讓您管理安全性和控制權限：

| 角色 | 說明 | 權限 | 群組成員資格 |
|---|---|---|---|
| 觀察者 | 此角色的使用者可以檢視專案詳細資訊，包括專案狀態。 | 專案的唯讀權限 | `workflow-users` 群組 |
| 編輯者 | 此角色的使用者可以上傳和編輯專案的內容。 | 對專案、相關中繼資料和相關資產的讀取和寫入存取權；上傳快照清單，以及審核和核准資產的權限；/etc/commerce的寫權限；修改特定專案的權限 | 工作流程使用者群組 |
| 擁有者 | 此角色的使用者可以起始專案。 擁有者可以建立專案、起始專案中的工作，以及將已核准的資產移至生產資料夾。 雖然項目中的所有其他任務也可以由所有者查看和執行。 | 寫入權限 `/etc/commerce` | `dam-users` 群組（以建立專案）專案管理員群組（以便建立專案和移動資產） |

>[!NOTE]
>
>當您建立專案並將使用者新增至各種角色時，系統會自動建立與專案相關的群組，以管理相關的權限。例如，名為Myproject的專案會有三個群組 **Myproject Owners**、 **Myproject Editors**、 **Myproject Obsertors**。不過，如果刪除專案，這些群組不會自動刪除。管理員需要手動刪除「工具 **>安全** 性 **>** 群組 ****」。
