---
title: 與 [!DNL Adobe Creative Cloud]整合的最佳實務
description: 最佳實務將Experience Manager部署與Adobe Creative Cloud整合，以簡化資產傳輸工作流程並達到最高效率。
contentOwner: AG
mini-toc-levels: 1
feature: 協作，Adobe資產連結，案頭應用程式
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 18%

---

# AEM與Creative Cloud整合最佳實務 {#aem-and-creative-cloud-integration-best-practices}

Adobe Experience Manager(AEM)Assets是數位資產管理(DAM)解決方案，可與Adobe Creative Cloud整合，協助DAM使用者與創意團隊合作，簡化內容建立程式中的共同作業。

Adobe Creative Cloud為創意團隊提供解決方案和服務生態系統，協助他們建立數位資產。 它包括案頭和移動應用程式、雲端服務（如具有案頭同步功能或網頁體驗的儲存空間），以及Adobe Stock等市場。

請閱讀以了解根據您的使用案例在案頭和企業級DAM之間挑選哪些整合，以及連線工作流程的相關最佳實務。

>[!NOTE]
>
>AEM對Creative Cloud資料夾共用現已淘汰，下文不再涵蓋。 Adobe建議使用Adobe資產連結或AEM案頭應用程式等較新功能，讓創意使用者能存取AEM中管理的資產。

## 創意人員、行銷人員和DAM使用者的共同作業需求 {#collaboration-need-of-creatives-marketers-and-dam-users}

| 需求 | 使用案例 | 相關曲面 |
|---|---|---|
| 簡化案頭創意人員的體驗 | 為創意專業人員（更廣泛而言）簡化從DAM(AEM Assets)存取資產的程式，或是讓使用案頭的使用者在原生資產建立應用程式中工作。 他們需要簡單明瞭的方式來探索、使用（開啟）、編輯和儲存對AEM的變更，以及上傳新檔案。 | Win或Mac案頭；Creative Cloud應用程式 |
| 提供來自Adobe Stock的高品質、現成可用資產 | 行銷人員可協助進行資產來源搜尋和探索，協助加速內容建立流程。 創意專業人員可直接在其創意工具中使用已核准的資產。 | AEM Assets;Adobe Stock市集；中繼資料欄位 |
| 按組織分發和共用資產 | 內部部門/當地分支機構和外部合作夥伴、分銷商和代理使用母公司共用的已核准資產。 該組織希望安全無縫地共用已建立的資產，以便更廣泛地重複使用。 | Brand Portal, Asset Share Commons |

## Adobe產品以支援協作需求 {#adobe-offerings-to-support-the-collaboration-need}

| 相關角色的價值主張 | Adobe產品 | 相關曲面 |
|---|---|---|
| 創意使用者可從AEM探索資產、開啟及使用資產、編輯和上傳對AEM的變更，以及將新檔案上傳至AEM，而無須離開Creative Cloud應用程式。 | [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator和InDesign |
| 業務使用者可簡化開啟和使用資產、編輯和上傳變更至AEM，以及從案頭環境將新檔案上傳至AEM。 他們會使用一般整合來開啟原生案頭應用程式中的任何資產類型，包括非Adobe的資產類型。 | [[!DNL Experience Manager] 桌面應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en) | AEM案頭應用程式在Win和Mac案頭上 |
| 行銷人員和商務使用者可從AEM探索、預覽、授權及儲存及管理Adobe Stock資產。 授權和儲存的資產可提供選取的Adobe Stock中繼資料，以改善控管。 | [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md) | AEM網頁介面 |

本文主要針對協作需求的前兩個方面。資產規模分配和採購作為一個使用案例被簡要提及。針對這些需求解決方案，請考慮Adobe品牌入口網站或資產共用公域。其他解決方案，例如 [AEM Brand Portal](https://helpx.adobe.com/tw/experience-manager/brand-portal/user-guide.html)，這些解決方案可以根據 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 元件、 [Link Share](share-assets.md)，使用 [](/help/assets/manage-digital-assets.md) AEM Web UI Assets建立，應根據特定需求審查。

![AEM的Creative Cloud連線：決定要使用的功能](assets/creative-connections-aem.png)

決定要使用哪種能力

### 對應使用案例和Adobe解決方案 {#mapping-of-use-cases-and-adobe-solutions}

| 使用案例 | Adobe資產連結 | AEM 桌面應用程式 | 注釋或替代方法 |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Discover — 瀏覽AEM資料夾 | 是 | AEM Web UI +案頭動作 | 瀏覽網路共用時，關閉縮圖以避免下載資產的二進位檔案。 |
| Discover — 存取AEM集合 | 是 | AEM Web UI +案頭動作 |  |
| Discover — 從AEM搜尋資產 | 是 | AEM Web UI +案頭動作 |  |
| 使用 — 開啟資產 | 是 | 是 — 適用於任何應用程式 | [從Web介面或](/help/assets/manage-digital-assets.md#previewing-assets) 從Finder開啟 |
| 使用 — 將資產從AEM放入檔案中 | 是 — 內嵌 | 是 — 連結或內嵌 | AEM案頭應用程式可讓您存取本機檔案系統上的檔案形式資產。 原生應用程式中的這些連結會以本機路徑表示。 |
| 編輯 — 開啟以進行編輯 | 是 — 結帳動作 | 是 — 開啟操作（在網路共用中） | [Aal中的簽出](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) 會依預設將資產儲存至使用者的Creative雲端儲存空間帳戶(由Creative Cloud應用程式同步)。 |
| 編輯 — 在AEM外進行中 | 是 — 使用者Creative Cloud儲存帳戶中可用的資產已同步至案頭。 | 是 |  |
| 編輯 — 上傳變更 | 是 — [簽入操作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)，帶可選注釋 | 是 |  |
| 上傳 — 單一檔案 | 是 — 上載當前活動文檔 | 是 | [透過網頁介面上傳](/help/assets/manage-digital-assets.md#uploading-assets) |
| 上傳 — 多個檔案/階層式資料夾結構 | 否 | 是 | [透過網頁介面上傳](/help/assets/manage-digital-assets.md#uploading-assets);自訂指令碼或工具 |
| Misc — 用戶和登錄 | Creative Cloud使用者登入Creative Cloud案頭應用程式後即可辨識(SSO) | AEM使用者/登入 | 這兩個解決方案的使用者會以AEM使用者配額計算。 |
| 雜項 — 網路和接入 | 需要通過網路從用戶的案頭到AEM部署的訪問 | 需要通過網路從用戶的案頭到AEM部署的訪問 | Adobe資產連結不共用網路代理環境。 |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

為支援資產散布使用案例，應考慮其他解決方案：

* [AEM Assets Brand ](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) Portal ，以取得可設定的資產附加元件以發佈資產。

* 自訂解決方案是根據[資產共用公域](https://adobe-marketing-cloud.github.io/asset-share-commons/)程式碼基底所建立。
* AEM [連結共用](/help/assets/share-assets.md)以使用連結來臨機共用資產。
* [AEM Assets ](/help/assets/manage-digital-assets.md) web介面由AEM存取控制設定所保護的外部方的區域，以及必要的IT/網路配置調整，讓這些外部使用者能存取AEM。

## 重要概念和使用案例 {#key-concepts-and-use-cases}

### 常用術語表 {#glossary-of-common-terms}

* **在製品或創意在製品 (WIP)：**&#x200B;在資產生命週期中，資產會經歷多次變更，且通常尚未準備好更廣泛地與其他團隊共用的階段。
* **創意成熟資產：**&#x200B;已準備好更廣泛地與其他團隊共用，或已獲創意團隊選取/核准，要與行銷或 LOB 團隊共用的資產。

* **資產核准：**&#x200B;針對已上傳至 DAM 的資產執行的核准程序，通常包括品牌核准、法律核准等。
* **最終資產：**&#x200B;已完成所有核准/中繼資料標記，且已準備好更廣泛地供團隊使用的資產。此類資產會儲存在 DAM 中，並提供給所有 (或所有相關的) 使用者使用。這類資產可用於行銷管道，或供創意團隊創作設計。

* **小幅度資產更新/變更：**&#x200B;數位資產的快速微幅變更。此類更新/變更通常是為了因應潤飾或微幅編輯請求、資產檢閱或核准 (例如重新定位、變更文字大小、調整飽和度/亮度、顏色等) 而進行的。
* **重大資產更新/變更：**&#x200B;需要大量工作，且有時需要較長時間才能完成的數位資產變更。其中通常包含多項變更。資產在更新時必須儲存多次。重大資產更新通常會導致資產進入 WIP 階段。
* **DAM：**&#x200B;數位資產管理。在此文件中，其意義與 AEM Experience Manager Assets 相同，除非另有特別說明。
* **創意使用者：**&#x200B;使用 Creative Cloud 應用程式和服務建立數位資產的創意專業人員。在某些情況下，創意使用者可能是可使用 Creative Cloud、但不會建立數位資產的創意團隊成員 (例如創意總監或創意團隊經理)。
* **DAM 使用者：** DAM 系統的一般使用者。視組織而異，DAM 使用者可能是行銷或非行銷使用者，例如企業營運 (LOB) 使用者、圖書管理員、銷售人員等。

### 使用AEM和Creative Cloud整合時的考量事項 {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

以下為AEM與Creative Cloud整合最佳實務的簡短摘要。 閱讀本檔案的其餘部分，以詳細了解這些內容。

* **對於在Photoshop、InDesign或Illustrator中工作的創意使用者：** Adobe Asset Link提供最佳的使用者體驗，包括對從AEM結帳的資產進行中工作的簡潔處理
* **** 為簡化從案頭存取任何一般檔案格式或應用程式的資產：使用AEM案頭應用程式
* **** 瞭解在DAM中儲存資產的原因及時機：更新將提供給組織中更廣大的團隊
* **** 請留意共用資產的數量：如果您的使用案例是資產分發，則治理和安全性可能是最重要的方面。請考慮使用大型工具 (例如品牌入口網站) 進行此作業。
* **** 瞭解資產生命週期：瞭解不同團隊在組織中如何處理資產
* **** 謹慎處理資產的頻繁儲存：Adobe Asset Link會透過PS、AI、ID為您處理。對於其他應用程式，請勿在映射/共用資料夾中執行進行中的工作，除非您需要DAM中的所有變更

### 從AEM Assets存取Adobe Stock資產 {#access-to-adobe-stock-assets-from-aem-assets}

[AEM與Adobe Stock](/help/assets/aem-assets-adobe-stock.md) 的整合可讓AEM使用者從Adobe Stock搜尋、預覽、授權及儲存資產至AEM。授權和儲存的Adobe Stock資產已選取Stock中繼資料，可用來搜尋含有額外篩選器的資產。

此整合的幾項重要要點：

* 從Adobe庫儲存存的資產儲存至AEM時，這些資產會變成一般AEM Assets，並以二進位檔儲存至AEM存放庫。 與Adobe Stock相關的某些中繼資料會儲存為AEM中的資產，否則擷取程式看起來與其他檔案相同。 例如，如果智慧標籤處於作用中狀態，則會在儲存時將標籤新增至這些資產。
* 儲存至AEM的資產是副本，而非回到Adobe Stock的連結。

**使用從Adobe Stock儲存至AEM的Creative Cloud**。此整合與Adobe資產連結無關，但Adobe資產連結會以這種方式辨識從Stock儲存的這些資產，並在Photoshop、Illustrator或InDesign的Adobe資產連結擴充功能UI中，在這些資產上顯示其他中繼資料和Stock圖示。 這些檔案可供瀏覽、開啟等使用，因為儲存至AEM時，這些檔案是一般的AEM資產。
在具有Adobe資產連結擴充功能的Creative Cloud應用程式中工作的創意使用者，除了可存取從Adobe Stock到AEM的已授權資產外，還可以使用Creative Cloud資料庫面板來搜尋、預覽和授權Adobe Stock資產。
授權並儲存至AEM的Adobe Stock資產可供存取AEM Assets部署的更多團隊使用，而透過「Creative Cloud資料庫」面板從Adobe Stock授權資產的創意工具，則預設只會在其Creative Cloud帳戶中供自己使用。

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

若要在創意與行銷/業務線(LOB)團隊之間設計有效的工作流程，並選擇最佳支援功能，請務必了解資產儲存於DAM的時間和原因。

### 資產為何儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，可讓資產輕鬆存取且可尋找。 它可確保組織或生態系統中的眾多使用者都能運用這些資產，包括合作夥伴、客戶等。

大多陣列織選擇僅儲存與下遊行銷/LOB流程相關的資產(透過AEM Sites發佈至Web管道等管道，或Adobe Experience Cloud提供的其他管道 — Marketing Cloud、Advertising Cloud，以及Analytics Cloud測量、提供給使用者/合作夥伴等)。 此外，組織會儲存DAM中可能經過審核/核准程式的資產。 這樣，DAM就能儲存大多數具有高利用機會的資產，並避免儲存閒置的資產。

儲存資產還需考慮技術和資源利用。 DAM提供儲存資產的其他相關服務，包括擷取中繼資料、版本設定、產生預覽/轉碼、管理參考以及新增存取控制資訊。 這些服務需要額外的時間和基礎架構資源。

通常，儲存所有資產和更新是不理想的。 例如，如果特定資產的更新品質不佳，且耗用過多資源，則資產可能不會儲存在DAM中。

#### 資產儲存在DAM時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對在資產生命週期的每個階段儲存資產不感興趣。 例如，在下列情況下，他們會避免儲存資產：

* 尚未完成或有待試驗的資產
* 無法通過創意/內部團隊審核週期的資產
* 與相關資產相比，團隊有更好的候選人來代表其工作給外部團隊

通常，下列類別資產會儲存在DAM中：

* 已到期且被視為可供共用的資產
* 創意團隊預先選取的資產
* 根據特定合約或協定（例如，從RAW檔案轉換的JPG檔案、從PSD原始檔案轉換的TIFF/影像），市場營銷可使用或請求的特定資產格式

#### 資產更新儲存於DAM時 {#when-updates-to-assets-are-stored-in-dam}

一般而言，DAM中只應儲存與較廣的DAM使用者集合相關的資產更新。 它可確保使用者（行銷和類似功能）只能在DAM資產時間軸中看到相關版本。

通常與資產生命週期中的主要里程碑相關的變更。 例如，創意團隊提供的初始行銷就緒資產或根據請求/檢閱的官方更新應儲存在DAM中，並加以版本控制。

創意團隊在請求變更DAM中現有資產後進行更新，供行銷團隊檢閱，這是相關更新的範例。 應將其儲存並在DAM中加以版本控制，以供進一步參考或還原為舊版。

以下是通常不相關的更新範例：

* 在資產可供行銷審核之前先上傳的舊版資產
* 在創意和行銷團隊決定資產已就緒之前，會在進行中階段經常對資產進行創意變更

### DAM的使用者存取權 {#user-access-to-dam}

AEM Assets根據使用者對AEM Assets部署的存取權限，支援兩種使用者。 企業網路（防火牆）內的使用者通常可直接存取DAM。 企業網路以外的其他使用者將無法直接存取。 使用者類型會從技術觀點決定可使用的整合。

#### 可直接存取DAM的創意使用者 {#creative-users-with-direct-access-to-dam}

內部創意團隊或已上線至內部網路的代理商/創意專業人員通常都能存取DAM例項，包括AEM登入。 可以設定AEM和網路基礎架構，以允許直接訪問外部方（通常是受信任的組織，如為客戶工作的機構），以通過網路訪問AEM，例如，通過VPN或IP允許清單。

在這種情況下，Adobe資產連結或AEM案頭應用程式可讓您輕鬆存取最終/核准的資產，並將創意資產儲存至DAM。

#### 無法存取DAM的創意使用者 {#creative-users-without-access-to-dam}

無法直接存取DAM例項的外部機構和自由工作者可能需要存取已核准的資產，或想要將其新設計新增至DAM。

使用下列策略來提供對最終/核准資產的存取權：

* 如果「資產連結」無法運作，請使用案頭應用程式。
* 使用[AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html)將資產安全地分發給外部合作夥伴
* 根據[Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)使用發佈和來源補充入口網站的自訂實作
* 使用AEM中設定的存取控制和必要的網路基礎架構（例如，允許的VPN和IP清單），讓外部方可存取您DAM中的專用內容區域。 他們可以使用AEM Web UI來取得資產，並將新內容上傳至DAM。

#### 從AEM處理資產的進行中 {#work-in-progress-on-assets-from-aem}

如本檔案所述，建議您對資產執行重大更新，有時稱為進行中的工作，而不要將所有儲存至本機檔案的編輯內容也隨著變更上傳至AEM。 這可加快案頭用戶的工作速度、限制所使用的網路頻寬，並保持資產時間清晰，並將重點放在受控的重大更新上。

Adobe資產連結對此使用案例提供良好支援：

* 當Photoshop、InDesign或Illustrator中的使用者想要編輯檔案時，會對指定資產執行結帳作業
* 資產會在背景下載，放入透過Creative Cloud案頭應用程式同步至磁碟的使用者Creative Cloud帳戶中，並在資產的AEM中切換簽出標幟，將編輯衝突降至最低
* 之後，使用者會在同步位置儲存於本機的檔案中操作，並可以繼續操作並儲存必要的變更，以執行任何所需頻率
* 此外，由於資產位於Creative Cloud帳戶中，因此也可在使用者可能擁有的其他裝置上使用(例如，可以在專用的Creative Cloud行動應用程式中開啟或編輯)，並且可與其他Creative Cloud使用者共用以進行共同作業。
* 創意使用者完成變更後，即可在其Creative Cloud應用程式中對該檔案執行簽入操作，並附上選用備注。 AEM中對應的資產會經過版本控制，並以新的二進位檔更新為。 AEM使用者（如行銷人員或LOB使用者）可透過AEM資產時間軸UI存取重大資產變更或里程碑。

AEM案頭應用程式為原生應用程式中開啟的資產提供網路共用。 依預設，在短暫後，所有在本機完成的變更都會自動上傳至AEM。 有了這種配置，在進行中階段頻繁保存的操作都將上載到AEM並進行版本控制，從而產生大量網路流量和潛在的可擴充性挑戰 — 更不用說AEM中不必要的版本了。

此處建議的方法是使用AEM案頭應用程式中的選項，透過應用程式資產狀態UI中的上傳變更動作，手動關閉自動更新，並將變更上傳至AEM。

#### 大量上傳至DAM {#bulk-upload-to-dam}

在某些情況下，您可能需要同時將大量檔案上傳至DAM，例如：

* 上傳像片或大型專案的結果
* 上傳由創意廣告公司提供的資產
* 如果選取是在DAM外完成，則從較大的集合上傳選取的資產

請注意，此說明指的是以正常的案頭使用者工作流程方式，在運作上（例如每週或每張像片）上傳檔案。 此處未涵蓋大型資產遷移。

您可善用下列上傳功能：

* 若要大量上傳大型/階層式資料夾，請使用提供[資料夾上傳](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload)功能的AEM案頭應用程式。 您也可以上傳階層式資料夾結構。 資產會在背景上傳，因此不會系結至網頁瀏覽器工作階段
* 若要從單一資料夾上傳幾個檔案，請直接將檔案拖曳至Web介面，或使用AEM Assets Web介面中的「建立」選項。
* 您也可以使用自訂上傳程式，視您的業務需求而定。

#### 直接從案頭管理數位資產 {#managing-digital-assets-directly-from-desktop}

如果您使用網路檔案共用來管理數位資產，只要使用AEM案頭應用程式對應的網路共用，就會被視為方便的替代項目。 從網路檔案共用轉換時，AEM網頁介面提供一組豐富的數位資產管理功能，遠超網路共用的功能（搜尋、集合、中繼資料、共同作業、預覽等），而AEM案頭應用程式則提供便利的連結，可將伺服器端的DAM存放庫與案頭上的工作連結。

避免使用AEM案頭應用程式直接在AEM Assets的網路共用中管理資產。 例如，請避免使用AEM案頭應用程式來移動/複製多個檔案。 請改為使用AEM Assets Web UI將資料夾從Finder/Explorer拖曳至網路共用，或使用AEM Assets資料夾上傳功能。

<!-- 
#### Asset migration {#asset-migration}

To plan and execute asset migrations from existing system to a new system or migration of large volume of assets stored on servers, see the [Migration Guide](/help/assets/assets-migration-guide.md). AEM desktop app and AEM to Creative Cloud integrations do not support such migrations. Due to the large volumes of assets to be ingested, and additional requirements around metadata mapping, transformation, and ingestion, migrations should be handled using different tools and approaches.
-->
