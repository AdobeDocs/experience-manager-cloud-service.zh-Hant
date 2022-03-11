---
title: 使用專案工作流程
description: 各種項目工作流都可開箱即用。
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 89972691dadb9573160ba16a220c5b7cb3ae9742
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 8%

---

# 使用專案工作流程 {#working-with-project-workflows}

現成的項目工作流包括以下內容：

* **項目審批工作流**  — 此工作流允許您將內容分配給用戶、審閱和批准。
* **請求啟動**  — 請求啟動的工作流。
* **請求登錄頁**  — 此工作流請求登錄頁。
* **請求電子郵件**  — 請求電子郵件的工作流。
* **DAM建立和翻譯副本和DAM建立語言副本**  — 為資產和資料夾建立已轉換的二進位檔案、元資料和標籤。

根據您選擇的項目模板，您可以使用某些工作流：

|  | **簡單專案** | **翻譯專案** |
|---|:-:|:-:|
| 項目審批工作流 | x |  |
| 請求啟動 | x |  |
| 請求登錄頁 | x |  |
| 請求電子郵件 | x |  |
| &amp;DAM建立語言複製； |  | x |
| &amp;DAM建立和翻譯語言副本； |  | x |

>[!NOTE]
>
>&amp;ast;這些工作流不是從 **工作流** 在項目中平鋪。 請參閱 [為資產建立語言副本。](/help/sites-cloud/administering/translation/managing-projects.md)

無論您選擇哪個工作流，啟動和完成工作流的步驟都相同。 只有步驟會改變。

您可以直接在項目中啟動工作流（DAM建立語言副本或DAM建立和翻譯語言副本除外）。 有關項目中任何未完成任務的資訊列於 **任務** 平鋪。 需要完成的任務的通知顯示在用戶表徵圖旁邊。

有關使用中的工作流的詳細信AEM息，請參閱：

* [參與工作流](/help/sites-cloud/authoring/workflows/participating.md)
* [將工作流應用於頁面](/help/sites-cloud/authoring/workflows/applying.md)
* [配置工作流](/help/sites-cloud/administering/workflows-administering.md)

本節介紹可用於項目的工作流。

## 項目審批工作流 {#project-approval-workflow}

在「項目審批」工作流中，您可以將內容分配給用戶、審閱並審批內容。

1. 在「簡單」項目中，選擇 **`+`** 登錄 **工作流** 平鋪和選擇 **項目審批工作流**。
1. 輸入標題，然後從「團隊」(Team)清單中選擇將其分配給誰。 如果適用，請輸入說明、內容路徑、任務優先順序和到期日期。

   ![請求批准](/help/sites-cloud/authoring/assets/projects-approval.png)

1. 按一下&#x200B;**建立**。工作流將啟動。 任務將出現在 **任務** 平鋪。

## 請求啟動工作流 {#request-launch-workflow}

此工作流允許您請求啟動。

1. 在您的「簡單」專案中，選取「工 **作流程」方塊中的** +登入，然後選取「請求啟 **動工作流程」******。
1. 輸入啟動的標題並提供啟動源路徑。 如果適用，還可以添加說明和即時日期。 根據您希望啟動的行為方式選擇「繼承源頁即時資料」或「排除子頁」。

   ![請求啟動](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. 按一下&#x200B;**建立**。工作流將啟動。 工作流將出現在 **工作流** 清單（按一下省略） **...** 的 **工作流** 磁貼以訪問此清單)。

## 為資產建立（和翻譯）語言複製工作流 {#create-and-translate-language-copy-workflow-for-assets}

的 **建立語言副本** 和 **建立和翻譯語言副本** 詳細介紹工作流 [為資產建立語言副本。](/help/assets/translate-assets.md)
