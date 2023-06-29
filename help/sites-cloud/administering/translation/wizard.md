---
title: 語言複製精靈
description: 瞭解如何在AEM中使用語言複製精靈。
feature: Language Copy
role: Admin
exl-id: bf8bdc53-0248-47de-bb9d-c884a7179ab0
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 3%

---

# 語言複製精靈 {#language-copy-wizard}

語言複製精靈是建立和檢測多語言內容結構的引導式體驗。 精靈可讓您輕鬆快速地建立語言副本。

>[!TIP]
>
>如果您不熟悉翻譯內容，請參閱 [網站翻譯歷程，](/help/journey-sites/translation/overview.md) 將引導您使用AEM強大的翻譯工具來翻譯AEM Sites內容，非常適合沒有AEM或翻譯經驗的人士。

>[!NOTE]
>
>使用者必須是 `project-administrators` 群組，以建立網站的語言副本。

若要存取精靈：

1. 在網站主控台中，選取頁面並點選或按一下 **建立** 並選取 **語言副本**.

   ![從精靈建立語言副本](../assets/language-copy-wizard.png)

1. 精靈會開啟並顯示 **選取來源** 可讓您新增/移除頁面的步驟。 您也可以選擇包含或排除子頁面。 選取您要包含的頁面，然後點選或按一下 **下一個**.

   ![使用精靈新增頁面](../assets/language-copy-wizard-add-pages.png)

1. 此 **設定** 精靈的步驟可讓您新增/移除語言並選取翻譯方法。 點選或按一下&#x200B;**下一步**。

   ![精靈的設定步驟](../assets/language-copy-wizard-configure.png)

   >[!NOTE]
   >
   >依預設，只有一個翻譯設定。 若要能夠選取其他設定，您必須先設定雲端設定。 另請參閱 [設定翻譯整合架構](integration-framework.md).

1. 在 **轉換** 精靈的步驟您可以選擇僅建立結構、建立新翻譯專案或新增到現有翻譯專案。

   >[!NOTE]
   >
   >如果您在上一個步驟中選取了多種語言，則會建立多個翻譯專案。

   ![精靈的翻譯步驟](../assets/language-copy-wizard-translate.png)

1. 此 **建立** 按鈕結束精靈。 點選或按一下 **完成** 關閉精靈或 **開啟** 以檢視產生的翻譯專案。

   ![結束精靈](../assets/language-copy-wizard-done.png)
