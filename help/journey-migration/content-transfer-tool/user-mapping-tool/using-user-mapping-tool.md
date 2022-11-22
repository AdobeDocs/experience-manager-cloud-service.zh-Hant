---
title: 使用使用者對應工具
description: 使用使用者對應工具
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
source-git-commit: 68ade018185892528854a9438953ee7eb4b90f27
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 3%

---

# 使用使用者對應工具 {#using-user-mapping-tool}

使用者對應工具使用API，可透過電子郵件查詢AdobeIdentity Management系統(IMS)使用者並傳回其IMS ID。 此API需要使用者為其組織、用戶端密碼和存取或承載權杖建立用戶端ID。

## 設定使用者對應工具 {#setting-up-user-mapping}

請依照下列步驟設定此設定：

1. 導覽至 [Adobe Developer Console](https://console.adobe.io) 使用您的Adobe ID。
1. 建立新專案或開啟現有專案。
1. 新增API — 按一下 **新增至專案** 選取 **API**
1. 選擇「用戶管理API」。  您必須擁有系統管理員權限才能使用此選項。
1. 建立JWT憑證。
1. 產生金鑰組或上傳公開金鑰（rsa不好）。  有個按鈕， **產生公開/私用金鑰組**，這會幫您完成。  請務必儲存公開金鑰和私密金鑰。
1. 導覽至「使用者管理API」。
1. 將您的私密金鑰內容貼入文字方塊，然後按一下，以產生存取權杖（或記號權杖） **產生代號**.
1. 儲存所有這些資訊，例如 **用戶端ID**, **用戶端密碼**, **技術帳戶ID**, **技術帳戶電子郵件**, **組織ID**，和 **存取權杖** 安全。

## 訪問用戶映射工具的用戶介面 {#user-interface}

使用者對應工具已整合至內容轉移工具。 您可以從下載「內容轉移工具」 [Software Distribution入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). 如需最新版本的詳細資訊，請參閱 [最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. 選取Adobe Experience Manager並導覽至工具 — > **操作** -> **內容移轉**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 按一下 **使用者對應** 卡片。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 按一下 **建立用戶映射配置**.

   >[!NOTE]
   >如果您略過此步驟，則會在提取階段期間略過使用者和群組對應。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   填入 **使用者管理API設定**，如下所述。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **組織ID**:輸入AdobeIdentity Management系統(IMS)組織ID，了解使用者要移轉的組織。

      >[!NOTE]
      >若要取得組織ID，請登入 [Admin Console](https://adminconsole.adobe.com/) 如果您屬於多個組織，請選擇您的組織（位於右上角）。 組織ID會以下列格式顯示於該頁面的URL中 `xx@AdobeOrg`，其中xx是IMS組織ID。  或者，您也可以在 [Adobe Developer Console](https://console.adobe.io) 產生存取權杖的頁面。

   * **用戶端ID**:輸入從「設定」步驟中儲存的用戶端ID。

   * **存取權杖**:輸入您從「設定」步驟儲存的「存取Token」。

      >[!NOTE]
      >存取權杖每24小時過期一次，而需要建立新的權杖。 若要建立新代號，請返回 [Adobe Developer Console](https://console.adobe.io)，選擇您的專案，按一下 **使用者管理API** 並將相同的私密金鑰貼到方塊中。

1. 填入欄位後，按一下 **測試配置** 來測試與使用者管理API服務的連線。 如果連線成功，您可以按一下 **儲存** 以儲存設定。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 儲存設定後，選取設定並按一下 **啟動用戶映射**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. 按一下 **開始** 從對話框啟動用戶映射進程。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   它會顯示 **狀態** as **執行中**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. 完成使用者對應後，按一下 **結果** 來查看摘要。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* 完成使用者對應後，您可以使用階層連結，導覽回「內容移轉」頁面。 「使用者對應」卡片會顯示狀態和時間戳記。 按一下 **內容轉移** 建立要運行提取的遷移集。 請參閱 [執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) 以取得更多詳細資訊。


### 繼續使用者對應程式 {#resume-user-mapping-process}

如果由於下列任一原因而停止了用戶映射進程：

* 所選用戶 **停止用戶映射**
* 存取權杖在處理期間過期，或
* 其他原因

   >[!NOTE]
   >進度會從程式停止的位置儲存。

請依照下列步驟繼續使用者對應程式：

1. 按一下 **檢視記錄** 查看用戶映射日誌以檢查保存的進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. 按一下 **啟動用戶映射** 按鈕，從其中斷的位置繼續。

   >[!NOTE]
   >重新啟動前，請確定存取權杖仍有效或已重新整理。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. 按一下 **開始** 從對話框繼續用戶映射進程。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   使用者對應程式完成後，您將檢視 **狀態** as **已完成** 特定配置。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
