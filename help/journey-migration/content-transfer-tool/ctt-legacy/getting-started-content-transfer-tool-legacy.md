---
title: 內容轉移工具快速入門（舊版）
description: 內容轉移工具快速入門
hide: true
hidefromtoc: true
exl-id: a6ee6996-510e-42d7-9a7c-f64732764f97
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 21%

---

# 內容轉移工具快速入門（舊版） {#getting-started-content-transfer-tool}


## 可用性 {#availability}

您可以從軟體發佈入口網站下載「內容轉移工具」的ZIP檔案。 您可以透過 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 在來源Adobe Experience Manager(AEM)例項上。 請務必下載最新版本。 如需最新版本的詳細資訊，請參閱 [發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載內容轉移工具。

## 源環境連接 {#source-environment-connectivity}

源AEM實例可能在防火牆後運行，在防火牆中它只能訪問已添加到允許清單中的某些主機。 若要成功執行擷取，必須從執行AEM的執行個體存取下列端點：

* 目標AEMas a Cloud Service環境： `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure blob儲存服務： `*.blob.core.windows.net`
* 用戶映射IO終結點： `usermanagement.adobe.io`

若要測試與目標AEMas a Cloud Service環境的連線，請從來源例項的殼層發出下列cURL命令(取代 `program_id`, `environment_id`，和 `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>若 `HTTP/2 200` 收到時，與AEMas a Cloud Service的連線成功。

## 執行「內容轉移工具」  {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


請依照以下章節了解如何使用「內容轉移工具」，將內容移轉至 AEM as a Cloud Service (製作/發佈)：

1. 選取Adobe Experience Manager並導覽至工具 — > **操作** -> **內容移轉**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. 選取 **內容轉移** 選項 **內容移轉** 嚮導。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. 建立第一個移轉集時，會顯示下列主控台。 按一下&#x200B;**建立移轉集**&#x200B;以建立新的移轉集。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >如果您有現有的移轉集，主控台會顯示現有移轉集清單及其目前狀態。


1. 填入 **建立移轉集** 螢幕，如下所述。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt04.png)

   1. **名稱**：輸入移轉集名稱。
      >[!NOTE]
      >移轉集名稱不允許使用特殊字元。

   1. **Cloud Service 設定**：輸入目標 AEM as a Cloud Service 製作 URL。

      >[!NOTE]
      >在內容轉移活動期間，您一次最多可以建立並維護10個移轉集。
      >此外，您還須針對每個特定環境 (*預備*、*開發*&#x200B;或&#x200B;*生產*) 分別建立移轉。

   1. **存取 Token**：輸入存取 Token。

      >[!NOTE]
      >您可以使用 **開啟存取權杖** 按鈕。 您必須確定自己屬於目標Cloud Service例項中的「管理員」群組。

   1. **參數**：選取以下參數以建立移轉集：

      1. **包含版本**：視需要選取。包含版本時，路徑 `/var/audit` 會自動納入，以移轉稽核事件。

         ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >如果您打算將版本納入移轉集，且要以 `wipe=false`，則您必須停用版本清除，因為「內容轉移工具」中目前有限制。 如果您偏好保持已啟用版本清除功能，並在移轉集中執行追加，則您必須以 `wipe=true`.


      1. **欲包含的路徑**：使用路徑瀏覽器來選取需要移轉的路徑。路徑選擇器通過鍵入或選擇接受輸入。

         >[!IMPORTANT]
         >建立移轉集時會限制下列路徑：
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (部分 `/etc` 允許在CTT中選擇路徑)


1. 按一下 **儲存** 填入 **建立移轉集** 詳細資訊畫面。

1. 您可在 **內容轉移** 嚮導，如下圖所示。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   所有現有移轉集都會顯示在 **內容轉移** 嚮導及其當前狀態和狀態資訊。 您可能會看到以下說明的其中一些圖示。

   * *紅色雲朵*&#x200B;表示您無法完成提取程序。
   * A *綠雲* 表示您可以完成提取程式。
   * *黃色圖示*&#x200B;表示您並未建立現有移轉集，且該特定移轉集是由相同例項中的其他使用者所建立。

1. 選取移轉集，然後按一下 **屬性** 查看或編輯遷移集屬性。 編輯屬性時，無法變更 **移轉集名稱** 或 **服務URL**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)

### 確定遷移集大小和磁碟空間 {#migration-set-size}

建立移轉集後，強烈建議您先對移轉集執行大小檢查，再開始提取程式。
對移轉集執行大小檢查後，您將能：
* 確定 `crx-quickstart` 子目錄，以成功完成提取。
* 判斷移轉集大小是否符合支援的產品限制，並避免內容擷取失敗。

請依照下列步驟執行大小檢查：

1. 選取移轉集，然後按一下 **檢查大小**.

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image1.png)

1. 這會開啟 **檢查大小** 對話框。

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image2.png)

1. 按一下 **檢查大小** 來啟動程式。 接著，您會返回移轉集清單檢視，並看到訊息，指出 **檢查大小** 執行中。

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image3.png)


1. 一次 **檢查大小** 程式已完成，狀態將變更為 **已完成**. 選取相同的移轉集，然後按一下 **檢查大小** 來查看結果。

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image4.png)

   以下是 **檢查大小** 結果沒有警告。

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image5.png)

1. 若 **檢查大小** 結果表明磁碟空間不足和/或遷移集超出產品限制， **警告** 狀態。

![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)

以下是 **檢查大小** 結果顯示警告。

![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png)


## 下一步 {#whats-next}

學習如何建立移轉集後，您現在就可以了解「內容轉移工具」中的提取和擷取程式。 在了解這些流程之前，您必須先檢閱 [處理大型內容存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 大幅加快內容轉移活動的擷取和擷取階段，以便將內容移至AEMas a Cloud Service。
