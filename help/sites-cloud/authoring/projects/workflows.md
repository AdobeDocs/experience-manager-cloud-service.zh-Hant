---
title: 使用專案工作流程
description: 各種專案工作流程都可立即使用。
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 8%

---

# 使用專案工作流程 {#working-with-project-workflows}

現成可用的專案工作流程包括下列專案：

* **專案核准工作流程**  — 此工作流程可讓您將內容指派給使用者、檢閱，然後核准。
* **請求啟動**  — 要求啟動的工作流程。
* **請求登陸頁面**  — 此工作流程會要求登入頁面。
* **要求電子郵件**  — 要求電子郵件的工作流程。
* **DAM建立和翻譯副本及DAM建立語言副本**  — 為資產和資料夾建立翻譯的二進位檔案、中繼資料和標籤。

根據您選取的專案範本，您有特定的工作流程可用：

|   | **簡單專案** | **翻譯專案** |
|---|:-:|:-:|
| 專案核准工作流程 | x |  |
| 請求啟動 | x |  |
| 請求登陸頁面 | x |  |
| 要求電子郵件 | x | |
| DAM建立語言副本&amp;ast； |  | x |
| DAM建立和翻譯語言副本&amp;ast； |   | x |

>[!NOTE]
>
>&amp;ast；這些工作流程不會從 **工作流程** 圖磚（在專案中）。 另請參閱 [建立資產的語言副本](/help/sites-cloud/administering/translation/managing-projects.md).

無論您選擇哪個工作流程，開始和完成工作流程的步驟都相同。 只有步驟會變更。

您直接在「專案」中啟動工作流程（「DAM建立語言副本」或「DAM建立和翻譯語言副本」除外）。 專案中任何未完成任務的資訊會列在 **任務** 圖磚。 使用者圖示旁會顯示需要完成之工作的通知。

如需在AEM中使用工作流程的詳細資訊，請參閱下列內容：

* [參與工作流程](/help/sites-cloud/authoring/workflows/participating.md)
* [將工作流程套用至頁面](/help/sites-cloud/authoring/workflows/applying.md)
* [設定工作流程](/help/sites-cloud/administering/workflows-administering.md)

本節說明專案可用的工作流程。

## 專案核准工作流程 {#project-approval-workflow}

在「專案核准」工作流程中，您可以將內容指派給使用者、檢閱，然後核准內容。

1. 在您的簡單專案中，選取 **`+`** 登入 **工作流程** 並選取 **專案核准工作流程**.
1. 輸入標題，並從「專案團隊」清單中選取指派給誰。 如果適用，請輸入說明、內容路徑、工作優先順序和到期日。

   ![請求核准](/help/sites-cloud/authoring/assets/projects-approval.png)

1. 按一下&#x200B;**建立**。工作流程隨即開始。 任務會出現在 **任務** 圖磚。

## 請求啟動工作流程 {#request-launch-workflow}

此工作流程可讓您請求啟動。

1. 在您的「簡單」專案中，選取「工 **作流程」方塊中的** +登入，然後選取「請求啟 **動工作流程」******。
1. 輸入啟動項的標題並提供啟動項來源路徑。 您也可以新增說明和上線日期（如適用）。 選取繼承來源頁面即時資料或排除子頁面（取決於您希望啟動項的行為）。

   ![要求啟動](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. 按一下&#x200B;**建立**。工作流程隨即開始。 工作流程會顯示在 **工作流程** 清單(按一下省略符號 **...** 於 **工作流程** 並排顯示)。

## 建立（及翻譯）資產的語言副本工作流程 {#create-and-translate-language-copy-workflow-for-assets}

此 **建立語言副本** 和 **建立和翻譯語言副本** 中詳細介紹了工作流程 [建立資產的語言副本](/help/assets/translate-assets.md).
