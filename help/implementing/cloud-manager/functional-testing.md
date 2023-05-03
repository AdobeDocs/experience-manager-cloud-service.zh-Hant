---
title: 功能測試
description: 了解內建在 AEM as a Cloud Service 部署流程中的三種不同類型的功能測試，以確保程式碼的品質和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 7d15440159a8e24314753acd5b37fcd2c5e8ec4c
workflow-type: ht
source-wordcount: '554'
ht-degree: 100%

---


# 功能測試 {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能測試"
>abstract="了解內置在 AEM as a Cloud Service 部署過程中的三種不同類型的功能測試，以確保程式碼的品質和可靠性。"

了解內建在 [AEM as a Cloud Service 部署流程](/help/implementing/cloud-manager/deploy-code.md)中的三種不同類型的功能測試，以確保程式碼的品質和可靠性。

## 範圍

Cloud Manager 管道中功能測試步驟的目的是確保應用程式的基本功能按預期運作。

此測試階段是將程式碼部署到生產環境之前的最後一層自動化測試。

功能測試不應取代，而應補充和擴展其他測試策略，如單元測試、整合測試，或在 Cloud Manager 管道執行之外執行的功能測試。

## 總覽 {#overview}

AEM as a Cloud Service 中有三種不同類型的功能測試。

* [產品功能測試](#product-functional-testing)
* [自訂功能測試](#custom-functional-testing)
* [自訂 UI 測試](#custom-ui-testing)

對於所有功能測試，作為[部署流程](/help/implementing/cloud-manager/deploy-code.md)的一部分，可以使用組建總覽畫面中的&#x200B;**下載組建記錄**&#x200B;按鈕，將測試的詳細結果下載為 `.zip` 檔案。

這些記錄不包括實際 AEM 執行時進程的記錄。若要存取這些記錄，請參閱[存取和管理記錄](/help/implementing/cloud-manager/manage-logs.md)文件以了解詳細資訊。

產品功能測試和範例自訂功能測試均以 [AEM 測試用戶端](https://github.com/adobe/aem-testing-clients)為基礎。

### 產品功能測試 {#product-functional-testing}

產品功能測試是 AEM 中核心功能 (例如編寫和複製任務) 的一組穩定 HTTP 整合測試 (IT)。這些測試由 Adobe 維護，旨在防止自訂應用計劃程式碼變更而破壞核心功能時進行部署。

* [產品管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)：每當您將新程式碼部署到 Cloud Manager 時，都會自動執行產品功能測試，且不能跳過。
* [非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)：可以選擇在執行非生產管道時執行產品功能測試。

產品功能測試會作為開放原始碼專案進行維護。如需詳細資訊，請參閱 GitHub 中的[產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)。

### 自訂功能測試 {#custom-functional-testing}

雖然產品功能測試由 Adobe 定義，但您可以為自己的應用計劃編寫自己的品質測試。這將作為自訂功能測試作為[生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)或選擇性[非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)的一部分執行，以確保您應用程式的品質。

自訂功能測試會針對自訂程式碼部署和推送升級執行，這對於編寫良好的功能測試，以防止 AEM 程式碼變更而破壞應用程式碼尤為重要。自訂功能測試步驟一律存在且不能跳過。

如需詳細資訊，請參閱 [Java 功能測試](/help/implementing/cloud-manager/java-functional-testing.md)。


### 自訂 UI 測試 {#custom-ui-testing}

自訂 UI 測試是一項選擇性功能，可讓您為應用計劃建立和自動執行 UI 測試。UI 測試是封裝在 Docker 影像中的 Selenium 型測試，以便在語言和架構 (例如 Java 和 Maven、Node 和 WebDriver.io 或任何其他根據 Selenium 建置的架構和技術) 中提供廣泛的選擇。

如需詳細資訊，請參閱[自訂 UI 測試](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)。

