---
title: 選擇編寫方法
description: 瞭解在決定如何在AEM中撰寫內容時的重要考量，以協助您為內容作者做出最佳決策。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 15eef2d3790d1c0cf5414ca55b191de5b644fed0
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# 選擇編寫方法 {#authoring-methods}

瞭解在決定如何在AEM中撰寫內容時的重要考量，以協助您為內容作者做出最佳決策。

## 考量事項概觀 {#overview}

無論您選擇檔案式撰寫還是WYSIWYG撰寫，AEM的彈性都能確保滿足您的撰寫需求。 開始考量時，請牢記以下事實。

* **一律讓內容作者參與決定。** — 您的內容作者是您的專家，他們的見解至關重要。
* **可以實作多種編寫方法。** — 雖然Adobe建議從簡單的開始，視需要分層處理複雜性，但多個撰寫方法可以在一個專案中一起運作。
* **您一律可以在事後變更您的編寫方法。** — 無論您決定要鎖定的專案。 在Adobe自動化移轉工具的協助下，您可以直接改變方法。
* **您不得在實施之前決定，而是必須作為實施的一部分決定。** - AEM是一個統一產品，因此這項重要決定不必是合約協商的一部分。 當您購買AEM時，就能獲得所有功能。 這其實是實作期間的決定。

Adobe可協助您在實作過程中決定最符合需求的方法（或方法）。

## 一種大小不適合全部 {#one-size}

AEM的每個實作都有自己的工作流程和目標。 一個專案可能涉及簡單的編寫模型，內容作者負責自己的出版物。 而另一個則可能有複雜的貢獻者和核准網路。

![不同的編寫工作流程](assets/authoring-workflows.png)

不同的專案可能有不同的（和多個）使用案例。

![使用案例](assets/use-cases.png)

Adobe瞭解這一點，因此不提供萬能的方法。 AEM是您的單一解決方案，提供不同的內容傳送和內容建立方法，以最符合您的需求。

若要決定最佳方法，您必須考量四個專案。

1. [您有內容傳送偏好設定嗎？](#content-delivery)
1. [您有內容編寫偏好設定嗎？](#content-authoring)
1. [您的專案目標是什麼？](#project-goals)
1. [您目前面臨哪些撰寫挑戰？](#authoring-challenges)

## 內容傳遞偏好設定 {#content-delivery}

您首先要考慮的應該是您希望如何傳送內容。 Edge Delivery Services提供極快的網站速度，但也許您的關注點在於headless交付。 以下決策樹可協助您考慮選項。

![內容傳遞決策樹](assets/content-delivery-decision-tree.png)

這可協助您決定是否需要：

* 使用內容片段編輯器和/或通用編輯器將[AEM用作Headless CMS](/help/headless/introduction.md)。
* 使用[以檔案為基礎的編輯](/help/edge/docs/authoring.md)或[WYSIWYG編寫與通用編輯器](/help/edge/wysiwyg-authoring/authoring.md)的AEMEdge Delivery Services。

## 內容製作偏好設定 {#content-authoring}

您下一個考量應該是您要如何編寫內容。 以下決策樹可協助您考慮選項。

![內容製作決策樹](assets/content-authoring-decision-tree.png)

這可協助您決定是否需要：

* 使用[檔案式編輯的AEMEdge Delivery Services。](/help/edge/docs/authoring.md)
* [使用通用編輯器進行WYSIWYG製作。](/help/edge/wysiwyg-authoring/authoring.md)

## 專案目標 {#project-goals}

您認為成功撰寫了什麼？ 如何定義專案的成功？

* 您可能需要讓更多人能夠建立內容，但希望避免接受新工具集的訓練。 （不妨考慮檔案式製作。）
* 您可能需要增加產生的內容量。 （不妨考慮檔案式製作。）
* 也許您需要專注於視覺內容版面配置，但儘量減少對編碼知識的需求。 （想想WYSIWYG製作。）

在實作開始時闡明明確的專案目標，可協助您針對編寫方法做出明智的決定。

## 製作挑戰 {#authoring-challenges}

最後，請考量您創作內容時現今面臨的特定挑戰。

* 您可能會遇到與在CMS外部建立的內容重複的工作，然後需要匯入或複製並貼上。 （不妨考慮檔案式製作。）
* 您可能需要縮短培訓作者如何使用CMS所需的時間。 （不妨考慮檔案式製作。）
* 也許您的作者需要經常編輯內容的視覺版面，需要持續開發人員的支援。 （想想WYSIWYG製作。）
