---
title: 企業開發團隊設定
description: 瞭解如何設定和擴展您的企業開發團隊，並瞭解AEMas a Cloud Service如何支援您的開發流程。
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: a31c3693c9b2af9bd7f9d7f1f6fb0a61a4411df0
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 0%

---

# 針對AEMas a Cloud Service的企業開發團隊設定 {#enterprise-setup}

瞭解如何設定和擴展您的企業開發團隊，並瞭解AEMas a Cloud Service如何支援您的開發流程。

## 簡介 {#introduction}

為支援具有企業開發設定的客AEM戶，as a Cloud Service與Cloud Manager及其專門構建的產品完全整合， [有意見的CI/CD管道。](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 這些管道和服務是基於最佳做法構建的，確保徹底 [測試和最高代碼質量。](/help/implementing/cloud-manager/code-quality-testing.md)

## 雲管理器在企業團隊開發設定中的支援 {#cloud-manager}

為確保快速入門，Cloud Manager提供立即開始開發數字型驗所需的一切，包括儲存自定義項的Git儲存庫，然後由Cloud Manager構建、驗證和部署。

使用雲管理器，開發團隊可以在不依賴Adobe人員的情況下頻繁地做出更改。

Cloud Manager中提供三種類型的環境。

* 開發
* 分段
* 生產

可以使用非生產流水線將代碼部署到開發環境。 對於總是一起進行的分段環境和生產環境，生產管道使用 [質量門](/help/implementing/cloud-manager/custom-code-quality-rules.md) 驗證應用程式碼和配置更改。

生產管道首先將代碼和配置部署到登台環境，test應用程式，最後部署到生產環境。

Cloud ServiceSDK始終用最新的as a Cloud ServiceAEM改進進行更新，允許直接利用開發人員的本地硬體進行本地開發。 這使得快速發展，週轉時間非常短。 因此，開發人員可以留在他們熟悉的本地環境中，從各種開發工具中進行選擇，並在他們認為合適時推動開發環境或生產。

Cloud Manager支援靈活的多組設定，可根據企業需要進行調整。 為確保與多個團隊進行穩定部署，同時避免出現一個團隊影響所有團隊生產的情況，Cloud Manager的有主見的管道始終會驗證並test所有團隊的代碼。

## 真實世界示例 {#real-world-example}

每個企業都有不同的需求，包括不同的團隊設定、流程和開發工作流。 下面介紹的設定由Adobe用於在as a Cloud Service之上提供經驗的AEM多個項目。

例如，Adobe Creative Cloud應用程式(如Adobe Photoshop或Adobe Illustrator)包括可供其最終用戶使用的教程、示例和指南等內容資源。 此內容由客戶端應用程式以無AEM頭方式使用as a Cloud Service、對雲發佈層進行API調用以將結構化內容作為JSON流檢索AEM，以及利用 [as a Cloud Service中的內容分發網路(CDN)](/help/implementing/dispatcher/cdn.md#content-delivery) 為結構化和非結構化內容提供最佳效能。

為此項目作出貢獻的團隊遵循以下流程。

每個團隊都使用自己的開發工作流，並有單獨的Git儲存庫。 附加的共用Git儲存庫用於登錄項目。 此Git儲存庫包含Cloud Manager的Git儲存庫的根結構，包括共用調度程式配置。

在啟用新項目時，需要在共用git儲存庫的根部的Reactor Maven項目檔案中列出。 對於調度程式配置，將在調度程式項目內建立新的配置檔案。 然後，主調度程式配置將包括此檔案。 每個團隊負責自己的調度程式配置檔案。 對共用Git儲存庫所做的更改很少，通常只有在掛接新項目時才需要更改。 主要工作由每個項目團隊在其自己的Git儲存庫中完成。

![工作流圖](/help/implementing/cloud-manager/assets/team-setup1.png)

使用 [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 遵循項目設定的最佳做AEM法。 唯一的例外是調度程式配置，如上所述在共用Git儲存庫中完成。

每個團隊都使用一個簡化的git工作流，它有兩個+ N分支，遵循git流模型：

* 穩定的釋放分支包含生產代碼。

* 開發分支包含最新的開發。

* 對於每個特徵，都會建立新分支。

開發是在特徵分支中完成的。 當特徵成熟時，它會合併到開發分支中。 從開發分支中選取已完成和已驗證的特徵並合併到穩定分支中。

所有更改都通過拉取請求(PR)完成。 每個PR都通過質量門自動驗證。 聲納用於質量檢查代碼，並運行一組test套件，以確保新代碼不引入任何回歸。

Cloud Manager的Git儲存庫中的安裝程式有兩個分支。

* 穩定的版本分支包含來自所有團隊的生產代碼。
* 開發分支包含所有團隊的開發代碼。

在開發或穩定分支中，每次向團隊的Git儲存庫推送都會觸發 [GitHub操作。](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code)

所有項目都遵循穩定分支的相同設定。 對項目的穩定分支的推送會自動推送到Cloud Manager的git儲存庫中的穩定分支。 Cloud Manager中的生產管道配置為通過推送到穩定分支來觸發。 因此，通過任何團隊的每次推動進入穩定分支來執行生產流水線，並且如果所有質量門都通過，則更新生產部署。

![推送圖](/help/implementing/cloud-manager/assets/team-setup2.png)

將推送到開發分支的處理方式不同。 當向團隊的git儲存庫中的開發人員分支的推送同時觸發GitHub操作，並且代碼自動推入到Cloud Manager的git儲存庫中的開發分支中時，非生產管道不會由代碼推送自動觸發。 它由對雲管理器API的調用觸發。

運行生產管道包括通過提供的質量門檢查所有團隊的代碼。 一旦將代碼部署到存放階段，將執行test和審計，以確保一切正常。 一旦所有門都通過，更改就會被推出到生產中，而不會造成任何中斷或停機。

就地方發展而言， [用於AEMas a Cloud Service的SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing) 的子菜單。 SDK允許設定本地作者、發佈和調度程式。 這可實現離線開發和快速週轉。 有時只使用作者環境進行開發，但快速設定調度程式和發佈環境允許在本地測試所有內容，然後再推入git儲存庫。

每個團隊的成員通常從共用的Git中籤出代碼以及他們自己的項目代碼。 由於項目是獨立的，因此無需簽出其他項目。

![本地簽出和SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

此真實世界設定可用作藍圖，然後根據企業的需要進行定制。 git的靈活分支和合併概念允許根據每個團隊的需要定制上述工作流的變體。 AEMas a Cloud Service支援所有這些變化，而不犧牲有見地的Cloud Manager管道的核心價值。

>[!TIP]
>
>請參閱文檔 [使用多個源Git儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html#managing-code) 瞭解有關此設定的詳細資訊。

### 多組設定的注意事項 {#considerations}

使用Cloud Manager的git儲存庫和生產流水線，所有質量門都始終運行完整的生產代碼，將其視為一個部署單元。 這樣，生產系統總是不中斷或不停機。

相反，沒有這樣的系統，因為每個團隊都可以單獨部署，所以單個團隊的更新可能會導致生產穩定性問題。 此外，它需要協調和計畫內停機來推出更新。 隨著團隊數量的增加，協調工作將變得複雜得多，並且很快無法管理。

如果在質量門中檢測到問題，則不影響生產，並且可以檢測並解決該問題，而不需要Adobe人員介入。 如果不進行Cloud Service，並且不總是對整個部署進行測試，部分部署可能會導致停機，這需要請求回滾，甚至需要從備份進行完全恢復。 部分測試還可能導致其他問題，這些問題在事實發生後需要Adobe人員的協調和支援才需要解決。

>[!TIP]
>
>對於任何多團隊設定，定義治理模型和所有團隊都必須遵循的一套標準至關重要。 多組設定的上一個藍圖允許跨更多組進行擴展，您可以將其用作起點。
