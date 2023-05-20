---
title: 使用隱藏條件
description: 隱藏條件可用於確定是否呈現元件資源。
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 2%

---

# 使用隱藏條件 {#using-hide-conditions}

隱藏條件可用於確定是否呈現元件資源。 一個示例是模板作者配置核心元件時 [清單元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) 的 [模板編輯器](/help/sites-cloud/authoring/features/templates.md) 並決定禁用基於子頁構建清單的選項。 在設計對話框中禁用此選項會設定屬性，以便在呈現清單元件時，將評估隱藏條件，並且不顯示顯示子頁的選項。

## 概觀 {#overview}

對話框可能會變得非常複雜，用戶可能只使用其可用選項的一小部分。 這可能給用戶帶來壓倒性的用戶介面體驗。

通過使用隱藏條件，管理員、開發人員和超級用戶可以根據一組規則來隱藏資源。 此功能允許作者在編輯內容時決定應顯示哪些資源。

>[!NOTE]
>
>基於表達式隱藏資源不會替換ACL權限。 內容仍然可編輯，但不顯示。

## 實施和使用詳細資訊 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 負責根據資源的存在和價值 `granite:hide` 屬性，位於要篩選的欄位上。 執行 `/libs/cq/gui/components/authoring/dialog/dialog.jsp` 包括 `FilteringResourceWrapper.`

實現利用花崗岩 [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) 並添加 `cqDesign` 通過ExpressionCustomizer自定義變數。

下面是設計節點上隱藏條件的幾個示例，該節點位於 `etc/design` 或內容策略。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定義隱藏表達式時，請牢記：

* 要有效，應表示找到屬性的範圍(例如， `cqDesign.myProperty`)。
* 值為只讀。
* 功能（如果需要）應限於服務提供的給定集。

## 範例 {#example}

可以在以下各處找到隱藏條AEM件的示例： [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 尤其是。 例如，請考慮 [清單核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) 如 [WKND教程。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

[使用模板編輯器](/help/sites-cloud/authoring/features/templates.md)，模板作者可以在設計對話框中定義頁面作者可使用的清單元件選項。 例如，是否允許清單為靜態清單、子頁清單、標籤頁清單等。 可以啟用或禁用。

如果模板作者選擇禁用子頁面選項，則會設定設計屬性並針對其評估隱藏條件，這將導致該選項不呈現給頁面作者。

1. 預設情況下，頁面作者可以使用清單核心元件通過選擇選項來使用子頁面構建清單 **子頁**。

   ![清單元件設定](assets/hide-conditions-list-settings.png)

1. 在清單核心元件的設計對話框中，模板作者可以選擇選項 **禁用子項** 以防止基於子頁生成清單的選項顯示給頁面作者。

   ![「清單元件設計」對話框](assets/hide-conditions-list-design.png)

1. 策略節點建立於 `/conf/wknd/settings/wcm/policies/wknd/components/list` 帶有 `disableChildren` 設定為 `true`。

   ![隱藏條件的節點結構](assets/hide-conditions-node-structure.png)

1. 隱藏條件定義為 `granite:hide` 對話框屬性節點上的屬性 `/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`

   ![隱藏條件的評估](assets/hide-conditions-evaluation.png)

1. 值 `disableChildren` 從設計配置和表達式中拉出 `${cqDesign.disableChildren}` 求 `false`，表示選項不會作為元件的一部分呈現。

1. 選項 **子頁** 在使用清單元件時不再為頁面作者呈現。

   ![禁用子選項的清單元件](assets/hide-conditions-child-disabled.png)
