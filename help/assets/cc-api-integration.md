---
title: Creative Cloud整合的內容自動化
description: 使用Creative Cloud整合產生資產變數
contentOwner: AG
feature: 上傳，資產處理，發佈，Asset compute微服務，工作流程
role: User,Admin
source-git-commit: 997f292be2498624c5218addd61ec40727eb48bc
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# 使用[!DNL Adobe Creative Cloud]整合產生資產變異 {#content-automation}

內容自動化附加元件整合了[!DNL Adobe Experience Manager Assets as a Cloud Service]和[!DNL Adobe Creative Cloud] API，以創意方式大規模處理您的資產。 [!DNL Experience Manager] 使用雲端資 [產微](/help/assets/asset-microservices-overview.md) 服務來使用功能， [!DNL Adobe Creative Cloud] 並自動化資產建立和媒體處理。

若要編輯[!DNL Adobe Photoshop]和[!DNL Adobe Lightroom]中的資產，您不必從[!DNL Experience Manager Assets]下載資產、編輯資產並再次上傳資產。 您只需在[!DNL Experience Manager]中建立和設定處理設定檔、將設定檔套用至資料夾，以及將資產上傳至資料夾即可。 您上傳的資產會根據處理設定檔重新處理，而您會得到這些資產的變體。 一致且輕鬆的大量處理功能可節省手動工作量並提升內容速度，而無須精湛的創意技能。 此外，開發人員和合作夥伴可以直接存取這些API，並包含自訂邏輯，以擴充資產微服務。
使用者可以建立處理設定檔，以自動處理其資產的下列創意操作：

* **自動調音**:利用人工智慧分析影像的內容，並根據影像的獨特屬性智慧地進行光和顏色校正。
* **自動直立**:利用人工智慧對影像內容進行分析，對影像中的傾斜透視進行修正。例如，要建立層視線。
* **Lightroom預設集**:使用自訂預設集對影像套用使用者定義的外觀，以達到一致的外觀。
* **影像挖剪**:使用人工智慧在顯著對象周圍建立選擇，並使用單個命令刪除背景。
* **影像遮色片**:使用人工智慧在突出物體周圍使用單一命令建立掩模。
* **Photoshop動作**:套用一系列工作(在Photoshop中)至檔案或一批檔案。
* **智慧型物件取代**:允許您交換影像，同時保留PSD檔案內套用的所有效果和調整，以大規模個人化。

## 使用處理設定檔大量編輯創意資產 {#process-assets}

若要使用處理設定檔來自動建立變異，請遵循下列步驟：

1. 請連絡[Adobe客戶服務](https://experienceleague.adobe.com/#support)以取得授權。

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**。

1. 選擇&#x200B;**[!UICONTROL Create]**，並指定&#x200B;**[!UICONTROL Name]**。

1. 選擇&#x200B;**[!UICONTROL Creative]**&#x200B;標籤，指定輸出資料夾，選擇&#x200B;**[!UICONTROL Add New]**&#x200B;以添加創作配置。

1. 提供&#x200B;**[!UICONTROL 轉譯名稱]**（或輸出名稱）、**[!UICONTROL 副檔名]**（或檔案類型）、選擇&#x200B;**[!UICONTROL 質量]**（或輸出參數）、選擇包括和排除MIME類型清單（或輸入資產篩選器），並選擇所需的創作操作。
   ![處理設定檔中的創意標籤](assets/creative-processing-profile.png)

1. 某些操作需要額外的參數（資產）。 視需要提供這些額外參數的值。

1. 將更多創意操作新增為相同處理設定檔的一部分，或儲存設定檔。

1. 將處理設定檔套用至資料夾。 在資料夾的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 資產處理]**，然後選取要套用的處理設定檔。

將處理設定檔套用至DAM資料夾後，除了標準處理作業外，此資料夾中上傳或更新的所有資產都會執行已定義的作業。 子資料夾會繼承與父資料夾上套用的相同設定檔。 使用者可以覆寫此繼承。

若要處理現有資產，請選取資產，選取&#x200B;**[!UICONTROL 重新處理]**&#x200B;選項，然後選取所需的處理設定檔。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager] 將資產處理限制為每個環境每分鐘300個請求，以及每個組織每分鐘700個請求。
* 對於[!DNL Adobe Photoshop] API操作，檔案大小限制為4 GB，對於[!DNL Adobe Lightroom]操作，檔案大小限制為1 GB。

>[!MORELIKETHIS]
>
>* [透過處理設定檔來設定和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)。
>* [ [!DNL Experience Manager] 與整合 [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md)。
>* [透過資產微服務擷取和處理資產：概述](/help/assets/asset-microservices-overview.md)。

