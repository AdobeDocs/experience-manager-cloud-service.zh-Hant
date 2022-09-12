---
title: Creative Cloud整合的內容自動化
description: 使用Creative Cloud整合產生資產變數
contentOwner: AG
feature: Upload,Asset Processing,Publishing,Asset Compute Microservices,Workflow
role: User,Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 30870502f0e6084991bdba79163651f43f15a99b
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# 使用 [!DNL Adobe Creative Cloud] 整合 {#content-automation}

內容自動化附加元件整合 [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] 和 [!DNL Adobe Creative Cloud] API，以創意方式大規模處理您的資產。 [!DNL Experience Manager] 使用雲端型 [資產微服務](/help/assets/asset-microservices-overview.md) 使用 [!DNL Adobe Creative Cloud] 功能，並自動化資產建立和媒體處理。

若要在中編輯資產 [!DNL Adobe Photoshop] 和 [!DNL Adobe Lightroom]，您不必從下載資產 [!DNL Experience Manager Assets]、編輯，然後再次上傳。 您可以在 [!DNL Experience Manager]，將設定檔套用至資料夾，然後上傳資產至資料夾。 您上傳的資產會根據處理設定檔重新處理，而您會得到這些資產的變體。 一致且輕鬆的大量處理功能可節省手動工作量並提升內容速度，而無須精湛的創意技能。 此外，開發人員和合作夥伴可以直接存取這些API，並包含自訂邏輯，以擴充資產微服務。

使用者可以建立處理設定檔，以自動處理其資產的下列創意操作：

* **自動色調**:利用人工智慧分析影像的內容，並根據影像的獨特屬性智慧地進行光和顏色校正。

* **自動直立**:利用人工智慧對影像內容進行分析，對影像中的傾斜透視進行修正。 例如，要建立層視線。

   ![自動色調](/help/assets/assets/content-automation-autotone.png)

   *圖：自動調色和自動拉直有助於改善傾斜影像。*

* **Lightroom預設集**:使用自訂預設集對影像套用使用者定義的外觀，以達到一致的外觀。

   ![Lightroom預設集](/help/assets/assets/content-automation-lrpresets.png)

   *圖：Adobe Lightroom預設集，以一致方式改善許多影像的影像品質。*

* **影像挖剪**:使用人工智慧在顯著對象周圍建立選擇，並使用單個命令刪除背景。

   ![移除背景並從像片中剪下影像](/help/assets/assets/content-automation-backgroundremove.png)

* **影像遮色片**:使用人工智慧在突出物體周圍使用單一命令建立掩模。

   ![使用AI遮罩影像](/help/assets/assets/content-automation-mask.png)

* **Photoshop動作**:套用一系列 [!DNL Adobe Photoshop] 對檔案或批次檔案執行任務。

   ![Photoshop動作](/help/assets/assets/content-automation-psactions.png)

* **智慧型物件取代**:允許您交換影像，同時保留套用在PSD檔案中的所有效果和調整，以大規模個人化。

   ![智慧替換對象](/help/assets/assets/content-automation-objectreplace.png)

## 為AEMas a Cloud Service計畫啟用內容自動化 {#enable-content-automation}

若要使用Cloud Manager啟用AEMas a Cloud Service程式的「內容自動化」附加元件：

1. 請連絡您的客戶代表，以授權「內容自動化」附加元件。
1. 存取Cloud Manager，並使用組織選取器切換至您的組織。
1. 按一下 **[!UICONTROL 添加程式]** 並指定程式名。
1. 按一下 **[!UICONTROL 繼續]**.
1. 展開 **[!UICONTROL 資產]** 選取 **[!UICONTROL 內容自動化]**.
1. 按一下&#x200B;**[!UICONTROL 建立]**。
1. 將管線運行到 [部署對Cloud Manager的變更](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

如果您需要將「內容自動化」附加元件新增至Cloud Manager中現有的AEMas a Cloud Service程式：

1. 按一下程式卡上的。

1. 選擇 **[!UICONTROL 編輯方案]** 然後選取 **[!UICONTROL 解決方案和附加元件]** 標籤。

1. 展開 **[!UICONTROL 資產]** 選取 **[!UICONTROL 內容自動化]**.
1. 按一下 **[!UICONTROL 更新]**.
1. 將管線運行到 [部署對Cloud Manager的變更](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## 使用處理設定檔大量編輯創意資產 {#process-assets}

若要使用處理設定檔來自動建立變異，請遵循下列步驟：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**.

1. 選擇 **[!UICONTROL 建立]**，並指定 **[!UICONTROL 名稱]**.

1. 選取 **[!UICONTROL 創意]** 頁簽，指定輸出資料夾，選擇 **[!UICONTROL 新增]** 來新增創意配置。

1. 提供 **[!UICONTROL 轉譯名稱]** （或輸出名稱）, **[!UICONTROL 擴充功能]** （或檔案類型），選擇 **[!UICONTROL 品質]** （或輸出參數），選擇 **[!UICONTROL 包含]** 和 **[!UICONTROL 排除]** MIME類型會列出（或輸入資產篩選器），然後選取所需的創作操作。

   ![[!UICONTROL 創意] 標籤 [!UICONTROL 處理設定檔]](assets/creative-processing-profile.png)

1. 某些操作需要額外的參數（資產）。 視需要提供這些額外參數的值。

1. 將更多創意操作新增為相同處理設定檔的一部分，或儲存設定檔。

1. 將處理設定檔套用至資料夾。 在資料夾的 **[!UICONTROL 屬性]** 頁面，選取 **[!UICONTROL 資產處理]**，然後選取要套用的處理設定檔。

將處理設定檔套用至DAM資料夾後，除了標準處理作業外，此資料夾中上傳或更新的所有資產都會執行已定義的作業。 子資料夾會繼承與父資料夾上套用的相同設定檔。 使用者可以覆寫此繼承。

若要處理現有資產，請選取資產，然後選取 **[!UICONTROL 重新處理]** 選項，然後選取所需的處理設定檔。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager] 將資產處理限制為每個環境每分鐘300個請求，以及每個組織每分鐘700個請求。
* 檔案大小限制為4 GB [!DNL Adobe Photoshop] API操作，1 GB [!DNL Adobe Lightroom] 操作。

>[!MORELIKETHIS]
>
>* [透過處理設定檔來設定和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md).
>* [整合 [!DNL Experience Manager] with [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [透過資產微服務擷取和處理資產：概述](/help/assets/asset-microservices-overview.md).

