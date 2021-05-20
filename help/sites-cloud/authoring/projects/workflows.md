---
title: 使用專案工作流程
description: 各種專案工作流程都可立即使用。
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 15%

---

# 使用專案工作流程 {#working-with-project-workflows}

現成可用的專案工作流程包括下列項目：

* **專案核准工作流程**  — 此工作流程可讓您將內容指派給使用者、檢閱，然後核准。
* **請求啟動**  — 請求啟動的工作流程。
* **要求登錄頁面**  — 此工作流程要求登錄頁面。
* **請求電子郵件**  — 請求電子郵件的工作流程。
* **DAM建立和翻譯復本和DAM建立語言復本**  — 建立資產和資料夾的翻譯二進位檔、中繼資料和標籤。

根據您選取的專案範本，您有特定的工作流程可用：

|  | **簡單專案** | **媒體專案** | **翻譯專案** |
|---|:-:|:-:|:-:|
| 請求副本 |  | x |  |
| 產品像片拍攝 |  | x |  |
| 專案核准 | x |  |  |
| 請求啟動 | x |  |  |
| 要求登陸頁面 | x |  |  |
| 要求電子郵件 | x |  |  |
| DAM Create Language Copy&amp;ast; |  |  | x |
| DAM建立和翻譯語言Copy&amp;ast; |  |  | x |

>[!NOTE]
>
>&amp;ast;這些工作流不是從「專案」的&#x200B;**Workflow**&#x200B;方塊啟動。 請參閱[建立資產的語言副本。](/help/sites-cloud/administering/translation/managing-projects.md)

無論您選擇哪個工作流程，啟動和完成工作流程的步驟都相同。 僅步驟會變更。

您可以直接在「專案」中啟動工作流程（DAM建立語言副本或DAM建立和翻譯語言副本除外）。 有關項目中任何未完成任務的資訊列在&#x200B;**任務**&#x200B;表徵圖中。 需要完成的任務通知會顯示在用戶表徵圖旁邊。

如需在AEM中使用工作流程的詳細資訊，請參閱下列內容：

* [參與工作流程](/help/sites-cloud/authoring/workflows/participating.md)
* [將工作流程套用至頁面](/help/sites-cloud/authoring/workflows/applying.md)
* [設定工作流程](/help/sites-cloud/administering/workflows-administering.md)

本節說明「專案」可用的工作流程。

## 請求複製工作流{#request-copy-workflow}

此工作流程可讓您向使用者請求手稿，然後核准。 要啟動請求複製工作流，請執行以下操作：

1. 在您的媒體專案中，選取「工 **作流程」方塊中的** +登入，然後選取「請求復 **制工作流程」******。
1. 輸入手稿標題，以及您要求的摘要。 如果適用，請輸入目標字數、任務優先順序和到期日。

   ![請求複製工作流](/help/sites-cloud/authoring/assets/projects-request-copy.png)

1. 按一下&#x200B;**建立**。工作流程會開始。 該任務顯示在&#x200B;**任務**&#x200B;表徵圖中。

   ![已新增請求副本](/help/sites-cloud/authoring/assets/projects-request-copy-add.png)

## 項目批准工作流{#project-approval-workflow}

在「專案核准」工作流程中，您會將內容指派給使用者、檢閱，然後核准內容。

1. 在「簡單」項目中，選擇&#x200B;**Workflows**&#x200B;表徵圖中的&#x200B;**`+`**，然後選擇&#x200B;**Project Approval Workflow**。
1. 輸入標題，然後從「團隊」(Team)清單中選擇要為其分配的人員。 如果適用，請輸入說明、內容路徑、任務優先順序和到期日。

   ![請求核准](/help/sites-cloud/authoring/assets/projects-approval.png)

1. 按一下&#x200B;**建立**。工作流程會開始。 該任務顯示在&#x200B;**任務**&#x200B;表徵圖中。

   ![已新增請求核准](/help/sites-cloud/authoring/assets/projects-approval-add.png)

## 請求啟動工作流程{#request-launch-workflow}

此工作流程可讓您要求啟動。

1. 在您的「簡單」專案中，選取「工 **作流程」方塊中的** +登入，然後選取「請求啟 **動工作流程」******。
1. 輸入啟動的標題，並提供啟動來源路徑。 您也可以新增說明和上線日期（如果適用）。 根據您希望啟動的行為方式，選擇「繼承源頁面即時資料」或「排除子頁面」。

   ![請求啟動](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. 按一下&#x200B;**建立**。工作流程會開始。 工作流程會顯示在&#x200B;**Workflows**&#x200B;清單中(按一下點&#x200B;**...**&#x200B;工作流程&#x200B;**圖磚上的**&#x200B;以存取此清單)。

## 建立（和翻譯）資產的語言複製工作流程{#create-and-translate-language-copy-workflow-for-assets}

「建 **立語言復本** 」和「 **** 建立和翻譯語言復本」工作流程在建立資產的語言復本時會有詳細說明。
