---
title: 瞭解通用編輯器 — 回應式模式
description: 本文說明如何使用通用編輯器中的不同模擬器預覽表單，以視覺化方式呈現表單在製作期間的外觀。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 1%

---


# WYSIWYG製作中的回應式模式

<span class="preview">此功能可透過搶先存取計畫使用。 若要要求存取權，請將您的GitHub組織名稱和存放庫名稱從您的官方地址傳送電子郵件至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> 。 例如，如果存放庫URL是https://github.com/adobe/abc，組織名稱是adobe，存放庫名稱是abc。</span>

## 回應式Forms簡介

在現今的多裝置世界中，無論是在桌上型電腦熒幕還是智慧型手機，各種大小的熒幕上都必須呈現優異的外觀和良好的功能。 Universal Editor中的回應式模式可讓您在編寫過程中預覽和測試跨不同裝置大小的表單，協助您達成此目標。

[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)可讓您建立自動適應不同熒幕大小的表單，提供最佳的使用者體驗，無論使用何種裝置。

## 在不同裝置的回應模式下預覽Forms

通用編輯器在熒幕右上角提供&#x200B;**模擬器**&#x200B;圖示，可讓您預覽不同裝置大小的頁面，並測試回應式設計的行為，以獲得更佳的使用者體驗。

若要在回應模式中預覽表單：

1. 在通用編輯器中開啟表單以進行編輯。
2. 按一下工具列中顯示裝置預覽符號![&#128279;](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%，width=2%}圖示的模擬器圖示。
3. 選取裝置格式：
   - 案頭（預設）
   - 平板電腦
   - 行動
   - 自訂（指定寬度和高度）

![通用編輯器的熒幕擷圖顯示不同裝置的回應式模式選項](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

在平板電腦或行動裝置上預覽時，您也可以使用&#x200B;**熒幕旋轉器**&#x200B;圖示，在直向與橫向之間切換。

通用編輯器提供不同的模擬器來預覽不同裝置上的表單。 下表列出可用的模擬器型別及其對應的裝置表示法：

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">模擬器型別</th>
        <th style="width: 80%">裝置影像</th>
    </tr>
    <tr>
        <td style="width: 20%">桌上型電腦</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="顯示全形版面配置的表單案頭檢視" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">平板電腦</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="顯示具有調整元件之中等寬度版面配置的表單平板電腦檢視" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">行動</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="顯示具有棧疊元件之窄版面配置的表單行動裝置檢視" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">自訂裝置</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="具有使用者指定維度的表單自訂裝置檢視" style="width: auto; height: auto"></td>
    </tr>
</table>

## 佈局功能

Universal Editor可讓您建立易於使用的表單，為使用者提供動態體驗。 表單版面配置會控制專案或元件在表單中的顯示方式。

Universal Editor支援下列型別的表單版面：

- [面板版面配置](#panel-layout)
- [精靈配置](#wizard-layout)
- [收合式選單版面](#accordion-layout)

### 面板布局

面板版面配置很適合用來組織相關欄位，讓您更輕鬆地導覽及尋找對應內容。 面板版面配置會將表單元件排列在表單的不同區段或面板中。

![在表單中顯示多個不同區段的面板配置](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**範例：**&#x200B;工作申請表單可能會使用面板，將「個人資訊」、「教育」、「工作體驗」和「參考」分隔成不同的區段。

**回應式行為：**&#x200B;在較小的熒幕上，面板通常會垂直棧疊，維持其不同的群組，同時調整為較窄的寬度。

您可以使用[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)，在表單中新增面板配置。 如需如何設定面板元件各種屬性的詳細指示，請參閱[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)文章。

### 精靈配置

精靈版面配置會將複雜表單分成不同步驟，有助於簡化表單。 每個步驟代表流程的不同部分，使用者會依序瀏覽各個步驟，通常使用&#x200B;**下一步**&#x200B;和&#x200B;**上一步**&#x200B;按鈕。 您可以使用精靈版面配置來建立包含多個區段或步驟的表單。

![精靈版面配置顯示具有導覽控制項的多步驟表單](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**範例：**&#x200B;保險索賠表單可能會使用精靈引導使用者提供事件詳細資料、上傳證據、輸入個人資訊及檢閱提交內容。

**回應式行為：**&#x200B;在行動裝置上，精靈會維持其逐步方式，但會調整每個步驟中的內容以適合較窄的熒幕，通常會棧疊在較大熒幕上並排顯示的元素。

您可以使用[精靈元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)在表單中新增精靈配置。 如需有關如何設定精靈元件各種屬性的詳細指示，請參閱[精靈元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)文章。

### 收合式選單版面配置

摺疊式功能表佈局會以最適化表單的可摺疊區段或面板顯示內容。 展開區段時，會在其中顯示內容，而其他區段仍會保持收合狀態。 此版面適合以精簡格式顯示大量資訊。

![摺疊式功能表版面配置顯示表單中的可展開區段](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**範例：**&#x200B;產品設定表單可能會使用「基本選項」、「進階功能」、「配件」和「付款方案」的收合式選單區段，讓使用者一次只能專注一個方面。

**回應式行為：**&#x200B;摺疊式功能表在行動裝置上特別好用，因為摺疊式功能表只會顯示擴充的內容區段，自然就能節省垂直空間，非常適合用於較小的熒幕。

您可以使用[摺疊式功能表元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)，在表單中新增摺疊式功能表配置。 如需如何設定摺疊式功能表元件的各種屬性的詳細指示，請參閱[摺疊式功能表元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)文章。

### 如何選擇正確的版面？

請務必選擇正確的版面以最佳化使用者體驗和表單功能。 此表格可協助您瞭解可用的不同版面配置選項，並引導您根據特定需求和使用案例選取最適合的版面：

| 功能 | 面板布局 | 精靈配置 | 收合式選單版面配置 |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **用途** | 將相關內容分組為不同的區段 | 引導使用者完成多步驟流程或表單 | 將內容組織成可摺疊的區段 |
| **結構** | 不同的區段 | 循序步驟/頁面 | 可摺疊面板/區段 |
| **導覽** | 按一下面板標題以進行導覽 |  — 前進：「下一步」按鈕<br> — 後退：「後退」按鈕<br> — 選擇性略過步驟 | 按一下標題可展開/收合區段 |
| **使用者體驗** | 以可管理的方式組織大量內容 | 逐步指導，減少負擔 | 具有展開/收合區段的精簡檢視 |
| **使用案例** | 具有已分類區段的複雜表單 | 設定程式、複雜表單 | 常見問題集、設定功能表、詳細內容區段 |
| **最適合行動裝置** | 稽核 — 面板垂直棧疊 | 良好 — 只持續關注目前的步驟 | 極佳 — 使用可摺疊的區段節省空間 |

## 回應式Forms的最佳作法

為確保您的表單在所有裝置間提供最佳體驗，請遵循下列最佳實務：

1. **首先針對行動裝置進行設計：**&#x200B;首先針對行動裝置設計您的表單，然後針對較大的熒幕進行增強。 此方法可確保核心功能在最小的熒幕上運作。

2. **使用適當的欄位型別：**&#x200B;選擇在觸控裝置上運作良好的欄位型別：
   - 選項很多時，請使用下拉式清單，而非選項按鈕
   - 使用專為觸控輸入設計的日期選擇器
   - 確認按鈕和觸控目標至少為44px x 44px

3. **簡化較小的熒幕：**
   - 在行動裝置上每列顯示較少的欄位
   - 請考慮隱藏「顯示更多」選項後的選用欄位
   - 在行動裝置上將複雜的表單分成更多步驟

4. **徹底測試：**&#x200B;請一律在實際裝置上測試您的表單，或在Universal Editor中使用模擬器模式，以確保這些表單在不同熒幕大小間都正常運作。

5. **請考慮載入時間：**&#x200B;最佳化影像大小並最小化所需資源，尤其是針對連線速度較慢的行動使用者。

## 疑難排解回應式Forms

| 問題 | 可能的原因 | 解決方案 |
|-------|---------------|----------|
| 行動裝置上的表單顯示為被切斷 | 修正寬度設定或溢位問題 | 使用相對單位(%， rem)而非畫素，並檢查溢位：隱藏屬性 |
| 難以互動的觸控元素 | 接觸目標太小或太接近 | 將按鈕/輸入大小增加到至少44px x 44px，並在互動元素之間增加更多空間 |
| 小熒幕上的內容溢位 | 小型檢視區沒有回應式規則 | 新增媒體查詢或回應式類別，以調整不同熒幕大小的版面 |
| 行動裝置上的表單速度太慢 | 大型影像或過多的指令碼 | 最佳化影像、最小化JavaScript，並考慮非關鍵元素的延遲載入 |
| 模擬器和實際裝置之間的外觀不同 | 瀏覽器專用轉譯或裝置變化 | 儘可能在實際裝置上進行測試，而不只是模擬器 |

## 另請參閱

{#see-more-eds-forms}
