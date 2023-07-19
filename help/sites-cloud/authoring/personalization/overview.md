---
title: 個人化和內容目標鎖定
description: 了解如何使用 AEM 建立個人化、鎖定目標的內容
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 100%

---


# 個人化和內容目標鎖定 {#personalization-and-content-targeting}

將您提供給客戶的網頁內容個人化，表示根據他們的興趣和需求量身打造這些體驗。你可以根據你掌握的關於他們的資訊來進行；例如購物摘要、年齡、性別、地理位置等。

有了 Adobe Experience Manager as a Cloud Service (AEM)，您可以建立一系列內容，然後指定哪些對象 (一般使用者群組) 會看到每個個別體驗。這表示您的個人化體驗的目標鎖定在特定對象。

當您的讀者在線時，目標定位引擎將查看此一般使用者的相關資訊，並將其與體驗定義相比較。然後，引擎&#x200B;*「決定」*&#x200B;應該顯示哪些個人化體驗。

AEM 提供一個工具框架，用於：

* 根據可用的客戶資訊，編寫已鎖定目標、適合一系列對象的內容。
* 定義規則，這些規則用於根據對象定義來解析已知使用者資訊。
* 設定您的頁面以呈現已鎖定目標的個人化體驗；呈現適用於目前一般使用者的特定內容。

以下概觀介紹 AEM as a Cloud Service 中用於個人化的一些術語，接著是建議的動作順序。

## 體驗 {#experience}

體驗是您想要向一般使用者展示的內容。

## 個人化體驗 {#personalized-experience}

個人化體驗是向有限對象展示的體驗。對象由您定義，只有當目前一般使用者的已知資訊對應該對象定義時，才會顯示內容。

建立頁面時，您定義了多個體驗，每個體驗都解析至一個 (或多個) 對象。如果未解析任何對象，則會顯示預設體驗。

### 選件 {#offer}

選件是一種個人化體驗，通常在有限的時間內提供。

例如，來自範例網站的頁面可以使用選件做為出現在頁面頂端的預告影像。30 歲以上的人和 30 歲以下的人將看到作為體驗預告的不同選件。

## 對象 {#audience}

對象是一般使用者群組，是個人化內容鎖定的目標。當訪客開啟網頁時，頁面邏輯會根據已知資訊決定他們所屬的對象。根據評估結果，AEM 會顯示您為該對象建立的內容。

對象是以行銷區段為基礎。它們是在 AEM 或 Adobe Target 中建立的；您可以使用對象主控台直接在 AEM 中建立 Adobe Target 對象。

### 區段 {#segment}

在 AEM ContextHub 中，對象被定義為根據規則 (條件) 的區段。然後，解析區段以呈現所需內容。

## 活動 {#activity}

活動：

* 定義特定對象 (區段) 與特定體驗的對應
* 定義套用目標鎖定的時段
* 識別頁面使用的[目標定位引擎](#targeting-engine)

活動可以是個人化活動，也可以是 A/B 測試活動 (在 AEM 和 Adobe Target 個人化工作流程的情況下)。

例如，一項活動可以為兩個不同的對象定義體驗：30 歲以上的人和 30 歲以下的人。然後，網站的一個頁面可能會為每個對象顯示不同的產品。

或者，舉另一個範例，您的產品目錄可能包含強調季節性產品的預告片。因此，夏季運動會活動可能會定義夏季預告片的目標對象。

使用[活動主控台](/help/sites-cloud/authoring/personalization/activities.md)為[品牌](#brand)建立和管理活動。您也可以在使用[目標定位模式](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode)編寫[已鎖定目標的內容](/help/sites-cloud/authoring/personalization/targeted-content.md)時建立活動。

### 品牌 {#brand}

品牌擁有一系列行銷活動和區域。

當您使用活動主控台建立品牌時，它也會出現在選件主控台中。

### 區域 {#area}

區域是品牌的細分。

## 目標定位模式 {#targeting-mode}

編寫時，這是用於啟動和設定個人化元件的編輯模式。

您可以使用 AEM 目標定位模式[編寫已鎖定目標的內容](/help/sites-cloud/authoring/personalization/targeted-content.md)。目標定位模式和目標元件提供用於建立行銷活動體驗內容的工具。

## 體驗片段 {#experience-fragments}

組成體驗的一組元件。

[體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment)由內容和資訊 (樣式等) 組成用於建立體驗；它們可以在編寫頁面時直接使用。它們可以被視為 AEM 頁面的子集。可讓內容作者重複使用跨管道的內容，包括 Sites 頁面和協力廠商系統。

對於個人化範例，可以將標題、影像、描述和行動號召按鈕合併以形成預告片體驗。使用體驗片段是使用 Adobe Target 個人化的關鍵部分。

## 目標定位引擎 {#targeting-engine}

目標定位引擎是將已鎖定目標之內容的邏輯進行解析的機制。[活動](/help/sites-cloud/authoring/personalization/activities.md)設定為使用兩個可用的目標定位引擎之一：AEM 和 Adobe Target。

目標定位引擎是決定要使用哪種個人化系統的平台或機制。

目前 AEM 可以使用：

* [AEM ContextHub](#aem-contexthub) (標準 AEM)
* [Adobe Target](#adobe-target)個人化引擎

>[!CAUTION]
>
>單一 AEM 頁面不能同時使用這兩個引擎。
>
>您可以在同一網站的不同頁面上使用這兩個引擎。

### AEM ContextHub {#aem-contexthub}

AEM 提供內建目標定位引擎 [ContextHub](/help/implementing/developing/personalization/contexthub.md)，用於處理頁面要求並決定要顯示的內容。使用 AEM 目標定位引擎時，您只能使用在 AEM 建立的區段來定義體驗的對象。

### Adobe Target {#adobe-target}

[Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) 目標定位引擎會使頁面被造訪時所收集的資訊在 Adobe Target 中被追蹤。

* 使用此目標定位引擎時，您可以使用從 Adobe Target 匯入的區段來定義體驗的對象。
* 使用 Adobe Target 引擎的活動[會同步到 Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target)。

如果[已整合 Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)，即可使用此引擎。

## 如何設定您的個人化內容 {#how-to-setup-personalized-content}

傳遞個人化內容需要各種步驟和定義：

1. 透過以下任一方式設定目標定位引擎：

   1. 設定 [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md)
   1. 整合 [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)

1. 設定對象。

   1. 視目標定位引擎而定，定義[Target 對象](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)或 [ContextHub 區段](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)以及規則。

1. 建立[品牌和活動](/help/sites-cloud/authoring/personalization/activities.md)。

1. 編寫您想要向各種不同對象展示的體驗選集。

1. 透過將其[目標定位](/help/sites-cloud/authoring/personalization/targeted-content.md)在特定對象 (區段) 來個人化這些體驗。