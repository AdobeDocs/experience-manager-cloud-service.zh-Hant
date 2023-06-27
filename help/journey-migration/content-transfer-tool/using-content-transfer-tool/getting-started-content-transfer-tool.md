---
title: 內容轉移工具快速入門
description: 內容轉移工具快速入門
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: ea5d86e1a43bb7ae0c7608fc0625983cf2bf273f
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 21%

---

# 內容轉移工具快速入門 {#getting-started-content-transfer-tool}


## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下載"
>abstract="內容轉移工具可以從 Software Distribution 入口網站下載其 zip 檔。您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。確保下載最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="發行說明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution 入口網站"

內容轉移工具可以從 Software Distribution 入口網站下載其 zip 檔。您可以透過以下方式安裝套件 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 在您的來源Adobe Experience Manager (AEM)例項上。 確保下載最新版本。有關最新版本的詳細資訊，請參閱 [發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

僅支援2.0.0版及更高版本，建議使用最新版本。

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載內容轉移工具。

## 來源環境連線能力 {#source-environment-connectivity}

>[!NOTE]
>
>如果從Cloud Acceleration Manager中刪除移轉集，也可能會發生連線錯誤。

來源AEM執行個體可能在防火牆後面執行，而防火牆只能連線至已新增至允許清單的特定主機。 若要成功執行擷取，需要從執行AEM的執行個體存取以下端點：

* Azure Blob儲存服務： `casstorageprod.blob.core.windows.net`

>[!NOTE]
>如果擷取因下列錯誤而失敗：「javax.net.ssl.SSLHandshakeException： sun.security.validator.ValidatorException： PKIX路徑建置失敗： sun.security.provider.certpath.SunCertPathBuilderException：找不到請求目標的有效憑證路徑」，則可匯入相關的CA憑證來解決此問題。

### 啟用SSL記錄 {#enable-ssl-logging}

瞭解SSL/TLS連線問題有時很困難。 若要疑難排解擷取程式期間的連線問題，您可以透過來源AEM環境的「系統主控台」啟用SSL記錄，步驟如下：

1. 導覽至來源執行個體上的Adobe Experience Manager Web Console，方法是前往 **工具 — 作業 — Web主控台** 或直接前往URL，網址為 *https://serveraddress:serverport/system/console/configMgr*
1. 搜尋 **內容轉移工具提取服務設定**
1. 使用鉛筆圖示按鈕來編輯其設定值
1. 啟用 **為擷取啟用SSL記錄** 設定，然後按 **儲存**：

   ![影像](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>此標幟僅適用於偵錯SSL問題。 在執行擷取之前，請確定旗標已停用，因為它可能需要大量的磁碟空間。 這可能會填滿磁碟機容量，導致擷取程式失敗。

## 執行「內容轉移工具」  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="執行內容轉移工具"
>abstract="了解如何使用內容轉移工具將內容移轉到 AEM as a Cloud Service (製作/發佈)。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 觀看示範"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=zh-Hant#migration" text="教學課程 - 使用內容轉移工具"

下一節適用於新版的「內容轉移工具」。 請詳閱本節，瞭解如何使用「內容轉移工具」將內容移轉至AEMas a Cloud Service：

### 提取設定階段 {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="提取設定階段"
>abstract="了解如何建立和管理移轉集以及如何複製提取金鑰。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=zh-Hant#migration" text="教學課程 - 使用內容轉移工具"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" needs to be added here -->

1. 登入Cloud Acceleration Manager (CAM)，然後按一下您先前建立的CAM專案，以評估您移至AEMas a Cloud Service的準備程度。 如果尚未建立CAM專案，請參閱在CAM中建立和管理專案。

1. 按一下 **內容轉移** 卡片。 這會將您帶到移轉集清單檢視。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. 按一下「 」以建立移轉集 **建立移轉集**.

   >[!NOTE]
   >
   >在Cloud Acceleration Manager中，每個專案最多可以建立5個移轉集，包括過期的集。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   下列對話方塊隨即顯示。 請注意，移轉集將在長時間不活動後過期。 在專案卡片和移轉工作表格列上顯示警告一段時間後，移轉集將過期，其資料將不再可用。 檢閱 [移轉集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 以取得詳細資訊。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >名稱必須遵循與AEM節點相同的慣例，因此不能包含以下任何字元： . / ： [ ] | *

1. 您現在應該會在清單檢視中看到移轉清單。 按一下三點符號(**...**)以開啟下拉式清單，然後按一下 **複製擷取金鑰**. 在擷取階段期間，您將需要此金鑰。 複製此擷取金鑰。

   >[!NOTE]
   >
   >擷取金鑰可讓您的來源AEM環境安全地連線至移轉集。 請謹慎處理此金鑰，就像對待密碼一樣，切勿透過不安全的媒體（例如電子郵件）共用此金鑰。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### 填入移轉集 {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="填入移轉集"
>abstract="建立移轉集後，需要填入來源執行個體中的內容，這些內容需要移至 AEM as a Cloud Service 環境。為此，內容轉移工具需要安裝在來源執行個體上。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=zh-Hant" text="提取內容"

若要填入您在Cloud Acceleration Manager中建立的移轉集，您必須在來源Adobe Experience Manager (AEM)執行個體上安裝最新版本的內容轉移工具。 請詳閱本節，瞭解如何填入移轉集。

1. 在來源Adobe Experience Manager執行個體上安裝最新版的內容轉移工具後，請前往 **作業 — 內容移轉**

1. 按一下 **建立移轉集**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. 將先前從CAM複製的擷取金鑰貼到的「擷取金鑰」輸入欄位 **建立移轉集** 表單。 執行此操作後，會自動填入移轉集名稱和Cloud Acceleration Manager (CAM)專案名稱欄位。 這些名稱應與CAM中的「移轉集」名稱及您建立的CAM專案名稱相符。 您現在可以新增內容路徑。 新增內容路徑後，請儲存移轉集。 您可以包含或排除的版本來執行擷取。

   >[!NOTE]
   >
   >請確定擷取金鑰有效，且未接近其到期日。 您可在以下連結中取得此資訊： **建立移轉集** 對話方塊。 如果出現連線錯誤，請參閱 [來源環境連線能力](#source-environment-connectivity) 以取得詳細資訊。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. 接著，選取下列引數以建立移轉集：

   1. **包含版本**：視需要選取。包含版本時，路徑 `/var/audit` 自動包含以移轉稽核事件。

      ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >如果您打算將版本納入移轉集，並使用執行追加功能 `wipe=false`，則由於「內容轉移工具」的目前限制，您必須停用版本清除。 如果您偏好啟用版本整個清除，並且要在移轉集中執行追加作業，則必須依照以下方式執行內嵌 `wipe=true`.


   1. **欲包含的路徑**：使用路徑瀏覽器來選取需要移轉的路徑。路徑選擇器透過輸入或選取來接受輸入。

      >[!IMPORTANT]
      >建立移轉集時會限制下列路徑：
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (部分 `/etc` 允許在CTT中選取路徑)

1. 按一下 **儲存** 填入 **建立移轉集** 詳細資訊畫面。

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click on **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### 決定移轉集大小 {#migration-set-size}

建立移轉集後，強烈建議您在開始提取程式之前，對移轉集執行大小檢查。
透過對移轉集執行大小檢查，您可以：

* 判斷磁碟空間是否足夠 `crx-quickstart` 子目錄以成功完成擷取。
* 判斷移轉集大小是否在支援的產品限制內，並避免失敗的內容擷取。

請依照下列步驟執行大小檢查：

1. 選取移轉集並按一下 **檢查大小**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. 這將會開啟 **檢查大小** 對話方塊。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. 按一下 **檢查大小** 以啟動程式。 然後，您會返回移轉集清單檢視，且應該會看到一則訊息，指出 **檢查大小** 執行中。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. 晚於 **檢查大小** 程式已完成，狀態會變更為 **已完成**. 選取相同的移轉集，然後按一下 **檢查大小** 以檢視結果。 以下是 **檢查大小** 沒有警告的結果。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. 如果 **檢查大小** 結果指出磁碟空間不足，或移轉集超過產品限制，或兩者皆超過。 **警告** 狀態會顯示。

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## 下一步 {#whats-next}

瞭解如何建立移轉集後，您現在就可以開始瞭解內容轉移工具中的擷取和擷取程式了。 在瞭解這些程式之前，您必須先檢閱 [處理大型內容存放庫](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 以顯著加快內容轉移活動的擷取和擷取階段，將內容移至AEMas a Cloud Service。
