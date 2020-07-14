---
title: 增強型智慧標記
description: 使用 Adobe Sensei 的 AI 和 ML 服務套用關聯式和描述性商業標記，以提升探索資產和處理內容的速度。
contentOwner: AG
translation-type: ht
source-git-commit: c24fa22178914b1186b7f29bdab64d3bca765fe5
workflow-type: ht
source-wordcount: '1009'
ht-degree: 100%

---


# 設定 Experience Manager 以使用資產的智慧標記 {#configure-aem-for-smart-tagging}

使用分類控制的詞彙來標記資產，以確保藉由標記式搜尋輕鬆識別及擷取資產。Adobe 提供的智慧標記可運用人工智慧和機器學習演算法來訓練影像。智慧標記會使用 [Adobe Sensei](https://www.adobe.com/tw/sensei/experience-cloud-artificial-intelligence.html) 的人工智慧架構，根據您的標記結構和商業分類訓練其影像識別演算法。

智慧標記功能可以 [!DNL Experience Manager] 附加元件的形式購買。在您購買後，系統會傳送電子郵件給您組織的管理員，並附上 Adobe 開發人員控制台的連結。管理員可存取該連結，以使用 Adobe 開發人員控制台將智慧標記與 [!DNL Experience Manager] 整合。

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
-->

## 使用 Adobe 開發人員控制台進行整合 {#aio-integration}

在使用 SCS 標記影像之前，請先使用 Adobe 開發人員控制台整合 [!DNL Adobe Experience Manager] 與智慧標記服務。在後端，伺服器會先透過 [!DNL Experience Manager] Adobe 開發人員控制台閘道驗證您的服務憑證，再將您的要求轉送至服務。

* 在 [!DNL Experience Manager] 中建立設定以產生公開金鑰。[取得公開憑證](#obtain-public-certificate)以進行 OAuth 整合。
* [在 Adobe 開發人員控制台中建立整合](#create-aio-integration)，並上傳產生的公開金鑰。
* 從 Adobe 開發人員控制台使用 API 金鑰和其他憑證，在您的 [!DNL Experience Manager] 例項中[設定智慧標記](#configure-smart-content-service)。
* [測試設定](#validate-the-configuration)。
* [在憑證過期後重新設定](#certrenew)。

### Adobe 開發人員控制台整合的必要條件 {#prerequisite-for-aio-integration}

您必須先確定下列在 Adobe 開發人員控制台上建立整合的條件，才可使用智慧標記：

* Adobe ID 帳戶具有組織的管理員權限。
* 您的組織已啟用智慧標記。

### 取得公開憑證 {#obtain-public-certificate}

公開憑證可讓您在 Adobe 開發人員控制台上驗證設定檔。您可以從 [!DNL Experience Manager] 中建立憑證。

1. 在 [!DNL Experience Manager] 使用者介面中，存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS 設定」]**。

1. 在 [!UICONTROL Adobe IMS 設定]頁面上，按一下&#x200B;**[!UICONTROL 「建立」]**。在&#x200B;**[!UICONTROL 雲端解決方案]**&#x200B;功能表中，選取&#x200B;**[!UICONTROL 「智慧標記」]**。

1. 選取&#x200B;**[!UICONTROL 「建立新憑證」]**。提供名稱，然後按一下&#x200B;**[!UICONTROL 「建立憑證」]**。按一下&#x200B;**[!UICONTROL 「確定」]**。

1. 按一下&#x200B;**[!UICONTROL 「下載公開金鑰」]**。

   ![Experience Manager 智慧標記建立公開金鑰](assets/aem_smarttags-config1.png)

### 建立整合 {#create-aio-integration}

若要使用智慧標記，請在 Adobe 開發人員控制台中建立整合，以產生 API 金鑰、技術帳戶 ID、組織 ID 和用戶端密碼。

1. 在瀏覽器中存取 [https://console.adobe.io](https://console.adobe.io/)。選取適當的帳戶，並確認相關聯的組織角色是系統管理員。
1. 以任何所需的名稱建立專案。按一下&#x200B;**[!UICONTROL 「新增 API」]**。
1. 在&#x200B;**[!UICONTROL 新增 API]** 頁面上選取&#x200B;**[!UICONTROL 「Experience Cloud」]**，然後選取&#x200B;**[!UICONTROL 「智慧內容」]**。按一下&#x200B;**[!UICONTROL 下一步]**。
1. 選取&#x200B;**[!UICONTROL 「上傳您的公開金鑰」]**。提供從 [!DNL Experience Manager] 下載的憑證檔案。畫面上會顯示[!UICONTROL 已成功上傳公開金鑰]訊息。按一下&#x200B;**[!UICONTROL 下一步]**。
1. [!UICONTROL 建立新的服務帳戶(JWT) 憑證]頁面會顯示剛設定的服務帳戶的公開金鑰。按一下&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 選取產品設定檔]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 「智慧內容服務」]**。按一下&#x200B;**[!UICONTROL 「儲存已設定的 API」]**。此時會出現一個頁面，顯示更多關於設定的資訊。請保持此頁面開啟，以便您在 [!DNL Experience Manager] 中進一步設定智慧標記時複製這些值，並將其新增至 Experience Manager 中。

   ![在「概覽」索引標籤中，您可以檢閱為整合提供的資訊。](assets/integration_details.png)

### 設定智慧標記 {#configure-smart-content-service}

若要設定整合，請使用 Adobe 開發人員控制台整合中的「裝載」、「用戶端密碼」、「授權伺服器」和「API 金鑰」等欄位的值。

1. 在 [!DNL Experience Manager] 使用者介面中，存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS 設定」]**。
1. 存取 **[!UICONTROL Adobe IMS 技術帳戶設定]**&#x200B;頁面，並提供所需的&#x200B;**[!UICONTROL 標題]**。
1. 在&#x200B;**[!UICONTROL 授權伺服器]**&#x200B;欄位中，提供 `https://ims-na1.adobelogin.com` URL。
1. 在 **[!UICONTROL API 金鑰]**&#x200B;欄位中，提供 [!DNL Adobe Developer Console] 中的&#x200B;**[!UICONTROL 用戶端 ID]**。
1. 在&#x200B;**[!UICONTROL 用戶端密碼]**&#x200B;欄位中，提供 [!DNL Adobe Developer Console] 中的&#x200B;**[!UICONTROL 用戶端密碼]**。按一下&#x200B;**[!UICONTROL 「擷取用戶端密碼」]**&#x200B;選項加以檢視。
1. 在 [!DNL Adobe Developer Console] 中，在您的專案中按一下左邊界的&#x200B;**[!UICONTROL 「服務帳戶 (JWT)」]**。按一下&#x200B;**[!UICONTROL 「產生 JWT」]**&#x200B;索引標籤。按一下&#x200B;**[!UICONTROL 「複製」]**，以複製顯示的 **[!UICONTROL JWT 裝載]**。在 [!DNL Experience Manager] 的&#x200B;**[!UICONTROL 裝載]**&#x200B;欄位中提供此值。按一下&#x200B;**[!UICONTROL 建立]**。

### 驗證設定 {#validate-the-configuration}

完成設定後，請依照下列步驟驗證設定。

1. 在 [!DNL Experience Manager] 使用者介面中，存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS 設定」]**。

1. 選取「智慧標記」設定。按一下工具列中的&#x200B;**[!UICONTROL 「檢查健全狀態」]**。按一下&#x200B;**[!UICONTROL 檢查]**。對話方塊中會顯示[!UICONTROL 設定狀況良好]訊息，確認設定正常運作中。

![驗證智慧標記設定](assets/smart-tag-config-validation.png)

### 在憑證過期時重新設定 {#certrenew}

憑證過期後，即不再受到信任。若要新增憑證，請依照下列步驟操作。您無法更新已過期的憑證。

1. 以管理員身分登入您的 [!DNL Experience Manager] 部署。按一 **[!UICONTROL 下「工具]** >安 **[!UICONTROL 全性]** >使 **[!UICONTROL 用者]**」。

1. 找到 **[!UICONTROL dam-update-service]** 使用者後按一下該使用者。按一下&#x200B;**[!UICONTROL 金鑰存放區]**&#x200B;索引標籤。
1. 刪除憑證已過期的現有 **[!UICONTROL similaritysearch]** 金鑰存放區。按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   ![刪除金鑰存放區中現有的 similaritysearch 項目，以新增安全性憑證](assets/smarttags_delete_similaritysearch_keystore.png)

   *圖：刪除金鑰存放區中現有的`similaritysearch`項目，以新增安全性憑證。*

1. 在 [!DNL Experience Manager] 使用者介面中，存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS 設定」]**。開啟可用的「智慧標記」設定。若要下載公開憑證，請按一下&#x200B;**[!UICONTROL 「下載公開憑證」]**。

1. 存取 [https://console.adobe.io](https://console.adobe.io)，並導覽至專案中的現有服務。上傳新憑證並進行設定。如需設定的詳細資訊，請參閱[建立 Adobe 開發人員控制台整合](#create-aio-integration)中的指示。

## 為新上傳的資產啟用智慧標記 (選用) {#enable-smart-tagging-for-uploaded-assets}

1. 在 [!DNL Experience Manager] 中，移至&#x200B;**[!UICONTROL 「工具 > 工作流程 > 模型」]**。
1. 在「 **[!UICONTROL 工作流模型]** 」頁面上，選擇「**[!UICONTROL DAM 更新資產]** 」工作流模型。
1. 按一下工具列中的&#x200B;**[!UICONTROL 「編輯」]**。
1. 展開「側面板」以顯示步驟。拖 **[!UICONTROL 曳DAM Workflow]**  (DAM工作流程) 區段中可用的智慧型標籤資產步驟，並將其置於&#x200B;**[!UICONTROL 「處理縮 圖」]**&#x200B;步驟之後 。

   ![在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟](assets/chlimage_1-105.png)

   *圖：在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟。*

1. 開啟要設定的步驟。在「 **[!UICONTROL 進階設定]**」下，確定已選取 **[!UICONTROL 「處理常式進階]** 」選項。

   ![設定在工作流程中繼續進行下一個步驟的處理常式。](assets/smart-tags-workflow-handler-setting.png)

1. 在&#x200B;**[!UICONTROL 引數]**&#x200B;索引標籤中，如果您要讓工作流程在預測標記時忽略失敗，請選取&#x200B;**[!UICONTROL 「忽略錯誤」]**。若無論是否對資料夾啟用智慧標記，都要在資產上傳時標記資產，請選取&#x200B;**[!UICONTROL 「忽略智慧標記旗標」]**。

1. 按一下&#x200B;**[!UICONTROL 「確定」]**&#x200B;關閉程序步驟，然後儲存工作流程。按一下&#x200B;**[!UICONTROL 「同步」]**。

>[!MORELIKETHIS]
>
>* [使用智慧服務標記資產](smart-tags.md)

