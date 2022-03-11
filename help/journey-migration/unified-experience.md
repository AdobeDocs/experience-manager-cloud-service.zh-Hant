---
title: 代碼重構工具的統一體驗
description: 代碼重構工具的統一體驗
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# 代碼重構工具的統一體驗 {#unified-experience}

我們開發了一些工具來自動執行一些與as a Cloud Service相容的代碼重構任AEM務。 為了降低與安裝和設定不同代碼重構工具相關的複雜性，我們開發了一個插件來統一在代碼和儲存庫上運行的工具。

## 好處 {#benefits}

「統一體驗」插件提供了以下好處：

* 將處理原始碼的工具統一為一個 `node.js` 應用程式公開 `aio-cli ` 插件為用戶提供一致的用戶體驗。

* 提供通過單個命令執行所有工具的能力，同時還提供根據需要執行特定工具的靈活性。

* 提供可擴充性以簡化新工具的添加，同時保持體驗的一致性。

## 瞭解插件 {#understanding-plugin}

的 `aio-cli-plugin-aem-cloud-service-migration` 插件由兩個主要部分組成：

* **使用者介面**

   * `aio-cli` 命令以執行一個或多個代碼重構工具（通過連結要按順序執行的工具）。
   * `config.yaml` 輸入所需的輸入參數。

* **基礎代碼重構工具套件**

   代碼重構工具通過以下方式執行其功能：

   * 掃描客戶代碼的相應部分並操縱代碼（基於最佳做法的代碼實現）以生成輸出，然後驗證和部署輸出。

   * 生成摘要報告以記錄執行期間執行的操作。

## 可用性 {#availability}

請參閱 [Git資源：aio-cli-plugin-aem — 雲服務 — 遷移](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 瞭解使用情況以及您如何為此插件代碼提供幫助，該插件代碼是在GitHub中開源的。

>[!NOTE]
>當前該插件已與AEMDispatcher Converter和Repository Modernizer整合。
