---
title: 如何設定Azure儲存空間？
description: 瞭解如何將表單與Azure儲存伺服器整合。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---

# 設定[!DNL Azure]儲存空間 {#configure-azure-storage}


![資料整合](assets/data-integeration.png)

[[!DNL Experience Manager Forms] 資料整合](data-integration.md)提供[!DNL Azure]儲存設定，以將表單與[!DNL Azure]儲存服務整合。 表單資料模型(FDM)可用來建立與[!DNL Azure]伺服器互動的Adaptive Forms，以啟用業務工作流程。 例如：

* 提交最適化表單時將資料寫入[!DNL Azure]。
* 透過表單資料模型(FDM)中定義的自訂實體將資料寫入[!DNL Azure]，反之亦然。
* 查詢[!DNL Azure]伺服器以取得資料並預先填入Adaptive Forms。
* 從[!DNL Azure]伺服器讀取資料。

## 建立[!DNL Azure]儲存設定 {#create-azure-storage-configuration}

在執行這些步驟之前，請確定您有[!DNL Azure]儲存體帳戶和存取金鑰，以授權存取[!DNL Azure]儲存體帳戶。

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure儲存體]**。
1. 選取資料夾以建立組態，並選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 標題]**&#x200B;欄位中指定組態的標題。
1. 在&#x200B;**[!UICONTROL Azure儲存體帳戶]**&#x200B;欄位中指定[!DNL Azure]儲存體帳戶的名稱。
1. 在&#x200B;**[!UICONTROL Azure存取金鑰]**&#x200B;欄位中指定存取Azure儲存體帳戶的金鑰，並選取&#x200B;**[!UICONTROL 儲存]**。

## 建立表單資料模型 {#create-azure-form-data-model}

建立[!DNL Azure]儲存體組態之後，您可以[建立表單資料模型](create-form-data-models.md)。 建立表單資料模型(FDM)時，請在&#x200B;**[!UICONTROL 資料Source設定]**&#x200B;欄位中指定包含[!DNL Azure]設定的資料夾。 然後，您可以從指定資料夾名稱中存在的設定清單中選取設定。

### 新增[!DNL Azure]服務至表單資料模型 {#add-azure-services}

建立表單資料模型(FDM)和資料模型物件後，您可以新增[!DNL Azure]服務至表單資料模型(FDM)。

若要新增[!DNL Azure]服務：

1. 在[編輯]模式中，從左窗格的&#x200B;**[!UICONTROL 服務]**&#x200B;區段中選取服務，然後選取&#x200B;**[!UICONTROL 新增選取的專案]**。 選取的服務會顯示在表單資料模型(FDM)的&#x200B;**[!UICONTROL 服務]**&#x200B;標籤中。

   ![新增選取的服務](assets/select-services.png)

1. 在&#x200B;**[!UICONTROL 服務]**&#x200B;索引標籤中，選取服務並&#x200B;**[!UICONTROL 編輯內容]**。 根據服務，定義服務的輸入或輸出模型物件。

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存表單資料模型(FDM)。

   下表說明可用的[!DNL Azure]服務：

   <table>
    <tbody>
     <tr>
      <th><strong>服務名稱</strong></th>
      <th><strong>說明</strong></th>
     </tr>
     <tr>
      <td>從Azure取得Blob</td>
      <td>使用ID或名稱擷取在Azure儲存體中儲存為Blob的資料</td>
     </tr>
     <tr>
      <td>從Azure取得具有二進位檔URL的Blob</td>
      <td>使用ID或名稱，針對Azure儲存體中的二進位檔，擷取以Blob形式儲存的資料(URL)</td>
     </tr>
     <tr>
      <td>在Azure中儲存Blob</td>
      <td>使用Blob ID在Azure儲存空間中儲存資料</td>
     </tr>
     <tr>
      <td>在Azure中更新Blob</td>
      <td>使用Blob ID更新Azure儲存體中的資料</td>
     </tr>
     <tr>
      <td>從Azure擷取Blob ID清單</td>
      <td>根據輸入請求中定義的數字從Azure擷取Blob ID清單。</td>
     </tr>
     <tr>
      <td>從Azure擷取Blob的SAS URL</td>
      <td>根據輸入請求中的Blob ID，從Azure擷取Blob的SAS URL。</td>
     </tr>
     <tr>
      <td>從Azure刪除Blob</td>
      <td>使用Blob ID從Azure儲存體中刪除資料</td>
     </tr>
    </tbody>
   </table>

### 將資料模型物件屬性定義為搜尋索引鍵 {#define-data-model-object-as-metadata}

若要將資料模型物件屬性定義為搜尋索引鍵：

1. 在&#x200B;**[!UICONTROL 模型]**&#x200B;索引標籤中，選取資料模型物件屬性，然後選取&#x200B;**[!UICONTROL 編輯屬性]**。
1. 將&#x200B;**[!UICONTROL 搜尋鍵]**&#x200B;切換選項切換至「開啟」狀態。 此選項僅適用於主要資料型別。
1. 選取&#x200B;**[!UICONTROL 完成]**，然後選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存表單資料模型(FDM)。

將資料模型物件屬性定義為搜尋索引鍵後，雜湊值會儲存在Azure索引標籤中，而Base64編碼值會儲存在Azure中繼資料中。

>[!NOTE]
>
>每個Azure實體只允許使用10個搜尋索引鍵，因為Azure僅允許每個Blob使用10個標籤，而且標示為搜尋索引鍵的屬性值會在雜湊後儲存在Azure索引標籤中。

<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->