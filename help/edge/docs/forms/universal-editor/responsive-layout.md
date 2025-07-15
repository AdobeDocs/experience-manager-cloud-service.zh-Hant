---
title: 了解通用編輯器：回應式模式
description: 此文章將說明如何在通用編輯器中使用不同的模擬器預覽表單，以便於製作過程中將其外觀視覺化呈現。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 99%

---


# WYSIWYG 製作的回應式模式

<span class="preview">這是透過我們的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-hant#new-features">發行前通道</a>提供的發行前功能。</span>

## 回應式表單簡介

在現今的多裝置世界中，您的表單在各種尺寸的螢幕上，包括從桌上型電腦顯示器到智慧型手機，必須一律看起來美觀且運作良好。通用編輯器中的回應式模式，能讓您在製作過程中以不同的裝置尺寸預覽及測試表單，以利達成上述目標。

[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)讓您能夠建立會自動適應不同螢幕尺寸的表單，無論使用何種裝置都能擁有最佳的使用者體驗。

## 以回應式模式預覽不同裝置上的表單情況

位於通用編輯器畫面右上角的&#x200B;**模擬器**&#x200B;圖示，讓您能夠以不同的裝置尺寸預覽頁面，以及測試回應式設計的行為，打造更好的使用者體驗。

若要以回應式模式預覽表單：

1. 在通用編輯器中開啟表單進行編輯。
2. 按一下工具列中的![顯示裝置預覽符號的模擬器圖示](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} 圖示。
3. 選取一種裝置格式：
   - 桌上型電腦 (預設)
   - 平板電腦
   - 行動裝置
   - 自訂 (指定寬度和高度)

![通用編輯器的螢幕擷圖，顯示不同裝置的回應式模式選項](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

在平板電腦或行動裝置上預覽時，您也可以使用&#x200B;**螢幕旋轉器**&#x200B;圖示，切換縱向和橫向檢視。

通用編輯器提供不同的模擬器，可以預覽在各種裝置上的表單。以下表格列出可用的模擬器類型，及其代表的相應裝置：

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">模擬器類型</th>
        <th style="width: 80%">裝置影像</th>
    </tr>
    <tr>
        <td style="width: 20%">桌上型電腦</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="表單的桌上型電腦視圖，顯示全寬版面" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">平板電腦</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="表單的平板電腦視圖，顯示中等寬度版面且元件有所調整" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">行動裝置</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="表單的行動裝置視圖，顯示窄版面且有堆疊的元件" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">自訂裝置</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="表單的自訂裝置視圖，顯示使用者指定的維度" style="width: auto; height: auto"></td>
    </tr>
</table>

## 版面配置功能

通用編輯器讓您能夠建立易於使用的表單，為一般使用者提供動態體驗。表單版面會控制項目或元件在表單中的顯示方式。

通用編輯器支援以下類型的表單版面：

- [面板版面](#panel-layout)
- [精靈版面](#wizard-layout)
- [摺疊式版面](#accordion-layout)

### 面板版面

面板版面對於組織相關欄位而言非常實用，可以更輕鬆地導覽和尋找相應內容。面板版面會將表單元件排列在表單中的不同區段或面板內。

![面板版面呈現出表單內的多個不同區段](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**舉例：**&#x200B;工作申請表單可能會使用面板將「個人資訊」、「教育程度」、「工作經驗」和「推薦人」分成不同的區段。

**回應式行為：**&#x200B;在較小的螢幕上，面板通常會垂直堆疊，維持多個不同的分組，同時調整為較窄的寬度。

您可以使用[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)在表單中新增面板版面。如需有關如何設定面板元件各種屬性的詳細說明，請參閱「[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)」一文。

### 精靈版面

精靈版面會將複雜的表單拆解為不同步驟，藉此將表單簡化。每個步驟都代表流程的不同部分，使用者依序導覽各步驟，通常會使用&#x200B;**下一步**&#x200B;和&#x200B;**返回**&#x200B;按鈕。您可以使用精靈版面來建立包含多個區段或步驟的表單。

![精靈版面呈現擁有導覽控制項的多步驟表單](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**舉例：**&#x200B;保險索賠表單可能會使用精靈來引導使用者提供事件詳細資訊、上傳證據、輸入個人資訊，以及檢閱提交內容。

**回應式行為：**&#x200B;在行動裝置上，精靈會維持其逐步操作的方式，但調整每個步驟中的內容以符合較窄的螢幕，通常會將在大螢幕上並排顯示的元素堆疊起來。

您可以使用[精靈元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)在表單中新增精靈版面。如需有關如何設定精靈元件各種屬性的詳細說明，請參閱「[精靈元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)」一文。

### 摺疊式版面

摺疊式版面以自適應表單中的可摺疊區段或面板來顯示內容。當某個區段展開時，會顯示其中的內容，而其他區段則保持摺疊狀態。這種版面非常適合以精簡的表單顯示大量資訊。

![摺疊式版面呈現出表單中可展開的區段](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**舉例：**&#x200B;產品設定表單可能會使用摺疊區段來顯示「基本選項」、「進階功能」、「配件」和「付款計劃」，讓使用者一次只需注意一個方面。

**回應式行為：**&#x200B;摺疊式版面在行動裝置上的效果特別好，僅顯示已展開的內容區段，自然地省下垂直空間，非常適合在小螢幕上顯示。

您可以使用[摺疊式元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)在表單中新增摺疊式版面。如需有關如何設定摺疊式元件各種屬性的詳細說明，請參閱「[摺疊式元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)」一文。

### 如何選擇合適的版面？

選取合適的版面，才能讓使用者體驗及表單功能最佳化。以下表格能協助您了解可用的不同版面選項，並引導您根據特定需求和使用案例選取最合適的版面：

| 功能 | 面板版面 | 精靈版面 | 摺疊式版面 |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **用途** | 將相關的內容分組到不同的區段 | 引導使用者完成多步驟流程或表單 | 將內容組織為可摺疊的區段 |
| **結構** | 不同的區段 | 連續的步驟/頁面 | 可摺疊的面板/區段 |
| **導覽** | 按一下面板標頭進行導覽 | - 往前：「下一步」按鈕<br>- 往回：「返回」按鈕<br>- 選擇性跳過步驟 | 按一下標頭可展開/摺疊區段 |
| **使用者體驗** | 以可管理的方式組織大量內容 | 逐步引導，減輕負荷 | 使用展開/摺疊區段呈現精簡視圖 |
| **使用案例** | 具有分類區段的複雜表單 | 設定流程、複雜的表單 | 常見問題集、設定選單、詳細的內容區段 |
| **適合行動裝置的程度** | 中等：面板會垂直堆疊 | 良好：僅聚焦於目前的步驟 | 極佳：可摺疊的區段能節省空間 |

## 回應式表單的最佳實務

為了確保您的表單在所有裝置上皆能提供最佳體驗，請遵循以下最佳實務：

1. **優先針對行動裝置進行設計：**&#x200B;一開始先以行動裝置為主體設計表單，然後再針對更大的螢幕進行增強。此方法能確保核心功能在最小的螢幕上也可正常運作。

2. **使用適當的欄位類型：**&#x200B;選擇適合觸控裝置的欄位類型：
   - 當有多個選項時，使用下拉式選單而非單選按鈕
   - 使用專為觸控輸入設計的日期選擇器
   - 確保按鈕和觸控目標至少為 44px x 44px

3. **針對小螢幕進行簡化：**
   - 在行動裝置上每行顯示較少的欄位數
   - 考慮將選用欄位隱藏在「顯示更多」選項後面
   - 在行動裝置上將複雜的表單拆解為更多步驟

4. **全面測試：**&#x200B;務必在實際的裝置上，或使用通用編輯器中的模擬器模式測試您的表單，確保在各種尺寸的螢幕上皆可正常運作。

5. **考量載入時間：**&#x200B;將影像大小最佳化，並將所需資源減至最低，特別是對於連線速度較慢的行動裝置使用者。

## 回應式表單疑難排解

| 問題 | 可能的原因 | 解決方案 |
|-------|---------------|----------|
| 表單在行動裝置上顯示為截斷狀態 | 固定寬度設定或有溢出問題 | 使用相對單位 (%、rem) 而非像素，並檢查 overflow:hidden 屬性 |
| 觸控元素互動困難 | 觸控目標太小或相距太近 | 將按鈕/輸入尺寸增加到至少 44px x 44px，並加大互動元素之間的空間 |
| 小螢幕上有內容溢出情形 | 較小的檢視區沒有回應式規則 | 新增媒體查詢或回應式類別來調整不同螢幕尺寸的版面 |
| 行動裝置上的表單載入太慢 | 有大型影像或過多指令碼 | 將影像最佳化、JavaScript 最小化，並考慮讓非關鍵元素延遲載入 |
| 模擬器和實際裝置間的顯示差異 | 瀏覽器特定的轉譯或裝置變化版本 | 盡可能在實際的裝置上進行測試，而非僅使用模擬器 |

## 另請參閱

{#see-more-eds-forms}
