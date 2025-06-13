---
title: 使用具有OpenAPI功能的Dynamic Media限制資產傳送
description: 瞭解如何使用OpenAPI功能限制資產傳送。
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: 5db419e674ceb3c861f53a19e7b852c89ebd3702
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 7%

---

# 使用具有OpenAPI功能的Dynamic Media限制資產傳送 {#restrict-access-to-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 與 Edge Delivery Services 整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>具有 OpenAPI 功能的 Dynamic Media 指南現已提供 PDF 格式。下載完整指南，並使用 Adobe Acrobat AI 助理來回答您的查詢問題。
>
>[!BADGE 具有 OpenAPI 功能的 Dynamic Media 指南 PDF]{type=Informative url="https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Manager中的中央資產控管可讓DAM管理員或品牌管理員透過Dynamic Media的OpenAPI功能管理可用資產的存取。 他們可以透過在其AEM as a Cloud Service作者服務上的資產上設定某些中繼資料，來限制將已核准資產（向下至個別資產）的傳送給所選的[Adobe Identity Management系統(IMS)使用者或群組](https://helpx.adobe.com/in/enterprise/using/users.html#user-mgt-strategy)。

在透過具有OpenAPI的Dynamic Media限制資產後，只有授權存取所述資產的（Adobe IMS已上線）使用者才會被授予存取權。 若要存取資產，使用者必須運用Dynamic Media的[搜尋](search-assets-api.md)和[傳遞](deliver-assets-apis.md)功能搭配OpenAPI。

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

受限制資產的傳送取決於成功存取資產的授權。 授權是透過[IMS持有人權杖](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/) (針對從[AEM Asset Selector](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)起始的請求而提出的應用程式)或安全Cookie (如果您已在AEM發佈/預覽服務上設定自訂身分識別服務提供者，並已設定Cookie建立和包含在頁面上)進行。

### AEM作者或資產選擇器請求的傳送 {#delivery-aem-author-asset-selector}

若要在請求是從AEM作者服務或AEM資產選擇器傳送時啟用受限制資產的傳送，有效的IMS持有人權杖至關重要。\
IMS持有人權杖會在AEM Cloud Service作者服務和Asset Selector上自動產生，並在成功登入後用於請求。

>[!NOTE]
>
>若要進一步瞭解如何在AEM Asset Selector型整合上啟用IMS驗證，請聯絡企業支援

1. 對於非Asset Selector型體驗，AEM as a Cloud Service和具有OpenAPI功能的Dynamic Media目前支援伺服器端API整合，且可產生IMS持有人權杖。
   * 依照[這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#the-server-to-server-flow)的指示，執行可透過[AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)擷取IMS持有人權杖的服務對伺服器API整合
   * 在有限的時間內，本機開發人員存取（不適用於生產使用案例）可以依照指示[這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#developer-flow)產生在[AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)上驗證的使用者的短期IMS持有人權杖

1. 發出[Search](search-assets-api.md)和[Delivery](deliver-assets-apis.md) API要求時，將取得的IMS持有人權杖新增至HTTP要求的&#x200B;**[!UICONTROL Authorization]**&#x200B;標頭（請確定它的值有前置詞&#x200B;**[!UICONTROL 持有人權杖]**）。

1. 若要驗證存取限制，請起始傳送API要求，其中含或不含&#x200B;**[!UICONTROL Authorization]**&#x200B;標頭。
   * 若沒有IMS持有人權杖或提供的IMS持有人權杖不屬於已授與資產存取許可權的使用者（直接或透過群組成員資格），回應將會產生`404`錯誤狀態碼。
   * 如果IMS持有者權杖是被授予資產存取權的一或多個使用者群組，回應將會產生具有資產二進位內容的`200`成功狀態代碼。

### 發佈服務上自訂身分提供者的傳遞 {#delivery-custom-identity-provider}

AEM Sites、AEM Assets和具有OpenAPI授權的Dynamic Media可搭配使用，允許在AEM Publish或Preview服務上託管的網站上設定受限制的資產傳送。 安全傳送流程會利用瀏覽器Cookie來建立使用者的存取權，而且必須具備發佈網域子網域所在傳送層的自訂網域，才能實作此使用案例。 如果AEM Sites的發佈和預覽服務設定為使用[自訂身分提供者(IdP)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)，則必須在發佈網域發佈使用者的驗證上設定名稱為`delivery-token`的封裝使用者群組成員資格的新Cookie。 傳遞層級會從secure-cookie擷取授權資料並驗證存取權。 如需詳細資訊，請記錄[企業支援票證](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities)。
