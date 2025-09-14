---
title: 階層式下拉式清單
description: 使用API整合以動態填入下拉式清單
feature: Edge Delivery Services
role: User,Developer
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 2%

---

# 使用案例說明

在建置表單或應用程式時，以結構化的方式引導使用者完成位置選擇通常會有幫助。 階層式下拉式清單可讓這項操作簡單且方便使用 — 使用者會先選取國家/地區（用於篩選可用州/省的清單），然後根據州進行最後的城市選擇。 此方法不僅可保持表單整潔，也可防止無效的組合（例如挑選不存在選定狀態的城市）。

完成此使用案例需要下列步驟

- 建立 API 整合
- 建立含有欄位的表單，以擷取國家/州/市
- 使用API整合建立規則以填入下拉式清單