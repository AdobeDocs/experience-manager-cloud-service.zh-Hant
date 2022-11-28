---
title: 內容轉移工具快速入門
description: 內容轉移工具快速入門
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: 4c2a02bb7ea981f78e51afc6ee20a3a936dfd666
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 7%

---

# 內容轉移工具快速入門 {#getting-started-content-transfer-tool}


## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下載"
>abstract="您可以從軟體發佈入口網站下載「內容轉移工具」的ZIP檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。請務必下載最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="發行說明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution入口網站"

您可以從軟體發佈入口網站下載「內容轉移工具」的ZIP檔案。 您可以透過 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 在來源Adobe Experience Manager(AEM)例項上。 請務必下載最新版本。 如需最新版本的詳細資訊，請參閱 [發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載內容轉移工具。

## 源環境連接 {#source-environment-connectivity}

>[!NOTE]
>
>如果從Cloud Acceleration Manager中刪除了移轉集，也可能會發生連線錯誤。

源AEM實例可能在防火牆後運行，在防火牆中它只能訪問已添加到允許清單中的某些主機。 若要成功執行擷取，必須從執行AEM的執行個體存取下列端點：

* Azure blob儲存服務： `casstorageprod.blob.core.windows.net`
* 用戶映射IO終結點： `usermanagement.adobe.io`

>[!NOTE]
>如果提取因下列錯誤而失敗：&quot;javax.net.ssl.SSLHandshakeException:sun.security.validator.ValidatorException:PKIX路徑生成失敗：sun.security.provider.certpath.SunCertPathBuilderException:找不到到被請求目標的有效證書路徑」，則可通過導入相關CA證書來解決此問題。

### 啟用SSL記錄 {#enable-ssl-logging}

了解SSL/TLS連線問題有時可能會很困難。 若要疑難排解提取程式期間的連線問題，您可以依照下列步驟，透過來源AEM環境的「系統控制台」啟用SSL記錄：

1. 導覽至來源例項上的Adobe Experience Manager Web Console，方法是前往 **工具 — 操作 — Web控制台** 或直接傳至URL() *https://serveraddress:serverport/system/console/configMgr*
1. 搜尋 **內容轉移工具提取服務設定**
1. 使用鉛筆圖示按鈕來編輯其設定值
1. 啟用 **啟用SSL記錄以進行擷取** 設定，然後按 **儲存**:

   ![影像](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)


## 執行「內容轉移工具」  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="執行內容轉移工具"
>abstract="了解如何使用「內容轉移工具」將內容移轉至AEMas a Cloud Service（製作/發佈）。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 請參閱示範"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教學課程 — 使用內容轉移工具"

以下章節適用於新版「內容轉移工具」。 請詳閱本節，了解如何使用「內容轉移工具」將內容移轉至AEMas a Cloud Service:

### 提取設定階段 {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="提取設定階段"
>abstract="了解如何建立移轉集並複製提取金鑰。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教學課程 — 使用內容轉移工具"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" needs to be added here -->

1. 登入Cloud Acceleration Manager(CAM)，然後按一下您先前建立的CAM專案，以評估您是否已準備好移轉至AEMas a Cloud Service。 如果尚未建立CAM項目，請參閱在CAM中建立和管理項目。

1. 按一下 **內容轉移** 卡片。 這會帶您進入「移轉集清單」檢視。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. 按一下 **建立移轉集**.

   >[!NOTE]
   >
   >在Cloud Acceleration Manager中，每個專案最多可建立5個移轉集。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

1. 您現在應該會在清單檢視中看到您的移轉清單。 按一下三點符號(**...**)以開啟下拉式清單，然後按一下 **複製提取金鑰**. 在提取階段期間，您需要此金鑰。 複製此提取金鑰。

   >[!NOTE]
   >
   >提取索引鍵可讓您的來源AEM環境安全地連線至移轉集。 請謹慎處理此金鑰，就像使用密碼一樣，絕不要透過電子郵件等不安全的媒體共用。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### 填入移轉集 {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="填充遷移集"
>abstract="建立移轉集後，必須從來源例項填入需要移至AEMas a Cloud Service環境的內容。 若要這麼做，「內容轉移工具」必須安裝在來源例項上。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="擷取內容"

若要填入您在Cloud Acceleration Manager中建立的移轉集，您必須在來源Adobe Experience Manager(AEM)執行個體上安裝最新版的「內容轉移工具」。 請依照本節了解如何填入移轉集。

1. 在您的來源Adobe Experience Manager例項上安裝最新版「內容轉移工具」後，請前往 **操作 — 內容遷移**

1. 按一下 **建立移轉集**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. 將先前從CAM複製的提取金鑰貼入的提取金鑰輸入欄位 **建立移轉集** 表單。 執行此操作後，將自動填入遷移集名稱和Cloud Acceleration Manager(CAM)項目名稱欄位。 這些名稱應與CAM中的遷移集名稱和您建立的CAM項目名稱相匹配。 您現在可以新增內容路徑。 新增內容路徑後，您便能儲存移轉集。 您可以執行包含或排除版本的擷取。

   >[!NOTE]
   >
   >請確定提取金鑰有效且不接近有效期。 您可以在 **建立移轉集** 對話框。 如果您收到連線錯誤，請參閱 [源環境連接](#source-environment-connectivity) 以取得更多資訊。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. 接下來，選擇以下參數以建立遷移集：

   1. **包含版本**：視需要選取。包含版本時，路徑 `/var/audit` 會自動納入，以移轉稽核事件。

      ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

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

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click on **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### 確定遷移集大小 {#migration-set-size}

建立移轉集後，強烈建議您先對移轉集執行大小檢查，再開始提取程式。
對移轉集執行大小檢查後，您將能：
* 確定 `crx-quickstart` 子目錄，以成功完成提取。
* 判斷移轉集大小是否符合支援的產品限制，並避免內容擷取失敗。

請依照下列步驟執行大小檢查：

1. 選取移轉集，然後按一下 **檢查大小**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. 這會開啟 **檢查大小** 對話框。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. 按一下 **檢查大小** 來啟動程式。 接著，您會返回移轉集清單檢視，並看到訊息，指出 **檢查大小** 執行中。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. 一次 **檢查大小** 程式已完成，狀態將變更為 **已完成**. 選取相同的移轉集，然後按一下 **檢查大小** 來查看結果。 以下是 **檢查大小** 結果沒有警告。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. 若 **檢查大小** 結果表明磁碟空間不足和/或遷移集超出產品限制， **警告** 狀態。

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## 下一步 {#whats-next}

學習如何建立移轉集後，您現在就可以了解「內容轉移工具」中的提取和擷取程式。 在了解這些流程之前，您必須先檢閱 [處理大型內容存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 大幅加快內容轉移活動的擷取和擷取階段，以便將內容移至AEMas a Cloud Service。
