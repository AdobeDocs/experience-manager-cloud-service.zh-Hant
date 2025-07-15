---
title: 自訂資產選擇器應用程式
description: 使用函式來自訂應用程式內的資產選擇器。
role: Admin, User
exl-id: 0fd0a9f7-8c7a-4c21-9578-7c49409df609
source-git-commit: c2ced432f3f0bd393bf5e8e7485c0e973c451b7a
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 25%

---

# 資產選擇器自訂 {#asset-selector-customization}

Asset Selector可讓您根據偏好設定、需求或功能需求來自訂各種元件。 您可以自訂下列元件[微前端資產選擇器](#overview-asset-selector.md)：

* [自訂篩選器面板](#customize-filter-panel)
* [在強制回應檢視中自訂資訊](#customize-info-in-modal-view)
* [啟用或停用拖放模式](#enable-disable-drag-and-drop)
* [選擇Assets](#selection-of-assets)
* [自訂過期的資產](#customize-expired-assets)
* [關聯式引動篩選](#contextual-invocation-filter)
* [dragOptions屬性](#drag-options-property)

您必須在&#x200B;**index.html**&#x200B;檔案或應用程式實作中的類似檔案中定義先決條件，以定義存取[!DNL Experience Manager Assets]存放庫的驗證詳細資料。 完成後，您可以視需求新增程式碼片段。

## 自訂篩選器面板 {#customize-filter-panel}

您可以在`assetSelectorProps`物件中新增下列程式碼片段，以自訂篩選器面板：

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

## 在強制回應檢視中自訂資訊 {#customize-info-in-modal-view}

按一下![資訊圖示](assets/info-icon.svg)圖示，即可自訂資產的詳細資料檢視。 執行以下程式碼：

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path')
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

## 啟用或停用拖放模式 {#enable-disable-drag-and-drop}

將下列屬性新增至`assetSelectorProp`以啟用拖放模式。 若要停用拖放，請將`true`引數取代為`false`。

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

## 選擇Assets {#selection-of-assets}

選取的資產類型是一個物件陣列，包含使用 `handleSelection`、`handleAssetSelection` 和 `onDrop` 函數時的資產資訊。

執行以下步驟，設定選取單一或多個資產的選項：

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

**結構語法**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'https://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

下表說明選取之資產物件的一些重要屬性。

| 屬性 | 類型 | 說明 |
|---|---|---|
| *repo:repositoryId* | 字串 | 儲存資產之存放庫的唯一識別碼。 |
| *repo:id* | 字串 | 資產的唯一識別碼。 |
| *repo:assetClass* | 字串 | 資產的分類 (例如影像或影片、文件)。 |
| *repo:name* | 字串 | 資產的名稱，包括檔案副檔名。 |
| *repo:size* | 數字 | 資產的大小，以位元組計。 |
| *repo:path* | 字串 | 資產在存放庫中的位置。 |
| *repo:ancestors* | `Array<string>` | 存放庫中資產的上階項目陣列。 |
| *repo:state* | 字串 | 存放庫中資產的目前狀態（例如，作用中、已刪除等）。 |
| *repo:createdBy* | 字串 | 建立資產的使用者或系統。 |
| *repo:createDate* | 字串 | 建立資產的日期與時間。 |
| *repo:modifiedBy* | 字串 | 上次修改資產的使用者或系統。 |
| *repo:modifyDate* | 字串 | 上次修改資產的日期和時間。 |
| *dc:format* | 字串 | 資產的格式，例如檔案型別(例如JPEG、PNG等)。 |
| *tiff:imageWidth* | 數字 | 資產的寬度。 |
| *tiff:imageLength* | 數字 | 資產的高度。 |
| *computedMetadata* | `Record<string, any>` | 代表貯體的一個物件，可存放各種類型之所有資產中繼資料 (存放庫、應用程式或嵌入式中繼資料)。 |
| *_links* | `Record<string, any>` | 相關資產的超媒體連結。包括中繼資料和轉譯等資源的連結。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition>`* | `Array<Object>` | 包含有關資產轉譯資訊的物件陣列。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].href>`* | 字串 | 轉譯的 URI。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].type>`* | 字串 | 轉譯的 MIME 類型。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].repo:size>`* | 數字 | 轉譯的大小，以位元組計。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].width>`* | 數字 | 轉譯的寬度。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].height>`* | 數字 | 轉譯的高度。 |

### 使用物件結構處理資產選擇 {#handling-selection}

`handleSelection` 屬性用於處理資產選擇器中單個或多個資產選擇。下面的範例說明使用 `handleSelection` 的語法。

![handle-selection](assets/handling-selection.png)

### 停用選擇的Assets {#disable-selection}

「停用選取」可用來隱藏或停用資產或資料夾無法選取的功能。 它會隱藏卡片或資產中的「選取」核取方塊，使其無法選取。 若要使用此功能，您可以宣告要在陣列中停用的資產或資料夾位置。 例如，如果您要停用選取出現在第一個位置的資料夾，可以新增下列程式碼：
`disableSelection: [0]:folder`

您可以為陣列提供您想要停用的mime型別（例如影像、資料夾、檔案或其他mime型別，例如image/jpeg）清單。 您宣告的mime型別對應到資產的`data-card-type`和`data-card-mimetype`屬性。

此外，已停用選取範圍的Assets是可拖曳的。 若要停用特定資產型別的拖放，您可以使用`dragOptions.allowList`屬性。

停用選取的語法如下：

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> 若是資產，選取核取方塊會隱藏；若是資料夾，則資料夾無法選取，但提及資料夾的導覽仍會顯示。

<!--For a complete list of properties and detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

## 自訂過期的資產 {#customize-expired-assets}

資產選擇器可讓您控制已過期資產的使用方式。 您可以使用&#x200B;**即將到期**&#x200B;徽章來自訂已到期的資產，這可以協助您提前知道將在目前日期起30天內到期的資產。 此外，您也可以視需求自訂。 您也可以允許在畫布上選取過期的資產，反之亦然。 您可以使用某些程式碼片段，以各種方式自訂過期的資產：

<!--{
    getExpiryStatus: function, // to control Expired/Expiring soon badges of the asset
    allowSelectionAndDrag: boolean, // set true to allow the selection of expired assets on canvas, set false, otherwise.
}-->

```
expiryOptions: {
    getExpiryStatus: getExpiryStatus;
}
```

### 選取已過期的資產 {#selection-of-expired-asset}

您可以自訂已過期資產的使用方式，使其成為可選取或無法選取。 您可以自訂是否允許在「資產選擇器」畫布上拖放過期的資產。 若要這麼做，請使用下列引數，讓資產在畫布上無法選取：

```
expiryOptions:{
    allowSelectionAndDrop: false;
}
```
<!--
Additionally, To do this, navigate to **[!UICONTROL Disable default expiry behavior]** under the [!UICONTROL Controls] tab and set the boolean value to `true` or `false` as per the requirement. If `true` is selected, you can see the select box over the expired asset, otherwise it remains unselected. You can hover to the info icon of an asset to know the details of an expired asset. 

![Disable default expiry behavior](assets/disable-default-expiry-behavior.png)-->

### 設定過期資產的持續時間 {#set-duration-of-expired-asset}

下列程式碼片段可協助您為將在未來五天內到期的資產設定&#x200B;**即將到期**&#x200B;徽章： <!--The `expirationDate` property is used to set the expiration duration of an asset. Refer to the code snippet below:-->

```
/**
  const getExpiryStatus = async (asset) => {
  if (!asset.expirationDate) {
    return null;
  }
  const currentDate = new Date();
  const millisecondsInDay = 1000 * 60 * 60 * 24;
  const fiveDaysFromNow = new Date(value: currentDate.getTime() + 5 * millisecondsInDay);
  const expirationDate = new Date(asset.expirationDate);
  if (expirationDate.getTime() < currentDate.getTime()) {
    return 'EXPIRED';
  } else if (expirationDate.getTime() < fiveDaysFromNow.getTime()) {
    return 'EXPIRING_SOON';
  } else {
    return 'NOT_EXPIRED';
  }
};
```

<!--In the above code snippet, the `getExpiryStatus` function is used to show the **Expiring soon** badge that have expiration date stored in `customExpirationDate`. Additionally, it sets the expiration date of an asset to five days from the current date. The `millisecondsInDay` helps you set expiry of an asset by specifying the time range in milliseconds. You can replace milliseconds with hours directly or customize function as per the requirement. Whereas, the `getTime()` function returns the number of milliseconds for the mentioned date. See [properties](#asset-selector-properties) to know about `expirationDate` property.-->

請參閱以下範例，瞭解屬性如何運作以擷取目前的日期和時間：

```
const currentData = new Date();
currentData.getTime(),
```

傳回`1718779013959`，其格式為日期格式2024-06-19T06:36:53.959Z。

### 自訂已過期資產的快顯通知訊息 {#customize-toast-message}

`showToast`屬性是用來自訂您要在過期資產上顯示的快顯通知訊息。

語法：

```
{
    type: 'ERROR', 'NEUTRAL', 'INFO', 'SUCCESS',
    message: '<message to be shown>',
    timeout: optional,
}
```

預設逾時為500毫秒。 然而，您可以視需要加以修改。 此外，傳遞值`timeout: 0`會保持快顯通知開啟，直到您按一下交叉按鈕為止。

以下是當需要禁止選取資料夾並顯示對應訊息時顯示快顯通知訊息的範例：

```
const showToast = {
    type: 'ERROR',
    message: 'Folder cannot be selected',
    timeout: 5000,
}
```

使用下列程式碼片段，顯示使用過期資產的快顯通知訊息：

```
(args) => {
    const [selectedAssets, setSelectedAssets] = useState([]);
    const [showToast, setShowToast] = React.useState(false);
    const handleAssetSelection = (assets) => {
        let directorySelectedFlag = false;
        const temp = assets.filter((asset) => {
            if (asset['repo:assetClass'] === 'directory') {
                directorySelectedFlag = true;
                setShowToast(true);
            }
            return !(asset['repo:assetClass'] === 'directory');
        });
        if (!directorySelectedFlag) {
            setShowToast(false);
        }
        setSelectedAssets(temp);
    };
    return (
        <ASDialogWrapper
            {...args}
            showToast={showToast ? args.showToast : null}
            selectedAssets={selectedAssets}
            handleAssetSelection={handleAssetSelection}
        />
    );
}
```

## 關聯式引動篩選{#contextual-invocation-filter}

資產選擇器可讓您新增標籤選取器篩選器。 它支援標籤群組，此群組會將所有相關標籤結合至特定標籤群組。 此外，它可讓您選取與您正在尋找的資產對應的其他標籤。 此外，您也可以在大部分由您使用的內容叫用篩選下設定預設標籤群組，以便您隨時可以存取這些群組。

>
>
> * 您必須新增內容引動程式碼片段，才能在搜尋中啟用標籤篩選器。
> * 必須使用對應至標籤群組型別`(property=xcm:keywords.id=)`的名稱屬性。

語法：

```
const filterSchema=useMemo(() => {
    return: [
        {
            element: 'taggroup',
            name: 'property=xcm:keywords.id='
        },
    ];
}, []);
```

若要在篩選器面板中新增標籤群組，必須至少新增一個標籤群組作為預設值。 此外，使用以下程式碼片段，新增從標籤群組中預先選取的預設標籤。

```
export const WithAssetTags = (props) = {
const [selectedTags, setSelectedTags] = useState (
new Set(['orientation', 'color', 'facebook', 'experience-fragments:', 'dam', 'monochrome'])
const handleSelectTags = (selected) => {
setSelectedTags (new Set (selected)) ;
};
const filterSchema = useMemo ((); => {
    return {
        schema: [
            ｛
                fields: [
                    {
                    element: 'checkbox', 
                    name: 'property=xcm:keywords=', 
                    defaultValue: Array. from(selectedTags), 
                    options: assetTags, 
                    orientation: 'vertical',
                    },
                ],
    header: 'Asset Tags', 
    groupkey: 'AssetTagsGroup',
        ],
    },
｝；
}, [selectedTags]);
```

![標籤群組篩選器](assets/tag-group.gif)

## 在資產選擇器中上傳 {#upload-in-asset-selector}

您可以從您的本機檔案系統上傳檔案或資料夾至Asset Selector。 若要使用本機檔案系統上傳檔案，您通常需要使用Asset Selector微前端應用程式提供的上傳功能。 在資產選擇器中叫用上傳所需的`upload`各種程式碼片段包括：

* [基本上傳表單程式碼片段](#basic-upload)
* [上傳設定](#upload-config)
* [使用中繼資料上傳](#upload-with-metadata)
* [自訂上傳](#customized-upload)
* [使用第三方來源上傳](#upload-using-third-party-source)

### 基本上傳表單 {#basic-upload}

```
import { AllInOneUpload } from '@assets/upload';
import { TextField, ContextualHelp } from '@adobe/react-spectrum';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

export const UploadExample = () => {
    return (
        <>
            <TextField
                marginStart="size-200"
                width="size-6000"
                isDisabled={true}
                label="Target Upload Path"
                value={targetUploadPath}
                contextualHelp={
                    <ContextualHelp>
                        <Content>Use Storybook Controls panel to change the default upload location</Content>
                    </ContextualHelp>
                }
            />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
            />
        <>
    )
}
```

### 上傳設定 {#upload-config}

```
uploadConfig: {
        onUploadStart: action('onUploadStart'),
        onUploadComplete: action('onUploadComplete'),
        metadataSchema: [
            {
                mapToProperty: 'dam:assetStatus',
                value: 'approved',
                element: 'hidden',
            },
        ],
        ... more properties
     }, 
```

*其他屬性包括`metadataSchema`、`onMetadataFormChange`、`targetUploadPath`、`hideUploadButton`、`onUploadStart`、`importSettings`、`onUploadComplete`、`onFilesChange`、`uploadingPlaceholder`*。 如需詳細資訊，請參閱[資產選擇器屬性](#asset-selector-properties.md)。

### 使用中繼資料上傳 {#upload-with-metadata}

```
import { AllInOneUpload } from '@assets/upload';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

/**
 * see https://git.corp.adobe.com/CQ/assets-upload/blob/main/packages/@assets/upload/stories/data/SampleMetadataSchemas.ts
 * for full schema shape used in rendered example below
 */
const metadataSchema = [
    {
        mapToProperty: 'gmo:lineofBusiness',
        label: 'Line of Business',
        placeholder: 'Select one',
        required: true,
        element: 'dropdown',
        dropdownOptions: [
            {
                id: 'corporate',
                name: 'Corporate',
            },
            {
                id: 'digital-media-dme',
                name: 'Digital Media (DMe)',
            },
            {
                id: 'digital-experience-dx',
                name: 'Digital Experience (DX)',
            },
            {
                id: 'business-solutions',
                name: 'Business Solutions',
            },
        ],
    },
    // ... see link above for full schema
    {
        mapToProperty: 'dam:assetStatus',
        value: 'approved',
        // hidden metadata element, this metadata will be applied to the asset without rendering UI for user input
        element: 'hidden',
    },
];

const handleMetadataFormChange = (event: MetadataChangeEvent) => {
    const { property, value } = event;

    console.log({ property, value });
}

const UploadExampleWithMetadataForm = () => {
    return (
        <AllInOneUpload
            repositoryId={repoId}
            apiToken={apiToken}
            targetUploadPath={targetUploadPath}
            metadataSchema={sampleMetadataSchema}
            onMetadataFormChange={handleMetadataFormChange}
        />
    )
}
```

### 自訂上傳 {#customized-upload}

```
const MultipleAllInOneUploadExample = () => {
    const mfeRef = React.useRef<{ iframeRef: { current: HTMLIFrameElement } }>(null);

    return (
        <>
            <Button
                onPress={() => UploadCoordinator.initiateUpload(mfeRef.current?.iframeRef?.current)}
            >
                External Initiate Upload
            </Button>
            <AllInOneUpload
                {...otherProps}
                ref={mfeRef}
            />
        <>
    );
}
```

### 使用第三方來源上傳 {#upload-using-third-party-source}

```
import { useState, useRef } from 'react';
import { AllInOneUpload, UploadCoordinator } from '@assets/upload';
import { Button, Flex, Divider } from '@adobe/react-spectrum';
import { sampleMetadataSchema } from './SampleMetadataSchemas';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

const defaultFiles = [
    new File(['file-content'], 'Controlled File 1'),
    new File(['file-content-with-more'], 'Controlled File 2')
];

const ControlledUploadExample = () => {
    const [controlledFiles, setControlledFiles] = useState<File[]>(defaultFiles)
    const inputRef = React.useRef<HTMLInputElement>(null);

    const handleFileInputChange = useCallback((e: ChangeEvent<HTMLInputElement>) => {
        if (e.target.files) {
            setMyFiles([...e.target.files]);
        }
    }, []);

    return (
        <Flex height="100%" alignItems="center" direction="column">
            <Flex direction="row" alignItems="center" justifyContent="center">
                <Button
                    variant="accent"
                    onPress={() => UploadCoordinator.initiateUpload()}
                    isDisabled={files.length < 1}
                >
                    External Initiate Upload
                </Button>
                <Button
                    variant="secondary"
                    onPress={() => {
                        inputRef.current?.click();
                    }}
                >
                    External Browse files
                </Button>
            </Flex>
            <Divider size="M" marginTop="size-200" />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
                files={controlledFiles}
                onFilesChange={setControlledFiles}
                hideUploadButton={true}
                metadataSchema={sampleMetadataSchema}
            />
            <input
                ref={inputRef}
                type="file"
                style={{ display: 'none' }}
                onChange={handleFileInputChange}
                multiple={true}
            />
        </Flex>
    )
}
```

### dragOptions屬性 {#drag-options-property}

```
dragOptions: {
            allowList: {
                '*': true,          // allow all types to be dragged
                'folder': false,    // except those explicitly set to disallow
                'image/jpeg': false // or those with specific mimeTypes
            },
         }
```

>[!MORELIKETHIS]
>
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
>* [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
>* [整合資產選擇器與具備 OpenAPI 功能的 Dynamic Media](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
