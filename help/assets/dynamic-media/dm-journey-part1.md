---
title: Dynamic Media之旅，第一部分
description: 《Dynamic Media之旅》介紹了Dynamic Media的基本知識、工作原理、能為您做什麼，以及它給您的工作和客戶帶來什麼價值。
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
source-git-commit: e16d107dff1817e8b62de86e295590b13d853bf0
workflow-type: tm+mt
source-wordcount: '3708'
ht-degree: 0%

---

# Dynamic Media之旅：《基礎》，第一部分 {#dm-journey-part1}

歡迎來到Dynamic Media之旅。

這段旅程涵蓋了Dynamic Media的基本知識、工作原理、它能為您帶來什麼，以及它給您的工作和客戶帶來什麼價值。

**_必備條件_**

* 對影像和視頻格式的基本理解
* 對HTML和CSS的基本理解
* 對Adobe Illustrator、Adobe Photoshop、Adobe XD等設計工具的基本理解
* 訪問Dynamic MediaExperience Manager很有幫助，但不是必需的

**_你可以期望學到的_**

_第一部分_

* 什麼是Dynamic Media，它能幫你什麼？
* 用於Dynamic Media
* 資產如何通過Dynamic Media系統

_第二部分_

* Dynamic MediaURL的剖析及Dynamic Media如何提供內容
* 建立影像預設以呈現資產的基礎
* 映像集、旋轉集和混合媒體集

**_觀眾_**
最適合這段旅程讀者的觀眾是那些剛到Dynamic MediaExperience Manager的讀者：

* 管理員
* 業務分析師
* 內容架構師
* 內容作者
* Designer
* 開發人員
* 營銷
* 產品經理/所有者

>[!TIP]
>
>為獲得最佳效果，Adobe建議您在台式電腦上閱讀和查看此Dynamic Media之旅。

## 什麼是Dynamic Media，它能幫你什麼？ {#dm-journey-a}

Dynamic Media幫助您按需提供豐富的視覺商品銷售和營銷資產。 它還幫助您建立和提供互動式觀看體驗，包括縮放、360度旋轉和視頻。 您的資產將動態擴展，以用於Web、移動和社交網站上的消費。 使用一組主要源資產（如影像、視頻和3D）,Dynamic Media通過其全球、可擴展、效能優化的CDN（內容交付網路）即時生成並提供此豐富內容的多種變體。

Dynamic Media公司採用Adobe Experience Manager資產數字資產管理解決方案的工作流程，以簡化和簡化數字市場活動管理流程。

### 一個檔案，無盡的可能

關於Dynamic Media的一個要點是 _一個具有無限可能性的主資產檔案_。

要更好地理解這一概念，請考慮您傳統上使用單一資產的方式。 通常建立一個主要資產。 然後，您可以為每個體驗、每個需要的設備、每個網頁以及使用它的每個屬性手動建立相同資產的版本。 隨著時間的推移，該單個資產可以增長到20、30或更多版本，但沒有附加版本歷史記錄。 現在，想像一下，對於你擁有的每幅影像或視頻，都要這樣做。 在維護和更新方面，資產版本的數量將很快變得巨大，更不用說儲存成本的增加了。

但是，Dynamic Media與其他系統有根本不同，因為您使用它來傳遞媒體 _動態_ 從單個、主要資產和URL調用。 您請求的Dynamic MediaURL路徑包含說明，說明在將資產交付到客戶螢幕時，如何顯示Adobe發佈伺服器。 例如，使用同一個主要資產，您可以立即以無限制的格式副本形式提供，更改大小、格式、解析度、重量、顏色、裁剪以及縮放視圖等效果。

這種獨特的傳送方法確保將一致的質量體驗發送到任何螢幕，而不管其大小或頻寬如何。 還針對所有螢幕類型對全尺寸視頻進行優化，並自適應地流式傳輸，以確保用戶體驗一致、高質量。

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![AdobeDynamic Media以不同大小和格式向不同介質提供相同的主映像。](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_AdobeDynamic Media確保向任何螢幕提供一致、高質量的體驗，而不管其大小和頻寬如何。_

在您閱讀時，您將瞭解為什麼「一個主要資產檔案，無限可能性」這一概念非常重要。

### 內容傳遞網路

當您準備好與影像資產或視頻資產一起直播時，Dynamic Media的骨幹網將支援它，該骨幹網由功能強大的頂層交付網路組成。 該網路每天為全球數百個客戶服務。 這些資產在由Akamai托管的內容交付網路（或CDN）上分發。 CDN是一個聯網的電腦服務系統，它透明地合作將內容，特別是大型富媒體內容遞送給最終用戶。

在CDN系統中，Web內容儲存在Internet上的Web快取中。 然後，它從Web快取被遞送到最終用戶，以便更快地遞送。 因此，當第一次有人下載網頁時，他們看到的資產會被傳送到CDN快取。 它們儲存在伺服器上，以便下次同一區域內的某人訪問網頁時，可以更快地傳遞相同的快取內容。 內容更快地傳遞，因為它位於離最終用戶更近的位置。 CDN使網頁顯示更快，但它減少了中央伺服器上的頻寬需求，因為內容是從快取網路而不是從每個實例的中央伺服器傳送的。 這種優化的流程意味著更好的用戶體驗，從而增加銷售。

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

過去，CDN每月向客戶提供3.5 PB的流量。 該系統一天可提供520億資產。 這一數字相當於864,000張影像和視頻成功地交付給客戶， _每秒_。

### 智慧型影像

Dynamic Media已經通過CDN在優化資產和確保移動和案頭系統上快速載入每個資產方面做了大量工作。 要實現這一點，在Dynamic Media使用影像預設來定義影像的質量。 它們還定義要發送的影像類型、影像的清晰度以及您經歷或頁面的不同部分的其他片段。

但是，要進一步增加Dynamic Media在影像預設之外的價值， _智慧映像_。

智慧映像通過根據客戶的瀏覽器功能自動優化映像的格式和檔案大小，提供更好的映像資產交付效能。 它可與您現有的影像預設配合使用（本旅程的第二部分將討論影像預設），並在交付時使用智慧。

這種智慧進一步減少了基於瀏覽器和網路連接速度的影像檔案大小。 因為影像資產佔頁面載入時間的大部分，所以效能改進會對關鍵業務指標產生徹底的影響，例如：

* 更高轉換
* 在站點上花費的時間
* 低站點彈跳率

總體而言，通過智慧映像，您可以期望根據現有映像預設設定和特定最終用戶特性，將效能提高22%到47%。 同時保持影像質量好像從未被觸及。

![智慧映像](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_Smart Imaging根據客戶的瀏覽器功能和網路速度自動優化映像的格式和檔案大小。_

預設情況下，智慧映像未開啟，因為它需要您與AdobeDynamic Media技術支援人員進行協調。 此外，啟用智慧映像需要完全清除CDN快取，然後重新填充時間。 如果您對使用智慧映像感興趣，可以通過提交技術支援票證與Adobe協作以啟用它。 然後，技術支援會為您提供一個URL參數，讓您提前嘗試智慧成像。 你可以在任何網頁或圖片上嘗試，這樣你就能看到你獲得的效能和節約。 然後，您可以為整個站點啟用智慧映像。

### 自適應視頻集

當頁面或首頁上有視頻時，您的客戶往往會更長時間地接觸該內容，並在頁面上停留更長時間，這通常是件好事。 這種行為已通過Adobe所做的分析展示出來。 然而，視頻可能很複雜。 首先，您通常有一個較大的主檔案。 確定如何調整大小和傳輸視頻是一件複雜的事情，所有這一切都是為了確保無論觀看哪台設備，無論頻寬如何，體驗都能順利運行。

為瞭解決這個問題，Dynamic Media讓你能夠 _自適應視頻集_。

![自適應視頻集](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_自適應視頻集將以不同比特率和格式編碼的同一視頻的版本分組。_

您首先將原始的主視頻上傳到系統中。 Dynamic Media自動調整大小，或 _轉碼_&#x200B;把那個視頻放進多個視頻里。 然後，在交付時，它智慧地確定要使用的視頻螢幕、質量和格式，並將其交付到電話、平板電腦或台式電腦。

例如，在iOS移動設備上，它檢測4G、5G或Wi-Fi等頻寬。 然後，自動從自適應視頻集內的各種視頻比特率中選擇正確編碼的視頻。 視頻被流式傳輸到移動設備、平板電腦或台式電腦。

此外，如果網路狀況改變，視頻質量將自動切換。 而且，如果客戶在案頭上進入全屏模式，則自適應視頻集會通過使用更好的解析度來響應，從而改善客戶的觀看體驗。

使用自適應視頻集為在多個螢幕和設備上播放Dynamic Media視頻的客戶提供了流暢、高質量的回放。 它真的把複雜性從視頻中去除了。

## 用於Dynamic Media {#dm-journey-b}

以下是常見的使用案例問題和解決方案，Dynamic Media可以幫助您推動積極的客戶參與、忠誠度、轉換和增加ROI。

### 用例：主檔案方法

Dynamic Media最重要的使用案例之一也是最明顯的例子之一。 也就是說，減輕頁面和體驗的重量，減少內容的大小，不管是影像還是視頻，這些內容正在被傳送。

以下顯示典型體驗或網頁。 大約90%的頁面由富媒體組成，例如影像和視頻，這些檔案通常比較重。

![內容頁面權重](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_典型網頁的內容頁面權重。_

其餘10%為HTML、CSS代碼和特定標籤。 您希望優化90%的頁面重量，而Dynamic Media則幫助您完成這一工作。 之前，你讀到了 _一個永無可能的主資產檔案_。 此方法對於降低總頁重量非常重要。 獲取一個主要資產並將其用於產品詳細資訊頁面、縮略圖頁面、購物車和搜索網格，這是一項非常寶貴的時間。 它還確保了不同體驗之間的一致性。

![主檔案方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_監視是一個主要資產檔案，但是它有多個格式副本，而不是副本，可以即時建立。_

讓我們更仔細地看看Dynamic Media用一個檔案解決的問題以及解決這一方法的一些解決方案。

| **問題** | **Dynamic Media解** |
|---|---|
| 建立並儲存每個資產。 | 使用單個影像檔案，僅在交付時自動建立所需的格式副本。 |
| 儲存成本高。 | 無需建立和儲存資產的多個副本。 |
| 難以維持監管鏈。 | 確保提供設備優化且一致的體驗。 |
| 沒有版本歷史記錄。 |  |
| 不同設備的品牌體驗不一致。 |  |
| 建立重複資產的不必要成本。 |  |

當您考慮一個檔案時，您正在為各種體驗建立資產。 您可能有一個起始映像，然後您必須建立該映像的20、30或40個變體，您最終必須儲存並支付該儲存的費用。

然後，您必須確保使用了正確的影像，這可能會影響您跨品牌保持一致性的能力。 而且，如果找不到映像，則必須返回並複製這些資產。

Dynamic Media讓你可以即時地從這個開始的影像中建立各種影像 它使您能夠利用該主要資產進行創新，並且不必與圖形設計師或照片工作室來回交流以建立附加內容。 省錢省時。

使用一個檔案方法，可使用一個主檔案。 然後，僅在客戶交付或看到這些版本或格式副本時，才在您的站點、屬性和體驗中建立這些版本或格式副本。 這樣的效率可以大大降低您的資產所需的儲存量，並降低您的總體工作流複雜性。 而且，借助Dynamic Media的傳送系統，它可確保每個影像和視頻都得到優化、載入快速，並且在所有螢幕和設備上都看起來非常出色。

### 用例：視頻

Dynamic Media解決的另一個用例是視頻。 視頻很複雜。 很難管理。 視頻檔案由於其固有的檔案大小而難以儲存和移動。

| **問題** | **Dynamic Media解** |
|---|---|
| 難以管理和提供針對各種設備優化的視頻。 | 使用可自動調整所有設備大小的單個視頻。 |
| 由於最終用戶的可用頻寬，視頻無法正常播放或播放。 | 通過HTML播放器傳輸視頻，該播放器可自動檢測可用頻寬並調整質量以確保高保真和流暢的播放。 |
| 手動建立視頻的所有版本是不可行且耗時的，只是為了確保在設備間良好地顯示和播放。 | 通過簡化的工作流消除耗時的代碼轉換工作。 |
|  | 騰出時間做價值更高的工作。 |

客戶來到Dynamic Media時，希望解決以下問題：

&quot;_我們有這段視頻，我們花了很多錢製作它。 但是我們沒有把它放在網頁上或是傳遞出去因為通過我們的測試我們無法保證視頻的質量或者它是否真的會播放 最終，這影響了我們的品牌，也可能影響到我們的角色，甚至是轉變。_&quot;

Dynamic Media的解決方案是獲取一個主視頻檔案，並讓Dynamic Media通過其轉碼過程製作所有大小。 然後，將其與Dynamic Media的智慧視頻播放器相配。 此工作流確保無論您是在主登錄頁上還是在類別或產品詳細資訊頁面上使用該視頻，都能夠在整個過程中保持一致並以高質量提供。

這裡還有幾個使用案例需要考慮。

### 用例：單一真相來源

| **問題** | **Dynamic Media解** |
|---|---|
| 分散在整個組織中的數字資產，分散在不同的團隊或業務部門。 | 將所有數字資產儲存和管理在一個中心位置。 |
| 團隊成員下載並建立本地版本。 | 團隊成員使用單個主檔案建立 _和_ 提供各種螢幕大小和設備所需的所有版本。 |
| 為每個體驗和設備建立的一次性資產。 | 消除一次性資產，節省時間和資金來建立這些資產。 |

### 用例：基於AI的富媒體智慧裁剪

| **問題** | **Dynamic Media解** |
|---|---|
| 手動繪製、測量和剪切影像或視頻以突出顯示焦點並在所有螢幕尺寸和設備上適當顯示，耗時且耗力。 | 使用Adobe Sensei人工智慧功能Dynamic Media的Smart Crop自動檢測任何影像或視頻中的焦點，並裁剪來維護它。 |
| 時間的損失可以更好地用於創造高影響體驗。 | 捕獲預期興趣點，而不管螢幕大小。 |
| 為每個體驗和設備建立的一次性資產。 | 消除繁瑣的手動任務，提供高質量、快速載入的影像和視頻，在任何設備或螢幕上都看起來不錯。 |

### 用例：互動式媒體創作

| **問題** | **Dynamic Media解** |
|---|---|
| 平整和靜態的客戶體驗，不參與、不產生忠誠度或不推動轉換。 | 使非技術用戶能夠輕鬆、無縫地添加熱點、線索和旋轉集等交互元素，以獲得更動態、更吸引人的體驗。 |
| 數字資產投資回報有限，客戶體驗平淡。 | 推動富媒體體驗的轉換和投資回報。 |

## 資產如何通過Dynamic Media系統 {#dm-journey-c}

下面顯示了Dynamic Media的典型工作流。

![Dynamic Media工作流](/help/assets/dynamic-media/assets/dm-workflow.png)
_資產如何通過Dynamic Media系統流動。_

您從建立階段開始，主要目標是將主要資產放在最後。 這些主要資產可能來自照片、視頻供應商，也可能是您建立的一些音頻檔案。 您可以使用Adobe的Creative Suite應用程式(如Adobe InDesign、Adobe Photoshop、Adobe Illustrator)來幫助您處理內容。

建立部件完成後，通過將資產上載到Dynamic Media，將資產放入「創作」解決方案。 在Dynamic Media，確保您擁有正確的影像預設和瀏覽器，以便在您的站點上為各種網頁排好隊。

最終，您優化所有內容並將其發佈到Dynamic Media伺服器，以便它可用於Web、打印、電子郵件、案頭和移動設備。

### 將資產上傳到Dynamic Media

建立完主資產後，將其上載到Dynamic Media。 您上載的檔案類型以及檔案的格式和大小是Dynamic Media的重要屬性。 在上載時，您需要確保從一個檔案支援中獲得最大值。

例如，下面的監視影像為4560 x 3020像素。 雖然你可能永遠不會使用這樣大的影像，但你仍然可以上傳它。 影像越大，Dynamic Media能提供的畫質就越好，甚至連縮略圖都是如此。 記住：您可以輕鬆 _減少_ 現有影像的解析度。 但如果你試著 _增加_ 影像的解析度，結果可能不令人滿意。

![建議的格式上傳到Dynamic Media](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_資產上載的注意事項。_

Adobe建議以無損格式上載資產。 通常，最好避免JPEG，因為當您提供JPEG或繼續保存JPEG時，您會逐漸失去影像質量。 您希望以可以使用的無損格式從最高解析度影像開始。 該格式通常為TIFF或PNG檔案。

關於顏色空間，當您想到數字通道或Web視圖時，通常會想到RGB（紅色、綠色、藍色）。

大多數人永遠不會考慮用CMYK遞送什麼，或者您甚至為什麼想用CMYK遞送。 原因在於，色彩空間最常用於遞送印刷品。 但是，Dynamic Media可以在兩種顏色空間中實現。

還有很多客戶還在印刷，比如倉庫批發俱樂部。 還有一些雜貨店，他們經常每週打印傳單。 此類客戶要求其影像位於兩個顏色空間中。 傳統上，這需要兩種不同的影像：一個在RGB，一個在CMYK。 但是，您可以直接將CMYK資產上傳到Dynamic Media，並讓Dynamic Media通過影像預設或通過顏色配置檔案自動傳送RGB資產。 不需要建立檔案的多個版本，因此維護了 _一個永無可能的主資產檔案_。

<!-- **The Value of Renditioning??? or Demo portion** -->

### 發佈和預覽資產

在你將資產上傳到Dynamic Media後 _發佈_ 通過選擇資產，然後按一下 **[!UICONTROL 發佈]** 或 **[!UICONTROL 快速發佈]** 在Dynamic Media。 如果您打算在任何經驗中使用資產，則發佈資產是必要的。 在發佈資產後，您可以使用您所複製的Dynamic Media生成的URL或通過在頁面上嵌入代碼的方式將其包括在網頁中。

除了手動發佈資產外，您還可以配置Dynamic Media，以便在上載時立即發佈資產（無需任何用戶干預）。

上載後，在Dynamic Media中預覽資產的格式副本有不同的方法。 預覽格式副本可以幫助您瞭解客戶所看到的內容。 常見的預覽方法是選擇一個資產，然後通過選擇 _影像預設_ 如下所示。

![基於「大影像」預設預覽資產的格式副本](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_基於所選「大」影像預設預覽資產的格式副本。 已按一下URL按鈕。 生成的URL路徑包含「大」影像預設名稱，可用於網頁。_

上面的URL是即時的！ [試試看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$)。

預覽資產的另一種方法是選擇影像資產，然後選擇 _查看者_ 如下所示。

![基於「縮放垂直光線查看器」預設預覽資產](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_根據所選的「ZoomVertical_light」查看器預設預覽資產。 滑鼠指針(`+`)被移到監視器上以放大。 注意URL和「嵌入」按鈕。_

上面的節目是實況轉播！ [試試看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light)。

## 可選 — 瞭解詳情

這趟旅程的第一部分涉及各種Dynamic Media主題的基本內容。 如果您想瞭解有關剛剛閱讀的內容的更多資訊，請使用下面的材料來更詳細地瞭解概念。 否則，你可以繼續你的旅程的第二部分。 請參閱 [這趟Dynamic Media之旅接下來是什麼](#whats-next)。

_Dynamic Media幫助主題_

* [與Dynamic MediaExperience Manager合作](/help/assets/dynamic-media/dynamic-media.md)
* [關於智慧映像](/help/assets/dynamic-media/imaging-faq.md)
* [如何建立自適應視頻集](/help/assets/dynamic-media/video.md)
* [影像品質最佳化的最佳作法](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [如何上載資產](/help/assets/add-assets.md#upload-assets)
* [如何預覽資產](/help/assets/dynamic-media/previewing-assets.md)
* [如何預覽3D資產](/help/assets/dynamic-media/previewing-3d-assets.md)
* [如何交付Dynamic Media資產](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [如何發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [與選擇性出版合作在Dynamic Media](/help/assets/dynamic-media/selective-publishing.md)

_Dynamic Media教程_

* [將Dynamic Media與Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager內容庫](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) （搜索） _Dynamic Media_)

_Dynamic Media觀眾_

* [現場演示](https://landing.adobe.com/tw/na/dynamic-media/ctir-2755/live-demos.html) 每位觀眾

## 這趟Dynamic Media之旅接下來是什麼 {#whats-next}

在此路程的第二部分中，您將更仔細地檢查Dynamic MediaURL，以便更好地瞭解交付資產時發生的情況。 您還將瞭解建立影像預設以呈現資產背後的基本原理，並瞭解影像集、旋轉集和混合媒體集及其建立方式。

帶我去 [Dynamic Media之旅：《基礎》，第二部](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d)。

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->