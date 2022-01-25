---
title: 如何配置Azure儲存？
description: 瞭解如何將表單與Azure儲存伺服器整合。
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 10284b1ac6fbad2e7f6231603c3dd60b6e404299
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# 設定[!DNL Azure]儲存空間 {#configure-azure-storage}

[[!DNL Experience Manager Forms] 資料整合](data-integration.md) 提供 [!DNL Azure] 儲存配置與 [!DNL Azure] 儲存服務。 表單資料模型可用於建立與交互的自適應Forms [!DNL Azure] 伺服器以啟用業務工作流。 例如：

* 將資料寫入 [!DNL Azure] 在自適應表單提交上。
* 將資料寫入 [!DNL Azure] 定義的自定義圖元，反之亦然。
* 查詢 [!DNL Azure] 用於資料和預填充AdaptiveForms。
* 從中讀取資料 [!DNL Azure] 伺服器。

## 建立 [!DNL Azure] 儲存配置 {#create-azure-storage-configuration}

在執行這些步驟之前，請確保 [!DNL Azure] 儲存帳戶和訪問密鑰，以授權對 [!DNL Azure] 儲存帳戶。

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure儲存]**。
1. 選擇要建立配置的資料夾並點擊 **[!UICONTROL 建立]**。
1. 在中為配置指定標題 **[!UICONTROL 標題]** 的子菜單。
1. 指定 [!DNL Azure] 儲存帳戶 **[!UICONTROL Azure儲存帳戶]** 的子菜單。
1. 指定在中訪問Azure儲存帳戶的密鑰 **[!UICONTROL Azure訪問密鑰]** 欄位和攻擊 **[!UICONTROL 保存]**。

## 建立表單資料模型 {#create-azure-form-data-model}

建立 [!DNL Azure] 儲存配置，您 [建立表單資料模型](create-form-data-models.md)。 指定包含 [!DNL Azure] 配置 **[!UICONTROL 資料源配置]** 的子菜單。 然後，可以從指定資料夾名稱中存在的配置清單中選擇配置。

### 添加 [!DNL Azure] 服務到窗體資料模型 {#add-azure-services}

建立「表單資料模型」和資料模型對象後，可以添加 [!DNL Azure] 服務到窗體資料模型。

添加 [!DNL Azure] 服務：

1. 在「編輯」模式下，從 **[!UICONTROL 服務]** 按鈕 **[!UICONTROL 添加選定項]**。 所選服務顯示在 **[!UICONTROL 服務]** 頁籤

   ![添加所選服務](assets/select-services.png)

1. 在 **[!UICONTROL 服務]** 頁籤，選擇服務和 **[!UICONTROL 編輯屬性]**。 基於服務，定義服務的輸入或輸出模型對象。

1. 點擊 **[!UICONTROL 保存]** 來修改標籤元素的屬性。

   下表介紹了可用 [!DNL Azure] 服務：

   <table>
    <tbody>
     <tr>
      <th><strong>服務名稱</strong></th>
      <th><strong>說明</strong></th>
     </tr>
     <tr>
      <td>從Azure獲取Blob</td>
      <td>使用ID或名稱檢索Azure儲存中作為Blob儲存的資料</td>
     </tr>
     <tr>
      <td>從Azure獲取帶二進位檔案URL的Blob</td>
      <td>使用ID或名稱檢索Azure儲存中二進位檔案的URL作為Blob儲存的資料</td>
     </tr>
     <tr>
      <td>在Azure中保存Blob</td>
      <td>使用Blob ID將資料保存在Azure儲存中</td>
     </tr>
     <tr>
      <td>更新Azure中的Blob</td>
      <td>使用Blob ID更新Azure儲存中的資料</td>
     </tr>
     <tr>
      <td>從Azure檢索Blob ID清單</td>
      <td>根據輸入請求中定義的編號從Azure檢索Blob ID清單。</td>
     </tr>
     <tr>
      <td>從Azure檢索Blob的SAS URL</td>
      <td>根據輸入請求中的Blob ID從Azure檢索Blob的SAS URL。</td>
     </tr>
     <tr>
      <td>從Azure中刪除Blob</td>
      <td>使用Blob ID從Azure儲存中刪除資料</td>
     </tr>
    </tbody>
   </table>

### 將資料模型對象屬性定義為搜索鍵 {#define-data-model-object-as-metadata}

要將資料模型對象屬性定義為搜索鍵：

1. 在 **[!UICONTROL 模型]** 頁籤，選擇資料模型對象屬性並點擊 **[!UICONTROL 編輯屬性]**。
1. 切換 **[!UICONTROL 搜索鍵]** 將選項切換到「開啟」狀態。 此選項僅對主資料類型可用。
1. 點擊 **[!UICONTROL 完成]** 然後點擊 **[!UICONTROL 保存]** 的子菜單。

在將資料模型對象屬性定義為搜索鍵後，散列值儲存在Azure索引標籤中，Base64編碼值儲存在Azure元資料中。

>[!NOTE]
>
>每個Azure實體只允許10個搜索密鑰，因為Azure僅允許每個Blob有10個標籤，而標籤為搜索密鑰的屬性值在散列後儲存在Azure索引標籤中。
