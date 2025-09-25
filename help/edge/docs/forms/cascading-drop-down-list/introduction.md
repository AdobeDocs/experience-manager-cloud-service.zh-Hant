---
title: 階層式下拉式清單
description: 使用 API 整合來動態填入下拉式清單
feature: Edge Delivery Services
role: User,Developer
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: ht
source-wordcount: '125'
ht-degree: 100%

---

# 使用案例說明

在建置表單或應用程式時，以結構化的方式引導使用者完成位置選取通常很實用。階層式下拉式清單可讓此操作變得簡單易用，使用者會先選取國家/地區 (用於篩選出可用州/省的清單)，然後根據所選州進行最後的城市選擇。此方法不僅可保持表單簡潔，也可防止無效組合 (例如選擇不存在所選州內的城市）。

完成此使用案例需要進行下列步驟

- 建立 API 整合
- 建立含有欄位的表單，來擷取國家/州/城市
- 建立規則以使用 API 整合填入下拉式清單