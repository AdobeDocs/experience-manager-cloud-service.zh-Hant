---
title: 無頭AEM
description: 項AEM目可以採用無頭和無頭的模式，但選擇不是二進位的。 為在AEM一個項目中利用這兩種模型的優點提供了靈活性。
exl-id: 709850ca-7757-47ab-9625-f411121cde2c
source-git-commit: e592dd7a3a717259493f23943933fe3d0e71b7ab
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# 無頭AEM {#headful-headless}

Adobe Experience Manager項目可以採用頭腦式和頭腦式兩種模式，但選擇不是二元的。 為在AEM一個項目中利用這兩種模型的優點提供了靈活性。 本文檔提供並概述了不同的模型，並介紹了整合SPA級別。

## 概覽 {#overview}

提AEM供了功能強大的工具，可管理內容的建立和在一個平台中的交付。 這是一種傳統的內容管理「大頭」模式，內容作者和開發人員在同一平台上工作，以向內容消費者提供體驗。

還可AEM以用於簡單地管理內容，允許由另一個平台管理內容的演示和傳遞。 這是內容管理的「無頭」模式，內容作者和開發人員在不同的平台上工作，為內容消費者提供體驗。

但這不一定是二進位的選擇。 提供AEM前所未有的靈活性，使您能夠利用這兩種模型對項目的優勢。

![實AEM施模式](/help/headless/assets/aem-implementation-models.png)

在頭型或全棧模型中，內容在儲存庫AEM和元件AEM中基於Java 、 HTL等進行管理。 用於為用戶體驗呈現內容。 在這個模型中，建立內容、設計內容、展示內容，以及交付內容都發生在AEM中。

在無頭模型中，內容在儲存庫中AEM被管理，但是通過API（如REST和GraphQL）將內容傳送到另一個系統，以便為用戶體驗呈現內容。 在此模型中，內容是在中創AEM建的，但是定義它，展示它，並交付它所有內容都發生在另一個平台上。

單頁應用程式SPA()通常是無需由它提供的內容的AEM目標。 然而，這SPA些不必完全是外部AEM的。 允AEM許您決定整合到SPA何種程度AEM。 我們舉個例子。

## Web Shop示例 {#web-shop-example}

假設您公司現有的Web商店SPA。 您擁有您所有的產品詳細資訊和影像。 然後，您介AEM紹以推動您的營銷工作，如促銷網站、部落格和促銷活動內容。 如何整合兩者？ 啟AEM用一系列選項：

* **允許系統獨立運行。**
* **通過GraphQL為Web商店提供有限AEM的內容。** 內容可由作者在中創AEM建，但只能通過Web商店查看SPA。
* **將Web商店嵌SPA入AEM。** 內容可由作者在中創AEM建，並在WebAEM商店的上下文中查看，但不受操作。
* **將Web商店嵌SPA入AEM，並啟用可編輯點。** 內容可由作者在AEM中建立，AEM並在Web商店的上下文中查看，並且作者在Web商店內操縱內容的能力SPA有限AEM。
* **將網頁商店SPA嵌AEM入，並啟用整個區域進行編輯。** 內容可由作者在AEM中建立，AEM並在Web商店的上下文中查看，並且作者在Web商店內操縱內容的能力SPA有限AEM。

下一節將更詳細地探討這些整合級別。

>[!NOTE]
>
>當然，您也可以將Web商店重新SPA實施為功能完AEM全SPA的 [使用編AEM輯器SPA框架。](/help/implementing/developing/hybrid/introduction.md) 如果您已AEM經且希望建立新Web商店或其SPA他網站，則建議使用此方法，但它不在本文檔的範圍內。

## 集SPA成級別 {#integration-levels}

整SPA合在四個層次AEM。

* **0級：無整合**
   * 和SPA分AEM開存在，不交換資訊。
   * 內容是在兩個獨立的系統中獨立建立、管理和提供的。
* **第1級：內容片段整合**
   * [內容片段](/help/assets/content-fragments/content-fragments.md) 用於創AEM建和管理受限內SPA容。
   * 將SPA此內容檢索AEM到 [GraphQL API。](/help/headless/graphql-api/content-fragments.md)
   * 某些內容在外部AEM系統中管理，有些在外部系統中管理。
   * 只能在中查看內SPA容。
* **第2級：嵌SPA入AEM**
   * [內容片段](/help/assets/content-fragments/content-fragments.md) 用於創AEM建和管理內容SPA。
   * 將SPA此內容檢索AEM到 [GraphQL API。](/help/headless/graphql-api/content-fragments.md)
   * 某些內容在外部AEM系統中管理，有些在外部系統中管理。
   * 內容可在內的上下文中查AEM看。
   * 可在中編輯有限的內AEM容。
* **第3級：在中嵌入並完SPA全啟AEM用**
   * [內容片段](/help/assets/content-fragments/content-fragments.md) 用於創AEM建和管理內容SPA。
   * 將SPA此內容檢索AEM到 [GraphQL API。](/help/headless/graphql-api/content-fragments.md)
   * 內容可在內的上下文中查AEM看。
   * 大多數內容都可在內AEM編輯。

1級是典型無頭實施的示例。 但內容作者只能在中的上下文中查看其內SPA容。 只AEM是創作工具。

在2和3級AEM時，其優勢和靈活性變得明顯，同時仍保SPA持。 內容作者可以在中創AEM建其內容，但也可以在上下文中查AEM看。 這SPA種能力在中提AEM供，但仍作為文SPA件。

## 實施整合級別 {#implementing}

根據您選擇的集AEM成級別，可用的工具不同。 每個級別都建立在上一級所使用的工具之上。 以下清單連結到相關資源。

* **第1級：** 內容片段和 [無頭框架](/help/headless/introduction.md) 可用於將內AEM容傳送到SPA。
* **第2級：** 除第一級：
   * [RemotePage元件](/help/implementing/developing/hybrid/remote-page.md) 可用於將外部內容SPA嵌AEM入到AEM上下文中查看的內容。
   * 還可SPA以啟用 [允許在中進行有限的編AEM輯。](/help/implementing/developing/hybrid/editing-external-spa.md)
* **第3級：** 除了第二級：
   * 可以啟用SPA整個區域，以便在中進行全面編AEM輯。
