---
title: 程式碼重構工具的統一體驗
description: 瞭解程式碼重構工具的統一體驗。
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# 程式碼重構工具的統一體驗 {#unified-experience}

Adobe已開發出工具，可自動執行與Adobe Experience Manager (AEM)as a Cloud Service相容所需的一些程式碼重構任務。 為了降低與安裝和設定不同程式碼重構工具相關的複雜性，Adobe開發了一個外掛程式，以統一在程式碼和存放庫上操作的工具。

## 優點 {#benefits}

統一的Experience外掛程式提供下列優點：

* 將處理原始程式碼的工具統一到一個公開為`aio-cli `外掛程式的`node.js`應用程式中，以便為使用者提供一致的使用者體驗。

* 透過單一指令執行所有工具，同時提供彈性以視需要執行特定工具。

* 簡化新工具的加入，同時保持一致的體驗。

## 瞭解外掛程式 {#understanding-plugin}

`aio-cli-plugin-aem-cloud-service-migration`外掛程式包含兩個主要部分：

* **使用者介面**

   * `aio-cli`命令以執行一或多個程式碼重構工具（透過連結要循序執行的工具）。
   * `config.yaml`接受必要的輸入引數。

* **基礎程式碼重構工具套裝**

  程式碼重構工具透過以下方式執行其功能：

   * 掃描客戶程式碼的個別區段並操控程式碼（根據最佳實務的程式碼實施）以產生輸出，然後可加以驗證和部署。

   * 產生摘要報告以記錄執行期間執行的作業。

## 可用性 {#availability}

請參閱[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)，瞭解使用情形以及如何為GitHub中開放來源的外掛程式程式碼貢獻內容。

>[!NOTE]
>目前，外掛程式已與AEM Dispatcher Converter和Repository Modernizer整合。
