---
title: 在通用編輯器中如何整合表單的表單資料模型 (FDM)？
description: 了解如何根據表單資料模型 (FDM) 建立表單。產生並編輯 FDM 中資料模型物件的樣本資料。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 33%

---


# 將Forms與表單資料模型(FDM)整合

使用FDM將表單連線至後端資料來源，以啟用資料繫結、驗證和提交工作流程。

## 先決條件

將FDM與表單整合前，請先完成下列步驟：

1. **[設定資料Source](/help/forms/configure-data-sources.md)**：設定後端連線
2. **[建立表單資料模型](/help/forms/create-form-data-models.md)**：定義資料結構和服務
3. **[設定資料模型物件](/help/forms/work-with-form-data-model.md)**：對應資料關係

## 考量事項

如果您在通用編輯器介面中沒有看到「**資料來源**」圖示，或在右側屬性面板中沒有看到「**繫結參考**」屬性，請在 **Extension Manager** 中啟用&#x200B;**資料來源**&#x200B;擴充功能。

![通用編輯器 Extension Manager 介面的螢幕擷圖顯示可用的擴充功能，包括為了表單整合而啟用的資料來源擴充功能](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

請參閱[Extension Manager 功能重點介紹](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，了解如何在通用編輯器中啟用和停用擴充功能。

## 選擇您的表單型別

Universal Editor支援兩種表單建立方法：

| 層面 | 綱要型表單 | 非綱要型表單 |
|--------|-------------------|----------------------|
| **設定複雜性** | 簡單（自動繫結） | 手動（依欄位繫結） |
| **使用案例** | 具有已定義資料結構的新表單 | 現有表單或彈性需求 |
| **資料來源** | 建立期間必填 | 可稍後新增 |
| **繫結** | 自動欄位繫結 | 每個欄位手動繫結 |

![通用編輯器中的表單類型](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## 綱要型表單

結構描述型表單會自動設定資料來源，並將表單欄位繫結至資料。 此方法適用於具有明確定義資料結構的新表單。

### 建立以結構描述為基礎的表單

1. **存取Forms主控台**
   - 登入您的[!DNL Experience Manager Forms]作者執行個體
   - 導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**

2. **開始表單建立**
   - 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 最適化Forms]**
   - 選擇Edge Delivery Services範本
   - 啟用時按一下&#x200B;**[!UICONTROL 建立]**

   ![Edge Delivery Services 範本](/help/edge/assets/create-eds-forms.png)

3. **設定資料模型**
   - 前往&#x200B;**資料**&#x200B;標籤
   - 為多個資料來源選取&#x200B;**表單資料模型(FDM)**，或為單一後端系統選取&#x200B;**JSON結構描述**
   - 選擇您建立的FDM （例如Pet表單資料模型）

   ![選取表單資料模型](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **完成表單設定**
   - 輸入&#x200B;**名稱**&#x200B;和&#x200B;**標題**
   - 指定&#x200B;**GitHub URL** （例如`https://github.com/wkndforms/edsforms`）
   - 按一下「**[!UICONTROL 建立]**」。

   ![建立綱要型表單](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### 驗證以結構描述為基礎的表單

表單會在具有預先設定資料繫結的通用編輯器中開啟：

![通用編輯器的螢幕擷圖顯示一份綱要型表單，內含預先填入的表單欄位，且內容瀏覽器顯示可用的資料來源元素](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![自動資料繫結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## 非綱要型表單

非結構描述表單需要手動設定資料來源和欄位繫結。 此方法可針對現有表單或複雜需求提供彈性。

### 建立非結構描述型表單

1. **存取表單屬性**
   - 登入您的[!DNL Experience Manager Forms]作者執行個體
   - 導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**
   - 選取您的表單並按一下&#x200B;**[!UICONTROL 屬性]**

   ![開啟表單屬性](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **設定表單模型**
   - 開啟&#x200B;**表單模型**&#x200B;標籤
   - 從&#x200B;**從**&#x200B;選取下拉式清單中選取&#x200B;**表單資料模型(FDM)**
   - 從清單中選擇您的FDM

   ![選取表單模型標籤](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![選取 FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **確認設定**
   - 在警告對話方塊中按一下&#x200B;**確定**
   - 按一下&#x200B;**[!UICONTROL 儲存並關閉]**

   ![表單模型精靈](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### 新增資料元素

1. **開啟表單進行編輯**
   - 表單會在通用編輯器中開啟

   ![非綱要型表單製作](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **存取資料Source元素**
   - 移至&#x200B;**[!UICONTROL 內容瀏覽器]**&#x200B;中的&#x200B;**[!UICONTROL 資料來源]**&#x200B;索引標籤
   - 檢視FDM中可用的資料元素

   ![表單資料來源](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **新增元素至表單**
   - 選取資料元素並按一下&#x200B;**[!UICONTROL 新增]**
   - 或是拖放元素以建置您的表單

   ![新增資料元素](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![螢幕擷圖顯示通用編輯器正在將資料元素從「資料來源」索引標籤拖放到表單結構中，以建置非綱要型表單](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### 新增手動資料繫結

針對現有的表單欄位，透過&#x200B;**繫結參考**&#x200B;屬性新增資料繫結：

1. **開啟欄位屬性**
   - 選取要繫結的表單欄位
   - 開啟其屬性面板

2. **設定繫結參考**
   - 移至&#x200B;**繫結參考**&#x200B;屬性
   - 按一下&#x200B;**瀏覽**&#x200B;圖示

   ![手動新增表單欄位的資料繫結](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **選取資料元素**
   - 從&#x200B;**選取繫結參考**&#x200B;精靈中的資料來源樹狀結構選擇
   - 選取所需的資料元素，然後按一下&#x200B;**選取**

   ![選取資料繫結參考](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![選取資料元素](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **驗證繫結**
   - 表單欄位現在會繫結至資料元素
   - 繫結出現在&#x200B;**繫結參考**&#x200B;屬性中

   ![自動資料繫結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## 驗證整合

完成整合後：

1. **測試資料繫結**：驗證表單欄位顯示正確資料
2. **驗證提交**：確保將資料儲存到已設定的來源
3. **檢查錯誤處理**：測試無效的資料案例

## 後續步驟

設定[提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)以完成您的表單工作流程。
