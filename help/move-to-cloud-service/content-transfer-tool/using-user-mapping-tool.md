---
title: 使用用戶映射工具
description: 使用用戶映射工具
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
translation-type: tm+mt
source-git-commit: 7bdf8f1e6d8ef1f37663434e7b14798aeb8883f4
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 3%

---

# 使用用戶映射工具{#user-mapping-tool}

## 概覽 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="使用者對應工具"
>abstract="內容傳輸工具可協助您將使用者和群組從現有系統移AEM動至AEMCloud Service。 現有的使用者和群組必須對應至其IMS ID，以避免在Cloud Service作者例項上出現重複的使用者和群組。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用用戶映射工具的重要注意事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="使用用戶映射工具"


在將使用者和群組從現有系統移AEM至Adobe Experience Manager()做為Cloud Service的過渡歷程中，您需要將使用者AEM和群組移AEM至Cloud Service。 這是由內容傳輸工具完成。

Cloud Service的主AEM要變更是完全整合使用AdobeID來存取作者層。  這需要使用[Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)來管理用戶和用戶組。 使用者設定檔資訊會集中在AdobeIdentity Management系統(IMS)中，可在所有Adobe雲端應用程式中提供單一登入。 有關詳細資訊，請參閱[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)。 由於這項變更，現有的使用者和群組必須對應至其IMS ID，以避免在Cloud Service作者例項上重複使用者和群組。

## 重要注意事項{#important-considerations}

### 例外案例{#exceptional-cases}

將記錄下列特定案例：

1. 如果用戶的&#x200B;*jcr*&#x200B;節點的`profile/email`欄位中沒有電子郵件地址，則將遷移該用戶或組，但不映射該用戶或組。

1. 如果在AdobeIdentity Management系統(IMS)系統上找不到使用之組織ID的指定電子郵件（或如果IMS ID因其他原因無法擷取），則會移轉相關的使用者或群組，但不會映射。

1. 如果用戶當前處於禁用狀態，則會將其視為未禁用狀態。 它會以正常方式進行映射和移轉，並在雲端例項上仍會停用。

1. 如果用戶與源實例上的一AEM個用戶名(rep:principalName)相同，則該用戶或AEM組將不遷移。

### 其他考量事項{#additional-considerations}

* 如果設定&#x200B;**在提取**&#x200B;之前擦除Cloud實例上的現有內容，則Cloud Service實例上已轉移的用戶將連同整個現有儲存庫一起刪除，並建立新儲存庫以將內容提取到中。 這也會重設所有設定，包括目標Cloud Service例項的權限，對於新增至&#x200B;**administrators**&#x200B;群組的管理員使用者而言，這是正確的。 管理員使用者必須重新新增至&#x200B;**administrators**&#x200B;群組，才能擷取CTT的存取Token。

* 建議您先從目標Cloud Service例項移除任何現AEM有使用者，再執行含使用者對應的CTT。 這是為了防止將用戶從源實例遷移到目標實AEM例之間發生任AEM何衝突。 如果源實例和目標實例上存在相同的用戶，則在提取過程中AEM將發生衝AEM突。

* 在執行內容頂層時，如果內容自上次傳輸後未變更而未傳送，則與該內容相關的使用者和群組也不會傳送，即使使用者和群組在同時已變更亦然。 這是因為使用者和群組會隨著與之關聯的內容一起移轉。

* 在以下情況下，擷取將會失敗：

1. 如果目標AEMCloud Service實例的用戶名不同，但電子郵件地址與源實例上的某個用戶AEM相同。

1. 如果源實例上有兩個用戶，但AEM用戶名不同，但電子郵件地址相同。 因AEM為Cloud Service不允許兩個使用者擁有相同的電子郵件地址。

## 使用用戶映射工具{#using-user-mapping-tool}

使用者對應工具使用API，可讓它透過電子郵件查詢AdobeIdentity Management系統(IMS)使用者並傳回其IMS ID。 此API要求使用者為其組織建立用戶端ID、用戶端密碼和存取權或承載權杖。

請依照下列步驟設定：

1. 使用您的Adobe ID導覽至「Adobe開發人員控制台」。[](https://console.adobe.io)
1. 建立新專案或開啟現有專案。
1. 新增API。
1. 選擇「使用者管理API」。
1. 建立JWT憑據。
1. 產生金鑰對，或上傳公開金鑰（rsa不行）。
1. 產生存取Token（或JWT Token或承載Token）。
1. 保存所有這些資訊，如&#x200B;**客戶機ID**、**客戶機密碼**、**技術帳戶ID**、**技術帳戶電子郵件**、**組織ID**&#x200B;和&#x200B;**訪問Token**&#x200B;安全無虞。

## 使用者介面{#user-interface}

使用者對應工具已整合至內容傳輸工具。 您可以從[軟體散發入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載內容傳輸工具。 有關最新版本的詳細資訊，請參閱[當前發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

1. 選擇 Adobe Experience Manager 並導覽至工具 -> **操作** -> **內容轉移**。
1. 按一下&#x200B;**建立用戶映射配置**。

   >[!NOTE]
   >如果您略過此步驟，在「擷取」階段中會略過使用者和群組對應。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   填入「使用者管理API設定」中的欄位，如下所述：

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **組織ID**:輸入要遷移用戶的組織的AdobeIdentity Management系統(IMS)組織ID。

      >[!NOTE]
      >若要取得組織ID，請登入[Admin Console](https://adminconsole.adobe.com/)，並選擇您的組織（位於右上角）（如果您屬於多個組織）。 組織ID將位於該頁面的URL中，格式如`xx@AdobeOrg`，其中xx是IMS組織ID。  或者，您也可以在[Adobe開發人員主控台](https://console.adobe.io)頁面中找到組織ID，您可在此頁面產生存取Token。

   * **用戶端ID**:輸入從「設定」步驟中保存的客戶機ID。

   * **存取Token**:輸入您從「設定」步驟儲存的存取Token。

      >[!NOTE]
      >存取Token每24小時過期一次，需要建立新的Token。 若要建立新的Token，請返回[Adobe開發人員主控台](https://console.adobe.io)，選擇您的專案，按一下&#x200B;**使用者管理API**，然後將相同的私密金鑰貼入方塊中。

1. 輸入上述資訊後，按一下「儲存」。****

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. 通過按一下&#x200B;**建立遷移集**&#x200B;並填充欄位，然後按一下&#x200B;**保存**&#x200B;來建立遷移集。 有關詳細資訊，請參閱[運行內容傳輸工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)。

   >[!NOTE]
   >切換開關，以包含IMS使用者和群組的對應使用者預設為開啟。 在此設定中，對此遷移集執行抽取時，用戶映射工具將作為抽取階段的一部分運行。 這是執行內容傳輸工具擷取階段的建議方式。 如果此切換關閉且／或未建立用戶映射配置，則在提取階段將跳過用戶和組映射。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. 要運行提取階段，請參閱[運行內容傳輸工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)。
