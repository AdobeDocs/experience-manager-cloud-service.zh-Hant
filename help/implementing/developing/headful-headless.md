---
title: AEM中的Headful和Headless
description: AEM專案可以建置在有頭和無頭的模型中，但選擇並非二進位。 AEM提供彈性，讓您在單一專案中運用這兩種模型的優點。
translation-type: tm+mt
source-git-commit: 772717b7ad3baa17a58e251c128663035eb89931
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---


# AEM {#headful-headless}中的Headful和Headless

Adobe Experience Manager專案可以同時建置在無頭和無頭兩種模型中，但選擇並非二進位。 AEM提供彈性，讓您在單一專案中運用這兩種模型的優點。 本檔案提供並概述不同的模型，並說明SPA整合的層級。

## 概覽 {#overview}

AEM提供強大的工具，可管理內容的建立及在單一平台中的發佈。 這是傳統的「頭腦式」內容管理模型，內容製作人和開發人員可在同一平台上工作，為內容消費者提供體驗。

AEM也可用來簡單管理內容，讓其他平台管理內容的簡報和傳送。 這是「無頭」的內容管理模型，內容作者和開發人員可在不同平台上工作，為內容消費者提供體驗。

但這不一定是二進位的選擇。 AEM提供前所未有的彈性，讓您能夠運用這兩種模型在專案中的優勢。

![AEM實作模型](headless/assets/aem-implementation-models.png)

在標題式或完整堆疊模型中，內容會以Java、HTL等為基礎，在AEM儲存庫和AEM元件中管理。 會用來轉譯使用者體驗的內容。 在此模型中，建立內容、設定內容樣式、展示內容，並在AEM中傳遞所有內容。

在無頭模型中，內容會在AEM儲存庫中管理，但是會透過REST和GraphQL等API傳送至其他系統，以呈現內容以提供使用者體驗。 在此模型中，內容是在AEM中建立的，但是會設定樣式、呈現內容，並在其他平台上發佈。

「單頁應用程式」(SPA)通常是AEM無端傳送內容的目的地。 不過，這些SPA不一定完全是AEM的外部。 AEM可讓您決定SPA與AEM的整合程度。 我們舉個例子

## Web Shop範例{#web-shop-example}

假設您有現有的網站商店，做為SPA提供給您的公司。 其中包含您所有的產品詳細資訊和影像。 然後您引進AEM，以強化您的行銷成果，例如促銷網站、部落格和促銷活動內容。 您如何整合兩者？ AEM可啟用多種選項：

* **允許系統獨立運行。**
* **透過GraphQL向Web Shop提供有限的AEM內容。** 內容可由作者在AEM中建立，但只能透過網頁商店SPA檢視。
* **在AEM中內嵌網頁商店SPA。** 內容可由作者在AEM中建立，並在AEM中在網頁商店的內容中檢視，但不受操控。
* **在AEM中內嵌網頁商店SPA，並啟用可編輯的點數。** 內容可由作者在AEM中建立，並在AEM中在Web Shop中檢視，而且作者在AEM中控制Web Shop SPA內容的能力有限。
* **在AEM中內嵌Web Shop SPA，並啟用整個區域進行編輯。** 內容可由作者在AEM中建立，並在AEM中在Web Shop中檢視，而且作者在AEM中控制Web Shop SPA內容的能力有限。

下節將更詳細地探討這些整合層級。

>[!NOTE]
>
>當然，您也可以使用AEM SPA編輯器架構，將網頁商店SPA重新建置為完整功能的AEM SPA [。](/help/implementing/developing/hybrid/introduction.md) 如果您已擁有AEM，並想要建立新的網頁商店或其他SPA，這是建議的方法，但超出本檔案的範圍。

## SPA整合級別{#integration-levels}

SPA整合在AEM中屬於四個層級。

* **0級：無整合**
   * SPA和AEM分別存在，且不交換任何資訊。
   * 內容是在兩個不同的系統中獨立建立、管理和傳送。
* **層級1:內容片段整合**
   * [內容](/help/assets/content-fragments/content-fragments.md) 片段用於AEM，以建立和管理SPA的有限內容。
   * SPA會透過AEM的[GraphQL API擷取此內容。](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 有些內容在AEM中管理，有些則在外部系統中管理。
   * 內容只能在SPA中檢視。
* **層級2:在AEM中內嵌SPA**
   * [內容](/help/assets/content-fragments/content-fragments.md) 片段用於AEM，以建立和管理SPA的內容。
   * SPA會透過AEM的[GraphQL API擷取此內容。](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 有些內容在AEM中管理，有些則在外部系統中管理。
   * 您可在AEM中以內容情境檢視內容。
   * 在AEM中可編輯有限的內容。
* **第3級：在AEM中內嵌並完全啟用SPA**
   * [內容](/help/assets/content-fragments/content-fragments.md) 片段用於AEM，以建立和管理SPA的內容。
   * SPA會透過AEM的[GraphQL API擷取此內容。](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 您可在AEM中以內容情境檢視內容。
   * 大部分的內容都可在AEM中編輯。

第1級是典型無頭實作的範例。 不過，內容作者只能在SPA中檢視其內容的內容內容。 AEM只是製作工具。

AEM的優勢和彈性在2和3級中變得明顯，同時仍保留SPA的優勢。 內容作者可以在AEM中建立其內容，但也可以在AEM中檢視其內容。 SPA具備在AEM中編寫，但仍以SPA形式提供的能力。

## 實作整合層級{#implementing}

AEM中有不同的工具可供使用，視您選擇的整合層級而定。 每個層級都以上一層所使用的工具為基礎。 下列清單連結至相關資源。

* **Level 1:** Content Fragments和 [AEM ](/help/implementing/developing/headless/introduction.md) leash Framework可用來將AEM內容傳送至SPA。
* **層級2:** 除了層級1:
   * [RemotePage元](/help/implementing/developing/hybrid/remote-page.md) 件可用來將外部SPA內嵌至AEM中，以便在AEM內容中檢視。
   * SPA上的某些點也可以啟用至[，以允許在AEM中進行有限編輯。](/help/implementing/developing/hybrid/editing-external-spa.md)
* **層級3:** 除層級2外：
   * SPA的整個區域都可以啟用，讓您在AEM中進行完整編輯。
