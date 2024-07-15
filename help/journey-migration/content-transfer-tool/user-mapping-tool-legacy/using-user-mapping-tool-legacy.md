---
title: 使用使用者對應工具（舊版）
description: 使用使用者對應工具（舊版）
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---

# 使用使用者對應工具（舊版） {#using-user-mapping-tool}

>[!INFO]
>
>本檔案是指該工具的已棄用版本。 如需最新版本的詳細資訊，請參閱[使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md)。

使用者對應工具使用API，可透過電子郵件查詢AdobeIdentity Management系統(IMS)使用者並傳回其IMS ID。 此API要求使用者為其組織建立使用者端ID、使用者端密碼以及存取或持有人權杖。

## 設定使用者對應工具 {#setting-up-user-mapping}

**先決條件：**&#x200B;使用者對應要求每個要對應至其IMS ID的使用者，在其AEM和IMS的設定檔中都需有電子郵件地址。 即使使用者使用電子郵件地址作為使用者ID登入，除非該電子郵件地址也位於設定檔以及IMS中，否則對應無法用於該使用者。

請依照下列步驟進行此設定：

1. 使用您的Adobe ID導覽至[Adobe Developer Console](https://developer.adobe.com/console/)。
1. 建立專案或開啟現有專案。
1. 新增API — 按一下&#x200B;**新增至專案**&#x200B;並選取&#x200B;**API**
1. 選擇使用者管理API。 您必須擁有系統管理員許可權才能使用此選項。
1. 建立JWT認證。
1. 產生金鑰組，或上傳公開金鑰（rsa沒有用）。 有一個按鈕&#x200B;**產生公用/私用金鑰組**，會為您建立此金鑰組。 請確定您同時儲存公開和私密金鑰。
1. 導覽至「使用者管理API」。
1. 將您的私密金鑰內容貼入文字方塊並按一下&#x200B;**產生Token**，以產生Access Token （或持有人權杖）。
1. 儲存所有資訊，例如&#x200B;**使用者端識別碼**、**使用者端密碼**、**技術帳戶識別碼**、**技術帳戶電子郵件**、**組織ID**&#x200B;以及&#x200B;**安全存取權杖**。

## 存取使用者對應工具的使用者介面 {#user-interface}

使用者對應工具已整合至內容轉移工具。 您可以從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載內容轉移工具。 如需最新版本的詳細資訊，請參閱[最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

1. 選取Adobe Experience Manager並導覽至工具> **作業** > **內容移轉**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 按一下&#x200B;**使用者對應**&#x200B;卡片。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 按一下&#x200B;**建立使用者對應設定**。

   >[!NOTE]
   >如果您略過此步驟，在擷取階段會略過使用者和群組對應。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   請依照下列說明，填入&#x200B;**使用者管理API組態**&#x200B;中的欄位。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **組織ID**：輸入要移轉使用者之組織的AdobeIdentity Management System (IMS)組織ID。

     >[!NOTE]
     >若要取得組織ID，請登入[Admin Console](https://adminconsole.adobe.com/)，並選擇您的組織（在右上角區域） （如果您屬於多個組織）。 組織ID位於該頁面的URL中，格式如`xx@AdobeOrg`，其中xx是IMS組織ID。 或者，您可以在產生「存取Token」的[Adobe Developer Console](https://developer.adobe.com/console/)頁面中找到組織ID。

   * **使用者端識別碼**：輸入您從設定步驟中儲存的使用者端識別碼。

   * **存取Token**：輸入您從設定步驟中儲存的Access Token。

     >[!NOTE]
     >存取Token每24小時過期一次，且必須建立新的Token。 若要建立Token，請返回[Adobe Developer Console](https://developer.adobe.com/console/)，選擇您的專案，按一下&#x200B;**使用者管理API**，然後將相同的私密金鑰貼到方塊中。

1. 填入欄位後，按一下&#x200B;**測試組態**&#x200B;以測試使用者管理API服務的連線。 如果連線成功，您可以按一下[儲存]儲存組態。****

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 儲存組態之後，請選取組態並按一下&#x200B;**開始使用者對應**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. 從對話方塊按一下&#x200B;**開始**，以開始使用者對應程式。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   它將&#x200B;**狀態**&#x200B;顯示為&#x200B;**執行中**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. 使用者對應完成後，按一下&#x200B;**結果**&#x200B;以檢視摘要。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >
   >* 使用者對應完成後，您可以使用階層連結導覽回「內容移轉」頁面。 「使用者對應」卡片會顯示狀態和時間戳記。 按一下&#x200B;**內容轉移**，以便建立移轉集以執行擷取。 如需詳細資訊，請參閱[執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool)。

### 繼續使用者對應程式 {#resume-user-mapping-process}

如果由於下列任何原因而停止使用者對應程式：

* 使用者已選取&#x200B;**停止使用者對應**&#x200B;選項。
* 該存取Token在程式期間過期。
* 或是其他原因。

  >[!NOTE]
  >進度會從程式停止的位置儲存。

請依照下列步驟繼續使用者對應程式：

1. 按一下&#x200B;**檢視記錄**&#x200B;以檢閱使用者對應記錄，以便您檢視儲存的進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. 再次按一下&#x200B;**開始使用者對應**&#x200B;按鈕，從中斷的地方繼續。

   >[!NOTE]
   >在重新啟動之前，請確定存取權杖仍然有效或已重新整理。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. 從對話方塊按一下&#x200B;**開始**，以繼續使用者對應程式。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   使用者對應程式完成後，您可以檢視該特定組態的&#x200B;**狀態**&#x200B;為&#x200B;**已完成**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
