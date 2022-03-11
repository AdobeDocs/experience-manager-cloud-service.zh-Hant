---
title: 資料夾中繼資料結構
description: 瞭解如何為中的資產資料夾建立元資料架構 [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: 7ea0e6c2d277199fc5216aab70e587bd23ac6baa
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 7%

---

# 資料夾中繼資料結構 {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] 用於為資產資料夾建立元資料方案，這些資料夾定義資料夾屬性頁中顯示的佈局和元資料。

## 添加資料夾元資料架構表單 {#add-a-folder-metadata-schema-form}

使用資料夾元資料架構Forms編輯器建立和編輯資料夾的元資料架構。

1. 點擊/按一下 [!DNL Experience Manager] 徽標，然後轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾元資料架構]**。
1. 在「資料夾元資料架構」Forms頁中，點擊/按一下 **[!UICONTROL 建立]**。
1. 指定表單的名稱，然後點擊/按一下 **[!UICONTROL 建立]**。 新架構表單列在「架構Forms」頁中。

## 編輯資料夾元資料架構表單 {#edit-folder-metadata-schema-forms}

您可以編輯新添加的或現有的元資料架構表單，其中包括以下內容：

* 索引標籤
* 制表符內的窗體項。

您可以將這些表單項映射到/配置到CRX儲存庫的元資料節點中的欄位。 可以將新頁籤或表單項添加到元資料架構表單中。

1. 在「架構Forms」頁中，選擇您建立的表單，然後點擊/按一下 **[!UICONTROL 編輯]** 的子菜單。
1. 在「資料夾元資料架構編輯器」頁中，按一下/按一下 **[!UICONTROL +]** 的子菜單。 要更名頁籤，請點擊/按一下預設名稱，然後在 **[!UICONTROL 設定]**。

   ![自定義頁籤](assets/custom_tab.png)

   要添加更多頁籤，請點擊/按一下 **[!UICONTROL +]** 表徵圖 點擊/按一下 **[!UICONTROL X]** 按鈕

1. 在活動頁籤中，從 **[!UICONTROL 生成窗體]** 頁籤。

   ![添加元件](assets/adding_components.png)

   如果建立多個頁籤，請點擊/按一下特定頁籤以添加元件。

1. 要配置元件，請選擇它並在 **[!UICONTROL 設定]** 頁籤。

   如果需要，請從 **[!UICONTROL 設定]** 頁籤。

   ![configure_properties](assets/configure_properties.png)

1. 點擊/按一下 **[!UICONTROL 保存]** 的子菜單。

### 要生成表單的元件 {#components-to-build-forms}

的 **[!UICONTROL 生成窗體]** 頁籤列出在資料夾元資料架構窗體中使用的窗體項。 的 **[!UICONTROL 設定]** 頁籤顯示您在 **[!UICONTROL 生成窗體]** 頁籤。 下面列出了 **[!UICONTROL 生成窗體]** 頁籤：

<table>
 <tbody>
  <tr>
   <td><p><strong>元件名稱</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>區段標題</p> </td>
   <td><p> 為公用元件清單添加節標題。</p> </td>
  </tr>
  <tr>
   <td><p>單行文字</p> </td>
   <td><p> 添加單行文本屬性。 它儲存為字串。</p> </td>
  </tr>
  <tr>
   <td><p>多值文字</p> </td>
   <td><p> 添加多值文本屬性。 它儲存為字串陣列。</p> </td>
  </tr>
  <tr>
   <td><p>數量</p> </td>
   <td><p> 添加數字元件。</p> </td>
  </tr>
  <tr>
   <td><p>日期</p> </td>
   <td><p> 添加日期元件。</p> </td>
  </tr>
  <tr>
   <td><p>下拉式</p> </td>
   <td><p> 添加下拉清單。</p> </td>
  </tr>
  <tr>
   <td><p>標準標記</p> </td>
   <td><p> 新增標記. </p> </td>
  </tr>
  <tr>
   <td><p>隱藏欄位</p> </td>
   <td><p> 添加隱藏欄位。 保存資產時，它將作為POST參數發送。</p> </td>
  </tr>
 </tbody>
</table>

### 編輯表單項 {#editing-form-items}

要編輯表單項的屬性，請點擊/按一下該元件，然後在 **[!UICONTROL 設定]** 頁籤。 建議只將一個欄位映射到元資料架構中的給定屬性。 否則，系統將選取映射到該屬性的最新添加欄位。

**[!UICONTROL 欄位標籤]**:顯示在資料夾屬性頁面上的元資料屬性的名稱。

**[!UICONTROL 映射到屬性]**:此屬性指定保存資料夾節點的CRX儲存庫中資料夾節點的相對路徑。 它以&quot;開頭&#x200B;**。/**&quot; ，表示路徑位於資料夾的節點下。

以下是屬性有效值的示例：

* `./jcr:content/metadata/dc:title`:將資料夾的元資料節點上的值儲存為屬性 `dc:title`。

* `./jcr:created`:儲存資產的建立日期和時間。 它是受保護的屬性。 如果配置這些屬性，Adobe建議將其標籤為 [!UICONTROL 禁用編輯]。

要確保元件在元資料架構表單中正確顯示，請不要在屬性路徑中包含空格。

**[!UICONTROL JSON路徑]**:使用它可指定JSON檔案的路徑，在該路徑中為選項指定鍵值對。

**[!UICONTROL 佔位符]**:使用此屬性可指定與元資料屬性相關的佔位符文本。

**[!UICONTROL 選擇]**:使用此屬性可指定清單中的選項。

**[!UICONTROL 說明]**:使用此屬性可為元資料元件添加簡短說明。

**[!UICONTROL 類]**:屬性與關聯的對象類。

## 刪除資料夾元資料架構表單 {#delete-folder-metadata-schema-forms}

可以從「資料夾元資料架構」Forms頁中刪除資料夾元資料架構表單。 要刪除表單，請選擇該表單並點擊/按一下工具欄中的「刪除」表徵圖。

![刪除窗體](assets/delete_form.png)

## 分配資料夾元資料架構 {#assign-a-folder-metadata-schema}

可以從「資料夾元資料方案」Forms頁或在建立資料夾時將資料夾元資料方案分配給資料夾。

如果為資料夾配置元資料架構，則架構表單的路徑將儲存在 `folderMetadataSchema` 資料夾節點的屬性。*/jcr：內容*。

### 從「資料夾元資料方案」頁分配到方案 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 點擊/按一下 [!DNL Experience Manager] 徽標，然後轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**> **[!UICONTROL 資料夾元資料架構]**。
1. 從「資料夾元資料方案」Forms頁中，選擇要應用於資料夾的方案表單。
1. 在工具欄上，點擊/按一下 **[!UICONTROL 應用於資料夾]**。

1. 選擇要應用該架構的資料夾，然後按一下/點擊 **[!UICONTROL 應用]**。 如果已在資料夾上應用元資料架構，則會顯示一則警告消息，通知您將覆蓋現有元資料架構。 點擊/按一下 **[!UICONTROL 覆蓋]**。
1. 開啟應用元資料架構的資料夾的元資料屬性。

   ![資料夾屬性](assets/folder_properties.png)

   若要檢視資料夾中繼資料欄位，請點選/按一下「資料夾中 **[!UICONTROL 繼資料]** 」標籤。

   ![資料夾_元資料_屬性](assets/folder_metadata_properties.png)

### 在建立資料夾時分配架構 {#assign-a-schema-when-creating-a-folder}

建立資料夾時，可以分配資料夾元資料架構。 如果系統中至少存在一個資料夾元資料架構，則在 **[!UICONTROL 建立資料夾]** 對話框。 可以選擇所需的架構。 預設情況下，未選擇任何架構。

1. 從 [!DNL Experience Manager Assets] 用戶介面，點擊/按一下 **[!UICONTROL 建立]** 的子菜單。
1. 指定資料夾的標題和名稱。
1. 從資料夾元資料架構清單中，選擇所需的架構。 然後，點擊/按一下 **[!UICONTROL 建立]**。

   ![選擇架構](assets/select_schema.png)

1. 開啟應用元資料架構的資料夾的元資料屬性。
1. 若要檢視資料夾中繼資料欄位，請點選/按一下「資料夾中 **[!UICONTROL 繼資料]** 」標籤。

## 使用資料夾元資料架構 {#use-the-folder-metadata-schema}

開啟配置了資料夾元資料架構的資料夾的屬性。「文 **[!UICONTROL 件夾元資料]** 」頁籤顯示在資料夾屬性頁中。要查看資料夾元資料結構表單，請選擇此頁籤。

在各個欄位中輸入元資料值，然後點擊/按一下 **[!UICONTROL 保存]** 儲存值。 您指定的值將儲存在CRX儲存庫的資料夾節點中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)
