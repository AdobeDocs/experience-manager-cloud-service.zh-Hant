---
title: 使用使用者對應工具
description: 使用使用者對應工具
source-git-commit: 2f763f774b21b0c3b43d61964dda2d2ae596161a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---


# 使用使用者對應工具 {#using-user-mapping-tool}

使用者對應工具使用API，可透過電子郵件查詢AdobeIdentity Management系統(IMS)使用者並傳回其IMS ID。 此API需要使用者為其組織、用戶端密碼和存取或承載權杖建立用戶端ID。

## 設定使用者對應工具 {#setting-up-user-mapping}

請依照下列步驟設定此設定：

1. 使用您的Adobe ID導覽至[Adobe開發人員控制台](https://console.adobe.io)。
1. 建立新專案或開啟現有專案。
1. 新增API — 按一下「新增至專案」**並選取「** API **」**
1. 選擇「用戶管理API」。  您可能需要取得權限才能擁有此選項。
1. 建立JWT憑證。
1. 產生金鑰組或上傳公開金鑰（rsa不好）。  有一個按鈕&#x200B;**生成公用/專用密鑰對**，它將為您執行此操作。  請務必儲存公開金鑰和私密金鑰。
1. 導覽至「使用者管理API」。
1. 將您的私密金鑰內容貼入文字方塊，然後按一下「產生代號」**，以產生存取代號（或承載代號）。**
1. 保存所有這些資訊，如&#x200B;**客戶端ID**、**客戶機密碼**、**技術帳戶ID**、**技術帳戶電子郵件**、**組織ID**&#x200B;和&#x200B;**安全訪問令牌**。

## 訪問用戶映射工具的用戶介面 {#user-interface}

使用者對應工具已整合至內容轉移工具。 您可以從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載「內容轉移工具」。 如需最新版本的詳細資訊，請參閱[最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

1. 選取Adobe Experience Manager並導覽至工具 — > **操作** -> **內容移轉**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 按一下「**使用者對應**」卡片。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 按一下&#x200B;**建立用戶映射配置**。

   >[!NOTE]
   >如果您略過此步驟，則會在提取階段期間略過使用者和群組對應。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   請依照下文所述，填入&#x200B;**User Management API Configuration**&#x200B;中的欄位。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **組織ID**:輸入AdobeIdentity Management系統(IMS)組織ID，了解使用者要移轉的組織。

      >[!NOTE]
      >若要取得組織ID，請登入[Admin Console](https://adminconsole.adobe.com/)，並選擇您的組織（位於右上角）（如果您屬於多個組織）。 組織ID會以`xx@AdobeOrg`等格式顯示在該頁面的URL中，其中xx是IMS組織ID。  或者，您也可以在您產生存取權杖的[Adobe開發人員控制台](https://console.adobe.io)頁面中找到組織ID。

   * **用戶端ID**:輸入從「設定」步驟中儲存的用戶端ID。

   * **存取權杖**:輸入您從「設定」步驟儲存的「存取Token」。

      >[!NOTE]
      >存取權杖每24小時過期一次，而需要建立新的權杖。 若要建立新代號，請返回[Adobe開發人員控制台](https://console.adobe.io)，選擇您的專案，按一下&#x200B;**使用者管理API**，然後將相同的私密金鑰貼入方塊中。

1. 填入欄位後，按一下&#x200B;**測試設定**&#x200B;以測試與使用者管理API服務的連線。 如果連接成功，則可以按一下&#x200B;**Save**&#x200B;以保存配置。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 保存配置後，選擇配置並按一下&#x200B;**啟動用戶映射**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. 完成用戶映射後，按一下&#x200B;**Results**&#x200B;以查看摘要。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >完成使用者對應後，您可以使用階層連結，導覽回「內容移轉」頁面。 「使用者對應」卡片會顯示狀態和時間戳記。 按一下&#x200B;**內容轉移**&#x200B;以建立移轉集以執行提取。 如需詳細資訊，請參閱[執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) 。
