---
title: Creative Cloud整合的內容自動化
description: 使用Creative Cloud整合產生資產變數
contentOwner: AG
feature: 上傳，資產處理，發佈，Asset compute微服務，工作流程
role: User,Admin
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---


# 使用[!DNL Adobe Creative Cloud]整合產生資產變異 {#content-automation}

內容自動化附加元件整合了Experience Manager資產作為Cloud Service和Adobe Creative Cloud API，以創意方式大規模處理您的資產。 Experience Manager使用雲端型[資產微服務](/help/assets/asset-microservices-overview.md)來運用Adobe Creative Cloud功能，並自動化資產建立和媒體處理。

若要編輯[!DNL Adobe Photoshop]和[!DNL Adobe Lightroom]中的資產，您不需要從下載、編輯和上傳至[!DNL Experience Manager Assets]。 只需建立並設定處理設定檔、將設定檔套用至資料夾，以及將資產上傳至資料夾即可。 上傳至資料夾的資產會經過處理，以建立該資產的不同變數。 以一致且輕鬆的方式大量處理和編輯資產，可節省人工費力，並提升內容速度。 此外，開發人員和合作夥伴可以直接存取這些API，並包含自訂邏輯，以擴充資產微服務。

使用者可以建立處理設定檔，以自動處理其資產的下列創意操作：

* **自動調音**:利用人工智慧來分析影像的內容，並基於影像的獨特屬性智慧地進行光和顏色校正。
* **自動直立**:利用人工智慧分析影像內容，糾正影像中的傾斜透視。例如，要建立層視線。
* **Lightroom預設集**:使用自訂預設集對影像套用使用者定義的外觀，以達到一致的外觀。
* **影像挖剪**:利用人工智慧在顯著對象周圍建立選擇，並使用單一命令去除背景。
* **影像遮色片**:利用人工智慧，通過單一命令在突出物體周圍建立掩模。
* **Photoshop動作**:套用一系列工作(在Photoshop中)至檔案或一批檔案。
* **智慧型物件取代**:通過允許您交換影像，同時保留PSD檔案中應用的所有效果和調整，按比例執行個性化。

## 使用處理設定檔來處理資產 {#process-assets}

若要使用處理設定檔來自動建立變異，請遵循下列步驟：

1. 請連絡[Adobe客戶服務](https://experienceleague.adobe.com/#support)以取得授權。

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**。

1. 選擇&#x200B;**[!UICONTROL Create]**，並指定&#x200B;**[!UICONTROL Name]**。

1. 選擇&#x200B;**[!UICONTROL Creative]**&#x200B;標籤，指定輸出資料夾，選擇&#x200B;**[!UICONTROL Add New]**&#x200B;以添加創作配置。

1. 提供&#x200B;**[!UICONTROL 轉譯名稱]**（或輸出名稱）、**[!UICONTROL 副檔名]**（或檔案類型）、選擇&#x200B;**[!UICONTROL 質量]**（或輸出參數）、選擇包括和排除MIME類型清單（或輸入資產篩選器），並選擇所需的創作操作。

1. 某些操作需要其他參數（資產）。 視需要提供此類其他參數的值。

1. 將更多創意操作新增為相同處理設定檔的一部分，或儲存設定檔。

1. 將處理設定檔套用至資料夾。 在資料夾的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 資產處理]**，然後選取要套用的處理設定檔。

將處理設定檔套用至DAM資料夾後，除了標準處理作業外，此資料夾中上傳或更新的所有資產都會執行已定義的作業。 子資料夾會繼承與父資料夾上所套用的相同設定檔。 使用者可以覆寫此繼承。

若要處理現有資產，請選取資產，選取&#x200B;**[!UICONTROL 重新處理]**&#x200B;選項，然後選取所需的處理設定檔。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager] 將資產處理限制為每個環境每分鐘300個請求，以及每個組織每分鐘700個請求。
* 對於[!DNL Adobe Photoshop] API操作，檔案大小限制為4 GB，對於[!DNL Adobe Lightroom]操作，檔案大小限制為1 GB。

>[!MORELIKETHIS]
>
>* [透過處理設定檔來設定和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)。
>* [ [!DNL Experience Manager] 與整合 [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md)。

