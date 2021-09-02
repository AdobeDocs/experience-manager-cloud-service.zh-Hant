---
title: 開始使用AEM Sites翻譯
description: 了解如何組織您的AEM Sites內容，以及AEM翻譯工具的運作方式。
index: true
hide: false
hidefromtoc: false
source-git-commit: 8c04ffde2cbafcb6d556de8d48fc19f5b130a2c1
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---


# 開始使用AEM Sites翻譯 {#getting-started}

了解如何組織您的AEM Sites內容，以及AEM翻譯工具的運作方式。

## 迄今為止的故事 {#story-so-far}

在AEM Sites翻譯歷程的上一份檔案中，[了解AEM Sites內容及如何在AEM](learn-about.md)中翻譯，您已了解AEM Sites的基本理論，現在應該：

* 了解建立AEM Sites內容的基本概念。
* 請熟悉AEM支援翻譯的方式。

本文以這些基本知識為基礎，讓您了解AEM如何儲存和管理內容，以及如何使用AEM翻譯工具來翻譯該內容。

## 目標 {#objective}

本檔案可協助您了解如何開始在AEM中轉譯網站內容。 閱讀後，您應：

* 了解內容結構對翻譯的重要性。
* 了解AEM如何儲存內容。
* 熟悉AEM翻譯工具。

## 需求與必要條件 {#requirements-prerequisites}

開始轉譯AEM內容之前，有許多需求。

### 知識 {#knowledge}

* 在CMS中轉譯內容的體驗。
* 使用大型CMS基本功能的經驗。
* 具備AEM基本處理的工作知識
* 了解您使用的翻譯服務
* 對翻譯的內容有基本的了解

>[!TIP]
>
>如果您不熟悉如何使用AEM等大型CMS，請考慮先檢閱[基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)檔案，再繼續操作。 基本處理檔案不屬於歷程，因此，完成時請返回本頁面。

### 工具 {#tools}

* 用於測試轉譯內容的沙箱存取
* 連接到首選翻譯服務的憑據
* 成為AEM中`project-administrators`組的成員

## AEM如何儲存內容 {#content-in-aem}

對於翻譯專家來說，深入了解AEM管理內容的方式並不重要。 不過，熟悉基本概念和術語後來使用AEM翻譯工具會很有幫助。 最重要的是，您需要了解您自己的內容，以及內容的結構，以便有效翻譯內容。

### Sites Console {#sites-console}

網站主控台會概略介紹您的內容結構，讓您輕鬆導覽內容，並透過建立新頁面、移動和複製頁面及發佈內容來管理內容。

要訪問站點控制台：

1. 在全域導覽功能表中，按一下或點選「**導覽** -> **Sites**」。
1. 網站主控台會開啟至您內容的頂層。
1. 使用視窗右上方的檢視選取器，確定已選取&#x200B;**欄檢視**。

   ![選擇列視圖](assets/selecting-column-view.png)

1. 點選或按一下欄中的項目，會在右側欄的階層中顯示其下方的內容。

   ![內容階層](assets/sites-console-hierarchy.png)

1. 點選或按一下欄中項目的核取方塊，即可選取該項目並在右側欄中顯示所選項目的詳細資訊，同時在上方工具列顯示所選項目可用的許多動作。

   ![內容選取](assets/sites-console-selection.png)

1. 點選或按一下左上方的邊欄選取器，您也可以顯示&#x200B;**內容樹狀結構**&#x200B;檢視，以取得內容的樹狀結構概觀。

   ![內容樹視圖](assets/sites-console-content-tree.png)

使用這些簡單的工具，您可以直覺地導覽您的內容結構。

>[!NOTE]
>
>內容架構者通常會定義內容結構，而內容作者則會在該結構內建立內容。
>
>作為翻譯專家，簡單了解如何瀏覽該結構並了解內容的位置非常重要。

### 頁面編輯器 {#page-editor}

網站主控台可讓您導覽內容，並概略說明其結構。 若要查看個別頁面的詳細資訊，您需要使用網站編輯器。

要編輯頁面：

1. 使用網站控制台來尋找並選取頁面。 請記住，您必須點選或按一下個別頁面的核取方塊，才能選取它。

   ![選擇要編輯的頁面](assets/sites-editor-select-page.png)

1. 點選工具列中的&#x200B;**Edit**&#x200B;選項。
1. 網站編輯器隨即開啟，選定頁面隨即載入，以在新的瀏覽器索引標籤中進行編輯。
1. 將滑鼠游標移過或點選內容會顯示個別元件的選取器。 元件是組成頁面的拖放建置區塊。

   ![編輯頁面](assets/sites-editor-title.png)

您可以隨時在瀏覽器中切換回該索引標籤，以返回網站主控台。 使用網站編輯器，內容作者和您的對象將看到頁面內容時，您就可以快速檢視頁面內容。

>[!NOTE]
>
>內容作者使用網站編輯器建立您的網站內容。
>
>身為翻譯專家，請務必簡單了解如何使用網站編輯器檢視該內容的詳細資訊。

## 結構是關鍵 {#content-structure}

AEM內容由其結構驅動。 AEM對內容結構只施加了很少的要求，但在項目規劃中仔細考慮您的內容層次結構可以使翻譯更簡單。

>[!TIP]
>
>在您的AEM專案開始時規劃翻譯。 及早與專案經理和內容架構師密切合作。
>
>國際化項目經理可能需要作為單獨的角色，其職責是定義哪些內容應翻譯，哪些內容不應翻譯，哪些翻譯內容可由區域或本地內容製作者修改。

## 建議的內容結構 {#recommended-structure}

如先前建議，請與內容架構師合作，為您自己的專案決定適當的內容結構。 但是以下是一個經驗證的、簡單的、直觀的結構，非常有效。

在`/content`下為項目定義基資料夾。

```text
/content/<your-project>
```

您的內容製作語言稱為語言根。 在我們的範例中，它是英文，應該位於此路徑下方。

```text
/content/<your-project>/en
```

所有可能需要本地化的專案內容都應放在語言根目錄下。

```text
/content/<your-project>/en/<your-project-content>
```

翻譯應與語言根目錄一起建立為同層級資料夾，其資料夾名稱代表語言的ISO-2語言代碼。 例如，德文會有下列路徑。

```text
/content/<your-project>/de
```

>[!NOTE]
>
>內容架構師通常負責建立這些語言資料夾。 如果未建立，AEM將無法稍後建立翻譯工作。

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

您應記下內容的特定路徑，因為稍後設定翻譯時需要它。

>[!NOTE]
>
>通常，內容架構者有責任定義內容結構，通常與翻譯專家合作。
>
>此處詳細說明了完整性。

## AEM翻譯工具 {#translation-tools}

現在您已了解網站主控台和編輯器，以及內容結構的重要性，我們可以了解如何翻譯內容。 AEM中的翻譯工具功能強大，但簡單易懂。

* **翻譯連接器**  — 連接器是AEM與您所使用翻譯服務之間的連結。
* **翻譯規則**  — 規則會定義特定路徑下應翻譯的內容。
* **翻譯專案**  — 翻譯專案會收集應以單一翻譯工作方式處理的內容，並追蹤翻譯進度，與連接器介面，以傳輸要翻譯的內容，並從翻譯服務接收回內容。

通常，您只需針對執行個體和每個專案的規則設定連接器一次。 然後，您可使用翻譯專案來翻譯內容，並持續更新翻譯內容。

## 下一步 {#what-is-next}

現在您已完成AEM Sites翻譯歷程的這一部分，您應：

* 了解內容結構對翻譯的重要性。
* 了解AEM如何儲存內容。
* 熟悉AEM翻譯工具。

基於此知識，接下來檢閱檔案[設定翻譯連接器](configure-connector.md)，繼續您的AEM Sites翻譯歷程，您將在此了解如何將AEM連線至翻譯服務。|

## 其他資源 {#additional-resources}

雖然建議您通過審閱文檔[配置翻譯連接器](configure-connector.md)來繼續翻譯過程的下一個部分，但以下是一些附加的可選資源，這些資源可以更深入地了解本文檔中提到的一些概念，但不需要繼續此過程。

* [AEM基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 了解AEM UI的基本知識，以便熟悉地導覽及執行基本工作，例如尋找您的內容。
* [識別要翻譯的內容](/help/sites-cloud/administering/translation/rules.md)  — 了解翻譯規則如何識別需要翻譯的內容。
* [配置翻譯整合框架](/help/sites-cloud/administering/translation/integration-framework.md)  — 了解如何配置翻譯整合框架以與第三方翻譯服務整合。
* [管理翻譯專案](/help/sites-cloud/administering/translation/managing-projects.md)  — 了解如何在AEM中建立和管理機器和人類翻譯專案。
