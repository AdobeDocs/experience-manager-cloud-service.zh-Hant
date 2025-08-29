---
title: 疑難排解Adaptive Forms的自訂提交動作中的502錯誤
description: 瞭解如何識別並解決在調適型Forms （核心元件）中使用自訂提交動作時發生的502錯誤頁面。 本指南說明常見原因（例如未處理的例外），並提供解決步驟。
feature: Adaptive Forms, Core Components
role: Developer
level: Intermediate
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 1%

---


# 疑難排解：自訂提交動作中的502錯誤頁面

使用最適化Forms （核心元件）時，您在提交使用自訂提交動作的表單後，可能會遇到&#x200B;**502錯誤頁面HTML**。

## 問題

**錯誤：**&#x200B;當自訂提交動作服務失敗時，會顯示502錯誤頁面HTML。

**原因：**&#x200B;如果自訂提交動作擲回未處理的錯誤，例如Null指標、無效的API回應或執行階段失敗，就會發生這種情況。

## 解決方法

若要防止502錯誤頁面，請使用try-catch區塊來包裝提交邏輯，以適當地處理錯誤。

如需詳細步驟，請參閱[為最適化Forms （核心元件）建立自訂提交動作](/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md)。
