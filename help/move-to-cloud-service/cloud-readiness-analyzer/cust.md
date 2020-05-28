---
title: 檢測到自定義
description: 檢測到自定義
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# 檢測到自定義 {#cust-pattern}

本頁介紹「檢測到自定義」模式代碼。

## 背景 {#background}

此模式碼可用來識別已對AEM例項進行的自訂。 由於AEM的自訂很常見，因此此模式不一定表示有問題。 它會識別自訂記錄，以便評估自訂記錄對升級計畫的影響。

檢測到的自定義包括：

* 客戶代碼（套件）和配置
* 協力廠商套件
* 與協力廠商服務整合
* 非標準Oak索引

## 模式資料 {#pattern-data}

模式的JSON表示法中包含下列物件：

* **item.message**: 是指模式的訊息。
* **item.context**: 參考概述資訊的其他資訊：
   * *類型*: customization.detected.
   * *資料*: 包含說明自訂之資料的JSON物件

### 可能的影響和風險 {#possible-implications}

不適用。

### 可能的解決方案  {#possible-solutions}

不適用。
