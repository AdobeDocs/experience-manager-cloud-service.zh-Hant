---
title: 設定推送失效
description: 瞭解如何設定推送失效，以建置您自己的生產CDN。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 7cded93c-325c-4a4b-8644-e6a2379d5179
source-git-commit: 0ac6856e8f3e664fcc7e3c08faac4c4f5c16af18
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 2%

---

# 設定推送失效

推播失效可確保作者所做的內容更新在發佈時自動從託管內容傳遞網路(CDN)中移除。 這麼做可確保只提供最新的內容。

系統會根據特定URL和快取標籤或索引鍵清除內容，確保清除過時的版本。

若要啟用推送失效，必須將特定屬性新增至專案的設定檔。 例如，SharePoint中名為`.helix/config.xlsx`的Microsoft Excel活頁簿，或Google Drive中的Google工作表名稱`.helix/config`。

以下設定屬性定義生產主機的名稱和CDN管理的型別：

| key | 值 | 個評論 |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | 生產網站的主機名稱。 例如，`www.example.com`。 |
| `cdn.prod.type` | 已管理 |   |

一旦對組態工作表進行變更，使用者必須使用[Sidekick工具](/help/edge/docs/sidekick.md)預覽並啟動它們以套用更新。

另請參閱[關於Cloud Manager中的Edge Delivery待辦事項清單](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list)。
