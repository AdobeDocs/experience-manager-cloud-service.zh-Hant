---
title: 自來源擷取內容
description: 自來源擷取內容
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 27%

---

# 自來源擷取內容 {#extracting-content}

## 內容轉移工具中的提取程式 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="內容提取"
>abstract="提取是指將來源 AEM 執行個體中的內容提取到稱為移轉集的暫時區域中。移轉集是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=zh-Hant#top-up-extraction-process" text="填滿提取"


請依照下列步驟，從「內容轉移工具」中提取您的移轉集：

>[!NOTE]
>如果使用Amazon S3、Azure資料存放區或檔案資料存放區作為資料存放區型別，您可以執行選用的預先複製步驟，大幅加快擷取階段。 預先複製步驟對第1次完整擷取和擷取最為有效。 另請參閱 [處理大型內容存放庫](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 以取得更多詳細資料。

1. 選取移轉集來源 **內容轉移** 精靈並按一下 **Extract** 以開始擷取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >請確定擷取金鑰有效且未接近其有效期。 如果快到期了，您可以選取移轉集並按一下「屬性」，以續約擷取金鑰。 按一下 **續約**. 這會將您帶到Cloud Acceleration Manager，您可以在其中按一下 **複製擷取金鑰**. 每次您按一下 **複製擷取金鑰**，會產生新的擷取金鑰，其有效期為從建立當日起的14天。
   >![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. 此時會顯示「擷取」對話方塊。 按一下 **Extract** 以開始提取階段。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
   >您可以選擇在提取階段期間覆寫預備容器。 若 **覆寫暫存容器** 停用「 」，可在內容路徑或包含版本設定未變更時，加快後續移轉的擷取速度。 不過，如果內容路徑或包含版本設定已變更，則 **覆寫暫存容器** 應該已啟用。

1. 此 **摘取** 欄位現在顯示 **執行中** 狀態，表示擷取正在進行中。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   您可以按一下 **檢視進度** 以取得進行中擷取的精細檢視。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   您也可以造訪「內容轉移」頁面，從Cloud Acceleration Manager監視提取階段進度，並按一下 **...** 然後開啟 **檢視詳細資料**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 擷取完成後，請檢閱其他欄，例如 **來源** 和 **路徑** 如需您透過按一下來填入的移轉集詳細資訊 **...** 然後開啟 **檢視詳細資料** 以檢視詳細資訊，包括擷取每個步驟的持續時間。 在擷取期間檢視此對話方塊，以檢視步驟的進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## 追加提取 {#top-up-extraction-process}

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。如果您已使用預先複製步驟進行第一次完整擷取，您可以略過預先複製以進行後續追加擷取（如果追加移轉集大小小於200GB），因為這樣可能會增加整個程式的時間。
>此外，從初次擷取到執行追加擷取期間，現有內容的內容結構必須不會變更。 追加無法針對自初始擷取以來結構已變更的內容執行。 請務必在移轉程式期間限制此專案。

提取程序一旦完成，您即可使用追加提取方法來轉移差異內容。

請遵循下列步驟：

1. 導覽至 **內容轉移** 精靈並選取您要執行追加提取的移轉集。 按一下&#x200B;**提取**&#x200B;即可開始追加提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. 此 **移轉集擷取** 對話方塊隨即顯示。按一下 **Extract**.

   >[!IMPORTANT]
   >您必須停用&#x200B;**在提取期間覆寫預備容器**選項。
   >![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## 下一步 {#whats-next}

一旦您學習了在「內容轉移工具」中從來源擷取內容，您現在就可以在「內容轉移工具」中學習擷取程式了。 另請參閱 [將內容擷取至Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 以瞭解如何從「內容轉移工具」內嵌移轉集。
