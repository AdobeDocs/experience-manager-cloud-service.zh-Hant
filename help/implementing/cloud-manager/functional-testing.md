---
title: 功能測試
description: 了解內建在 AEM as a Cloud Service 部署流程中的三種不同類型的功能測試，以確保程式碼的品質和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 9%

---


# 簡介 {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能測試"
>abstract="了解內建在 AEM as a Cloud Service 部署流程中的三種不同類型的功能測試，以確保程式碼的品質和可靠性。"

瞭解中可用的品質門檻 [AEMas a Cloud Service部署程式](/help/implementing/cloud-manager/deploy-code.md)，以及內建的不同功能測試型別、貢獻方式以及如何在整體測試策略中妥善運用這些工具。

## 概觀

下圖提供整體測試策略背景下可用管道的整體概觀，以及 [AEMas a Cloud Service部署程式](/help/implementing/cloud-manager/deploy-code.md).

![AEM Cloud Service部署品質閘道](assets/functional-testing/quality-gates-compact.svg)

## 用途

AEM Cloud Service部署管道的用途是在開發和AEM產品發行生命週期的各個階段促進穩定且安全的部署。 這些管道在不同層級合併多個品質閘道，以確保部署AEM應用程式變更和AEM產品更新的完整性和安全性。

Adobe提供數個內建品質閘道，而其他閘道則需要您的介入以進行實作和設定。 這些品質門檻是多種多樣的，其中一些適用於生命週期的不同階段，甚至可整合到您自己的開發設定和CI/CD流程中。

內建品質門檻主要在AEM應用程式內容中驗證AEM產品的功能。 相較之下，您設定的自訂品質閘道則可驗證應用程式的關鍵功能和使用者互動是否如預期般執行。 這兩組品質閘道共同運作，確保程式碼修改和AEM產品更新的穩定且安全的自動部署。

請務必注意，這些品質閘道並非旨在作為您整個測試策略的全面測試架構。 AEM產品在進入AEM雲端服務部署程式前會接受大量測試。 同樣地，您的應用程式在到達部署階段之前應該已經是高品質的。 此方法可確保品質門檻專注於維護部署流程的主要目標，而不是取代完整的測試制度。

## 品質閘道

下圖提供可用品質閘道的詳細檢視，及其在整體測試策略中的使用情況，以及 [AEMas a Cloud Service部署程式](/help/implementing/cloud-manager/deploy-code.md).

![AEM Cloud Service部署品質閘道](assets/functional-testing/quality-gates-overview.svg)

### 摘要客戶提供的品質閘道

|                               | 單元測試 | 自訂<br/> 功能測試 | 自訂<br/> UI測試 | 客戶<br/> 驗證 | 手動<br/> 測試 |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **生產管道** | 是<br/>封鎖<br/> | 是<br/>封鎖<br/>60m逾時 | 是<br/>封鎖<br/>60m逾時 | 否 | 否 |
| **非生產管道** | 是<br/>封鎖<br/> | 選擇加入<br/>封鎖<br/>60m逾時 | 選擇加入<br/>封鎖<br/>60m逾時 | 否 | 否 |
| **Adobe內部驗證** | 是<br/>封鎖<br/> | 是<br/>封鎖<br/>60m逾時 | 是<br/>封鎖<br/>60m逾時 | 否 | 否 |
| **客戶CI/CD** | 是 | 是 | 是 | 是 | 是 |
| **客戶當地開發人員** | 是 | 是 | 是 | 是 | 是 |

### 單元測試

建議您為AEM應用程式提供單元測試，這是每個測試策略的基礎。 這些設定旨在快速且經常地執行，並提供早期且快速的意見反應。 它們已緊密整合到開發人員工作流程、您自己的CI/CD和AEM雲端服務部署管道中。

它們會使用JUnit實作，並使用Maven執行。 另請參閱 [AEM專案原型的核心模組](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/core.html#unit-tests) AEM的單元測試及快速入門範例。

### 程式碼品質

此品質閘道是現成可用的設定，且會對AEM應用程式程式碼執行靜態程式碼分析。

另請參閱 [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md) 和 [自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md) 以取得詳細資訊。

### 產品測試

產品功能測試是 AEM 中核心功能 (例如編寫和複製任務) 的一組穩定 HTTP 整合測試 (IT)。Adobe提供和維護開箱即用的功能。 它們旨在防止自訂應用程式程式碼變更而中斷AEM產品中的核心功能時進行部署。

透過Junit實作、使用Maven執行並使用官方的 [AEM測試使用者端](https://github.com/adobe/aem-testing-clients). 產品測試套件會維護為 [開放原始碼專案](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)，會遵循最佳實務，且可以視為實施測試的良好起點。

### 自訂功能測試

和產品測試一樣，客戶功能測試是HTTP整合測試(IT)，也使用Junit實作，使用Maven執行並在官方網站上建置 [AEM測試使用者端](https://github.com/adobe/aem-testing-clients).

>[!NOTE]
>
>自訂功能測試會在生產和非生產（選擇加入）管道中執行，您的AEM應用程式會使用這些管道變更部署和AEM產品推播更新，因此是協助確保應用程式正常運作並提高發行安全性的關鍵貢獻。 客戶功能測試也會在每個客戶的內部發行前驗證管道中執行，這有助於提供早期意見反應。

為了保持管道執行效率，我們建議專注於關鍵功能和主要使用者互動流程。 建議使用約15分鐘或更短的執行時間進行功能測試。 建議在客戶開發流程中，將不符合此品質閘道的完整功能測試套裝作為一般客戶驗證管道的一部分執行。

另請參閱 [開放原始碼產品測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 或 [AEM專案原型的it.tests模組](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/ittests.html) 例如。

如需詳細資訊，請參閱 [Java 功能測試](/help/implementing/cloud-manager/java-functional-testing.md)。

### 自訂UI測試

為了最大化客戶特定開發的風險控制，Adobe強烈建議您將關鍵UI測試擷取到AEMCS中。 其數量有限，但對客戶體驗的影響最大。

測試封裝在Docker映像中 — 設計為儘可能易變（支援Cypress、Selenium、Java和Javascript）。 它們遵循與自訂功能測試相同的特性和目的。

>[!NOTE]
>
>自訂UI測試會在生產和非生產（選擇加入）管道中執行，您的AEM應用程式會使用這些管道變更部署和AEM產品推播更新，因此是協助確保應用程式正常運作並提高發行安全性的重要貢獻。 客戶UI測試也會在每個客戶的內部發行前驗證管道中執行，這有助於提供早期意見反應。

為了保持管道執行效率，我們建議專注於關鍵功能和主要使用者互動流程。 建議在客戶開發流程期間，作為一般客戶驗證管道的一部分執行不符合此品質閘道的完整UI測試套裝。

另請參閱 [開放原始碼範例測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) 或 [AEM專案原型的ui.tests模組](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uitests.html) 例如。

如需詳細資訊，請參閱[自訂 UI 測試](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)。

### 體驗稽核

體驗稽核品質閘道正在執行 [Google燈塔](https://developer.chrome.com/docs/lighthouse/overview/) 會針對客戶網頁進行稽核。

此品質閘道由AEM現成提供，但未封鎖部署管道。 依預設，會針對根頁面進行稽核(`/`)的設定檔。 您可以設定最多25個要納入稽核考量的自訂路徑，以便協助撰寫。

另請參閱 [體驗稽核測試](/help/implementing/cloud-manager/experience-audit-testing.md) 以取得詳細資訊。

### 客戶驗證

客戶驗證品質閘道是客戶自身測試策略和工作的預留位置，在客戶的應用程式變更傳至AEM雲端部署管道之前執行。

您可以在此處選擇您偏好的工具和架構。 相較於客戶功能測試和自訂UI測試，沒有與AEMas a Cloud Service相關的限制，因此我們建議在這裡執行長期執行的功能和UI測試。

雖然您可以自由選擇任何工具和架構，但建議您將HTTP型整合測試和UI測試與自訂功能測試和自訂UI測試品質閘道中可用的工具和架構搭配起來。 我們建議整合 [快速開發環境(RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 使用本機測試策略，儘可能在AEM雲端環境中進行測試。

### 手動測試

手動測試品質閘道是進行手動測試之客戶的預留位置。 AEM雲端管道不支援手動測試，因此這需要在您自己的本機測試策略中進行。

若是手動測試，將其與其他AEM Cloud Service開發環境整合會很有用。
