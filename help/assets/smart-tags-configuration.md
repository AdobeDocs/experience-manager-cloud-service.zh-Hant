---
title: 增強的智慧型標籤
description: 使用Adobe Sensei的AI和ML服務套用情境式和描述式商業標籤，以改善資產發現和內容速度。
contentOwner: AG
translation-type: tm+mt
source-git-commit: bf7bb91dd488f39181a08adc592971d6314817de
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 12%

---


# 設定Experience Manager以智慧標籤資產 {#configure-aem-for-smart-tagging}

使用分類控制的辭彙來標籤資產，可確保透過標籤搜尋輕鬆識別和擷取資產。 Adobe提供智慧型標籤，使用人工智慧和機器學習演算法來訓練影像。 智慧型標籤使用 [Adobe Sensei的人工智慧架構](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) ，針對您的標籤結構和商業分類法訓練其影像識別演算法。

智慧型標籤功能可作為附加元件購買 [!DNL Experience Manager]。 在您購買後，系統會寄送電子郵件給您組織的管理員，並附上Adobe I/O的連結。 管理員會存取連結以整合智慧型標籤與 [!DNL Experience Manager] 使用Adobe I/O。

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## 與Adobe I/O整合 {#aio-integration}

在使用SCS標籤影像之前，請使 [!DNL Adobe Experience Manager] 用Adobe I/O與「智慧標籤」服務整合。 在後端，伺服器會先 [!DNL Experience Manager] 使用Adobe I/O閘道驗證您的服務認證，然後再將您的要求轉送至服務。

* 在中建立配 [!DNL Experience Manager] 置以生成公共密鑰。 取得OAuth整合的公用憑證。
* 在Adobe I/O中建立整合，並上傳產生的公開金鑰。
* 使用 [!DNL Experience Manager] API金鑰和Adobe I/O的其他認證來設定您的例項。
* （可選）在資產上傳時啟用自動標籤。

### Adobe I/O整合的先決條件 {#prerequisite-for-aio-integration}

在使用智慧型標籤之前，請確定下列項目以建立Adobe I/O整合：

* 具有組織管理員權限的Adobe ID帳戶。
* 您的組織會啟用智慧標籤。

### Obtain a public certificate {#obtain-public-certificate}

公開憑證可讓您在Adobe I/O上驗證您的個人檔案。

1. 在使用 [!DNL Experience Manager] 者介面中，存 **[!UICONTROL 取「工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務]**」。

1. On the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. 在「建 **[!UICONTROL 立設定]** 」對話方塊中，指定「智慧標籤」設定的標題和名稱。 按一下&#x200B;**[!UICONTROL 建立]**。

1. 在「 **[!UICONTROL AEM智慧型內容服務]** 」對話方塊中，使用下列值：

   **[!UICONTROL 服務 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授權伺服器]**: `https://ims-na1.adobelogin.com`

   現在將其他欄位留空（稍後將提供）。 按一下 **[!UICONTROL 確定]**。

   ![Experience Manager Smart Content Service對話框，用於提供內容服務URL](assets/aem_scs.png)

1. 按一 **[!UICONTROL 下「下載OAuth整合的公用憑證]**」，然後下載公用憑證檔案 `AEM-SmartTags.crt`。

   ![為智慧標籤服務建立的設定](assets/download_link.png)

### 如果證書過期，請重新配置 {#certrenew}

當憑證過期時，它不再受信任。 若要新增憑證，請依照下列步驟進行。 您無法為過期的憑證續約。

1. Log in your [!DNL Experience Manager] deployment as an administrator. 按一 **[!UICONTROL 下「工具]** >安 **[!UICONTROL 全性]** >使 **[!UICONTROL 用者]**」。

1. 找到並按 **[!UICONTROL 一下dam-update-service使用者]** 。 按一下「密鑰 **[!UICONTROL 庫]** 」頁籤。
1. 刪除具有過 **[!UICONTROL 期證書的]** 現有相似性search密鑰庫。 Click **[!UICONTROL Save &amp; Close]**.

   ![刪除Keystore中現有的相似性搜尋項目，以新增安全憑證](assets/smarttags_delete_similaritysearch_keystore.png)

   *圖： 刪除Keystore中`similaritysearch`的現有條目，以添加新的安全證書。*

1. 導覽至「 **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務」]**。按一 **[!UICONTROL 下「資產智慧標籤]** >顯 **[!UICONTROL 示設定]** >可 **[!UICONTROL 用設定」]**。按一下所需的設定。

1. 若要下載公用憑證，請按一下「 **[!UICONTROL 下載OAuth整合的公用憑證」]**。

1. 存 [取https://console.adobe.io](https://console.adobe.io) ，並導覽至專案中的現有服務。 上傳新憑證。 如需詳細資訊，請參閱「建立 [Adobe I/O整合」中的指示](#create-aio-integration)。

### 建立整合 {#create-aio-integration}

若要使用智慧型標籤API，請在Adobe I/O中建立整合，以產生API金鑰、技術帳戶ID、組織ID和用戶端密碼。

1. 存取 [https://console.adobe.io](https://console.adobe.io/)。
1. 選擇適當的帳戶並驗證關聯的組織角色是系統管理員。 建立專案或開啟現有專案。 在專案頁面上，按一下「 **[!UICONTROL 新增API」]**。
1. 在「新 **[!UICONTROL 增API]** 」頁面上，選 **[!UICONTROL 取「Experience Cloud]** 」並選 **[!UICONTROL 取「智慧內容]**」。 按一 **[!UICONTROL 下繼續]**。
1. 在下一頁，選擇「新 **[!UICONTROL 增整合」]**。 按一 **[!UICONTROL 下繼續]**。
1. 在「整 **[!UICONTROL 合詳細資訊]** 」頁面上，指定整合閘道的名稱並新增說明。
1. 在公 **[!UICONTROL 開金鑰憑證中]**，上 `AEM-SmartTags.crt` 傳您先前下載的檔案。
1. 按一下&#x200B;**[!UICONTROL 建立整合項目]**。
1. 若要檢視整合資訊，請按一下「 **[!UICONTROL 繼續」以取得整合詳細資訊]**。

   ![在「概述」索引標籤中，您可以檢閱為整合提供的資訊。](assets/integration_details.png)

### 設定智慧標籤 {#configure-smart-content-service}

若要設定整合，請使用Adobe I/O整合中「技術帳戶ID」、「組織ID」、「用戶端密碼」、「授權伺服器」和「API金鑰」欄位的值。 建立智慧型標籤雲端設定可讓您驗證來自例項的API [!DNL Experience Manager] 請求。

1. 在中 [!DNL Experience Manager]，導覽至「 **[!UICONTROL 工具>雲端服務>舊版雲端服務」以開啟]** Cloud Services  Console。
1. 在「資 **[!UICONTROL 產智慧標籤]**」下，開啟上述建立的設定。 在服務設定頁面上，按一下「 **[!UICONTROL 編輯]**」。
1. 在「 **[!UICONTROL AEM Smart Content Service]** 」對話方塊中 **[!UICONTROL ，使用「服務URL」和「授權伺服器」欄位的預先填入值]****** 。
1. 對於「 **[!UICONTROL API金鑰]**」、「 **[!UICONTROL Technical Account Id]**」、「 **[!UICONTROL Organization Id]**」和「Client Secret **[!UICONTROL 」欄位，請使]**&#x200B;用上述產生的值。

### 驗證配置 {#validate-the-configuration}

完成配置後，可使用JMX MBean來驗證配置。 若要驗證，請遵循下列步驟。

1. 訪問您 [!DNL Experience Manager] 的伺服器 `https://[aem_server]:[port]`。

1. 前往「 **[!UICONTROL 工具>作業> Web Console]** 」以開啟OSGi主控台。 按一 **[!UICONTROL 下「主要> JMX]**」。
1. 按一 **[!UICONTROL 下com.day.cq.dam.similaritysearch.internal.impl]**。 它會開啟「 **[!UICONTROL 相似性搜尋雜項任務」]**。
1. 按一 **[!UICONTROL 下validateConfigs()]**。 在「驗證 **[!UICONTROL 配置」對話]** ，按一下 **[!UICONTROL 調用]**。

   驗證結果會顯示在相同的對話方塊中。

## 為新上傳的資產啟用智慧標籤（可選） {#enable-smart-tagging-for-uploaded-assets}

1. 在中， [!DNL Experience Manager]請轉至「工 **[!UICONTROL 具」>「工作流」>「模型」]**。
1. 在「工 **[!UICONTROL 作流模型]** 」頁面上，選擇 **** 「DAM更新資產」工作流模型。
1. 從工具 **[!UICONTROL 列按一下]** 「編輯」。
1. 展開「側面板」以顯示步驟。拖 **[!UICONTROL 曳DAM Workflow]**  (DAM工作流程) 區段中可用的智慧型標籤資產步驟，並將其置於「處理縮 **[!UICONTROL 圖」步驟之後]** 。

   ![在「DAM更新資產」工作流程中，在流程縮圖步驟之後新增智慧型標籤資產步驟](assets/chlimage_1-105.png)

   *圖： 在「DAM更新資產」工作流程中，在流程縮圖步驟之後新增智慧型標籤資產步驟。*

1. 開啟要設定的步驟。 在「 **[!UICONTROL 進階設定]**」下，確定已選 **[!UICONTROL 取「處理常式進階]** 」選項。

   ![設定處理常式，以進入工作流程的下一個步驟。](assets/smart-tags-workflow-handler-setting.png)

1. 在「參 **[!UICONTROL 數]** 」頁籤中，如果希望工作流在預測標籤時忽略失敗 **** ，請選擇「忽略錯誤」。 若要在資產上傳時標籤資產，而不論資料夾上是否啟用智慧型標籤，請選取「忽略智慧 **[!UICONTROL 型標籤標籤」]**。

1. 按一下 **[!UICONTROL 確定]** ，關閉流程步驟，然後保存工作流。 按一 **[!UICONTROL 下同步]**。

>[!MORELIKETHIS]
>
>* [使用智慧型服務來標籤資產](smart-tags.md)

