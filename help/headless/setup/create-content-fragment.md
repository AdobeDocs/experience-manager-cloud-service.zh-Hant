---
title: 建立內容片段 — 無頭設定
description: 了解如何使用AEM內容片段來設計、建立、組織及使用無頭式傳送的獨立於頁面的內容。
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: d6038920a5866c19a94980cc14fa46dec48daf51
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 建立內容片段 — 無頭設定 {#creating-content-fragments}

了解如何使用AEM內容片段來設計、建立、組織及使用無頭式傳送的獨立於頁面的內容。

## 什麼是內容片段？ {#what-are-content-fragments}

[現在您已建立資產資料夾](create-assets-folder.md) 您現在可以在其中儲存內容片段！

內容片段可讓您設計、建立、組織和發佈不受頁面影響的內容。 它們可讓您準備內容，以便在多個位置和多個頻道中使用。

內容片段包含結構化內容，可以以JSON格式傳送。

## 如何建立內容片段 {#how-to-create-a-content-fragment}

內容作者將建立任意數量的內容片段，以代表其建立的內容。 這將是他們在AEM中的主要工作。 為了方便閱讀快速入門手冊，我們只需建立指南。

1. 登入AEMas a Cloud Service，然後從主功能表選取 **導覽** -> **內容片段**.

1. 點選或按一下 [檔案夾。](create-assets-folder.md)
1. 點選或按一下 **建立**.
1. 內容片段的建立會以對話方塊呈現。
選取您要用來建立內容片段的位置和模型。

   * 可用的模型取決於 [**雲端設定** 您為「資產」資料夾定義](create-assets-folder.md) 建立內容片段時所使用的ID。
   * 如果您的模型無法使用，請檢查資產資料夾的設定。

   新增「標題」、「名稱」，並視需要新增「說明」。

   ![建立新內容片段對話方塊](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

1. 點選或按一下 **建立** 或  **建立和開啟**.

內容片段可參考其他內容片段，以視需要允許巢狀內容結構。

內容片段也可以參考AEM中的其他資產。 [這些資產需要儲存在AEM](/help/assets/manage-digital-assets.md) 建立參考內容片段之前。

## 後續步驟 {#next-steps}

現在您已建立內容片段，可以繼續前往快速入門手冊的最後部分，以及 [建立API請求以存取及傳送內容片段。](create-api-request.md)

>[!TIP]
>
>如需管理內容片段的完整詳細資訊，請參閱 [內容片段檔案](/help/sites-cloud/administering/content-fragments/content-fragments.md)
