---
title: Assets HTTP API
description: 在以下位置使用HTTP API建立、讀取、更新、刪除、管理數位資產： [!DNL Experience Manager Assets].
contentOwner: AG
feature: Assets HTTP API,APIs
role: Developer,Architect,Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager Assets] HTTP API {#assets-http-api}

## 總覽 {#overview}

此 [!DNL Assets] HTTP API允許對數位資產（包括中繼資料、轉譯和註解）以及使用的結構化內容執行建立 — 讀取 — 更新 — 刪除(CRUD)操作 [!DNL Experience Manager] 內容片段。 在 `/api/assets` 並實作為REST API。 包括 [支援內容片段](/help/assets/content-fragments/assets-api-content-fragments.md).

若要存取API:

1. 在開啟API服務檔案： `https://[hostname]:[port]/api.json`.
1. 關注 [!DNL Assets] 服務連結導向 `https://[hostname]:[server]/api/assets.json`.

API回應是某些MIME類型的JSON檔案，也是所有MIME類型的回應代碼。 JSON回應為選用，例如PDF檔案可能無法使用。 請仰賴回應程式碼進行進一步分析或動作。

>[!NOTE]
>
>不建議使用與上傳或更新資產或二進位檔（如轉譯）相關的所有API呼叫 [!DNL Experience Manager] as a [!DNL Cloud Service] 部署。 若要上傳二進位檔，請使用 [直接二進位上傳API](developer-reference-material-apis.md#asset-upload) 。

## 內容片段 {#content-fragments}

A [內容片段](/help/assets/content-fragments/content-fragments.md) 是資產的特殊類型。 它可用來存取結構化資料，例如文字、數字、日期等。 因為 `standard` 資產（例如影像或檔案）、處理內容片段時，會套用一些其他規則。

如需詳細資訊，請參閱 [中的內容片段支援 [!DNL Experience Manager Assets] HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md).

## 資料模型 {#data-model}

此 [!DNL Assets] HTTP API公開兩個主要元素、資料夾和資產（適用於標準資產）。 此外，也會針對描述內容片段中結構化內容的自訂資料模型，公開更詳細的元素。 請參閱 [內容片段資料模型](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) 以取得更多資訊。

### 資料夾 {#folders}

資料夾與傳統檔案系統中的目錄類似。 資料夾只能包含資產、資料夾或資料夾和資產。 資料夾具有下列元件：

**實體**:資料夾的實體是其子元素，可以是資料夾和資產。

**屬性**:

* `name` 是資料夾的名稱。 這與URL路徑中沒有副檔名的最後一個區段相同。
* `title` 是資料夾的選用標題，可顯示該標題而非其名稱。

>[!NOTE]
>
>資料夾或資產的某些屬性會對應至不同的首碼。 此 `jcr` 前置詞 `jcr:title`, `jcr:description`，和 `jcr:language` 取代為 `dc` 前置詞。 因此，在傳回的JSON中， `dc:title` 和 `dc:description` 包含 `jcr:title` 和 `jcr:description`，分別為。

**連結** 資料夾會公開三個連結：

* `self`:連結到自己。
* `parent`:連結至父資料夾。
* `thumbnail`:（選用）連結至資料夾縮圖影像。

### Assets {#assets}

在 [!DNL Experience Manager] 資產包含下列元素：

* 資產的屬性和中繼資料。
* 原本上傳的資產二進位檔案。
* 依設定進行多次轉譯。 這些影像可以是不同大小的影像、不同編碼的視訊，或是從PDF或 [!DNL Adobe InDesign] 檔案。
* 可選注釋。

如需內容片段中元素的相關資訊，請參閱 [Experience Manager Assets HTTP API中的內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md).

在 [!DNL Experience Manager] 資料夾具有下列元件：

* 實體：資產的子項即為其轉譯。
* 屬性.
* 連結.

## 可用功能 {#available-features}

此 [!DNL Assets] HTTP API包含下列功能：

* [檢索資料夾清單](#retrieve-a-folder-listing).
* [建立資料夾](#create-a-folder).
* [建立資產（已過時）](#create-an-asset)
* [更新資產二進位檔（已淘汰）](#update-asset-binary).
* [更新資產中繼資料](#update-asset-metadata).
* [建立資產轉譯](#create-an-asset-rendition).
* [更新資產轉譯](#update-an-asset-rendition).
* [建立資產註解](#create-an-asset-comment).
* [複製資料夾或資產](#copy-a-folder-or-asset).
* [移動資料夾或資產](#move-a-folder-or-asset).
* [刪除資料夾、資產或轉譯](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>為方便閱讀，下列範例會忽略完整的cURL備注。 標籤符號與 [雷斯蒂](https://github.com/micha/resty) 是cURL的指令碼包裝函式。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## 檢索資料夾清單 {#retrieve-a-folder-listing}

檢索現有資料夾及其子實體（子資料夾或資產）的Siren表示。

**要求**: `GET /api/assets/myFolder.json`

**回應代碼**:回應代碼為：

* 200 — 好 — 成功。
* 404 — 找不到 — 資料夾不存在或無法存取。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

**回應**:傳回的實體類別為資產或資料夾。 包含實體的屬性是每個實體的全部屬性集的子集。 為了取得實體的完整表示法，用戶端應擷取連結所指向之URL的內容，該連結具有 `rel` of `self`.

## 建立資料夾 {#create-a-folder}

建立 `sling`: `OrderedFolder` 在給定的路徑。 若 `*` 提供的servlet不是節點名稱，而是使用參數名稱作為節點名稱。 請求接受以下任一項：

* 新資料夾的Siren表示
* 一組名稱值組，編碼為 `application/www-form-urlencoded` 或 `multipart`/ `form`- `data`. 這些功能有助於直接從HTML表單建立資料夾。

此外，資料夾的屬性可指定為URL查詢參數。

API呼叫會以 `500` 回應代碼（如果提供路徑的父節點不存在）。 呼叫會傳回回應代碼 `409` 如果資料夾存在。

**參數**: `name` 是資料夾名稱。

**要求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**回應代碼**:回應代碼為：

* 201 — 建立 — 成功建立時。
* 409 — 衝突 — 如果資料夾存在。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 建立資產 {#create-an-asset}

請參閱 [資產上傳](developer-reference-material-apis.md) ，以了解如何建立資產。 您無法使用HTTP API建立資產。

## 更新資產二進位檔 {#update-asset-binary}

請參閱 [資產上傳](developer-reference-material-apis.md) 以了解如何更新資產二進位檔。 您無法使用HTTP API更新資產二進位檔。

## 更新資產的中繼資料 {#update-asset-metadata}

更新資產中繼資料屬性。 如果您更新 `dc:` 命名空間，API會更新 `jcr` 命名空間。 API不會同步兩個命名空間下的屬性。

**要求**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 建立資產轉譯 {#create-an-asset-rendition}

為資產建立轉譯。 如果未提供請求參數名稱，則會將檔案名稱用作格式副本名稱。

**參數**:參數為 `name` 格式副本的名稱，以及 `file` 作為檔案參考。

**要求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**回應代碼**

* 201 — 已建立 — 如果已成功建立轉譯。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 更新資產轉譯 {#update-an-asset-rendition}

更新會分別以新的二進位資料取代資產轉譯。

**要求**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果已成功更新轉譯。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 在資產上新增註解 {#create-an-asset-comment}

**參數**:參數為 `message` 以取得留言的訊息內文，並 `annotationData` ，以取得JSON格式的附註資料。

**要求**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果已成功建立注釋。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 複製資料夾或資產 {#copy-a-folder-or-asset}

複製提供路徑中可用的資料夾或資產，以前往新目的地。

**請求標題**:參數為：

* `X-Destination` - API解決方案範圍內的新目標URI，可將資源複製到。
* `X-Depth` - `infinity` 或 `0`. 使用 `0` 僅複製資源及其屬性，而不複製其子項。
* `X-Overwrite`  — 使用 `F` 防止覆寫現有目的地的資產。

**要求**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製至非現有目的地。
* 204 — 無內容 — 如果資料夾/資產已複製至現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標題。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 移動資料夾或資產 {#move-a-folder-or-asset}

將指定路徑的資料夾或資產移至新目的地。

**請求標題**:參數為：

* `X-Destination` - API解決方案範圍內的新目標URI，可將資源複製到。
* `X-Depth` - `infinity` 或 `0`. 使用 `0` 僅複製資源及其屬性，而不複製其子項。
* `X-Overwrite`  — 使用 `T` 強制刪除現有資源或 `F` 防止覆寫現有資源。

**要求**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製至非現有目的地。
* 204 — 無內容 — 如果資料夾/資產已複製至現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標題。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 刪除資料夾、資產或轉譯 {#delete-a-folder-asset-or-rendition}

刪除提供路徑上的資源(-tree)。

**要求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果已成功刪除資料夾。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 提示、最佳實務和限制 {#tips-limitations}

* 在 [!UICONTROL 關閉時間]，資產及其轉譯無法透過 [!DNL Assets] 網頁介面和透過HTTP API。 若 [!UICONTROL 準時] 是未來或 [!UICONTROL 關閉時間] 是過去。

* 資產HTTP API不會傳回完整的中繼資料。 命名空間會以硬式編碼撰寫，且只會傳回那些命名空間。 如需完整的中繼資料，請參閱資產路徑 `/jcr_content/metadata.json`.

* 使用API更新時，資料夾或資產的某些屬性會對應至不同的首碼。 此 `jcr` 前置詞 `jcr:title`, `jcr:description`，和 `jcr:language` 取代為 `dc` 前置詞。 因此，在傳回的JSON中， `dc:title` 和 `dc:description` 包含 `jcr:title` 和 `jcr:description`，分別為。

>[!MORELIKETHIS]
>
>* [適用於的開發人員參考檔案 [!DNL Assets]](/help/assets/developer-reference-material-apis.md)

