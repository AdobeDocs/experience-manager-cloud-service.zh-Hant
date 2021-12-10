---
title: 如何建立最適化表單？
description: '了解如何使用 [!DNL Experience Manager Forms]. 適用性Forms是回應式HTML5表單，可簡化資訊收集和處理。 進一步了解如何根據表單資料模型和XML或JSON結構建立最適化表單。 '
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 0%

---

# 建立最適化表單 {#creating-an-adaptive-form}

適用性Forms可讓您建立吸引人、回應式、動態且最適化的表單。 [!DNL AEM Forms] 提供直覺式使用者介面和現成可用的元件，供您建立及使用適用性Forms。 您可以選擇根據表單模型或架構建立適用性表單，或不使用表單模型。 必須仔細選擇不僅符合您要求而且擴展您現有基礎設施投資和資產的表單模型。 您可以從下列選項中選擇以建立最適化表單：

* **使用表單資料模型**
   [資料整合](data-integration.md) 可讓您將不同資料來源的實體和服務整合到表單資料模型中，以便用來建立適用性Forms。 如果您建立的適用性表單涉及從多個資料來源擷取資料並將其寫入多個資料來源，請選擇「表單資料模型」。

   <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. -->

* **使用XML結構定義(XSD)或JSON結構**
XML和JSON結構代表組織內的後端系統產生或使用資料的結構。 您可以將結構與適用性表單建立關聯，並使用其元素將動態內容新增至適用性表單。 製作最適化Forms時，架構的元素將可用於內容瀏覽器的「資料模型物件」標籤。

* **無或不使用表單模型**
使用此選項建立的適用性Forms不使用任何表單模型。 從這種表單生成的資料XML具有帶有欄位和相應值的扁平結構。

## 先決條件

您需要下列項目才能建立最適化表單：

* 最適化表單範本。 範本提供基本結構並定義最適化表單的外觀（配置和樣式）。 它具有預先格式化的元件，包含某些屬性和內容結構，您可以 [建立新範本](template-editor.md)，請匯入現有範本，或下載並匯入一些 [範本](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:3f89abe1-0ece-492a-b5af-57c73badad52).
* 最適化表單主題。 主題包含元件和面板的樣式詳細資料。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 應用主題時，指定的樣式會反映在相應的元件上。 您可以 [建立新主題](themes.md), [導入現有主題](import-export-forms-templates.md#uploading-a-theme)，或下載並匯入 [範例主題](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:2779f80e-16ba-4cd1-a96f-8e2b53f3be25).
* 將使用者新增至 [!DNL forms-users] 提供建立最適化表單的權限。 如需特定使用者群組的表單詳細清單，請參閱 [群組和權限](forms-groups-privileges-tasks.md).

## 建立最適化表單 {#strong-create-an-adaptive-form-strong}

請依照下列步驟建立最適化表單。

1. 存取 [!DNL Experience Manager Forms] 製作例項。 可以是雲端例項或本機開發例項。

1. 在Experience Manager登入頁面上輸入您的憑證。

   登入後，在左上角，點選 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.

1. 點選 **[!UICONTROL 建立]** 選取 **[!UICONTROL 適用性表單]**. 選取範本並點選 **[!UICONTROL 下一個]**.
1. 選項 **[!UICONTROL 新增屬性]** 框。 指定下列屬性欄位的值。 標題和名稱欄位是必填欄位：

   * **[!UICONTROL 標題：]** 指定表單的顯示名稱。 標題可協助您識別 [!DNL Experience Manager Forms] 使用者介面。
   * **[!UICONTROL 名稱：]** 指定表單的名稱。 在儲存庫中建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議的值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。
   * **[!UICONTROL 說明：]** 指定有關表單的詳細資訊。
   * **[!UICONTROL 標籤：]** 指定用以唯一識別最適化表單的標籤。 標籤有助於搜尋表單。 若要建立標籤，請在 **[!UICONTROL 標籤]** 框。

1. 您可以根據下列其中一個表單模型建立適用性表單：

   * [表單資料模型](#fdm)

   <!--* [XFA form template](#create-an-adaptive-form-based-on-an-xfa-form-template)-->
   * [XML或JSON結構](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 無或沒有任何表單模型

   您可以透過 **[!UICONTROL 表單模型]** 標籤 **[!UICONTROL 新增屬性]** 頁面。 依預設，選取的表單模型為 **[!UICONTROL 無]**.

1. 點選 **[!UICONTROL 建立]**. 隨即建立適用性表單，並出現一個對話方塊以開啟表單以進行編輯。

1. 點選 **[!UICONTROL 開啟]** 在新頁簽中開啟新建立的窗體。 表單隨即開啟供編輯，並顯示範本中可用的內容。 它也會顯示邊欄，以根據需求自訂新建立的表單。

   根據最適化表單的類型，關聯 <!--XFA form template, -->XML結構或JSON結構會顯示在 **[!UICONTROL 資料模型物件]** 的 **[!UICONTROL 內容瀏覽器]** 欄。 您也可以拖放這些元素來建立最適化表單。

## 根據表單資料模型建立最適化表單 {#fdm}

[資料整合](data-integration.md) 可讓您整合多個資料來源，並將其實體和服務整合在一起，以建立表單資料模型。 此為JSON結構描述的擴充功能。 您可以使用表單資料模型來建立最適化表單。 在「表單資料模型」中配置的實體或資料模型對象可作為資料模型對象用於表單創作。 它們會系結至個別的資料來源，並用來預填表單，並將提交的資料寫回個別資料來源。 您也可以使用適用性表單規則呼叫在表單資料模型中設定的服務。

若要使用表單資料模型建立最適化表單：

1. 在「添加屬性」螢幕上的「表單模型」頁簽中，選擇 **[!UICONTROL 表單資料模型]** 在 **[!UICONTROL 從]** 下拉式清單。

   ![建立最適化表單](assets/create-af-1-1.png)

1. 點選以展開 **[!UICONTROL 選擇表單資料模型]**. 列出所有可用的表單資料模型。從資料模型中選擇。

>[!NOTE]
>
>您也可以變更最適化表單的表單資料模型。 如需詳細步驟，請參閱 [編輯最適化表單的表單模型屬性](#edit-form-model).

## 根據XML或JSON結構建立最適化表單 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML和JSON結構代表組織內的後端系統產生或使用資料的結構。 您可以將結構與適用性表單建立關聯，並使用其元素將動態內容新增至適用性表單。 結構的元素可在內容瀏覽器的「資料模型物件」標籤中取得，以編寫適用性Forms。 您可以拖放結構元素以建立表單。

請參閱下列檔案，了解如何設計XML或JSON結構，以編寫適用性Forms。

* [使用XML結構建立適用性Forms](adaptive-form-xml-schema-form-model.md)
* [使用JSON結構建立適用性Forms](adaptive-form-json-schema-form-model.md)

請執行下列動作，將XML或JSON結構描述用作最適化表單的表單模型：

1. 在 **[!UICONTROL 新增屬性]** 建立適用性表單頁面的步驟，點選 **[!UICONTROL 表單模型]** 標籤。
1. 在「表單模型」頁簽中，選擇 **[!UICONTROL 結構]** 從 **[!UICONTROL 從]** 下拉式欄位。

1. 點選 **[!UICONTROL 選擇架構]** 並執行下列其中一項操作：

   * **[!UICONTROL 從磁碟上傳]**  — 選取此選項，然後點選「上傳結構定義」，從您的檔案系統瀏覽及上傳XML結構或JSON結構。 上傳的結構檔案以表單為單位，且無法供其他適用性Forms存取。
   * **[!UICONTROL 在儲存庫中搜尋]**  — 選擇此選項，從儲存庫中可用的架構定義檔案清單中進行選擇。 選取XML或JSON結構檔案作為表單模型。 選取的結構會參照與表單相關聯，且可供其他適用性Forms使用。

      請確定JSON結構檔案名稱的結尾為 **.schema.json**. 例如：mySchema.schema.json
   ![選取XML或JSON結構](assets/upload-schema.png)
   **圖：** *選取XML或JSON結構*

1. （僅適用於XML架構）選取或上傳XML架構後，請指定所選XSD檔案的根元素，以與適用性表單對應。

   ![選擇XSD根元素](assets/xsd-root-element.png)
   **圖：** *選擇XSD根元素*

>[!NOTE]
>
>您也可以變更適用性表單的結構。 如需詳細步驟，請參閱 [編輯最適化表單的表單模型屬性](#edit-form-model).

## 編輯最適化表單的表單模型屬性 {#edit-form-model}

適用性Forms建立時沒有表單模型（對表單模型使用「無」選項），或使用表單模型，例如 <!-- form template, --> XML結構、JSON結構或表單資料模型。 您可以將適用性表單的表單模型從「無」變更為其他表單模型。 針對以表單模型為基礎的適用性表單，您可以選擇其他表單 <!-- form template,--> 相同表單模型的XML結構、JSON結構或表單資料模型。 但是，您不能將一個表單模型更改為另一個表單模型。

1. 選取「適用性表單」，然後點選 **屬性** 表徵圖。
1. 開啟 **[!UICONTROL 表單模型]** 標籤，然後執行下列任一操作。

   * 如果適用性表單沒有表單模型，則可以選擇其他表單模型並相應地選擇 <!-- a form template, --> XML或JSON結構，或表單資料模型。
   * 如果適用性表單是以表單模型為基礎，您可以選擇其他表單 <!-- form template, --> XML或JSON結構，或相同表單模型的表單資料模型。

1. 點選 **[!UICONTROL 儲存]** 以儲存屬性。
