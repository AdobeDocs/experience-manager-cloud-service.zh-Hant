---
title: 限制Experience Manager中的資產傳遞
description: 瞭解如何限制 [!DNL Experience Manager]中的資產傳遞。
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# 限制對[!DNL Experience Manager]中資產的存取 {#restrict-access-to-assets}

Experience Manager中的中央資產控管可讓DAM管理員或品牌管理員管理對資產的存取。 他們可以透過在編寫端為已核准的資產設定角色來限制存取權，尤其是在AEM as a Cloud Service編寫執行個體上。

成功通過授權程式後，使用者[搜尋](search-assets-api.md)或使用[傳遞URL](deliver-assets-apis.md)即可取得受限制資產的存取權。

![已限制存取資產](/help/assets/assets/restricted-access.png)

## 使用IMS權杖的受限制傳遞 {#restrict-delivery-ims-token}

在Experience Manager中，透過IMS的受限制傳送涉及兩個關鍵階段：

* 製作
* 傳遞

### 製作 {#authoring}

您可以根據角色限制[!DNL Experience Manager]內資產的傳遞。 若要設定角色，請執行下列步驟：

1. 以DAM管理員身分前往[!DNL Experience Manager]。
1. 選取您需要為其設定角色的資產。
1. 導覽至&#x200B;**[!UICONTROL 屬性]** > **[!UICONTROL 進階]**，並確定[!UICONTROL 進階中繼資料]索引標籤中存在&#x200B;**[!UICONTROL 角色]**&#x200B;欄位。

   ![角色中繼資料](/help/assets/assets/roles_metadata.jpg)
如果該欄位無法使用，請使用以下步驟來新增該欄位：

   1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。
   1. 選取中繼資料結構描述，然後按一下&#x200B;**[!UICONTROL 編輯&#x200B;_(e)_]**。
   1. 從表單右側的&#x200B;**[!UICONTROL 建置表單]**&#x200B;區段新增一個&#x200B;**[!UICONTROL 多值文字]**&#x200B;欄位到表單的中繼資料區段。
   1. 按一下新新增的欄位，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;面板中執行下列更新：
      1. 將&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;變更為&#x200B;_角色_。
      1. 將&#x200B;**[!UICONTROL 對應更新至屬性]**&#x200B;至&#x200B;_。/jcr：content/metadata/dam：roles_。

1. 取得要新增至資產角色中繼資料的IMS群組。 若要擷取IMS群組，請執行以下步驟：
   1. 登入https://adminconsole.adobe.com/。
   1. 前往您個別的組織，並導覽至&#x200B;**[!UICONTROL 使用者群組]**。
   1. 選取您需要新增的&#x200B;**[!UICONTROL 使用者群組]**，並從URL擷取&#x200B;**[!UICONTROL orgID]**&#x200B;和&#x200B;**[!UICONTROL userGroupID]**，或使用您的組織識別碼，例如`{orgID}@AdobeOrg:{usergroupID}`。

1. 將群組識別碼新增至資產屬性的&#x200B;**[!UICONTROL 角色]**&#x200B;欄位。 <br>
在**[!UICONTROL 角色]**&#x200B;欄位中定義的群組ID是唯一可存取資產的使用者。 您也可以在&#x200B;**[!UICONTROL 角色]**&#x200B;欄位中新增IMS使用者端ID和IMS設定檔ID。 例如，`{orgId}@AdobeOrg:{profileId}`。

   >[!NOTE]
   >
   >對於新的Assets檢視，您只能將存取權授予檔案夾層級，並僅限群組而非個別使用者存取。 深入瞭解[在Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions)中管理許可權。

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### 使用開啟和關閉日期與時間限制資產傳遞 {#restrict-delivery-assets-date-time}

DAM作者也可以定義資產屬性中可用的啟動開啟或關閉時間，以限制資產的傳送。

如果您為資產的啟用定義準時，則會在定義的時間產生資產的傳遞URL。 在定義的時間之前，資產保持非使用中狀態。 同樣地，如果您為資產定義關閉時間，資產會在定義的時間停用，而資產的傳送URL會停止顯示資產。

執行以下步驟，設定資產的開啟和關閉時間：

1. 選取資產並按一下&#x200B;**[!UICONTROL 屬性]**。

1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;標籤的&#x200B;**[!UICONTROL 已排程（停用）啟動]**&#x200B;區段中，根據您的需求定義開啟時間或關閉時間。

同樣地，在Assets檢視中，您可以選取資產並按一下&#x200B;**[!UICONTROL 詳細資料]**&#x200B;以檢視資產屬性並定義開啟時間和關閉時間。

預設中繼資料表單中可使用該欄位。 如果您的資產不是根據預設中繼資料結構，並且開啟時間和關閉時間欄位在資產屬性中無法使用，請在「管理員」檢視中執行以下步驟：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。
1. 選取中繼資料結構描述，然後按一下&#x200B;**[!UICONTROL 編輯]**。
1. 從右側的&#x200B;**[!UICONTROL 建置表單]**&#x200B;區段新增一個&#x200B;**[!UICONTROL 日期]**&#x200B;欄位到表單的中繼資料區段。
1. 按一下新新增的欄位，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;面板中執行下列更新：
   1. 將&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;變更為&#x200B;**開啟時間**&#x200B;或&#x200B;**關閉時間**。
   1. 將&#x200B;**[!UICONTROL 對應更新至屬性]**&#x200B;至&#x200B;_。/jcr：content/onTime_ （針對&#x200B;**開啟時間**&#x200B;欄位和&#x200B;_）。/jcr：content/offTime_&#x200B;為&#x200B;**關閉時間**&#x200B;欄位。
1. 按一下「**[!UICONTROL 儲存]**」。

同樣地，針對Assets檢視，如果您的資產不是根據預設中繼資料結構，且資產屬性中沒有開啟時間和關閉時間欄位，請執行以下步驟：

1. 按一下&#x200B;**[!UICONTROL 設定]**&#x200B;區段中的&#x200B;**[!UICONTROL 中繼資料Forms]**。
1. 選取中繼資料表單並按一下&#x200B;**[!UICONTROL 編輯]**。
1. 從左窗格的&#x200B;**[!UICONTROL 元件]**&#x200B;區段新增一個&#x200B;**[!UICONTROL 日期]**&#x200B;欄位至表單。
1. 按一下新新增的欄位，並將&#x200B;**[!UICONTROL 標籤]**&#x200B;變更為&#x200B;**開啟時間**&#x200B;或&#x200B;**關閉時間**。
1. 將&#x200B;**[!UICONTROL 中繼資料屬性]**&#x200B;更新為&#x200B;_。/jcr：content/onTime_ （針對&#x200B;**開啟時間**&#x200B;欄位和&#x200B;_）。/jcr：content/offTime_&#x200B;為&#x200B;**關閉時間**&#x200B;欄位。
1. 按一下「**[!UICONTROL 儲存]**」。



### 受限制資產的傳遞 {#delivery-restricted-assets}

受限制資產的傳送取決於成功存取資產的授權。 如果請求是從AEM作者執行個體或資產選擇器傳送，則授權會以IMS權杖為基礎，或者，如果您Publish或預覽執行個體上設定了自訂身分識別服務提供者，授權會以特殊Cookie為基礎。

#### AEM作者或資產選擇器請求的傳送 {#delivery-aem-author-asset-selector}

若要在請求從AEM作者執行個體或資產選擇器傳送時啟用受限制資產的傳送，有效的IMS權杖至關重要。 請依照下列步驟執行：

1. [產生存取權杖](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)。
   * 登入您的AEM as a Cloud Service環境的開發主控台。

   * 瀏覽至&#x200B;**[!UICONTROL 環境]** > **[!UICONTROL 整合]** > **[!UICONTROL 本機權杖]** > **[!UICONTROL 取得本機開發權杖]** > **[!UICONTROL 複製accessToken值]**。 深入瞭解[如何存取Token及相關層面](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. 將取得的存取權杖整合至&#x200B;**[!UICONTROL 授權]**&#x200B;標頭，確保其值會加上前置詞&#x200B;**[!UICONTROL 持有者]**。

1. 透過起始請求來驗證存取權杖的功能。 如果沒有IMS存取權杖，或提供的存取權杖缺少與資產中繼資料中新增的主體或群組，應該會產生404錯誤。

#### Publish例項上自訂身分提供者的傳送 {#delivery-custom-identity-provider}

若是您Publish或Preview執行個體上設定的自訂身分提供者，您可以提及在設定程式期間必須有權存取`groupMembership`屬性內之安全資產的群組。 當您透過[SAML整合](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)登入自訂身分提供者時，會讀取`groupMembership`屬性並用來建構Cookie，這會在所有驗證請求中傳送，類似於AEM作者或資產選擇器請求時的IMS權杖。

當頁面上提供安全資產，且傳送URL收到轉譯資產的要求時，AEM會檢查Cookie或IMS權杖中存在的角色，並將其與資產編寫期間套用的`dam:roles property`配對。 如果有相符專案，則會顯示資產。

>[!NOTE]
>
> 在[支援票證中，提及使用案例中受限制的傳遞，以啟動具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities)。 Adobe工程將協助您進行必要的澄清，及/或設定受限傳遞的程式。
