---
title: Assets HTTP API
description: 使用 [!DNL Adobe Experience Manager Assets]中的HTTP API建立、讀取、更新、刪除、管理數位資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 1%

---


# Assets HTTP API {#assets-http-api}

## 概覽 {#overview}

資產HTTP API可讓您對數位資產（包括中繼資料、轉譯和注釋）以及使用[!DNL Experience Manager]內容片段的結構化內容進行建立——讀取——更新——刪除(CRUD)作業。 它在`/api/assets`公開，並實作為REST API。 它包含[內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)。

若要存取API:

1. 在`https://[hostname]:[port]/api.json`開啟API服務檔案。
1. 遵循導向`https://[hostname]:[server]/api/assets.json`的「資產」服務連結。

API回應是某些MIME類型的JSON檔案，也是所有MIME類型的回應代碼。 JSON回應是選擇性的，可能無法使用，例如PDF檔案。 請依賴回應程式碼進行進一步分析或動作。

在[!UICONTROL 關閉時間]之後，資產及其轉譯無法透過[!DNL Assets]網頁介面和HTTP API使用。 如果[!UICONTROL 開機時間]是將來或[!UICONTROL 關機時間]是過去，則API會傳回404錯誤訊息。

>[!NOTE]
>
>對於AEM，所有與上傳或更新資產或二進位檔案相關的API呼叫一般都不再提倡使用[!DNL Cloud Service]部署。 對於上傳二進位檔案，請改用[直接二進位上傳API](developer-reference-material-apis.md#asset-upload-technical)。

## 內容片段 {#content-fragments}

[內容片段](/help/assets/content-fragments/content-fragments.md)是特殊類型的資產。 它可用來存取結構化資料，例如文字、數字、日期等。 由於`standard`資產（例如影像或檔案）有數項差異，因此處理內容片段時會套用一些其他規則。

如需詳細資訊，請參閱Experience Manager Assets HTTP API[中的「內容片段支援」。](/help/assets/content-fragments/assets-api-content-fragments.md)

## 資料模型{#data-model}

資產HTTP API會公開兩個主要元素、資料夾和資產（適用於標準資產）。

此外，它還會針對描述「內容片段」中結構化內容的自訂資料模型公開更詳細的元素。 如需詳細資訊，請參閱[內容片段資料模型](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments)。

### 資料夾 {#folders}

資料夾與傳統檔案系統中的目錄類似。 它們是其他資料夾或斷言的容器。 資料夾具有以下元件：

**實體**:資料夾的實體是其子元素，可以是資料夾和資產。

**屬性**:

* `name` 是資料夾的名稱。這與URL路徑中沒有副檔名的最後一個區段相同。
* `title` 是可顯示的資料夾的可選標題，而非其名稱。

>[!NOTE]
>
>資料夾或資產的某些屬性會對應至不同的首碼。 `jcr:title`、`jcr:description`和`jcr:language`的`jcr`前置詞被`dc`前置詞替換。 因此，在傳回的JSON中，`dc:title`和`dc:description`分別包含`jcr:title`和`jcr:description`的值。

**LinksFolders** 會公開三個連結：

* `self`:連結到自己。
* `parent`:連結至父資料夾。
* `thumbnail`:（選用）資料夾縮圖影像的連結。

### 資產 {#assets}

在[!DNL Experience Manager]中，資產包含下列元素：

* 資產的屬性和中繼資料。
* 多個轉譯，例如原始轉譯（原始上傳的資產）、縮圖和各種其他轉譯。 其他轉譯可能是不同大小的影像、不同的視訊編碼，或從PDF或Adobe InDesign檔案擷取的頁面。
* 選用的注釋。

如需內容片段中元素的詳細資訊，請參閱Experience Manager Assets HTTP API[中的「內容片段支援」。](/help/assets/content-fragments/assets-api-content-fragments.md)

在[!DNL Experience Manager]中，資料夾具有以下元件：

* 實體：資產的子系是其轉譯。
* 屬性.
* 連結.

## 可用功能{#available-features}

資產HTTP API包含下列功能：

* 檢索資料夾清單。
* 建立資料夾。
* 建立資產（已過時）。
* 更新資產二進位檔（已過時）。
* 更新資產中繼資料。
* 建立資產轉譯。
* 更新資產轉譯。
* 建立資產註解。
* 複製資料夾或資產。
* 移動資料夾或資產。
* 刪除資料夾、資產或轉譯。

>[!NOTE]
>
>為方便閱讀，下列範例會省略完整的cURL符號。 事實上，該符號確實與[Resty](https://github.com/micha/resty)相關，後者是`cURL`的指令碼包裝函式。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## 檢索列出{#retrieve-a-folder-listing}的資料夾

檢索現有資料夾及其子實體（子資料夾或資產）的Siren表示法。

**要求**:  `GET /api/assets/myFolder.json`

**回應碼**:響應代碼為：

* 200 —— 好——成功。
* 404 —— 找不到——資料夾不存在或無法訪問。
* 500 —— 內部伺服器錯誤——如果有其它問題。

**回應**:傳回的實體類別為資產或資料夾。包含實體的屬性是每個實體的完整屬性集的子集。 為了獲得實體的完整表示法，客戶端應檢索連結指向的URL內容，該連結具有`self`的`rel`。

## 建立資料夾{#create-a-folder}

建立新`sling`:`OrderedFolder`。 如果提供`*`而非節點名稱，則servlet將使用參數名稱作為節點名稱。 接受為請求資料是新資料夾的Siren表示法或一組名稱——值配對，編碼為`application/www-form-urlencoded`或`multipart`/ `form`- `data`，對於直接從HTML表單建立資料夾非常有用。 此外，資料夾的屬性可指定為URL查詢參數。

如果所提供路徑的父節點不存在，則API呼叫會以`500`回應代碼失敗。 如果資料夾已存在，則調用返迴響應代碼`409`。

**參數**: `name` 是資料夾名稱。

**要求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**回應碼**:響應代碼為：

* 201 —— 建立——成功建立。
* 409 —— 衝突——如果資料夾已存在。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 建立資產{#create-an-asset}

如需如何使用API建立資產的詳細資訊，請參閱[資產上傳](developer-reference-material-apis.md)。 不建議使用HTTP API建立資產。

## 更新資產二進位檔{#update-asset-binary}

如需如何使用API更新資產二進位檔案的詳細資訊，請參閱[asset upload](developer-reference-material-apis.md)。 不建議使用HTTP API更新資產二進位檔。

## 更新資產{#update-asset-metadata}的中繼資料

更新資產中繼資料屬性。 如果您更新`dc:`命名空間中的任何屬性，API會更新`jcr`命名空間中的相同屬性。 API不會同步兩個名稱空間下的屬性。

**要求**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**回應碼**:響應代碼為：

* 200 —— 確定——如果資產已成功更新。
* 404 —— 找不到——如果在提供的URI中找不到或訪問資產，請執行此操作。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 建立資產轉譯{#create-an-asset-rendition}

為資產建立新的資產轉譯。 如果未提供請求參數名稱，則會使用檔案名稱做為轉譯名稱。

**參數**:這些參數 `name` 是格式副本的名稱， `file` 並作為檔案參考。

**要求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**回應碼**

* 201 —— 已建立——如果已成功建立轉譯。
* 404 —— 找不到——如果在提供的URI中找不到或訪問資產，請執行此操作。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 更新資產轉譯{#update-an-asset-rendition}

更新會分別以新的二進位資料取代資產轉譯。

**要求**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**回應碼**:響應代碼為：

* 200 —— 確定——如果已成功更新轉譯。
* 404 —— 找不到——如果在提供的URI中找不到或訪問資產，請執行此操作。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 在資產{#create-an-asset-comment}上新增註解

建立新資產註解。

**參數**:參數是 `message` 用於注釋的消息主體和 `annotationData` JSON格式的注釋資料。

**要求**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**回應碼**:響應代碼為：

* 201 —— 已建立——如果已成功建立注釋。
* 404 —— 找不到——如果在提供的URI中找不到或訪問資產，請執行此操作。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 複製資料夾或資產{#copy-a-folder-or-asset}

複製位於提供路徑中的可用資料夾或資產，以連至新目標。

**請求標題**:參數包括：

* `X-Destination` - API解決方案範圍內的新目標URI，用於將資源複製到。
* `X-Depth` - `infinity` 或 `0`。使用`0`僅複製資源及其屬性，而不複製其子項。
* `X-Overwrite` -用 `F` 於防止覆寫現有目標的資產。

**要求**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**回應碼**:響應代碼為：

* 201 —— 已建立——如果資料夾／資產已複製到非現有目標。
* 204 —— 無內容——如果資料夾／資產已複製至現有目的地。
* 412 —— 前提條件失敗——如果缺少請求標題。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 移動資料夾或資產{#move-a-folder-or-asset}

將指定路徑上的資料夾或資產移動到新目標。

**請求標題**:參數包括：

* `X-Destination` - API解決方案範圍內的新目標URI，用於將資源複製到。
* `X-Depth` - `infinity` 或 `0`。使用`0`僅複製資源及其屬性，而不複製其子項。
* `X-Overwrite` -使用強 `T` 制刪除現有資源或 `F` 防止覆寫現有資源。

**要求**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**回應碼**:響應代碼為：

* 201 —— 已建立——如果資料夾／資產已複製到非現有目標。
* 204 —— 無內容——如果資料夾／資產已複製至現有目的地。
* 412 —— 前提條件失敗——如果缺少請求標題。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 刪除資料夾、資產或轉譯{#delete-a-folder-asset-or-rendition}

刪除提供路徑上的資源(-tree)。

**要求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**回應碼**:響應代碼為：

* 200 —— 確定——如果資料夾已成功刪除。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。
