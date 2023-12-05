---
title: 使用使用者對應工具（舊版）
description: 使用使用者對應工具（舊版）
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---

# 使用使用者對應工具（舊版） {#using-user-mapping-tool}

>[!INFO]
>
>本檔案是指該工具的已棄用版本。 如需最新版本的詳細資訊，請參閱 [使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

使用者對應工具使用API，可透過電子郵件查詢AdobeIdentity Management系統(IMS)使用者並傳回其IMS ID。 此API要求使用者為其組織建立使用者端ID、使用者端密碼以及存取或持有人權杖。

## 設定使用者對應工具 {#setting-up-user-mapping}

**先決條件：** 使用者對應要求對應到其IMS ID的每個使用者在其AEM和IMS中的設定檔中都有一個電子郵件地址。 即使使用者使用電子郵件地址作為使用者ID登入，除非該電子郵件地址也位於設定檔以及IMS中，否則對應無法用於該使用者。

請依照下列步驟進行此設定：

1. 瀏覽至 [Adobe Developer Console](https://developer.adobe.com/console/) 使用您的Adobe ID。
1. 建立專案或開啟現有專案。
1. 新增API — 按一下 **新增至專案** 並選取 **API**
1. 選擇使用者管理API。 您必須擁有系統管理員許可權才能使用此選項。
1. 建立JWT認證。
1. 產生金鑰組，或上傳公開金鑰（rsa沒有用）。 有個按鈕， **產生公用/私用金鑰組** 會為您建立此金鑰組。 請確定您同時儲存公開和私密金鑰。
1. 導覽至「使用者管理API」。
1. 將您的私密金鑰內容貼入文字方塊並按一下，以產生Access Token （或持有人權杖） **產生Token**.
1. 儲存以下所有資訊，例如 **使用者端ID**， **使用者端密碼**， **技術帳戶ID**， **技術帳戶電子郵件**， **組織ID**、和 **存取權杖** 安全無虞。

## 存取使用者對應工具的使用者介面 {#user-interface}

使用者對應工具已整合至內容轉移工具。 您可以從以下位置下載「內容轉移工具」 [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). 如需最新版本的詳細資訊，請參閱 [最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. 選取Adobe Experience Manager並導覽至「工具> 」 **作業** > **內容移轉**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 按一下 **使用者對應** 卡片。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 按一下 **建立使用者對應設定**.

   >[!NOTE]
   >如果您略過此步驟，在擷取階段會略過使用者和群組對應。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   填入中的欄位 **使用者管理API設定**，如下所述。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **組織ID**：輸入要移轉使用者之組織的Identity Management系統(IMS)組織IDAdobe。

     >[!NOTE]
     >若要取得組織ID，請登入 [Admin Console](https://adminconsole.adobe.com/) 如果您隸屬於多個組織，請選擇您的組織（位於右上角區域）。 組織ID位在該頁面的URL中，格式如下 `xx@AdobeOrg`，其中xx為IMS組織ID。 或者，您也可以在下列位置找到組織ID： [Adobe Developer Console](https://developer.adobe.com/console/) 產生「存取Token」的頁面。

   * **使用者端ID**：輸入您在設定步驟中儲存的使用者端ID。

   * **存取權杖**：輸入您從設定步驟儲存的存取Token。

     >[!NOTE]
     >存取Token每24小時過期一次，且必須建立新的Token。 若要建立Token，請返回 [Adobe Developer Console](https://developer.adobe.com/console/)，選擇您的專案，按一下 **使用者管理API**，並將相同的私密金鑰貼到方塊中。

1. 填入欄位後，按一下 **測試設定** 測試與使用者管理API服務的連線。 如果連線成功，您可以按一下 **儲存** 以儲存組態。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 儲存設定後，選取設定並按一下 **開始使用者對應**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. 按一下 **開始** 從對話方塊中啟動「使用者對應」程式。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   它顯示 **狀態** 作為 **執行中**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. 使用者對應完成後，按一下 **結果** 以檢視摘要。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >
   >* 使用者對應完成後，您可以使用階層連結導覽回「內容移轉」頁面。 「使用者對應」卡片會顯示狀態和時間戳記。 按一下 **內容轉移** 以便建立移轉集來執行擷取。 另請參閱 [執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) 以取得更多詳細資料。

### 繼續使用者對應程式 {#resume-user-mapping-process}

如果由於下列任何原因而停止使用者對應程式：

* 選項 **停止使用者對應** 已由使用者選取。
* 該存取Token在程式期間過期。
* 或是其他原因。

  >[!NOTE]
  >進度會從程式停止的位置儲存。

請依照下列步驟繼續使用者對應程式：

1. 按一下 **檢視記錄** 以檢閱使用者對應記錄，以便檢查儲存的進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. 按一下 **開始使用者對應** 按鈕以從中斷處繼續。

   >[!NOTE]
   >在重新啟動之前，請確定存取權杖仍然有效或已重新整理。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. 按一下 **開始** 從對話方塊中，以繼續使用者對應程式。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   在「使用者對應」程式完成後，您可以檢視 **狀態** 作為 **已完成** 特定設定的。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
