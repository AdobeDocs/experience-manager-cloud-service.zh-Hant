---
title: Edge Delivery Services 仍在開發中的 Sites 功能
description: 了解哪些 AEM Sites 功能和使用案例仍在開發中，並在使用 Edge Delivery Services 時探索替代解決方案。
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
source-git-commit: 92da26452438f2b56cdec1aecc76587d4982f00e
workflow-type: ht
source-wordcount: '473'
ht-degree: 100%

---

# Edge Delivery Services 仍在開發中的 Sites 功能 {#wip-sites-features}

了解哪些 AEM Sites 功能和使用案例仍在開發中，並在使用 Edge Delivery Services 時探索替代解決方案。

>[!TIP]
>
>仍在開發中的狀態並不代表窮途末路。如果您需要本文件中列為仍在開發中的功能或使用案例，請與您的 Adobe 代表聯絡。您和 Adobe 可以合作了解您的特定需求，並尋找替代解決方案。

## 仍在開發中的功能 {#wip-features}

將 Edge Delivery Services 與 AEM Sites 搭配使用時，大多數 Sites 功能都可使用。例如，[Sites 主控台](/help/sites-cloud/authoring/sites-console/introduction.md)中提供的所有動作幾乎都適用於 Edge Delivery Services。

但是，某些功能仍在開發中 (WIP)。WIP 功能是 Sites 主控台的功能，但於 AEM Sites 的 Edge Delivery Services 尚無法使用，或僅部分可用。因此，WIP 功能的呈現方式可能與其 Sites 對應功能不同，或針對使用案例可能有替代解決方案。

以下清單列出此類 WIP 功能和替代解決方案。如果您的專案需要 WIP 功能，請檢閱下方建議的替代方案，並與 Adobe 聯絡以共同了解您的使用案例。

| Sites 功能 | Edge 上的狀態 | 備註 | Edge 文件 |
|---|---|---|---|
| [頁面繼承](/help/sites-cloud/administering/msm-and-translation.md) | 可使用 |  | [通用編輯器中的內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [元件繼承](/help/sites-cloud/administering/msm-and-translation.md) | 部分可用 | 元件繼承內容，但繼承只能在頁面層級恢復 | [通用編輯器中的內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [語言副本](/help/sites-cloud/administering/translation/overview.md) | 部分可用 | 元件繼承內容，但繼承只能在頁面層級恢復 | [通用編輯器中的內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [多網站管理](/help/sites-cloud/administering/msm/overview.md) | 部分可用 | 元件繼承內容，但繼承只能在頁面層級恢復 | [通用編輯器中的內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [啟動](/help/sites-cloud/authoring/launches/overview.md) | 部分可用 | 元件繼承內容，但繼承只能在頁面層級恢復 | [通用編輯器中的內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [頁面範本](/help/sites-cloud/authoring/page-editor/templates.md) | 部分可用 | 從範本建立的頁面，是原始範本的獨立副本。 | [將頁面範本與通用編輯器搭配使用](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [Context Hub 和目標市場選擇](/help/sites-cloud/authoring/personalization/overview.md) | 無法使用 |  |  |
| [時間扭曲](/help/sites-cloud/authoring/launches/preview.md) | 無法使用 |  |  |
| [相關聯的內容](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | 無法使用 |  |  |
| [體驗片段](/help/sites-cloud/authoring/fragments/experience-fragments.md) | 替代方案 | 建立頁面並使用片段元件 |  |

## 仍在開發中的使用案例 {#wip-use-cases}

由於 Edge Delivery Services 建構在全新的現代技術堆疊上，因此 AEM Sites 的以下使用案例尚未完全涵蓋，而且仍在開發中。如果您的專案需要 WIP 使用案例，請與 Adobe 聯絡以共同了解您的專案需求。

| Sites 使用案例 | 詳細資料 |
|---|---|
| 轉譯頁面的伺服器端邏輯 | 使用 AEM 的執行階段作為應用程式伺服器 |
| 動態頁面 | SSI 或任何動態包含技術 |
| 使用者管理 | 使用 AEM 作為 IdP |
| 驗證 | 使用 AEM 保護內容 |
| 內容授權 | 將 AEM 作為安全外部網路 |
