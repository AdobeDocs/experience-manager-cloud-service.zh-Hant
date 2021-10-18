---
title: 從來源擷取內容
description: 從來源擷取內容
source-git-commit: 86df5e29567d9da8bc56c1c62b11ab1444586415
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 39%

---


# 從來源擷取內容 {#extracting-content}

## 內容轉移工具中的提取程式 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="內容擷取"
>abstract="提取是指從來源AEM例項擷取內容，放入名為移轉集的暫存區域。 移轉集是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="追加提取"

>[!IMPORTANT]
>從來源擷取內容之前，您應先執行「使用者對應」工具。 請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) 以取得更多詳細資訊。

請依照下列步驟，從「內容轉移工具」中提取您的移轉集：
>[!NOTE]
>如果使用Amazon S3或Azure資料存放區作為資料存放區類型，您可以執行選用的預複製步驟，大幅加速提取階段。 若要這麼做，您必須設定 `azcopy.config` 檔案，然後再執行解壓縮。 請參閱 [處理大型內容存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 以取得更多詳細資訊。

1. 從中選擇遷移集 **內容轉移** 精靈，按一下 **Extract** 開始提取。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-01.png)

1. 此 **移轉集擷取** 對話框顯示，然後按一下 **Extract** 開始提取階段。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >您可以選擇在提取階段中覆寫預備容器。

1. 此 **提取** 欄位現在會顯示 **執行中** 狀態，指出提取正在進行中。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-03.png)

   提取一旦完成，移轉集的狀態會更新為&#x200B;**已完成**，而&#x200B;**資訊**&#x200B;欄位下會顯示一個&#x200B;*實心綠色*&#x200B;的雲朵圖示。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >UI具有自動重新載入功能，可重新載入 **內容轉移** 精靈每30秒。
   >提取階段開始時將建立寫入鎖定，並在 *60 秒*&#x200B;後釋放。因此，如果提取停止，則需等待一分鐘才能釋放鎖定並重新開始提取。

## 追加提取 {#top-up-extraction-process}

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。
>此外，必須不要將現有內容的內容結構從採取初始擷取時變更為執行追加擷取時。 自初始擷取後，無法對結構已變更的內容執行追加。 請務必在移轉程式期間加以限制。

提取程序一旦完成，您即可使用追加提取方法來轉移差異內容。

請遵循下列步驟：

1. 導覽至 **內容轉移** 精靈，並選取您要執行追加提取的移轉集。 按一下&#x200B;**提取**&#x200B;即可開始追加提取。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-05.png)

1. 此 **移轉集擷取** 對話框。按一下 **Extract**.

   >[!IMPORTANT]
   >您必須停用&#x200B;**在提取期間覆寫預備容器**選項。
   >![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-06.png)


## 下一步 {#whats-next}

在您學習了「內容轉移工具」中的「從來源擷取內容」後，您現在就可以了解「內容轉移工具」中的擷取程式。 請參閱 [將內容擷取至Target](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 了解如何從「內容轉移工具」擷取您的移轉集。
