---
title: Dynamic Media旅程，第一部分
description: Dynamic Media歷程涵蓋Dynamic Media的基本概念、運作方式、可為您做什麼，以及為您的工作和客戶帶來哪些價值。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: 1200dc41af22ae8f34f33d176de1c0db7c7ae424
workflow-type: tm+mt
source-wordcount: '3712'
ht-degree: 0%

---

# Dynamic Media歷程：基本知識，第一部分 {#dm-journey-part1}

歡迎使用Dynamic Media歷程。

此歷程涵蓋Dynamic Media的基本概念、運作方式、可為您提供的功能，以及為您的工作和客戶帶來的價值。

**_必備條件_**

* 基本了解影像和視訊格式
* HTML和CSS的基本了解
* 基本了解設計工具，例如Adobe Illustrator、Adobe Photoshop、Adobe XD
* 在Experience Manager上存取Dynamic Media雖然有用，但並非必要

**_您能學到的_**

_第一部分_

* 什麼是Dynamic Media，它能為您帶來什麼幫助？
* Dynamic Media的使用案例
* 資產如何透過Dynamic Media系統

_第二部分_

* Dynamic Media URL及Dynamic Media如何傳遞內容的解剖
* 建立影像預設集以轉譯資產的基本知識
* 影像集、回轉集和混合媒體集

**_對象_**
最符合此歷程讀者的對象為剛接觸Dynamic MediaExperience Manager的以下人士：

* 管理員
* 業務分析人員
* 內容架構師
* 內容作者
* Designer
* 開發人員
* 行銷
* 產品經理/擁有者

>[!TIP]
>
>為獲得最佳結果，Adobe建議您在桌上型電腦上閱讀並檢視此Dynamic Media歷程。

## 什麼是Dynamic Media，它能為您帶來什麼幫助？ {#dm-journey-a}

Dynamic Media可協助您隨需提供豐富的視覺化銷售和行銷資產。 此外，它還可協助您建立和提供互動式檢視體驗，包括縮放、360度旋轉和視訊。 您的資產會動態調整規模，以供網站、行動裝置及社交網站使用。 使用一組主要來源資產（例如影像、視訊和3D）,Dynamic Media可透過其全域可擴充、效能最佳化的CDN（內容傳遞網路），即時產生並傳遞此豐富內容的多種變異。

Dynamic Media整合了Adobe Experience Manager Assets數位資產管理解決方案的工作流程，以簡化和簡化數位行銷活動管理流程。

### 一個檔案，有無限的可能

關於Dynamic Media的一個要點是 _一個主要資產檔案，提供無限可能_.

為了更清楚了解此概念，請思考您傳統上處理單一資產（例如影像或影片）的方式。 您通常會建立一個主要資產。 接著，您會針對每個體驗、所需的每個裝置、每個網頁以及使用該資產的每個屬性，手動建立相同資產的版本。 隨著時間推移，單一資產可增長至20、30或更新版本，且不附加任何版本記錄。 現在，想像一下，對你擁有的每一張影像或視頻都這樣做。 要維護和更新資產版本的數量將很快變得非常龐大，更不用說儲存成本的增加了。

然而，Dynamic Media與其他系統有根本不同，因為您使用它來傳送媒體 _動態_ 從單一、主要資產和從URL呼叫。 您要求的Dynamic Media URL路徑包含指示，告訴Adobe發佈伺服器在資產傳遞至客戶畫面時如何顯示資產。 例如，使用相同的單一主要資產，您可以立即以無限制的轉譯、變更大小、格式、解析度、重量、顏色、裁切和效果（例如縮放檢視）傳送資產。

此獨特的傳送方法可確保將一致的品質體驗傳送至任何畫面，不論其大小或頻寬為何。 還針對所有螢幕類型對全尺寸視頻進行優化，並自適應地流式傳輸，以確保一致、優質的用戶體驗。

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![AdobeDynamic Media以不同大小和格式將相同的主影像傳送給不同的媒體。](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_AdobeDynamic Media可確保將一致的品質體驗提供至任何畫面，無論其大小或頻寬為何。_

隨著您閱讀，您將進一步了解「單一主要資產檔案，無限可能性」的概念為何如此重要。

### 內容傳遞網路

當您準備好使用影像資產或視訊資產上線時，Dynamic Media的骨幹網路即可支援此資產，其中包含強大的頂層傳送網路。 該網路每天為全球數百個客戶端提供服務。 資產會在由Akamai托管的內容傳送網路（或CDN）上分發。 CDN是電腦服務的系統，會以透明方式合作，將內容（尤其是大型多媒體內容）傳送給使用者。

在CDN系統中，Web內容儲存在網際網路上的Web快取中。 然後會從Web快取傳送給使用者，以加快傳送速度。 因此，當使用者第一次下載網頁時，會將他們看到的資產傳送至CDN快取。 它們儲存在伺服器上，以便在同一區域的下一次訪問網頁時，能夠更快地提供相同的快取內容。 內容的傳送速度較快，因為其位置更接近使用者。 CDN可讓網頁顯示更快，但卻可降低中央伺服器的頻寬需求，因為內容是透過快取網路傳送，而非透過每個執行個體的中央伺服器傳送。 此最佳化的流程意味著更佳的使用者體驗，進而提高銷售。

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

過去，CDN每月會為客戶提供3.5 PB的流量。 該系統一天可交付520億個資產。 這個數字相當於成功地向客戶交付了864,000個影像和視頻， _每秒_.

### 智慧型影像

Dynamic Media已透過CDN，在最佳化資產及確保每個資產在行動與案頭系統上快速載入方面，做得非常出色。 為了達成此目的，Dynamic Media中會使用影像預設集來定義影像品質。 它們也會定義您要傳送的影像類型、其清晰度，以及體驗或頁面不同部分的其他片段。

但除了影像預設集以外，若要進一步為Dynamic Media新增值， _智慧型影像_.

智慧影像處理根據客戶的瀏覽器功能自動最佳化影像的格式和檔案大小，提供更出色的影像資產傳送效能。 它可與您現有的影像預設集搭配使用（本歷程第II部分會討論影像預設集），並在傳送時使用智慧。

這種智慧會進一步根據瀏覽器和網路連線速度來縮小影像檔案大小。 由於影像資產佔頁面載入時間的大部分，因此效能改善可能會對關鍵業務指標產生徹底影響，例如：

* 較高轉換
* 網站逗留時間
* 網站跳出率較低

整體而言，透過智慧型影像處理，您可以預期效能會提升22%至47%，具體取決於您現有的影像預設集設定和特定的一般使用者特徵。 同時保持影像質量，好像從未接觸過。

![智慧型影像](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_智慧影像處理會根據客戶的瀏覽器功能和網路速度，自動最佳化影像的格式和檔案大小。_

智慧型影像處理預設不會開啟，因為您需要與AdobeDynamic Media技術支援人員進行協調努力。 此外，若要啟用智慧型影像處理，必須完全清除CDN快取，然後會重新填入時間。 如果您有興趣使用智慧影像處理，可以通過提交技術支援票證來與Adobe協作以啟用它。 技術支援接著會提供URL參數，讓您事先試用智慧型影像處理。 您可以在任何網頁或影像上試用它，以便查看您獲得的效能和節省的成本。 然後，您就可以為整個網站開啟智慧型影像處理。

### 最適化視訊集

當頁面或主要頁面上有影片時，您的客戶與該內容的互動時間會更長，而在頁面上停留的時間會更長，這通常是件好事。 此行為已透過Adobe的分析展現。 不過，視訊可能很複雜。 首先，您通常有大型主檔案。 要判斷視訊的大小和傳送方式很複雜，所有這一切都能確保體驗順暢運作，無論其正在觀看的裝置為何，無論頻寬為何。

為解決此問題，Dynamic Media可讓您建立 _最適化視訊集_.

![最適化視訊集](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_適用性視訊集會將以不同位元速率和格式編碼的相同視訊版本分組。_

從您上傳至系統的原始主要視訊開始。 Dynamic Media會自動調整大小，或 _轉碼_，將該影片放入多個影片中。 然後，在傳送時，它會智慧地決定要使用的視訊螢幕、品質和格式，並將其傳送至手機、平板電腦或桌上型電腦。

例如，在iOS行動裝置上，會偵測頻寬，例如4G、5G或Wi-Fi。 然後，它自動從自適應視訊集內的各種視訊位速率中選取正確編碼的視訊。 視訊會串流至行動裝置、平板電腦或桌上型電腦。

此外，如果網路條件改變，視頻質量被動態地切換。 此外，如果客戶在桌上型電腦上進入全螢幕模式，最適化視訊集會使用更佳的解析度來回應，改善客戶的觀看體驗。

使用適用性視訊集，可讓客戶在多個畫面和裝置上播放Dynamic Media視訊，以順暢、高品質的播放方式。 它真的把複雜度從視頻中剔除了。

## Dynamic Media的使用案例 {#dm-journey-b}

以下是常見的使用案例問題和解決方案，Dynamic Media可協助您提升客戶參與度、忠誠度、轉換率，以及提高投資報酬率。

### 使用案例：主要檔案方法

Dynamic Media最重要的使用案例之一也是最明顯的使用案例。 也就是說，可減輕頁面和體驗的重量，以及所傳送內容的大小，無論內容是影像或影片。

以下顯示典型體驗或網頁。 約90%的頁面是由多媒體組成，例如影像和視訊，這些檔案通常比較重。

![內容頁面權數](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_典型網頁的內容頁面權重。_

其餘10%為HTML、CSS程式碼和特定標籤。 您想要將該頁面的90%重量最佳化，Dynamic Media可協助您處理。 之前，您讀到 _一個主資產檔案，無盡的可能_. 此方法在降低整體頁面重量方面相當重要。 您可以取用一個主要資產，並將其用於產品詳細資料頁面、縮圖頁面、購物車和搜尋格線，這是絕佳的時機。 此外，還可確保體驗之間的一致性。

![主要檔案方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_手錶是一個主要資產檔案，但會即時建立並多次轉譯（而非復本）。_

讓我們更仔細地了解Dynamic Media使用單一檔案解決的問題，以及該方法的一些解決方案。

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 建立並儲存每個資產。 | 使用單一影像檔案，只有在傳送時才自動建立必要的轉譯。 |
| 儲存成本高。 | 無需建立和儲存資產的多個復本。 |
| 難以維持保管鏈。 | 保證提供裝置最佳化且一致的體驗。 |
| 沒有版本歷史記錄。 |  |
| 各裝置的品牌體驗不一致。 |  |
| 重複資產建立的不必要成本。 |  |

當您思考一個檔案時，會針對各種體驗建立資產。 您可能有一個起始影像，然後您必須建立該影像的20、30或40個變體，您最終必須儲存並支付該儲存空間的費用。

然後，您必須確定已使用正確的影像，而這可能會影響您在不同品牌間保持一致的能力。 此外，如果您找不到影像，則必須返回並複製這些資產。

Dynamic Media可讓您從該起始影像即時建立影像的變體。 它可讓您使用該主要資產發揮創意，而無須與您的平面設計藝術家或像片工作室來回往返，以建立其他內容。 這是省錢省時的。

使用單一檔案方法時，可使用單一主檔案。 然後建立您的網站、屬性和體驗所需的版本或轉譯，且必須等到客戶傳送或檢視這些版本或轉譯的時間。 這樣的效率可以大大降低資產所需的儲存量，並降低整體工作流的複雜性。 透過Dynamic Media的傳送系統，可確保每個影像和視訊都經過最佳化、快速載入，且在所有螢幕和裝置上皆呈現絕佳外觀。

### 使用案例：影片

Dynamic Media解決的另一個使用案例是視訊。 視訊很複雜。 很難管理。 視訊檔案的固有檔案大小，使其難以儲存和移動。

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 難以管理和提供針對各種裝置最佳化的視訊。 | 使用可自動調整所有裝置大小的單一視訊。 |
| 由於一般使用者的可用頻寬，影片會停止播放或以低品質播放。 | 透過HTML播放器傳送視訊，可自動偵測可用頻寬並調整品質，以確保高保真度和順暢播放。 |
| 手動建立所有版本的視訊是不可行的且耗時，僅為了確保在裝置間良好的顯示和播放。 | 透過簡化的工作流程，消除繁瑣的轉碼工作時間。 |
|  | 騰出時間用於更高價值的工作。 |

客戶來到Dynamic Media時，有下列問題想要解決：

&quot;_我們有視頻，我們花了很多錢製作。 但我們迴避把它放在網頁上，或者把它遞出來，因為從我們的測試中，我們真的無法保證視頻的質量，或者它真的要播放。 最終，這會影響我們的品牌，甚至可能影響我們在轉換方面的角色。_&quot;

Dynamic Media的解決方案是取用該一個主要視訊檔案，並讓Dynamic Media透過轉碼程式處理所有大小。 然後，將其與Dynamic Media的智慧視訊播放器配對。 此工作流程可保證無論您是在主要登陸頁面上，還是在類別或產品詳細資料頁面上使用該影片，都能在整個過程中保持一致，並以高品質提供。

以下是幾個需要考慮的使用案例。

### 使用案例：單一真相來源

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 分散在不同團隊或業務單位的數位資產。 | 在集中位置儲存及管理所有數位資產。 |
| 團隊成員下載並建立本機版本。 | 團隊成員使用單個主檔案來建立 _和_ 在不同的螢幕大小和裝置上提供所有必要的版本。 |
| 為每個體驗和裝置建立的單一使用資產。 | 消除了單一使用的資產，節省了建立這些資產的時間和資金。 |

### 使用案例：適用於多媒體的AI支援智慧型裁切

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 手動繪製、測量和剪切影像或視頻，以突出顯示焦點並適當顯示所有螢幕大小和設備，耗時且耗費大量人力。 | 使用Adobe Sensei AI功能Dynamic Media中的智慧型裁切功能，自動偵測任何影像或視訊中的焦點，並裁切以加以維護。 |
| 時間損失，可以更有效地用於建立高影響力體驗。 | 擷取預期的地標，而不論螢幕大小。 |
| 為每個體驗和裝置建立的單一使用資產。 | 消除了繁瑣的手動任務，並提供在任何設備或螢幕上看起來都不錯的高質量、快速載入的影像和視頻。 |

### 使用案例：互動式媒體製作

| **問題** | **Dynamic Media解決方案** |
|---|---|
| 不會參與、產生忠誠度或促進轉換的固定和靜態客戶體驗。 | 讓非技術使用者輕鬆順暢地新增互動式元素，例如熱點、輪播和回轉集，以提供更動態且吸引人的體驗。 |
| 數位資產投資回報有限，客戶體驗平淡。 | 從多媒體體驗推動轉換和投資報酬率。 |

## 資產如何透過Dynamic Media系統 {#dm-journey-c}

以下顯示Dynamic Media的典型工作流程。

![Dynamic Media工作流程](/help/assets/dynamic-media/assets/dm-workflow.png)
_資產如何透過Dynamic Media系統。_

您從建立階段開始，主要目標是將主要資產放在最後。 這些主要資產可能來自照片、視訊廠商，或是您建立的一些音訊檔案。 您可以使用Adobe的Creative Suite應用程式(例如Adobe InDesign、Adobe Photoshop、Adobe Illustrator)來協助您處理內容。

建立部分完成後，您會將資產上傳至Dynamic Media，將資產放入製作解決方案。 在Dynamic Media中，請確定您的網站上有正確的影像預設集和檢視器，以供您的各種網頁使用。

最終，您可以最佳化所有內容，並將其發佈至Dynamic Media伺服器，以便供網頁、列印、電子郵件、桌上型電腦和行動裝置使用。

### 將資產上傳至Dynamic Media

完成主要資產的建立後，即可將其上傳至Dynamic Media。 上傳的檔案類型、檔案的格式和大小是Dynamic Media的重要屬性。 上傳時，您需要確保從單一檔案支援中獲得最大價值。

例如，下方的監看影像為4560 x 3020像素。 雖然您可能永遠不會使用如此大的影像，但您仍可以上傳它。 影像愈大，Dynamic Media可傳送的品質就愈高，甚至縮圖轉譯也愈好。 記住：您可以輕鬆 _減少_ 現有影像的解析度。 但如果你想 _增加_ 影像的解析度，結果可能不令人滿意。

![上傳至Dynamic Media的建議格式](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_上傳資產的考量事項。_

Adobe建議您以無損格式上傳資產。 一般來說，最好避免JPEG，因為當您傳送JPEG或繼續儲存JPEG時，影像品質會隨著時間而開始下降。 您希望從最高解析度的影像開始，以無損格式顯示，您可以使用。 該格式通常為TIFF或PNG檔案。

關於色域，當您思考數位頻道或Web檢視時，通常會考慮RGB（紅色、綠色、藍色）。

大多數人永遠不會想到以CMYK傳送某些內容，或您甚至可能想以CMYK傳送的原因。 原因是色域最常用於傳送印刷品。 但是，Dynamic Media可以在兩種顏色空間中傳遞。

還有很多顧客仍在印刷品，例如倉庫批發俱樂部。 還有一些雜貨店經常每週打印傳單。 這類客戶要求其影像同時位於兩色空間。 傳統上，這需要兩種不同的影像：一個RGB，一個CMYK。 不過，您可以直接將CMYK資產上傳至Dynamic Media，並讓Dynamic Media自動透過影像預設集或顏色設定檔傳送RGB資產。 不需要建立檔案的多個版本，因此維護 _一個主資產檔案，無盡的可能_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### 發佈和預覽資產

將資產上傳至Dynamic Media後，最好使用 _發佈_ 選取資產，然後按一下 **[!UICONTROL 發佈]** 或 **[!UICONTROL 快速發佈]** 在Dynamic Media。 如果您想要在任何體驗中使用資產，則必須發佈資產。 發佈資產後，您就可以使用您複製的Dynamic Media產生URL，或透過在頁面上內嵌程式碼，將資產加入網頁中。

除了手動發佈資產，您還可以設定Dynamic Media，以便在上傳時立即發佈資產（不需任何使用者干預）。

上傳後，您可以透過不同方式在Dynamic Media中預覽資產的轉譯。 預覽轉譯可協助您了解客戶會看見的內容。 常見的預覽方法是選取資產，然後選取 _影像預設集_ 如下所示。

![根據大型影像預設集預覽資產的轉譯](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_根據選取的「大型」影像預設集預覽資產的轉譯。 已按一下URL按鈕。 產生的URL路徑包含「大型」影像預設集名稱，可用於網頁。_

上述URL為即時！ [試試看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$){target=&quot;_blank&quot;}。

預覽資產的另一種方法是選取影像資產，然後選取 _檢視器_ 預設集，如下所示。

![根據「縮放垂直光源」檢視器預設集預覽資產](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_根據選取的「ZoomVertical_light」檢視器預設集預覽資產。 滑鼠指針(`+`)移過手錶以放大。 請注意URL和內嵌按鈕。_

上述轉譯為即時！ [試試看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light){target=&quot;_blank&quot;}。

## 選用 — 深入了解

本歷程的第一部分說明各種Dynamic Media主題的基本概念。 如果您想要進一步了解剛才閱讀的內容，請使用下列材料，更詳細地探索概念。 否則，您可以繼續進行您的旅程的第二部分。 請參閱 [這個Dynamic Media旅程的接下來是什麼](#whats-next).

_Dynamic Media說明主題_

* [與Dynamic Media合作Experience Manager](/help/assets/dynamic-media/dynamic-media.md)
* [關於智慧型影像](/help/assets/dynamic-media/imaging-faq.md)
* [如何建立最適化視訊集](/help/assets/dynamic-media/video.md)
* [影像品質最佳化的最佳作法](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [如何上傳資產](/help/assets/add-assets.md#upload-assets)
* [如何預覽資產](/help/assets/dynamic-media/previewing-assets.md)
* [如何預覽3D資產](/help/assets/dynamic-media/previewing-3d-assets.md)
* [如何傳送Dynamic Media Assets](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [如何發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [在 Dynamic Media 中使用選擇性發佈](/help/assets/dynamic-media/selective-publishing.md)

_Dynamic Media教學課程_

* [將Dynamic Media與Experience Manager Assets搭配使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager內容庫](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (搜尋 _Dynamic Media_)

_Dynamic Media檢視器_

* [即時演示](https://landing.adobe.com/tw/na/dynamic-media/ctir-2755/live-demos.html) 每個檢視者

## 這個Dynamic Media旅程的接下來是什麼 {#whats-next}

在此歷程的第II部分，您將會稍微了解Dynamic Media URL，以便更清楚了解資產傳送時的狀況。 您也將進一步了解建立影像預設集來轉譯資產背後的基本原理，並了解影像集、回轉集和混合媒體集及其建立方式。

帶我去 [Dynamic Media歷程：基本知識，第二部分](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->