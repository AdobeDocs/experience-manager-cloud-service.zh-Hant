---
title: 使用GitHub Copilot和AEM MCP設定JetBrains
description: 瞭解如何在JetBrains IDE中設定GitHub Copilot以連線至AEM MCP伺服器
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: e153da42-51e0-49ea-8457-10bb5e77e2de
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 1%

---

# 使用GitHub Copilot和AEM MCP設定JetBrains {#setup-jetbrains-copilot}

請依照下列步驟，在JetBrains IDE （例如IntelliJ IDEA、WebStorm或PyCharm）中將GitHub Copilot連線至AEM的MCP伺服器。

1. 按一下編輯器右側的&#x200B;**GitHub Copilot Chat**&#x200B;圖示，在JetBrains IDE中開啟GitHub Copilot Chat。

   ![已開啟GitHub Copilot Chat的JetBrains IDE。](assets/jetbrains-copilot-1.png)

1. 按一下Copilot Chat面板中的&#x200B;**設定**&#x200B;圖示以開啟MCP設定。

   ![反白顯示設定圖示的GitHub Copilot聊天面板。](assets/jetbrains-copilot-2.png)

1. 在&#x200B;**設定**&#x200B;中，瀏覽至&#x200B;**工具> GitHub Copilot >模型內容通訊協定(MCP)**，然後按一下&#x200B;**設定**&#x200B;以開啟`mcp.json`設定檔。

   ![顯示GitHub Copilot下模型內容通訊協定(MCP)組態的JetBrains設定對話方塊。](assets/jetbrains-copilot-3.png)

1. 將一或多個AEM MCP伺服器URL新增至`mcp.json`檔案。 例如：

   ```json
   {
     "servers": {
       "aem": {
         "url": "https://mcp.adobeaemcloud.com/adobe/mcp/content"
       }
     }
   }
   ```


   ![具有AEM MCP伺服器URL的mcp.json設定檔。](assets/jetbrains-copilot-4.png)


1. 儲存檔案。GitHub Copilot會自動偵測新的伺服器設定，並顯示&#x200B;**啟動**&#x200B;動作。

   ![mcp.json檔案顯示設定的AEM伺服器包含偵測到的工具。](assets/jetbrains-copilot-5.png)

1. 按一下&#x200B;**開始**&#x200B;動作，然後在出現提示時，使用您的Adobe ID登入以完成驗證流程。

1. 您可以按一下Copilot Chat面板中顯示的&#x200B;**tools**&#x200B;指示器，檢閱和管理發現的工具。 可選擇啟用或停用個別工具。


   ![[設定工具]對話方塊顯示可用的AEM MCP工具。](assets/jetbrains-copilot-6.png)

1. 使用GitHub Copilot Chat，叫用AEM工具作為開發或內容工作流程的一部分。
