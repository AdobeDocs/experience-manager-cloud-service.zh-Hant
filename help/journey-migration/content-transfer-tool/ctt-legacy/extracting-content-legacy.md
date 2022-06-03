---
title: 從源中提取內容（舊版）
description: 從源中提取內容
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 36%

---

# 從源中提取內容（舊版） {#extracting-content}

## 內容傳輸工具中的抽取過程 {#extraction-process}

請依照下列步驟，從「內容轉移工具」中提取您的移轉集：
>[!NOTE]
>如果將AmazonS3或Azure資料儲存用作資料儲存的類型，則可以運行可選的預複製步驟以顯著加快提取階段。 為此，您需要配置 `azcopy.config` 檔案，然後運行抽取。 請參閱 [處理大型內容儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 的子菜單。

>[!IMPORTANT]
>在從源中提取內容之前，應運行「用戶映射」工具。 請參閱 [使用用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) 的子菜單。

1. 從中選擇遷移集 **內容傳輸** 嚮導 **提取** 開始提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. 的 **遷移集提取** 對話框顯示並按一下 **提取** 開始提取階段。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >您可以選擇在提取階段中覆寫預備容器。

   >[!IMPORTANT]
   >如果在從源中提取內容之前尚未在此遷移集上運行用戶映射，您將看到一個警告，顯示「用戶映射」步驟處於掛起狀態，如下圖所示。 按一下 **映射用戶** 以運行用戶映射工具。
   >![影像](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. 的 **提取** 欄位現在顯示 **正在運行** 狀態，指示正在提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   提取一旦完成，移轉集的狀態會更新為&#x200B;**已完成**，而&#x200B;**資訊**&#x200B;欄位下會顯示一個&#x200B;*實心綠色*&#x200B;的雲朵圖示。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >UI具有自動重新載入功能，可重新載入 **內容傳輸** 嚮導。
   >提取階段開始時將建立寫入鎖定，並在 *60 秒*&#x200B;後釋放。因此，如果提取停止，則需等待一分鐘才能釋放鎖定並重新開始提取。

## 追加提取 {#top-up-extraction-process}

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。
>此外，從初始提取到運行頂層提取時，必須不改變現有內容的內容結構。 無法對自初始提取後結構已更改的內容運行頂層。 請確保在遷移過程中限制此操作。

提取程序一旦完成，您即可使用追加提取方法來轉移差異內容。

請遵循下列步驟：

1. 導航到 **內容傳輸** 嚮導，然後選擇要為其執行頂部抽取的遷移集。 按一下&#x200B;**提取**&#x200B;即可開始追加提取。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. 的 **遷移集提取** 對話框。按一下 **提取**。

   >[!IMPORTANT]
   >您必須停用&#x200B;**在提取期間覆寫預備容器**選項。
   >![影像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## 下一步 {#whats-next}

在內容傳輸工具中學習了從源中提取內容後，您現在就可以學習內容傳輸工具中的攝取過程。 請參閱 [將內容插入目標](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 瞭解如何從內容傳輸工具中獲取遷移集。
