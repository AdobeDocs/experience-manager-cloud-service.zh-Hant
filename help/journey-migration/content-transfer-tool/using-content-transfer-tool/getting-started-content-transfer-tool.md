---
title: 內容轉移工具快速入門
description: 瞭解如何開始使用內容轉移工具
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
feature: Migration
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 14%

---


# 內容轉移工具快速入門 {#getting-started-content-transfer-tool}


## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下載"
>abstract="內容轉移工具可以從 Software Distribution 入口網站下載其 zip 檔。您可以透過封裝管理員在來源 Adobe Experience Manager (AEM) 執行個體上安裝套件。確保下載最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html" text="發行說明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution 入口網站"

內容轉移工具可以從 Software Distribution 入口網站下載其 zip 檔。您可以在來源Adobe Experience Manager (AEM)執行個體上透過[封裝管理員](/help/implementing/developing/tools/package-manager.md)安裝封裝。 請務必下載最新版本。 如需最新版本的詳細資訊，請參閱[發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html)。

僅支援2.0.0版及更新版本，建議您使用最新版本。

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載內容轉移工具。

## Source環境連線 {#source-environment-connectivity}

>[!NOTE]
>
>如果移轉集已從Cloud Acceleration Manager中刪除，也可能會發生連線錯誤。

來源AEM執行個體可能正在防火牆後面執行，而它只能連線至已新增至允許清單的特定主機。 若要成功執行擷取，下列端點必須可從執行AEM的執行個體存取：

* Azure Blob儲存服務： `casstorageprod.blob.core.windows.net`

>[!NOTE]
>如果擷取因下列錯誤而失敗：「javax.net.ssl.SSLHandshakeException： sun.security.validator.ValidatorException： PKIX路徑建置失敗： sun.security.provider.certpath.SunCertPathBuilderException：找不到請求目標的有效憑證路徑」，則可透過匯入相關的CA憑證來解決此問題。

### 啟用SSL記錄 {#enable-ssl-logging}

瞭解SSL/TLS連線問題有時很困難。 若要疑難排解擷取程式期間的連線問題，您可以透過來源AEM環境的「系統主控台」啟用SSL記錄，步驟如下：

1. 導覽至來源執行個體上的Adobe Experience Manager Web主控台，方法是前往&#x200B;**工具>作業> Web主控台**，或直接導覽至&#x200B;*https://serveraddress:serverport/system/console/configMgr*&#x200B;的URL
1. 搜尋&#x200B;**內容轉移工具擷取服務組態**
1. 使用鉛筆圖示按鈕來編輯其設定值
1. 啟用&#x200B;**啟用SSL記錄以供擷取**&#x200B;設定，然後按&#x200B;**儲存**：

   ![影像](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>
>此標幟僅用於偵錯SSL問題。 在執行擷取之前，請確定旗標已停用，因為它可能需要大量的磁碟空間。 這可能會填滿磁碟機容量，導致擷取程式失敗。

## 執行「內容轉移工具」  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="執行內容轉移工具"
>abstract="了解如何使用內容轉移工具將內容移轉到 AEM as a Cloud Service (製作/發佈)。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&learn=on" text=" 觀看示範"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="教學課程 - 使用內容轉移工具"

下一節適用於新版的「內容轉移工具」。 請詳閱本節，瞭解如何使用「內容轉移工具」將內容移轉至AEM as a Cloud Service：

### 提取設定階段 {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="提取設定階段"
>abstract="了解如何建立和管理移轉集以及如何複製提取金鑰。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="教學課程 - 使用內容轉移工具"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" must be added here -->

1. 登入Cloud Acceleration Manager (CAM)，然後按一下您先前建立的CAM專案，以評估您移至AEM as a Cloud Service的準備程度。 如果尚未建立CAM專案，請參閱在CAM中建立和管理專案。

1. 按一下&#x200B;**內容轉移**&#x200B;卡片以開啟移轉集清單檢視。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. 按一下&#x200B;**建立移轉集**&#x200B;以建立移轉集。

   >[!NOTE]
   >
   >在Cloud Acceleration Manager中，每個專案最多可以建立10個移轉集，包括過期的集。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   下列對話方塊隨即顯示。 請注意，移轉集將在長時間不活動後過期。 在專案卡片和移轉工作表格列顯示一段時間的警告後，移轉集將會到期，其資料將不再可用。 檢閱[移轉集到期日](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)以取得詳細資料。

   在建立移轉集期間，您可以挑選將儲存暫時移轉資料的地理區域。  建議您選擇最接近目標雲端環境的區域，以確保擷取期間的最佳效能。  在建立移轉集後無法變更區域；若要使用其他區域，您必須建立新的移轉集。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >名稱必須遵循與AEM節點相同的慣例，因此不能包含下列任何字元： `. / : [ ] | * < > ^ ? { } % # `或任何不尋常的符號或emoji。

1. 您現在應該會在清單檢視中看到移轉清單。 選取三點符號(**...**)以開啟下拉式清單，並選取&#x200B;**複製擷取金鑰**。 在提取階段您需要此金鑰。 複製此擷取金鑰。

   >[!NOTE]
   >
   >擷取金鑰可讓您的來源AEM環境安全地連線至移轉集。 請謹慎處理此金鑰，就像輸入密碼一樣，切勿透過不安全的媒體（例如電子郵件）共用密碼。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### 填入移轉集 {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="填入移轉集"
>abstract="建立移轉集後，需要填入來源執行個體中的內容，這些內容需要移至 AEM as a Cloud Service 環境。為此，內容轉移工具需要安裝在來源執行個體上。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="提取內容"

若要填入您在Cloud Acceleration Manager中建立的移轉集，請在來源Adobe Experience Manager (AEM)例項上安裝最新版的「內容轉移工具」 。 若要瞭解如何填入移轉集，請遵循本節。

1. 在您的來源Adobe Experience Manager執行個體上安裝最新版的內容轉移工具後，請移至&#x200B;**作業 — 內容移轉**

1. 按一下&#x200B;**建立移轉集**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. 將先前從CAM複製的擷取金鑰貼到&#x200B;**建立移轉集**&#x200B;表單的擷取金鑰輸入欄位。 執行此操作後，會自動填入移轉集名稱和Cloud Acceleration Manager (CAM)專案名稱欄位。 這些名稱應與CAM中的「移轉集」名稱及您建立的CAM專案名稱相符。 您現在可以新增內容路徑。 新增內容路徑後，請儲存移轉集。 您可以使用包含或排除的版本來執行擷取。

   >[!NOTE]
   >
   >請確定擷取金鑰有效且不在到期日附近。 貼上擷取金鑰後，您可以在&#x200B;**建立移轉集**&#x200B;對話方塊中取得此資訊。 如果發生連線錯誤，請參閱[Source環境連線](#source-environment-connectivity)以取得詳細資訊。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/createMigrationSet.png)

1. 接著，選取下列引數以建立移轉集：

   1. **包含版本**：視需要選取。 包含版本時，會自動包含路徑`/var/audit`以移轉稽核事件。

      ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/includeVersion.png)

      >[!NOTE]
      >如果您打算將版本納入移轉集，並使用`wipe=false`執行追加作業，則由於「內容轉移工具」目前的限制，您必須停用版本清除功能。 如果您偏好啟用版本清除，並且正在移轉集中執行追加作業，則必須以`wipe=true`身分執行內嵌。

      >[!NOTE]
      >從CTT版本(3.0.24)開始，「內容轉移工具」已加入新功能，以強化包含和排除路徑的程式。 以前，必須逐一選擇路徑，這既繁瑣又耗時。 現在，使用者可以直接從UI加入路徑，或根據其偏好上傳CSV檔案。  CSV檔案的每行必須有一個路徑，且不能使用逗號。

   1. **要包含的路徑**：使用路徑瀏覽器來選取需要移轉的路徑。 路徑選擇器透過輸入或選取來接受輸入。 使用者只能選取一個選項來包含路徑：從UI或上傳CSV檔案。
      >[!IMPORTANT]
      >建立移轉集時會限制下列路徑：
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` （在CTT中允許選取某些`/etc`路徑）

      ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/includeAndExcludePath.png)

      1. 只允許選擇路徑，而且必須至少有一個路徑。如果未選擇路徑，則會發生伺服器錯誤。

         ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ServerError.png)

      1. 使用&#x200B;**CSV上傳選項**&#x200B;時，CSV檔案必須包含有效的路徑。

         ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/validCsvUpload.png)

      1. 若要切換迴路徑選擇器，使用者必須重新整理頁面並重新開始。

      1. 如果在上傳的CSV中找到&#x200B;**個無效的路徑**，則會顯示個別的對話方塊。

         ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/invalidPathsInCsv.png)

      1. 使用者必須更正CSV檔案並再次上傳它，或重新整理UI以透過路徑選擇器選取路徑。

   1. **要排除的路徑**：新功能可讓使用者排除不想包含的特定路徑。 例如，如果包含區段中的路徑是/content/dam，使用者現在可以排除/content/dam/catalogs等路徑。

      ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/excludePathHighlighted.png)

1. 填入&#x200B;**建立移轉集**&#x200B;詳細資訊畫面中的所有欄位後，請按一下&#x200B;**儲存**。

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### 正在決定移轉集大小 {#migration-set-size}

建立移轉集後，強烈建議先對移轉集執行大小檢查，然後再開始提取程式。
透過對移轉集執行大小檢查，您可以：

* 判斷`crx-quickstart`子目錄是否有足夠的磁碟空間可以成功完成擷取。
* 判斷移轉集大小是否在支援的產品限制內，並避免失敗的內容擷取。

請依照下列步驟執行大小檢查：

1. 選取移轉集並按一下&#x200B;**檢查大小**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. 這會開啟&#x200B;**檢查大小**&#x200B;對話方塊。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/checkMigrationSetSize.png)

1. 按一下&#x200B;**檢查大小**&#x200B;以啟動程式。 然後，您將返回移轉集清單檢視，而且您應該會看到一則訊息，指出&#x200B;**檢查大小**&#x200B;正在執行。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. **檢查大小**&#x200B;程式完成後，狀態會變更為&#x200B;**已完成**。 選取相同的移轉集，然後按一下&#x200B;**檢查大小**&#x200B;以檢視結果。 以下是&#x200B;**檢查大小**&#x200B;結果無警告的範例。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/checkSizeAfterFinished.png)

1. 如果&#x200B;**檢查大小**&#x200B;結果指出磁碟空間不足，或移轉集超過產品限制，或兩者皆超過，則會顯示&#x200B;**警告**&#x200B;狀態。

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## 後續步驟 {#whats-next}

瞭解如何建立移轉集後，您現在就能開始瞭解內容轉移工具中的擷取和擷取程式。 在學習這些程式之前，您必須檢閱[處理大型內容存放庫](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)，以大幅加快內容轉移活動的擷取和擷取階段，將內容移至AEM as a Cloud Service。
