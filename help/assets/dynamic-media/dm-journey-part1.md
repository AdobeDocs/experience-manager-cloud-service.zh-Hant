---
title: Dynamic Media歷程，第一部分
description: Dynamic Media歷程涵蓋Dynamic Media的基本概念、運作方式、可為您做哪些事，以及可為您的工作和客戶帶來哪些價值。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles,Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '3614'
ht-degree: 3%

---

# Dynamic Media歷程：基礎知識，第一部分 {#dm-journey-part1}

{{see-also-dm}}

歡迎使用Dynamic Media歷程。

此歷程涵蓋Dynamic Media的基本概念、運作方式、可為您做的事情，以及可為您的工作和客戶帶來的價值。

**_先決條件_**

* 影像和視訊格式的基本瞭解
* 對HTML和CSS的基本瞭解
* 基本瞭解Adobe Illustrator、Adobe Photoshop、Adobe XD等設計工具
* 在Experience Manager上存取Dynamic Media有所幫助，但並非必要

**_您可以瞭解的內容_**

_第一部分_

* 什麼是Dynamic Media以及它如何協助您？
* Dynamic Media的使用案例
* 資產如何流經Dynamic Media系統

_第二部分_

* Dynamic Media URL剖析，以及Dynamic Media如何傳遞內容
* 建立影像預設集以轉譯資產的基礎知識
* 影像集、迴轉集及混合媒體集

**_對象_**
剛接觸Experience Manager上Dynamic Media的以下受眾最適合此歷程的讀者：

* 管理員
* 業務分析師
* 內容架構師
* 內容作者
* Designer
* 開發人員
* 行銷
* 產品經理/擁有者

>[!TIP]
>
>為達到最佳效果，Adobe建議您透過桌上型電腦閱讀及檢視此Dynamic Media歷程。

## 什麼是Dynamic Media以及它如何協助您？ {#dm-journey-a}

Dynamic Media 能協助您按照需求提供豐富的視覺化銷售和行銷資產。亦能協助您建立與提供互動式檢視體驗，包括縮放、360 度迴轉和影片。您的資產會動態擴展，以供網頁、行動裝置及社交網站使用。Dynamic Media 使用一組主要來源資產 (例如影像、影片和 3D)，透過其全球可擴展、效能最佳化的 CDN (內容傳遞網路) 即時產生並傳遞此豐富內容的多種變化版本。

Dynamic Media整合Adobe Experience Manager Assets數位資產管理解決方案的工作流程，以簡化及簡化數位行銷活動管理程式。

### 單一檔案，提供無限可能

有關Dynamic Media要瞭解的要點之一，就是&#x200B;_單一主要資產檔案的概念，具有無限可能性_。

若要更深入瞭解此概念，請思考您傳統上使用單一資產（例如影像或影片）的方式。 您通常會建立一個主要資產。 接著，您可以為每個體驗、所需每個裝置、每個網頁及其使用處的每個屬性，手動建立相同資產的版本。 隨著時間過去，該單一資產可能會增加到20個、30個或更多版本，且沒有附加版本記錄。 現在，想像一下針對您擁有的每個影像或視訊執行此動作。 資產版本的數目將很快變得難以維護和更新，更不用說儲存成本的增加了。

不過，Dynamic Media與其他系統截然不同，因為您會使用它，從單一、主要資產和URL呼叫，以動態方式傳送您的媒體&#x200B;__。 您請求的Dynamic Media URL路徑包含指示，告知Adobe發佈伺服器如何在資產傳送至客戶熒幕時顯示資產。 例如，使用相同的單一主要資產，您可以讓資產以無限制的轉譯立即傳送，並變更大小、格式、解析度、重量、顏色、裁切和縮放檢視等效果。

這種獨特的傳送方式可確保將一致的品質體驗傳送至任何畫面，無論畫面大小或頻寬為何。 全尺寸視訊也針對所有熒幕型別最佳化，並以適應性串流處理，同時確保使用者體驗的一致性、品質。

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![Adobe Dynamic Media會將相同的主要影像提供給不同大小和格式的不同媒體](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_Adobe Dynamic Media可確保在任何熒幕都能提供一致、高品質的體驗，無論熒幕大小或頻寬為何。_

閱讀本文，您將深入瞭解「單一主要資產檔案，無限可能」的概念為何如此重要。

### 內容傳遞網路

當您準備好使用影像資產或視訊資產時，Dynamic Media的中樞會提供支援，其中包括強大的頂層傳送網路。 該網路每天為全世界數百個使用者端提供服務。 資產會分散在由Akamai託管的內容傳遞網路（或CDN）上。 CDN是一種以網路連線方式的電腦服務系統，能以透明方式合作，將內容（尤其是大型多媒體內容）傳送給使用者。

在CDN系統中，網頁內容會儲存在網際網路上的網頁快取中。 然後，它從網頁快取傳送給使用者，以加快傳送速度。 因此，第一次有人下載網頁時，他們看到的資產會傳送到CDN快取。 這些快取內容會儲存在伺服器上，以便下次同一區域中的某人存取網頁時，可以更快速地傳送相同的快取內容。 因為位置更接近使用者，所以可更快地提供內容。 CDN可加快網頁顯示速度，但會降低中央伺服器的頻寬需求，因為內容是由快取網路傳送，而非每個執行個體的中央伺服器。 此最佳化的流程意味著更佳的使用者體驗，進而提高銷售額。

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

過去，CDN每月會提供3.5 PB的流量給客戶。 此系統在一天內可提供520億個資產。 該數字等於成功傳送給客戶的864,000張影像和視訊，_每秒_。

### 智慧型影像處理

Dynamic Media在最佳化資產以及確保每個資產可透過CDN在行動裝置和桌上型電腦系統上快速載入方面已經功不可沒。 為了達到此目的，Dynamic Media使用影像預設集來定義影像品質。 它們也會定義您要傳送的影像型別、其銳利度，以及您體驗或頁面不同部分的其他片段。

但若要在影像預設集之外進一步增加Dynamic Media的價值，則有&#x200B;_智慧型影像_。

智慧型影像可依據客戶的瀏覽器功能，自動最佳化影像的格式和檔案大小，以提供更優異的影像資產傳送效能。 它可搭配您現有的影像預設集運作（此歷程第二部分將討論影像預設集），並在傳送時使用情報。

此智慧功能可依據瀏覽器和網路連線速度，進一步縮小影像檔案大小。 由於影像資產佔頁面載入時間的大部分，因此效能提升會對關鍵業務指標產生徹底影響，例如：

* 較高的轉換
* 網站逗留時間
* 較低的網站跳出率

整體而言，使用智慧型影像處理，視您現有的影像預設集設定和特定使用者特性而定，效能可望提升22%至47%。 同時保持影像品質，如同從未接觸過一樣。

![智慧型影像](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_智慧型影像處理會根據客戶的瀏覽器功能和網路速度，自動最佳化影像的格式和檔案大小。_

智慧型影像處理預設不會開啟，因為您需要與Adobe Dynamic Media技術支援人員協調運作。 此外，啟用智慧型影像處理需要完全清除CDN快取，然後重新填入時間。 如果您有興趣使用智慧型影像，可以透過Adobe提交技術支援票證來開啟。 然後，技術支援會提供URL引數，讓您預先嘗試智慧型影像。 您可以在任何網頁或影像上試用，瞭解獲得的效能和節省的成本。 接著，您就可以為完整網站開啟智慧型影像處理。

### 最適化視訊集

當頁面上或首頁面上出現影片時，您的客戶往往會與該內容互動更久，並在頁面上停留更久，這通常是好事。 Adobe會透過分析展現此行為。 不過，影片可能很複雜。 首先，您通常有一個大型的主要檔案。 要決定視訊的大小和傳送方式相當複雜，這完全是為了確保體驗能順暢地執行，無論是在哪台裝置上觀看，也不論頻寬為何。

為了解決此問題，Dynamic Media可讓您建立&#x200B;_最適化視訊集_。

「自我調整視訊集」會將使用不同位元速率和格式編碼的相同視訊版本分組。

您會從上傳至系統的原始主要影片開始。Dynamic Media會自動調整視訊大小，或將&#x200B;_轉碼為_&#x200B;多個視訊。 然後，在傳遞時，其會智慧地判定使用何種影片畫面、何種畫質以及何種格式，將其傳遞至手機、平板電腦或桌上型電腦。

例如，在iOS行動裝置上，它會偵測4G、5G或Wi-Fi等頻寬。 之後，它會從「自我調整視訊集」中的各種視訊位元速率中，自動選取正確的編碼視訊。 影片會串流至行動裝置、平板電腦或桌上型電腦。

此外，視訊品質也會在網路狀況變更時自動切換。 此外，如果客戶在桌上型電腦上進入全熒幕模式，Adaptive Video Set會使用更好的解析度來回應，進而改善客戶的觀看體驗。

使用自我調整視訊集可為客戶在多重熒幕和裝置上播放Dynamic Media視訊提供流暢、高品質的播放。 真正能省去視訊的複雜性。

## Dynamic Media的使用案例 {#dm-journey-b}

以下是常見的用例問題和解決方案，Dynamic Media可以幫助您實現積極的客戶參與、忠誠度、轉化和提高ROI。

### 使用案例：主要檔案方法

Dynamic Media最重要的使用案例之一，也是最明顯的使用案例之一。 也就是說，無論是要傳送的影像或影片，都能減少頁面和體驗的重量及內容大小。

以下顯示典型的體驗或網頁。 一個頁面中約有90%是由豐富的媒體所組成，例如影像和視訊，這些通常是較重的檔案。

![內容頁面權數](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_典型網頁的內容頁面權數。_

其餘10%為HTML、CSS程式碼和特定標籤。 您想要最佳化該頁面90%的權重，Dynamic Media可協助您完成此工作。 您先前已閱讀&#x200B;_單一主要資產檔案的概念，其可能性無窮無盡_。 此方法對於減少整體頁面權重相當重要。 能夠取得一個主要資產，並在產品詳細資料頁面、縮圖頁面、購物車和搜尋格線上使用它，是絕佳的節省時間。 而且可確保體驗之間的一致性。

![主要檔案方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_手錶是一個主要資產檔案，但會即時建立多個轉譯（而非復本）。_

讓我們更詳細地瞭解Dynamic Media透過單一檔案解決的問題，以及這種方法的一些解決方案。

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 建立並儲存每個資產。 | 使用單一影像檔案，僅在傳送時自動建立所需的轉譯。 |
| 高儲存成本。 | 無須建立和儲存資產的多個復本。 |
| 難以維護保管鏈。 | 保證提供裝置最佳化且一致的體驗。 |
| 沒有版本記錄。 | |
| 跨裝置的不一致品牌體驗。 | |
| 建立重複資產的不必要成本。 | |

當您思考一個檔案時，您會為各種體驗建立一個資產。 您可能會有一個起始影像，然後您必須建立該影像的20、30或40種變體，最終必須儲存並支付儲存費用。

然後您必須確定已使用正確的影像，這可能會影響您維持品牌一致性的能力。 此外，如果您找不到影像，則必須返回並複製這些資產。

Dynamic Media可讓您從該起始影像即時建立影像的變體。 它可讓您使用該主要資產發揮創意，而不需與平面設計藝術家或攝影工作室來回奔波，即可建立其他內容。 這樣就能節省金錢和時間。

使用單一檔案方法時，會使用單一主要檔案。 然後，只有在客戶交付或看到網站、屬性和體驗時，才建立所需的這些版本或轉譯。 如此的效率可大幅減少資產所需的儲存容量，並降低整體工作流程的複雜性。 藉由Dynamic Media的傳送系統，可確保每個影像和視訊都經過最佳化、快速載入，並在所有熒幕和裝置上看起來都不錯。

### 使用案例：影片

Dynamic Media為解決的另一個使用案例是視訊。 視訊很複雜。 很難管理。 視訊檔案因其本身的檔案大小而難以儲存和移動。

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 難以管理和傳送針對各種裝置最佳化的視訊。 | 使用單一視訊來自動調整所有裝置的大小。 |
| 由於使用者可用的頻寬，影片會以低品質停止播放或播放。 | 透過HTML播放器傳送視訊，自動偵測可用頻寬並調整品質，以確保高傳真度且順暢播放。 |
| 手動建立所有視訊版本既不可行又耗時，只是為了確保裝置間能良好顯示和播放。 | 透過簡化的工作流程，省去數小時繁瑣的轉碼工作。 |
| | 騰出時間處理更高價值的工作。 |

來到Dynamic Media的客戶有以下他們想要解決的問題：

「_我的企業擁有視訊，部門花費了大量資金製作它，但避免將它放在網頁上或送達。 原因是因為從測試來看，視訊品質無法得到保證，即便真的要播放。 最終，這會影響企業的品牌，以及其轉換角色。_」

Dynamic Media的解決方案是取用那個主要視訊檔案，讓Dynamic Media透過轉碼程式完成所有大小。 接著，請將其與Dynamic Media的智慧型視訊播放器配對。 此工作流程可保證您在主要登陸頁面、類別或產品詳細資料頁面上使用該影片，其全程將保持一致，並提供高品質。

以下是其他幾個需考慮的使用案例。

### 使用案例：單一信任來源

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 分散在組織中、分散在不同的團隊或業務單位的數位資產。 | 在一個中央位置儲存和管理所有數位資產。 |
| 團隊成員下載並建立本機版本。 | 團隊成員使用單一主要檔案來建立&#x200B;_和_，並提供各種熒幕大小和裝置的所有必要版本。 |
| 為每個體驗和裝置建立的一次性資產。 | 消除一次性使用的資產，以節省時間和金錢建立它們。 |

### 使用案例：適用於多媒體的AI支援智慧型裁切

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 手動繪製、測量及剪下影像或視訊，以強調焦點並在所有熒幕大小和裝置上適當地顯示，既費時又費力。 | 使用Adobe AI功能Dynamic Media中的智慧型裁切功能，自動偵測任何影像或視訊中的焦點，並裁切以維持焦點。 |
| 可以更妥善地用於建立具高度影響力的體驗的時間損失。 | 擷取預期的興趣點，無論熒幕大小為何。 |
| 為每個體驗和裝置建立的一次性資產。 | 省去繁瑣的手動工作，並提供高品質、快速載入的影像和視訊，在任何裝置或熒幕上都能完美呈現。 |

### 使用案例：互動媒體製作

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 無法參與、無法帶來忠誠度或促進轉換的固定和靜態客戶體驗。 | 可讓非技術使用者輕鬆且順暢地新增互動元素，例如熱點、輪播和迴轉集，以獲得更動態且吸引人的體驗。 |
| 數位資產的投資回報有限，而客戶體驗乏善可陳。 | 推動多媒體體驗的轉換和投資報酬率。 |

## 資產如何流經Dynamic Media系統 {#dm-journey-c}

以下顯示Dynamic Media的典型工作流程。

![Dynamic Media工作流程](/help/assets/dynamic-media/assets/dm-workflow.png)
_資產如何流經Dynamic Media系統。_

從建立階段開始，主要目標是要將主要資產放在結尾。 這些主要資產可能來自像片拍攝、視訊廠商，或可能是您已建立的部分音訊檔案。 您可以使用Adobe的Creative Suite應用程式(例如Adobe InDesign、Adobe Photoshop、Adobe Illustrator)來協助您編寫內容。

建立部分完成後，您需透過將資產上傳至Dynamic Media，將資產放入Authoring解決方案。 在Dynamic Media中，請確定您的網站針對各種網頁已設定適當的影像預設集和檢視器。

最後，您會最佳化所有內容，並將其發佈至Dynamic Media伺服器，以便用於網路、列印、電子郵件、桌上型電腦和行動裝置。

### 將資產上傳至Dynamic Media

完成建立主要資產後，可將其上傳至Dynamic Media。 上傳的檔案型別、檔案的格式與大小是Dynamic Media的重要屬性。 您想在上傳時確定從單一檔案支援中獲得最大值。

例如，下面的手錶影像是4560 x 3020畫素。 雖然您絕不能使用這個大小的影像，但您仍可以上傳它。 影像越大，Dynamic Media所能提供的品質就越好，甚至可低至縮圖轉譯。 請記住：您可以輕鬆&#x200B;_降低_&#x200B;現有影像的解析度。 但如果您嘗試&#x200B;_增加_&#x200B;影像的解析度，結果可能會不令人滿意。

![建議上傳至Dynamic Media的格式](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_資產上傳的考量事項。_

Adobe建議您以無損格式上傳資產。 一般來說，最好避免JPEG，因為當您傳送JPEG或繼續儲存JPEG時，會隨著時間逐漸失去影像品質。 您想要以無損格式從最高解析度的影像開始，讓您隨時都能存取。 該格式通常是TIFF或PNG檔案。

關於色域，當您考慮數位頻道或Web檢視時，您通常會考慮RGB （紅色、綠色、藍色）。

大部分使用者都不會考慮以CMYK傳送任何專案，或是您為何可能想要以CMYK傳送。 原因是色彩空間最常用於傳送列印專案。 但是，Dynamic Media可以在兩個色域中傳送。

還有許多客戶仍會列印紙張，例如倉儲批發俱樂部。 此外還有雜貨店，他們通常每週列印傳單。 這類客戶要求將影像同時置於兩個色域中。 傳統上，這需要兩個不同的影像：一個在RGB中，另一個在CMYK中。 不過，您可以直接將CMYK資產上傳至Dynamic Media，讓Dynamic Media透過影像預設集或色彩設定檔自動傳遞RGB資產。 不需要建立多個版本的檔案，因此維護了&#x200B;_一個主要資產檔案的概念，並提供了無限可能性_。

<!-- **The Value of Renditioning??? or Demo portion** -->

### 發佈和預覽資產

將資產上傳到Dynamic Media之後，請選取資產，然後按一下Dynamic Media中的&#x200B;_發佈_&#x200B;或&#x200B;**[!UICONTROL 快速發佈]**，以便&#x200B;**[!UICONTROL 發佈]**&#x200B;資產，這是不錯的作法。 如果您想要在任何體驗中使用資產，則必須發佈資產。 發佈資產後，您可使用複製的動態媒體產生URL或透過將程式碼內嵌在頁面上，將資產納入網頁中。

除了手動發佈資產外，您可以設定Dynamic Media，以便在上傳時立即發佈資產（無需任何使用者介入）。

上傳後，有不同的方式可在Dynamic Media中預覽資產的轉譯。 預覽轉譯可協助您瞭解客戶所看到的內容。 常見的預覽方法是選取資產，然後選取&#x200B;_影像預設集_，檢視其轉譯，如下所示。

![根據大型影像預設集預覽資產的轉譯](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_根據選取的「大」影像預設集預覽資產的轉譯。 已按一下URL按鈕。 產生的URL路徑包含「大」影像預設集名稱，且可用於網頁。_

上述URL為即時網址！ [試用](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$){target="_blank"}。

另一種預覽資產的方法是選取影像資產，然後選取&#x200B;_檢視器_&#x200B;預設集，如下所示。

![根據Zoom Vertical Light檢視器預設集預覽資產](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_根據選取的「ZoomVertical_light」檢視器預設集預覽資產。 滑鼠指標(`+`)移到手錶上以放大。 請注意URL和內嵌按鈕。_

以上轉譯為即時轉譯！ [試用](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&config=jpearldemo/ZoomVertical_light){target="_blank"}。

## 選擇性 — 瞭解更多

此歷程的第一部分涵蓋各種Dynamic Media主題的基本知識。 如果您想深入瞭解您所閱讀的內容，請使用下列資料更詳細地探索概念。 否則，您可以繼續歷程的第二部分。 檢視[此Dynamic Media歷程的下一步是什麼](#whats-next)。

<!--
_Dynamic Media Help topics_

* [Work with Dynamic Media in Experience Manager](/help/assets/dynamic-media/dynamic-media.md)
* [About Smart Imaging](/help/assets/dynamic-media/imaging-faq.md)
* [How to create Adaptive Video Sets](/help/assets/dynamic-media/video.md)
* [Best practices for optimizing the quality of your images](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [How to upload assets](/help/assets/add-assets.md#upload-assets)
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to deliver Dynamic Media Assets](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [How to publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [Work with Selective Publish in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md) -->

_動態媒體教學課程_

* [搭配Experience Manager Assets使用Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager內容庫](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) （在&#x200B;_Dynamic Media_&#x200B;上搜尋）

_Dynamic Media檢視器_

* 每個檢視者的[即時示範](https://landing.adobe.com/tw/na/dynamic-media/ctir-2755/live-demos.html)

## 此Dynamic Media歷程的下一步發展 {#whats-next}

在此歷程的第二部分，您會詳細檢查Dynamic Media URL，以更清楚瞭解傳送資產時發生的情況。 您也會進一步瞭解建立影像預設集以轉譯資產背後的基礎知識，並瞭解影像集、迴轉集和混合媒體集及其建立方式。

帶我前往[Dynamic Media歷程：基本知識，第二部分](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d)。

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->