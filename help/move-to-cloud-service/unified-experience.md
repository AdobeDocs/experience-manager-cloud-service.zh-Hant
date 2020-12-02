---
title: 程式碼重構工具的統一體驗
description: 程式碼重構工具的統一體驗
translation-type: tm+mt
source-git-commit: 5d2b14c827603297a59cba7180fc1a68de0c841a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---


# 程式碼重構工具的統一體驗{#unified-experience}

我們已開發工具來自動化某些程式碼重構工作，以便與AEM（即雲端服務）相容。 為了降低安裝和設定不同程式碼重構工具的複雜性，我們開發了一個外掛程式，以統一在程式碼和儲存庫上運作的工具。

## 優點{#benefits}

Unified Experience外掛程式提供下列優點：

* 將處理原始碼的工具統一至以`aio-cli `外掛程式形式公開的`node.js`應用程式，為使用者提供一致的使用者體驗。

* 提供透過單一命令執行所有工具的功能，同時提供視需要執行特定工具的彈性。

* 提供擴充性，以簡化新工具的加入，同時維持體驗的一致性。

## 瞭解外掛程式{#understanding-plugin}

`aio-cli-plugin-aem-cloud-service-migration`外掛程式包含兩個主要部分：

* **使用者介面**

   * `aio-cli` 命令執行一個或多個代碼重構工具（通過連結要按順序執行的工具）。
   * `config.yaml` 輸入所需的輸入參數。

* **基礎程式碼重構工具套裝**

   代碼重構工具通過以下方式執行其功能：

   * 掃描客戶程式碼的個別區段並控製程式碼（根據最佳實務的程式碼實作）以產生輸出，然後驗證並部署。

   * 生成摘要報告以記錄執行期間執行的操作。

## 可用性 {#availability}

請參閱[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)，以瞭解使用情況，以及如何對此外掛程式程式碼貢獻心力，此外掛程式碼是以GitHub開啟。

>[!NOTE]
>目前，外掛程式已與AEM Dispatcher Converter和Repository Modernizer整合。
