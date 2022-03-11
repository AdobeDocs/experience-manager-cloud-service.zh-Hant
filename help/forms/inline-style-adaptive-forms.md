---
title: 如何將內嵌樣式應用於自適應表單元件？
description: 雖然可以在自適應表單上應用自定義樣式，但也可以在自適應表單的各個元件上應用內嵌CSS屬性。 瞭解如何將內聯樣式應用於Adaptive Form元件。 使用示例將內聯樣式應用於文本欄位元件進行深入挖掘。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# 自適應表單元件的內聯樣式 {#inline-styling-of-adaptive-form-components}

通過使用指定樣式來定義自適應表單的總體外觀和樣式 [主題編輯器](themes.md)。 此外，您還可以將內聯CSS樣式應用於單個Adaptive Form元件，並即時預覽更改。 內聯樣式會覆蓋主題中提供的樣式。

## 應用內聯CSS屬性 {#apply-inline-css-properties}

要向元件添加內聯樣式：

1. 在窗體編輯器中開啟窗體，並將模式更改為樣式模式。 要將模式更改為樣式模式，請在頁面工具欄中按一下 ![畫布下拉清單](assets/Smock_ChevronDown.svg) > **[!UICONTROL 樣式]**。
1. 在頁面中選擇元件，然後按一下編輯按鈕 ![編輯按鈕](assets/edit.svg)。 樣式屬性在邊欄中開啟。

   也可以從邊欄的表單層次結構樹中選擇元件。 表單層次結構樹在提要欄中可用作表單對象。

   在 [!UICONTROL 樣式] 模式下，可以查看「表單對象」(Form Objects)下列出的元件。 但是，邊欄中的「表單對象」清單會列出欄位和面板等元件。 欄位和面板是可包含文本框和單選按鈕等元件的通用元件。

   從提要欄中選擇元件時，將看到列出的所有子元件以及選定元件的屬性。 可以選擇特定的子元件並對其進行樣式化。

1. 按一下提要欄中的頁籤以指定CSS屬性。 可以指定屬性，如：

   * [!UICONTROL Dimension和職位] （顯示設定、填充、高度、寬度、邊距、位置、z-index、浮點、清除、溢出）
   * [!UICONTROL 文本] （字型系列、粗細、顏色、大小、行高和對齊方式）
   * [!UICONTROL 背景] （影像和漸變，背景顏色）
   * [!UICONTROL 邊框] （寬度、樣式、顏色、半徑）
   * [!UICONTROL 效果] （陰影、不透明度）
   * [!UICONTROL 高級] （用於為元件編寫自定義CSS）

1. 同樣，您可以對元件的其它部分應用樣式，如 [!UICONTROL 小部件]。 [!UICONTROL 標題], [!UICONTROL 幫助]。
1. 點擊 **[!UICONTROL 完成]** 確認更改或 **[!UICONTROL 取消]** 來放棄更改。

## 示例：欄位元件的內聯樣式 {#example-inline-styles-for-a-field-component}

以下影像描述了在將內嵌樣式應用到它之前和之後的文本欄位。

![應用內聯樣式之前的文本框元件](assets/no-style.png)

應用內聯樣式屬性之前的文本框元件

注意在應用以下CSS屬性後，文本框樣式的更改如下圖所示。

<table>
 <tbody>
  <tr>
   <td><p>選擇器</p> </td>
   <td><p>CSS屬性</p> </td>
   <td><p>值</p> </td>
   <td><p>效果</p> </td>
  </tr>
  <tr>
   <td><p>欄位</p> </td>
   <td><p>邊界</p> </td>
   <td><p>邊框寬度=2px</p> <p>邊框樣式=實體</p> <p>邊框顏色=#1111</p> </td>
   <td><p>在欄位周圍建立2像素的黑色寬邊框</p> </td>
  </tr>
  <tr>
   <td><p>文本框</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>將背景顏色更改為CornflowerBlue(#6495ED)</p> <p>注：可以在值欄位中指定顏色名稱或其十六進位代碼。</p> </td>
  </tr>
  <tr>
   <td><p>標籤</p> </td>
   <td><p>Dimension和位置&gt;寬度</p> </td>
   <td><p>100px</p> </td>
   <td><p>將標籤的寬度固定為100px</p> </td>
  </tr>
  <tr>
   <td>欄位說明圖示</td>
   <td>文本&gt;字型顏色</td>
   <td>#2ECC40</td>
   <td>更改幫助表徵圖臉的顏色。</td>
  </tr>
  <tr>
   <td><p>長描述</p> </td>
   <td><p>text-align</p> </td>
   <td><p>中心點</p> </td>
   <td><p>將幫助的詳細說明與中心對齊</p> </td>
  </tr>
 </tbody>
</table>

![應用內聯樣式後的文本框樣式](assets/applied-style.png)

應用內聯樣式屬性後的文本框元件

按照上述步驟，您可以選擇和設定其他元件的樣式，如面板、提交按鈕和單選按鈕。

>[!NOTE]
>
>造型屬性會因所選元件而異。

## 複製和貼上樣式 {#copy-paste-styles}

也可以在「自適應表單」中將樣式從一個元件複製並貼上到另一個元件。 在 **[!UICONTROL 樣式]** 模式，按一下元件並按一下「Copy（複製）」表徵圖 ![複製](assets/property-copy-icon.svg)。

按一下同一類型的其他元件，然後按一下「貼上」表徵圖 ![複製](assets/Smock_Paste_18_N.svg) 來修改標籤元素的屬性。 也可按一下「清除樣式」表徵圖 ![複製](assets/clear-style-icon.svg) 來修改標籤元素的屬性。

## 為元件的不同狀態設定樣式 {#set-styles-for-states}

可以為元件類型的不同狀態設定樣式。 不同的狀態包括： [!UICONTROL 焦點]。 [!UICONTROL 已禁用]。 [!UICONTROL 懸停]。 [!UICONTROL 錯誤]。 [!UICONTROL 成功], [!UICONTROL 強制]。

要定義元件狀態的樣式，請執行以下操作：

1. 在 **[!UICONTROL 樣式]** 模式，按一下元件並按一下「Edit（編輯）」表徵圖 ![編輯](assets/Smock_Edit_18_N.svg)。

1. 使用 **[!UICONTROL 州]** 的子菜單。

   ![選擇狀態](assets/select-state.png)

1. 為元件的選定狀態定義造型並點擊 ![保存](assets/save_icon.svg) 的子菜單。

您還可以模擬成功和錯誤狀態。 按一下「展開」表徵圖查看 **[!UICONTROL 模擬成功]** 和 **[!UICONTROL 模擬錯誤]** 頁籤

![模擬狀態](assets/simulate-states.png)
