---
title: 個人化和內容鎖定
description: 了解AEM如何建立個人化內容
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# 個人化和內容鎖定 {#personalization}

## 個人化和內容鎖定 {#personalization-and-content-targeting}

AEM提供工具架構，用於編寫目標內容及呈現個人化體驗。

## 定位模式 {#targeting-mode}

[製作目標內容](/help/sites-cloud/authoring/personalization/targeted-content.md) 使用AEM的目標定位模式。 定位模式和Target元件提供工具，用於建立行銷活動體驗的內容。

## 活動 {#activities}

活動可定義並組織您的行銷工作。 活動包含您要鎖定的對象，以及套用鎖定目標的時段。

例如，您的產品目錄可能包括專注於季節性產品的茶匙。 「夏季運動」活動會定義茶具在夏季月份鎖定的行銷區段。

活動也會識別 [目標引擎](#targeting-engine) 頁面所使用。

使用 [活動主控台](/help/sites-cloud/authoring/personalization/activities.md) 來建立和管理您品牌的活動。 您也可以像您一樣建立活動 [作者目標內容](/help/sites-cloud/authoring/personalization/targeted-content.md).

## 體驗 {#experiences}

您會針對每個活動定義一或多個體驗，以識別您要鎖定的對象。 AEM可讓您控制包含每個體驗的內容。

受眾是根據在AEM或Adobe Target中建立的行銷區段。 訪客開啟網頁時，頁面邏輯會決定其所屬的對象，並顯示您為該對象建立的內容。

例如，活動會定義兩個不同對象的體驗：30歲以上婦女和30歲以下婦女。 網站的女性頁面可能會針對每個體驗顯示不同的產品。

您定義活動的體驗。 您可以使用 [活動主控台](/help/sites-cloud/authoring/personalization/activities.md#adding-editing-an-activity-using-the-activities-console) 或 [定位模式](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode) 將體驗新增至活動。

## 選件 {#offers}

選件是顯示在體驗之頁面上某個位置的內容。 針對不同的體驗使用不同的選件，以最大化內容對對象的效益。

例如，範例網站的女性頁面可以使用選件作為預告影像，顯示在頁面頂端。 另一個優惠方案則用作30歲以上女性體驗和30歲以下女性體驗的預告。

使用 [選件主控台](/help/sites-cloud/authoring/personalization/offers.md) 來建立可在多個體驗中使用的選件。 建立單一使用選件，或在 [製作目標內容](/help/sites-cloud/authoring/personalization/targeted-content.md).

## 定位引擎 {#targeting-engine}

定位引擎是驅動目標內容邏輯的機制。 [活動](/help/sites-cloud/authoring/personalization/activities.md) 已設定為使用兩個可用定位引擎之一：AEM和Adobe Target。

### AEM {#aem}

AEM提供內建的定位引擎，可處理頁面要求並決定要顯示的內容。 使用AEM定位引擎時，您只能使用在AEM中建立的區段來定義體驗的對象。

### Adobe Target {#adobe-target}

Adobe Target定位引擎會使從頁面造訪收集到的資訊在Adobe Target中受到追蹤。

* 使用此定位引擎時，您會使用從Adobe Target匯入的區段來定義體驗的對象。
* 使用Adobe Target引擎的活動包括 [已同步到Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

與Adobe Target整合後，即可使用此引擎。 <!--You can use this engine when you have [integrated with Adobe Target](/help/sites-administering/opt-in.md).-->
