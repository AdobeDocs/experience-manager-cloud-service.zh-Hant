---
title: 從來源擷取內容
description: 從來源擷取內容
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: e9af2bee0867b6787cd25f4af80cf8bf6a4d706a
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 19%

---

# 從來源擷取內容 {#extracting-content}

## 內容轉移工具中的提取程式 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="內容擷取"
>abstract="提取是指從來源AEM例項擷取內容，放入名為移轉集的暫存區域。 移轉集是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="追加提取"


請依照下列步驟，從「內容轉移工具」中提取您的移轉集：

>[!NOTE]
>如果使用Amazon S3、Azure資料存放區或檔案資料存放區作為資料存放區類型，您可以執行選用的預複製步驟，大幅加速提取階段。 預複製步驟對於第1次完全擷取和擷取最有效。 若要這麼做，您必須設定 `azcopy.config` 檔案，然後再執行解壓縮。 請參閱 [處理大型內容存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 以取得更多詳細資訊。

>[!IMPORTANT]
>從來源擷取內容之前，您應先執行「使用者對應」工具。 請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) 以取得更多詳細資訊。

1. 從中選擇遷移集 **內容轉移** 精靈，按一下 **Extract** 開始提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >請確定提取金鑰有效，且未接近其有效期。 如果快到到期日，您可以選取移轉集並按一下「屬性」，以續約提取金鑰。 按一下 **續約**. 這會帶您前往Cloud Acceleration Manager，您可在此按一下 **複製提取金鑰**. 每次您點按 **複製提取金鑰**，則會產生新的提取金鑰，自建立時起14天內有效。
   >[!影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. 這會顯示提取對話方塊。 按一下 **Extract** 開始提取階段。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
   >您可以選擇在提取階段期間覆寫預備容器。 若 **覆寫預備容器** 如果已停用，它可加快後續移轉的擷取速度，而內容路徑或包含版本設定未變更。 不過，如果內容路徑或包含版本設定已變更，則 **覆寫預備容器** 的URL。

   >[!IMPORTANT]
   >如果在從來源擷取內容之前尚未在此移轉集上執行使用者對應，您會看到警告，指出使用者對應步驟擱置中，如上圖所示。 按一下 **對應使用者** 來運行用戶映射工具。

1. 此 **提取** 欄位現在會顯示 **執行中** 狀態，指出提取正在進行中。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   您可以按一下 **查看進度** 以取得目前提取的詳細檢視。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   您也可以造訪「內容轉移」頁面，監控從Cloud Acceleration Manager提取階段的進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 提取一旦完成，請檢閱其他欄，如 **來源** 和 **路徑** 以取得您填入的移轉集詳細資訊，請按一下 **...** 然後 **查看詳細資訊**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18.png)


## 追加提取 {#top-up-extraction-process}

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。如果您已將預複製步驟用於第一次完整提取，則可以跳過預複製以用於後續追加提取（如果追加遷移集大小小於200GB），因為這可能會為整個過程增加時間。
>此外，必須不要將現有內容的內容結構從採取初始擷取時變更為執行追加擷取時。 自初始擷取後，結構已變更的內容無法執行追加。 請務必在移轉程式期間加以限制。

提取程序一旦完成，您即可使用追加提取方法來轉移差異內容。

請遵循下列步驟：

1. 導覽至 **內容轉移** 精靈，並選取您要執行追加提取的移轉集。 按一下&#x200B;**提取**&#x200B;即可開始追加提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. 此 **移轉集擷取** 對話框。按一下 **Extract**.

   >[!IMPORTANT]
   >您必須停用&#x200B;**在提取期間覆寫預備容器**選項。
   >![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## 下一步 {#whats-next}

在您學習了「內容轉移工具」中的「從來源擷取內容」後，您現在就可以了解「內容轉移工具」中的擷取程式。 請參閱 [將內容擷取至Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 了解如何從「內容轉移工具」擷取您的移轉集。
