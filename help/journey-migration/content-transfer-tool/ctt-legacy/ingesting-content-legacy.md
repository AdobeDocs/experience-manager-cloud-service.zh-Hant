---
title: 將內容擷取至Target（舊版）
description: 將內容擷取至Target
hide: true
hidefromtoc: true
exl-id: 326b3e98-5055-49b5-a005-63fd3ca35202
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 26%

---

# 將內容擷取至Target（舊版） {#ingesting-content}

## 內容轉移工具中的擷取程式 {#ingestion-process}

請依照下列步驟，從「內容轉移工具」中擷取您的移轉集：
>[!NOTE]
>您可以執行選用的預先複製步驟，大幅加快擷取階段。 請參閱 [使用AzCopy擷取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) 以取得更多詳細資訊。

1. 從中選擇遷移集 **內容轉移** 頁面，按一下 **內嵌** 開始擷取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. **移轉集擷取**&#x200B;對話框隨即顯示。一次可將內容擷取至製作例項或發佈例項。 選取要擷取內容的例項。 按一下 **內嵌** 以開始擷取階段。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >如果使用預復本擷取（適用於S3或Azure資料存放區），建議您先單獨執行製作擷取。 這會在稍後執行時加速發佈擷取。

   >[!IMPORTANT]
   >當 **擷取前先擦去雲端例項上的現有內容** 選項，該選項將刪除整個現有儲存庫並建立新儲存庫以將內容嵌入。 這表示會重設所有設定，包括目標Cloud Service例項的權限。 對於新增至 **管理員** 群組。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   此外，按一下 **客戶服務** 記錄票證，如下圖所示。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   另請參閱 [使用內容轉移工具的重要考量](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) 了解更多。

1. 擷取完成後， **製作擷取** 更新至 **已完成**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## 追加擷取 {#top-up-ingestion-process}

「內容轉移工具」具備支援&#x200B;*追加*&#x200B;差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

擷取程序一旦完成，您即可使用追加擷取方法來轉移差異內容。請遵循下列步驟：

1. 導覽至 **內容轉移** 精靈，並選取您要執行追加擷取的移轉集。 按一下&#x200B;**擷取**&#x200B;即可開始追加提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. **移轉集擷取**&#x200B;對話框隨即顯示。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >您應停用 **擷取前先擦去雲端例項上的現有內容** 選項，以防止從先前的擷取活動中刪除現有內容。 此外，按一下 **客戶服務** 記錄票證，如上圖所示。

## 下一步 {#whats-next}

在內容轉移工具中學習將內容擷取至Target後，您就可以在完成每個步驟（擷取和擷取）時檢視記錄，並尋找錯誤。 請參閱 [檢視移轉集記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) 了解更多。
