---
title: WYSIWYGEdge Delivery Services內容製作
description: 了解內容製作如何與 Edge Delivery Services 搭配使用，以及如何使用 Edge Delivery Services 製作 AEM 內容。
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
role: User
source-git-commit: f0cb108c620a31c4f8a48f1d2530860ca01b06c3
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 69%

---


# WYSIWYGEdge Delivery Services內容製作 {#authoring-edge}

使用 Edge Delivery Services 時，製作很簡單、快速且靈活。您有兩種選擇來為 Edge Delivery Services 製作內容：

* [通用編輯器](#universal-editor) — 可在AEM中編寫內容的現代「所見即所得」(WYSIWYG) UI
* [文件型製作](#document-based) - 例如 Microsoft Word 或 Google Docs

## Universal Editor 製作 {#universal-editor}

將 Edge Delivery Services 與 AEM as a Cloud Service 搭配使用時，需要了解的最基本事實是您製作的內容將保留在 AEM as a Cloud Service 中。

![WYSIWYG製作如何搭配Edge Delivery Services使用](assets/how-aem-edge-works.png)

1. [AEM Sites環境](/help/sites-cloud/authoring/quick-start.md)用於內容管理，例如建立新頁面、體驗片段、內容片段等。
   * AEM 的所有功能均適用，例如工作流程、MSM、翻譯、啟動等。
1. [Universal Editor](/help/sites-cloud/authoring/universal-editor/authoring.md) 是用來製作 AEM 所管理的內容。
   * Universal Editor 為內容製作提供了全新且現代化的使用者介面。
   * 在內容製作方面，AEM 會轉譯 HTML，但包括來自 Edge Delivery Services 的指令碼、樣式、圖示和其他資源。
   * 儘管使用了 Universal Editor，但所有變更都會保留到 AEM。
   * Universal Editor 尚未與 AEM Page Editor 具有同等功能，且某些 AEM 功能在 Universal Editor 中可能無法使用。
1. 您使用 Universal Editor 製作並保留到 AEM 的內容將發佈到 Edge Delivery Services。
   * 內容仍儲存在 AEM 中。
   * AEM 會轉譯擷取所需的語意 HTML。
   * 內容發佈到 Edge Delivery Services。
1. [Edge Delivery Services](/help/edge/developer/keeping-it-100.md) 可確保 100% 的 Lighthouse 分數。

區塊是 Edge Delivery Services 提交的頁面基本元件。作者可以從 Adob&#x200B;&#x200B;e 作為標準提供的預設區塊或開發人員為您專案量身定制的區塊中進行選擇。

Universal Editor 提供了一個現代且直觀的 GUI，可透過拖放區塊來製作內容。

![Universal Editor 中的拖放區塊](assets/blocks.png)

然後，在屬性邊欄內可設定區塊的詳細資訊。

![設定區塊屬性](assets/block-properties.png)

有關如何使用 Universal Editor 的詳細資訊，請參閱文件[「使用 Universal Editor 製作內容」。](/help/sites-cloud/authoring/universal-editor/authoring.md)

請參閱[使用Edge Delivery Services進行WYSIWYG編寫的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)，瞭解如何開始使用AEM和Edge Delivery Services編寫您自己的專案。

## 其他撰寫方法  {#authoring-methods}

所見即所得撰寫是內容作者適用的強大且直覺式工具。 不過，有許多不同的撰寫使用案例，這就是為什麼AEM要提供其他撰寫解決方案的原因。

請參閱檔案[選擇撰寫方法](/help/edge/authoring-methods.md)，以進一步瞭解AEM提供的撰寫解決方案，包括檔案式撰寫和Headless。
