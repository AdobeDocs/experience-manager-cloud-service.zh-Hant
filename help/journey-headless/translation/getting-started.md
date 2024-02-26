---
title: AEM Headless 翻譯快速入門
description: 了解如何組織 Headless 內容以及 AEM 翻譯工具的運作原理。
exl-id: 04ae2cd6-aba3-4785-9099-2f6ef24e1daf
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 100%

---

# AEM Headless 翻譯快速入門 {#getting-started}

了解如何組織 Headless 內容以及 AEM 翻譯工具的運作原理。

## 目前進度 {#story-so-far}

在 AEM Headless 翻譯歷程的上一個文件「[了解 Headless 內容以及如何在 AEM 中翻譯](learn-about.md)」中，您已了解 Headless CMS 的基本理論，現在您應該：

* 了解 Headless 內容傳遞的基本概念。
* 熟悉 AEM 如何支援 Headless 和翻譯。

本文章以這些基本知識為基礎，以便您了解 AEM 如何儲存和管理 Headless 內容，以及您如何使用 AEM 的翻譯工具來翻譯該內容。

## 目標 {#objective}

本文件可協助您了解如何開始在 AEM 中翻譯 Headless 內容。閱讀本文件後，您應該：

* 了解內容結構對翻譯的重要性。
* 了解 AEM 如何儲存 Headless 內容。
* 熟悉 AEM 的翻譯工具。

## 要求和先決條件 {#requirements-prerequisites}

您必須先滿足數個要求，才能開始翻譯 Headless AEM 內容。

### 知識 {#knowledge}

* 有在 CMS 中翻譯內容的經驗
* 有使用大型 CMS 基本功能的經驗
* 具備 AEM 基本處理的工作知識
* 了解您正在使用的翻譯服務
* 對您要翻譯的內容有基本的了解

>[!TIP]
>
>如果您不熟悉使用 AEM 等大型 CMS，請考慮查閱[基本處理](/help/sites-cloud/authoring/basic-handling.md)文件再繼續進行。「基本處理」文件不是歷程的一部分。因此，請在完成後返回此頁面。

### 工具 {#tools}

* 用於測試內容翻譯作業的沙箱存取權
* 用於連接到您偏好之翻譯服務的認證
* 是 AEM `project-administrators` 群組的成員

## 結構是關鍵 {#content-structure}

AEM 的內容，無論是 Headless 網頁還是傳統網頁，都是由其結構驅動的。AEM 對內容結構的要求很少，但在規劃專案時請仔細考慮您的內容階層，可使翻譯工作變得更簡單。

>[!TIP]
>
>在 Headless 專案一開始就為翻譯進行規劃。儘早與專案經理和內容架構師密切合作。
>
>可能需要一位具獨立角色的國際化專案經理，其職責是定義哪些內容應該翻譯，哪些內容不應該翻譯，以及哪些已翻譯內容可以由區域或本地內容製作者修改。

## AEM 如何儲存 Headless 內容 {#headless-content-in-aem}

對於翻譯專家來說，深入了解 AEM 如何管理 Headless 內容並不重要。但是，熟悉基本概念和術語有助於您以後使用 AEM 的翻譯工具。最重要的是，您需要了解自己的內容及其結構，以便有效地翻譯內容。

### 內容模型 {#content-models}

為了跨管道、地區和語言一致地傳遞 Headless 內容，內容必須高度結構化。AEM 使用內容模型來強制使用此結構。將內容模型視為一種用於建立 Headless 內容的範本或模式。因為每個專案都有自己的需求，所以每個專案都定義了自己的內容片段模型。AEM 對此類模型沒有固定要求或結構。

內容架構師在專案早期工作以定義此結構。作為翻譯專家，您應該與內容架構師密切合作以理解和組織內容。

>[!NOTE]
>
>內容架構師負責定義內容模型。翻譯專家應只需熟悉以下步驟中概述的結構。

因為內容模型定義了內容結構，所以您需要知道模型的哪些欄位必須翻譯。通常，您與內容架構師一起定義它。若要瀏覽內容模型的欄位，請按照以下步驟操作。

1. 導覽至「**工具**」>「**一般**」>「**內容片段模型**」。
1. 內容片段模型通常儲存在資料夾結構中。選取您的專案資料夾。
1. 接著列出模型。選取模型來查看詳細資訊。
   ![內容片段模型](assets/content-fragment-models.png)
1. **內容片段模型編輯器**&#x200B;開啟。
   1. 左欄包含模型的欄位。我們對此欄感興趣。
   1. 左欄包含可新增至模型的欄位。此欄我們可以忽略。
      ![內容片段模型編輯器](assets/content-fragment-model-editor.png)
1. 選取模型的其中一個欄位。AEM 會標記該欄位，該欄位的詳細資料會顯示在右欄中。
   ![內容片段模型編輯器詳細資料](assets/content-fragment-model-editor-detail.png)
1. 內容架構者會在每一個需要翻譯的內容模型欄位上啟用「**可翻譯**」欄位。

>[!TIP]
>
>通常，內容架構師負責確定哪些欄位需要翻譯。前述步驟是為了讓翻譯專家能夠理解而提供的。

### 內容片段 {#content-fragments}

內容作者使用內容模型來建立實際的 Headless 內容。內容作者選擇哪個模型做為內容的基礎，然後建立內容片段。內容片段是模型的執行個體，代表要以 Headless 方式傳遞的實際內容。

如果內容模型是內容的模式，那麼內容片段就是基於這些模式的實際內容。內容片段代表必須翻譯的內容。

內容片段在 AEM 中以資產形式加以管理，視為數位資產管理 (DAM) 的一部分。這很重要，因為它們都位於路徑 `/content/dam` 下。

## 建議的內容結構 {#recommended-structure}

如前所述，與您的內容架構師一起確定適合您自己專案的內容結構。然而，以下是一個經過證明、簡單、直覺的結構，它非常有效。

在 `/content/dam` 下定義專案的基本資料夾。

```text
/content/dam/<your-project>
```

製作內容所用的語言稱為語言根。我們的範例是使用英語，它應該位在此路徑下。

```text
/content/dam/<your-project>/en
```

所有可能需要本地化的專案內容都應該放在語言根下。

```text
/content/dam/<your-project>/en/<your-project-content>
```

建立語言根時應同時建立同層級資料夾用於翻譯工作，資料夾名稱代表該語言的 ISO-2 語言碼。例如，德語將具有以下路徑。

```text
/content/dam/<your-project>/de
```

>[!NOTE]
>
>內容架構師通常負責建立這些語言資料夾。如果未建立，AEM 之後將無法建立翻譯工作。

最終結構可能如下所示。

```text
/content
    |- dam
        |- your-project
            |- en
                |- some
                |- exciting
                |- headless
                |- content
            |- de
            |- fr
            |- it
            |- ...
        |- another-project
        |- ...
```

您應該記下內容的特定路徑，因為之後需要用於設定您的翻譯。

>[!NOTE]
>
>內容架構師通常負責定義內容結構，但可以與翻譯專家協力完成。
>
>為了完整起見，這裡有詳細說明。

## AEM 翻譯工具 {#translation-tools}

現在您了解了什麼是內容片段以及內容結構的重要性，我們可以看看如何翻譯這些內容。AEM 的翻譯工具非常強大，其大致概念很容易理解。

* **翻譯連接器** - 連接器是 AEM 與您使用的翻譯服務之間的連結。
* **翻譯專案** - 翻譯專案收集由單一翻譯工作處理的內容並追蹤翻譯進度，與連接器連接以傳送要翻譯的內容並接收翻譯服務傳回的內容。

您通常只為您的執行個體設定一次連接器。然後，您使用翻譯專案來翻譯您的內容，並持續更新其翻譯。

## 下一步 {#what-is-next}

您已完成 Headless 翻譯歷程的此部分，您應該：

* 了解內容結構對翻譯的重要性。
* 了解 AEM 如何儲存 Headless 內容。
* 熟悉 AEM 的翻譯工具。

以這些知識為基礎並繼續的 AEM Headless 翻譯歷程，接著檢閱文件「[設定翻譯整合](configure-connector.md)」，從中了解如何將 AEM 連接到翻譯服務。|

## 其他資源 {#additional-resources}

雖然建議您查閱文件[設定翻譯連接器](configure-connector.md)來繼續 Headless 翻譯歷程的下個部分，以下也有一些其他選擇性資源，在深入探究本文件提到的一些概念，但不是繼續 Headless 歷程的必要條件。

* [AEM 基本處理](/help/sites-cloud/authoring/basic-handling.md) - 了解 AEM UI 的基本知識，以便能夠輕鬆導覽和執行基本任務，例如尋找您的內容。
* [識別要翻譯的內容](/help/sites-cloud/administering/translation/rules.md) - 了解翻譯規則如何識別需要翻譯的內容。
* [設定翻譯整合框架](/help/sites-cloud/administering/translation/integration-framework.md) - 了解如何設定翻譯整合框架以與協力廠商翻譯服務整合。
* [管理翻譯專案](/help/sites-cloud/administering/translation/managing-projects.md) - 了解如何在 AEM 中建立和管理機器和人工翻譯專案。
* [AEM as a Headless CMS 簡介](/help/headless/introduction.md)
* [AEM 中的 Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
