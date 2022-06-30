---
title: 建立內容片段 — 無頭設定
description: 瞭解如何使用內AEM容片段來設計、建立、建立和使用與頁面無關的內容進行無頭傳送。
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: c0b48db0cbef6232f153dc59432ea7289b430538
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 建立內容片段 — 無頭設定 {#creating-content-fragments}

瞭解如何使用內AEM容片段來設計、建立、建立和使用與頁面無關的內容進行無頭傳送。

## 什麼是內容片段？ {#what-are-content-fragments}

[現在您已建立資產資料夾](create-assets-folder.md) 您可以在其中儲存內容片段，現在可以建立片段！

內容片段允許您設計、建立、建立和發佈與頁面無關的內容。 它們使您能夠準備內容，以便在多個位置和多個渠道中使用。

內容片段包含結構化內容，可以以JSON格式傳送。

## 如何建立內容片段 {#how-to-create-a-content-fragment}

內容作者將建立任意數量的內容片段來表示他們建立的內容。 這將是他們的主要任AEM務。 為本入門指南的目的，我們只需建立一個。

1. 登錄AEM到as a Cloud Service並從主菜單選擇 **導航** -> **內容片段**。

1. 點擊或按一下 [資料夾。](create-assets-folder.md)
1. 點擊或按一下 **建立**。
1. 內容片段的建立將作為對話框顯示。
選擇要用於建立內容片段的位置和模型。

   * 可用型號取決於 [**雲配置** 為「資產」資料夾定義的](create-assets-folder.md) 建立內容片段。
   * 如果模型不可用，請檢查資產資料夾的配置。

   添加標題、名稱，並根據需要添加說明。

   ![「新建內容片段」對話框](/help/headless/content-fragments/assets/cfc-console-create.png)

1. 點擊或按一下 **建立** 或  **建立並開啟**。

內容片段可以引用其他內容片段，從而允許在必要時使用嵌套的內容結構。

Content Fragments還可以在中引用其他AEM資產。 [這些資產需要儲存AEM在](/help/assets/manage-digital-assets.md) 建立引用內容片段之前。

## 後續步驟 {#next-steps}

現在您已建立了內容片段，您可以轉到入門指南的最後部分， [建立訪問和傳遞內容片段的API請求。](create-api-request.md)

>[!TIP]
>
>有關管理內容片段的完整詳細資訊，請參見 [內容片段文檔](/help/sites-cloud/administering/content-fragments/content-fragments.md)
