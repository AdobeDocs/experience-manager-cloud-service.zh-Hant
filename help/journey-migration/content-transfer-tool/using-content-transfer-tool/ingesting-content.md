---
title: 將內容插入目標
description: 將內容插入目標
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 29%

---

# 將內容插入目標 {#ingesting-content}

## 內容傳輸工具中的攝取過程 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="內容攝取"
>abstract="Ingestion是指從遷移集中接收內容到目標Cloud Service實例。 「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="追加擷取"

請依照下列步驟，從「內容轉移工具」中擷取您的移轉集：
>[!NOTE]
>您可以運行可選的預複製步驟，以顯著加快接收階段。 請參閱 [使用AzCopy插入](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) 的子菜單。

1. 從中選擇遷移集 **內容傳輸** 的 **英格斯特** 開始攝取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. **移轉集擷取**&#x200B;對話框隨即顯示。一次可以將內容攝取到「作者」實例或「發佈」實例。 選擇要將內容接收到的實例。 按一下 **英格斯特** 開始攝取階段。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >如果使用預拷貝進行接收（對於S3或Azure資料儲存），建議先單獨運行Author接收。 這將在稍後運行「發佈」接收時加速。

   >[!IMPORTANT]
   >當 **在接收之前擦除雲實例上的現有內容** 選項，它將刪除整個現有儲存庫並建立新儲存庫以將內容插入。 這意味著它會重置所有設定，包括對目標Cloud Service實例的權限。 對於添加到 **管理員** 組。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   此外，按一下 **客戶服務** 記錄票證，如下圖所示。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   另請參閱 [使用內容傳輸工具的重要注意事項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) 來瞭解更多資訊。

1. 攝入完成後， **作者攝取** 更新 **已完成**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## 追加擷取 {#top-up-ingestion-process}

「內容轉移工具」具備支援&#x200B;*追加*&#x200B;差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

擷取程序一旦完成，您即可使用追加擷取方法來轉移差異內容。請遵循下列步驟：

1. 導航到 **內容傳輸** 嚮導，然後選擇要為其執行頂層攝取的遷移集。 按一下&#x200B;**擷取**&#x200B;即可開始追加提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. **移轉集擷取**&#x200B;對話框隨即顯示。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >應禁用 **在接收之前擦除雲實例上的現有內容** 選項，以防止從以前的接收活動中刪除現有內容。 此外，按一下 **客戶服務** 記錄票證，如上圖所示。

## 下一步是什麼 {#whats-next}

在內容傳輸工具中學習「將內容導入目標」後，您可以在完成每個步驟（提取和接收）後查看日誌，並查找錯誤。 請參閱 [查看遷移集的日誌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) 來瞭解更多資訊。
