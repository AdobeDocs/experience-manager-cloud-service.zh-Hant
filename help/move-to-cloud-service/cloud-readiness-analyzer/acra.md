---
title: AEM系統概觀
description: AEM系統概觀
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 1%

---


# AEM系統概觀 {#aem-system}

本頁將AEM描述為雲端服務，可提供新功能，與舊版AEM相比，其架構具有顯著增強功能。 升級至此新架構需要付出大量努力。

## 說明 {#background}

ACRA中繼模式可用來識別與AEM升級為雲端服務相關的數個問題。 它通過模式的反向連結和&quot;referencedBy&quot;值及其上下文對象的 *組合* ，支援多種類型的 *建議資訊* 。 上 *下文物* 件中的類型 *值* ，會決定已偵測到的特定問題。

ACRA模式中包括的就緒性問題預計導致建議的實例較少。 AEM雲端服務可能有許多執行個體需要注意，而且這些執行個體會有其他相關的準備問題。 （請參閱UUI和URS。）

## 模式資料 {#pattern-data}

模式的JSON表示法中包含下列物件：

* **item.message**: 就緒問題類型。 （請參閱下文。）
* **資料**: 包含與類型對應之資料的JSON物件。

### 可能的影響和風險 {#possible-implications}

TBD

### 可能的解決方案  {#possible-solutions}

TBD
