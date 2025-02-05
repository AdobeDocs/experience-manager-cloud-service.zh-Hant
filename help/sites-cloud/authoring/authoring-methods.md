---
title: 在AEM中創作內容的方法
description: 瞭解您可以在AEM中編寫內容的不同方式以及它們之間的差異。
feature: Authoring
exl-id: ef482843-451b-474e-a8d0-d0bfcc17221b
solution: Experience Manager Sites
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 在AEM中創作內容的方法 {#authoring-methods}

瞭解您可以在AEM中編寫內容的不同方式、其差異，以及您何時可以使用其中一種工具取代另一種工具。

## AEM編寫彈性 {#authoring-flexibility}

AEM as a Cloud Service提供數種不同的編輯器，可編輯不同型別的內容並支援不同的編寫使用案例。

* [使用頁面編輯器進行WYSIWYG製作](#page-editor) — 頁面編輯器是在AEM中製作內容的傳統編輯器，已嘗試並信任數千個網站。
* [使用通用編輯器進行WYSIWYG編寫](#universal-editor) — 通用編輯器是一種現代化的UI，可讓您以無內容的方式進行AEM內容編寫，可用於利用Edge Delivery Services的AEM專案。
* [檔案式撰寫](#document-based) — 如果您使用Edge Delivery服務，您可以選擇在AEM主控台之外完全以Microsoft Word或Google Docs等傳統檔案的形式撰寫內容。
* [AEM內容片段編輯器](#cf-editor) — 這是建立Headless內容的選擇編輯器。

由於AEM的整合與可擴充性質，這些方法可依據您的專案需求專門使用或相互組合。

如果您不確定哪些撰寫選項可供您使用，或您想要探索新的內容撰寫選項，請洽詢您的系統管理員或專案經理。

## 使用頁面編輯器進行WYSIWYG製作 {#page-editor}

這是在AEM中編寫內容的傳統編輯器，在數千個網站上受到成千上萬人的嘗試和信任。

![AEM頁面編輯器](assets/authoring-methods-page-editor.png)

AEM頁面編輯器提供整合式環境，讓您可使用「所見即所得」(WYSIWYG)介面創作內容。 拖放預先定義的元件，就地建置頁面及編輯內容。

若要深入瞭解AEM頁面編輯器，請參閱檔案[AEM頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)。

## 使用通用編輯器進行WYSIWYG製作 {#universal-editor}

Universal Editor是現代化的UI，可讓您以不受內容限制的方式創作AEM內容，並且是利用Edge Delivery Services的AEM專案的第一個選擇。

![Universal Editor](assets/authoring-methods-ue.png)

通用編輯器可透過AEM內的Sites主控台存取，但提供強大且與內容無關的靈活性，不僅可編寫您的AEM內容，還可編寫正確儀表化的外部內容。

若要深入瞭解通用編輯器，請參閱檔案[使用通用編輯器編寫內容](/help/sites-cloud/authoring/universal-editor/authoring.md)。

## 文件型製作  {#document-based}

如果您使用Edge Delivery服務，您可以選擇在[AEM **Sites**&#x200B;主控台](/help/sites-cloud/authoring/sites-console/introduction.md)之外將您的內容製作為傳統檔案，例如Microsoft Word或Google Docs。

![編輯檔案型內容](assets/authoring-methods-document.jpg)

透過檔案式撰寫，作者可以使用他們已有的工具，並且仍可受益於AEMEdge Delivery Services的速度和效能，以發佈其內容。 檔案式撰寫不需要使用AEM主控台。

若要深入瞭解檔案式撰寫，請參閱[撰寫與發佈內容](/help/edge/docs/authoring.md)。

## AEM內容片段編輯器 {#cf-editor}

AEM內容片段編輯器是建立Headless內容的首選編輯器。

![AEM內容片段編輯器](assets/authoring-methods-cf-editor.png)

AEM內容片段編輯器提供用於建立和管理結構化內容的清晰介面，適用於Headless傳送。

若要深入瞭解AEM內容片段編輯器，請參閱檔案[管理內容片段](/help/sites-cloud/administering/content-fragments/managing.md)和[編寫內容片段](/help/sites-cloud/administering/content-fragments/managing.md)。

>[!NOTE]
>
>針對AEM as a Cloud Service在本機開發時，無法使用此區段中醒目提示的&#x200B;*新*&#x200B;編輯器。
>
>[*原始*&#x200B;內容片段編輯器](/help/assets/content-fragments/content-fragments-variations.md)也可供使用。
