---
title: 使用用戶映射工具
description: 使用用戶映射工具
translation-type: tm+mt
source-git-commit: 410b7900981596590fa80b286b40a965700f108e
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 1%

---


# 使用用戶映射工具{#user-mapping-tool}

## 概覽 {#overview}

在AEM的雲端服務轉型歷程中，您需要將使用者和群組從您現有的AEM系統移至AEM做為雲端服務。 這是由內容傳輸工具完成。

AEM雲端服務的重大變更，是完全整合使用Adobe ID來存取作者層。  這需要使用Adobe Admin Console來管理使用者和使用者群組。 使用者設定檔資訊會集中在Adobe Identity Management System(IMS)中，該系統可跨所有Adobe雲端應用程式提供單一登入。 如需詳細資訊，請參閱「身分識別管理」。 由於這項變更，現有的使用者和群組必須對應至其IMS ID，以避免在雲端服務作者實例上重複使用者和群組。

## 重要注意事項{#important-considerations}

有一些例外情況需要考慮。 將記錄下列特定案例，且不會映射相關的使用者或群組：

1. 如果用戶在其jcr節點的`profile/email`欄位中沒有電子郵件地址。

1. 如果在IMS系統上找不到使用之組織ID的指定電子郵件（或是由於其他原因無法擷取IMS ID）。

1. 如果使用者目前已停用，則會視為未停用的使用者。  它會以正常方式進行映射和移轉，並在雲端例項上仍會停用。

## 使用用戶映射工具{#using-user-mapping-tool}

使用者對應工具使用API，可讓它透過電子郵件查閱IMS使用者並傳回其IMS ID。 此API要求使用者為其組織建立用戶端ID、用戶端密碼和存取Token/Bearer Token。

請依照下列步驟設定：

1. 使用您的Adobe ID導覽至[Adobe Developer Console](https://console.adobe.io)。
1. 建立新專案或開啟現有專案
1. 新增API
1. 選擇使用者管理API
1. 建立JWT憑據
1. 產生金鑰對，或上傳公開金鑰（rsa不行）
1. 產生存取Token（或JWT Token或承載Token）。
1. 將所有這些資訊（用戶端ID、用戶端密碼、技術帳戶ID、技術帳戶電子郵件、組織ID、存取Token）儲存在安全的位置。

## 使用者介面{#user-interface}

使用者對應工具已整合至內容傳輸工具。 您可從Software Distribution Portal下載內容傳輸工具。 如需最新版本的詳細資訊，請參閱版本注意事項。

1. 選擇「選擇Adobe Experience Manager」，並導覽至「工具」->「操作」**->「內容傳輸」**。****
1. 按一下&#x200B;**建立用戶映射配置**。

   >[!NOTE]
   >如果您略過此步驟，在擷取階段中會略過使用者和群組對應。

   填入「使用者管理API設定」中的欄位，如下所述：

   * **組織ID**:輸入要移轉之使用者之組織的IMS組織ID。

      >[!NOTE]
      >若要取得組織ID，請登入[管理控制台](https://adminconsole.adobe.com/)，並選擇您的組織（位於右上角）（如果您屬於多個組織）。 組織ID將位於該頁面的URL中，格式如`xx@AdobeOrg`，其中xx是IMS組織ID。  或者，您也可以在產生存取Token的[Adobe Developer Console](https://console.adobe.io)頁面中找到組織ID。

   * **用戶端ID**:輸入從「設定」步驟中保存的客戶機ID

   * **存取Token**:輸入您從「設定」步驟儲存的存取Token

      >[!NOTE]
      >存取Token每24小時過期一次，需要建立新的Token。 若要建立新的Token，請返回[Adobe Developer Console](https://console.adobe.io)，選擇您的專案，按一下「使用者管理API」，然後將相同的私密金鑰貼入方塊中。

1. 輸入上述資訊後，按一下「儲存」。

1. 按一下「建立移轉集」並填入欄位，然後按一下「儲存」，以建立移轉集。 如需詳細資訊，請參閱執行內容傳輸工具。

   >[!NOTE]
   >切換開關，以包含IMS使用者和群組的對應使用者預設為開啟。 在此設定中，對此遷移集執行抽取時，用戶映射工具將作為抽取階段的一部分運行。 這是執行內容傳輸工具擷取階段的建議方式。 如果此切換關閉且／或未建立用戶映射配置，則在提取階段將跳過用戶和組映射。

1. 要運行提取階段，請參閱[運行內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool)。



