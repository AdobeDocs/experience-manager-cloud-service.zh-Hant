---
title: 頁面編輯器和通用編輯器
description: Adobe 仍然支援頁面編輯器，但通用編輯器為您的新專案帶來令人期待的可能性。
feature: Developing
role: Admin, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 100%

---

# 頁面編輯器和通用編輯器 {#page-editor-universal-editor}

Adobe 仍然支援頁面編輯器，但通用編輯器為您的新專案帶來令人期待的可能性。

## 背景 {#background}

Adobe 於 2024 年推出[通用編輯器](/help/implementing/universal-editor/introduction.md)，這是一款採用現代 Javascript 型開發方法的精簡編輯器。通用編輯器是 Adobe 想要提供流暢且可擴充之視覺化內容製作體驗的願景。

Adobe 深知[頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)擁有豐富的功能，而且在 AEM 的悠久歷史中已有無數專案投資使用頁面編輯器，因此 Adobe 將繼續全面支援頁面編輯器，但是創新功能的研發會以通用編輯器為主。

## 建議 {#recommendation}

儘管差距正在迅速縮小，但通用編輯器和頁面編輯器之間的功能仍然有差距 ([下個區段會提供功能比較資訊](#feature-comparison))。

根據經驗法則：

* **新專案**&#x200B;應預設運用通用編輯器。
* **現有專案**&#x200B;應繼續使用頁面編輯器，並在啟動 Edge Delivery 或無周邊工作時考慮使用通用編輯器。

**您選擇哪一種編輯器，完全根據您的個別專案需求決定。**

## 功能比較 {#feature-comparison}

由於兩種編輯器之間的功能差距越來越小，請務必查閱[通用編輯器發行說明](/help/release-notes/universal-editor/current.md)，了解最新開發進展。

### 傳遞 {#delivery}

|  | 頁面編輯器 | 備註 | 通用編輯器 | 備註 |
|---|---|---|---|---|
| [發佈傳遞](/help/sites-cloud/authoring/author-publish.md) | [!BADGE 可用]{type=Positive} | 建議搭配核心元件及傳統 AEM 專案使用 | [!BADGE 無法使用]{type=Negative} | 傳統 AEM 頁面通常會依賴幾個頁面編輯器特定的功能，而通用編輯器沒辦法依照原樣複製這些功能。 |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE 無法使用]{type=Negative} |  | [!BADGE 可用]{type=Positive} |  |
| [無周邊傳遞](/help/headless/introduction.md) | [!BADGE 部分可用]{type=Caution} | 僅能透過 [SPA 編輯器](/help/implementing/developing/hybrid/introduction.md)，[已淘汰](/help/implementing/developing/hybrid/spa-editor-deprecation.md)並改用通用編輯器 | [!BADGE 可用]{type=Positive} | 通用編輯器讓開發人員能夠使用自己的網頁應用程式，但沒有施加任何特定的框架需求或實施限制。 |

### 持續性 {#persistence}

|  | 頁面編輯器 | 備註 | 通用編輯器 | 備註 |
|---|---|---|---|---|
| 編輯頁面元件 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 編輯[內容片段](/help/assets/content-fragments/content-fragments.md) | [!BADGE 無法使用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | 包括插入新片段以及重新排列片段 |

### 功能 {#capabilities}

|  | 頁面編輯器 | 備註 | 通用編輯器 | 備註 |
|---|---|---|---|---|
| 頁面範本 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 通用編輯器與系統所使用的範本無關。然而，典型的實施模式偏好使用開發人員定義的範本，因為使用現代的前端工具，開發人員可以直接在程式碼中輕鬆地定義及維護範本邏輯。 |
| WYSIWYG 編輯 | [!BADGE 可用]{type=Positive} | 僅限頁面 | [!BADGE 可用]{type=Positive} | 支援頁面和內容片段 |
| [產生變化版本](/help/generative-ai/generate-variations.md) | [!BADGE 無法使用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | [可以用作擴充功能](/help/implementing/universal-editor/extending.md) |
| 插入新區塊 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 重新排列區塊 | [!BADGE 可用]{type=Positive} | 可以在內容中使用拖放功能，但不能在「樹狀視圖」側面板中進行 | [!BADGE 可用]{type=Positive} | 可以在「樹狀視圖」側面板透過拖放功能來達成，但目前尚未在內容中進行 (已規劃) |
| 剪下/複製貼上區塊 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 套用樣式 | [!BADGE 可用]{type=Positive} | 可以使用[樣式系統](/help/sites-cloud/authoring/page-editor/style-system.md)將樣式套用至元件上。 | [!BADGE 可用]{type=Positive} | 可以使用常規元件 (或內容片段) 屬性套用樣式。通用編輯器中無法使用相同的樣式選取器，但透過多重選取小工具可以達到非常相似的使用者體驗。 |
| 套用版面 | [!BADGE 可用]{type=Positive} | 網站必須實施 [AEM 回應式網格](/help/implementing/developing/introduction/responsive-design.md)，讓作者能夠跨三個預先定義的中斷點調整元件大小。 | [!BADGE 可用]{type=Positive} | 可以使用常規元件 (或內容片段) 屬性套用版面，但不支援回應式網格。 |
| 還原及取消復原 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 發佈 (以及預覽) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [啟動工作流程](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可以用作擴充功能 |
| 評論 | [!BADGE 可用]{type=Positive} | 使用[註解](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE 無法使用]{type=Negative} | 已規劃 |
| Workfront 整合 | [!BADGE 無法使用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | 可以用作擴充功能 |
| [MSM 和啟動](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可以用作頁面擴充功能 |
| 實驗和個人化 | [!BADGE 可用]{type=Positive} | 使用[目標模式](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE 可用]{type=Positive} | 可以用作 Edge Delivery Services 擴充功能 |
| 內容樹 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 也允許在樹內重新排列 |
| 裝置模擬 | [!BADGE 可用]{type=Positive} | [可以模擬已設定的裝置，](/help/sites-cloud/administering/responsive-layout.md)但使用者無法手動輸入任何不同的螢幕尺寸進行模擬。 | [!BADGE 可用]{type=Positive} | [可以手動輸入任何要模擬的螢幕尺寸，](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)但無法設定預設的中斷點。 |
| [頁面鎖定](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 依循 Sites 控制台內設定的鎖定狀態，並能透過擴充功能從編輯器鎖定/解除鎖定頁面 |
| [頁面屬性](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可以從網站管理員處取得，並能透過擴充功能從編輯器存取頁面的屬性 |
| 多欄位屬性 | [!BADGE 可用]{type=Positive} |  | [!BADGE 無法使用]{type=Negative} | 已規劃 |
| [遠端 DAM](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [頁面版本設定](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [時間扭曲](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp)和[差異視圖](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 無法使用]{type=Negative} | 已規劃 |
| 在管理員視圖中檢視 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可以用作頁面擴充功能 |
| 檢視頁面狀態 | [!BADGE 可用]{type=Positive} |  | [!BADGE 無法使用]{type=Negative} | 可在 Sites 控制台內使用 |
| 可擴充性 | [!BADGE 可用]{type=Positive} | 做為 AEM 覆蓋 | [!BADGE 可用]{type=Positive} | 做為使用 App Builder 的明確定義的擴充點，且只需要很少的 AEM 特定知識 |

## 採用通用編輯器 {#adopt-ue}

通用編輯器具有許多優勢，是適合新專案的絕佳解決方案。

* **視覺化編輯：**&#x200B;與頁面編輯器一樣，作者可以直接在預覽中編輯內容，並立即看到其變更如何影響訪客體驗。
* **符合未來需求：** AEM 的路徑圖將通用編輯器作為視覺化編輯器優先考量。採用通用編輯器可以確保獲得最新的創新和增強功能。
* **更簡單的整合：**&#x200B;使用通用編輯器不需要 AEM 特定的 SDK，減少過度依賴技術堆疊的情形。
* **自備應用程式：**&#x200B;通用編輯器支援任何網頁框架或架構，不需要複雜的重構過程即可採用。
* **可擴充性：**&#x200B;因為擁有強大的[擴充框架，](/help/implementing/universal-editor/extending.md)包括與生成式 AI、Workfront 等的整合，使通用編輯器更具優勢。

### 移轉至通用編輯器 {#migrate-ue}

從頁面編輯器移轉至通用編輯器並沒有直接路徑。這是因為兩種技術存在根本差異。

* 通用編輯器並未重新引進範本編輯器、樣式系統或回應式網格等功能。
   * 現在透過 Edge Delivery Services 或無周邊專案中的精益型前端 CSS 和 Javascript，可以更有效地處理這些使用案例。
* 由於通用編輯器是一種編輯器即服務，因此無法讓實施者將 CSS 或 JS 注入元件對話框中。
   * 故不能從頁面編輯器自動轉換元件對話框。
   * 此情況會影響對話框的很多地方，例如自訂小工具、欄位驗證、顯示/隱藏規則，以及範本型自訂功能。
      * 雖然這些功能仍然可行，但通用編輯器是透過設定來解決這些問題，而非在對話框中部署自訂 JavaScript。

雖然通用編輯器在技術上可以支援編輯傳統 AEM 專案 (例如使用核心元件建置) 的頁面，但這些網站通常會依賴幾個頁面編輯器特定的功能，例如樣式系統、回應式網格、可編輯範本，以及對話框中的自訂 Javascript。

由於通用編輯器採用更精簡、現代化的方法，並不支援這些舊版功能，因此移轉此類網站需要進行大量重構工作。因此，**唯有轉換至 Edge Delivery Services 的專案，才會建議將頁面編輯器網站移轉至通用編輯器。**
