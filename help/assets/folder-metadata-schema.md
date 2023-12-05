---
title: 資料夾中繼資料結構
description: 瞭解如何在中建立資產資料夾的中繼資料結構 [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 9%

---

# 資料夾中繼資料結構 {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] 可讓您建立資產資料夾的中繼資料結構，定義資料夾屬性頁面中顯示的版面和中繼資料。

## 新增資料夾中繼資料結構表單 {#add-a-folder-metadata-schema-form}

使用資料夾中繼資料結構Forms編輯器可建立和編輯資料夾的中繼資料結構。

1. 選取 [!DNL Experience Manager] 標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾中繼資料結構]**.
1. 在「資料夾中繼資料結構Forms」頁面中，選取 **[!UICONTROL 建立]**.
1. 指定表單的名稱，然後選取 **[!UICONTROL 建立]**. 新的結構表單會列在「結構Forms」頁面中。

## 編輯資料夾中繼資料結構表單 {#edit-folder-metadata-schema-forms}

您可以編輯新新增或現有的中繼資料結構表單，其中包括：

* 索引標籤
* 索引標籤中的表單專案。

您可以將這些表單專案對應/設定到CRX存放庫中中繼資料節點內的欄位。 您可以將新的索引標籤或表單專案新增到中繼資料結構表單。

1. 在「方案Forms」頁面中，選取您建立的表單，然後選取 **[!UICONTROL 編輯]** 圖示。
1. 在「資料夾中繼資料結構編輯器」頁面中，選取 **[!UICONTROL +]** 圖示以新增索引標籤至表單。 若要重新命名標籤，請選取預設名稱，並在 **[!UICONTROL 設定]**.

   ![custom_tab](assets/custom_tab.png)

   若要新增更多標籤，請選取 **[!UICONTROL +]** 圖示。 選取 **[!UICONTROL X]** 以刪除標籤。

1. 在使用中標籤中，從新增一或多個元件 **[!UICONTROL 建置表單]** 標籤。

   ![adding_components](assets/adding_components.png)

   如果您建立多個標籤，請選取特定標籤以新增元件。

1. 若要設定元件，請選取該元件，並在下列位置修改其屬性： **[!UICONTROL 設定]** 標籤。

   如有必要，請從以下位置刪除元件： **[!UICONTROL 設定]** 標籤。

   ![configure_properties](assets/configure_properties.png)

1. 選取 **[!UICONTROL 儲存]** 以儲存變更。

### 建立表單的元件 {#components-to-build-forms}

此 **[!UICONTROL 建置表單]** 索引標籤會列出您在資料夾中繼資料結構表單中使用的表單專案。 此 **[!UICONTROL 設定]** 標籤會顯示您在「 」中選取的每個專案的屬性。 **[!UICONTROL 建置表單]** 標籤。 以下是中可用的表單專案清單 **[!UICONTROL 建置表單]** 標籤：

<table>
 <tbody>
  <tr>
   <td><p><strong>元件名稱</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>區段標題</p> </td>
   <td><p> 新增區段標題以取得常用元件清單。</p> </td>
  </tr>
  <tr>
   <td><p>單行文字</p> </td>
   <td><p> 新增單行文字屬性。 它會儲存為字串。</p> </td>
  </tr>
  <tr>
   <td><p>多值文字</p> </td>
   <td><p> 新增多值文字屬性。 它會儲存為字串陣列。</p> </td>
  </tr>
  <tr>
   <td><p>數字</p> </td>
   <td><p> 新增數字元件。</p> </td>
  </tr>
  <tr>
   <td><p>日期</p> </td>
   <td><p> 新增日期元件。</p> </td>
  </tr>
  <tr>
   <td><p>下拉式</p> </td>
   <td><p> 新增下拉式清單。</p> </td>
  </tr>
  <tr>
   <td><p>標準標記</p> </td>
   <td><p> 新增標籤。 </p> </td>
  </tr>
  <tr>
   <td><p>隱藏欄位</p> </td>
   <td><p> 新增隱藏欄位。 儲存資產時，會以POST引數的形式傳送。</p> </td>
  </tr>
 </tbody>
</table>

### 編輯表單專案 {#editing-form-items}

若要編輯表單專案的屬性，請選取元件並在下列專案編輯下列屬性的全部或子集： **[!UICONTROL 設定]** 標籤。 建議僅將一個欄位對應到中繼資料結構描述中的指定屬性。 否則，系統會挑選對應至屬性的最新新增欄位。

**[!UICONTROL 欄位標籤]**：在資料夾的屬性頁面上顯示的中繼資料屬性名稱。

**[!UICONTROL 對應至屬性]**：此屬性會指定資料夾節點在CRX儲存庫中儲存位置的相對路徑。 開頭為&quot;**./**&quot;，表示路徑在資料夾的節點下。

以下是屬性的有效值範例：

* `./jcr:content/metadata/dc:title`：將值儲存在資料夾的中繼資料節點，做為屬性 `dc:title`.

* `./jcr:created`：儲存資產的建立日期和時間。 這是受保護的屬性。 如果您設定這些屬性，Adobe建議您將其標籤為 [!UICONTROL 停用編輯].

為確保元件在中繼資料結構表單中正確顯示，請勿在屬性路徑中包含空格。

**[!UICONTROL JSON路徑]**：用來指定JSON檔案的路徑，您可在此指定選項的索引鍵值配對。

**[!UICONTROL 預留位置]**：使用此屬性可指定與中繼資料屬性相關的預留位置文字。

**[!UICONTROL 選擇]**：使用此屬性來指定清單中的選項。

**[!UICONTROL 說明]**：使用此屬性為中繼資料元件新增簡短說明。

**[!UICONTROL 類別]**：與屬性相關聯的物件類別。

## 刪除資料夾中繼資料結構表單 {#delete-folder-metadata-schema-forms}

您可以從「資料夾中繼資料結構Forms」頁面中刪除資料夾中繼資料結構表單。 若要刪除表單，請選取該表單，然後從工具列選取刪除圖示。

![delete_form](assets/delete_form.png)

## 指派資料夾中繼資料結構 {#assign-a-folder-metadata-schema}

您可以從「資料夾中繼資料結構Forms」頁面或在建立資料夾時，將資料夾中繼資料結構指派給資料夾。

如果您為資料夾設定中繼資料結構，則結構表單的路徑會儲存在 `folderMetadataSchema` 「 」下資料夾節點的屬性。*/jcr：content*.

### 從「資料夾中繼資料結構」頁面指派至結構 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 選取 [!DNL Experience Manager] 標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**> **[!UICONTROL 資料夾中繼資料結構]**.
1. 在「資料夾中繼資料結構Forms」頁面中，選取您要套用至資料夾的結構表單。
1. 從工具列中選取 **[!UICONTROL 套用至資料夾]**.

1. 選取要套用結構描述的資料夾，然後選取 **[!UICONTROL 套用]**. 如果資料夾已套用中繼資料結構，則會出現警告訊息，告知您即將覆寫現有的中繼資料結構。 選取 **[!UICONTROL 覆寫]**.
1. 開啟您套用中繼資料結構的資料夾的中繼資料屬性。

   ![folder_properties](assets/folder_properties.png)

   若要檢視資料夾中繼資料欄位，請選取 **[!UICONTROL 資料夾中繼資料]** 標籤。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### 建立資料夾時指派結構 {#assign-a-schema-when-creating-a-folder}

建立資料夾時，您可以指派資料夾中繼資料結構。 如果系統中至少存在一個資料夾中繼資料結構，則會在 **[!UICONTROL 建立資料夾]** 對話方塊。 您可以選取所需的結構描述。 依預設，不會選取結構描述。

1. 從 [!DNL Experience Manager Assets] 使用者介面，選取 **[!UICONTROL 建立]** 工具列中的。
1. 指定資料夾的標題和名稱。
1. 從「資料夾中繼資料結構」清單中，選取所需的結構。 然後，選取 **[!UICONTROL 建立]**.

   ![select_schema](assets/select_schema.png)

1. 開啟您套用中繼資料結構的資料夾的中繼資料屬性。
1. 若要檢視資料夾中繼資料欄位，請選取 **[!UICONTROL 資料夾中繼資料]** 標籤。

## 使用資料夾中繼資料結構 {#use-the-folder-metadata-schema}

開啟配置了資料夾元資料架構的資料夾的屬性。「文 **[!UICONTROL 件夾元資料]** 」頁籤顯示在資料夾屬性頁中。要查看資料夾元資料結構表單，請選擇此頁籤。

在各個欄位中輸入中繼資料值，然後選取 **[!UICONTROL 儲存]** 以儲存值。 您指定的值會儲存在CRX存放庫的資料夾節點中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
