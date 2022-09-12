---
title: 企業開發團隊設定
description: 了解如何設定和擴充您的企業開發團隊，並了解AEM as a Cloud Service如何支援您的開發流程。
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: a31c3693c9b2af9bd7f9d7f1f6fb0a61a4411df0
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 0%

---

# AEMas a Cloud Service的企業開發團隊設定 {#enterprise-setup}

了解如何設定和擴充您的企業開發團隊，並了解AEM as a Cloud Service如何支援您的開發流程。

## 簡介 {#introduction}

為了透過企業開發設定支援客戶，AEM as a Cloud Service與Cloud Manager及其專門建立的完全整合， [確信的CI/CD管道。](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 這些管道和服務是根據最佳做法構建的，確保做到徹底 [測試和最高的程式碼品質。](/help/implementing/cloud-manager/code-quality-testing.md)

## Cloud Manager在企業團隊開發設定中的支援 {#cloud-manager}

為確保快速上線，Cloud Manager提供立即開始開發數位體驗所需的一切，包括Git存放庫，以儲存自訂內容，然後由Cloud Manager建立、驗證和部署。

使用Cloud Manager，開發團隊可以經常致力於提交變更，而不需依賴Adobe人員。

Cloud Manager提供三種類型的環境。

* 開發
* 分段
* 生產

可使用非生產管道將程式碼部署至開發環境。 對於測試環境和生產環境，生產管道會使用 [質量門](/help/implementing/cloud-manager/custom-code-quality-rules.md) 以驗證應用程式程式碼和設定變更。

生產管道會先將程式碼和設定部署至測試環境，測試應用程式，最後部署至生產環境。

隨時更新的Cloud ServiceSDK具有最新的AEMas a Cloud Service改善，可讓開發人員的本機硬體直接用於本機開發。 這使得可以以非常低的週轉時間實現快速開發。 因此，開發人員可以停留在熟悉的本機環境中，從多種開發工具中進行選擇，並在發現適合時推送至開發環境或生產環境。

Cloud Manager支援靈活的多團隊設定，可根據企業需求進行調整。 為確保有多個團隊進行穩定部署，同時避免某個團隊影響所有團隊的生產，Cloud Manager的確定管道一律會一起驗證並測試所有團隊的程式碼。

## 真實世界範例 {#real-world-example}

每個企業都有不同的需求，包括不同的團隊設定、流程和開發工作流程。 以下說明的設定供Adobe用於在AEMas a Cloud Service上提供體驗的數個專案。

例如，Adobe Creative Cloud應用程式(例如Adobe Photoshop或Adobe Illustrator)包含教學課程、範例和指南等內容資源，供一般使用者使用。 用戶端應用程式會以無頭方式使用AEMas a Cloud Service、對AEM Cloud發佈層級進行API呼叫以擷取結構化內容（如JSON資料流），並運用 [AEMas a Cloud Service中的內容傳遞網路(CDN)](/help/implementing/dispatcher/cdn.md#content-delivery) 以最佳效能為結構化和非結構化內容提供服務。

本專案的參與團隊會遵循下列程式。

每個團隊都會使用自己的開發工作流程，並有個別的Git存放庫。 額外的共用Git存放庫用於上線專案。 此Git存放庫包含Cloud Manager的Git存放庫根結構，包括共用Dispatcher設定。

若要上線新專案，須將清單列在共用Git存放庫根目錄的reactor Maven專案檔案中。 對於Dispatcher設定，會在Dispatcher專案內建立新的設定檔案。 然後，主要Dispatcher設定便會包含此檔案。 每個團隊都負責各自的Dispatcher設定檔案。 共用Git存放庫很少有變更，且通常只有在新專案上線時才需要變更。 主要工作由各專案團隊在各自的Git存放庫中完成。

![工作流程圖](/help/implementing/cloud-manager/assets/team-setup1.png)

每個的Git存放庫都使用 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 並遵循設定AEM專案的最佳實務。 唯一的例外是在共用Git存放庫中完成的Dispatcher設定，如上所述。

每個團隊依照git流程模型，使用兩個+ N分支的簡化git工作流程：

* 穩定的發行分支包含生產代碼。

* 開發分支包含最新開發。

* 為每個特徵建立新分支。

開發在特徵分支中完成。 特徵成熟後，將合併到開發分支中。 已完成和已驗證的功能會從開發分支中挑選，並合併到穩定分支中。

所有變更都是透過提取請求(PR)完成。 每個PR都會由品質閘門自動驗證。 聲納用於檢查程式碼的品質，並執行一組測試套裝，以確保新程式碼不會引入任何回歸。

Cloud Manager的Git存放庫中的設定有兩個分支。

* 穩定的發行分支包含所有團隊的生產代碼。
* 開發分支包含所有團隊的開發程式碼。

開發或穩定分支中推送至團隊的Git存放庫時，都會觸發 [GitHub動作。](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code)

所有項目都遵循穩定分支的相同設定。 推送至專案的穩定分支會自動推送至Cloud Manager的Git存放庫中的穩定分支。 Cloud Manager中的生產管道設定為透過推送至穩定分支而觸發。 因此，生產管道會由任何團隊的每個推送執行至穩定的分支，而且，如果所有品質閘道都通過，生產部署會更新。

![推播圖表](/help/implementing/cloud-manager/assets/team-setup2.png)

推送至開發分支的處理方式不同。 推送至團隊Git存放庫中的開發人員分支時，也會觸發GitHub動作，且程式碼會自動推送至Cloud Manager Git存放庫的開發分支，而程式碼推送不會自動觸發非生產管道。 這會由呼叫Cloud Manager的API觸發。

執行生產管道包括透過提供的品質閘道檢查所有團隊的程式碼。 將程式碼部署至預備後，會執行測試和稽核，以確保一切皆如預期般運作。 一旦所有門都通過，更改就可以在生產環境中進行，而不會發生任何中斷或停機。

就地方發展而言， [AEM適用的SDKas a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing) 中所有規則的URL區段。 SDK可讓您設定本機作者、發佈和調度程式。 這可讓離線開發及快速週轉時間。 有時只會使用製作環境進行開發，但快速設定Dispatcher和發佈環境，可在將一切都推送至Git存放庫之前，先在本機測試。

每個團隊的成員通常會從的共用Git結帳程式碼，以及其專案程式碼。 由於專案獨立，因此不需要結帳其他專案。

![本機結帳和SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

這個現實世界的設定可作為藍圖，然後根據企業的需求進行自訂。 Git的彈性分支和合併概念可提供上述工作流程的各種變數，並根據每個團隊的需求加以自訂。 AEM as a Cloud Service支援所有這些變異，但不會犧牲確信的Cloud Manager管道的核心值。

>[!TIP]
>
>請參閱該文檔 [使用多個來源Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html#managing-code) 以深入了解此設定。

### 多團隊設定的考量事項 {#considerations}

透過Cloud Manager的git存放庫和生產管道，完整的生產程式碼一律會在所有品質入口執行，並將其視為一個部署單位。 這樣，生產系統就始終處於正常運行狀態，不會中斷或停機。

相反，如果沒有這樣的系統，因為每個團隊都可以單獨部署，所以來自單個團隊的更新可能會導致生產穩定性問題。 此外，它需要協調和計畫內停機，才能推出更新。 隨著團隊人數的增加，協調工作將變得複雜得多，而且很快無法管理。

如果在質量門中檢測到問題，則不影響生產，並且可以檢測並修復問題，而不需要Adobe人員介入。 如果不進行Cloud Service，而且不總是要測試整個部署，部分部署可能會導致停機，需要請求回滾，甚至需要從備份中完全恢復。 部分測試也可能導致其他問題，在事實再次發生後，這些問題需要Adobe人員的協調和支援。

>[!TIP]
>
>對於任何多團隊設定，定義治理模式和一套所有團隊都必須遵循的標準至關重要。 多團隊設定的上一個藍圖可讓更多團隊擴充，以供您作為起點。
