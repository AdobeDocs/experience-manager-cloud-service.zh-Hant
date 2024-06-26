---
title: 限制Experience Manager中的資產傳遞
description: 瞭解如何在中限制資產傳送 [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# 限制存取中的資產 [!DNL Experience Manager] {#restrict-access-to-assets}

Experience Manager中的中央資產控管可讓DAM管理員或品牌管理員管理對資產的存取。 他們可以透過在編寫端為已核准的資產設定角色來限制存取權，尤其是在AEM as a Cloud Service編寫執行個體上。

使用者 [搜尋](search-assets-api.md) 或利用 [傳遞URL](deliver-assets-apis.md) 成功通過授權程式後，即可獲得對受限制資產的存取權。

![限制存取資產](/help/assets/assets/restricted-access.png)

## 使用IMS權杖的受限制傳遞 {#restrict-delivery-ims-token}

在Experience Manager中，透過IMS的受限制傳送涉及兩個關鍵階段：

* 製作
* 傳遞

### 製作 {#authoring}

您可以限制以下範圍內的資產傳送： [!DNL Experience Manager] 根據角色而定。 若要設定角色，請執行下列步驟：

1. 前往 [!DNL Experience Manager] 作為DAM管理員。
1. 選取您需要為其設定角色的資產。
1. 瀏覽至 **[!UICONTROL 屬性]** > **[!UICONTROL 進階]**，並確保 **[!UICONTROL 角色]** 欄位存在於 [!UICONTROL 進階中繼資料] 標籤。

   ![角色中繼資料](/help/assets/assets/roles_metadata.jpg)
如果該欄位無法使用，請使用以下步驟來新增該欄位：

   1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構]**.
   1. 選取中繼資料結構，然後按一下 **[!UICONTROL 編輯 _(e)_]**.
   1. 新增 **[!UICONTROL 多值文字]** 欄位來自 **[!UICONTROL 建置表單]** 區段至表單中的中繼資料區段。
   1. 按一下新新增的欄位，然後在  **[!UICONTROL 設定]** 面板：
      1. 變更 **[!UICONTROL 欄位標籤]** 至 _角色_.
      1. 更新 **[!UICONTROL 對應至屬性]** 至 _./jcr：content/metadata/dam：roles_.

1. 取得要新增至資產角色中繼資料的IMS群組。 若要擷取IMS群組，請執行以下步驟：
   1. 登入https://adminconsole.adobe.com/。
   1. 前往您個別的組織，並導覽至 **[!UICONTROL 使用者群組]**.
   1. 選取 **[!UICONTROL 使用者群組]** 您需要新增並擷取 **[!UICONTROL orgid]** 和 **[!UICONTROL userGroupID]** 或使用您的組織ID，例如 `{orgID}@AdobeOrg:{usergroupID}`.

1. 將群組ID新增至 **[!UICONTROL 角色]** 資產屬性的欄位。 <br>
中定義的群組ID **[!UICONTROL 角色]** 欄位是唯一可存取資產的使用者。 您也可以新增IMS使用者端ID和IMS設定檔ID，於 **[!UICONTROL 角色]** 欄位。 例如，`{orgId}@AdobeOrg:{profileId}`。

   >[!NOTE]
   >
   >對於新的Assets檢視，您只能將存取權授予檔案夾層級，並僅限群組而非個別使用者存取。 進一步瞭解 [在Experience Manager Assets中管理許可權](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### 使用開啟和關閉日期與時間限制資產傳遞 {#restrict-delivery-assets-date-time}

DAM作者也可以定義資產屬性中可用的啟動開啟或關閉時間，以限制資產的傳送。

如果您為資產的啟用定義準時，則會在定義的時間產生資產的傳遞URL。 在定義的時間之前，資產保持非使用中狀態。 同樣地，如果您為資產定義關閉時間，資產會在定義的時間停用，而資產的傳送URL會停止顯示資產。

執行以下步驟，設定資產的開啟和關閉時間：

1. 選取資產並按一下 **[!UICONTROL 屬性]**.

1. 在 **[!UICONTROL 已排程（停用）啟動]** 的區段 **[!UICONTROL 基本]** 標籤，根據您的需求定義開啟時間或關閉時間。

同樣地，在Assets檢視中，您可以選取資產並按一下 **[!UICONTROL 詳細資料]** 以檢視資產屬性並定義開啟時間和關閉時間。

預設中繼資料表單中可使用該欄位。 如果您的資產不是根據預設中繼資料結構，並且開啟時間和關閉時間欄位在資產屬性中無法使用，請在「管理員」檢視中執行以下步驟：

1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構]**.
1. 選取中繼資料結構，然後按一下 **[!UICONTROL 編輯]**.
1. 新增 **[!UICONTROL 日期]** 欄位來自 **[!UICONTROL 建置表單]** 區段至表單中的中繼資料區段。
1. 按一下新新增的欄位，然後在  **[!UICONTROL 設定]** 面板：
   1. 變更 **[!UICONTROL 欄位標籤]** 至 **準時** 或 **關閉時間**.
   1. 更新 **[!UICONTROL 對應至屬性]** 至 _./jcr：content/onTime_ 的 **準時** 欄位和 _./jcr：content/offTime_ 的 **關閉時間** 欄位。
1. 按一下「**[!UICONTROL 儲存]**」。

同樣地，針對Assets檢視，如果您的資產不是根據預設中繼資料結構，且資產屬性中沒有開啟時間和關閉時間欄位，請執行以下步驟：

1. 按一下 **[!UICONTROL 中繼資料Forms]** 在 **[!UICONTROL 設定]** 區段。
1. 選取中繼資料表單，然後按一下 **[!UICONTROL 編輯]**.
1. 新增 **[!UICONTROL 日期]** 欄位來自 **[!UICONTROL 元件]** 區段新增至表單。
1. 按一下新新增的欄位並變更 **[!UICONTROL 標籤]** 至 **準時** 或 **關閉時間**.
1. 更新 **[!UICONTROL 中繼資料屬性]** 至 _./jcr：content/onTime_ 的 **準時** 欄位和 _./jcr：content/offTime_ 的 **關閉時間** 欄位。
1. 按一下「**[!UICONTROL 儲存]**」。



### 受限制資產的傳遞 {#delivery-restricted-assets}

受限制資產的傳送取決於成功存取資產的授權。 如果請求是從AEM作者執行個體或資產選擇器傳送，則授權會以IMS權杖為基礎，或者，如果您Publish或預覽執行個體上設定了自訂身分識別服務提供者，授權會以特殊Cookie為基礎。

#### AEM作者或資產選擇器請求的傳送 {#delivery-aem-author-asset-selector}

若要在請求從AEM作者執行個體或資產選擇器傳送時啟用受限制資產的傳送，有效的IMS權杖至關重要。 請依照下列步驟執行：

1. [產生存取權杖](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * 登入您的AEM as a Cloud Service環境的開發主控台。

   * 瀏覽至 **[!UICONTROL 環境]** > **[!UICONTROL 整合]** > **[!UICONTROL 本機Token]** > **[!UICONTROL 取得本機開發權杖]** > **[!UICONTROL 複製accessToken值]**. 進一步瞭解 [如何存取權杖及相關層面](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. 將取得的存取權杖整合至 **[!UICONTROL Authorization]** 標題，確定其值會加上前置詞 **[!UICONTROL 持有人]**.

1. 透過起始請求來驗證存取權杖的功能。 如果沒有IMS存取權杖，或提供的存取權杖缺少與資產中繼資料中新增的主體或群組，應該會產生404錯誤。

#### Publish例項上自訂身分提供者的傳送 {#delivery-custom-identity-provider}

如果您在Publish或預覽執行個體上設定了自訂身分提供者，您可以提及必須擁有中安全資產存取權的群組。 `groupMembership` 屬性。 當您透過登入自訂身分提供者 [SAML整合](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)，則 `groupMembership` 屬性會被讀取並用來建構Cookie，這會在所有驗證請求中傳送，類似於AEM作者或資產選擇器請求時的IMS權杖。

當頁面上提供安全資產，並向傳送URL提出轉譯資產請求時，AEM會檢查Cookie或IMS權杖中存在的角色，並將其與配對 `dam:roles property` 套用至資產製作期間。 如果有相符專案，則會顯示資產。

>[!NOTE]
>
> 在 [支援票證以透過OpenAPI功能啟用Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities)，在使用案例中提及受限制的傳遞。 Adobe工程將協助您進行必要的澄清，及/或設定受限傳遞的程式。
