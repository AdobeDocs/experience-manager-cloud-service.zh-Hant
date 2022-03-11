---
title: 與整合的最佳做法 [!DNL Adobe Creative Cloud]
description: 最佳做法將Experience Manager部署與Adobe Creative Cloud整合，以簡化資產轉移工作流並實現最高效率。
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration,Adobe Asset Link,Desktop App
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '3443'
ht-degree: 15%

---

# Adobe Experience Manager和Creative Cloud整合最佳做法 {#aem-and-creative-cloud-integration-best-practices}

Adobe Experience Manager資產是一種數字資產管理(DAM)解決方案，可以與Adobe Creative Cloud整合，幫助DAM用戶與創意團隊協作，簡化內容建立過程中的協作。

Adobe Creative Cloud為創意團隊提供解決方案和服務生態系統，幫助他們建立數字資產。 它包括案頭和移動應用程式、雲服務（如具有案頭同步或Web體驗的儲存）以及Adobe Stock等市場。

閱讀以瞭解根據您的使用案例在台式機和企業級DAM之間選擇哪些整合以及連接工作流的相關最佳實踐。

>[!NOTE]
>
>Experience Manager到Creative Cloud資料夾共用現在已棄用，下面不再涉及。 Adobe建議使用更新的功能，如Adobe資產連結或Experience Manager案頭應用，使創意用戶能夠訪問Experience Manager中管理的資產。

## 創意人員、營銷人員和DAM用戶的協作需求 {#collaboration-need-of-creatives-marketers-and-dam-users}

| 要求 | 用例 | 涉及的曲面 |
|---|---|---|
| 簡化台式機創意人員的體驗 | 優化對DAM資產的訪問([!DNL Assets])，或更廣泛地說，適用於在本機資產建立應用程式中工作的台式機用戶。 他們需要一種簡單而直接的方法來發現、使用（開啟）、編輯和保存對Experience Manager的更改，以及上載新檔案。 | Win或Mac台式機；Creative Cloud應用 |
| 提供高質量、可隨時使用的資產 [!DNL Adobe Stock] | 營銷人員通過協助進行資產採購和發現幫助加快內容建立過程。 創意專業人員在其創意工具中直接使用已批准的資產。 | [!DNL Assets]; [!DNL Adobe Stock] 市場；元資料欄位 |
| 按組織分配和共用資產 | 內部部門/地方分支機構和外部合作夥伴、分銷商和代理機構使用母公司共用的批准資產。 該組織希望安全、無縫地共用建立的資產，以便更廣泛地重複使用。 | [!DNL Brand Portal], [!DNL Asset Share Commons] |
| 自動生成上載資產的預定義變體 | 自動處理資產，利用Adobe獨特的介質處理和轉換技術執行預定義的操作。 建立自定義邏輯以使用API和資產微服務定義您自己的操作。 | [!DNL Assets] 用戶介面 |

## Adobe支援協作需求的產品 {#adobe-offerings-to-support-the-collaboration-need}

| 涉案人員的價值主張 | Adobe | 涉及的曲面 |
|---|---|---|
| 創意用戶從 [!DNL Experience Manager]，開啟並使用它們，編輯和上載更改 [!DNL Experience Manager]，以及將新檔案上載到 [!DNL Experience Manager]不離開他們 [!DNL Creative Cloud] 的子菜單。 | [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) | Photoshop,Illustrator和InDesign。 |
| 業務用戶簡化了資產的開啟和使用、編輯和上載更改 [!DNL Experience Manager]，將新檔案上載到 [!DNL Experience Manager] 從案頭環境中。 它們使用通用整合來開啟本機案頭應用程式中的任何資產類型，包括非Adobe類型。 | [[!DNL Experience Manager] 桌面應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Experience ManagerWin和Mac案頭應用 |
| 營銷商和商業用戶從Experience Manager中發現、預覽、許可和保存並管理Adobe Stock資產。 獲得許可和保存的資產可提供精選的Adobe Stock元資料，以更好地治理。 | [Experience Manager和Adobe Stock一體化](aem-assets-adobe-stock.md) | [!DNL Experience Manager] Web介面 |
| 改進數字產品設計者和營銷人員之間的協作。 讓設計師在Adobe XD畫布上的設計和線框模型中使用數字資產。 | [[!DNL Adobe Asset Link] 為 [!DNL Adobe XD]](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| 營銷人員可以根據上載的資產和使用自定義建立的預定義操作自動建立變體和衍生。 使用此自動化提高內容速度並減少手動工作量。 | [內容自動化](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] Web介面 |

本文主要針對協作需求的前兩個方面。資產規模分配和採購作為一個使用案例被簡要提及。針對這些需求解決方案，請考慮Adobe品牌入口網站或資產共用公域。備用解決方案，如 [Experience Manager AssetsBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可基於 [資產共用共用](https://opensource.adobe.com/asset-share-commons/) 元件， [連結共用](share-assets.md)，使用 [Experience Manager Assets網頁用戶介面](/help/assets/manage-digital-assets.md) 應根據具體要求進行審查。

![Creative CloudExperience Manager連接：確定要使用的功能](assets/creative-connections-aem.png)

決定使用哪些能力

### 用例和Adobe解決方案的映射 {#mapping-of-use-cases-and-adobe-solutions}

| 用例 | Adobe資產連結 | Experience manager 桌面應用程式 | 注釋或替代方法 |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| 發現 — 瀏覽資料夾 | 是 | Experience ManagerWeb UI +案頭操作 | 瀏覽網路共用時，關閉縮略圖以避免下載資產的二進位檔案。 |
| 發現 — 訪問集合 | 是 | Experience ManagerWeb UI +案頭操作 |  |
| 發現 — 搜索資產 | 是 | Experience ManagerWeb UI +案頭操作 |  |
| 使用 — 開啟資產 | 是 | 是 — 適用於任何應用 | [從Web介面開啟](/help/assets/manage-digital-assets.md#previewing-assets) 或來自Finder |
| 使用 — 將資產從Experience Manager置入文檔 | 是 — 嵌入 | 是 — 連結或嵌入 | Experience Manager案頭應用允許以本地檔案系統上的檔案形式訪問資產。 本機應用中的這些連結由本地路徑表示。 |
| 編輯 — 開啟以進行編輯 | 是 — 簽出操作 | 是 — 開啟操作（在網路共用中） | [AAL簽出](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) 預設情況下，將資產保存到用戶的創意雲儲存帳戶(由Creative Cloud應用同步)。 |
| 編輯 — 在Experience Manager外進行中 | 是 — 在與案頭同步的用戶Creative Cloud儲存帳戶中可用的資產。 | 是 |  |
| 編輯 — 上載更改 | 是 —  [簽入操作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 帶可選注釋 | 是 |  |
| 上載 — 單個檔案 | 是 — 上載當前活動文檔 | 是 | [通過Web介面上載](/help/assets/manage-digital-assets.md#uploading-assets) |
| 上載 — 多個檔案/分層資料夾結構 | 否 | 是 | [通過Web介面上載](/help/assets/manage-digital-assets.md#uploading-assets);自定義指令碼或工具 |
| 雜項 — 用戶和登錄 | Creative Cloud用戶登錄Creative Cloud案頭應用程式後可被識別(SSO) | Experience Manager用戶/登錄 | 兩個解決方案的用戶都按Experience Manager用戶配額計算。 |
| 雜項 — 網路和訪問 | 需要從用戶案頭訪問網路上的Experience Manager部署 | 需要從用戶案頭訪問網路上的Experience Manager部署 | Adobe資產連結不共用網路代理環境。 |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

要支援資產分配使用案例，請考慮以下選項：

* [Experience Manager AssetsBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 可配置的「資產」載入項以發佈資產。

* 定制解決方案基於 [資產共用共用](https://opensource.adobe.com/asset-share-commons/) 代碼庫。
* Experience Manager [連結共用](/help/assets/share-assets.md) 使用連結臨時共用資產。
* [資產Web介面](/help/assets/manage-digital-assets.md) 通過Experience Manager訪問控制設定保護外部用戶的區域以及必要的IT/網路配置調整，使這些外部用戶能夠訪問Experience Manager。

## 關鍵概念和使用案例 {#key-concepts-and-use-cases}

### 通用術語表 {#glossary-of-common-terms}

* **在製品或創意在製品 (WIP)：**&#x200B;在資產生命週期中，資產會經歷多次變更，且通常尚未準備好更廣泛地與其他團隊共用的階段。
* **創意成熟資產：**&#x200B;已準備好更廣泛地與其他團隊共用，或已獲創意團隊選取/核准，要與行銷或 LOB 團隊共用的資產。

* **資產核准：**&#x200B;針對已上傳至 DAM 的資產執行的核准程序，通常包括品牌核准、法律核准等。
* **最終資產：**&#x200B;已完成所有核准/中繼資料標記，且已準備好更廣泛地供團隊使用的資產。此類資產會儲存在 DAM 中，並提供給所有 (或所有相關的) 使用者使用。這類資產可用於行銷管道，或供創意團隊創作設計。

* **小幅度資產更新/變更：**&#x200B;數位資產的快速微幅變更。此類更新/變更通常是為了因應潤飾或微幅編輯請求、資產檢閱或核准 (例如重新定位、變更文字大小、調整飽和度/亮度、顏色等) 而進行的。
* **重大資產更新/變更：**&#x200B;需要大量工作，且有時需要較長時間才能完成的數位資產變更。其中通常包含多項變更。資產在更新時必須儲存多次。重大資產更新通常會導致資產進入 WIP 階段。
* **DAM：**&#x200B;數位資產管理。在此文件中，其意義與 Experience Manager Assets 相同，除非另有特別說明。
* **創意使用者：**&#x200B;使用 Creative Cloud 應用程式和服務建立數位資產的創意專業人員。在某些情況下，創意使用者可能是可使用 Creative Cloud、但不會建立數位資產的創意團隊成員 (例如創意總監或創意團隊經理)。
* **DAM 使用者：** DAM 系統的一般使用者。視組織而異，DAM 使用者可能是行銷或非行銷使用者，例如企業營運 (LOB) 使用者、圖書管理員、銷售人員等。

### 使用Experience Manager和Creative Cloud整合時的注意事項 {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

這是Experience Manager和Creative Cloud整合最佳實踐的簡要摘要。 閱讀本文檔的其餘部分，以詳細瞭解這些內容。

* **對於在Photoshop、InDesign或Illustrator工作的創意用戶：** Adobe資產連結提供最佳用戶體驗，包括清理從Experience Manager中籤出的資產的在製品處理
* **為簡化從案頭訪問任何通用檔案格式或應用程式的資產：** 使用Experience Manager案頭應用
* **** 瞭解在DAM中儲存資產的原因及時機：更新將提供給組織中更廣大的團隊
* **** 請留意共用資產的數量：如果您的使用案例是資產分發，則治理和安全性可能是最重要的方面。請考慮使用大型工具 (例如品牌入口網站) 進行此作業。
* **** 瞭解資產生命週期：瞭解不同團隊在組織中如何處理資產
* **** 謹慎處理資產的頻繁儲存：Adobe Asset Link會透過PS、AI、ID為您處理。對於其他應用程式，請勿在映射/共用資料夾中執行進行中的工作，除非您需要DAM中的所有變更

### 從Experience Manager Assets獲得Adobe Stock資產 {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager和Adobe Stock一體化](/help/assets/aem-assets-adobe-stock.md) 使Experience Manager用戶能夠從Adobe Stock搜索、預覽、許可和保存資產到Experience Manager。 已獲許可和保存的Adobe Stock資產已選擇了Stock元資料，該元資料可用於使用額外的篩選器搜索這些元資料。

關於此整合的幾個重要點：

* 將Adobe庫中的資產保存到Experience Manager後，這些資產將變成常規Experience Manager Assets，二進位檔案將保存到Experience Manager庫。 與Adobe Stock相關的某些元資料會保存到Experience Manager中的資產，否則，接收過程與任何其他檔案看起來相同。 例如，如果智慧標籤處於活動狀態，則在保存時，這些標籤會添加到這些資產中。
* 保存到Experience Manager的資產是副本，而不是返回到Adobe Stock的連結。

**使用從Adobe Stock節省下來的資產轉為Creative Cloud的Experience Manager**。 此整合與Adobe資產連結無關，但Adobe資產連結通過這種方式識別從存貨中保存的這些資產，並在Photoshop、Illustrator或InDesign的Adobe資產連結擴展UI中顯示這些資產的附加元資料和存貨表徵圖。 這些檔案可用於瀏覽、開啟等 — 因為它們是保存到Experience Manager時的常規Experience Manager資產。
在Creative Cloud應用程式中工作且存在Adobe資產連結擴展的創意用戶，除了能夠訪問從Adobe Stock到Experience Manager的已許可資產外，還可以使用Creative Cloud庫面板搜索、預覽和許可Adobe Stock資產。
獲得Adobe Stock授權並保存到Experience Manager中的資產可供更廣泛的團隊訪問Experience Manager Assets部署，而通過Creative Cloud庫面板授權Adobe Stock資產的創意人員則只能在其Creative Cloud帳戶中預設自用。

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

要在創意和營銷/業務線(LOB)團隊之間設計一個高效的工作流，並選擇最佳支援功能，瞭解資產在何時以及為什麼儲存在DAM中非常重要。

### 為什麼資產儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，可輕鬆訪問和查找。 它確保整個組織或生態系統中的眾多用戶能夠利用這些資產，包括合作夥伴、客戶等。

大多陣列織選擇只儲存與下游市場營銷/LOB流程相關的資產(通過Experience Manager Sites或Adobe Experience Cloud服務的其他渠道發佈到Web渠道等渠道 — Marketing Cloud、Advertising Cloud，以及Analytics Cloud衡量、向用戶/合作夥伴提供等)。 此外，組織在DAM中儲存可能要經過審核/批准過程的資產。 這樣，DAM就可以儲存大部分具有高槓桿率的資產，並避免儲存閒置資產。

儲存資產還需要考慮技術和資源利用方面的考慮。 DAM圍繞儲存的資產提供其他服務，包括提取元資料、版本控制、生成預覽/轉碼、管理引用和添加訪問控制資訊。 這些服務消耗了額外的時間和基礎架構資源。

通常，儲存所有資產和更新是不可取的。 例如，如果對特定資產的更新質量差，並且消耗了過多的資源，則資產可能不會儲存在DAM中。

#### 當資產儲存在DAM中時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對在資產生命週期的每個階段儲存資產不感興趣。 例如，在以下情況下，它們避免儲存資產：

* 尚未定稿或有待試驗的資產
* 未能通過創意/內部團隊審核週期的資產
* 與相關資產相比，團隊有更好的候選人將工作代表給外部團隊

通常，以下類資產儲存在DAM中：

* 已到期且被視為可共用的資產
* 由創意團隊預先選擇的資產
* 根據特定合同或協定(例如，從RAW檔案轉換的JPG檔案、從PSD原件轉換的TIFF/影像)，市場營銷可使用或請求的特定資產格式

#### 當資產更新儲存在DAM中 {#when-updates-to-assets-are-stored-in-dam}

通常，只應將與更廣的DAM用戶組相關的資產更新儲存在DAM中。 它確保用戶（營銷和類似功能）只能在DAM資產時間表中查看相關版本。

通常與資產生命週期中的主要里程碑相關的更改。 例如，應將初始市場準備資產或創意團隊提供的基於請求/審查的正式更新儲存在DAM中並對其進行版本控制。

在請求更改DAM中的現有資產後，創意團隊的更新以供市場營銷團隊審閱是相關更新的示例。 應將其儲存並版本化到DAM中，以供進一步參考或還原到以前的版本。

以下是通常不相關的更新示例：

* 在準備好進行營銷審查之前上載的資產的早期版本
* 在進行中工作階段頻繁對資產進行創造性更改，然後創意和營銷團隊才確定資產已準備好

### 用戶對DAM的訪問 {#user-access-to-dam}

Experience Manager Assets根據用戶對Experience Manager Assets部署的訪問支援兩類用戶。 通常，企業網路（防火牆）內的用戶可以直接訪問DAM。 企業網路之外的其他用戶將無權直接訪問。 用戶類型從技術角度確定可以使用哪些整合。

#### 直接訪問DAM的創意用戶 {#creative-users-with-direct-access-to-dam}

通常，內部創意團隊或機構/參與內部網路的創意專業人士可以訪問DAM實例，包括Experience Manager登錄。 可以設定Experience Manager和網路基礎架構，以允許直接訪問外部方 — 通常是受信任的組織，如為客戶工作的機構 — 有權通過網路訪問Experience Manager，例如，通過VPN或IP允許清單。

在這種情況下，Adobe資產連結或Experience Manager案頭應用程式可以輕鬆訪問最終/批准的資產，並允許您將創意就緒的資產保存到DAM。

#### 無法訪問DAM的創意用戶 {#creative-users-without-access-to-dam}

沒有直接訪問DAM實例的外部機構和自由職業者可能需要訪問經批准的資產或希望將其新設計添加到DAM。

使用以下策略提供對最終/批准資產的訪問：

* 如果資產連結不工作，則使用案頭應用。
* 使用 [Experience Manager AssetsBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用於將資產安全地分發給外部合作夥伴
* 使用基於的分發和採購門戶的自定義實現 [資產共用共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在Experience Manager和必要的網路基礎架構（例如，VPN和IP允許清單）中設定的訪問控制，使外部方可以訪問DAM中的專用內容區域。 他們可以使用Experience ManagerWeb UI獲取資產並將新內容上載到您的DAM中。

#### 正在對來自Experience Manager的資產進行處理 {#work-in-progress-on-assets-from-aem}

如本文檔中所討論的，建議對資產執行重大更新，有時稱為正在進行的工作，而不會將保存到本地檔案的所有編輯內容也作為更改上載到Experience Manager。 這可加快案頭用戶的工作速度，限制網路頻寬的使用，並保持資產時間線整潔，並專注於受控的主要更新。

Adobe資產連結為此使用情形提供了良好的支援：

* 當Photoshop、InDesign或Illustrator的用戶想要編輯檔案時，他們將對給定資產執行「簽出」操作
* 資產在後台下載，通過Creative Cloud案頭應用將其放入與磁碟同步的用戶Creative Cloud帳戶中，並且簽出標誌在資產上Experience Manager，以最大限度地減少編輯衝突
* 從此，用戶將在儲存在同步位置本地的檔案中工作，並可以繼續工作並以任何所需頻率保存必要的更改
* 此外，由於資產在Creative Cloud帳戶中，因此用戶可能具有的其他設備上也提供了該資產(例如，可以在專用的Creative Cloud移動應用中開啟或編輯)，並且可以與其他Creative Cloud用戶共用以進行協作。
* 當創意用戶完成更改後，他們可以在其Creative Cloud應用程式中對該檔案執行「簽入」操作，並附上可選注釋。 對Experience Manager中的相應資產進行版本控制並使用新二進位更新到。 Experience Manager用戶（如營銷人員或LOB用戶）可以通過Experience Manager資產時間表UI訪問重大資產更改或里程碑。

Experience Manager案頭應用為在本機應用中開啟的資產提供網路共用。 預設情況下，本地完成的所有更改在短暫一段時間後自動上載到Experience Manager。 有了這種配置，在進行中工作階段經常進行的儲存將全部上傳到Experience Manager中並進行版本控制，從而產生大量網路流量和潛在的可擴充性挑戰 — 更不用說Experience Manager中不必要的版本了。

此處推薦的方法是使用Experience Manager案頭應用中的選項來關閉自動更新，並利用應用的「資產狀態」UI中的上載更改操作將更改上載到Experience Manager中。

#### 批量上載到DAM {#bulk-upload-to-dam}

在某些情況下，您可能需要同時將大量檔案上載到DAM中，例如：

* 上傳照片或大型項目的結果
* 上傳創意機構提供的資產
* 如果選擇在DAM外完成，則從較大集上載所選資產

請注意，此描述是指在操作上（例如，每週或每張照片）上傳檔案，作為案頭用戶工作流的正常部分。 此處未涵蓋大型資產遷移。

您可以利用以下上載功能：

* 要批量上載大型/分層資料夾，請使用Experience Manager案頭應用程式 [資料夾上載](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets) 功能。 您還可以上載分層資料夾結構。 資產在後台上載，因此不會與Web瀏覽器會話關聯
* 要從單個資料夾上載幾個檔案，請將檔案直接拖到Web介面或使用Experience Manager AssetsWeb介面中的「建立」選項。
* 根據您的業務需求，您還可以使用自定義上載程式。

#### 直接從台式機管理數字資產 {#managing-digital-assets-directly-from-desktop}

如果您使用網路檔案共用來管理數字資產，僅使用Experience Manager案頭應用映射的網路共用就可以被視為方便的替代。 從網路檔案共用轉換時，Experience ManagerWeb介面提供了一組豐富的數字資產管理功能，遠遠超出了網路共用（搜索、收集、元資料、協作、預覽等）的可能範圍，而Experience Manager案頭應用提供了將伺服器端DAM儲存庫與案頭工作連接起來的便捷連結。

避免使用Experience Manager案頭應用直接管理Experience Manager Assets網路共用中的資產。 例如，避免使用Experience Manager案頭應用移動/複製多個檔案。 相反，使用Experience Manager AssetsWeb UI將資料夾從Finder/Explorer拖到網路共用或使用Experience Manager Assets資料夾上載功能。
