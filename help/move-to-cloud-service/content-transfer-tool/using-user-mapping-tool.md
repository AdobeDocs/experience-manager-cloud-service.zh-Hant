---
title: 使用使用者對應工具
description: 使用使用者對應工具
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
source-git-commit: 44b46358528f768476a8ec73119957bba3880d76
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 2%

---

# 使用用戶映射工具{#user-mapping-tool}

## 概覽 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="使用者對應工具"
>abstract="「內容轉移工具」可協助您將使用者和群組從您現有的AEM系統移至AEM作為Cloud Service。 現有的使用者和群組必須對應至其IMS ID，以避免Cloud Service製作例項上出現重複的使用者和群組。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用使用者對應工具的重要考量"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="使用使用者對應工具"


在轉換至Adobe Experience Manager(AEM)作為Cloud Service的過程中，您需要將使用者和群組從您現有的AEM系統移至AEM作為Cloud Service。 這是由「內容轉移工具」完成。

AEM as aCloud Service的重大變更，是完整整合使用AdobeID來存取製作階層。  這需要使用[Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)來管理使用者和使用者群組。 AdobeIdentity Management系統(IMS)會集中提供使用者設定檔資訊，以針對所有Adobe雲端應用程式提供單一登入。 如需詳細資訊，請參閱[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)。 因為此變更，現有的使用者和群組必須對應至其IMS ID，以避免Cloud Service製作例項上出現重複的使用者和群組。

### 用戶映射工具{#user-mapping-tool}

「內容轉移工具」（不含「使用者對應」）將移轉與要移轉之內容相關聯的任何使用者和群組。  「使用者對應工具」是「內容轉移工具」的一部分，其唯一用途是修改使用者和群組，以便讓IMS(AEM作為Cloud Service使用的單一登入功能)正確識別。  完成這些修改後，「內容轉移工具」會照常移轉指定內容的使用者和群組。

## 重要注意事項{#important-considerations}

### 例外案例{#exceptional-cases}

將記錄下列特定案例：

1. 如果使用者的&#x200B;*jcr*&#x200B;節點的`profile/email`欄位中沒有電子郵件地址，則有關的使用者或群組將會移轉，但不會對應。

1. 如果在AdobeIdentity Management系統(IMS)系統上找不到所使用組織ID的指定電子郵件（或如果IMS ID因其他原因無法擷取），則相關的使用者或群組將會移轉，但不會對應。

1. 如果用戶當前已禁用，則會將其視為與未禁用相同。 它會照常對應和移轉，並在雲端例項上保持停用狀態。

1. 如果目標AEMCloud Service實例上存在與源AEM實例上的某個用戶具有相同用戶名(rep:principalName)的用戶，則不會遷移有關的用戶或組。

### 其他注意事項{#additional-considerations}

* 如果設定「在擷取&#x200B;**之前擦去雲端例項上的現有內容」 ，則Cloud Service例項上已轉移的使用者將會與整個現有存放庫一起刪除，並會建立新存放庫以將內容擷取至。**&#x200B;這也會重設所有設定，包括目標Cloud Service例項的權限，且新增至&#x200B;**administrators**&#x200B;群組的管理員使用者為true。 管理員使用者需要重新新增至&#x200B;**administrators**&#x200B;群組，才能擷取CTT的存取權杖。

* 建議您先從目標Cloud ServiceAEM例項移除任何現有使用者，再透過「使用者對應」執行CTT。 這是為了防止將使用者從來源AEM例項移轉至目標AEM例項之間發生任何衝突。 如果來源AEM例項和目標AEM例項上存在相同的使用者，擷取期間便會發生衝突。

* 執行內容追加時，如果自上次轉移後內容未變更而未轉移，則與該內容相關聯的使用者和群組也不會轉移，即使在此期間使用者和群組已變更亦然。 這是因為使用者和群組會與其相關聯的內容一起移轉。

* 在下列情況下擷取會失敗：

1. 如果目標AEMCloud Service例項的使用者具有不同的使用者名稱，但電子郵件地址與來源AEM例項上的其中一位使用者相同。

1. 如果來源AEM例項上有兩個使用者，其使用者名稱不同，但電子郵件地址相同。 AEM as aCloud Service不允許兩個使用者擁有相同的電子郵件地址。

## 使用用戶映射工具{#using-user-mapping-tool}

使用者對應工具使用API，可透過電子郵件查詢AdobeIdentity Management系統(IMS)使用者並傳回其IMS ID。 此API需要使用者為其組織、用戶端密碼和存取或承載權杖建立用戶端ID。

請依照下列步驟設定此設定：

1. 使用您的Adobe ID導覽至[Adobe開發人員控制台](https://console.adobe.io)。
1. 建立新專案或開啟現有專案。
1. 新增API。
1. 選擇「用戶管理API」。
1. 建立JWT憑證。
1. 產生金鑰組或上傳公開金鑰（rsa不好）。
1. 產生存取權杖（或JWT權杖或承載權杖）。
1. 保存所有這些資訊，如&#x200B;**客戶端ID**、**客戶機密碼**、**技術帳戶ID**、**技術帳戶電子郵件**、**組織ID**&#x200B;和&#x200B;**安全訪問令牌**。

## 使用者介面{#user-interface}

使用者對應工具已整合至內容轉移工具。 您可以從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載「內容轉移工具」。 如需最新版本的詳細資訊，請參閱[最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

1. 選擇 Adobe Experience Manager 並導覽至工具 -> **操作** -> **內容轉移**。
1. 按一下&#x200B;**建立用戶映射配置**。

   >[!NOTE]
   >如果您略過此步驟，則會在提取階段期間略過使用者和群組對應。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   依照下列說明填入「使用者管理API設定」中的欄位：

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **組織ID**:輸入AdobeIdentity Management系統(IMS)組織ID，了解使用者要移轉的組織。

      >[!NOTE]
      >若要取得組織ID，請登入[Admin Console](https://adminconsole.adobe.com/)，並選擇您的組織（位於右上角）（如果您屬於多個組織）。 組織ID會以`xx@AdobeOrg`等格式顯示在該頁面的URL中，其中xx是IMS組織ID。  或者，您也可以在您產生存取權杖的[Adobe開發人員控制台](https://console.adobe.io)頁面中找到組織ID。

   * **用戶端ID**:輸入從「設定」步驟中儲存的用戶端ID。

   * **存取權杖**:輸入您從「設定」步驟儲存的「存取Token」。

      >[!NOTE]
      >存取權杖每24小時過期一次，而需要建立新的權杖。 若要建立新代號，請返回[Adobe開發人員控制台](https://console.adobe.io)，選擇您的專案，按一下&#x200B;**使用者管理API**，然後將相同的私密金鑰貼入方塊中。

1. 輸入上述資訊後，按一下&#x200B;**Save**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. 按一下&#x200B;**建立移轉集**&#x200B;並填入欄位，然後按一下&#x200B;**儲存**，以建立移轉集。 如需詳細資訊，請參閱[執行內容轉移工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)。

   >[!NOTE]
   >將切換為包含來自IMS使用者和群組的對應使用者，預設為開啟。 透過此設定，當對此移轉集執行提取時，使用者對應工具將會在提取階段中執行。 這是執行內容轉移工具提取階段的建議方式。 如果此切換關閉，且/或未建立使用者對應設定，則在提取階段期間會略過使用者和群組對應。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. 若要執行提取階段，請參閱[執行內容轉移工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)。
