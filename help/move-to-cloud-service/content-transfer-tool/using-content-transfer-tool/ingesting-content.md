---
title: 在內容轉移工具中將內容擷取到目標中
description: 在內容轉移工具中將內容擷取到目標中
source-git-commit: d638fe0f4711bd152bd9c4be99a68662f12072e6
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 34%

---


# 在內容轉移工具中將內容擷取到目標中 {#ingesting-content}

## 內容轉移工具中的擷取程式 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="內容擷取"
>abstract="擷取是指從移轉集擷取內容，並放入目標Cloud Service例項。 「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="追加擷取"

請依照下列步驟，從「內容轉移工具」中擷取您的移轉集：
>[!NOTE]
>如果使用Amazon S3或Azure資料存放區作為資料存放區類型，您可以執行選用的預複製步驟，大幅加快擷取階段。 有關詳細資訊，請參閱[使用AzCopy擷取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) 。

1. 從&#x200B;**內容轉移**&#x200B;頁面選取移轉集，然後按一下&#x200B;**擷取**&#x200B;以開始擷取。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-01.png)

1. **移轉集擷取**&#x200B;對話框隨即顯示。一次可將內容擷取至製作例項或發佈例項。 選取要擷取內容的例項。 按一下&#x200B;**擷取**&#x200B;以開始擷取階段。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >如果使用預復本擷取（適用於S3或Azure資料存放區），建議您先單獨執行製作擷取。 這會在稍後執行時加速發佈擷取。

   >[!IMPORTANT]
   >啟用「在擷取&#x200B;**之前擦去雲端例項上的現有內容」選項時，它會刪除整個現有存放庫，並建立新存放庫以將內容擷取至中。**&#x200B;這表示會重設所有設定，包括目標Cloud Service例項的權限。 對於新增至&#x200B;**administrators**&#x200B;群組的管理員使用者，也是如此。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-03.png)

   此外，按一下&#x200B;**客戶服務**&#x200B;來記錄票證，如下圖所示。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-04.png)

   另請參閱[使用內容轉移工具的重要考量](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations)以深入了解。

1. 擷取完成後，**製作擷取**&#x200B;底下的狀態會更新為&#x200B;**FINISHED**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

## 追加擷取 {#top-up-ingestion-process}

「內容轉移工具」具備支援&#x200B;*追加*&#x200B;差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

擷取程序一旦完成，您即可使用追加擷取方法來轉移差異內容。請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要執行追加擷取的移轉集。按一下&#x200B;**擷取**&#x200B;即可開始追加提取。**移轉集擷取**&#x200B;對話框隨即顯示。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >您應停用「擷取&#x200B;**之前擦去雲端例項上的現有內容」選項，以防止從先前的擷取活動中刪除現有內容。**&#x200B;此外，按一下&#x200B;**客戶服務**&#x200B;來記錄票證，如上圖所示。
