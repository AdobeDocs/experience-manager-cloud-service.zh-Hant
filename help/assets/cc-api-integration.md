---
title: Creative Cloud整合的內容自動化
description: 使用Creative Cloud整合產生資產的變體
contentOwner: AG
feature: Upload, Asset Processing, Publishing, Asset Compute Microservices
role: User, Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 5%

---

# 使用[!DNL Adobe Creative Cloud]整合產生資產的變體 {#content-automation}

內容自動化附加元件將[!DNL Adobe Experience Manager Assets]整合為[!DNL Cloud Service]和[!DNL Adobe Creative Cloud] API，以大規模創意處理您的資產。 [!DNL Experience Manager]使用雲端式[資產微服務](/help/assets/asset-microservices-overview.md)來使用[!DNL Adobe Creative Cloud]功能，並自動化資產的建立和媒體處理。

若要在[!DNL Adobe Photoshop]和[!DNL Adobe Lightroom]中編輯資產，您不必從[!DNL Experience Manager Assets]下載資產、編輯和再次上傳。 您在[!DNL Experience Manager]中建立並設定處理設定檔，將設定檔套用至資料夾，然後將資產上傳至資料夾。 系統會根據處理設定檔，重新處理您上傳的資產，並取得這些資產的變數。 一致且輕鬆的大量處理可節省手動工作並提升內容速度，而不需要卓越的創意技巧。 此外，開發人員和合作夥伴可以透過直接存取這些API來擴充資產微服務，並包含自訂邏輯。

使用者可以建立處理設定檔，以自動對其資產進行下列創意操作：

* **自動色調**：使用人工智慧來分析影像內容，並依據影像的獨特屬性，聰明地校正光線和色彩。

* **自動直立**：使用人工智慧來分析影像內容並修正影像中的傾斜透視。 例如，若要建立層級視野。

  ![自動色調](/help/assets/assets/content-automation-autotone.png)

  *圖：自動色調和自動拉直有助於改善傾斜影像。*

* **Lightroom預設集**：將使用者定義的外觀套用至影像，以使用自訂的預設集達到一致的外觀。

  ![Lightroom預設集](/help/assets/assets/content-automation-lrpresets.png)

  *圖：Adobe Lightroom預設集可透過一致的方式改善許多影像的影像品質。*

* **影像挖剪圖案**：使用人工智慧在顯著物件周圍建立選取範圍，並使用單一命令移除背景。

  ![移除背景並從像片中剪下影像](/help/assets/assets/content-automation-backgroundremove.png)

* **影像遮色片**：使用人工智慧，透過單一命令在主要物件周圍建立遮色片。

  ![使用AI遮罩影像](/help/assets/assets/content-automation-mask.png)

* **Photoshop動作**：將一系列[!DNL Adobe Photoshop]工作套用至檔案或批次檔案。

  ![Photoshop動作](/help/assets/assets/content-automation-psactions.png)

* **智慧型物件取代**：可讓您交換影像，同時保留PSD檔案中套用的所有效果和調整，以大規模個人化。

  ![聰明地取代物件](/help/assets/assets/content-automation-objectreplace.png)

## 為AEM as a Cloud Service程式啟用內容自動化 {#enable-content-automation}

若要使用Cloud Manager為AEM as a Cloud Service程式啟用Content Automation附加元件：

1. 請聯絡您的客戶代表以授權Content Automation附加元件。
1. 存取Cloud Manager，並使用組織選擇器切換至您的組織。
1. 按一下&#x200B;**[!UICONTROL 新增程式]**&#x200B;並指定程式名稱。
1. 按一下「**[!UICONTROL 繼續]**」。
1. 展開&#x200B;**[!UICONTROL Assets]**&#x200B;並選取&#x200B;**[!UICONTROL Content Automation]**。
1. 按一下「**[!UICONTROL 建立]**」。
1. 執行管道以[將變更部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。

如果您需要將Content Automation附加元件新增至Cloud Manager中的現有AEM as a Cloud Service程式：

1. 按一下計畫卡上的…… 。

1. 選取&#x200B;**[!UICONTROL 編輯程式]**，然後選取&#x200B;**[!UICONTROL 解決方案和附加元件]**&#x200B;索引標籤。

1. 展開&#x200B;**[!UICONTROL Assets]**&#x200B;並選取&#x200B;**[!UICONTROL Content Automation]**。
1. 按一下&#x200B;**[!UICONTROL 更新]**。
1. 執行管道以[將變更部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。

## 使用處理設定檔來大量編輯您的創意資產 {#process-assets}

若要使用處理設定檔來自動建立變數，請遵循下列步驟：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 處理設定檔]**。

1. 選取&#x200B;**[!UICONTROL 建立]**，並指定&#x200B;**[!UICONTROL 名稱]**。

1. 選取&#x200B;**[!UICONTROL Creative]**&#x200B;索引標籤，指定輸出資料夾，選取&#x200B;**[!UICONTROL 新增]**&#x200B;以新增創意設定。

1. 提供&#x200B;**[!UICONTROL 轉譯名稱]** （或輸出名稱）、**[!UICONTROL 副檔名]** （或檔案型別）、選取&#x200B;**[!UICONTROL 品質]** （或輸出引數）、選取&#x200B;**[!UICONTROL 包含]**&#x200B;和&#x200B;**[!UICONTROL 排除]** MIME型別清單（或輸入資產篩選），並選取必要的創意作業。

   在[!UICONTROL 處理設定檔]](assets/creative-processing-profile.png)中的![[!UICONTROL Creative]索引標籤

1. 某些作業需要額外的引數（資產）。 如有必要，請為這些額外的引數提供值。

1. 將更多創意操作新增為相同處理設定檔的一部分，或儲存設定檔。

1. 將處理設定檔套用至資料夾。 在資料夾的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 資產處理]**，然後選取要套用的處理設定檔。

將處理設定檔套用至DAM資料夾後，此資料夾中上傳或更新的所有資產除了執行標準處理外，還會執行定義的操作。 子資料夾會繼承父資料夾上套用的相同設定檔。 使用者可以覆寫此繼承。

若要處理現有資產，請選取資產，選取&#x200B;**[!UICONTROL 重新處理]**&#x200B;選項，然後選取必要的處理設定檔。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager]將資產處理限製為每個環境每分鐘300個請求，每個組織每分鐘700個請求。
* [!DNL Adobe Photoshop] API作業的檔案大小限製為4 GB，[!DNL Adobe Lightroom]作業的檔案大小限製為1 GB。
* Microsoft Office檔案(「.docx」、「.doc」、「.ppt」、「.pptx」、「.xls」、「.xlsx」)的PDF轉譯僅限於100MB以下的檔案。
* 視訊轉碼僅限於15GB以下的輸入檔案。

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
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [透過處理設定檔來設定及使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)。
>* [整合 [!DNL Experience Manager] 與 [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md)。
>* [使用資產微服務進行資產擷取與處理：概覽](/help/assets/asset-microservices-overview.md)。
