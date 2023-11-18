---
title: 整合的最佳實務 [!DNL Adobe Creative Cloud]
description: 最佳實務會整合Experience Manager部署與Adobe Creative Cloud，以簡化資產傳輸工作流程並實現最高效率。
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration,Adobe Asset Link,Desktop App
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '3489'
ht-degree: 15%

---

# Adobe Experience Manager與Creative Cloud整合最佳實務 {#aem-and-creative-cloud-integration-best-practices}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

Adobe Experience Manager Assets是數位資產管理(DAM)解決方案，可與Adobe Creative Cloud整合，以協助DAM使用者與創意團隊合作，精簡內容建立過程中的共同作業。

Adobe Creative Cloud為創意團隊提供解決方案和服務的生態系統，以協助他們建立數位資產。 其中包括桌上型電腦和行動應用程式、具備案頭同步或Web體驗的儲存空間等雲端服務，以及Adobe Stock等市集。

請閱讀下文，瞭解根據您的使用案例，在桌上型電腦和企業級DAM之間選擇哪些整合，以及連線工作流程的相關最佳實務為何。

>[!NOTE]
>
>Creative Cloud資料夾共用的Experience Manager現已棄用，不再涵蓋於下方。 Adobe建議使用較新的功能，例如Adobe Asset Link或Experience Manager案頭應用程式，以便創意使用者可以存取Experience Manager中管理的資產。

## 創意工作者、行銷人員和DAM使用者的共同作業需求 {#collaboration-need-of-creatives-marketers-and-dam-users}

| 要求 | 使用案例 | 相關曲面 |
|---|---|---|
| 簡化創意人員在桌上型電腦上的體驗 | 簡化從DAM存取資產([!DNL Assets])適合創意專家，或更廣義地說，適合使用原生資產建立應用程式的案頭使用者。 他們需要一種簡單明瞭的方式，以探索、使用（開啟）、編輯和儲存對Experience Manager的變更，以及上傳新檔案。 | Win或Mac案頭；Creative Cloud應用程式 |
| 提供高品質、現成可用的資產，來自 [!DNL Adobe Stock] | 行銷人員協助資產來源和探索，以加速內容建立流程。 創意專業人士會直接從自己的創意工具中使用核准的資產。 | [!DNL Assets]； [!DNL Adobe Stock] 市集；中繼資料欄位 |
| 依組織分配與共用資產 | 內部部門/當地分支機構和外部合作夥伴、分銷商和代理商會使用上級組織共用的已核准資產。 企業想要安全且順暢地共用已建立的資產，以便更廣泛地重複使用。 | [!DNL Brand Portal]、[!DNL Asset Share Commons] |
| 自動產生已上傳資產的預先定義變體 | 使用Adobe獨特的媒體處理和轉換技術，針對預先定義的動作自動處理資產。 建立自訂邏輯，以使用API和資產微服務定義您自己的動作。 | [!DNL Assets] 使用者介面 |

## 支援協同合作需求的Adobe方案 {#adobe-offerings-to-support-the-collaboration-need}

| 相關角色的價值主張 | Adobe產品 | 相關曲面 |
|---|---|---|
| 創意使用者可從發現資產 [!DNL Experience Manager]，開啟並使用它們、編輯和上傳變更至 [!DNL Experience Manager]，並將新檔案上傳至 [!DNL Experience Manager]，而不需離開其 [!DNL Creative Cloud] 應用程式。 | [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator和InDesign。 |
| 業務使用者簡化開啟和使用資產、編輯及上傳變更至 [!DNL Experience Manager]，並將新檔案上傳至 [!DNL Experience Manager] 從案頭環境。 他們使用一般整合，在原生案頭應用程式中開啟任何資產型別，包括非Adobe資產型別。 | [[!DNL Experience Manager] 桌面應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | 在Win和Mac案頭上Experience Manager案頭應用程式 |
| 行銷人員和商務使用者可在Experience Manager中探索、預覽、授權並儲存及管理Adobe Stock資產。 授權和儲存的資產可提供精選的Adobe Stock中繼資料，以改善治理。 | [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md) | [!DNL Experience Manager] 網頁介面 |
| 改善數位產品設計師和行銷人員之間的協同合作。 讓設計人員在Adobe XD畫布上的設計和線框模型中使用數位資產。 | [[!DNL Adobe Asset Link] 代表 [!DNL Adobe XD]](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| 行銷人員可以根據上傳的資產和使用自訂建立的預先定義動作，自動建立變數和衍生產品。 使用此自動化功能來改善內容速度並減少手動操作。 | [內容自動化](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] 網頁介面 |

本文主要針對協作需求的前兩個方面。資產規模分配和採購作為一個使用案例被簡要提及。針對這些需求解決方案，請考慮Adobe品牌入口網站或資產共用公域。替代解決方案，例如 [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可根據以下專案建置的解決方案： [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) 元件， [連結共用](share-assets.md)，使用 [Experience Manager Assets Web UI](/help/assets/manage-digital-assets.md) 應根據特定需求審查。

![用於Experience Manager的Creative Cloud連線：決定要使用哪個功能](assets/creative-connections-aem.png)

決定要使用哪個功能

### 使用案例和Adobe解決方案的對應 {#mapping-of-use-cases-and-adobe-solutions}

| 使用案例 | Adobe Asset Link | Experience manager 桌面應用程式 | 備註或替代方法 |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| 探索 — 瀏覽資料夾 | 是 | Experience ManagerWeb UI +案頭動作 | 瀏覽網路共用時，請關閉縮圖以避免下載資產的二進位檔案。 |
| 探索 — 存取集合 | 是 | Experience ManagerWeb UI +案頭動作 |  |
| 探索 — 搜尋資產 | 是 | Experience ManagerWeb UI +案頭動作 |  |
| 使用 — 開啟資產 | 是 | 是 — 適用於任何應用程式 | [從Web介面開啟](/help/assets/manage-digital-assets.md#previewing-assets) 或從Finder |
| 使用 — 將資產從Experience Manager放入檔案中 | 是 — 內嵌 | 是 — 連結或內嵌 | Experience Manager案頭應用程式可存取本機檔案系統上的資產。 原生應用程式中的這些連結會以本機路徑表示。 |
| 編輯 — 開啟以進行編輯 | 是 — 結帳動作 | 是 — 開啟動作（在網路共用中） | [在AAL簽出](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 依預設，會將資產儲存至使用者的creative cloud storage帳戶(由Creative Cloud應用程式同步)。 |
| 編輯 — 在Experience Manager外部進行中的工作 | 是 — 資產可在同步至桌上型電腦的使用者Creative Cloud儲存帳戶中使用。 | 是 |  |
| 編輯 — 上傳變更 | 是 —  [簽入動作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 含選擇性註解 | 是 |  |
| 上傳 — 單一檔案 | 是 — 上傳目前作用中的檔案 | 是 | [透過網頁介面上傳](/help/assets/manage-digital-assets.md#uploading-assets) |
| 上傳 — 多個檔案/階層資料夾結構 | 否 | 是 | [透過網頁介面上傳](/help/assets/manage-digital-assets.md#uploading-assets)；自訂指令碼或工具 |
| 其他 — 使用者和登入 | 可辨識登入Creative Cloud案頭應用程式的Creative Cloud使用者(SSO) | Experience Manager使用者/登入 | 這兩個解決方案的使用者都會計入Experience Manager的使用者配額。 |
| 雜項 — 網路與存取 | 需要從使用者的案頭存取許可權，才能透過網路Experience Manager部署 | 需要從使用者的案頭存取許可權，才能透過網路Experience Manager部署 | Adobe資產連結不共用網路Proxy環境。 |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

若要支援資產散佈使用案例，請考慮下列選項：

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) ，用於可設定的Assets附加元件以發佈資產。

* 自訂解決方案是根據 [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) 程式碼基底。
* Experience Manager [連結共用](/help/assets/share-assets.md) 以使用連結來臨機共用資產。
* [Assets網頁介面](/help/assets/manage-digital-assets.md) 利用Experience Manager存取控制設定保護外部合作方的區域，以及必要的IT/網路組態調整，讓這些外部使用者能夠存取Experience Manager。

## 重要概念與使用案例 {#key-concepts-and-use-cases}

### 常用辭彙表 {#glossary-of-common-terms}

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

以下是Experience Manager和Creative Cloud整合最佳實務的簡短摘要。 請閱讀本檔案的其餘部分，以取得這些專案的詳細瞭解。

* **對於在Photoshop、InDesign或Illustrator中工作的創意使用者：** Adobe Asset Link提供最佳的使用者體驗，包括對從Experience Manager結帳的資產進行中工作的簡潔處理
* **為簡化從案頭存取任何一般檔案格式或應用程式的資產：** 使用Experience Manager案頭應用程式
* **** 瞭解在DAM中儲存資產的原因及時機：更新將提供給組織中更廣大的團隊
* **** 請留意共用資產的數量：如果您的使用案例是資產分發，則治理和安全性可能是最重要的方面。請考慮使用大型工具 (例如品牌入口網站) 進行此作業。
* **** 瞭解資產生命週期：瞭解不同團隊在組織中如何處理資產
* **** 謹慎處理資產的頻繁儲存：Adobe Asset Link會透過PS、AI、ID為您處理。對於其他應用程式，請勿在對映/共用資料夾中執行進行中的工作，除非您需要DAM中的所有變更

### 從Experience Manager Assets存取Adobe Stock資產 {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager與Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md) 讓Experience Manager使用者能夠從Adobe Stock搜尋、預覽、授權及儲存資產，並將其儲存至Experience Manager。 授權並儲存的Adobe Stock資產已選取Stock中繼資料，這些中繼資料可用來透過額外篩選器搜尋這些資產。

關於這項整合的一些要點：

* 來自Adobe庫存的資產儲存到Experience Manager時，它們會變成一般Experience Manager Assets，而二進位檔案會儲存到Experience Manager存放庫。 系統會為資產儲存一些與Adobe Stock相關的中繼資料，以便使用Experience Manager，否則擷取程式看起來會與任何其他檔案相同。 例如，如果智慧標籤作用中，會在儲存時將標籤新增到這些資產。
* 儲存至Experience Manager的資產為副本，而非返回Adobe Stock的連結。

**使用從Adobe Stock儲存到Creative CloudExperience Manager中的資產**. 此整合獨立於Adobe Asset Link，但Adobe Asset Link可辨識以此方式從Stock儲存的這些資產，並在Photoshop、Illustrator或InDesign的Adobe Asset Link擴充功能UI中，於這些資產上顯示其他中繼資料和庫存圖示。 檔案可供瀏覽、開啟等操作，因為它們是儲存為Experience Manager時的一般Experience Manager資產。
創意內容使用者在Creative Cloud應用程式中使用Adobe Asset Link擴充功能，除了可以從Adobe Stock存取已授權的資產至Experience Manager之外，還可以使用Creative Cloud資料庫面板來搜尋、預覽和授權Adobe Stock資產。
從Adobe Stock授權並儲存至Experience Manager的資產可供存取Experience Manager Assets部署的更廣泛團隊使用，而創意人員透過Adobe Stock的Creative Cloud資料庫面板授權資產，使其預設只能在其Creative Cloud帳戶中供自己使用。

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

為了在創意和行銷/業務線(LOB)團隊之間設計有效率的工作流程，並選擇最佳支援功能，瞭解資產儲存在DAM中的時間和原因非常重要。

### 為何資產儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，可讓您輕鬆存取及找到資產。 這可確保整個組織或生態系統中的多位使用者（包括合作夥伴、客戶等）都能使用資產。

大部分組織會選擇僅儲存與下遊行銷/LOB流程相關的資產(透過Experience Manager Sites發佈至Web頻道等頻道，或由Adobe Experience Cloud提供的其他頻道(Marketing Cloud、Advertising Cloud和由Analytics Cloud測量，提供給使用者/合作夥伴等)。 此外，組織可儲存資產，這些資產可能會在DAM中接受稽核/核准程式。 如此一來，DAM主要儲存極有可能使用的資產，避免儲存閒置資產。

儲存資產也受到技術和資源使用率考量的限制。 DAM提供有關已儲存資產的其他服務，包括擷取中繼資料、版本設定、產生預覽/轉碼、管理參考和新增存取控制資訊。 這些服務會消耗額外的時間和基礎架構資源。

通常情況下，儲存所有資產和更新是不合需要的。 例如，如果特定資產的更新品質不佳並消耗過多資源，則資產可能不會儲存在DAM中。

#### 當資產儲存在DAM時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對儲存資產生命週期每個階段的資產不感興趣。 例如，他們會避免在下列情況下儲存資產：

* 尚未完成或有待實驗的資產
* 未通過創意/內部團隊稽核週期的資產
* 相較於相關資產，團隊擁有更好的候選人來向外部團隊代表他們的工作

通常，以下類別資產會儲存在DAM中：

* 達到特定到期日且被視為可共用的資產
* 創意團隊預先選取的資產
* 行銷可用或要求的特定資產格式，取決於特定合約或協定(例如，從RAW檔案轉換的JPG檔案、來自PSD原始資料的TIFF/影像)

#### 當資產的更新儲存在DAM中時 {#when-updates-to-assets-are-stored-in-dam}

一般而言，只有與更廣泛的DAM使用者組相關的資產更新才應儲存在DAM中。 這可確保使用者（行銷和類似功能）在DAM資產時間軸中只能看到相關版本。

通常會與資產生命週期中的主要里程碑相關的變更。 例如，初始行銷就緒資產或根據創意團隊提供的請求/稽核的正式更新應儲存在DAM中並進行版本設定。

相關更新的範例為創意團隊的更新，以供行銷團隊在請求變更DAM中的現有資產後檢閱。 應儲存在DAM中並進行版本設定，以供進一步參考或回覆至先前的版本。

以下是通常不相關的更新範例：

* 在資產準備好供行銷檢閱之前上傳資產的早期版本
* 創意和行銷團隊決定資產準備好之前，經常在創作中階段對資產進行創意變更

### DAM的使用者存取權 {#user-access-to-dam}

根據使用者對Experience Manager Assets部署的存取權，Experience Manager Assets支援兩種使用者。 一般而言，企業網路（防火牆）內的使用者可直接存取DAM。 企業網路以外的其他使用者無法直接存取。 使用者型別會從技術的角度決定可使用哪些整合。

#### 可直接存取DAM的創意使用者 {#creative-users-with-direct-access-to-dam}

通常，內部創意團隊或加入內部網路的代理/創意專業人士有權存取DAM執行個體，包括Experience Manager登入。 可以設定Experience Manager和網路基礎結構，允許直接存取外部合作對象（通常是受信任的組織，例如為使用者端工作的機構），以透過網路（例如，透過VPN或IP允許清單）存取Experience Manager。

在這種情況下，Adobe資產連結或Experience Manager案頭應用程式可讓您輕鬆存取最終/核准的資產，並可讓您將創意就緒的資產儲存到DAM。

#### 沒有DAM存取權的創意使用者 {#creative-users-without-access-to-dam}

無法直接存取DAM例項的外部機構和自由職業者可能會要求存取已核准的資產，或想要將其新設計新增到DAM。

使用下列策略提供最終/已核准資產的存取權：

* 如果Asset Link無法運作，請使用案頭應用程式。
* 使用 [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用於將資產安全地分發給外部合作夥伴
* 根據下列條件使用自訂的發佈和來源入口網站實作： [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用Experience Manager中設定的存取控制和必要的網路基礎結構（例如VPN和IP允許清單），讓外部各方能夠存取DAM中的專用內容區域。 他們可以使用Experience Manager Web UI來取得資產，並將新內容上傳到您的DAM。

#### 來自Experience Manager的資產工作進行中 {#work-in-progress-on-assets-from-aem}

如本檔案所述，建議對資產進行重大更新，有時稱為進行中的工作，而不需將所有編輯內容儲存至本機檔案，也不會以變更的形式上傳至Experience Manager。 這可加快案頭使用者的工作速度、限制使用的網路頻寬，並讓資產時間表保持整潔，並專注於受控制的重大更新。

Adobe Asset Link針對此使用案例提供良好的支援：

* 當Photoshop、InDesign或Illustrator的使用者意圖編輯檔案時，會對指定的資產執行簽出操作
* 資產會在背景下載，並透過Creative Cloud案頭應用程式放入與磁碟同步的使用者Creative Cloud帳戶中，而取出旗標會在資產上以Experience Manager切換，以將編輯衝突減至最低
* 從此處，使用者可在檔案中工作，該檔案儲存在同步位置中的本機，並可繼續工作，並視需要以任意頻率儲存必要的變更
* 此外，由於資產位於Creative Cloud帳戶中，因此該資產也可在使用者可能擁有的其他裝置上使用(例如，可在專用的Creative Cloud行動應用程式中開啟或編輯)，並可與其他Creative Cloud使用者共用，以進行共同作業。
* 當創意使用者完成變更時，他們可以在其Creative Cloud應用程式中對該檔案執行簽入操作，並附上可選註釋。 Experience Manager中的對應資產會建立版本，並使用新的二進位檔更新為。 行銷人員或LOB使用者等Experience Manager使用者可透過Experience Manager資產時間軸UI存取重大資產變更或里程碑。

Experience Manager案頭應用程式為在原生應用程式中開啟的資產提供網路共用。 依預設，所有在本機完成的變更都會在短時間內自動上傳至Experience Manager。 透過這種設定，進行中階段期間頻繁的儲存將全部上傳到Experience Manager並進行版本設定，從而造成大量的網路流量和潛在的可擴充性挑戰，更不用說不必要的Experience Manager版本了。

這裡建議的方法是使用Experience Manager案頭應用程式中的選項來關閉自動更新，並使用應用程式資產狀態UI中的上傳變更動作手動上傳資產變更以Experience Manager。

#### 大量上傳至DAM {#bulk-upload-to-dam}

在某些案例中，您可能會需要同時將大量檔案上傳到DAM，例如：

* 上傳拍照或大型專案的結果
* 上傳創意公司提供的資產
* 如果選取是在DAM以外完成，則從較大的集合上傳選取的資產

請注意，此說明是指以作業方式上傳檔案（例如，每週或每次拍照），作為案頭使用者工作流程的一般部分。 這裡不涵蓋大型資產移轉。

您可以使用以下上傳功能：

* 若要大量上傳大型/階層資料夾，請使用提供下列功能的Experience Manager案頭應用程式： [資料夾上傳](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets) 功能。 您也可以上傳階層資料夾結構。 資產會在背景上傳，因此不會與網頁瀏覽器工作階段繫結
* 若要從單一資料夾上傳一些檔案，請直接將檔案拖曳至網頁介面，或使用Experience Manager Assets網頁介面中的「建立」選項。
* 您也可以根據您的業務需求使用自訂上傳程式。

#### 直接從案頭管理數位資產 {#managing-digital-assets-directly-from-desktop}

如果您使用「網路檔案共用」來管理數位資產，只需使用Experience Manager案頭應用程式對應的網路共用即可視為方便的替代方式。 從網路檔案共用轉換時，Experience Manager網頁介面提供了一組豐富的數位資產管理功能，遠遠超出網路共用上的能力（搜尋、收集、中繼資料、共同作業、預覽等），而Experience Manager案頭應用程式則提供方便使用的連結，可將伺服器端DAM存放庫與案頭上的工作連結。

避免使用Experience Manager案頭應用程式，直接在Experience Manager Assets的網路共用中管理資產。 例如，請避免使用Experience Manager案頭應用程式來移動/複製多個檔案。 請改用Experience Manager Assets網頁UI，將資料夾從Finder/Explorer拖曳至網路共用，或使用Experience Manager Assets資料夾上傳功能。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
