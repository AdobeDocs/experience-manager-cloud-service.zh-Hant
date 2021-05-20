---
title: 建立內容片段無頭快速入門手冊
description: 了解如何使用AEM內容片段來設計、建立、組織及使用無頭式傳送的獨立於頁面的內容。
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: 088fa5c90d549c52ca2832bd026be4fcddb31b78
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---

# 建立內容片段無頭快速入門手冊{#creating-content-fragments}

了解如何使用AEM內容片段來設計、建立、組織及使用無頭式傳送的獨立於頁面的內容。

## 什麼是內容片段？{#what-are-content-fragments}

[現在您已建立可儲存內](create-assets-folder.md) 容片段的資產資料夾，可以建立片段了！

內容片段可讓您設計、建立、組織和發佈不受頁面影響的內容。 它們可讓您準備內容，以便在多個位置和多個頻道中使用。

內容片段包含結構化內容，可以以JSON格式傳送。

## 如何建立內容片段{#how-to-create-a-content-fragment}

內容作者將建立任意數量的內容片段，以代表其建立的內容。 這將是他們在AEM中的主要工作。 為了方便閱讀快速入門手冊，我們只需建立指南。

1. 以Cloud Service身分登入AEM，然後在主功能表中選取&#x200B;**導覽 — >資產**。
1. 點選或按一下您先前建立的[資料夾。](create-assets-folder.md)
1. 點選或按一下「**建立 — >內容片段**」。
1. 建立內容片段會以精靈的形式呈現，分為兩個步驟。 首先，選取您要使用哪個模型來建立內容片段，然後點選或按一下「**Next**」。
   * 可用的模型取決於您為要建立內容片段的資產資料夾](create-assets-folder.md)定義的&#x200B;[**雲端設定**。
   * 如果您收到訊息`We could not find any models`，請檢查資產資料夾的設定。

   ![選取內容片段模型](../assets/content-fragment-model-select.png)
1. 視需要提供&#x200B;**Title**、**Description**&#x200B;和&#x200B;**Tags**，然後點選或按一下&#x200B;**Create**。

   ![建立內容片段](../assets/content-fragment-create.png)
1. 點選或按一下確認視窗中的&#x200B;**開啟**。

   ![內容片段已建立確認](../assets/content-fragment-confirmation.png)
1. 在內容片段編輯器中提供內容片段的詳細資訊。

   ![內容片段編輯器](../assets/content-fragment-edit.png)
1. 點選或按一下「**儲存**」或「**儲存並關閉**」。

內容片段可參考其他內容片段，以視需要允許巢狀內容結構。

內容片段也可以參考AEM中的其他資產。 [建立參考內容片段之前，](/help/assets/manage-digital-assets.md) 這些資產必須儲存在AEM中。

## 後續步驟{#next-steps}

現在您已建立內容片段，您可以繼續前往快速入門手冊的最後一部分，以及[建立API請求以存取和傳送內容片段。](create-api-request.md)

>[!TIP]
>
>如需管理內容片段的完整詳細資訊，請參閱[內容片段檔案](/help/assets/content-fragments/content-fragments.md)
