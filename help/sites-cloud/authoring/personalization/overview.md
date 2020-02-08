---
title: 個人化與內容定位
description: 瞭解AEM如何建立個人化內容
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# 個人化與內容定位 {#personalization}

## 個人化與內容定位 {#personalization-and-content-targeting}

AEM提供工具架構，以製作目標內容並呈現個人化體驗。

## 定位模式 {#targeting-mode}

[使用AEM的「定位](/help/sites-cloud/authoring/personalization/targeted-content.md) 」模式來製作目標內容。 定位模式和Target元件提供工具，讓您建立行銷活動體驗的內容。

## 活動 {#activities}

活動可定義並組織您的行銷工作。 活動包括您要定位的對象，以及套用定位的時段。

例如，您的產品目錄可能包含注重季節性產品的茶具。 「夏季運動」活動定義了茶具在夏季月份鎖定的行銷區段。

活動也會識別 [您的頁面](#targeting-engine) 所使用的定位引擎。

使用「 [活動」主控台](/help/sites-cloud/authoring/personalization/activities.md) ，建立並管理您品牌的活動。 您也可以在製作目標內容時 [建立活動](/help/sites-cloud/authoring/personalization/targeted-content.md)。

## 體驗 {#experiences}

針對每個活動，您定義一或多個體驗，以識別您所鎖定的對象。 AEM可讓您控制包含每個體驗的內容。

觀眾是以在AEM或Adobe target中建立的行銷區段為基礎。 當訪客開啟網頁時，頁面邏輯會決定其所屬的對象，並顯示您為該對象建立的內容。

例如，活動會定義兩個不同對象的體驗：30歲以上婦女和30歲以下婦女。 網站的女性頁面可能會針對每個體驗顯示不同的產品。

您定義活動的體驗。 您可以使用「活 [動」主控台](/help/sites-cloud/authoring/personalization/activities.md#adding-editing-an-activity-using-the-activities-console) 或「 [定位」模式](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode) ，將體驗新增至活動。

## 選件 {#offers}

選件是顯示在頁面上體驗位置的內容。 針對不同的體驗使用不同的選件，為您的受眾提供最佳的內容效果。

例如，範例網站的女性頁面可以使用選件作為出現在頁面頂端的摘要影像。 不同的選件會用作「女性30歲以上（女性30歲以下）」體驗和「女性30歲以下（女性30歲以下）」體驗的摘要。

使用選 [件主控台](/help/sites-cloud/authoring/personalization/offers.md) ，建立可用於多個體驗的選件。 在製作目標內容時，從選件程式庫建立單一用途的選件或 [新增選件](/help/sites-cloud/authoring/personalization/targeted-content.md)。

## Targeting Engine {#targeting-engine}

定位引擎是驅動定位內容邏輯的機制。 [活動](/help/sites-cloud/authoring/personalization/activities.md) 」設定為使用兩個可用的定位引擎之一：AEM和Adobe Target。

### AEM {#aem}

AEM提供內建定位引擎，可處理頁面請求並決定要顯示的內容。 使用AEM定位引擎時，您只能使用在AEM中建立的區段來定義體驗的觀眾。

### Adobe Target {#adobe-target}

Adobe target定位引擎會在Adobe target中追蹤從頁面瀏覽收集到的資訊。

* 使用此定位引擎時，您會使用從Adobe Target匯入的區段來定義體驗的觀眾。
* 使用Adobe target引擎的活動會 [同步至Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target)。

當您與Adobe Target整合後，即可使用此引擎。 <!--You can use this engine when you have [integrated with Adobe Target](/help/sites-administering/opt-in.md).-->
