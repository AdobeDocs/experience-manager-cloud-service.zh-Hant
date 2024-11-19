---
title: Edge Delivery Services的進行中網站功能
description: 瞭解哪些AEM Sites功能和使用案例正在進行，並探索使用Edge Delivery Services時的替代解決方案。
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
source-git-commit: 92da26452438f2b56cdec1aecc76587d4982f00e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Edge Delivery Services的進行中網站功能 {#wip-sites-features}

瞭解哪些AEM Sites功能和使用案例正在進行，並探索使用Edge Delivery Services時的替代解決方案。

>[!TIP]
>
>工作進行中並不代表道路已結束。 如果您需要本檔案中列為進行中的功能或使用案例，請洽詢您的Adobe代表。 您和Adobe可以共同合作，瞭解您的特定需求，並尋找替代解決方案。

## 創作中的功能 {#wip-features}

搭配AEM Sites使用Edge Delivery Services時，大部分的網站功能都可供使用。 例如，[網站主控台](/help/sites-cloud/authoring/sites-console/introduction.md)中幾乎任何可用的動作都適用於Edge Delivery Services。

但是，有些功能是進行中的工作(WIP)。 WIP功能是Sites主控台的功能，目前尚未適用於AEM Sites的Edge Delivery Services，或僅部分可用。 因此，WIP功能的顯示方式可能與Sites功能不同，或者可能有其他解決方案可供使用案例。

下列清單顯示此類在製品功能與替代解決方案。 如果您的專案需要WIP功能，請檢閱下方建議的替代方案，並聯絡Adobe共同合作，瞭解您的使用案例。

| 網站功能 | Edge狀態 | 附註 | Edge檔案 |
|---|---|---|---|
| [頁面繼承](/help/sites-cloud/administering/msm-and-translation.md) | 可使用 |  | 通用編輯器中的[內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [元件繼承](/help/sites-cloud/administering/msm-and-translation.md) | 部分可用 | 元件會繼承內容，但繼承只能在頁面層級還原 | 通用編輯器中的[內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [語言副本](/help/sites-cloud/administering/translation/overview.md) | 部分可用 | 元件會繼承內容，但繼承只能在頁面層級還原 | 通用編輯器中的[內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [多網站管理](/help/sites-cloud/administering/msm/overview.md) | 部分可用 | 元件會繼承內容，但繼承只能在頁面層級還原 | 通用編輯器中的[內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [啟動](/help/sites-cloud/authoring/launches/overview.md) | 部分可用 | 元件會繼承內容，但繼承只能在頁面層級還原 | 通用編輯器中的[內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [頁面範本](/help/sites-cloud/authoring/page-editor/templates.md) | 部分可用 | 從範本建立的頁面是原始範本的獨立副本。 | [將頁面範本與通用編輯器搭配使用](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [內容中心與目標](/help/sites-cloud/authoring/personalization/overview.md) | 無法使用 |  |  |
| [時間扭曲](/help/sites-cloud/authoring/launches/preview.md) | 無法使用 |  |  |
| [相關聯的內容](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | 無法使用 |  |  |
| [體驗片段](/help/sites-cloud/authoring/fragments/experience-fragments.md) | 替代方案 | 建立頁面並使用片段元件 |  |

## 進行中工作使用案例 {#wip-use-cases}

由於Edge Delivery Services建置在全新的現代技術棧疊上，因此下列AEM Sites使用案例尚未完全涵蓋，因此正在開發中。 如果您的專案需要WIP使用案例，請洽詢Adobe以一起合作，並瞭解您的專案需求。

| 網站使用案例 | 詳細資料 |
|---|---|
| 轉譯頁面的伺服器端邏輯 | 將AEM執行階段用作應用程式伺服器 |
| 動態頁面 | SSI或任何動態include技術 |
| User management | 使用AEM作為IdP |
| 驗證 | 將AEM用於安全內容 |
| 內容許可權 | AEM作為安全外部網路 |
