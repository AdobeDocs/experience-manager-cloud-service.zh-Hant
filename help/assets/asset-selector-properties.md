---
title: 用於自訂的資產選擇器屬性
description: 在應用程式內使用資產選擇器搜尋、查找和檢索資產的中繼資料和轉譯。
role: Admin, User
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 37%

---

# 資產選擇器屬性 {#asset-selector-properties}

您可以使用資產選擇器屬性自訂資產選擇器的呈現方式。下表列出可用於自訂和使用資產選擇器的屬性。

| 屬性 | 類型 | 必要 | 預設 | 說明 |
|---|---|---|---|---|
| *rail* | 布林值 | 否 | 假 | 如果標籤為`true`，資產選擇器將會在左側邊欄檢視中轉譯。 如果資產選擇器標示為`false`，則會以模組檢視呈現。 |
| *imsOrg* | 字串 | 是 | | Adobe Identity Management System (IMS) ID 是在為您的組織佈建 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 時所指派的。`imsOrg`金鑰是驗證您所存取的組織是否位於Adobe IMS下的必要專案。 |
| *imsToken* | 字串 | 否 | | 用於身份驗證的 IMS 持有人語彙基元。如果您使用`imsToken`應用程式進行整合，則需要[!DNL Adobe]。 |
| *apiKey* | 字串 | 否 | | 用於存取 AEM Discovery 服務的 API 金鑰。如果您使用`apiKey`應用程式整合，則需要[!DNL Adobe]。 |
| *filterSchema* | 陣列 | 否 | | 用於設定篩選器屬性的模式。這可用於想要限制資產選擇器中的特定篩選器選項時。 |
| *filterForm Prop* | 物件 | 否 | | 指定用於調整搜尋所需的篩選器屬性。針對！ 例如，MIME型別JPG、PNG、GIF。 |
| *selectedAssets* | 陣列 `<Object>` | 否 |                 | 呈現資產選擇器時指定選取的資產。需要包含資產的 id 屬性的物件陣列。例如，在目前的目錄中必須可以使用 `[{id: 'urn:234}, {id: 'urn:555'}]` 資產。如果您需要使用不同的目錄，請為該 `path` 屬性提供一個值。 |
| *acvConfig* | 物件 | 否 | | 包含要覆寫預設值之自訂設定的物件的資產集合檢視屬性。 此外，此屬性會與`rail`屬性搭配使用，以啟用資產檢視器的邊欄檢視。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |                 | 如果OOTB轉譯不足以滿足您的應用程式需求，您可以公開介面，讓您透過`i18nSymbols` prop傳遞自己的自訂本地化值。 透過此介面傳遞值會覆寫所提供的預設翻譯，並改用您自己的翻譯。 若要執行覆寫，您必須傳遞一個有效的 [Message Descriptor](https://formatjs.io/docs/react-intl/api/#message-descriptor) 物件至您想要覆寫的 `i18nSymbols` 金鑰。 |
| *intl* | 物件 | 否 | | 資產選擇器提供預設的OOTB翻譯。 您可以透過 `intl.locale`prop 提供有效的語言環境字串，以選擇翻譯語言。例如：`intl={{ locale: "es-es" }}`</br></br>支援的語言環境字串遵循 [ISO 639 - 代碼](https://www.iso.org/iso-639-language-codes.html)來選擇代表語言標準名稱的代碼。</br></br>支援的語言環境清單：英文 - &#39;en-us&#39; (預設) 西班牙文 - &#39;es-es&#39; 德文 - &#39;de-de&#39; 法文 - &#39;fr-fr&#39; 義大利文 - &#39;it-it&#39; 日文 - &#39;ja-jp&#39;韓文 - &#39;ko-kr&#39; 葡萄牙文 - &#39;pt-br&#39; 中文 (繁體)- &#39;zh-cn&#39; 中文 (台灣) - &#39;zh-tw&#39; |
| *repositoryId* | 字串 | 否 | &#39;&#39; | 資產選擇器從中載入內容的存放庫。 |
| *additionalAemSolutions* | `Array<string>` | 否 | [ ] | 它可讓您新增其他AEM存放庫的清單。 如果此屬性未提供任何資訊，則僅考慮媒體資料庫或 AEM Assets 存放庫。 |
| *hideTreeNav* | 布林值 | 否 |  | 指定顯示或隱藏資產樹導覽側邊欄。那僅用於模組視圖，因此，此屬性在邊欄視圖中沒有影響。 |
| *onDrop* | 函數 | 否 | | 「依序放置」功能可用來將資產拖曳並釋放至指定的放置區域。 它提供互動式使用者介面，可讓您順暢地移動和處理資產。 |
| *dropOptions* | `{allowList?: Object}` | 否 | | 使用 &#39;allowList&#39; 設定放置選項。 |
| *colorScheme* | 字串 | 否 | | 為資產選擇器設定主題 (`light`或者`dark`)。 |
| *主題* | 字串 | 否 | 預設 | 套用主題至`default`到`express`之間的資產選擇器應用程式。 它也支援`@react-spectrum/theme-express`。 |
| *handleSelection* | 函數 | 否 | | 在選取資產並按一下`Select`模組上的按鈕時，叫用資產項目陣列。此函數僅在模組視圖中叫用。對於邊欄視圖，請使用 `handleAssetSelection`或`onDrop` 函數。範例： <pre>handleSelection=（資產：資產[]）=> {...}</pre> 如需詳細資訊，請參閱[選取的資產](/help/assets/asset-selector-customization.md#selection-of-assets)。 |
| *handleAssetSelection* | 函數 | 否 | | 在選擇或取消選擇資產時，以項目陣列叫用。當您想要在使用者選擇資產時進行監聽，這是十分實用的功能。範例： <pre>handleSelection=（資產：資產[]）=> {...}</pre> 如需詳細資訊，請參閱[選取的資產](/help/assets/asset-selector-customization.md#selection-of-assets)。 |
| *onClose* | 函數 | 否 | | 在按下`Close`模組視圖中的按鈕時叫用。這只在`modal`視圖中呼叫，而在`rail`視圖中忽略。 |
| *onFilterSubmit* | 函數 | 否 | | 當使用者變更不同的篩選條件時，以篩選項目叫用。 |
| *selectionType* | 字串 | 否 | 單身 | 一次設定`single`或`multiple`資產選擇方式。 |
| *dragOptions.allowList* | 布林值 | 否 | | 屬性可用來允許或拒絕拖曳無法選取的資產。 請參閱[dragOptions屬性](/help/assets/asset-selector-customization.md#drag-options-property) |
| *aemTierType* | 字串 | 否 |  | 它可讓您選取是否要顯示傳送層級、作者層級或兩者的資產。 <br><br>語法： `aemTierType:[0]: "author" 1: "delivery"` <br><br>例如，如果同時使用`["author","delivery"]`，則存放庫切換器會顯示製作和傳遞的選項。 |
| *handleNavigateToAsset* | 函數 | 否 | | 這是一個Callback函式，可處理資產的選取專案。 |
| *noWrap* | 布林值 | 否 | | *noWrap*&#x200B;屬性有助於在側邊欄面板中轉譯「資產選取器」。 如果未提及此屬性，預設會轉譯&#x200B;*對話方塊檢視*。 |
| *dialogSize* | 小型、中型、大型、全熒幕或全熒幕接管 | 字串 | 選用 | 您可以使用指定的選項指定版面大小，以控制版面。 |
| *colorScheme* | 淺色或深色 | 否 | | 此屬性用於設定Asset Selector應用程式的主題。 您可以選擇淺色或深色主題。 |
| *filterRepoList* | 函數 | 否 |  | 您可以使用`filterRepoList`回呼函式來呼叫Experience Manager存放庫並傳回已篩選的存放庫清單。 |
| *expiryOptions* | 函數 | | | 您可以在下列兩個屬性之間使用： **getExpiryStatus**，它提供過期資產的狀態。 函式會根據您提供的資產到期日傳回`EXPIRED`、`EXPIRING_SOON`或`NOT_EXPIRED`。 請參閱[自訂過期的資產](/help/assets/asset-selector-customization.md#customize-expired-assets)。 此外，您可以使用&#x200B;**allowSelectionAndDrag**，函式值可以是`true`或`false`。 當值設定為`false`時，無法在畫布上選取或拖曳過期的資產。 |
| *showToast* | | 否 | | 它可讓「資產選擇器」顯示已過期資產的自訂快顯通知訊息。 |
| *uploadConfig* | 物件 | | | 此物件包含上傳的自訂設定。 請參閱[上傳組態](#asset-selector-customization.md#upload-config)以瞭解可用性。 |
| *metadataSchema* | 陣列 | 否 | | 此屬性巢狀於`uploadConfig`屬性之下。 新增您提供的欄位陣列，以從使用者收集中繼資料。 使用此屬性，您也可以使用自動指派給資產但使用者不可見的隱藏中繼資料。 |
| *onMetadataFormChange* | 回呼函式 | 否 | | 此屬性巢狀於`uploadConfig`屬性之下。 它包含`property`和`value`。 `Property`等於從值正在更新的&#x200B;*metadataSchema*&#x200B;傳遞之欄位的&#x200B;*mapToProperty*。 而提供`value`等於新值作為輸入。 |
| *targetUploadPath* | 字串 |  | `"/content/dam"` | 此屬性巢狀於`uploadConfig`屬性之下。 預設為資產存放庫根的檔案目標上傳路徑。 |
| *hideUploadButton* | 布林值 | | 假 | 這可確保內部上傳按鈕是否隱藏。 此屬性巢狀於`uploadConfig`屬性之下。 |
| *onUploadStart* | 函數 | 否 |  | 這是一個回呼函式，用來在Dropbox、OneDrive或本機之間傳遞上傳來源。 語法為`(uploadInfo: UploadInfo) => void`。 此屬性巢狀於`uploadConfig`屬性之下。 |
| *importSettings* | 函數 | | | 如此可支援從第三方來源匯入資產。 `sourceTypes`使用您要啟用的匯入來源陣列。 支援的來源為Onedrive和Dropbox。 語法為`{ sourceTypes?: ImportSourceType[]; apiKey?: string; }`。 此外，此屬性是巢狀位於`uploadConfig`屬性下。 |
| *onUploadComplete* | 函數 | 否 | | 這是一個回呼函式，用來傳遞成功、失敗或重複之間的檔案上傳狀態。 語法為`(uploadStats: UploadStats) => void`。 此外，此屬性是巢狀位於`uploadConfig`屬性下。 |
| *onFilesChange* | 函數 | 否 | | 此屬性巢狀於`uploadConfig`屬性之下。 這是一個回呼函式，用來顯示檔案變更時上傳的行為。 它會傳遞擱置上傳的新檔案陣列以及上傳的來源型別。 如果發生錯誤，Source型別可以是null。 語法為`(newFiles: File[], uploadType: UploadType) => void` |
| *uploadingPlaceholder* | 字串 | | | 這是預留位置影像，可在啟動資產上傳時取代中繼資料表單。 語法為`{ href: string; alt: string; }`，此外，此屬性是巢狀位於`uploadConfig`屬性下。 |
| *功能集* | 陣列 | 字串 | | `featureSet:[ ]`屬性是用來啟用或停用Asset Selector應用程式中的特定功能。 若要啟用元件或功能，您可以在陣列中傳遞字串值，或將陣列保留空白以停用該元件。  例如，您想在「資產選擇器」中啟用上傳功能，請使用語法`featureSet:[0:"upload"]`。 同樣地，您可以使用`featureSet:[0:"collections"]`在Asset Selector中啟用集合。 此外，使用`featureSet:[0:"detail-panel"]`可啟用資產的[詳細資料面板](overview-asset-selector.md#asset-details-and-metadata)。 若要同時使用這些功能，語法為`featureSet:["upload", "collections", "detail-panel"]`。 |

<!--
| *selectedRendition* | Object | | | This property allows users to define and control which renditions of an asset are displayed when the panel is accessed. This customization enhances user experience by filtering out unnecessary renditions and showcasing only the most relevant renditions. For example, `CopyUrlHref` allows you to use Dynamic Media renditions in your Asset Selector application (delivery URL). |
| *featureSet* | Array | String | | The `featureSet:[ ]` property is used to enable or disable a particular functionaly in the Asset Selector application. To enable the component or a feature, you can pass a string value in the array or leave the array empty to disable that component. For example, you want to enable upload functionality in the Asset Selector, use the syntax `featureSet:[0:"upload"]`. Similarly, you can use `featureSet:[0:"collections"]` to enable collections in the Asset Selector. Addidionally, use `featureSet:[0:"detail-panel"]` to enable [details panel](overview-asset-selector.md#asset-details-and-metadata) of an asset. Also, `featureSet:[0:"dm-renditions"]` to show Dynamic Media renditions of an asset.|
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->

>[!MORELIKETHIS]
>
>* [資產選擇器自訂](/help/assets/asset-selector-customization.md)
>* [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
>* [整合資產選擇器與具備 OpenAPI 功能的 Dynamic Media](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [整合Asset Selector與協力廠商應用程式](/help/assets/integrate-asset-selector-non-adobe-app.md)
