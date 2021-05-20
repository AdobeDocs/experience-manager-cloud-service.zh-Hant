---
title: 程式碼重構工具的統一體驗
description: 程式碼重構工具的統一體驗
exl-id: 856bce12-7d5e-4f8c-b252-7752bcbeebc4
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# 代碼重構工具{#unified-experience}的統一體驗

我們開發了一些工具來自動化某些程式碼重構工作，這些工作是為了與AEM as aCloud Service相容。 為了降低安裝和設定不同程式碼重構工具的相關複雜度，我們開發了外掛程式，以統一可在程式碼和存放庫上運作的工具。

## 優點 {#benefits}

Unified Experience外掛程式提供下列優點：

* 將處理原始碼的工具統整到作為`aio-cli `外掛程式公開的一個`node.js`應用程式中，為使用者提供一致的使用者體驗。

* 通過單個命令執行所有工具，同時提供根據需要執行特定工具的靈活性。

* 提供擴充性，以簡化新工具的新增作業，同時維持體驗的一致性。

## 了解外掛程式{#understanding-plugin}

`aio-cli-plugin-aem-cloud-service-migration`外掛程式包含兩個主要部分：

* **使用者介面**

   * `aio-cli` 命令，執行一個或多個代碼重構工具（通過連結要按順序執行的工具）。
   * `config.yaml` 會輸入所需的輸入參數。

* **基礎程式碼重構工具套裝**

   程式碼重構工具透過下列方式執行其功能：

   * 掃描客戶代碼的各個部分並操作代碼（基於最佳實務的代碼實現）以生成輸出，然後驗證並部署輸出。

   * 生成摘要報告以記錄執行期間執行的操作。

## 可用性 {#availability}

請參閱[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)以了解使用方式，以及如何貢獻此外掛程式程式碼（源自GitHub開啟）。

>[!NOTE]
>目前，外掛程式已與AEM Dispatcher Converter和Repository Modernizer整合。
