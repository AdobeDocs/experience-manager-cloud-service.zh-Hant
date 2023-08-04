---
title: 程式碼重構工具的統一體驗
description: 瞭解程式碼重構工具的統一體驗。
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# 程式碼重構工具的統一體驗 {#unified-experience}

我們開發了工具，可自動執行與AEMas a Cloud Service相容所需的一些程式碼重構任務。 為了降低不同程式碼重構工具的安裝和設定相關複雜性，我們開發了一個外掛程式，以統一在程式碼和存放庫上操作的工具。

## 優點 {#benefits}

統一的Experience外掛程式提供下列優點：

* 將處理原始程式碼的工具統一為一個 `node.js` 應用程式公開為 `aio-cli ` 外掛程式，為使用者提供一致的使用者體驗。

* 提供透過單一命令執行所有工具的功能，同時提供根據需要執行特定工具的靈活性。

* 提供擴充功能以簡化新工具的加入，同時保持一致的體驗。

## 瞭解外掛程式 {#understanding-plugin}

此 `aio-cli-plugin-aem-cloud-service-migration` 外掛程式包含兩個主要部分：

* **使用者介面**

   * `aio-cli` 指令來執行一或多個程式碼重構工具（透過連結要循序執行的工具）。
   * `config.yaml` 這會採用必要的輸入引數。

* **基礎程式碼重構工具套裝**

  程式碼重構工具透過以下方式執行其功能：

   * 掃描客戶程式碼的個別區段並操控程式碼（根據最佳實務的程式碼實施）以產生輸出，然後可以驗證和部署。

   * 產生摘要報告以記錄執行期間執行的作業。

## 可用性 {#availability}

另請參閱 [Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 瞭解其使用方式，以及如何為GitHub中開放來源的外掛程式程式碼貢獻內容。

>[!NOTE]
>目前，外掛程式已與AEM Dispatcher Converter和Repository Modernizer整合。
