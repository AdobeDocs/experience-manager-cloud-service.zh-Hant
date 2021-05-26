---
title: Assets HTTP API
description: 使用 [!DNL Experience Manager Assets]中的HTTP API建立、讀取、更新、刪除、管理數位資產。
contentOwner: AG
feature: Assets HTTP API,API
role: Developer,Architect,Administrator
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: 2e00b62efa07488fbdba723d283b9b76b53f6d34
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager Assets] HTTP API  {#assets-http-api}

## 概覽 {#overview}

[!DNL Assets] HTTP API允許對數位資產（包括中繼資料、轉譯和註解），以及使用[!DNL Experience Manager]內容片段的結構化內容執行建立 — 讀取 — 更新 — 刪除(CRUD)操作。 它在`/api/assets`公開，並以REST API實作。 其中包含[支援內容片段](/help/assets/content-fragments/assets-api-content-fragments.md)。

若要存取API:

1. 在`https://[hostname]:[port]/api.json`開啟API服務檔案。
1. 遵循導向`https://[hostname]:[server]/api/assets.json`的[!DNL Assets]服務連結。

API回應是某些MIME類型的JSON檔案，也是所有MIME類型的回應代碼。 JSON回應為選用，例如PDF檔案可能無法使用。 請仰賴回應程式碼進行進一步分析或動作。

>[!NOTE]
>
>[!DNL Experience Manager]的[!DNL Cloud Service]部署會不建議使用與上傳或更新一般資產或二進位檔（如轉譯）相關的所有API呼叫。 若是上傳二進位檔，請改用[直接二進位上傳API](developer-reference-material-apis.md#asset-upload)。

## 內容片段 {#content-fragments}

[內容片段](/help/assets/content-fragments/content-fragments.md)是特殊類型的資產。 它可用來存取結構化資料，例如文字、數字、日期等。 由於`standard`資產（例如影像或檔案）有幾項差異，因此處理內容片段時會套用一些其他規則。

如需詳細資訊，請參閱 [!DNL Experience Manager Assets] HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[內容片段支援。

## 資料模型{#data-model}

[!DNL Assets] HTTP API公開兩個主要元素、資料夾和資產（適用於標準資產）。 此外，也會針對描述內容片段中結構化內容的自訂資料模型，公開更詳細的元素。 如需詳細資訊，請參閱[內容片段資料模型](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments)。

### 資料夾 {#folders}

資料夾與傳統檔案系統中的目錄類似。 資料夾只能包含資產、資料夾或資料夾和資產。 資料夾具有下列元件：

**實體**:資料夾的實體是其子元素，可以是資料夾和資產。

**屬性**:

* `name` 是資料夾的名稱。這與URL路徑中沒有副檔名的最後一個區段相同。
* `title` 是資料夾的選用標題，可顯示該標題而非其名稱。

>[!NOTE]
>
>資料夾或資產的某些屬性會對應至不同的首碼。 `jcr`前置詞`jcr:title`、`jcr:description`和`jcr:language`會以`dc`前置詞取代。 因此，在傳回的JSON中，`dc:title`和`dc:description`分別包含`jcr:title`和`jcr:description`的值。

**** LinksFolders公開三個連結：

* `self`:連結到自己。
* `parent`:連結至父資料夾。
* `thumbnail`:（選用）連結至資料夾縮圖影像。

### 資產 {#assets}

在[!DNL Experience Manager]中，資產包含下列元素：

* 資產的屬性和中繼資料。
* 原本上傳的資產二進位檔案。
* 依設定進行多次轉譯。 這些影像可以是不同大小的影像、不同編碼的視訊，或從PDF或[!DNL Adobe InDesign]檔案中擷取的頁面。
* 可選注釋。

如需內容片段中元素的相關資訊，請參閱Experience Manager資產HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[內容片段支援。

在[!DNL Experience Manager]中，資料夾具有以下元件：

* 實體：資產的子項即為其轉譯。
* 屬性.
* 連結.

## 可用功能{#available-features}

[!DNL Assets] HTTP API包含下列功能：

* [擷取資料夾清單](#retrieve-a-folder-listing)。
* [建立資料夾](#create-a-folder)。
* [建立資產（已過時）](#create-an-asset)
* [更新資產二進位檔（已淘汰）](#update-asset-binary)。
* [更新資產中繼資料](#update-asset-metadata)。
* [建立資產轉譯](#create-an-asset-rendition)。
* [更新資產轉譯](#update-an-asset-rendition)。
* [建立資產註解](#create-an-asset-comment)。
* [複製資料夾或資產](#copy-a-folder-or-asset)。
* [移動資料夾或資產](#move-a-folder-or-asset)。
* [刪除資料夾、資產或轉譯](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>為方便閱讀，下列範例會忽略完整的cURL備注。 標籤法會與[Resty](https://github.com/micha/resty)關聯，後者是cURL的指令碼包裝函式。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## 檢索清單{#retrieve-a-folder-listing}的資料夾

檢索現有資料夾及其子實體（子資料夾或資產）的Siren表示。

**請求**:  `GET /api/assets/myFolder.json`

**回應代碼**:回應代碼為：

* 200 — 好 — 成功。
* 404 — 找不到 — 資料夾不存在或無法存取。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

**回應**:傳回的實體類別為資產或資料夾。包含的實體的屬性是每個實體的全部屬性集的子集。 為了獲得實體的完整表示，客戶端應檢索連結所指向的URL的內容，該連結具有`self`的`rel`。

## 建立資料夾{#create-a-folder}

建立`sling`:`OrderedFolder`。 如果提供`*`而非節點名稱，則servlet將參數名稱用作節點名稱。 請求接受以下任一項：

* 新資料夾的Siren表示
* 一組名稱值對，編碼為`application/www-form-urlencoded`或`multipart`/ `form`- `data`。 這些功能有助於直接從HTML表單建立資料夾。

此外，資料夾的屬性可指定為URL查詢參數。

如果提供路徑的父節點不存在，則API呼叫會因`500`回應代碼而失敗。 如果資料夾存在，呼叫會傳回回應代碼`409`。

**參數**: `name` 是資料夾名稱。

**要求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**回應代碼**:回應代碼為：

* 201 — 建立 — 成功建立時。
* 409 — 衝突 — 如果資料夾存在。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 建立資產{#create-an-asset}

如需如何建立資產的詳細資訊，請參閱[資產上傳](developer-reference-material-apis.md)。 您無法使用HTTP API建立資產。

## 更新資產二進位檔{#update-asset-binary}

如需如何更新資產二進位檔的資訊，請參閱[資產上傳](developer-reference-material-apis.md)。 您無法使用HTTP API更新資產二進位檔。

## 更新資產{#update-asset-metadata}的中繼資料

更新資產中繼資料屬性。 如果您更新`dc:`命名空間中的任何屬性，API會更新`jcr`命名空間中的相同屬性。 API不會同步兩個命名空間下的屬性。

**請求**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 建立資產轉譯{#create-an-asset-rendition}

為資產建立轉譯。 如果未提供請求參數名稱，則會將檔案名稱用作格式副本名稱。

**參數**:參數用 `name` 於格式副本的名稱， `file` 並作為檔案引用。

**要求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**回應代碼**

* 201 — 已建立 — 如果已成功建立轉譯。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 更新資產轉譯{#update-an-asset-rendition}

更新會分別以新的二進位資料取代資產轉譯。

**請求**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果已成功更新轉譯。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 在資產{#create-an-asset-comment}上新增註解

**參數**:參數適 `message` 用於註解的訊息內文，以 `annotationData` 及JSON格式的附註資料。

**請求**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果已成功建立注釋。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 複製資料夾或資產{#copy-a-folder-or-asset}

複製提供路徑中可用的資料夾或資產，以前往新目的地。

**請求標題**:參數為：

* `X-Destination` - API解決方案範圍內的新目標URI，可將資源複製到。
* `X-Depth` - `infinity` 或 `0`。使用`0`只會複製資源及其屬性，而不會複製其子項。
* `X-Overwrite`  — 使 `F` 用防止覆寫現有目的地的資產。

**請求**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製至非現有目的地。
* 204 — 無內容 — 如果資料夾/資產已複製至現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標題。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 移動資料夾或資產{#move-a-folder-or-asset}

將指定路徑的資料夾或資產移至新目的地。

**請求標題**:參數為：

* `X-Destination` - API解決方案範圍內的新目標URI，可將資源複製到。
* `X-Depth` - `infinity` 或 `0`。使用`0`只會複製資源及其屬性，而不會複製其子項。
* `X-Overwrite`  — 使用強 `T` 制刪除現有資源或 `F` 防止覆寫現有資源。

**請求**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製至非現有目的地。
* 204 — 無內容 — 如果資料夾/資產已複製至現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標題。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 刪除資料夾、資產或轉譯{#delete-a-folder-asset-or-rendition}

刪除提供路徑上的資源(-tree)。

**要求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果已成功刪除資料夾。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 提示、最佳作法和限制{#tips-limitations}

* 在[!UICONTROL 關閉時間]之後，資產及其轉譯無法透過[!DNL Assets]網頁介面和HTTP API使用。 如果[!UICONTROL 準時]為將來或[!UICONTROL 非時間]為過去，則API會傳回404錯誤訊息。

* 資產HTTP API不會傳回完整的中繼資料。 命名空間會以硬式編碼撰寫，且只會傳回那些命名空間。 如需完整中繼資料，請參閱資產路徑`/jcr_content/metadata.json`。

* 使用API更新時，資料夾或資產的某些屬性會對應至不同的首碼。 `jcr`前置詞`jcr:title`、`jcr:description`和`jcr:language`會以`dc`前置詞取代。 因此，在傳回的JSON中，`dc:title`和`dc:description`分別包含`jcr:title`和`jcr:description`的值。

>[!MORELIKETHIS]
>
>* [ [!DNL Assets]的開發人員參考檔案](/help/assets/developer-reference-material-apis.md)

