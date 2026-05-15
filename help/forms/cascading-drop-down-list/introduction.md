---
title: 階層式下拉式清單
description: 使用最適化Forms運算式來新增自動驗證、計算，並開啟或關閉區段的可見度。
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 86%

---

# 使用案例說明

在建置表單或應用程式時，以結構化的方式引導使用者完成位置選取通常很實用。 階層式下拉式清單可讓此操作變得簡單易用，使用者會先選取國家/地區 (用於篩選出可用州/省的清單)，然後根據所選州進行最後的城市選擇。 此方法不僅可保持表單簡潔，也可防止無效組合 (例如選擇不存在所選州內的城市）。

完成此使用案例需要進行下列步驟

- 建立 API 整合
- 建立含有欄位的表單，來擷取國家/州/城市
- 建立規則以使用 API 整合填入下拉式清單