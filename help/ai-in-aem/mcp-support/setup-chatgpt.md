---
title: 使用AEM MCP設定OpenAI ChatGPT
description: 瞭解如何設定OpenAI ChatGPT以連線至AEM MCP伺服器
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 1f116225-168b-483c-9df6-c752a573b57b
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 使用AEM MCP設定OpenAI ChatGPT {#setup-chatgpt}

請依照下列步驟，將OpenAI ChatGPT連線至AEM的MCP伺服器。

* 在設定MCP連線或工具的區域中新增一或多個AEM MCP伺服器URL。
* 在重新導向時，觸發連線並使用您的Adobe ID登入。
* 在聊天中，在提示中參考已設定的AEM工具，例如：

  ```
  "Using the configured AEM MCP tools, list all sites in the author environment."
  ```

>[!NOTE]
>
>OpenAI ChatGPT使用者介面可能會有所變更，且不是決定性的。 這些指示僅供說明用途。

1. 開啟&#x200B;**設定**，以便您可以連線到設定MCP連線或工具的區域。

   ![ChatGPT設定對話方塊。](assets/chatgpt-1.png)

1. 在&#x200B;**應用程式和聯結器**&#x200B;中，開啟&#x200B;**進階設定**&#x200B;以管理聯結器和MCP相關選項。

   ![ChatGPT中的[應用程式和聯結器進階設定]面板。](assets/chatgpt-2.png)

1. 在&#x200B;**應用程式和聯結器**&#x200B;中啟用&#x200B;**開發人員模式**，以便您可以新增和設定自訂應用程式或聯結器。

   ![正在啟用應用程式和聯結器區段中的開發人員模式。](assets/chatgpt-3.png)

1. 啟動&#x200B;**建立新的應用程式** （或同等的控制項），為您的AEM MCP伺服器新增應用程式專案。

   ![在ChatGPT中建立新應用程式的對話方塊。](assets/chatgpt-4.png)

1. 完成&#x200B;**新增應用程式**&#x200B;表單 — 例如，命名應用程式並輸入您的AEM MCP伺服器URL和任何其他必要欄位 — 然後&#x200B;**儲存**。

   ![ChatGPT中的新應用程式設定表單。](assets/chatgpt-5.png)

1. 確認&#x200B;**AEM內容MCP服務** （或您設定的應用程式）出現在&#x200B;**應用程式和聯結器**&#x200B;中，讓ChatGPT能夠使用它。

   ![應用程式和聯結器中列出的AEM內容MCP服務。](assets/chatgpt-6.png)

1. 在聊天中，撰寫提示以通知ChatGPT使用設定的&#x200B;**AEM工具** （例如，查詢作者內容或網站）。

   ![提示ChatGPT使用AEM內容MCP服務。](assets/chatgpt-7.png)
