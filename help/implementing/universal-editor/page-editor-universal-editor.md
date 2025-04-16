---
title: 頁面編輯器和通用編輯器
description: 頁面編輯器仍受Adobe支援，但通用編輯器為您的新專案帶來現有可能性。
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 9fdc24600c9dd4ebf6a3d12462eb9bd387815360
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 3%

---


# 頁面編輯器和通用編輯器 {#page-editor-universal-editor}

頁面編輯器仍受Adobe支援，但通用編輯器為您的新專案帶來現有可能性。

## 背景 {#background}

Adobe於2024年推出[Universal Editor](/help/implementing/universal-editor/introduction.md)，將其簡化為採用現代Javascript開發方法的編輯器。 Universal Editor是Adobe的願景，提供順暢且可擴充的視覺內容製作體驗。

Adobe認可[頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)的豐富功能集以及長期投資於AEM的無數專案，仍持續完整支援頁面編輯器，不過創新將集中在通用編輯器上。

## 推薦 {#recommendation}

雖然快速縮小，但通用編輯器和頁面編輯器之間仍存在功能間隙（[可在下一節](#feature-comparison)中找到功能比較）。

根據經驗：

* **新專案**&#x200B;預設為使用通用編輯器。
* **現有專案**&#x200B;應繼續使用頁面編輯器，並在啟動Edge Delivery或Headless作業時考量通用編輯器。

**您選擇的編輯器應完全由您個別專案的需求驅動。**

## 功能比較 {#feature-comparison}

由於兩個編輯器之間的功能間隔不斷縮小，請務必參閱Universal Editor的[發行說明](/help/release-notes/universal-editor/current.md)以瞭解最新發展。

### 傳遞 {#delivery}

|  | 頁面編輯器 | 備註 | 通用編輯器 | 備註 |
|---|---|---|---|---|
| [傳統AEM傳遞](/help/sites-cloud/authoring/author-publish.md) | [!BADGE 可用]{type=Positive} | 建議與核心元件搭配使用 | [!BADGE 不能利用的]{type=Negative} | 經典AEM頁面通常依賴於特定於頁面編輯器的多個功能，這些功能很難通過通用編輯器按原樣複製。 |
| [邊緣傳送](/help/edge/overview.md) | [!BADGE 無法使用]{type=Negative} |  | [!BADGE 可用]{type=Positive} |  |
| [Headless傳遞](/help/headless/introduction.md) | [!BADGE 部分可用]{type=Caution} | 只有[SPA Editor，](/help/implementing/developing/hybrid/introduction.md)已[棄用](/help/implementing/developing/hybrid/spa-editor-deprecation.md)，而改用通用編輯器 | [!BADGE 可用]{type=Positive} | Universal Editor可讓開發人員自備Web應用程式，而不需要強制實施任何特定框架要求或實施限制。 |

### 持續性 {#persistence}

|  | 頁面編輯器 | 注意 | 通用編輯器 | 備註 |
|---|---|---|---|---|
| 編輯頁面元件 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 正在編輯[內容片段](/help/assets/content-fragments/content-fragments.md) | [!BADGE 無法使用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | 包括插入新片段和重新排序片段 |

### 功能 {#capabilities}

|  | 頁面編輯器 | 注意 | 通用編輯器 | 備註 |
|---|---|---|---|---|
| 頁面範本 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 通用編輯器與所使用的範本系統無關。 但是，典型的實施模式傾向於開發人員定義的範本，因為現代前端工具使開發人員更容易直接在代碼中定義和維護範本邏輯。 |
| WYSIWYG編輯 | [!BADGE 可用]{type=Positive}僅限頁面 |  | [!BADGE 可用]{type=Positive} | 支援的頁面和內容片段 |
| [產生變化版本](/help/generative-ai/generate-variations.md) | [!BADGE 無法使用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | [可作為擴充功能使用](/help/implementing/universal-editor/extending.md) |
| 插入新區塊 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 重新排序區塊 | [!BADGE 可用]{type=Positive} | 可能使用內文中拖放，但無法在「樹狀檢視」側面板中使用 | [!BADGE 可用]{type=Positive} | 可能透過拖放至「樹狀檢視」側面板進行，但尚無法置於內文中檢視（已規劃） |
| 剪下/複製 — 貼上區塊 | [!BADGE 可用]{type=Positive} |  | [!BADGE 無法使用]{type=Negative} | 已計劃 |
| 套用樣式 | [!BADGE 可用]{type=Positive} | 樣式可以使用[樣式系統](/help/sites-cloud/authoring/page-editor/style-system.md)套用至元件。 | [!BADGE 可用]{type=Positive} | 可使用一般元件（或內容片段）屬性套用樣式。 通用編輯器中沒有相同的樣式選擇器，但是使用多選Widget可以達到非常類似的UX。 |
| 套用配置 | [!BADGE 可用]{type=Positive} | Sites必須實施 [AEM回應式網格](/help/implementing/developing/introduction/responsive-design.md) ，以使作者能夠跨三個預定義的斷點調整元件大小。 | [!BADGE 可用]{type=Positive} | 可以使用常規元件（或內容片段）屬性應用佈局，但不支援回應式網格。 |
| 還原-取消復原 | [!BADGE 可用]{type=Positive} |  | [!BADGE 無法使用]{type=Negative} | 已計劃 |
| 發佈（也用於預覽） | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [開始工作流程](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可作為擴充功能使用 |
| 註解 | [!BADGE 可用]{type=Positive} | 使用 [批注](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE 不能利用的]{type=Negative} | 已計劃 |
| 工作面集成 | [!BADGE 不能利用的]{type=Negative} |  | [!BADGE 可用]{type=Positive} | 可作為擴充功能使用 |
| [MSM和啟動](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可作為擴充功能用於頁面 |
| 實驗與個人化 | [!BADGE 可用]{type=Positive} | 使用[目標模式](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE 可用]{type=Positive} | 可作為Edge Delivery Services的擴充功能使用 |
| 內容樹 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 也允許在樹狀結構中重新排序 |
| 裝置模擬 | [!BADGE 可用]{type=Positive} | [可模擬已設定的裝置，](/help/sites-cloud/administering/responsive-layout.md)，但使用者無法手動輸入任何要模擬的不同熒幕尺寸。 | [!BADGE 可用]{type=Positive} | [可以手動輸入任何要模擬的熒幕維度，](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)，但無法設定預設中斷點。 |
| [頁面鎖定](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 尊重在Sites Console中設定的鎖定狀態，其擴充功能可用於從編輯器鎖定/解鎖頁面 |
| [頁面屬性](/help/sites-cloud/authoring/sites-console/page-properties.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 「網站管理員」可提供，擴充功能也可用來從編輯器存取頁面屬性 |
| 多欄位屬性 | [!BADGE 可用]{type=Positive} |  | [!BADGE 無法使用]{type=Negative} | 已計劃 |
| [遠端DAM](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [頁面版本設定](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [TimeWarp](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp)和[差異檢視](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 不能利用的]{type=Negative} | 已計劃 |
| 檢視 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可作為頁面擴充功能使用 |
| 檢視頁面狀態 | [!BADGE 可用]{type=Positive} |  | [!BADGE 無法使用]{type=Negative} | 可在Sites主控台中使用 |
| 擴充性 | [!BADGE 可用]{type=Positive} | 作為AEM覆蓋圖 | [!BADGE 可用]{type=Positive} | 使用App Builder定義清晰的擴充功能點，且AEM的特定知識非常少 |

## 採用通用編輯器 {#adopt-ue}

通用編輯器具有許多優點，使其成為新項目的絕佳解決方案。

* **可视化编辑：** 與頁面编辑器一樣，作者可以直接在預覽中编辑內容，並立即查看其更改如何影響訪客體驗。
* **面向未來：** AEM的路線圖將通用編輯器作為可視化編輯者優先考慮。 採用它可確保獲得最新的創新和增強功能。
* **更簡單的集成：** 使用通用編輯器不需要特定於AEM的SDK，從而減少了技術堆疊鎖定。
* **自備應用程式：** Universal Editor支援任何Web架構或架構，允許採用而不需要複雜的重構。
* **擴充性：** Universal Editor受益於強大的[擴充架構，](/help/implementing/universal-editor/extending.md)，包括與GenAI、Workfront等的整合。

### 移轉至通用編輯器 {#migrate-ue}

沒有從頁面編輯器直接移轉至通用編輯器的路徑。 這是因為兩種技術的根本差異。

* 通用編輯器不會重新引入範本編輯器、樣式系統或回應式格線等功能。
   * 在Edge Delivery Services或Headless專案中，現在可以使用精簡前端CSS和Javascript更高效地處理這些使用案例。
* 由於通用編輯器是editor-as-a-service，實作人員無法將CSS或JS插入元件對話方塊中。
   * 這可防止從頁面編輯器自動轉換元件對話方塊。
   * 這會影響對話方塊的許多區域，例如自訂Widget、欄位驗證、顯示/隱藏規則，以及範本型自訂。
      * 雖然仍可使用這些功能，但通用編輯器會透過設定解決它們，而不是透過對話方塊部署的自訂JavaScript。

雖然通用編輯器在技術上可以啟用傳統AEM頁面的編輯（例如使用核心元件建置），但這些網站通常需依賴數個頁面編輯器特定功能，例如樣式系統、回應式格線、可編輯範本和對話方塊中的自訂Javascript。

由於通用編輯器遵循不支援這些舊功能的更簡化的現代方法，因此遷移此類網站需要進行重大重構。 因此，只建議將專案轉換為Edge Delivery Services時，**將頁面編輯器網站移轉至Universal Editor。**
