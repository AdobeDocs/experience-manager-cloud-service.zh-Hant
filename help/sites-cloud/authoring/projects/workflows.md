---
title: 使用專案工作流程
description: 各種專案工作流程都可立即使用。
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 7%

---

# 使用專案工作流程 {#working-with-project-workflows}

現成可用的專案工作流程包括下列專案：

* **專案核准工作流程** — 此工作流程可讓您指派內容給使用者、檢閱及核准。
* **要求啟動** — 要求啟動的工作流程。
* **要求登陸頁面** — 此工作流程會要求登陸頁面。
* **要求電子郵件** — 要求電子郵件的工作流程。
* **DAM建立和翻譯復本及DAM建立語言復本** — 為資產和資料夾建立翻譯的二進位檔、中繼資料和標籤。

根據您選取的專案範本，您有特定可用的工作流程：

|   | **簡單專案** | **翻譯專案** |
|---|:-:|:-:|
| 專案核准工作流程 | x |  |
| 要求啟動 | x |  |
| 請求登陸頁面 | x |  |
| 要求電子郵件 | x | |
| DAM建立語言副本&amp;amp；ast； |  | x |
| DAM建立及翻譯語言副本&amp;amp；ast； |   | x |

>[!NOTE]
>
>&amp;amp；ast；這些工作流程並非從專案中的&#x200B;**工作流程**&#x200B;圖磚開始。 請參閱[建立Assets的語言復本](/help/sites-cloud/administering/translation/managing-projects.md)。

無論您選擇哪個工作流程，開始和完成工作流程的步驟都相同。 只有步驟會變更。

您直接在專案中啟動工作流程（DAM建立語言副本或DAM建立和翻譯語言副本除外）。 有關專案中所有未完成任務的資訊會列在&#x200B;**任務**&#x200B;圖磚中。 使用者圖示旁會顯示需要完成之工作的通知。

如需在AEM中使用工作流程的詳細資訊，請參閱下列內容：

* [參與工作流程](/help/sites-cloud/authoring/workflows/participating.md)
* [將工作流程套用至頁面](/help/sites-cloud/authoring/workflows/applying.md)
* [設定工作流程](/help/sites-cloud/administering/workflows-administering.md)

本節說明專案可用的工作流程。

## 專案核准工作流程 {#project-approval-workflow}

在「專案核准」工作流程中，您可以將內容指派給使用者、檢閱，然後核准內容。

1. 在您的簡單專案中，選取&#x200B;**工作流程**&#x200B;方塊中的&#x200B;**`+`**&#x200B;登入，然後選取&#x200B;**專案核准工作流程**。
1. 輸入標題，並從「專案團隊」清單中選取要指派給它的使用者。 如果適用，請輸入說明、內容路徑、工作優先順序和到期日。

   ![要求核准](/help/sites-cloud/authoring/assets/projects-approval.png)

1. 按一下「**建立**」。工作流程隨即開始。 任務會出現在&#x200B;**任務**&#x200B;拼貼中。

## 請求啟動工作流程 {#request-launch-workflow}

此工作流程可讓您請求啟動。

1. 在您的「簡單」專案中，選取「工 **作流程」方塊中的** +登入，然後選取「請求啟 **動工作流程」**&#x200B;**&#x200B;**。
1. 輸入啟動的標題並提供啟動來源路徑。 您也可以新增說明和上線日期（如適用）。 根據您想要啟動項的行為，選取「繼承來源頁面即時資料」或「排除子頁面」 。

   ![要求啟動](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. 按一下「**建立**」。工作流程隨即開始。 工作流程出現在&#x200B;**工作流程**&#x200B;清單中（按一下&#x200B;**工作流程**&#x200B;方塊上的省略符號&#x200B;**...**&#x200B;以存取此清單）。

## 建立（及翻譯）Assets的語言副本工作流程 {#create-and-translate-language-copy-workflow-for-assets}

**建立語言副本**&#x200B;和&#x200B;**建立和翻譯語言副本**&#x200B;工作流程在[建立資產的語言副本](/help/assets/translate-assets.md)中有詳細介紹。
