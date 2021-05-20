---
title: 使用隱藏條件
description: 隱藏條件可用來判斷元件資源是否已呈現。
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
source-git-commit: fa3280defb2a97954c5ab1b70e7600382e370606
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# 使用隱藏條件{#using-hide-conditions}

隱藏條件可用來判斷元件資源是否已呈現。 範本作者在[範本編輯器](/help/sites-cloud/authoring/features/templates.md)中設定核心元件[清單元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html)並決定停用根據子頁面建立清單的選項時，就會是這個例子。 在設計對話框中禁用此選項會設定一個屬性，以便在呈現清單元件時計算隱藏條件，並且不顯示顯示子頁的選項。

## 概覽 {#overview}

對話方塊可能會變得非常複雜，用戶可能只使用其可支配選項的一小部分。 這可能導致使用者的使用者介面體驗過量。

使用隱藏條件，管理員、開發人員和超級使用者就能根據一組規則來隱藏資源。 此功能可讓作者決定當作者編輯內容時應顯示哪些資源。

>[!NOTE]
>
>根據運算式隱藏資源不會取代ACL權限。 內容仍可編輯，但不會顯示。

## 實作與使用詳細資料{#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 負責根據屬性的存在和值來篩選 `granite:hide` 資源，此屬性位於要篩選的欄位上。`/libs/cq/gui/components/authoring/dialog/dialog.jsp`的實作包含`FilteringResourceWrapper.`的例項

實作會使用Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html)並透過ExpressionCustomizer新增`cqDesign`自訂變數。

以下是位於`etc/design`下或作為「內容策略」的設計節點上隱藏條件的一些示例。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定義隱藏運算式時請記住：

* 為了有效，應表示找到屬性的範圍(例如`cqDesign.myProperty`)。
* 值為唯讀。
* 函式（如有需要）應限於服務提供的指定集。

## 範例 {#example}

您可以在AEM中找到隱藏條件的範例，尤其是[核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)。 例如，請考慮[清單核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html)，如[WKND教學課程中實作。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

[範本作者可使用範本編輯器](/help/sites-cloud/authoring/features/templates.md)，在設計對話方塊中定義頁面作者可使用的清單元件選項。例如是否允許該清單為靜態清單、子頁清單、標籤頁清單等。 可啟用或停用。

如果範本作者選擇停用子頁面選項，則會設定設計屬性並據此評估隱藏條件，導致選項無法為頁面作者呈現。

1. 依預設，頁面作者可使用清單核心元件，透過選擇&#x200B;**Child pages**&#x200B;選項，使用子頁面來建立清單。

   ![清單元件設定](assets/hide-conditions-list-settings.png)

1. 在清單核心元件的設計對話方塊中，範本作者可選擇選項&#x200B;**停用子項**，以防止將根據子頁面產生清單的選項顯示給頁面作者。

   ![清單元件設計對話方塊](assets/hide-conditions-list-design.png)

1. 在`/conf/wknd/settings/wcm/policies/wknd/components/list`下建立策略節點，其屬性`disableChildren`設定為`true`。

   ![隱藏條件的節點結構](assets/hide-conditions-node-structure.png)

1. 隱藏條件定義為對話屬性節點`/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`上`granite:hide`屬性的值

   ![隱藏條件的評估](assets/hide-conditions-evaluation.png)

1. 從設計配置提取`disableChildren`值，表達式`${cqDesign.disableChildren}`評估為`false`，這表示將不會在元件中呈現該選項。

1. 使用清單元件時，頁面作者不再轉譯&#x200B;**子頁面**&#x200B;選項。

   ![禁用子選項的清單元件](assets/hide-conditions-child-disabled.png)
