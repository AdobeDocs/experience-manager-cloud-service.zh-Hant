---
title: 內容傳輸工具入門
description: 內容傳輸工具入門
source-git-commit: 0951942690949c23a99da3494526c1c78e7bcf22
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 22%

---

# 內容傳輸工具入門 {#getting-started-content-transfer-tool}


## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下載"
>abstract="內容傳輸工具可從軟體分發門戶下載為zip檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。確保下載最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="發行說明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="軟體分發門戶"

內容傳輸工具可從軟體分發門戶下載為zip檔案。 您可以通過 [包管理器](/help/implementing/developing/tools/package-manager.md) 源Adobe Experience Manager(AEM)實例。 確保下載最新版本。 有關最新版本的詳細資訊，請參閱 [發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載內容轉移工具。

## 源環境連接 {#source-environment-connectivity}

源實AEM例可能在防火牆後運行，在防火牆中它只能訪問已添加到允許清單的某些主機。 為了成功運行抽取，需要從正在運行的實例訪問以下終結點AEM:

* 目標AEMas a Cloud Service環境： `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure Blob儲存服務： `*.blob.core.windows.net`
* 用戶映射IO終結點： `usermanagement.adobe.io`

要test到目標as a Cloud ServiceAEM環境的連接，請從源實例的shell中發出以下cURL命令(替換 `program_id`。 `environment_id`, `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>如果 `HTTP/2 200` 已接收，連接到AEMas a Cloud Service成功。

## 執行「內容轉移工具」  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="運行內容傳輸工具"
>abstract="瞭解如何使用內容傳輸工具將內容遷移AEM到as a Cloud Service（作者/發佈）。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 請參閱演示"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教程 — 使用內容傳輸工具"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


請依照以下章節了解如何使用「內容轉移工具」，將內容移轉至 AEM as a Cloud Service (製作/發佈)：

1. 選擇Adobe Experience Manager並導航至工具 — > **操作** -> **內容遷移**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. 選擇 **內容傳輸** 選項 **內容遷移** 的子菜單。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. 建立第一個遷移集時，將顯示以下控制台。 按一下&#x200B;**建立移轉集**&#x200B;以建立新的移轉集。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >如果您有現有遷移集，控制台將顯示現有遷移集的清單，其當前狀態為。


1. 填充中的欄位 **建立遷移集** 螢幕，如下所述。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt04.png)

   1. **名稱**：輸入移轉集名稱。
      >[!NOTE]
      >移轉集名稱不允許使用特殊字元。

   1. **Cloud Service 設定**：輸入目標 AEM as a Cloud Service 製作 URL。

      >[!NOTE]
      >在內容傳輸活動期間，您一次最多可以建立和維護十個遷移集。
      >此外，您還須針對每個特定環境 (*預備*、*開發*&#x200B;或&#x200B;*生產*) 分別建立移轉。

   1. **存取 Token**：輸入存取 Token。

      >[!NOTE]
      >可以使用 **開啟訪問令牌** 按鈕 您需要確保您屬於目標Cloud Service實例中的「管理員」組。

   1. **參數**：選取以下參數以建立移轉集：

      1. **包含版本**：視需要選取。包含版本時，路徑 `/var/audit` 自動包含以遷移審核事件。

         ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

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

1. 您將在 **內容傳輸** ，如下圖所示。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   所有現有遷移集都顯示在 **內容傳輸** 的子菜單。 您可能會看到下面介紹的一些表徵圖。

   * *紅色雲朵*&#x200B;表示您無法完成提取程序。
   * A *綠雲* 表示您可以完成提取過程。
   * *黃色圖示*&#x200B;表示您並未建立現有移轉集，且該特定移轉集是由相同例項中的其他使用者所建立。

1. 選擇遷移集並按一下 **屬性** 查看或編輯遷移集屬性。 編輯屬性時，無法更改 **遷移集名稱** 或 **服務URL**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)

### 確定遷移集大小和磁碟空間 {#migration-set-size}

建立遷移集後，強烈建議在啟動抽取進程之前對遷移集運行大小檢查。
通過對遷移集運行大小檢查，您將能夠：
* 確定磁碟空間是否足夠 `crx-quickstart` 子目錄以成功完成提取。
* 確定遷移集大小是否在支援的產品限制範圍內，並避免內容攝取失敗。

按照以下步驟運行大小檢查：

1. 選擇遷移集並按一下 **檢查大小**。

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image1.png)

1. 這將開啟 **檢查大小** 對話框。

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image2.png)

1. 按一下 **檢查大小** 以啟動進程。 然後，您將返回到遷移集清單視圖，您應看到一條消息，指出 **檢查大小** 正在運行。

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image3.png)


1. 一次 **檢查大小** 進程已完成，狀態將更改為 **已完成**。 選擇同一遷移集，然後按一下 **檢查大小** 的子菜單。

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image4.png)

   下面是 **檢查大小** 結果沒有警告。

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image5.png)

1. 如果 **檢查大小** 結果表明磁碟空間不足和/或遷移集超出產品限制， **警告** 將顯示狀態。

![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)

下面是 **檢查大小** 結果帶有警告。

![影像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png)


## 下一步是什麼 {#whats-next}

學會了如何建立遷移集後，您現在就可以學習內容傳輸工具中的提取和接收過程。 在瞭解這些流程之前，必須先查看 [處理大型內容儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 顯著加快內容傳輸活動的提取和攝取階段，以將內容移動到AEMas a Cloud Service。
