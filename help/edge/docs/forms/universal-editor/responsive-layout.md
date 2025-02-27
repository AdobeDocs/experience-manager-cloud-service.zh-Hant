---
title: 瞭解通用編輯器 — 回應式模式
description: 本文說明如何使用通用編輯器中的不同模擬器預覽表單，以視覺化方式呈現表單在製作期間的外觀。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 8f5b4d863ab469c44b4c221eab1fb128706b45c7
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 2%

---

# WYSIWYG製作中的回應式模式

<span class="preview">此功能可透過搶先存取計畫使用。 若要要求存取權，請從您的正式地址傳送電子郵件至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，其中包含您的GitHub組織名稱和存放庫名稱。 例如，如果存放庫URL是https://github.com/adobe/abc，組織名稱是adobe，存放庫名稱是abc。</span>


[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)可讓您使用不同的模擬器預覽Edge Delivery Services Forms，以檢視表單在製作過程中的外觀。

回應式模式可讓開發人員設計可自動適應不同熒幕大小的版面，包括桌上型電腦、平板電腦和行動裝置。 Universal Editor支援適用於桌上型電腦、平板電腦和行動裝置的模擬器。 您可以根據熒幕大小設定高度和寬度，並執行下列動作：

* 設定方向
* 指定寬度和高度
* 變更方向

## 在不同裝置的回應模式下預覽Forms

通用編輯器在熒幕右上角提供&#x200B;**模擬器**&#x200B;圖示，可讓您預覽不同裝置大小的頁面，並測試回應式設計的行為，以獲得更佳的使用者體驗。

若要檢視Universal Editor在不同熒幕大小上呈現表單的方式，請執行以下步驟：

1. 在通用編輯器中開啟表單以進行編輯。
1. 選取通用編輯器工具列上可用的![模擬器圖示](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%，width=2%}，然後按一下模擬器圖示以顯示選項。

   ![回應模式](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

1. 選取要在所選裝置上模擬通用編輯器中表單的選項：案頭、平板電腦、行動裝置。

   ![回應式模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=40%，height=40%}

   依預設，編輯器會在案頭版面配置中開啟，其高度和寬度由瀏覽器自動決定。 或者，您也可以模擬行動裝置或平板電腦裝置上的表單。 您也可以自訂自訂裝置的熒幕寬度和高度。

通用編輯器提供不同的模擬器來預覽不同裝置上的表單。 下表列出可用的模擬器型別及其對應的裝置表示法：

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">模擬器型別</th>
        <th style="width: 80%">裝置影像</th>
    </tr>
    <tr>
        <td style="width: 20%">桌上型電腦</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="案頭模擬器" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">平板電腦</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="平板電腦模擬器" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">行動</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="行動模擬器" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">自訂裝置</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="自訂裝置模擬器" style="width: auto; height: auto"></td>
    </tr>
</table>

在不同裝置上預覽表單時，您可以使用&#x200B;**熒幕旋轉器**&#x200B;圖示，在直向與橫向之間切換。 它可協助開發人員測試回應式設計如何適應各種裝置上的熒幕旋轉。

Universal Editor支援各種表單版面。 若要探索不同的配置，請參閱[配置功能](#layout-capabilities)區段。

## 佈局功能

Universal Editor可讓您建立易於使用的表單，為使用者提供動態體驗。 表單版面配置會控制專案或元件在表單中的顯示方式。

Universal Editor支援下列型別的表單版面：
* [面板版面配置](#panel-layout)
* [精靈配置](#wizard-layout)
* [收合式選單版面](#accordion-layout)

### 面板布局

面板版面配置很適合用來組織相關欄位，讓您更輕鬆地導覽及尋找對應內容。 面板配置會將表單元件排列在表單的不同區段或面板中。

![面板配置](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

您可以使用[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)，在表單中新增面板配置。 如需如何設定面板元件各種屬性的詳細指示，請參閱[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)文章。

### 精靈配置


精靈配置將複雜表單分成不同的步驟，有助於簡化表單。 每個步驟代表流程的不同部分，使用者會依序瀏覽各個步驟，通常使用&#x200B;**下一步**&#x200B;和&#x200B;**上一步**&#x200B;按鈕。 您可以使用精靈版面配置來建立包含多個區段或步驟的表單。

![精靈配置](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

您可以使用[精靈元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)在表單中新增精靈配置。 如需有關如何設定精靈元件各種屬性的詳細指示，請參閱[精靈元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)文章。

### 收合式選單版面配置

摺疊式功能表佈局會以最適化表單的可摺疊區段或面板顯示內容。 展開區段時，會在其中顯示內容，而其他區段仍會保持收合狀態。 此版面適合以精簡格式顯示大量資訊。

![收合式選單配置](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

您可以使用[摺疊式功能表元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)，在表單中新增摺疊式功能表配置。 如需如何設定摺疊式功能表元件的各種屬性的詳細指示，請參閱[摺疊式功能表元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)文章。

### 如何選擇正確的版面？

請務必選擇正確的版面以最佳化使用者體驗和表單功能。 此表格可協助您瞭解可用的不同版面配置選項，並引導您根據特定需求和使用案例選取最適合的版面：

| 功能 | 面板布局 | 精靈配置 | 收合式選單版面配置 |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **用途** | 將相關內容分組為不同的區段 | 引導使用者完成多步驟流程或表單 | 將內容組織成可摺疊的區段 |
| **結構** | 不同的區段 | 循序步驟/頁面 | 可摺疊面板/區段 |
| **導覽** | 按一下面板標題以進行導覽 |  — 前進：「下一步」按鈕<br> — 後退：「後退」按鈕<br> — 選擇性略過步驟 | 按一下標題可展開/收合區段 |
| **使用者體驗** | 以可管理的方式組織大量內容 | 逐步指導，減少負擔 | 具有展開/收合區段的精簡檢視 |
| **使用案例** | 具有已分類區段的複雜表單 | 設定程式、複雜表單 | 常見問題集、設定功能表、詳細內容區段 |

## 另請參閱

{{universal-editor-see-also}}
