---
title: 擴充通用編輯器
description: 瞭解擴充Universal Editor功能的不同選項，以支援內容作者的需求。
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0cab4a807be4aa402667feddb6a948f0d2db371f
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# 擴充通用編輯器 {#extending}

瞭解擴充Universal Editor功能的不同選項，以支援內容作者的需求。

>[!TIP]
>
>Universal Editor也提供數個[自訂選項，](/help/implementing/universal-editor/customizing.md)可讓您更符合專案需求。

## 擴充功能 {#extensions}

作為Adobe Experience Cloud服務，Universal Editor的UI可以使用App Builder和Experience Manager進行擴充。 Adobe提供許多您專案可使用的現成擴充功能。

* **[Universal Editor的AEM產品選擇器](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**：從編輯器選取或移除產品資料，以整合Adobe Commerce資料。
* **[通用編輯器內容草稿](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**：建立、編輯及管理多個內容草稿。
* **[可設定的資產選取器](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**：啟用從已編輯頁面所使用存放庫以外的存放庫選取資產。
* **Forms規則編輯器**：以視覺化方式將動態行為新增至AEM Forms欄位，無需編碼。
* **[將內容片段匯出至Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**：將在Adobe Experience Manager as a Cloud Service中建立的內容片段匯出至Adobe Target，以在Target活動中作為選件使用，以大規模測試並個人化體驗。
* **[內容片段工作流程](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**：起始所選內容片段的AEM工作流程。

## 擴充UI {#extending-ui}

Universal Editor的UI擴充功能是使用Adobe App Builder建置的JavaScript應用程式。 使用這些相同的工具，您還可以將自己的按鈕和動作新增到頁首選單和屬性面板，並為通用編輯器建立自己的事件。

如果您想探索建立自己的擴充功能的可能性，請參閱下列資源：

1. [UI擴充功能](https://developer.adobe.com/uix/docs/) — 這是UI擴充功能的開發人員檔案。
1. [UI擴充性指南](https://developer.adobe.com/uix/docs/guides/) — 如何開發您自己的擴充功能的逐步指示
1. [通用編輯器UI擴充點數](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) — 通用編輯器專用的擴充點數檔案

>[!TIP]
>
>如果您偏好以範例學習，請參閱[AEM UI擴充功能教學課程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview)。 雖然重點在於擴充內容片段主控台，但在通用編輯器中實作UI擴充功能的概念是相同的。

[在AEM Sites中使用Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)，您可以為每個執行個體啟用或停用擴充功能、存取Adobe的第一方擴充功能（包括Universal Editor的擴充功能）等等。

## 延伸點 {#extension-points}

除了UI擴充功能外，通用編輯器還提供許多其他彈性的擴充點，以實現自訂業務需求的順暢整合。

* **[區塊](/help/edge/developer/block-collection.md)**：在簡單的JSON格式中，專案可以調整可用於內容建立的區塊和UE功能。
* **[自訂使用者介面](#extending-ui)**：擴充功能可以在側面板或模型對話方塊中顯示必要的UI。
* **[事件](/help/implementing/universal-editor/events.md)**：擴充功能會收到有關作者在頁面上的動作和選取專案的事件，以適當地回應。
