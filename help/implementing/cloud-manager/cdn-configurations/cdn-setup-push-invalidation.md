---
title: 設定推送失效
description: 瞭解如何設定推送失效，以建置您自己的生產CDN。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
source-git-commit: 3941b7f97d434946a3cb796633f306b89e68c0a4
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 2%

---

# 設定推送失效

推播失效可確保作者所做的內容更新在發佈時自動從託管內容傳遞網路(CDN)中移除，因此僅提供最新的內容。

系統會根據特定URL和快取標籤或索引鍵清除內容，確保清除過時的版本。

若要啟用推送失效，必須將特定屬性新增至專案的設定檔。 例如，SharePoint中名為`.helix/config.xlsx`的Microsoft Excel活頁簿，或Google Drive中的Google工作表名稱`.helix/config`。

以下設定屬性定義生產主機的名稱和CDN管理的型別：

| key | 值 | 個評論 |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | 生產網站的主機名稱。 例如，`www.example.com`。 |
| `cdn.prod.type` | 已管理 |   |

一旦對組態工作表進行變更，使用者必須使用[Sidekick工具](/help/edge/docs/sidekick.md)預覽並啟動它們以套用更新。
