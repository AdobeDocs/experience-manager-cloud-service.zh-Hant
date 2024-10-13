---
title: 使用具有OpenAPI功能的Dynamic Media限制資產傳送
description: 瞭解如何使用OpenAPI功能限制資產傳送。
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: 6e9fa8301fba9cab1a185bf2d81917e45acfe3a3
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 2%

---

# 使用具有OpenAPI功能的Dynamic Media限制資產傳送 {#restrict-access-to-assets}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Experience Manager的中央資產控管可讓DAM管理員或品牌管理員透過Dynamic Media的OpenAPI功能管理可用資產的存取權。 他們可以透過在AEM as a Cloud Service作者服務上的資產上設定某些中繼資料，將已核准的資產（精確到個別資產）的傳送限製為所選的[AdobeIdentity Management系統(IMS)使用者或群組](https://helpx.adobe.com/in/enterprise/using/users.html#user-mgt-strategy)。

一旦透過OpenAPI的Dynamic Media限制資產，只有授權存取所述資產的（Adobe IMS已上線）使用者才會被授予存取權。 若要存取資產，使用者必須運用Dynamic Media的[搜尋](search-assets-api.md)和[傳遞](deliver-assets-apis.md)功能搭配OpenAPI。

![已限制存取資產](/help/assets/assets/restricted-access.png)

在Experience Manager Assets中，透過IMS的受限制傳送涉及兩個關鍵階段：

* 製作
* 傳遞

## 製作 {#authoring}

### 使用IMS持有人權杖的受限制傳遞 {#restrict-delivery-ims-token}

您可以根據IMS使用者和群組身分限制[!DNL Experience Manager]內資產的傳遞。

>[!NOTE]
>
> 此功能目前不是自助式。 若要限制IMS [使用者](https://helpx.adobe.com/in/enterprise/using/manage-directory-users.html)和[群組](https://helpx.adobe.com/in/enterprise/using/user-groups.html)的資產傳遞，請洽詢您的企業支援團隊，以取得如何從[Adobe Admin Console](https://adminconsole.adobe.com/)入口網站擷取限制存取所需的資訊，以及如何在AEM as a Cloud Service作者服務中設定存取許可權的相關指引。

### 使用開啟和關閉日期與時間限制資產傳遞 {#restrict-delivery-assets-date-time}

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



## 受限制資產的傳遞 {#delivery-restricted-assets}

受限制資產的傳送取決於成功存取資產的授權。 授權是透過[IMS持有人權杖](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/IMS/) (從[AEM Asset Selector](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)起始之要求的應用程式)或安全Cookie (如果您已在AEM Publish/預覽服務上設定自訂身分識別服務提供者，並已設定Cookie建立和包含在頁面上)進行。

### AEM作者或資產選擇器請求的傳送 {#delivery-aem-author-asset-selector}

若要在請求是從AEM作者服務或AEM資產選擇器傳送時啟用受限制資產的傳遞，有效的IMS持有人權杖至關重要。\
在AEM Cloud Service作者服務以及資產選擇器中，會自動產生IMS持有人權杖並在成功登入後用於請求。

>[!NOTE]
>
>若要進一步瞭解如何在AEM Asset Selector型整合上啟用IMS驗證，請聯絡企業支援

1. 對於非Asset Selector型體驗，AEM as a Cloud Service和具有OpenAPI功能的Dynamic Media目前支援伺服器端API整合，且可產生IMS持有人權杖。
   * 依照[這裡](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#the-server-to-server-flow)的指示，執行可透過[AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)擷取IMS持有人權杖的服務對伺服器API整合
   * 在有限的時間內，本機開發人員存取（不適用於生產使用案例）可以依照指示[這裡](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#developer-flow)產生在[AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)上驗證的使用者的短期IMS持有人權杖

1. 發出[Search](search-assets-api.md)和[Delivery](deliver-assets-apis.md) API要求時，將取得的IMS持有人權杖新增至HTTP要求的&#x200B;**[!UICONTROL Authorization]**&#x200B;標頭（請確定它的值有前置詞&#x200B;**[!UICONTROL 持有人權杖]**）。

1. 若要驗證存取限制，請起始傳送API要求，其中含或不含&#x200B;**[!UICONTROL Authorization]**&#x200B;標頭。
   * 若沒有IMS持有人權杖或提供的IMS持有人權杖不屬於已授與資產存取許可權的使用者（直接或透過群組成員資格），回應將會產生`404`錯誤狀態碼。
   * 如果IMS持有者權杖是被授予資產存取權的一或多個使用者群組，回應將會產生具有資產二進位內容的`200`成功狀態代碼。

### Publish服務上自訂身分提供者的傳送 {#delivery-custom-identity-provider}

AEM Sites、AEM Assets和Dynamic Media搭配OpenAPI授權可搭配使用，而限制的資產傳送可在透過AEM Publish或預覽服務傳送的網站上設定。
如果AEM Sites的Publish和預覽服務設定為使用[自訂身分提供者(IdP)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)，則在設定程式期間，`groupMembership`屬性中可包含必須擁有其中安全資產存取權的群組。\
當網站使用者登入自訂身分提供者並存取Publish/預覽服務上託管的網站時，會讀取`groupMembership`屬性，並在成功驗證後，在網站上建構並傳遞安全Cookie。 所有後續傳送網站內容給使用者代理程式的請求都會包含此secure-cookie。

當頁面上要求安全資產時，AEM Publish和預覽層級會從secure-cookie擷取授權資料並驗證存取權。 如果有相符專案，則會顯示資產。

>[!NOTE]
>
> 在[支援票證中，提及使用案例中受限制的傳遞，以啟動具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities)。 Adobe工程將協助您進行必要的澄清，及/或設定受限傳遞的程式。