---
title: Assets HTTP API
description: 在 [!DNL Experience Manager Assets]中使用HTTP API來建立、讀取、更新、刪除及管理數位資產。
contentOwner: AG
feature: Assets HTTP API
role: Developer, Architect, Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: 4cec40947f1b50dd627321cabfbe43033a224f8b
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager Assets] HTTP API {#assets-http-api}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

## 概觀 {#overview}

[!DNL Assets] HTTP API允許對數位資產進行建立 — 讀取 — 更新 — 刪除(CRUD)作業，包括對中繼資料、轉譯和評論的作業，以及使用[!DNL Experience Manager]內容片段的結構化內容。 它在`/api/assets`公開，並實作為REST API。 它包含對內容片段的[支援](/help/assets/content-fragments/assets-api-content-fragments.md)。

>[!NOTE]
>
> 提供內容片段管理API的現代化OpenAPI實作。 如需完整檔案，請參閱[內容片段管理API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)。 建議使用新的OpenAPI實作。 內容片段的Assets HTTP API現有使用應移轉至新的內容片段管理OpenAPI。

若要存取API：

1. 在`https://[hostname]:[port]/api.json`開啟API服務檔案。
1. 依循前往`https://[hostname]:[server]/api/assets.json`的[!DNL Assets]服務連結。

API回應是部分MIME型別的JSON檔案，以及所有MIME型別的回應代碼。 JSON回應為選用專案，可能無法用於PDF檔案等用途。 仰賴回應程式碼進行進一步分析或動作。

>[!NOTE]
>
>與上傳或更新一般資產或二進位檔（如轉譯）相關的所有API呼叫已針對[!DNL Experience Manager]棄用作為[!DNL Cloud Service]部署。 若要上傳二進位檔，請改用[直接二進位上傳API](developer-reference-material-apis.md#asset-upload)。

## 內容片段 {#content-fragments}

[內容片段](/help/assets/content-fragments/content-fragments.md)是特殊型別的資產。 它可用來存取結構化資料，例如文字、數字、日期等。 由於`standard`資產（例如影像或檔案）有幾項差異，因此處理內容片段會套用一些其他規則。

如需詳細資訊，請參閱 [!DNL Experience Manager Assets] HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[內容片段支援。

>[!NOTE]
>
>請參閱[結構化內容傳遞與管理的AEM API](/help/headless/apis-headless-and-content-fragments.md)，以取得各種可用API的概觀，以及所涉及概念的比較。
>
>也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。

## 資料模型 {#data-model}

[!DNL Assets] HTTP API公開兩個主要元素：資料夾和資產（適用於標準資產）。 此外，它會公開自訂資料模型的更詳細元素，這些模型說明內容片段中的結構化內容。 如需進一步資訊，請參閱[內容片段資料模型](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments)。

>[!NOTE]
>
>也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。

### 資料夾 {#folders}

資料夾與傳統檔案系統中的目錄類似。 資料夾可以只包含資產，只有資料夾或資料夾和資產。 資料夾包含下列元件：

**實體**：資料夾的實體是其子元素，可以是資料夾和資產。

**屬性**：

* `name`是資料夾的名稱。 這與URL路徑中沒有副檔名的最後一個區段相同。
* `title`是資料夾的選用標題，可顯示而非其名稱。

>[!NOTE]
>
>資料夾或資產的某些屬性會對應至不同的首碼。 `jcr:title`、`jcr:description`和`jcr:language`的`jcr`首碼已取代為`dc`首碼。 因此，在傳回的JSON中，`dc:title`和`dc:description`分別包含`jcr:title`和`jcr:description`的值。

**連結**&#x200B;資料夾公開三個連結：

* `self`：連結到本身。
* `parent`：連結至父資料夾。
* `thumbnail`： （選用）連結至資料夾縮圖影像。

### Assets {#assets}

在[!DNL Experience Manager]中，資產包含下列元素：

* 資產的屬性和中繼資料。
* 原本是上傳資產的二進位檔案。
* 已設定多個轉譯。 這些可能是不同大小的影像、不同編碼的視訊，或是從PDF或[!DNL Adobe InDesign]檔案擷取的頁面。
* 選擇性註解。

如需內容片段中元素的詳細資訊，請參閱[Experience Manager Assets HTTP API中的內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)。

>[!NOTE]
>
>也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。

在[!DNL Experience Manager]中，資料夾有下列元件：

* 實體：資產的子系是其轉譯。
* 屬性。
* 連結。

## 可用功能 {#available-features}

[!DNL Assets] HTTP API包含下列功能：

* [擷取資料夾清單](#retrieve-a-folder-listing)。
* [建立資料夾](#create-a-folder)。
* [建立資產（已棄用）](#create-an-asset)
* [更新資產二進位檔（已棄用）](#update-asset-binary)。
* [更新資產中繼資料](#update-asset-metadata)。
* [建立資產轉譯](#create-an-asset-rendition)。
* [更新資產轉譯](#update-an-asset-rendition)。
* [建立資產註解](#create-an-asset-comment)。
* [複製資料夾或資產](#copy-a-folder-or-asset)。
* [行動資料夾或資產](#move-a-folder-or-asset)。
* [刪除資料夾、資產或轉譯](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>為了方便閱讀，下列範例會忽略完整的cURL標籤。 表示法與cURL的指令碼包裝函式[Resty](https://github.com/micha/resty)相關。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## 擷取資料夾清單 {#retrieve-a-folder-listing}

擷取現有資料夾及其子系圖元（子資料夾或資產）的Siren表示。

**要求**： `GET /api/assets/myFolder.json`

**回應代碼**：回應代碼為：

* 200 — 確定 — 成功。
* 404 - NOT FOUND — 資料夾不存在或無法存取。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

**回應**：傳回的實體類別是資產或資料夾。 包含之圖元的屬性是每個圖元之完整屬性集的子集。 若要取得實體的完整表示法，使用者端應擷取連結所指向的URL內容，該URL具有`self`的`rel`。

## 建立資料夾 {#create-a-folder}

在指定路徑建立`sling`： `OrderedFolder`。 如果提供`*`而非節點名稱，則servlet會使用引數名稱作為節點名稱。 請求接受下列其中一項：

* 新資料夾的警報表示法
* 一組名稱 — 值組，編碼為`application/www-form-urlencoded`或`multipart`/ `form`- `data`。 直接從HTML表單建立資料夾時，這些功能相當實用。

此外，資料夾的屬性可指定為URL查詢引數。

如果所提供路徑的父節點不存在，則API呼叫會因`500`回應代碼而失敗。 如果資料夾存在，呼叫會傳回回應代碼`409`。

**引數**： `name`是資料夾名稱。

**請求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**回應代碼**：回應代碼為：

* 201 — 建立 — 成功建立時。
* 409 — 衝突 — 如果資料夾存在。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 建立資產 {#create-an-asset}

如需如何建立資產的詳細資訊，請參閱[資產上傳](developer-reference-material-apis.md)。 您無法使用HTTP API建立資產。

## 更新資產二進位檔 {#update-asset-binary}

如需如何更新資產二進位檔的詳細資訊，請參閱[資產上傳](developer-reference-material-apis.md)。 您無法使用HTTP API更新資產二進位檔。

## 更新資產的中繼資料 {#update-asset-metadata}

更新資產中繼資料屬性。 如果您更新`dc:`名稱空間中的任何屬性，API會更新`jcr`名稱空間中的相同屬性。 此API不會同步兩個名稱空間下的屬性。

**要求**： `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**回應代碼**：回應代碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 - NOT FOUND — 如果在提供的URI中找不到或無法存取資產。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 建立資產轉譯 {#create-an-asset-rendition}

建立資產的轉譯。 如果未提供請求引數名稱，則會使用檔案名稱作為轉譯名稱。

**引數**：轉譯名稱的引數為`name`，且為檔案參考的`file`。

**請求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**回應代碼**

* 201 - CREATED — 表示已成功建立轉譯。
* 404 - NOT FOUND — 如果在提供的URI中找不到或無法存取資產。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 更新資產轉譯 {#update-an-asset-rendition}

更新會分別以新的二進位資料取代資產轉譯。

**要求**： `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**回應代碼**：回應代碼為：

* 200 — 確定 — 如果已成功更新轉譯。
* 404 - NOT FOUND — 如果在提供的URI中找不到或無法存取資產。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 在資產上新增註解 {#create-an-asset-comment}

**引數**：註解的訊息本文引數是`message`，JSON格式的註解資料引數是`annotationData`。

**要求**： `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**回應代碼**：回應代碼為：

* 201 - CREATED — 如果評論已成功建立。
* 404 - NOT FOUND — 如果在提供的URI中找不到或無法存取資產。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 複製資料夾或資產 {#copy-a-folder-or-asset}

將所提供路徑下可用的資料夾或資產複製到新目的地。

**要求標頭**：引數為：

* `X-Destination` - API解決方案範圍內的新目的地URI，可將資源複製到其中。
* `X-Depth` - `infinity`或`0`。 使用`0`只會複製資源及其屬性，不會複製其子系。
* `X-Overwrite` — 使用`F`防止覆寫現有目的地的資產。

**要求**： `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**回應代碼**：回應代碼為：

* 201 - CREATED — 若資料夾/資產已複製到不存在的目的地。
* 204 — 無內容 — 若資料夾/資產已複製到現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標頭。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 行動資料夾或資產 {#move-a-folder-or-asset}

將指定路徑的資料夾或資產移至新目的地。

**要求標頭**：引數為：

* `X-Destination` - API解決方案範圍內的新目的地URI，可將資源複製到其中。
* `X-Depth` - `infinity`或`0`。 使用`0`只會複製資源及其屬性，不會複製其子系。
* `X-Overwrite` — 使用`T`強制刪除現有資源，或使用`F`防止覆寫現有資源。

**要求**： `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**回應代碼**：回應代碼為：

* 201 - CREATED — 若資料夾/資產已複製到不存在的目的地。
* 204 — 無內容 — 若資料夾/資產已複製到現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標頭。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 刪除資料夾、資產或轉譯 {#delete-a-folder-asset-or-rendition}

在提供的路徑刪除資源(-tree)。

**請求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**回應代碼**：回應代碼為：

* 200 — 確定 — 如果資料夾已成功刪除。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 提示、最佳實務和限制 {#tips-limitations}

* 在[!UICONTROL 關閉時間]之後，無法透過[!DNL Assets]網頁介面及HTTP API使用資產及其轉譯。 如果[!UICONTROL 開啟時間]是未來時間，或[!UICONTROL 關閉時間]是過去時間，API會傳回404錯誤訊息。

* Assets HTTP API未傳回完整的中繼資料。 系統會以硬式編碼撰寫名稱空間，而且只會傳回這些名稱空間。 如需完整的中繼資料，請參閱資產路徑`/jcr_content/metadata.json`。

* 使用API更新時，資料夾或資產的某些屬性會對應至不同的首碼。 `jcr:title`、`jcr:description`和`jcr:language`的`jcr`首碼已取代為`dc`首碼。 因此，在傳回的JSON中，`dc:title`和`dc:description`分別包含`jcr:title`和`jcr:description`的值。

**另請參閱**

* [翻譯資產](translate-assets.md)
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
>*  [!DNL Assets]](/help/assets/developer-reference-material-apis.md)的[開發人員參考檔案
