---
title: ' [!DNL Assets]的開發人員參考'
description: '[!DNL Assets] API和開發人員參考內容可讓您管理資產，包括二進位檔案、中繼資料、轉譯、註解和 [!DNL Content Fragments]。'
contentOwner: AG
feature: Assets HTTP API
role: Developer, Architect, Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager Assets]開發人員使用案例、API和參考資料 {#assets-cloud-service-apis}

文章包含[!DNL Assets]開發人員的建議、參考資料和資源，以[!DNL Cloud Service]形式提供。 其中包含新的資產上傳模組、API參考資料，以及有關後處理工作流程中所提供支援的資訊。

## [!DNL Experience Manager Assets] API與作業 {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service]提供數個API，以程式設計方式與數位資產互動。 每個API都支援特定使用案例，如下表所述。 [!DNL Assets]使用者介面、[!DNL Experience Manager]案頭應用程式和[!DNL Adobe Asset Link]支援所有或部分作業。

>[!CAUTION]
>
>有些API持續存在，但未主動支援(以×表示)。 請儘量不要使用這些API。

| 支援等級 | 說明 |
| ------------- | --------------------------- |
| ✓ | 支援 |
| × | 不支援。 請勿使用。 |
| - | 無法使用 |

| 使用案例 | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager / Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) Java API | [資產計算服務](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlet | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **原始二進位檔** |  |  |  |  |  |  |
| 建立原始檔案 | ✓ | × | - | × | × | - |
| 讀取原始檔案 | - | × | ✓ | ✓ | ✓ | - |
| 更新原始檔案 | ✓ | × | ✓ | × | × | - |
| 刪除原始檔案 | - | ✓ | - | ✓ | ✓ | - |
| 複製原始檔案 | - | ✓ | - | ✓ | ✓ | - |
| 移動原始檔案 | - | ✓ | - | ✓ | ✓ | - |
| **中繼資料** |  |  |  |  |  |  |
| 建立中繼資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 讀取中繼資料 | - | ✓ | - | ✓ | ✓ | - |
| 更新中繼資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 刪除中繼資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 複製中繼資料 | - | ✓ | - | ✓ | ✓ | - |
| 移動中繼資料 | - | ✓ | - | ✓ | ✓ | - |
| **內容片段(CF)** |  |  |  |  |  |  |
| 建立CF | - | ✓ | - | ✓ | - | - |
| 讀取CF | - | ✓ | - | ✓ | - | ✓ |
| 更新CF | - | ✓ | - | ✓ | - | - |
| 刪除CF | - | ✓ | - | ✓ | - | - |
| 複製CF | - | ✓ | - | ✓ | - | - |
| 移動CF | - | ✓ | - | ✓ | - | - |
| **版本** |  |  |  |  |  |  |
| 建立版本 | ✓ | ✓ | - | - | - | - |
| 讀取版本 | - | ✓ | - | - | - | - |
| 刪除版本 | - | ✓ | - | - | - | - |
| **資料夾** |  |  |  |  |  |  |
| 建立資料夾 | ✓ | ✓ | - | ✓ | - | - |
| 讀取資料夾 | - | ✓ | - | ✓ | - | - |
| 刪除資料夾 | ✓ | ✓ | - | ✓ | - | - |
| 複製資料夾 | ✓ | ✓ | - | ✓ | - | - |
| 行動資料夾 | ✓ | ✓ | - | ✓ | - | - |

## 資產上傳 {#asset-upload}

在[!DNL Experience Manager]中以[!DNL Cloud Service]身分，您可以使用HTTP API直接將資產上傳到雲端儲存空間。 上傳二進位檔案的步驟如下。 在外部應用程式中執行這些步驟，而不是在[!DNL Experience Manager] JVM中執行。

1. [提交HTTP要求](#initiate-upload)。 它會通知[!DNL Experience Manage]r部署您打算上傳新的二進位檔。
1. [將二進位檔](#upload-binary)的內容PUT至起始要求提供的一或多個URI。
1. [提交HTTP要求](#complete-upload)，通知伺服器已成功上傳二進位檔的內容。

![直接二進位上傳通訊協定概觀](assets/add-assets-technical.png)

>[!IMPORTANT]
>
>在外部應用程式中而不是在[!DNL Experience Manager] JVM中執行上述步驟。

方法提供可擴充且效能更高的資產上傳處理方式。 與[!DNL Experience Manager] 6.5的差異如下：

* 二進位檔不會通過[!DNL Experience Manager]，現在只是協調上傳程式與為部署設定的二進位雲端儲存空間。
* 二進位雲端儲存空間可與內容傳遞網路(CDN)或Edge網路搭配使用。 CDN會選取較接近使用者端的上傳端點。 當資料傳輸至附近端點的距離較短時，上傳效能和使用者體驗會改善，尤其是對於分散各地的團隊。

>[!NOTE]
>
>檢視使用者端代碼，以在開放原始碼[aem-upload程式庫](https://github.com/adobe/aem-upload)中實作此方法。
>
>[!IMPORTANT]
>
>在某些情況下，由於Cloud Service中的儲存最終具有一致的性質，變更可能不會在對Experience Manager的請求之間完全傳播。 這會導致404個起始或完成上傳呼叫的回應，因為必要的資料夾建立未傳播。 使用者端應該會收到404個回應，並透過實作附有後退策略的重試來處理這些回應。

### 啟動上傳 {#initiate-upload}

將HTTP POST請求提交至所需的資料夾。 在此資料夾中建立或更新Assets。 包含選擇器`.initiateUpload.json`，以表示要求將啟動二進位檔案的上傳。 例如，應建立資產的資料夾路徑為`/assets/folder`。 POST要求是`POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`。

要求內文的內容型別應為`application/x-www-form-urlencoded`表單資料，包含下列欄位：

* `(string) fileName`：必要。 資產在[!DNL Experience Manager]中顯示的名稱。
* `(number) fileSize`：必要。 上傳資產的檔案大小（位元組）。

只要每個二進位檔案都包含必要欄位，就可以使用單一要求來起始多個二進位檔案的上傳。 如果成功，請求會以下列格式回應`201`狀態代碼和包含JSON資料的內文：

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` （字串）：當二進位檔完成上傳時，呼叫此URI。 URI可以是絕對URI或相對URI，使用者端應該能夠處理任一個。 也就是說，值可以是`"https://[aem_server]:[port]/content/dam.completeUpload.json"`或`"/content/dam.completeUpload.json"`請參閱[完成上傳](#complete-upload)。
* `folderPath` （字串）：上傳二進位檔的資料夾完整路徑。
* `(files)` （陣列）：元素清單，其長度和順序符合起始要求中提供的二進位資訊清單長度和順序。
* `fileName` （字串）：起始要求中提供的對應二進位檔名稱。 此值應包含在完整請求中。
* `mimeType` （字串）：起始要求中提供的對應二進位檔的mime型別。 此值應包含在完整請求中。
* `uploadToken` （字串）：對應二進位檔的上傳權杖。 此值應包含在完整請求中。
* `uploadURIs` （陣列）：字串清單，其值是二進位內容應上傳到的完整URI （請參閱[上傳二進位檔案](#upload-binary)）。
* `minPartSize` （數字）：如果有多個URI，可以提供給任一`uploadURIs`之資料的最小長度（位元組）。
* `maxPartSize` （數字）：如果有多個URI，可提供給`uploadURIs`之任一方的最大資料長度（位元組）。

### 上傳二進位檔 {#upload-binary}

起始上傳的輸出包含一或多個上傳URI值。 如果提供超過一個URI，使用者端可以依序將二進位檔案分割成多個部分，並對提供的上傳URI提出每個部分的PUT請求。 如果您選擇將二進位檔案分割成零件，請遵循下列准則：

* 除了最後一個零件外，每個零件的大小必須大於或等於`minPartSize`。
* 每個部分的大小必須小於或等於`maxPartSize`。
* 如果二進位檔的大小超過`maxPartSize`，請將二進位檔分割成多個部分以上傳。
* 您不需要使用所有URI。

如果您的二進位檔大小小於或等於`maxPartSize`，您可以改為將整個二進位檔上傳至單一上傳URI。 如果提供了多個上傳URI，請使用第一個並忽略其餘的URI。 您不需要使用所有URI。

CDN邊緣節點有助於加速要求的二進位檔上傳。

最簡單的方法是使用`maxPartSize`的值做為零件大小。 如果您使用此值作為部分大小，API合約可確保有足夠的上傳URI來上傳您的二進位檔。 若要這麼做，請依序將二進位檔案分割成大小為`maxPartSize`的部分，每個部分使用一個URI。 最後部分的大小可小於或等於`maxPartSize`。 例如，假設二進位檔案的總大小為20,000個位元組，`minPartSize`為5,000個位元組，`maxPartSize`為8,000個位元組，而且上傳URI的數量為5。 執行以下步驟：

* 使用第一個上傳URI上傳二進位的前8,000個位元組。
* 使用第二個上傳URI上傳二進位檔案的第二個8,000位元組。
* 使用第三個上傳URI上傳二進位檔案的最後4,000個位元組。 因為這是最後部分，所以它不需要大於`minPartSize`。
* 您不需要使用最後兩個上傳URI。 您可以忽略它們。

常見的錯誤是根據API提供的上傳URI數量來計算零件大小。 API合約無法保證此方法可正常運作，而且可能會造成零件大小超出`minPartSize`到`maxPartSize`的範圍。 這可能會造成二進位上傳失敗。

同樣地，最簡單且最安全的方式是隻使用大小等於`maxPartSize`的部分。

如果上傳成功，伺服器會以`201`狀態代碼回應每個要求。

>[!NOTE]
>
>如需上傳演演算法的詳細資訊，請參閱Apache Jackrabbit Oak專案中的[正式功能檔案](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload)和[API檔案](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html)。

### 完成上傳 {#complete-upload}

上傳二進位檔案的所有部分後，將HTTP POST要求提交至初始化資料提供的完整URI。 要求內文的內容型別應為`application/x-www-form-urlencoded`表單資料，包含下列欄位。

| 欄位 | 類型 | 必要與否 | 說明 |
|---|---|---|---|
| `fileName` | 字串 | 必要 | 由初始資料提供的資產名稱。 |
| `mimeType` | 字串 | 必要 | 由起始資料提供的二進位檔的HTTP內容型別。 |
| `uploadToken` | 字串 | 必要 | 上傳二進位的Token，如初始化資料所提供。 |
| `createVersion` | 布林值 | 選用 | 如果`True`和指定名稱的資產存在，則[!DNL Experience Manager]會建立該資產的新版本。 |
| `versionLabel` | 字串 | 選用 | 如果建立新版本，則會提供與資產新版本相關聯的標籤。 |
| `versionComment` | 字串 | 選用 | 如果建立了新版本，註釋會與該版本相關聯。 |
| `replace` | 布林值 | 選用 | 如果`True`和指定名稱的資產存在，[!DNL Experience Manager]會刪除該資產，然後重新建立它。 |
| `uploadDuration` | 數字 | 選用 | 檔案完整上傳的總時間，以毫秒為單位。 如果指定，上傳持續時間會包含在系統的記錄檔中，以進行傳輸率分析。 |
| `fileSize` | 數字 | 選用 | 檔案的大小（位元組）。 如果指定，檔案大小會包含在系統的記錄檔中，以進行傳輸速率分析。 |

>[!NOTE]
>
>如果資產存在，且既未指定`createVersion`也未指定`replace`，則[!DNL Experience Manager]會以新的二進位檔更新資產的目前版本。

如同起始程式，完整的請求資料可能包含多個檔案的資訊。

在呼叫檔案的完整URL之前，不會完成上傳二進位檔的程式。 資產會在上傳程式完成後處理。 即使資產的二進位檔案已完全上傳，但上傳程式未完成，處理作業也不會開始。 如果上傳成功，伺服器會以`200`狀態碼回應。

### 將資產上傳至AEM as a Cloud Service的範例殼層指令碼 {#upload-assets-shell-script}

AEM as a Cloud Service中直接二進位存取的多步驟上傳程式如下範例殼層指令碼`aem-upload.sh`所示：

```bash
#!/bin/bash

# Check if pv is installed
if ! command -v pv &> /dev/null; then
    echo "Error: 'pv' command not found. Please install it before running the script."
    exit 1
fi

# Check if jq is installed
if ! command -v jq &> /dev/null; then
    echo "Error: 'jq' command not found. Please install it before running the script."
    exit 1
fi

# Set DEBUG to true to enable debug statements
DEBUG=true

# Function for printing debug statements
function debug() {
    if [ "${DEBUG}" = true ]; then
        echo "[DEBUG] $1"
    fi
}

# Function to check if a file exists
function file_exists() {
    [ -e "$1" ]
}

# Function to check if a path is a directory
function is_directory() {
    [ -d "$1" ]
}

# Check if the required number of parameters are provided
if [ "$#" -ne 4 ]; then
    echo "Usage: $0 <aem-url> <asset-folder> <file-to-upload> <bearer-token>"
    exit 1
fi

AEM_URL="$1"
ASSET_FOLDER="$2"
FILE_TO_UPLOAD="$3"
BEARER_TOKEN="$4"

# Extracting file name or folder name from the file path
NAME=$(basename "${FILE_TO_UPLOAD}")

# Step 1: Check if "file-to-upload" is a folder
if is_directory "${FILE_TO_UPLOAD}"; then
    echo "Uploading files from the folder recursively..."
    
    # Recursively upload files in the folder
    find "${FILE_TO_UPLOAD}" -type f | while read -r FILE_PATH; do
        FILE_NAME=$(basename "${FILE_PATH}")
        debug "Uploading file: ${FILE_PATH}"
        
        # You can choose to initiate upload for each file here
        # For simplicity, let's assume you use the same ASSET_FOLDER for all files
        ./aem-upload.sh "${AEM_URL}" "${ASSET_FOLDER}" "${FILE_PATH}" "${BEARER_TOKEN}"
    done
else
    # "file-to-upload" is a single file
    FILE_NAME="${NAME}"

    # Step 2: Calculate File Size
    FILE_SIZE=$(stat -c %s "${FILE_TO_UPLOAD}")

    # Step 3: Initiate Upload
    INITIATE_UPLOAD_ENDPOINT="${AEM_URL}/content/dam/${ASSET_FOLDER}.initiateUpload.json"

    debug "Initiating upload..."
    debug "Initiate Upload Endpoint: ${INITIATE_UPLOAD_ENDPOINT}"
    debug "File Name: ${FILE_NAME}"
    debug "File Size: ${FILE_SIZE}"

    INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
        -d "fileName=${FILE_NAME}" \
        -d "fileSize=${FILE_SIZE}" \
        ${INITIATE_UPLOAD_ENDPOINT})

    # Continue with the rest of the script...
fi


# Check if the response body contains the specified HTML content for a 404 error
if echo "${INITIATE_UPLOAD_RESPONSE}" | grep -q "<title>404 Specified folder not found</title>"; then
    echo "Folder not found. Creating the folder..."

    # Attempt to create the folder
    CREATE_FOLDER_ENDPOINT="${AEM_URL}/api/assets/${ASSET_FOLDER}"

    debug "Creating folder..."
    debug "Create Folder Endpoint: ${CREATE_FOLDER_ENDPOINT}"

    CREATE_FOLDER_RESPONSE=$(curl -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -d '{"class":"'${ASSET_FOLDER}'","properties":{"title":"'${ASSET_FOLDER}'"}}' \
        ${CREATE_FOLDER_ENDPOINT})

    # Check the response code and inform the user accordingly
    STATUS_CODE_CREATE_FOLDER=$(echo "${CREATE_FOLDER_RESPONSE}" | jq -r '.properties."status.code"')
    case ${STATUS_CODE_CREATE_FOLDER} in
        201)
            echo "Folder created successfully. Initiating upload again..."

            # Retry Initiate Upload after creating the folder
            INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
                -H "Authorization: Bearer ${BEARER_TOKEN}" \
                -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
                -d "fileName=${FILE_NAME}" \
                -d "fileSize=${FILE_SIZE}" \
                ${INITIATE_UPLOAD_ENDPOINT})
            ;;
        409)
            echo "Error: Folder already exists."
            ;;
        412)
            echo "Error: Precondition failed. Root collection cannot be found or accessed."
            exit 1
            ;;
        500)
            echo "Error: Internal Server Error. Something went wrong."
            exit 1
            ;;
        *)
            echo "Error: Unexpected response code ${STATUS_CODE_CREATE_FOLDER}"
            exit 1
            ;;
    esac
fi

# Extracting values from the response
FOLDER_PATH=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.folderPath')
UPLOAD_URIS=($(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadURIs[]'))
UPLOAD_TOKEN=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadToken')
MIME_TYPE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].mimeType')
MIN_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].minPartSize')
MAX_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].maxPartSize')
COMPLETE_URI=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.completeURI')

# Extracting "Affinity-cookie" from the response headers
AFFINITY_COOKIE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | grep -i 'Affinity-cookie' | awk '{print $2}')

debug "Folder Path: ${FOLDER_PATH}"
debug "Upload Token: ${UPLOAD_TOKEN}"
debug "MIME Type: ${MIME_TYPE}"
debug "Min Part Size: ${MIN_PART_SIZE}"
debug "Max Part Size: ${MAX_PART_SIZE}"
debug "Complete URI: ${COMPLETE_URI}"
debug "Affinity Cookie: ${AFFINITY_COOKIE}"
if $DEBUG; then
    i=1
    for UPLOAD_URI in "${UPLOAD_URIS[@]}"; do
        debug "Upload URI $i: "$UPLOAD_URI
        i=$((i+1))
    done
fi


# Calculate the number of parts needed
NUM_PARTS=$(( (FILE_SIZE + MAX_PART_SIZE - 1) / MAX_PART_SIZE ))
debug "Number of Parts: $NUM_PARTS"

# Calculate the part size for the last chunk
LAST_PART_SIZE=$(( FILE_SIZE % MAX_PART_SIZE ))
if [ "${LAST_PART_SIZE}" -eq 0 ]; then
    LAST_PART_SIZE=${MAX_PART_SIZE}
fi

# Step 4: Upload binary to the blob store in parts
PART_NUMBER=1
for i in $(seq 1 $NUM_PARTS); do
    PART_SIZE=${MAX_PART_SIZE}
    if [ ${PART_NUMBER} -eq ${NUM_PARTS} ]; then
        PART_SIZE=${LAST_PART_SIZE}
        debug "Last part size: ${PART_SIZE}"
    fi

    PART_FILE="/tmp/${FILE_NAME}_part${PART_NUMBER}"

    # Creating part file 
    SKIP=$((PART_NUMBER - 1))
    SKIP=$((MAX_PART_SIZE * SKIP))
    dd if="${FILE_TO_UPLOAD}" of="${PART_FILE}"  bs="${PART_SIZE}" skip="${SKIP}" count="${PART_SIZE}" iflag=skip_bytes,count_bytes  > /dev/null 2>&1
    debug "Creating part file: ${PART_FILE} with size ${PART_SIZE}, skipping first ${SKIP} bytes."

    
    UPLOAD_URI=${UPLOAD_URIS[$PART_NUMBER-1]}

    debug "Uploading part ${PART_NUMBER}..."
    debug "Part Size: $PART_SIZE"
    debug "Part File: ${PART_FILE}"
    debug "Part File Size: $(stat -c %s "${PART_FILE}")"
    debug "Upload URI: ${UPLOAD_URI}"

    # Upload the part in the background
    if command -v pv &> /dev/null; then
        pv "${PART_FILE}" | curl --progress-bar -X PUT --data-binary "@-" "${UPLOAD_URI}" &
    else
        curl -# -X PUT --data-binary "@${PART_FILE}" "${UPLOAD_URI}" &
    fi

    PART_NUMBER=$((PART_NUMBER + 1))
done

# Wait for all background processes to finish
wait

# Step 5: Complete the upload in AEM
COMPLETE_UPLOAD_ENDPOINT="${AEM_URL}${COMPLETE_URI}"

debug "Completing the upload..."
debug "Complete Upload Endpoint: ${COMPLETE_UPLOAD_ENDPOINT}"

RESPONSE=$(curl -X POST \
    -H "Authorization: Bearer ${BEARER_TOKEN}" \
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
    -H "Affinity-cookie: ${AFFINITY_COOKIE}" \
    --data-urlencode "uploadToken=${UPLOAD_TOKEN}" \
    --data-urlencode "fileName=${FILE_NAME}" \
    --data-urlencode "mimeType=${MIME_TYPE}" \
    "${COMPLETE_UPLOAD_ENDPOINT}")
    
debug $RESPONSE

echo "File upload completed successfully."
```

### 開放原始碼上傳程式庫 {#open-source-upload-library}

若要深入瞭解上傳演演算法，或若要建置您自己的上傳指令碼和工具，Adobe提供開放原始碼程式庫和工具：

* [開放原始碼aem-upload程式庫](https://github.com/adobe/aem-upload)。
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)。

>[!NOTE]
>
>aem-upload程式庫和命令列工具都使用[node-httptransfer程式庫](https://github.com/adobe/node-httptransfer/)

### 已棄用的資產上傳API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

只有[!DNL Adobe Experience Manager]支援新的上傳方法做為[!DNL Cloud Service]。 來自[!DNL Adobe Experience Manager] 6.5的API已過時。 下列API中不建議使用與上傳或更新資產或轉譯（任何二進位上傳）相關的方法：

* [EXPERIENCE MANAGER ASSETS HTTP API](mac-api-assets.md)
* `AssetManager` Java API，例如`AssetManager.createAsset(..)`、`AssetManager.createAssetForBinary(..)`、`AssetManager.getAssetForBinary(..)`、`AssetManager.removeAssetForBinary(..)`、`AssetManager.createOrUpdateAsset(..)`、`AssetManager.createOrReplaceAsset(..)`

>[!MORELIKETHIS]
>
>* [開放原始碼aem-upload程式庫](https://github.com/adobe/aem-upload)。
>* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)。
>* [直接上傳的Apache Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload)。

## 資產處理和後續處理工作流程 {#post-processing-workflows}

在[!DNL Experience Manager]中，資產處理是以使用[資產微服務](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)的&#x200B;**[!UICONTROL 處理設定檔]**&#x200B;組態為基礎。 處理不需要開發人員擴充功能。

若要設定後續處理工作流程，請將標準工作流程與擴充功能搭配使用，並搭配自訂步驟。

## 支援後處理工作流程中的工作流程步驟 {#post-processing-workflows-steps}

如果您從舊版[!DNL Experience Manager]升級，則可以使用資產微服務來處理資產。 雲端原生資產微服務可更輕鬆設定和使用。 不支援舊版的[!UICONTROL DAM更新資產]工作流程中所使用的幾個工作流程步驟。 如需支援類別的詳細資訊，請參閱[Java API參考或Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html)。

以下技術工作流程模型已由資產微服務取代，或無法提供支援：

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。