---
title: 為 Edge Delivery 網站設定推播失效
description: 了解如何為 Edge Delivery 網站設定推播失效，以確保內容更新和快取控制的效率。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 7cded93c-325c-4a4b-8644-e6a2379d5179
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: ht
source-wordcount: '173'
ht-degree: 100%

---

# 設定推播失效

推播失效可確保作者所做的內容更新在發佈時會自動從受管理的內容傳遞網路 (CDN) 中移除。此做法能確保僅提供最新的內容。

系統會根據特定的 URL 和快取標記或金鑰來清除內容，確保清除過時的版本。

若要啟用推播失效，必須將特定屬性新增至專案的設定檔案中。例如，在 SharePoint 中名為 `.helix/config.xlsx` 的 Microsoft Excel 活頁簿，或 Google Drive 中名為 `.helix/config` 的 Google Sheet。

以下設定屬性會定義生產主機的名稱和內容傳遞網路管理的類型：

| 金鑰 | 值 | 註解 |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | 生產網站的主機名稱。例如，`www.example.com`。 |
| `cdn.prod.type` | 受管理 |   |

對設定表單進行變更後，使用者必須使用 [Sidekick 工具](https://www.aem.live/docs/sidekick)進行預覽並將其啟動，方能套用更新的內容。

另請參閱「[關於 Cloud Manager 中的 Edge Delivery 待辦事項清單](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list)」。
