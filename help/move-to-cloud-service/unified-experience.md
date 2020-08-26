---
title: 程式碼重構工具的統一體驗
description: 程式碼重構工具的統一體驗
translation-type: tm+mt
source-git-commit: 9ef0681f93c8c25a1e5115cccb987d2db32c318e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# 程式碼重構工具的統一體驗 {#unified-experience}

Unified Experience for Code Reforgent工具將AEM的執行體驗統一為Cloud Service程式碼重構工具，可在分派程式檔、程式碼和儲存庫上運作。

此工具可降低使用程式碼重構工具的複雜性，而每種工具在安裝、設定和執行方面都有不同的執行需求。

![影像](/help/move-to-cloud-service/assets/unified-one.png)

## 優點 {#benefits}

「程式碼重構的統一體驗」工具會叫用並執行所有程式碼重構工具，這些工具可在同一處處理原始碼。

這些工具以及輔助儲存庫允許：

* 將所有處理原始碼移轉的工具統一到一個公開的 `node.js` 應用程式中， `aio-cli plugin` 為使用者提供一致的使用者體驗。

* 提供資源，以透過單一命令執行整體移轉，同時提供依需求執行特定工具的彈性。

* 簡化日後新增工具（例如新增工具至外掛程式）的程式，只需為開發人員新增新命令，並為使用者提供簡單的外掛程式更新，體驗就會與增加更多價值保持一致。

## 瞭解外掛程式 {#understanding-plugin}

這會 `aio-cli-plugin-aem-cloud-service-migration` 重新調整客戶本機上的代碼、儲存庫結構或配置。 本頁摘要瞭解統一體驗的詳細需求和設計決策。
它可做為社群的開放原始碼，以擴充自訂使用案例。

此工具將所有程式碼重構工具統一為公開的node.js應用程式， `aio-cli plugin` 為使用者提供一致的使用者體驗。 此外掛程式會掃描客戶的本機程式碼庫，並產生AEM做為Cloud Service相容的程式碼、組態和套件，然後可部署至Cloud Service環境。

外掛程式包含兩個主要部分：

* **使用者介面**

   `aio-cli` 命令執行一個或多個遷移工具（通過連結要按順序執行的工具）`config.yaml` ，該遷移工具將輸入所需的輸入參數

* **基礎移轉工具套件**

   遷移工具通過以下方式執行其功能：

   * 掃描客戶代碼的各個部分並執行遷移（根據最佳做法的代碼實施）以生成輸出，然後驗證和部署輸出。

   * 以一致的順序記錄遷移時執行的操作，以生成摘要報告。

## 可用性 {#availability}

您可以安裝並使用 `aio-cli-plugin-aem-cloud-service-migration` via `aio-cli`。

>[!NOTE]
>目前，此工具僅與Dispatcher Converter整合。

請參閱 [Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) ，以瞭解使用情況，以及如何為此外掛程式程式程式碼提供貢獻，此外掛程式程式碼是以GitHub開啟。

