---
title: 內容自動化以實現Creative Cloud整合
description: 使用Creative Cloud整合生成資產變更
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

內容自動化附加模組整合 [!DNL Adobe Experience Manager Assets] 作為 [!DNL Cloud Service] 和 [!DNL Adobe Creative Cloud] API，可創造性地按規模處理您的資產。 [!DNL Experience Manager] 使用基於雲的 [資產微服務](/help/assets/asset-microservices-overview.md) 使用 [!DNL Adobe Creative Cloud] 並自動化資產建立和介質處理。

在中編輯資產 [!DNL Adobe Photoshop] 和 [!DNL Adobe Lightroom]，您不必從 [!DNL Experience Manager Assets]，編輯並再次上載。 在中建立和配置處理配置檔案 [!DNL Experience Manager]，將配置檔案應用到資料夾，然後將資產上載到資料夾。 您上傳的資產會根據處理配置檔案重新處理，您會得到這些資產的變體。 始終如一且輕鬆的批量處理可節省手動工作並提高內容速度，而且無需高超的創作技能。 此外，開發商和合作夥伴可以通過直接訪問這些API來擴展資產微服務，並包括定制邏輯。

用戶可以建立處理配置檔案，以自動執行以下對其資產的創造性操作：

* **自動調音**:利用人工智慧對影像內容進行分析，根據影像的獨特屬性智慧地進行光和顏色校正。

* **自動直立**:利用人工智慧對影像內容進行分析，並修正影像中的偏斜透視。 例如，建立水準視圖。

   ![自動聲調](/help/assets/assets/content-automation-autotone.png)

   *圖：自動調色和自動校直有助於改善扭曲影像。*

* **Lightroom預設**:將用戶定義的外觀應用於影像，以使用自定義預設獲得一致的外觀。

   ![Lightroom預設](/help/assets/assets/content-automation-lrpresets.png)

   *圖：Adobe Lightroom預設為以一致的方式改善許多影像的影像質量。*

* **影像剪切**:使用人工智慧在顯著對象周圍建立選區，並使用單個命令刪除背景。

   ![刪除背景並從照片中剪切影像](/help/assets/assets/content-automation-backgroundremove.png)

* **影像蒙版**:使用人工智慧通過單個命令在顯著對象周圍建立蒙版。

   ![使用AI屏蔽影像](/help/assets/assets/content-automation-mask.png)

* **Photoshop行動**:應用一系列 [!DNL Adobe Photoshop] 任務到檔案或檔案批。

   ![Photoshop行動](/help/assets/assets/content-automation-psactions.png)

* **智慧對象替換**:通過允許您在保留PSD檔案中應用的所有效果和調整的同時交換影像，實現按比例個性化。

   ![智慧替換對象](/help/assets/assets/content-automation-objectreplace.png)

## 為as a Cloud Service程式啟AEM用內容自動化 {#enable-content-automation}

要使用雲管理器為as a Cloud Service程式啟AEM用內容自動附加程式：

1. 請與您的客戶代表聯繫，以許可「內容自動化」附加模組。
1. 訪問Cloud Manager，然後使用組織選擇器切換到您的組織。
1. 按一下 **[!UICONTROL 添加程式]** 並指定程式名。
1. 按一下 **[!UICONTROL 繼續]**。
1. 展開 **[!UICONTROL 資產]** 選擇 **[!UICONTROL 內容自動化]**。
1. 按一下&#x200B;**[!UICONTROL 建立]**。
1. 將管線運行到 [將更改部署到雲管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。

如果您需要將Content Automation附加模組添加到Cloud Manager中AEM的現有as a Cloud Service程式：

1. 按一下……在程式卡上。

1. 選擇 **[!UICONTROL 編輯程式]** ，然後選擇 **[!UICONTROL 解決方案和附加模組]** 頁籤。

1. 展開 **[!UICONTROL 資產]** 選擇 **[!UICONTROL 內容自動化]**。
1. 按一下 **[!UICONTROL 更新]**。
1. 將管線運行到 [將更改部署到雲管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。

## 使用處理配置檔案批量編輯您的創意資產 {#process-assets}

要使用處理配置檔案自動建立變體，請執行以下步驟：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理配置檔案]**。

1. 選擇 **[!UICONTROL 建立]**，並指定 **[!UICONTROL 名稱]**。

1. 選擇 **[!UICONTROL 創意]** 頁籤，指定輸出資料夾，選擇 **[!UICONTROL 添加新]** 的子菜單。

1. 提供 **[!UICONTROL 格式副本名稱]** （或輸出名稱）, **[!UICONTROL 擴展]** （或檔案類型），選擇 **[!UICONTROL 質量]** （或輸出參數），選擇 **[!UICONTROL 包括]** 和 **[!UICONTROL 不包括]** MIME類型清單（或輸入資產篩選器），並選擇所需的建立操作。

   ![[!UICONTROL 創意] 頁籤 [!UICONTROL 處理配置檔案]](assets/creative-processing-profile.png)

1. 某些操作需要額外的參數（資產）。 根據需要為這些額外參數提供值。

1. 將更多創意操作作為同一處理配置檔案的一部分或「保存配置檔案」。

1. 將處理配置檔案應用到資料夾。 在資料夾上 **[!UICONTROL 屬性]** ，選擇 **[!UICONTROL 資產處理]**，然後選擇要應用的處理配置檔案。

將處理配置檔案應用到DAM資料夾後，此資料夾中上載或更新的所有資產除了執行標準處理外，還會執行定義的操作。 子資料夾繼承的配置檔案與應用於父資料夾的配置檔案相同。 用戶可以覆蓋此繼承。

要處理現有資產，請選擇資產，選擇 **[!UICONTROL 重新處理]** ，然後選擇所需的處理配置檔案。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager] 將資產處理限制為每個環境每分鐘300次請求和每個組織每分鐘700次請求。
* 檔案大小限制為4 GB [!DNL Adobe Photoshop] API操作，1 GB [!DNL Adobe Lightroom] 操作。

>[!MORELIKETHIS]
>
>* [通過處理配置檔案配置和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)。
>* [整合 [!DNL Experience Manager] 與 [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md)。
>* [利用資產微服務進行資產接收和處理：概述](/help/assets/asset-microservices-overview.md)。

