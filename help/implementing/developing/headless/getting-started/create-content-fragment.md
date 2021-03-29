---
title: 建立內容片段無頭快速入門手冊
description: 瞭解如何使用內AEM容片段來設計、建立、組織和使用不受頁面限制的內容，以進行無頭傳送。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 2%

---


# 建立內容片段無頭快速入門手冊{#creating-content-fragments}

瞭解如何使用內AEM容片段來設計、建立、組織和使用不受頁面限制的內容，以進行無頭傳送。

## 什麼是內容片段？{#what-are-content-fragments}

[現在您已建立資產資料](create-assets-folder.md) 夾，可儲存內容片段，您現在可以建立片段！

內容片段可讓您設計、建立、組織和發佈不受頁面影響的內容。 它們可讓您準備內容，以便在多個位置和多個通道上使用。

內容片段包含結構化內容，可以以JSON格式傳送。

## 如何建立內容片段{#how-to-create-a-content-fragment}

內容作者將建立任意數目的內容片段，以代表他們建立的內容。 這將是他們的主要任務AEM。 為了本快速入門手冊的目的，我們只需建立一個指南。

1. 以Cloud ServiceAEM身分登入，並從主功能表選擇&#x200B;**Navigation -> Assets**。
1. 點選或按一下您先前建立的[資料夾。](create-assets-folder.md)
1. 點選或按一下「建立->內容片段&#x200B;**」。**
1. 內容片段的建立會在兩個步驟中顯示為精靈。 首先，選取您要用來建立內容片段的模型，然後點選或按一下「下一步」**。**
   * 可用的模型取決於您為資產資料夾](create-assets-folder.md)定義的&#x200B;[**雲端設定**，您在其中建立內容片段。
   * 如果您收到訊息`We could not find any models`，請檢查資產資料夾的設定。

   ![選取內容片段模型](../assets/content-fragment-model-select.png)
1. 視需要提供&#x200B;**Title**、**Description**&#x200B;和&#x200B;**Tags**，然後點選或按一下「建立&#x200B;**」。**

   ![建立內容片段](../assets/content-fragment-create.png)
1. 點選或按一下確認視窗中的&#x200B;**開啟**。

   ![內容片段已建立確認](../assets/content-fragment-confirmation.png)
1. 在內容片段編輯器中提供內容片段的詳細資訊。

   ![內容片段編輯器](../assets/content-fragment-edit.png)
1. 點選或按一下「儲存並關閉」**。**

內容片段可參照其他內容片段，如有需要，可允許巢狀內容結構。

內容片段也可以參考中的其他AEM資產。 [這些資產必須先儲存在](/help/assets/manage-digital-assets.md) AEM中，才能建立參照的內容片段。

## 後續步驟{#next-steps}

現在您已建立內容片段，您可以繼續進入快速入門手冊的最後部分，並[建立API要求以存取和傳送內容片段。](create-api-request.md)

>[!TIP]
>
>如需管理內容片段的完整詳細資訊，請參閱[內容片段檔案](/help/assets/content-fragments/content-fragments.md)
