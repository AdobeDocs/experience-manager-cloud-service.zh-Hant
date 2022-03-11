---
title: 個性化和內容目標
description: 瞭解如何AEM建立個性化內容
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# 個性化和內容目標 {#personalization}

## 個性化和內容目標 {#personalization-and-content-targeting}

提AEM供用於創作目標內容和呈現個性化體驗的工具框架。

## 目標模式 {#targeting-mode}

[作者目標內容](/help/sites-cloud/authoring/personalization/targeted-content.md) 使用的目標模式AEM。 目標模式和目標元件提供了工具，用於為您的營銷活動體驗建立內容。

## 活動 {#activities}

活動定義和組織您的營銷工作。 活動包括您所針對的受眾以及應用目標的時間段。

例如，您的產品目錄可能包括專門關注季節性產品的茶具。 夏季體育活動定義了茶具在夏季月份瞄準的市場細分。

活動還確定 [目標引擎](#targeting-engine) 你的頁面所用。

使用 [活動控制台](/help/sites-cloud/authoring/personalization/activities.md) 建立和管理品牌的活動。 您還可以建立活動 [作者目標內容](/help/sites-cloud/authoring/personalization/targeted-content.md)。

## 體驗 {#experiences}

對於每個活動，您都定義一個或多個體驗，這些體驗標識您所針對的受眾。 使您AEM能夠控制包含每種體驗的內容。

觀眾基於在Adobe Target或建立的營AEM銷部門。 當訪問者開啟網頁時，頁面邏輯將確定他們所屬的訪問群體並顯示您為該訪問群體建立的內容。

例如，活動定義兩個不同受眾的體驗：30歲以上婦女和30歲以下婦女。 網站的女性頁面可能會針對每種體驗顯示不同的產品。

定義活動的體驗。 您可以使用 [活動控制台](/help/sites-cloud/authoring/personalization/activities.md#adding-editing-an-activity-using-the-activities-console) 或 [目標模式](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode) 向活動添加體驗。

## 選件 {#offers}

優惠是顯示在頁面上某個位置以獲得體驗的內容。 使用不同的服務來提供不同的體驗，以最大限度地提高內容對受眾的效率。

例如，示例網站的婦女頁面可以使用優惠作為顯示在頁面頂部的誘惑影像。 對於30歲以上的女性和30歲以下的女性，則採用不同的報價作為誘惑。

使用 [提供控制台](/help/sites-cloud/authoring/personalization/offers.md) 建立可在多種體驗中使用的優惠。 在以下情況下建立一次性優惠或從優惠庫中添加優惠 [創作目標內容](/help/sites-cloud/authoring/personalization/targeted-content.md)。

## 目標引擎 {#targeting-engine}

目標引擎是驅動目標內容邏輯的機制。 [活動](/help/sites-cloud/authoring/personalization/activities.md) 已配置為使用兩個可用的目標引擎之一：和AEMAdobe Target。

### AEM {#aem}

提AEM供一個內置目標引擎，用於處理頁面請求並確定要顯示的內容。 使用目標引AEM擎時，您只能使用在中建立的段來定義AEM您的體驗的受眾。

### Adobe Target {#adobe-target}

Adobe Target瞄準引擎使從網頁訪問中收集到的資訊在Adobe Target得到跟蹤。

* 使用此目標引擎時，您會使用從Adobe Target導入的段來定義您的體驗的受眾。
* 使用Adobe Target引擎的活動 [已同步到目標](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target)。

當你與Adobe Target整合時，你可以使用這個引擎。 <!--You can use this engine when you have [integrated with Adobe Target](/help/sites-administering/opt-in.md).-->
