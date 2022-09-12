---
title: AEM中的Headful和Headless
description: AEM專案可以以無頭和無頭模型實作，但選項不是二進位。 AEM提供在單一專案中充分運用這兩種模型優點的彈性。
exl-id: 709850ca-7757-47ab-9625-f411121cde2c
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# AEM中的Headful和Headless {#headful-headless}

Adobe Experience Manager專案可在無頭和無頭兩種模型中實作，但選項並非二進位。 AEM提供在單一專案中充分運用這兩種模型優點的彈性。 本檔案提供並概述不同的模型，並說明SPA整合的層級。

## 總覽 {#overview}

AEM提供強大的工具，可在單一平台中管理內容的建立及其傳遞。 這是傳統的「有頭腦」內容管理模式，內容作者和開發人員可在相同平台上工作，將體驗提供給內容消費者。

AEM也可用來簡單地管理內容，讓內容的呈現和傳遞可由其他平台管理。 這是「無頭式」的內容管理模型，內容作者和開發人員在不同平台上工作，為內容消費者提供體驗。

但這不需要二進位選擇。 AEM提供前所未有的彈性，讓您可充分運用這兩種模型在專案中的優點。

![AEM實作模型](/help/headless/assets/aem-implementation-models.png)

在帶頭式或完整堆疊模型中，內容是根據Java、HTL等在AEM存放庫和AEM元件中管理。 用於呈現使用者體驗的內容。 在此模型中，建立內容、設定內容樣式、呈現內容，然後在AEM中傳送所有內容。

在無周邊模型中，內容會在AEM存放庫中管理，但透過API（例如REST和GraphQL）傳送至其他系統，以便為使用者體驗呈現內容。 在此模型中，內容是在AEM中建立，但會以樣式設定、呈現，以及傳遞所有內容都會發生在其他平台上。

單頁應用程式(SPA)通常是AEM無條件傳送內容的目的地。 不過，這些SPA不一定完全外部於AEM。 AEM可讓您決定將SPA整合至AEM的程度。 讓我們舉個例子。

## Web Shop範例 {#web-shop-example}

假設您已有公司的Web Shop作為SPA。 其中包含所有產品詳細資訊和影像。 然後您會導入AEM，以強化促銷網站、部落格和促銷活動內容等行銷工作。 如何整合兩者？ AEM可啟用一系列選項：

* **允許系統獨立運行。**
* **透過GraphQL從AEM提供有限內容給Web Shop。** 內容可由作者在AEM中建立，但只能透過網店SPA檢視。
* **將網店SPA內嵌在AEM中。** 內容可由作者在AEM中建立，並在AEM中於網店內容中檢視，但不受操控。
* **將Web Shop SPA內嵌在AEM中，並啟用可編輯的點。** 內容可由作者在AEM中建立，並在AEM中於Web Shop中檢視，而作者在AEM中操控Web Shop SPA內容的能力有限。
* **在AEM中嵌入網頁商店SPA，並啟用整個區域進行編輯。** 內容可由作者在AEM中建立，並在AEM中於Web Shop中檢視，而作者在AEM中操控Web Shop SPA內容的能力有限。

下一節將更詳細探討這些整合層級。

>[!NOTE]
>
>當然，您也可以將網店SPA重新實作為完全運作的AEM SPA [使用AEM SPA Editor架構。](/help/implementing/developing/hybrid/introduction.md) 如果您已有AEM且想要建立新的Web商店或其他SPA，則此為建議的方法，但不在本檔案的討論範圍內。

## SPA整合層級 {#integration-levels}

SPA整合屬於AEM的四個層級。

* **0級：無整合**
   * SPA和AEM分別存在，且不會交換任何資訊。
   * 內容是在兩個不同的系統中獨立建立、管理和傳送的。
* **第1級：內容片段整合**
   * [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md) 用於AEM中，以建立和管理SPA的有限內容。
   * SPA會透過AEM擷取此內容 [GraphQL API。](/help/headless/graphql-api/content-fragments.md)
   * 有些內容在AEM中管理，有些則在外部系統中管理。
   * 內容只能在SPA中檢視。
* **第2層：將SPA內嵌於AEM**
   * [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md) 用於AEM中，以建立和管理SPA的內容。
   * SPA會透過AEM擷取此內容 [GraphQL API。](/help/headless/graphql-api/content-fragments.md)
   * 有些內容在AEM中管理，有些則在外部系統中管理。
   * 可在AEM中以內容檢視內容。
   * 可在AEM中編輯有限的內容。
* **第3層：在AEM中內嵌並完全啟用SPA**
   * [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md) 用於AEM中，以建立和管理SPA的內容。
   * SPA會透過AEM擷取此內容 [GraphQL API。](/help/headless/graphql-api/content-fragments.md)
   * 可在AEM中以內容檢視內容。
   * 大部分內容都可在AEM內編輯。

1級是典型無頭式實作的範例。 不過，內容作者只能在SPA內以內容檢視其內容。 AEM只是製作工具。

在2和3級時，AEM的優點和彈性就變得明顯，同時仍保留SPA的優點。 內容作者可在AEM中建立其內容，但也可在AEM中以內容方式查看。 SPA可在AEM中撰寫，但仍以SPA形式提供。

## 實作整合層級 {#implementing}

AEM中有不同的工具可供使用，端視您選擇的整合層級而定。 每個層級都以先前使用的工具為基礎。 下列清單會連結至相關資源。

* **第1級：** 內容片段與 [AEM無頭框架](/help/headless/introduction.md) 可用來傳送AEM內容至SPA。
* **第2層：** 除了第一級：
   * [RemotePage元件](/help/implementing/developing/hybrid/remote-page.md) 可用來將外部SPA內嵌至AEM中，以便在內容中檢視AEM內容。
   * SPA上的某些點也可以啟用 [允許在AEM中進行有限編輯。](/help/implementing/developing/hybrid/editing-external-spa.md)
* **第3層：** 除了第二級：
   * SPA的整個區域都可啟用，以允許在AEM中進行全面編輯。
