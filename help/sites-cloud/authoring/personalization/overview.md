---
title: 個人化和內容鎖定
description: 了解如何使用AEM建立個人化、目標式內容
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: d2975ec84745f9520ead89588ab727af8e43b740
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 1%

---


# 個人化和內容鎖定 {#personalization-and-content-targeting}

您提供給客戶的網頁內容個人化，是指根據客戶的興趣和需求量身打造這些體驗。 您可以根據自己掌握的資訊來執行此操作；例如購物摘要、年齡、性別、地理等。

透過Adobe Experience Manager as a Cloud Service(AEM)，您可以建立選取的內容，然後指定將看到每個個別體驗的對象（一般使用者群組）。 這表示您正在鎖定特定對象的個人化體驗。

當您的閱讀程式上線時，您的定位引擎將會檢閱關於使用者的可用資訊，並與體驗定義進行比較。 然後引擎 *&quot;決定&quot;* 應顯示哪些個人化體驗。

AEM提供以下工具的架構：

* 根據可用的客戶資訊，製作適合眾多受眾的鎖定內容。
* 定義用來根據對象定義解析已知使用者資訊的規則。
* 設定您的頁面以呈現鎖定的個人化體驗；來呈現適用於目前使用者的特定內容。

下列概觀顯示AEMas a Cloud Service中用於個人化的一些詞語，及其後是建議的動作順序。

## 體驗 {#experience}

體驗是您想要向使用者顯示的內容。

## 個人化體驗 {#personalized-experience}

個人化體驗是指對有限對象顯示的體驗。 對象由您定義，且只有在目前使用者的已知資訊符合該對象定義時，才會顯示內容。

建立頁面時，您會定義多個體驗，每個體驗會解析為一（或多個）對象。 如果未解析任何對象，則會顯示預設體驗。

### 選件 {#offer}

優惠方案是個人化體驗，通常可在有限的時段內使用。

例如，範例網站的頁面可以使用選件作為預告影像，顯示在頁面頂端。 30歲以上的人和30歲以下的人會將不同的優惠方案視為體驗預告。

## 對象 {#audience}

受眾是您想透過個人化內容鎖定的一組使用者。 訪客開啟網頁時，頁面邏輯會根據已知資訊決定其所屬的對象。 根據該評估AEM顯示您為該對象建立的內容。

受眾是以行銷區段為基礎。 這些變數會在AEM或Adobe Target中建立；您可以使用「對象」主控台直接在AEM中建立Adobe Target對象。

### 區段 {#segment}

在AEM ContextHub中，受眾是根據規則（條件）定義為區段。 接著會解析這些內容，以呈現所需內容。

## 活動 {#activity}

活動：

* 定義特定對象（區段）與特定體驗的對應
* 定義套用定位的時段
* 識別 [目標引擎](#targeting-engine) 您的頁面使用

活動可以是個人化活動或A/B測試活動(在AEM和Adobe Target個人化工作流程的案例中)。

例如，活動可定義兩個不同對象的體驗：30歲以上的人和30歲以下的人。 然後，您網站的某個頁面可能會針對每個對象顯示不同的產品。

或者，作為另一個例子，您的產品目錄可能包括專注於季節性產品的茶匙。 因此，夏季運動活動可能會定義茶具在夏季月份鎖定的對象。

使用 [活動主控台](/help/sites-cloud/authoring/personalization/activities.md) 為 [品牌](#brand). 您也可以在製作活動時建立活動 [目標內容](/help/sites-cloud/authoring/personalization/targeted-content.md) with [定位模式](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode).

### 品牌 {#brand}

品牌包含一系列行銷活動和區域。

使用活動控制台建立品牌時，該品牌也會顯示在選件控制台中。

### 區域 {#area}

區域是品牌的細分。

## 定位模式 {#targeting-mode}

製作時，這是用來啟動和設定個人化元件的編輯模式。

您可以 [製作目標內容](/help/sites-cloud/authoring/personalization/targeted-content.md) 使用AEM的「定位」模式。 定位模式和Target元件提供工具，用於建立行銷活動體驗的內容。

## 體驗片段 {#experience-fragments}

組成體驗的分組元件集。

[體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) 由內容和資訊（樣式等）組成，以建立體驗；頁面編寫時可直接使用。 它們可視為AEM頁面的子集。 它們可讓內容作者跨管道重複使用內容，包括網站頁面和協力廠商系統。

在個人化範例中，您可以結合標題、影像、說明和動作呼叫按鈕來形成預告體驗。 使用體驗片段是使用Adobe Target個人化的重要一環。

## 定位引擎 {#targeting-engine}

定位引擎是解析目標內容邏輯的機制。 [活動](/help/sites-cloud/authoring/personalization/activities.md) 已設定為使用兩個可用定位引擎之一：AEM和Adobe Target。

定位引擎是決定要使用哪個個人化系統的平台或機制。

目前AEM可使用：

* [AEM ContextHub](#aem-contexthub) (標準AEM)
* the [Adobe Target](#adobe-target) 個人化引擎

>[!CAUTION]
>
>單一AEM頁面無法同時使用兩個引擎。
>
>您可以在相同網站內的個別頁面上使用這兩個引擎。

### AEM ContextHub {#aem-contexthub}

AEM提供內建的定位引擎ContextHub，用於處理頁面請求並決定要顯示的內容。 使用AEM定位引擎時，您只能使用在AEM中建立的區段來定義體驗的對象。

### Adobe Target {#adobe-target}

Adobe Target定位引擎會使從頁面造訪收集到的資訊在Adobe Target中受到追蹤。

* 使用此定位引擎時，您會使用從Adobe Target匯入的區段來定義體驗的對象。
* 使用Adobe Target引擎的活動包括 [已同步到Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

若您有 [與Adobe Target整合](/help/sites-cloud/integrating/integration-adobe-target-ims.md).

## 如何設定您的個人化內容 {#how-to-setup-personalized-content}

提供個人化內容需要各種步驟和定義：

1. 將AEM與您的定位引擎整合。

1. 設定對象。

   1. 根據您的定位引擎，定義對象或區段以及規則。

1. 建立您的品牌和活動。

1. 製作您要向各種對象顯示的體驗選集。

1. 將體驗鎖定在特定對象（區段），借此個人化這些體驗。