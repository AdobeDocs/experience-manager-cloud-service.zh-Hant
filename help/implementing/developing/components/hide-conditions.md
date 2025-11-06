---
title: 使用隱藏條件
description: 隱藏條件可用於判斷元件資源是否已轉譯。
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 1%

---

# 使用隱藏條件 {#using-hide-conditions}

隱藏條件可用於判斷元件資源是否已轉譯。 例如，範本作者在[範本編輯器](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html?lang=zh-Hant)中設定核心元件[list元件](/help/sites-cloud/authoring/page-editor/templates.md)，並決定停用根據子頁面建立清單的選項。 在「設計」對話方塊中停用此選項會設定屬性，以便在轉譯清單元件時，會評估隱藏條件，且不顯示顯示子頁面的選項。

## 概觀 {#overview}

對話方塊可能會變得非常複雜，使用者可能會使用許多選項，而他們只能使用一小部分可用的選項。 這可能會導致使用者無法承受的使用者介面體驗。

透過使用隱藏條件，管理員、開發人員和超級使用者便能根據一組規則來隱藏資源。 此功能可讓他們決定在作者編輯內容時應該顯示哪些資源。

>[!NOTE]
>
>根據運算式隱藏資源不會取代ACL許可權。 內容仍可編輯，但不會顯示。

## 實作與使用細節 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper`負責根據`granite:hide`屬性的存在與值來篩選資源，該屬性位於要篩選的欄位上。 `/libs/cq/gui/components/authoring/dialog/dialog.jsp`的實作包含`FilteringResourceWrapper.`的執行個體

實作使用Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html)，並透過ExpressionCustomizer新增`cqDesign`自訂變數。

以下是位於`etc/design`下或作為內容原則之設計節點上的幾個隱藏條件範例。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定義隱藏運算式時，請牢記以下事項：

* 若要有效，應該表示找到屬性的範圍（例如`cqDesign.myProperty`）。
* 值是唯讀的。
* 功能（如有需要）應限製為服務提供的一組給定值。

## 範例 {#example}

隱藏條件的範例可在整個AEM中找到，特別是[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)。 例如，將[清單核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html?lang=zh-Hant)視為在[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)中實作。

[使用範本編輯器](/help/sites-cloud/authoring/page-editor/templates.md)，範本作者可以在設計對話方塊中定義清單元件中哪些選項可供頁面作者使用。 您可以啟用或停用選項，例如是否允許清單成為靜態清單、子頁面清單、標籤頁面清單等。

如果範本作者選擇停用子頁面選項，則會設定設計屬性，並評估其隱藏條件，導致該選項無法針對頁面作者呈現。

1. 依預設，頁面作者可以使用清單核心元件，透過選擇選項&#x200B;**子頁面**&#x200B;來使用子頁面建立清單。

   ![列出元件設定](assets/hide-conditions-list-settings.png)

1. 在清單核心元件的「設計」對話方塊中，範本作者可以選擇選項&#x200B;**停用子項**，以防止根據子頁面產生清單的選項顯示給頁面作者。

   ![清單元件設計對話方塊](assets/hide-conditions-list-design.png)

1. 原則節點是在`/conf/wknd/settings/wcm/policies/wknd/components/list`下建立，屬性`disableChildren`設定為`true`。

   ![隱藏條件的節點結構](assets/hide-conditions-node-structure.png)

1. 隱藏條件定義為對話方塊屬性節點`granite:hide`上`/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`屬性的值

   ![隱藏條件的評估](assets/hide-conditions-evaluation.png)

1. 從設計組態中提取`disableChildren`的值，而運算式`${cqDesign.disableChildren}`評估為`false`，表示選項將不會呈現為元件的一部分。

1. 使用清單元件時，不再為頁面作者轉譯選項&#x200B;**子頁面**。

   ![已停用子選項的List元件](assets/hide-conditions-child-disabled.png)
