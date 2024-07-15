---
title: 語言複製精靈
description: 瞭解如何在AEM中使用語言複製精靈。
feature: Language Copy
role: Admin
exl-id: bf8bdc53-0248-47de-bb9d-c884a7179ab0
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 15%

---

# 語言複製精靈 {#language-copy-wizard}

語言複製精靈是建立和檢測多語言內容結構的引導式體驗。 精靈可讓您輕鬆快速地建立語言副本。

>[!TIP]
>
>如果您不熟悉翻譯內容，請參閱 [Sites 翻譯歷程](/help/journey-sites/translation/overview.md)，此路徑會逐步引導您了解如何使用 AEM 強大的翻譯工具翻譯 AEM Sites 內容，非常適合那些沒有 AEM 或翻譯經驗的使用者。

>[!NOTE]
>
>使用者必須是`project-administrators`群組的成員才能建立網站的語言副本。

若要存取精靈：

1. 在網站主控台中，選取頁面，然後選取&#x200B;**建立**&#x200B;並選取&#x200B;**語言副本**。

   ![從精靈建立語言副本](../assets/language-copy-wizard.png)

1. 精靈會開啟至&#x200B;**選取Source**&#x200B;步驟，您可在此新增/移除頁面。 您也可以選擇包含或排除子頁面。 選取您要包含的頁面，然後選取&#x200B;**下一步**。

   ![使用精靈新增頁面](../assets/language-copy-wizard-add-pages.png)

1. 精靈的&#x200B;**設定**&#x200B;步驟可讓您新增/移除語言並選取翻譯方法。 選取&#x200B;**「下一步」**。

   ![設定精靈的步驟](../assets/language-copy-wizard-configure.png)

   >[!NOTE]
   >
   >依預設，只有一個翻譯設定。 若要能夠選取其他設定，您必須先設定雲端設定。 請參閱[設定翻譯整合架構](integration-framework.md)。

1. 在精靈的&#x200B;**翻譯**&#x200B;步驟中，您可以選擇僅建立結構、建立翻譯專案或新增到現有的翻譯專案。

   >[!NOTE]
   >
   >如果您在上一步中選取了多種語言，則會建立多個翻譯專案。

   精靈的![翻譯步驟](../assets/language-copy-wizard-translate.png)

1. **建立**&#x200B;按鈕會結束精靈。 選取&#x200B;**完成**&#x200B;以關閉精靈，或選取&#x200B;**開啟**&#x200B;以檢視產生的翻譯專案。

   ![結束精靈](../assets/language-copy-wizard-done.png)
