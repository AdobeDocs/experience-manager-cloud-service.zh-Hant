---
title: 開始使用 AEM Sites 翻譯
description: 了解如何組織 AEM Sites 內容以及 AEM 翻譯工具的運作方式。
index: true
hide: false
hidefromtoc: false
exl-id: 9bfc3995-ac8e-488e-b68f-9e1b5b4a3176
solution: Experience Manager Sites
feature: Translation
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 100%

---

# 開始使用 AEM Sites 翻譯 {#getting-started}

了解如何組織 AEM Sites 內容以及 AEM 翻譯工具的運作方式。

## 目前進度 {#story-so-far}

在 AEM Sites 翻譯歷程的上一個文件「[了解 AEM Sites 內容以及如何在 AEM 中翻譯](learn-about.md)」中，您已了解 AEM Sites 的基本原理，現在您應該：

* 了解 AEM Sites 內容建立的基本概念。
* 熟悉 AEM 如何支援翻譯。

本文章以這些基本知識為基礎，以便您了解 AEM 如何儲存和管理內容，以及您如何使用 AEM 的翻譯工具來翻譯該內容。

## 目標 {#objective}

本文件協助您了解如何開始在 AEM 中翻譯網站內容。閱讀本文件後，您應該：

* 了解內容結構對翻譯的重要性。
* 了解 AEM 如何儲存內容。
* 熟悉 AEM 的翻譯工具。

## 要求和先決條件 {#requirements-prerequisites}

您必須先滿足數個要求，才能開始翻譯您的 AEM 內容。

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

## AEM 如何儲存內容 {#content-in-aem}

對於翻譯專家來說，深入了解 AEM 如何管理內容並不重要。但是，熟悉基本概念和術語有助於您以後使用 AEM 的翻譯工具。最重要的是，您需要了解自己的內容及其結構，才能有效地翻譯內容。

### Sites 主控台 {#sites-console}

Sites 主控台提供您的內容之結構概觀，使您可以透過建立新頁面、行動和複製頁面以及發佈內容來輕鬆導覽和管理內容。

若要存取Sites 主控台：

1. 在全域導覽功能表中，選取「**導覽**」>「**網站**」。
1. Sites 主控台將開啟，並顯示頂層內容。
1. 使用視窗右上角的檢視選擇器確保選取「**欄視圖**」。

   ![選擇欄視圖](assets/selecting-column-view.png)

1. 透過點擊或點擊列中的某個項目，它會在右側列的層次結構中顯示該項目下方的內容。

   ![內容階層](assets/sites-console-hierarchy.png)

1. 點選或按一下欄中某個項目的核取方塊，它會選取該項目，並在右側的欄中顯示所選項目的詳細資訊，並在上方工具列中顯示所選項目的可用動作。

   ![內容選擇](assets/sites-console-selection.png)

1. 點選或按一下左上角的邊欄選擇器，您也可以顯示「**內容樹**」視圖，以樹狀圖顯示內容概觀。

   ![內容樹視圖](assets/sites-console-content-tree.png)

使用這些簡單的工具，您可以依直覺導覽您的內容結構。

>[!NOTE]
>
>內容架構者通常會定義內容結構，而內容作者在該結構內建立內容。
>
>作為翻譯專家，必須了解如何導覽該結構並了解內容所在位置。

### 頁面編輯器 {#page-editor}

Sites 主控台讓您導覽內容並提供其結構的概觀。要查看單一頁面的詳細資訊，您必須使用網站編輯器。

若要編輯頁面：

1. 使用 Sites 主控台尋找並選取頁面。請記住，您必須選取單一頁面的核取方塊才能選取該頁面。

   ![選取要編輯的頁面](assets/sites-editor-select-page.png)

1. 選取工具列中的「**編輯**」選項。
1. 網站編輯器將開啟並載入選定的頁面，以便在新的瀏覽器分頁中進行編輯。
1. 將滑鼠懸停在內容上方或點選內容會顯示各個組件的選擇器。元件是構成頁面的拖放式建構元件。

   ![編輯頁面](assets/sites-editor-title.png)

您可以隨時切換回瀏覽器中的該分頁，即可返回Sites 主控台。使用網站編輯器，您可用內容作者的身份快速查看頁面內容，並讓您的對象可以看到內容。

>[!NOTE]
>
>內容作者使用網站編輯器建立您的網站內容。
>
>作為翻譯專家，必須了解如何使用網站編輯器查看該內容的詳細資訊。

## 結構是關鍵 {#content-structure}

AEM 的內容由其結構驅動。AEM 對內容結構的要求很少，但在規劃專案時請仔細考慮您的內容階層，可使翻譯工作變得更簡單。

>[!TIP]
>
>在 AEM 專案一開始就規劃翻譯事宜。儘早與專案經理和內容架構師密切合作。
>
>可能需要一位具獨立角色的國際化專案經理，其職責是定義哪些內容應該翻譯，哪些內容不應該翻譯，以及哪些已翻譯內容可以由區域或本地內容製作者修改。

## 建議的內容結構 {#recommended-structure}

如前所述，與您的內容架構師一起確定適合您自己專案的內容結構。然而，以下是一個經過證明、簡單、直覺的結構，它非常有效。

在 `/content` 下定義專案的基本資料夾。

```text
/content/<your-project>
```

製作內容所用的語言稱為語言根。我們的範例是使用英語，它應該位在此路徑下。

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

您應該記下內容的特定路徑，因為之後設定您的翻譯時需要使用。

>[!NOTE]
>
>一般是由內容架構者負責定義內容結構，但通常會與翻譯專家共同作業。
>
>為了完整起見，這裡有詳細說明。

## AEM 翻譯工具 {#translation-tools}

現在您了解什麼是 Sites 主控台和編輯器以及結構的重要性，我們可以來了解如何翻譯內容。AEM 的翻譯工具非常強大，其大致概念很容易理解。

* **翻譯連接器** - 連接器是 AEM 與您使用的翻譯服務之間的連結。
* **翻譯規則** - 規則定義特定路徑下哪些內容應該翻譯。
* **翻譯專案** - 翻譯專案收集由單一翻譯工作處理的內容並追蹤翻譯進度，與連接器連接以傳送要翻譯的內容並接收翻譯服務傳回的內容。

您通常只為每個專案的執行個體和規則設定一次連接器。然後，您使用翻譯專案來翻譯您的內容，並持續更新其翻譯。

## 下一步 {#what-is-next}

您已完成 AEM Sites 翻譯歷程的這個部分，您應該：

* 了解內容結構對翻譯的重要性。
* 了解 AEM 如何儲存內容。
* 熟悉 AEM 的翻譯工具。

以這些知識為基礎並繼續您的 AEM Sites 翻譯歷程，接著檢閱文件「[設定翻譯連接器](configure-connector.md)」，從中學習如何將 AEM 連接到翻譯服務。

## 其他資源 {#additional-resources}

雖然建議您查閱文件[設定翻譯連接器](configure-connector.md)來繼續翻譯歷程的下個部分，以下也有一些其他選擇性資源，協助深入瞭解本文件提及的一些概念，但是這些並非繼續執行歷程的必要條件。

* [AEM 基本處理](/help/sites-cloud/authoring/basic-handling.md) - 了解 AEM UI 的基本知識，以便能夠輕鬆導覽和執行基本任務，例如尋找您的內容。
* [識別要翻譯的內容](/help/sites-cloud/administering/translation/rules.md) - 了解翻譯規則如何識別需要翻譯的內容。
* [設定翻譯整合框架](/help/sites-cloud/administering/translation/integration-framework.md) - 了解如何設定翻譯整合框架以與協力廠商翻譯服務整合。
* [管理翻譯專案](/help/sites-cloud/administering/translation/managing-projects.md) - 了解如何在 AEM 中建立和管理機器和人工翻譯專案。
