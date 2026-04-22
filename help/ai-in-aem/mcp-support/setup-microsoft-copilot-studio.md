---
title: 使用AEM MCP設定Microsoft Copilot Studio
description: 瞭解如何設定Microsoft Copilot Studio以連線至AEM MCP伺服器
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: c8e96fe6-1a05-47c0-8215-0c28705e5e48
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# 使用AEM MCP設定Microsoft Copilot Studio {#setup-microsoft-copilot-studio}

請依照下列步驟，將Microsoft Copilot Studio連線至AEM的MCP伺服器。

>[!NOTE]
>
>Microsoft Copilot Studio使用者介面可能會有所變更，且並非決定性。 這些指示僅供說明用途。

1. 在&#x200B;**代理程式**&#x200B;中，啟動流程以新增將使用AEM MCP工具的代理程式。

   * 建立新的代理程式。

   ![Microsoft Copilot Studio中的Agents面板。](assets/copilot-1.png)

1. 開啟該代理程式的工具區域，以便您可以註冊其呼叫外部功能的方式。

   * 瀏覽至工具區段，然後按一下&#x200B;**新增工具**。

   ![Microsoft Copilot Studio中的[新增工具]對話方塊。](assets/copilot-2.png)

1. 決定是要重複使用現有的整合，還是定義新的MCP支援工具。

   * 選取現有工具或建立新工具。

   ![正在選取模型內容通訊協定做為工具型別。](assets/copilot-3.png)

1. 當您建立新的MCP工具時，請繼續進行&#x200B;**模型內容通訊協定**&#x200B;伺服器步驟，包括出現時的預覽模式。

   * 設定指向一或多個AEM MCP伺服器&#x200B;**URL**&#x200B;的新MCP工具。

   ![正在以預覽模式新增模型內容通訊協定伺服器。](assets/copilot-4.png)

1. 定義代理程式到達此MCP端點的方式，包括存取是共用還是專用的。

   * 建立連線，可在代理程式之間&#x200B;**共用**&#x200B;或&#x200B;**專用**。

   ![用來建立新連線的對話方塊。](assets/copilot-5.png)

1. 在&#x200B;**新增並設定**&#x200B;上，提供或確認MCP工具詳細資料，讓代理程式可以存取您的AEM環境。

   ![MCP工具的新增和設定面板。](assets/copilot-6.png)

1. 完成MCP工具表單上的欄位（例如，伺服器&#x200B;**URL**&#x200B;和驗證相關選項）。

   * 選擇性地啟用&#x200B;**自動確認模式**，或針對所有工具互動需要&#x200B;**一般使用者確認**。

   ![MCP工具組態表單。](assets/copilot-7.png)

1. 驗證與MCP伺服器的連線；當Copilot Studio將您重新導向時完成瀏覽器登入。

   * 重新導向時，使用您的&#x200B;**Adobe ID**&#x200B;登入。

   ![正在測試與AEM MCP伺服器的連線。](assets/copilot-8.png)

1. 在執行測試之前，請開啟&#x200B;**管理連線** （或&#x200B;**連線管理員**），並將正確的連線指派給您的工作階段。

   * 測試代理程式時，請先開啟&#x200B;**連線管理員**，將連線指派給您的工作階段。

   ![「管理連線」面板顯示可用的連線。](assets/copilot-9.png)

1. 在測試體驗中，針對您的AEM MCP連線執行代理程式。

   * 測試代理程式時，請在&#x200B;**連線管理員**&#x200B;中指派連線後，按&#x200B;**重試**。

   ![正在使用AEM MCP連線測試代理程式。](assets/copilot-10.png)
