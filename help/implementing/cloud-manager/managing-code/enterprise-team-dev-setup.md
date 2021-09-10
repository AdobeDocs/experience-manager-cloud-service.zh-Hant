---
title: 企業團隊開發設定 — Cloud Services
description: 請依照本頁面了解有關企業團隊開發設定的詳細資訊
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: 3cdee254eebcf45762feff8fe081b006a803ef1b
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 0%

---

# AEM as aCloud Service的企業團隊開發設定 {#enterprise-setup}

## 簡介 {#introduction}

AEM as Cloud Service是雲端原生產品，提供AEM as a service，旨在透過10多年依其特定需求，為企業團隊提供企業軟體而獲益。 它將AEM推進雲端原生世界，提供隨時開啟、隨時最新、永遠安全且隨時可擴充的新值，同時仍保留AEM作為可自訂平台提供給客戶的主要價值主張，並讓企業級團隊整合在其開發和傳遞程式中。

為了透過企業開發設定支援客戶，AEM as aCloud Service與Cloud Manager及其專門建立的確信CI/CD管道完全整合，這些管道具備最佳實務，並從多年的企業級開發與部署經驗中汲取經驗，確保全面測試和最高的程式碼品質，以提供卓越的體驗。

## Cloud Manager在企業團隊開發設定中的支援 {#cloud-manager}

為確保客戶快速上線，Cloud Manager提供立即開始開發體驗所需的一切，包括Git存放庫，以儲存自訂內容，然後由Cloud Manager建立、驗證和部署。
使用Cloud Manager，開發團隊可以經常致力於提交變更，而不需依賴Adobe人員。

Cloud Manager提供三種環境類型：

* 開發
* 分段
* 生產

可使用非生產管道將程式碼部署至開發環境。 對於Stage和Production（始終一起執行，從而確保在生產部署前進行驗證，作為最佳做法），生產管道使用質量門來驗證應用程式代碼和配置更改。

生產管道會先將程式碼和設定部署至測試環境，測試應用程式，最後部署至生產環境。
隨時更新的Cloud ServiceSDK可改善最新的Cloud Service，以便直接使用開發人員的本機硬體進行本機開發。 這使得可以以非常低的週轉時間實現快速開發。 因此，開發人員可以停留在熟悉的本機環境中，從多種開發工具中進行選擇，並在發現適合時推送至開發環境或生產環境。

Cloud Manager支援靈活的多團隊設定，可根據企業需求進行調整。 這適用於Cloud Service和AMS。 為了確保部署多個團隊並避免一個團隊影響所有團隊的生產， Cloud Managers確信管道一律會一起驗證並測試所有團隊的程式碼。


## 真實世界範例 {#real-world-example}

每個企業都有不同的需求，包括不同的團隊設定、流程和開發工作流程。 以下所述的設定供Adobe用於以AEM為Cloud Service來提供體驗的數個專案。

例如，Adobe Creative Cloud應用程式(例如Adobe Photoshop或Adobe Illustrator)包含教學課程、範例和指南等內容資源，供一般使用者使用。 用戶端應用程式會以&#x200B;*headless*&#x200B;方式使用AEM作為Cloud Service，方法是向AEM Cloud發佈層發出API呼叫，將結構化內容擷取為JSON資料流，並運用AEM中的[內容傳送網路(CDN)作為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery)，以最佳效能同時提供結構化和非結構化內容。

為本專案貢獻內容的團隊會遵循以下所述的程式。

>[!NOTE]
>請參閱[使用多個來源Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html#managing-code)以深入了解設定。

每個團隊都使用其專屬的開發工作流程，並有個別的Git存放庫。 額外的共用Git存放庫用於上線專案。 此Git存放庫包含Cloud Manager的Git存放庫根結構，包括共用Dispatcher設定。 若要上線新專案，須將清單列在共用Git存放庫根目錄的reactor Maven專案檔案中。 對於Dispatcher設定，會在Dispatcher專案內建立新的設定檔案。 然後，主要Dispatcher設定便會包含此檔案。 每個團隊都負責各自的Dispatcher設定檔案。 共用Git存放庫很少有變更，且通常只有在新專案上線時才需要變更。 主要工作由各專案團隊在各自的Git存放庫中完成。

![](/help/implementing/cloud-manager/assets/team-setup1.png)

每個團隊的Git存放庫皆已使用AEM Maven原型設定，因此會遵循設定AEM專案的最佳實務。 唯一的例外是處理在共用Git存放庫中完成的Dispatcher設定，如上所述。
每個團隊依照Git流程模型，使用兩個+ N分支的簡化Git工作流程：

* 穩定的發行分支包含生產代碼

* 開發分支包含最新開發

* 為每個特徵建立新分支


開發在特徵分支中完成，當特徵成熟時，它將合併到開發分支中。 已完成和已驗證的功能會從開發分支中挑選，並合併到穩定分支中。 所有變更都是透過提取請求(PR)完成。 每個PR都會由品質閘門自動驗證。 聲納用於檢查程式碼的品質，並執行一組測試套裝，以確保新程式碼不會引入任何回歸。

Cloud Manager的Git存放庫中的設定有兩個分支：

* *穩定的發行分支*，包含所有團隊的生產代碼
* *開發分支*，包含所有團隊的開發代碼

在開發或穩定分支中推送至團隊的git存放庫時，每次都會觸發[github動作](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html?lang=en#managing-code)。 所有項目都遵循穩定分支的相同設定。 推送至專案的穩定分支會自動推送至Cloud Manager的Git存放庫中的穩定分支。 Cloud Manager中的生產管道設定為透過推送至穩定分支而觸發。 因此，生產管道會由任何團隊的每個推送執行至穩定的分支，而且，如果所有品質閘道都通過，生產部署會更新。

![](/help/implementing/cloud-manager/assets/team-setup2.png)

推送至開發分支的處理方式不同。 雖然推送至團隊Git存放庫中的開發人員分支也會觸發github動作，且程式碼會自動推送至Cloud Manager Git存放庫的開發分支，但程式碼推送不會自動觸發非生產管道。 由呼叫Cloud Manager的api觸發。
執行生產管道包括透過提供的品質閘道檢查所有團隊的程式碼。 將程式碼部署至預備後，會執行測試和稽核，以確保一切皆如預期般運作。 一旦所有門都通過，更改就可以在生產環境中進行，而不會發生任何中斷或停機。
針對本機開發，會使用[AEM as aCloud Service的SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)。 SDK可讓您設定本機作者、發佈和調度程式。 這可讓離線開發及快速週轉時間。 有時只有作者用於開發，但快速設定Dispatcher和發佈可讓您在本機測試所有內容，再將內容推送至Git存放庫。 每個團隊的成員通常會從的共用Git結帳程式碼，以及其專案程式碼。 由於專案獨立，因此不需要結帳其他專案。

![](/help/implementing/cloud-manager/assets/team-setup3.png)

這個現實世界的設定可作為藍圖，然後根據企業的需求進行自訂。 Git的彈性分支和合併概念可提供上述工作流程的各種變數，並根據每個團隊的需求加以自訂。 AEM as aCloud Service支援所有這些變數，但不會犧牲確信的Cloud Manager管道的核心值。

### 多團隊設定的考量事項 {#considerations}

>[!NOTE]
>對於任何多個團隊的設定，定義治理模型和所有團隊都必須遵循的一組標準至關重要。 以上概述的多團隊設定藍圖可讓更多團隊進行擴充，而您可以使用此藍圖作為起點。

有了Cloud Manager的git存放庫和生產管道，完整的生產程式碼一律會在所有品質入口執行，並將其視為一個部署單位。 這樣，生產系統將&#x200B;*始終保持在*上，不會中斷或停機。
相反，如果沒有這樣的系統，因為每個團隊都可以單獨部署，所以來自單個團隊的更新可能會導致生產穩定性問題。 此外，它需要協調和計畫內停機，才能推出更新。 隨著團隊人數的增加，協調工作將變得複雜得多，而且很快無法管理。

如果在質量門中檢測到問題，則不影響生產，並且可以檢測並修復問題，而不需要Adobe人員介入。 如果不進行Cloud Service，而且不總是要測試整個部署，部分部署可能會導致停機，需要請求回滾，甚至需要從備份中完全恢復。 部分測試也可能導致其他問題，在事實再次發生後，這些問題需要Adobe人員的協調和支援。
