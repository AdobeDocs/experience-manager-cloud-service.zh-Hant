---
title: 企業開發團隊設定
description: 了解如何設定和擴展您的企業開發團隊，並了解 AEM as a Cloud Service 如何支援您的開發流程。
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 40%

---

# AEM as a Cloud Service的企業開發團隊設定 {#enterprise-setup}

瞭解如何設定和擴展您的企業開發團隊，並瞭解AEM (Adobe Experience Manager) as a Cloud Service如何支援您的開發流程。

## 簡介 {#introduction}

為了支援具有企業開發設定的客戶，AEM as a Cloud Service 與 Cloud Manager 及其專門建置的[教條式 CI/CD 管道完全整合](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。這些管道和服務根據最佳實務建置，以確保整體的[測試和最高的程式碼品質](/help/implementing/cloud-manager/code-quality-testing.md)。

## Cloud Manager在企業團隊開發設定中的支援 {#cloud-manager}

為確保快速入門，Cloud Manager提供了立即開始開發數位體驗所需的一切，包括用於儲存自訂的Git存放庫，然後由Cloud Manager建置、驗證和部署。

使用 Cloud Manager，開發團隊可以在不依賴 Adobe 人員的情況下頻繁提交變更。

Cloud Manager 中提供了三種類型的環境。

* 開發
* 測試
* 生產

可以使用非生產管道將程式碼部署到開發環境。測試和生產環境總是一起執行，從而確保在生產部署之前進行驗證作為最佳實務，生產管道使用[品質門檻](/help/implementing/cloud-manager/custom-code-quality-rules.md)來驗證應用計劃程式碼和設定變更。

生產管道會先將程式碼和設定部署到測試環境、測試應用計劃，最後部署到生產環境。

Cloud Service SDK一律使用最新的AEM as a Cloud Service改良功能進行更新，允許直接使用開發人員的本機硬體進行本機開發。 此方法可在極短的返回時間內實現快速開發。 因此，開發人員可以留在他們熟悉的本機環境中，並從各種開發工具中進行選擇，以在他們認為合適的時候推動開發環境或生產。

Cloud Manager支援靈活的多團隊設定，可以根據企業的需求進行調整。 為了確保跨多個團隊的穩定部署，Cloud Manager教條式管道一起驗證和測試來自所有團隊的計畫碼。 此方法有助於防止一個團隊的變更影響所有團隊的生產情況。

## 真實世界的範例 {#real-world-example}

每個企業都有不同的需求，包括不同的團隊設定、流程和開發工作流程。Adobe 將下述設定用於在 AEM as a Cloud Service 之上提供體驗的多個專案。

例如，Adobe Photoshop 或 Adobe Illustrator 等 Adobe Creative Cloud 應用程式包括可供一般使用者使用的教學課程、範例和指南等內容資源。使用者端應用程式會以Headless方式使用AEM as a Cloud Service的內容。 他們對AEM雲端發佈層進行API呼叫，以將結構化內容擷取為JSON資料流。 此外，AEM as a Cloud Service[中的](/help/implementing/dispatcher/cdn.md#content-delivery)內容傳遞網路(CDN)是用來以最佳效能提供結構化和非結構化內容。

為本專案貢獻內容的團隊應遵循以下流程。

每個團隊都使用自己的開發工作流程，並擁有單獨的Git存放庫。 額外的共用Git存放庫用於入門專案。 此Git存放庫包含Cloud Manager的Git存放庫的根結構，包括共用的Dispatcher設定。

加入新專案需要在共用Git存放庫根目錄下的反應器Maven專案檔案中列出。 針對Dispatcher設定，會在Dispatcher專案中建立新的設定檔案。 主要Dispatcher設定接著會包含此檔案。 每個團隊負責自己的Dispatcher設定檔。 共用Git存放庫很少會有變更，通常只有在新專案上線時才需要變更。 主要工作由每個專案團隊在自己的Git存放庫中完成。

![工作流程圖](/help/implementing/cloud-manager/assets/team-setup1.png)

各個Git存放庫都使用[AEM專案原型](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/developing/archetype/overview)設定，因此遵循設定AEM專案的最佳實務。 唯一的例外是Dispatcher設定，此設定是在共用Git存放庫中完成，如上所述。

每個團隊都會使用簡化的Git工作流程，其中包含兩個+ N分支，遵循Git流程模型：

* 穩定發行分支包含生產程式碼。

* 開發分支包含最新的開發。

* 對於每個功能，都會建立一個新分支。

開發是在功能分支中完成的。當功能成熟時，它會合併到開發分支中。 從開發分支中挑選完成和驗證的功能並合併到穩定分支中。

所有變更均透過PR （提取請求）完成。 品質門檻會自動驗證每個PR。 Sonar 用於對程式碼進行品質檢查，並執行一組測試套件以確保新程式碼不會引入任何迴歸。

Cloud Manager的Git存放庫中的設定有兩個分支。

* 穩定發行分支包含自所有團隊的生產程式碼。
* 開發分支包含來自所有團隊的開發程式碼。

在開發或穩定分支中，每次推送到團隊的Git存放庫都會觸發[GitHub動作](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code)。

所有專案都遵循相同的穩定分支設定。推送到專案的穩定分支會自動推送到Cloud Manager的Git存放庫中的穩定分支。 推送至穩定分支會觸發Cloud Manager中的生產管道。 任何團隊每次推送到穩定分支都會觸發生產管道。 如果所有品質門檻都通過，生產部署則會更新。

![推送圖](/help/implementing/cloud-manager/assets/team-setup2.png)

推送到開發分支的處理方式不同。推送到團隊Git存放庫中的開發人員分支也會觸發GitHub動作。 這個動作會自動將程式碼推送到Cloud Manager的Git存放庫中的開發分支。 不過，此程式碼推送不會自動觸發非生產管道。 對Cloud Manager的API的呼叫會觸發它。

執行生產管道包括透過提供的品質門檻檢查所有團隊的程式碼。將程式碼部署到階段後，就會執行測試和稽核，讓一切都如預期般運作。 透過了所有門檻後，這些變更就會在沒有任何中斷或停機的情況下推廣到生產環境。

對於本機開發，使用[適用於 AEM as a Cloud Service的 SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing)。SDK可設定本機作者、發佈和Dispatcher。 此工作流程可啟用離線開發和快速返回時間。 有時只使用作者環境進行開發，但快速設定Dispatcher和發佈環境允許在推送至Git存放庫之前在本機測試所有內容。

每個團隊的成員通常會從共用的Git中籤出程式碼，以供他們自己的專案程式碼使用。 不需要簽出其他專案，因為這些專案是獨立的。

![本機簽出和 SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

這種現實世界的設定可以作為藍圖，然後根據企業的需求進行自訂。Git靈活的分支和合併概念能容許上述工作流程的變化，並根據每個團隊的需求進行自訂。 AEM as a Cloud Service 支援這些變化，而不會犧牲教條式 Cloud Manager 管道的核心價值。

>[!TIP]
>
>請參閱[使用多個Source Git存放庫](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-manager/content/managing-code/multiple-git-repos#managing-code)以深入瞭解此設定。

### 多團隊設定的考量事項 {#considerations}

有了Cloud Manager的Git存放庫和生產管道，完整的生產計畫碼一律會通過所有品質門檻，並將其視為一個部署單位。 這樣，生產系統一律處於執行狀態而不會中斷或停機。

相反地，如果沒有這樣的系統，因為每個團隊都可以單獨部署，所以單一團隊的更新可能會導致生產穩定性問題。 此外，它需要協調和規劃停機時間來推出更新。隨著團隊數量增加，協調工作將變得更加複雜且很快會變得難以管理。

如果在品質門檻中偵測到問題則不會影響生產，且無需 Adobe 人員介入即可偵測和修復問題。如果沒有 Cloud Service 且並未一直測試整個部署，部分部署可能會造成中斷而必須要求復原或甚至從備份中完全還原。部分測試還會導致其他問題，這些問題必須在稍後解決，再次需要Adobe人員的協調和支援。

>[!TIP]
>
>對於任何多團隊設定，定義治理模型和所有團隊都必須遵循的一組標準至關重要。 之前的多團隊設定藍圖允許跨大量團隊進行擴展，您可以將其作為起點。
