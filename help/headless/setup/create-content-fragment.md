---
title: 建立內容片段 - Headless 設定
description: 了解如何使用 AEM 的內容片段來設計、建立、規劃和使用每頁自主的內容以進行 Headless 傳遞。
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: ht
source-wordcount: '347'
ht-degree: 100%

---

# 建立內容片段 - Headless 設定 {#creating-content-fragments}

了解如何使用 AEM 的內容片段來設計、建立、規劃和使用每頁自主的內容以進行 Headless 傳遞。

## 什麼是內容片段？ {#what-are-content-fragments}

[您已經建立資產資料夾](create-assets-folder.md)，其中可以儲存內容片段，現在您可以建立片段了！

內容片段允許您設計、建立、規劃和發佈每頁自主的內容。它們可讓您將內容準備就緒用於多個位置和多個管道。

內容片段包含結構化內容，能以 JSON 格式傳遞。

## 如何建立內容片段 {#how-to-create-a-content-fragment}

內容作者將建立任意數量的內容片段來表示他們建立的內容。這是他們在 AEM 中的主要任務。出於本快速入門指南的目的，我們只需要建立一個。

1. 登入 AEM as a Cloud Service，然後從主選單中選擇&#x200B;**導覽** -> **內容片段**。

1. 點選或按一下[您之前建立的資料夾。](create-assets-folder.md)
1. 點選或按一下&#x200B;**建立**。
1. 建立內容片段以顯示為對話框。
選擇您希望用於建立內容片段的位置和模型。

   * 可用模型取決於您為內容片段建立所在資產資料夾所定義的&#x200B;[**雲端設定**](create-assets-folder.md)。
   * 如果您的模型不可用，請檢查資產資料夾的設定。

   新增標題、名稱，如果需要，可以新增描述。

   ![「建立新內容片段」對話框](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

1. 點選或按一下&#x200B;**建立**&#x200B;或&#x200B;**建立並開啟**。

內容片段可以參考其他內容片段，必要時允許巢狀內容結構。

內容片段也可以參考 AEM 中的其他資產。在建立參考的內容片段之前，[這些資產需要儲存在 AEM](/help/assets/manage-digital-assets.md)。

## 後續步驟 {#next-steps}

現在您已經建立了一個內容片段，您可以繼續閱讀快速入門指南的最後一部分，[建立 API 要求以存取和傳遞內容片段。](create-api-request.md)

>[!TIP]
>
>如需有關管理內容片段的完整詳細資訊，請參閱[內容片段文件](/help/sites-cloud/administering/content-fragments/content-fragments.md)
