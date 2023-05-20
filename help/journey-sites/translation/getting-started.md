---
title: AEM Sites 翻譯快速入門
description: 瞭解如何組織您的AEM Sites內容以及翻譯工AEM具的工作。
index: true
hide: false
hidefromtoc: false
exl-id: 9bfc3995-ac8e-488e-b68f-9e1b5b4a3176
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 44%

---

# 開始AEM Sites翻譯 {#getting-started}

瞭解如何組織您的AEM Sites內容以及翻譯工AEM具的工作。

## 到目前為止 {#story-so-far}

在AEM Sites的前期翻譯過程中， [瞭解AEM Sites內容及翻譯方AEM法](learn-about.md) 你學到了AEM Sites的基本理論，現在就該說：

* 瞭解AEM Sites內容建立的基本概念。
* 熟悉如何支AEM持翻譯。

本文基於這些基礎知識，以便您了AEM解如何儲存和管理內容，以及如何使用翻AEM譯工具翻譯內容。

## 目標 {#objective}

此文檔可幫助您瞭解如何開始翻譯網站內容AEM。 閱讀本文件後，您應該：

* 了解內容結構對翻譯的重要性。
* 瞭解內AEM容的儲存方式。
* 熟悉 AEM 的翻譯工具。

## 要求和先決條件 {#requirements-prerequisites}

在開始翻譯內容之前，有許多要AEM求。

### 知識 {#knowledge}

* 有在 CMS 中翻譯內容的經驗
* 有使用大型 CMS 基本功能的經驗
* 具備 AEM 基本處理的工作知識
* 了解您正在使用的翻譯服務
* 對您要翻譯的內容有基本的了解

>[!TIP]
>
>如果您不熟悉使用 AEM 等大型 CMS，請考慮查閱[基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)文件再繼續進行。「基本處理」文件不是歷程的一部分，因此請在完成後返回此頁面。

### 工具 {#tools}

* 用於測試內容翻譯作業的沙箱存取權
* 用於連接到您偏好之翻譯服務的認證
* 是 AEM `project-administrators` 群組的成員

## AEM 如何儲存 內容 {#content-in-aem}

對於翻譯專家來說，深入瞭解內容管理方式並AEM不重要。 但是，熟悉基本概念和術語將有助於您以後使用 AEM 的翻譯工具。最重要的是，您需要了解自己的內容及其結構，以便有效地翻譯內容。

### 站點控制台 {#sites-console}

站點控制台概述了您的內容結構，通過建立新頁面、移動和複製頁面以及發佈內容，您可以輕鬆瀏覽內容並管理內容。

要訪問站點控制台：

1. 在全局導航菜單中，按一下或點擊 **導航** -> **站點**。
1. 站點控制台開啟到內容的頂級。
1. 確保 **列視圖** 的子菜單。

   ![選擇列視圖](assets/selecting-column-view.png)

1. 按一下或按一下列中的項，它將在右側列的層次結構中顯示其下方的內容。

   ![內容層次](assets/sites-console-hierarchy.png)

1. 按一下或按一下列中某個項的複選框，它將選擇該項，並在右側的列中顯示選定項的詳細資訊，同時顯示上面工具欄中選定項的可用操作數。

   ![內容選擇](assets/sites-console-selection.png)

1. 通過點擊或按一下左上方的滑軌選擇器，還可以顯示 **內容樹** 的子菜單。

   ![內容樹視圖](assets/sites-console-content-tree.png)

使用這些簡單的工具，您可以直觀地瀏覽內容結構。

>[!NOTE]
>
>內容架構師通常定義內容結構，而內容作者在該結構內建立內容。
>
>作為翻譯專家，簡單瞭解如何瀏覽該結構並瞭解內容所在位置非常重要。

### 頁面編輯器 {#page-editor}

站點控制台允許您瀏覽內容並概述其結構。 要查看單個頁面的詳細資訊，需要使用站點編輯器。

編輯頁面：

1. 使用站點控制台查找並選擇頁面。 請記住，您需要點擊或按一下單個頁面的複選框才能選擇它。

   ![選擇要編輯的頁面](assets/sites-editor-select-page.png)

1. 點擊 **編輯** 的子菜單。
1. 站點編輯器隨即開啟，其中已載入選定頁面，以便在新瀏覽器頁籤中進行編輯。
1. 對內容進行滑鼠移動或點擊顯示各個元件的選擇器。 元件是組成頁面的拖放構建塊。

   ![編輯頁面](assets/sites-editor-title.png)

您可以隨時切換回瀏覽器中的該頁籤，以返回到站點控制台。 使用網站編輯器，您可以快速查看內容作者和您的受眾將看到該頁面的內容。

>[!NOTE]
>
>內容作者使用站點編輯器建立您的站點內容。
>
>作為翻譯專家，只需瞭解如何使用站點編輯器查看該內容的詳細資訊就很重要。

## 結構是關鍵 {#content-structure}

內AEM容由其結構驅動。 AEM 對內容結構的要求很少，但在規劃專案時請仔細考慮您的內容階層可以使翻譯變得更加簡單。

>[!TIP]
>
>在項目開始時計畫AEM翻譯。 儘早與專案經理和內容架構師密切合作。
>
>可能需要一位具獨立角色的國際化專案經理，其職責是定義哪些內容應該翻譯，哪些內容不應該翻譯，以及哪些已翻譯內容可以由區域或本地內容製作者修改。

## 建議的內容結構 {#recommended-structure}

如前所述，與您的內容架構師一起確定適合您自己專案的內容結構。然而，以下是一個經過證明、簡單、直覺的結構，它非常有效。

在 `/content` 下定義專案的基本資料夾。

```text
/content/<your-project>
```

編寫內容所用的語言稱為語言根。我們的範例是使用英語，它應該位在此路徑下。

```text
/content/<your-project>/en
```

所有可能需要本地化的專案內容都應該放在語言根下。

```text
/content/<your-project>/en/<your-project-content>
```

建立語言根時應同時建立同層級資料夾用於翻譯工作，資料夾名稱代表該語言的 ISO-2 語言碼。例如，德語將具有以下路徑。

```text
/content/<your-project>/de
```

>[!NOTE]
>
>內容架構師通常負責建立這些語言資料夾。如果未建立，AEM 之後將無法建立翻譯工作。

最終結構可能如下所示。

```text
/content
    |- your-project
        |- en
            |- some
            |- exciting
            |- sites
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
>通常，內容架構師有責任定義內容結構，通常與翻譯專家協作。
>
>為了完整起見，這裡有詳細說明。

## AEM 翻譯工具 {#translation-tools}

現在，您瞭解了站點控制台和編輯器以及內容結構的重要性，我們可以瞭解如何翻譯內容。 AEM 的翻譯工具非常強大，其大致概念很容易理解。

* **翻譯連接器** - 連接器是 AEM 與您使用的翻譯服務之間的連結。
* **翻譯規則**  — 規則定義應翻譯特定路徑下的內容。
* **翻譯專案** - 翻譯專案收集由單一翻譯工作處理的內容並追蹤翻譯進度，與連接器連接以傳送要翻譯的內容並接收翻譯服務傳回的內容。

通常，您只為實例和每個項目的規則設定一次連接器。 然後，您使用翻譯專案來翻譯您的內容，並持續更新其翻譯。

## 下一步 {#what-is-next}

現在，您已完成AEM Sites翻譯過程的這一部分，您應：

* 了解內容結構對翻譯的重要性。
* 瞭解內AEM容的儲存方式。
* 熟悉 AEM 的翻譯工具。

在此知識基礎上，繼續您的AEM Sites翻譯之旅，下一步查看文檔 [配置翻譯連接器](configure-connector.md) 您將學習如何連AEM接到翻譯服務。|

## 其他資源 {#additional-resources}

建議您通過審閱文檔來進入翻譯過程的下一部分 [配置翻譯連接器](configure-connector.md) 下面是一些附加的可選資源，這些資源對本文檔中提到的一些概念進行了更深入的瞭解，但不需要繼續旅行。

* [AEM 基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md) - 了解 AEM UI 的基本知識，以便能夠輕鬆導覽和執行基本任務，例如尋找您的內容。
* [識別要翻譯的內容](/help/sites-cloud/administering/translation/rules.md) - 了解翻譯規則如何識別需要翻譯的內容。
* [設定翻譯整合框架](/help/sites-cloud/administering/translation/integration-framework.md) - 了解如何設定翻譯整合框架以與協力廠商翻譯服務整合。
* [管理翻譯專案](/help/sites-cloud/administering/translation/managing-projects.md) - 了解如何在 AEM 中建立和管理機器和人工翻譯專案。
