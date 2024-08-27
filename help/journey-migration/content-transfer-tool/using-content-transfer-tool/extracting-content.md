---
title: 自來源擷取內容
description: 瞭解如何從來源Adobe Experience Manager (AEM)例項擷取內容，以便稍後將其傳輸至Cloud ServiceAEM例項。
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 19%

---

# 自來源擷取內容 {#extracting-content}

## 內容轉移工具中的摘取程序 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="內容摘取"
>abstract="提取是指將來源 Adobe Experience Manager (AEM) 執行個體中的內容提取到稱為移轉集的暫時區域中。移轉集是 Adobe 提供的雲端儲存區，用於暫時儲存在來源 AEM 執行個體和 Cloud Service AEM 執行個體之間轉移的內容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-extraction-process" text="填滿提取"


請依照下列步驟，從「內容轉移工具」中提取您的移轉集：

>[!NOTE]
>如果使用Amazon S3、Azure資料存放區或檔案資料存放區作為資料存放區型別，您可以執行選用的預先複製步驟以提高擷取階段的速度。 預先複製步驟在第一次完整擷取和擷取時最有效。 如需詳細資訊，請參閱[處理大型內容存放庫](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)。

1. 從&#x200B;**內容轉移**&#x200B;精靈中選取移轉集，然後按一下&#x200B;**擷取**&#x200B;開始擷取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!TIP]
   >現在，內嵌可排程在擷取成功後立即自動開始。 如需詳細資訊，請參閱[將內容擷取至Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)。

   >[!IMPORTANT]
   >
   >請確定擷取金鑰有效且不在到期日附近。 如果快到期了，您可以選取移轉集並按一下「屬性」，以續約擷取金鑰。 按一下&#x200B;**續約**。 這會將您帶往Cloud Acceleration Manager，您可以在其中按一下&#x200B;**複製擷取金鑰**。 每次按一下&#x200B;**複製擷取金鑰**時，就會產生新的擷取金鑰，從建立時起的14天有效。
   >![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. 這會顯示擷取對話方塊。 按一下&#x200B;**擷取**&#x200B;以開始擷取階段。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14b.png)

   >[!NOTE]
   >您可以選擇在提取階段期間覆寫預備容器。 如果&#x200B;**覆寫暫存容器**&#x200B;已停用，它可以加快後續移轉的擷取速度，因為內容路徑或包含版本設定尚未變更。 不過，如果內容路徑或包含版本設定已變更，則應啟用&#x200B;**覆寫暫存容器**。

1. **擷取**&#x200B;欄位現在會顯示&#x200B;**正在執行**&#x200B;狀態，表示擷取正在進行中。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   您可以按一下&#x200B;**檢視進度**&#x200B;以取得進行中擷取的精細檢視。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   您也可以造訪「內容轉移」頁面，以從Cloud Acceleration Manager監視擷取階段進度，並按一下&#x200B;**...** > **檢視詳細資料**&#x200B;以更詳細地檢視該頁面。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 擷取完成時，請檢閱其他資料行，例如&#x200B;**Source**&#x200B;和&#x200B;**路徑**，以取得您填入的移轉集詳細資訊。 按一下&#x200B;**...** > **檢視詳細資料**&#x200B;以檢視詳細資料，包括擷取每個步驟的持續時間。 在擷取期間檢視此對話方塊，以便您檢視步驟的進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## 追加提取 {#top-up-extraction-process}

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於Cloud Service上線。 如果您已在第一次完整擷取中使用預先複製步驟，您可以略過後續追加擷取的預先複製（如果追加移轉集大小小於200 GB）。 原因是它可能會增加整個程式的時間。
>此外，進行初始擷取到執行追加擷取期間，必須保持現有內容的內容結構不變。 追加無法針對自初始擷取以來結構已變更的內容執行。 請務必在移轉程式期間限制此專案。

提取程式一旦完成，您即可使用追加提取方法來轉移差異內容。

請遵循下列步驟：

1. 導覽至&#x200B;**內容轉移**&#x200B;精靈，並選取您要執行追加提取的移轉集。 按一下&#x200B;**提取**&#x200B;即可開始追加提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. **移轉集擷取**&#x200B;對話方塊隨即顯示。 按一下&#x200B;**擷取**。

   >[!IMPORTANT]
   >您必須停用&#x200B;**在提取期間覆寫預備容器**選項。
   >![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## 下一步 {#whats-next}

您已在內容轉移工具中學習從Source擷取內容後，現在即可在內容轉移工具中學習擷取程式。 請參閱[將內容擷取至Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)，瞭解如何從「內容轉移工具」擷取移轉集。
