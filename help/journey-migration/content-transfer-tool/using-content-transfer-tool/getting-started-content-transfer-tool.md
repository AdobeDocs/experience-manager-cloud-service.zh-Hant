---
title: 內容傳輸工具入門
description: 內容傳輸工具入門
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: 7bebdff5095786005d5c4c91b7b699d71f9813a7
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 7%

---

# 內容傳輸工具入門 {#getting-started-content-transfer-tool}


## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下載"
>abstract="內容傳輸工具可從軟體分發門戶下載為zip檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。確保下載最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="發行說明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="軟體分發門戶"

內容傳輸工具可從軟體分發門戶下載為zip檔案。 您可以通過 [包管理器](/help/implementing/developing/tools/package-manager.md) 源Adobe Experience Manager(AEM)實例。 確保下載最新版本。 有關最新版本的詳細資訊，請參閱 [發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html)。

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載內容轉移工具。

## 源環境連接 {#source-environment-connectivity}

>[!NOTE]
>
>如果從雲加速管理器中刪除了遷移集，則還可能出現連接錯誤。

源實AEM例可能在防火牆後運行，在防火牆中它只能訪問已添加到允許清單的某些主機。 為了成功運行抽取，需要從正在運行的實例訪問以下終結點AEM:

* 目標AEMas a Cloud Service環境： `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure Blob儲存服務： `*.blob.core.windows.net`
* 用戶映射IO終結點： `usermanagement.adobe.io`

要test到目標as a Cloud ServiceAEM環境的連接，請從源實例的shell中發出以下cURL命令(替換 `program_id`。 `environment_id`, `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>如果 `HTTP/2 200` 已接收，連接到AEMas a Cloud Service成功。

### 啟用SSL日誌記錄 {#enable-ssl-logging}

瞭解SSL/TLS連接問題有時會很困難。 要在提取過程中排除連接問題，您可以通過源環境的系統控制台啟用SSL日誌記錄，AEM具體步驟如下：

1. 轉到源實例上的Adobe Experience ManagerWeb控制台 **工具 — 操作 — Web控制台** 或直接到URL *https://serveraddress:serverport/system/console/configMgr*
1. 搜索 **內容傳輸工具抽取服務配置**
1. 使用鉛筆表徵圖按鈕編輯其配置值
1. 啟用 **啟用SSL日誌以進行提取** 設定，然後按 **保存**:

   ![影像](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)


## 執行「內容轉移工具」  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="運行內容傳輸工具"
>abstract="瞭解如何使用內容傳輸工具將內容遷移AEM到as a Cloud Service（作者/發佈）。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 請參閱演示"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教程 — 使用內容傳輸工具"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)
<!-- Need to remove the video -->

以下部分適用於新版本的內容傳輸工具。 按照本節介紹如何使用內容傳輸工具將內容遷移到AEMas a Cloud Service:

### 提取設定階段 {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="提取設定階段"
>abstract="瞭解如何建立遷移集並複製抽取密鑰。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教程 — 使用內容傳輸工具"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" needs to be added here -->

1. 登錄到雲加速管理器(CAM)，然後按一下您以前建立的CAM項目，以評估您是否準備好移至AEMas a Cloud Service。 如果尚未建立CAM項目，請參閱在CAM中建立和管理項目。

1. 按一下 **內容傳輸** 卡。 這將帶您進入「遷移集清單」視圖。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. 通過按一下 **建立遷移集**。

   >[!NOTE]
   >
   >在雲加速管理器中，每個項目最多可建立五個遷移集。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

1. 現在，您應該在清單視圖中看到遷移清單。 按一下三點符號(**...**)以開啟下拉菜單，然後按一下 **複製提取鍵**。 在提取階段，您需要此密鑰。 複製此抽取密鑰。

   >[!NOTE]
   >
   >抽取密鑰使源環境AEM能夠安全地連接到遷移集。 請像使用密碼一樣小心地對待此密鑰，並且不要通過電子郵件等不安全的介質共用它。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### 填充遷移集 {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="填充遷移集&quot; abstract=&quot;建立遷移集後，需要將源實例中需要移動到as a Cloud Service環境的內容填充遷AEM移集。 為此，需要在源實例上安裝內容傳輸工具。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="提取內容"

要填充在雲加速管理器中建立的遷移集，您需要在源Adobe Experience Manager(AEM)實例上安裝最新版本的內容傳輸工具。 請按照本部分瞭解如何填充遷移集。

1. 在源Adobe Experience Manager實例上安裝最新版本(v2.0.10)的內容傳輸工具後，請轉到 **操作 — 內容遷移**

1. 按一下 **建立遷移集**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. 將先前從CAM複製的提取鍵貼上到的「提取鍵」輸入欄位 **建立遷移集** 的雙曲餘切值。 執行此操作後，將自動填充遷移集名稱和雲加速管理器(CAM)項目名稱欄位。 這些名稱應與CAM中的「遷移集」名稱和您建立的CAM項目名稱相匹配。 現在可以添加內容路徑。 添加內容路徑後，您將能夠保存遷移集。 您可以在包含或排除的版本中運行抽取。

   >[!NOTE]
   >
   >確保提取密鑰有效且未接近其到期。 您可以在 **建立遷移集** 對話框。 如果出現連接錯誤，請參閱 [源環境連接](#source-environment-connectivity) 的子菜單。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. 接下來，選擇以下參數以建立遷移集：

   1. **包含版本**：視需要選取。包含版本時，路徑 `/var/audit` 自動包含以遷移審核事件。

      ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >如果您打算將版本作為遷移集的一部分包括，並且正在執行 `wipe=false`，則由於內容傳輸工具中的當前限制，您必須禁用版本清除。 如果您希望啟用版本清除功能，並在遷移集中執行頂置操作，則必須將接收操作執行為 `wipe=true`。


   1. **欲包含的路徑**：使用路徑瀏覽器來選取需要移轉的路徑。路徑選取器通過鍵入或選擇接受輸入。

      >[!IMPORTANT]
      >建立移轉集時會限制下列路徑：
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` （部分） `/etc` 允許在CTT中選擇路徑)


1. 按一下 **保存** 填充了 **建立遷移集** 詳細資訊螢幕。

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click on **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### 確定遷移集大小 {#migration-set-size}

建立遷移集後，強烈建議在啟動抽取進程之前對遷移集運行大小檢查。
通過對遷移集運行大小檢查，您將能夠：
* 確定磁碟空間是否足夠 `crx-quickstart` 子目錄以成功完成提取。
* 確定遷移集大小是否在支援的產品限制範圍內，並避免內容攝取失敗。

按照以下步驟運行大小檢查：

1. 選擇遷移集並按一下 **檢查大小**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. 這將開啟 **檢查大小** 對話框。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. 按一下 **檢查大小** 以啟動進程。 然後，您將返回到遷移集清單視圖，您應看到一條消息，指出 **檢查大小** 正在運行。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. 一次 **檢查大小** 進程已完成，狀態將更改為 **已完成**。 選擇同一遷移集，然後按一下 **檢查大小** 的子菜單。 下面是 **檢查大小** 結果沒有警告。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. 如果 **檢查大小** 結果表明磁碟空間不足和/或遷移集超出產品限制， **警告** 將顯示狀態。

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## 下一步 {#whats-next}

學會了如何建立遷移集後，您現在就可以學習內容傳輸工具中的提取和接收過程。 在瞭解這些流程之前，必須先查看 [處理大型內容儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 顯著加快內容傳輸活動的提取和攝取階段，以將內容移動到AEMas a Cloud Service。
