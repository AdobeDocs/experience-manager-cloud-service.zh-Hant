---
title: Assets HTTP API
description: 使用HTTP API建立、讀取、更新、刪除、管理數字資產 [!DNL Experience Manager Assets]。
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

## 概覽 {#overview}

的 [!DNL Assets] HTTP API允許對數字資產（包括元資料、格式副本和注釋）以及結構化內容（使用）執行建立 — 讀取 — 更新 — 刪除(CRUD)操作 [!DNL Experience Manager] 內容片段。 它在 `/api/assets` 並作為REST API實現。 包括 [支援內容片段](/help/assets/content-fragments/assets-api-content-fragments.md)。

要訪問API:

1. 在以下位置開啟API服務文檔： `https://[hostname]:[port]/api.json`。
1. 關注 [!DNL Assets] 服務連結導向 `https://[hostname]:[server]/api/assets.json`。

API響應是某些MIME類型的JSON檔案，是所有MIME類型的響應代碼。 JSON響應是可選的，可能不可用，例如，PDF檔案。 依靠響應代碼進行進一步分析或操作。

>[!NOTE]
>
>與上傳或更新一般資產或二進位檔案（如格式副本）相關的所有API調用均不建議使用 [!DNL Experience Manager] 作為 [!DNL Cloud Service] 部署。 要上載二進位檔案，請使用 [直接二進位上載API](developer-reference-material-apis.md#asset-upload) 的雙曲餘切值。

## 內容片段 {#content-fragments}

A [內容片段](/help/assets/content-fragments/content-fragments.md) 是一種特殊的資產類型。 它可用於訪問結構化資料，如文本、數字、日期等。 由於有幾種不同 `standard` 資產（如影像或文檔），某些附加規則適用於處理內容片段。

有關詳細資訊，請參見 [在中支援內容片段 [!DNL Experience Manager Assets] HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)。

## 資料模型 {#data-model}

的 [!DNL Assets] HTTP API公開兩個主要元素，資料夾和資產（對於標準資產）。 此外，它還為描述內容片段中結構化內容的自定義資料模型顯示更詳細的元素。 請參閱 [內容片段資料模型](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) 的上界。

### 資料夾 {#folders}

資料夾與傳統檔案系統中的目錄類似。 資料夾只能包含資產、資料夾或資料夾和資產。 資料夾具有以下元件：

**實體**:資料夾的實體是其子元素，可以是資料夾和資產。

**屬性**:

* `name` 是資料夾的名稱。 這與URL路徑中沒有副檔名的最後一個段相同。
* `title` 是資料夾的可選標題，可以顯示該標題，而不是其名稱。

>[!NOTE]
>
>資料夾或資產的某些屬性映射到其他前置詞。 的 `jcr` 前置詞 `jcr:title`。 `jcr:description`, `jcr:language` 替換為 `dc` 前置詞。 因此，在返回的JSON中， `dc:title` 和 `dc:description` 包含 `jcr:title` 和 `jcr:description`的下界。

**連結** 資料夾公開三個連結：

* `self`:連結到自身。
* `parent`:連結到父資料夾。
* `thumbnail`:（可選）指向資料夾縮略圖的連結。

### 資產 {#assets}

在 [!DNL Experience Manager] 資產包含以下元素：

* 資產的屬性和元資料。
* 最初上載了資產的二進位檔案。
* 配置了多個格式副本。 這些影像可以是不同大小的影像、不同編碼的視頻，或從PDF或 [!DNL Adobe InDesign] 的子菜單。
* 可選注釋。

有關內容片段中元素的資訊，請參見 [Experience Manager AssetsHTTP API中的內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)。

在 [!DNL Experience Manager] 資料夾具有以下元件：

* 實體：資產的子項是其格式副本。
* 屬性.
* 連結.

## 可用功能 {#available-features}

的 [!DNL Assets] HTTP API包括以下功能：

* [檢索資料夾清單](#retrieve-a-folder-listing)。
* [建立資料夾](#create-a-folder)。
* [建立資產（不建議使用）](#create-an-asset)
* [更新資產二進位檔案（不建議使用）](#update-asset-binary)。
* [更新資產元資料](#update-asset-metadata)。
* [建立資產格式副本](#create-an-asset-rendition)。
* [更新資產格式副本](#update-an-asset-rendition)。
* [建立資產注釋](#create-an-asset-comment)。
* [複製資料夾或資產](#copy-a-folder-or-asset)。
* [移動資料夾或資產](#move-a-folder-or-asset)。
* [刪除資料夾、資產或格式副本](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>為便於閱讀，以下示例省略了完整的cURL符號。 符號與 [雷斯蒂](https://github.com/micha/resty) 是cURL的指令碼包裝。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## 檢索資料夾清單 {#retrieve-a-folder-listing}

檢索現有資料夾及其子實體（子資料夾或資產）的Siren表示法。

**請求**: `GET /api/assets/myFolder.json`

**響應代碼**:響應代碼為：

* 200 — 好 — 成功。
* 404 — 未找到 — 資料夾不存在或無法訪問。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

**響應**:返回的實體類是資產或資料夾。 包含的實體的屬性是每個實體的全部屬性集的子集。 為了獲得實體的完整表示形式，客戶端應檢索連結指向的URL的內容 `rel` 共 `self`。

## 建立資料夾 {#create-a-folder}

建立 `sling`: `OrderedFolder` 在給定路徑上。 如果 `*` 提供而不是節點名稱，servlet將參數名稱用作節點名稱。 請求接受以下任一項：

* 新資料夾的警報表示
* 一組名稱 — 值對，編碼為 `application/www-form-urlencoded` 或 `multipart`/ `form`- `data`。 這些功能對於直接從HTML窗體建立資料夾非常有用。

此外，資料夾的屬性可以指定為URL查詢參數。

API調用失敗， `500` 響應代碼（如果提供路徑的父節點不存在）。 呼叫返迴響應代碼 `409` 資料夾。

**參數**: `name` 是資料夾名稱。

**要求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**響應代碼**:響應代碼為：

* 201 — 建立 — 成功建立。
* 409 — 衝突 — 如果資料夾存在。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 建立資產 {#create-an-asset}

請參閱 [資產上載](developer-reference-material-apis.md) 的子菜單。 不能使用HTTP API建立資產。

## 更新資產二進位 {#update-asset-binary}

請參閱 [資產上載](developer-reference-material-apis.md) 有關如何更新資產二進位檔案的資訊。 不能使用HTTP API更新資產二進位檔案。

## 更新資產的元資料 {#update-asset-metadata}

更新資產元資料屬性。 如果更新中的任何屬性 `dc:` 命名空間， API更新 `jcr` 命名空間。 API不同步兩個命名空間下的屬性。

**請求**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**響應代碼**:響應代碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 — 未找到 — 如果在提供的URI中找不到或無法訪問資產。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 建立資產格式副本 {#create-an-asset-rendition}

為資產建立格式副本。 如果未提供請求參數名，則檔案名將用作格式副本名稱。

**參數**:參數為 `name` 格式副本的名稱和 `file` 檔案引用。

**要求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**響應代碼**

* 201 — 已建立 — 如果已成功建立格式副本。
* 404 — 未找到 — 如果在提供的URI中找不到或無法訪問資產。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 更新資產格式副本 {#update-an-asset-rendition}

更新分別用新二進位資料替換資產格式副本。

**請求**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**響應代碼**:響應代碼為：

* 200 — 確定 — 如果格式副本已成功更新。
* 404 — 未找到 — 如果在提供的URI中找不到或無法訪問資產。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 在資產上添加註釋 {#create-an-asset-comment}

**參數**:參數為 `message` 以獲取注釋和 `annotationData` 標籤。

**請求**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**響應代碼**:響應代碼為：

* 201 — 已建立 — 如果已成功建立注釋。
* 404 — 未找到 — 如果在提供的URI中找不到或無法訪問資產。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 複製資料夾或資產 {#copy-a-folder-or-asset}

複製在提供的路徑中可用到新目標的資料夾或資產。

**請求標題**:參數包括：

* `X-Destination` - API解決方案作用域內的新目標URI，將資源複製到。
* `X-Depth` - `infinity` 或 `0`。 使用 `0` 只複製資源及其屬性，而不複製其子項。
* `X-Overwrite`  — 使用 `F` 來防止覆蓋現有目標上的資產。

**請求**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**響應代碼**:響應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製到非現有目標。
* 204 — 無內容 — 如果資料夾/資產已複製到現有目標。
* 412 - PRECONTIDE FAILED — 如果缺少請求標頭。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 移動資料夾或資產 {#move-a-folder-or-asset}

將給定路徑上的資料夾或資產移動到新目標。

**請求標題**:參數包括：

* `X-Destination` - API解決方案作用域內的新目標URI，將資源複製到。
* `X-Depth` - `infinity` 或 `0`。 使用 `0` 只複製資源及其屬性，而不複製其子項。
* `X-Overwrite`  — 使用 `T` 強制刪除現有資源或 `F` 來防止覆蓋現有資源。

**請求**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**響應代碼**:響應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製到非現有目標。
* 204 — 無內容 — 如果資料夾/資產已複製到現有目標。
* 412 - PRECONTIDE FAILED — 如果缺少請求標頭。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 刪除資料夾、資產或格式副本 {#delete-a-folder-asset-or-rendition}

刪除所提供路徑上的資源(-tree)。

**要求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**響應代碼**:響應代碼為：

* 200 — 確定 — 如果資料夾已成功刪除。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 提示、最佳做法和限制 {#tips-limitations}

* 在 [!UICONTROL 關機時間]，資產及其格式副本不可通過 [!DNL Assets] Web介面和通過HTTP API。 如果 [!UICONTROL 準時] 是將來的 [!UICONTROL 關機時間] 是過去。

* 資產HTTP API不返回完整的元資料。 命名空間是硬編碼的，只返回那些命名空間。 有關完整元資料，請參閱資產路徑 `/jcr_content/metadata.json`。

* 使用API更新時，資料夾或資產的某些屬性會映射到其他前置詞。 的 `jcr` 前置詞 `jcr:title`。 `jcr:description`, `jcr:language` 替換為 `dc` 前置詞。 因此，在返回的JSON中， `dc:title` 和 `dc:description` 包含 `jcr:title` 和 `jcr:description`的下界。

>[!MORELIKETHIS]
>
>* [開發人員參考文檔 [!DNL Assets]](/help/assets/developer-reference-material-apis.md)

