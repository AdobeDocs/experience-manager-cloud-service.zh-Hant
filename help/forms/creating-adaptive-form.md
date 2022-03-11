---
title: 如何建立自適應表單？
description: '瞭解如何使用 [!DNL Experience Manager Forms]。 自適應Forms是可以簡化資訊收集和處理的響應性HTML5表。 更深入地瞭解如何基於表單資料模型和XML或JSON架構建立自適應表單。 '
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 1%

---

# 建立最適化表單 {#creating-an-adaptive-form}

自適應Forms允許您建立具有吸引力、響應性、動態性和適應性的表單。 [!DNL AEM Forms] 提供了直觀的用戶介面和開箱即用的元件，用於建立和使用AdaptiveForms。 您可以選擇基於表單模型或模式或不使用表單模型建立自適應表單。 必須仔細選擇不僅適合您的要求，而且擴展您現有的基礎設施投資和資產的表單模式。 您可以從以下選項中進行選擇以建立自適應表單：

* **使用表單資料模型**
   [資料整合](data-integration.md) 允許您將來自不同資料源的實體和服務整合到一個表單資料模型中，您可以使用該模型建立自適應Forms。 如果要建立的自適應表單涉及從多個資料源讀取和寫入資料，請選擇「表單資料模型」。

   <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. -->

* **使用XML架構定義(XSD)或JSON架構**
XML和JSON架構表示組織中後端系統生成或使用資料的結構。 可以將模式與自適應表單相關聯，並使用其元素將動態內容添加到自適應表單。 創作自適應Forms時，模式的元素將可用於內容瀏覽器的「資料模型對象」頁籤中。

* **使用無或沒有表單模型**
使用此選項建立的自適應Forms不使用任何窗體模型。 從這些表單生成的資料XML具有帶欄位和相應值的扁平結構。

## 先決條件

您需要使用以下命令建立「自適應表單」：

* 自適應表單模板。 模板提供基本結構並定義自適應表單的外觀（佈局和樣式）。 它具有預格式化的元件，包含某些屬性和內容結構。 [建立新模板](template-editor.md)，導入現有模板，或下載並導入一些 [示例模板](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:3f89abe1-0ece-492a-b5af-57c73badad52)。
* 自適應窗體主題。 主題包含元件和面板的樣式詳細資訊。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 應用主題時，指定的樣式將反映在相應的元件上。 你可以 [建立新主題](themes.md)。 [導入現有主題](import-export-forms-templates.md#uploading-a-theme)，或下載並導入 [示例主題](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:2779f80e-16ba-4cd1-a96f-8e2b53f3be25)。
* 將用戶添加到 [!DNL forms-users] 為他們提供建立自適應表單的權限。 有關特定用戶組的表單的詳細清單，請參見 [組和權限](forms-groups-privileges-tasks.md)。

## 建立最適化表單 {#strong-create-an-adaptive-form-strong}

按照以下步驟建立「自適應表單」。

1. 訪問 [!DNL Experience Manager Forms] 作者實例。 它可以是雲實例或本地開發實例。

1. 在Experience Manager登錄頁上輸入憑據。

   登錄後，在左上角，點擊 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。

1. 點擊 **[!UICONTROL 建立]** 選擇 **[!UICONTROL 自適應窗體]**。 選擇模板並點擊 **[!UICONTROL 下一個]**。
1. 一個選項 **[!UICONTROL 添加屬性]** 的子菜單。 指定以下屬性欄位的值。 「標題」(Title)和「名稱」(Name)欄位是必填的：

   * **[!UICONTROL 標題：]** 指定窗體的顯示名稱。 標題可幫助您在 [!DNL Experience Manager Forms] 用戶介面。
   * **[!UICONTROL 名稱：]** 指定窗體的名稱。 在儲存庫中建立具有指定名稱的節點。 開始鍵入標題時，將自動生成名稱欄位的值。 您可以更改建議的值。 名稱欄位只能包含字母數字字元、連字元和下划線。 所有無效輸入都用連字元替換。
   * **[!UICONTROL 描述：]** 指定有關表單的詳細資訊。
   * **[!UICONTROL 標籤：]** 指定用於唯一標識自適應表單的標籤。 標籤在搜索窗體中的幫助。 要建立標籤，請在 **[!UICONTROL 標籤]** 框。

1. 可以基於以下表單模型之一建立自適應表單：

   * [表單資料模型](#fdm)

   <!--* [XFA form template](#create-an-adaptive-form-based-on-an-xfa-form-template)-->
   * [XML或JSON架構](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 無或沒有任何窗體模型

   您可以從 **[!UICONTROL 窗體模型]** 的 **[!UICONTROL 添加屬性]** 的子菜單。 預設情況下，所選的表單模型為 **[!UICONTROL 無]**。

1. 點擊 **[!UICONTROL 建立]**。 將建立「自適應表單」，並出現一個用於開啟表單進行編輯的對話框。

1. 點擊 **[!UICONTROL 開啟]** 的子菜單。 此窗體開啟以進行編輯，並顯示模板中的可用內容。 它還顯示邊欄，以根據需要定制新建立的表單。

   根據「自適應表單」的類型，在關聯的 <!--XFA form template, -->XML架構或JSON架構顯示在 **[!UICONTROL 資料模型對象]** 頁籤 **[!UICONTROL 內容瀏覽器]** 欄。 也可以拖放這些元素來構建自適應表單。

## 基於表單資料模型建立自適應表單 {#fdm}

[資料整合](data-integration.md) 允許您整合多個資料源，並將其實體和服務組合在一起以建立表單資料模型。 它是JSON架構的擴展。 可以使用「表單資料模型」建立「自適應表單」。 在「表單資料模型」中配置的實體或資料模型對象可用作表單創作的資料模型對象。 它們綁定到各自的資料源，用於預填表單並將提交的資料寫回各自的資料源。 您還可以使用自適應表單規則調用在表單資料模型中配置的服務。

要使用表單資料模型建立自適應表單：

1. 在「添加屬性」螢幕的「表單模型」頁籤中，選擇 **[!UICONTROL 窗體資料模型]** 的 **[!UICONTROL 從中選擇]** 的子菜單。

   ![建立最適化表單](assets/create-af-1-1.png)

1. 點擊以展開 **[!UICONTROL 選擇表單資料模型]**。 列出所有可用表單資料模型。從資料模型中選擇。

>[!NOTE]
>
>也可更改自適應表單的表單資料模型。 有關詳細步驟，請參見 [編輯自適應表單的表單模型屬性](#edit-form-model)。

## 基於XML或JSON架構建立自適應表單 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML和JSON架構表示組織中後端系統生成或使用資料的結構。 可以將模式與自適應表單相關聯，並使用其元素將動態內容添加到自適應表單。 模式的元素可在內容瀏覽器的「資料模型對象」頁籤中用於創作自適應Forms。 可以拖放架構元素以構建表單。

請參閱以下文檔，瞭解如何設計XML或JSON架構以創作AdaptiveForms。

* [使用XML架構建立自適應Forms](adaptive-form-xml-schema-form-model.md)
* [使用JSON架構建立自適應Forms](adaptive-form-json-schema-form-model.md)

執行以下操作以將XML或JSON架構用作自適應表單的表單模型：

1. 在 **[!UICONTROL 添加屬性]** 在「自適應表單建立」頁的步驟中，按一下 **[!UICONTROL 窗體模型]** 頁籤。
1. 在「表單模型」(Form Model)頁籤中，選擇 **[!UICONTROL 架構]** 從 **[!UICONTROL 從中選擇]** 下拉欄位。

1. 點擊 **[!UICONTROL 選擇方案]** 並執行以下操作之一：

   * **[!UICONTROL 從磁碟上載]**  — 選擇此選項，然後點擊「上載架構定義」以瀏覽並從檔案系統上載XML架構或JSON架構。 上載的架構檔案駐留在窗體中，其他AdaptiveForms無法訪問。
   * **[!UICONTROL 在儲存庫中搜索]**  — 選擇此選項可從儲存庫中可用的架構定義檔案清單中選擇。 選擇XML或JSON架構檔案作為表單模型。 所選模式通過引用與表單關聯，並且可以在其它自適應Forms中使用。

      確保JSON架構檔案名以結尾 **.schema.json**。 例如：mySchema.schema.json
   ![選擇XML或JSON架構](assets/upload-schema.png)
   **圖：** *選擇XML或JSON架構*

1. （僅適用於XML架構）在選擇或上載XML架構後，請指定要與Adaptive Form映射的選定XSD檔案的根元素。

   ![選擇XSD根元素](assets/xsd-root-element.png)
   **圖：** *選擇XSD根元素*

>[!NOTE]
>
>也可以更改自適應表單的模式。 有關詳細步驟，請參見 [編輯自適應表單的表單模型屬性](#edit-form-model)。

## 編輯自適應表單的表單模型屬性 {#edit-form-model}

建立自適應Forms時不使用表單模型（對表單模型使用「無」選項）或使用表單模型，如 <!-- form template, --> XML架構或JSON架構或表單資料模型。 可將「自適應表單」的表單模型從「無」更改為其它表單模型。 對於基於表單模型的自適應表單，可以選擇其他 <!-- form template,--> 同一表單模型的XML架構、JSON架構或表單資料模型。 但是，不能將一個表單模型更改為另一個表單模型。

1. 選擇「自適應表單」並點擊 **屬性** 表徵圖
1. 開啟 **[!UICONTROL 窗體模型]** ，然後執行以下操作之一。

   * 如果「自適應表單」沒有表單模型，則可以選擇另一個表單模型，並相應地選擇 <!-- a form template, --> XML或JSON架構或表單資料模型。
   * 如果「自適應表單」基於表單模型，則可以選擇其他 <!-- form template, --> XML或JSON架構，或同一表單模型的表單資料模型。

1. 點擊 **[!UICONTROL 保存]** 的子菜單。
