---
title: 如何在通用編輯器中整合表單的表單資料模型 (FDM)？
description: 了解如何根據表單資料模型 (FDM) 建立 Edge Delivery Services 的表單。產生及編輯 FDM 中資料模型物件的樣本資料。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 7d3ea5bdc6545b9610f595660fcfb2ef70c837de
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 100%

---


# 將表單與表單資料模型 (FDM) 整合

使用 FDM 將您的表單連接到後端資料來源，以啟用資料繫結、驗證和提交工作流程。

## 先決條件

在將 FDM 與您的表單整合之前，請完成以下步驟：

1. **[設定資料來源](/help/forms/configure-data-sources.md)**：設定後端連線
2. **[建立表單資料模型](/help/forms/create-form-data-models.md)**：定義資料結構和服務
3. **[設定資料模型物件](/help/forms/work-with-form-data-model.md)**：對應資料關係

## 考量事項

如果您在通用編輯器介面中沒有看到「**資料來源**」圖示，或在右側屬性面板中沒有看到「**繫結參考**」屬性，請在 **Extension Manager** 中啟用&#x200B;**資料來源**&#x200B;擴充功能。

![通用編輯器 Extension Manager 介面的螢幕擷圖顯示可用的擴充功能，包括為了表單整合而啟用的資料來源擴充功能](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

請參閱 [Extension Manager 功能重點介紹](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，了解如何在通用編輯器中啟用和停用擴充功能。

## 選擇您的表單類型

通用編輯器支援兩種表單建立方法：

| 層面 | 結構描述型表單 | 非結構描述型表單 |
|--------|-------------------|----------------------|
| **設定複雜度** | 簡單 (自動繫結) | 手動 (逐個欄位繫結) |
| **使用案例** | 已定義資料結構的新表單 | 現有表單或彈性要求 |
| **資料來源** | 建立期間便是必要項目 | 可以日後新增 |
| **繫結** | 自動欄位繫結 | 每個欄位手動繫結 |

![通用編輯器中的表單類型](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## 結構描述型表單

結構描述型表單自動設定資料來源並將表單欄位繫結到資料。對於具有明確定義資料結構的新表單來說，這是很合適的方法。

### 建立結構描述型表單

1. **存取表單控制台**
   - 登入您的 [!DNL Experience Manager Forms] 作者實例
   - 導覽至「**[!UICONTROL Adobe Experience Manager]**」>「**[!UICONTROL 表單]**」>「**[!UICONTROL 表單與文件]**」

2. **開始建立表單**
   - 選取「**[!UICONTROL 建立]**」>「**[!UICONTROL 自適應表單]**」
   - 選擇 Edge Delivery Services 範本
   - 啟用時按一下「**[!UICONTROL 建立]**」

   ![Edge Delivery Services 範本](/help/edge/assets/create-eds-forms.png)

3. **設定資料模型**
   - 前往「**資料**」標籤
   - 對於多個資料來源，請選取「**表單資料模型 (FDM)**」，而對於單一後端系統，請選取「**JSON 結構描述**」
   - 選擇您建立的 FDM (例如寵物表單資料模型)

   ![選取表單資料模型](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **完成表單設定**
   - 輸入「**名稱**」和「**標題**」
   - 指定「**GitHub URL**」(例如 `https://github.com/wkndforms/edsforms`)。
   - 按一下「**[!UICONTROL 建立]**」

   ![建立結構描述型表單](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### 確認結構描述型表單

該表單在通用編輯器中開啟，而且已經預先設定資料繫結：

![通用編輯器的螢幕擷圖顯示一份結構描述型表單，已預先填入表單欄位，且內容瀏覽器顯示可用的資料來源元素](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![自動資料繫結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## 非結構描述型表單

非結構描述型表單需要手動設定資料來源和欄位繫結。這種方法讓使用者可以彈性處理現有表單或複雜要求。

### 建立非結構描述型表單

1. **存取表單屬性**
   - 登入您的 [!DNL Experience Manager Forms] 作者實例
   - 導覽至「**[!UICONTROL Adobe Experience Manager]**」>「**[!UICONTROL 表單]**」>「**[!UICONTROL 表單與文件]**」
   - 選取您的表單然後按一下「**[!UICONTROL 屬性]**」

   ![開啟表單屬性](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **設定表單模型**
   - 開啟「**表單模型**」標籤
   - 從「**選取來源**」下拉式選單選取「**表單資料模型 (FDM)**」
   - 從清單中選擇您的 FDM

   ![選取表單模型標籤](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![選取 FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **確認設定**
   - 在警告對話框中按一下「**確定**」
   - 按一下「**[!UICONTROL 儲存並關閉]**」

   ![表單模型精靈](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### 新增資料元素

1. **開啟表單進行編輯**
   - 表單在通用編輯器中開啟

   ![非結構描述型表單製作](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **存取資料來源元素**
   - 前往&#x200B;**[!UICONTROL 內容瀏覽器]**&#x200B;中的「**[!UICONTROL 資料來源]**」標籤
   - 檢視 FDM 中的可用資料元素

   ![表單資料來源](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **在表單中新增元素**
   - 選取資料元素並按一下「**[!UICONTROL 新增]**」
   - 或拖放元素來建置表單

   ![新增資料元素](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![螢幕擷圖顯示通用編輯器，正在將資料元素從「資料來源」標籤拖放到表單結構中，以建置非結構描述型表單](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### 新增手動資料繫結

對於現有的表單欄位，透過「**繫結參考**」屬性新增資料繫結：

1. **開啟欄位屬性**
   - 選取要繫結的表單欄位
   - 開啟屬性面板

2. **設定繫結參考**
   - 前往「**繫結參考**」屬性
   - 按一下「**瀏覽**」圖示

   ![手動新增表單欄位的資料繫結](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **選取資料元素**
   - 從「**選取繫結參考**」精靈中的資料來源樹狀結構選擇。
   - 選擇所需的資料元素並按一下「**選取**」

   ![選取資料繫結參考](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![選取資料元素](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **確認繫結**
   - 表單欄位現在與資料元素繫結
   - 繫結出現在「**繫結參考**」屬性中

   ![自動資料繫結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## 確認整合

完成整合後：

1. **測試資料繫結**：確認表單欄位顯示正確的資料
2. **驗證提交**：確保資料儲存到所設定的來源
3. **檢查錯誤處理**：使用無效資料情境進行測試

## 後續步驟

設定[提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)以完成您的表單工作流程。
