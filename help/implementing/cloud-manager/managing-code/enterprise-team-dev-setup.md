---
title: 企業開發團隊設定
description: 了解如何設定和擴展您的企業開發團隊，並了解 AEM as a Cloud Service 如何支援您的開發流程。
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: a31c3693c9b2af9bd7f9d7f1f6fb0a61a4411df0
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 100%

---

# AEM as a Cloud Service 的企業開發團隊設定 {#enterprise-setup}

了解如何設定和擴展您的企業開發團隊，並了解 AEM as a Cloud Service 如何支援您的開發流程。

## 簡介 {#introduction}

為了支援具有企業開發設定的客戶，AEM as a Cloud Service 與 Cloud Manager 及其專門建置的[教條式 CI/CD 管道完全整合。](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)這些管道和服務根據最佳實務建置，以確保整體的[ 測試和最高的計劃碼品質。](/help/implementing/cloud-manager/code-quality-testing.md)

## 在企業團隊開發設定中 Cloud Manager 的支援 {#cloud-manager}

為確保快速入門，Cloud Manager 提供了立即開始開發數位體驗所需的一切，包括用於儲存自訂的 Git 存放庫，然後由 Cloud Manager 建置、驗證和部署。

使用 Cloud Manager，開發團隊可以在不依賴 Adobe 人員的情況下頻繁提交變更。

Cloud Manager 中提供了三種類型的環境。

* 開發
* 測試
* 生產

可以使用非生產管道將計劃碼部署到開發環境。測試和生產環境總是一起執行，從而確保在生產部署之前進行驗證作為最佳實務，生產管道使用[品質門檻](/help/implementing/cloud-manager/custom-code-quality-rules.md)來驗證應用計劃計劃碼和設定變更。

生產管道會先將計劃碼和設定部署到測試環境、測試應用計劃，最後部署到生產環境。

雲端服務 SDK 一律使用最新的 AEM as a Cloud Service 改善進行更新，允許直接利用開發人員的本機硬體進行本機開發。這可以在極短的返回時間內實現快速開發。因此，開發人員可以留在他們熟悉的本機環境中，並從各種開發工具中進行選擇，以在他們認為合適的時候推動開發環境或生產。

Cloud Manager 支援靈活的多團隊設定，可以根據企業的需求進行調整。為了確保多個團隊的穩定部署，同時避免一個團隊影響所有團隊的生產情況，Cloud Manager 教條式管道總是一起驗證和測試來自所有團隊的計劃碼。

## 真實世界的範例 {#real-world-example}

每個企業都有不同的需求，包括不同的團隊設定、流程和開發工作流程。Adobe 將下述設定用於在 AEM as a Cloud Service 之上提供體驗的多個專案。

例如，Adobe Photoshop 或 Adobe Illustrator 等 Adobe Creative Cloud 應用計劃包括可供一般使用者使用的教學課程、範例和指南等內容資源。此內容由使用 AEM as a Cloud Service 的用戶端應用計劃以無頭方式使用，透過對 AEM 雲端發佈層進行 API 呼叫以將結構化內容擷取為 JSON 串流，並利用 [AEM as a Cloud Service 中的內容交付網路 (CDN)](/help/implementing/dispatcher/cdn.md#content-delivery)，以最佳效能提供結構化和非結構化內容。

為本專案貢獻內容的團隊應遵循以下流程。

每個團隊都使用自己的開發工作流程並擁有單獨的 Git 存放庫。額外的共用 Git 存放庫用於入門專案。此 Git 存放庫包含 Cloud Manager 之 Git 存放庫的根結構，包括共用 Dispatcher 設定。

加入新專案需要在共用 Git 存放庫根目錄下的反應器 Maven 專案檔案中列出。對於 Dispatcher 設定，在 Dispatcher 專案中建立一個新的設定檔。然後此檔案會包含在主要 Dispatcher 設定中。每個團隊負責自己的 Dispatcher 設定檔。並不常對共用 Git 存放庫進行變更，通常僅在新專案入門時才需要。主要工作由每個專案團隊在自己的 Git 存放庫中完成。

![工作流程圖](/help/implementing/cloud-manager/assets/team-setup1.png)

各個 Git 存放庫都使用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)，因此遵循設定 AEM 專案的最佳實務。唯一的例外是在共用 Git 存放庫中完成的 Dispatcher 設定 (如上所述)。

每個團隊都會使用簡化的 Git 工作流程，其中包含兩個 + N 分支，遵循 Git 流程模型：

* 穩定發行分支包含生產計劃碼。

* 開發分支包含最新的開發。

* 對於每個功能，都會建立一個新分支。

開發是在功能分支中完成的。當功能成熟時，它會合併到開發分支中。從開發分支中挑選完成和驗證的功能並合併到穩定分支中。

所有變更都是透過提取要求 (PR) 完成的。每個 PR 都由品質門檻自動驗證。Sonar 用於對計劃碼進行品質檢查，並執行一組測試套件以確保新計劃碼不會引入任何迴歸。

Cloud Manager 的 Git 存放庫中的設定有兩個分支。

* 穩定發行分支包含自所有團隊的生產計劃碼。
* 開發分支包含來自所有團隊的開發計劃碼。

在開發或穩定分支中，每次推送到團隊的 Git 存放庫都會觸發 [GitHub 動作。](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code)

所有專案都遵循相同的穩定分支設定。推送到專案的穩定分支會自動推送到 Cloud Manager Git 存放庫中的穩定分支。Cloud Manager 中的生產管道設定為透過推送到穩定分支來觸發。因此，生產管道由任何團隊每次推送到穩定分支來執行，如果所有品質門檻都透過，生產部署就會更新。

![推送圖](/help/implementing/cloud-manager/assets/team-setup2.png)

推送到開發分支的處理方式不同。雖然推送到團隊 Git 存放庫中的開發人員分支也會觸發 GitHub 動作，且計劃碼會自動推送到 Cloud Manager Git 存放庫中的開發分支，但計劃碼推送不會自動觸發非生產管道。它由呼叫 Cloud Manager 的 API 觸發。

執行生產管道包括透過提供的品質門檻檢查所有團隊的計劃碼。將計劃碼部署到階段後，將執行測試和稽核以確保一切如期運作。透過了所有的門檻後，這些變更就會在沒有任何中斷或停機的情況下推廣到生產中。

對於本機開發，使用[適用於 AEM as a Cloud Service的 SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing)。SDK 可設定本機作者、發佈和 Dispatcher。這讓離線開發和快速返回時間有可能實現。有時只使用作者環境進行開發，但快速設定 Dispatcher 和發佈環境允許在推送至 Git 存放庫之前在本機測試所有內容。

每個團隊的成員通常會從共用的 Git 中簽出計劃碼以及他們自己的專案計劃碼。由於專案是獨立的，因此無需簽出其他專案。

![本機簽出和 SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

這種現實世界的設定可以作為藍圖，然後根據企業的需求進行自訂。Git 靈活的分支和合併概念能容許上述工作流程的變化，並根據每個團隊的需求進行自訂。AEM as a Cloud Service 支援這些變化，而不會犧牲教條式 Cloud Manager 管道的核心價值。

>[!TIP]
>
>若想了解此設定的更多資訊，請參閱文件：[使用多來源 Git 存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html?lang=zh-Hant#managing-code)。

### 多團隊設定的注意事項 {#considerations}

藉由 Cloud Manager 的 Git 存放庫和生產管道，完整的生產計劃碼一律透過所有品質門檻執行，並將其視為一個部署單位。這樣，生產系統一律處於執行狀態而不會中斷或停機。

相反，如果沒有這樣的系統，因為每個團隊都可以單獨部署，所以單個團隊的更新可能會導致生產穩定性問題。此外，它需要協調和規劃停機時間來推出更新。隨著團隊數量增加，協調工作將變得更加複雜且很快會變得難以管理。

如果在品質門檻中偵測到問題則不會影響生產，且無需 Adobe 人員介入即可偵測和修復問題。如果沒有 Cloud Service 且沒有總是測試整個部署，部分部署可能會造成中斷，需要要求復原甚至從備份中完全還原。部分測試還可能導致其他問題，而這些問題需要在事後由 Adobe 人員協調和支援來解決。

>[!TIP]
>
>對於任何多團隊設定，定義治理模型和所有團隊都必須遵循的一組標準至關重要。之前的多團隊設定藍圖允許跨大量團隊進行擴展，您可以將其作為起點。
