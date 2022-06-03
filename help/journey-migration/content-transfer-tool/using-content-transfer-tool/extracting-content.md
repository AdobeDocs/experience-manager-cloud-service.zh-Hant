---
title: 從源中提取內容
description: 從源中提取內容
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 5075482f48bf9aaf2c7386af74c14a50b4469840
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 19%

---

# 從源中提取內容 {#extracting-content}

## 內容傳輸工具中的抽取過程 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="內容提取"
>abstract="抽取是指將源實例中的內AEM容提取到稱為遷移集的臨時區域。 移轉集是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="上頂提取"


請依照下列步驟，從「內容轉移工具」中提取您的移轉集：

>[!NOTE]
>如果將AmazonS3、Azure資料儲存或檔案資料儲存用作資料儲存類型，則可以運行可選的預複製步驟以顯著加快提取階段。 預拷貝步驟對第一次完全提取和攝取最有效。 為此，您需要配置 `azcopy.config` 檔案，然後運行抽取。 請參閱 [處理大型內容儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 的子菜單。

>[!IMPORTANT]
>在從源中提取內容之前，應運行「用戶映射」工具。 請參閱 [使用用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) 的子菜單。

1. 從中選擇遷移集 **內容傳輸** 嚮導 **提取** 開始提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >!![IMPORTANT]
   確保抽取密鑰有效且未接近其到期。 如果它接近到其到期日期，則可以通過選擇遷移集並按一下「屬性」來續訂抽取密鑰。 按一下 **續訂**。 這將帶您到雲加速管理器，您可以在其中按一下 **複製提取密鑰**。 每次你點擊 **複製提取密鑰**，將生成一個新抽取密鑰，該密鑰自建立之日起有效14天。
   [!影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. 這將顯示「提取」對話框。 按一下 **提取** 開始提取階段。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
您可以選擇在提取階段覆蓋轉移容器。 如果 **覆蓋暫存容器** 如果禁用，則它可以加快後續遷移的提取速度，其中內容路徑或包括版本設定未更改。 但是，如果內容路徑或包含版本設定已更改，則 **覆蓋暫存容器** 應啟用。

   >[!IMPORTANT]
如果在從源中提取內容之前尚未在此遷移集上運行用戶映射，您將看到一個警告，顯示「用戶映射」步驟處於掛起狀態，如上圖所示。 按一下 **映射用戶** 以運行用戶映射工具。

1. 的 **提取** 欄位現在顯示 **正在運行** 狀態，指示正在提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   可以按一下 **查看進度** 以細緻地瞭解正在進行的提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   您還可以通過訪問「內容傳輸」頁來監視Cloud Acceleration Manager的提取階段進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 提取完成後，查看其他列，如 **源** 和 **路徑** 有關通過按一下 **...** 然後 **查看詳細資訊**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18.png)


## 追加提取 {#top-up-extraction-process}

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。如果已將預複製步驟用於第一次完全提取，則可以跳過預複製步驟以進行後續的自頂向上提取（如果自頂向上遷移集大小小於200GB），因為它可能會為整個過程添加時間。
此外，從初始提取到運行頂層提取時，必須不改變現有內容的內容結構。 無法對自初始提取後結構已更改的內容運行頂層。 請確保在遷移過程中限制此操作。

提取程序一旦完成，您即可使用追加提取方法來轉移差異內容。

請遵循下列步驟：

1. 導航到 **內容傳輸** 嚮導，然後選擇要為其執行頂部抽取的遷移集。 按一下&#x200B;**提取**&#x200B;即可開始追加提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. 的 **遷移集提取** 對話框。按一下 **提取**。

   >[!IMPORTANT]您必須停用&#x200B;**在提取期間覆寫預備容器**選項。
   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## 下一步 {#whats-next}

在內容傳輸工具中學習了從源中提取內容後，您現在就可以學習內容傳輸工具中的攝取過程。 請參閱 [將內容插入目標](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 瞭解如何從內容傳輸工具中獲取遷移集。
