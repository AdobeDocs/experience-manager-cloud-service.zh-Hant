---
title: 程式碼重構工具的統一體驗
description: 程式碼重構工具的統一體驗
translation-type: tm+mt
source-git-commit: c00b10b4d564e05099740b9ff991624db4f37a3d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# 程式碼重構工具的統一體驗 {#unified-experience}

為客戶提供多種不同互動點的工具，可讓客戶產生不連貫的體驗，並增加使用工具的複雜性，而每種工具在安裝、設定和執行方面的執行需求都不同。

## 優點 {#benefits}

「代碼重構工具的統一體驗」會叫用並執行所有代碼重構工具，這些工具可在同一位置處理原始碼。

「代碼重構工具的統一體驗」以及配套的儲存庫允許：

* 將所有處理原始碼移轉的工具統一到一個公開的 `node.js` 應用程式中， `aio-cli plugin` 為使用者提供一致的使用者體驗。

* 預配以透過單一命令執行整體移轉，同時提供依需求執行特定工具的彈性。

* 簡化日後新增工具（例如新增工具至外掛程式）的流程，只需為開發人員新增新命令，並為使用者提供簡單的外掛程式更新，如此，您的體驗就會與增加更多價值保持一致。

### 瞭解應用程式設計

此工具將所有程式碼重構工具統一為公開的node.js應用程式， `aio-cli plugin` 為使用者提供一致的使用者體驗。

外掛程式包含兩個主要部分：

* **使用者介面**

   `aio-cli` 命令執行一個或多個遷移工具（通過連結要按順序執行的工具）`config.yaml` ，該遷移工具將輸入所需的輸入參數

* **基礎移轉工具套件**

   遷移工具通過以下方式執行其功能：

   * 掃描客戶代碼的各個部分並執行遷移（根據最佳做法的代碼實施）以生成輸出，然後驗證和部署輸出。

   * 以一致的順序記錄遷移時執行的操作，以生成摘要報告。

## 使用外掛程式 {#using-plugin}

這會 `aio-cli-plugin-aem-cloud-service-migration` 重新調整客戶本機上的代碼、儲存庫結構或配置。 本頁摘要瞭解統一體驗的詳細需求和設計決策。
它可做為社群的開放原始碼，以擴充自訂使用案例。

## 可用性 {#availability}

您可以安裝和使用via(目 `aio-cli-plugin-aem-cloud-service-migration` 前僅與 `aio-cli` dispatcher轉換器整合)。

請參閱 [Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) ，以瞭解此工具的使用情況，以及您如何為此工具貢獻心力。

外掛程式程式碼已開啟，來源於Github。

