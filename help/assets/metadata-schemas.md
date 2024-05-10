---
title: 中繼資料結構描述會定義中繼資料屬性頁面的配置
description: 中繼資料結構會定義屬性頁面的配置，以及為資產顯示的中繼資料屬性。 瞭解如何建立自訂中繼資料結構、編輯中繼資料結構，以及如何將中繼資料結構套用至資產。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 9e94afeb-1c54-4653-bf52-b0910c0cb6c1
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '2634'
ht-degree: 9%

---

# 中繼資料結構描述 {#metadata-schemas}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-schemas.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

組織會提出中繼資料模型，藉以強化資產探索、使用、互通性等。 正確的中繼資料應用程式對於維護中繼資料驅動的工作流程和流程至關重要。 若要遵循組織範圍的中繼資料策略和標準，您可以使用可協助DAM使用者調整的中繼資料結構。 [!DNL Adobe Experience Manager] 允許以簡單且靈活的方法建立、維護和套用中繼資料結構。

在 [!DNL Adobe Experience Manager Assets]，結構描述包含要填寫的特定資訊的特定欄位。 它也包含版面資訊，以便以方便使用的方式顯示中繼資料欄位。 中繼資料屬性包括標題、說明、MIME型別、標籤等。 您可以使用 [!UICONTROL 中繼資料結構Forms] 編輯器以修改現有方案或新增自訂中繼資料方案。

若要檢視及編輯資產的屬性頁面，請遵循下列步驟：

1. 按一下 **[!UICONTROL 檢視屬性]** 卡片檢視中資產圖磚上的快速動作選項。 或者，選取資產，然後按一下 **[!UICONTROL 屬性]** ![檢視屬性](assets/do-not-localize/info-circle-icon.png) 工具列中的。

1. 您可以在可用的標籤下編輯各種可編輯的中繼資料屬性。 但是，您無法修改資產 [!UICONTROL 型別] 在 [!UICONTROL 基本] 屬性頁面的索引標籤。

   ![資產屬性的基本索引標籤，無法變更資產型別](assets/asset-properties-basic-tab.png)

   *圖：資產上的基本索引標籤 [!UICONTROL 屬性].*

   若要修改資產的MIME型別，請使用自訂中繼資料結構表單或修改現有表單。 另請參閱 [編輯中繼資料結構Forms](#edit-metadata-schema-forms) 以取得詳細資訊。 如果您修改MIME型別的中繼資料結構，資產和所有子型別的屬性頁面配置都會被修改。 例如，修改底下的jpeg架構 `default/image` 僅修改MIME型別資產的中繼資料配置（資產屬性） `image/jpeg`. 不過，如果您編輯預設架構，您所做的變更會修改所有資產型別的中繼資料配置。

## 中繼資料結構表單 {#default-metadata-schema-forms}

若要檢視表單或範本清單，請在 [!DNL Experience Manager] 介面導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.

[!DNL Experience Manager] 提供下列中繼資料結構表單範本。

| 範本 | | 說明 |
|---|---|---|
| [!UICONTROL 預設] | | 資產的基本中繼資料結構表單。 |
| | 下列子表單會繼承 [!UICONTROL 預設] 表單： | |
| | <ul><li>[!UICONTROL dm_video]</li></ul> | Dynamic Media影片的結構描述表單。 |
| | <ul><li>[!UICONTROL 影像]</li></ul> | 具有MIME型別的影像的結構表單，例如 `image/jpeg` 和 `image/png`. <br> 此 [!UICONTROL 影像] 表單有以下子表單範本： <ul><li> [!UICONTROL jpeg]：具有子型別的資產的結構描述表單 [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]：具有子型別TIFF的資產的結構描述表單。</li></ul> |
| | <ul><li>[!UICONTROL 應用計畫]</li></ul> | 具有MIME型別的資產的結構表單，例如 `application/pdf` 和 `application/zip`. <br>[!UICONTROL pdf]：具有子型別PDF的資產結構表單。 |
| | <ul><li>[!UICONTROL 視訊]</li></ul> | 具有MIME型別的視訊資產的結構表單，例如 `video/avi` 和 `video/mp4`. |
| [!UICONTROL 集合] | | 集合的結構表單。 |
| [!UICONTROL contentfragment] | | 內容片段的結構描述表單。 |
| [!UICONTROL 表單] | | 此結構表單與 [!DNL Adobe Experience Manager Forms]. |
| [!UICONTROL ugc_contentfragment] | | 使用者產生的內容片段和資產的結構描述表單，可從社群媒體整合至Experience Manager。 |

>[!NOTE]
>
>若要檢視方案表單的子表單，請按一下方案表單名稱。

## 新增中繼資料結構表單 {#add-a-metadata-schema-form}

若要新增中繼資料結構表單，請執行下列步驟：

1. 若要新增自訂範本至清單，請按一下 **[!UICONTROL 建立]** 工具列中的。

   >[!NOTE]
   >
   >鎖定符號會與未編輯的範本一起顯示。 如果您自訂範本，則範本不會鎖定 ![鎖定已關閉](assets/do-not-localize/lock_closed_icon.svg).

1. 在對話方塊中，提供結構表單的標題，然後按一下 **[!UICONTROL 建立]** 以完成表單建立程式。

## 編輯中繼資料結構表單 {#edit-metadata-schema-forms}

您可以編輯新新增或現有的中繼資料結構表單。 中繼資料結構表單包含索引標籤以及索引標籤內的表單專案。 您可以將這些表單專案對應/設定到CRX存放庫中中繼資料節點內的欄位。 您可以將索引標籤或表單專案新增到中繼資料結構表單。 從父項衍生的標籤和表單專案處於鎖定狀態。 您無法在子層級變更它們。

1. 在 [!UICONTROL 中繼資料結構Forms] 頁面，選取表單並按一下 **[!UICONTROL 編輯]** （在工具列中）。

1. 在 **[!UICONTROL 中繼資料結構表單編輯器]** 頁面，自訂中繼資料表單。 將所需的元件從 **[!UICONTROL 建置表單]** 標籤移至其中一個標籤。

   ![中繼資料結構編輯器可自訂資產屬性頁面](assets/metadata-schema-editor.png)

   *圖：A [!UICONTROL 中繼資料結構表單編輯器] 具有可用索引標籤的頁面。*

1. 若要設定元件，請選取該元件，並在下列位置修改其屬性： **[!UICONTROL 設定]** 標籤。

### 內的元件 [!UICONTROL 建置表單] 標籤 {#components-within-the-build-form-tab}

此 **[!UICONTROL 建置表單]** 索引標籤會列出您在結構表單中使用的表單專案。 此 **[!UICONTROL 設定]** 標籤會提供您在「 」中選取的每個專案屬性。 **[!UICONTROL 建置表單]** 標籤。 下表列出 **[!UICONTROL 建置表單]** 標籤：

| 元件名稱 | 說明 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 區段標題] | 新增區段標題以取得常用元件清單。 |
| [!UICONTROL 單行文字] | 新增單行文字屬性。 它會儲存為字串。 |
| [!UICONTROL 多值文字] | 新增多值文字屬性。 它會儲存為字串陣列。 |
| [!UICONTROL 數字] | 新增數字元件。 |
| [!UICONTROL 日期] | 新增日期元件。 |
| [!UICONTROL 下拉式清單] | 新增下拉式清單。 |
| [!UICONTROL 標準標籤] | 新增標籤。 |
| [!UICONTROL 智慧標記] | 透過自動新增中繼資料標記增強搜尋功能。 |
| [!UICONTROL 隱藏欄位] | 新增隱藏欄位。 儲存資產時，會以POST引數的形式傳送。 |
| [!UICONTROL 資產引用者] | 新增此元件以檢視資產所參考的資產清單。 |
| [!UICONTROL 資產引用] | 新增以顯示參照資產的資產清單。 |
| [!UICONTROL 產品引用] | 新增以顯示與資產連結的產品清單。 |
| [!UICONTROL 內容中繼資料] | 新增以控制其他中繼資料索引標籤在資產屬性頁面中的顯示。 |

<!-- TBD: Ratings are not available in Experience Manager as a Cloud Service. Removed via cqdoc-18089 ticket. 
| [!UICONTROL Asset Rating]        | Add to display options for rating the asset.                                       |
-->

#### 編輯中繼資料元件 {#edit-the-metadata-component}

若要編輯表單上中繼資料元件的屬性，請按一下該元件以編輯表單中下列屬性的全部或子集： **[!UICONTROL 設定]** 標籤。 建議僅將一個欄位對應到中繼資料結構描述中的指定屬性。 否則，系統會挑選對應至屬性的最新新增欄位。

**欄位標籤**：在資產的屬性頁面上顯示的中繼資料屬性名稱。

**對應至屬性**：此屬性會指定資產節點（儲存於CRX存放庫中）的相對路徑或名稱。 開始於 `./` 以指出路徑位於資產的節點下。

以下是屬性的有效值範例：

* `./jcr:content/metadata/dc:title`:將值儲存在資產的中繼資料節點，做為屬性 `dc:title`。

* `./jcr:created`：儲存資產的建立日期和時間。 這是受保護的屬性。 如果您設定這些屬性，Adobe建議您將其標示為「停用編輯」。 否則，當您儲存資產的屬性時，會出現「資產無法修改」錯誤。

為確保元件在中繼資料結構表單中正確顯示，屬性路徑不應包含任何空格。

* **預留位置**：使用此屬性可指定與中繼資料屬性相關的預留位置文字。
* **必填**：使用此屬性可將中繼資料屬性標示為屬性頁面上的必要屬性。
* **停用編輯**：使用此屬性可禁止對屬性頁面上的屬性進行任何編輯。
* **以唯讀方式顯示空白欄位**：標示此屬性以在屬性頁面上顯示中繼資料屬性，即使該屬性沒有值亦然。 根據預設，當中繼資料屬性沒有值時，它不會列在屬性頁面上。
* **顯示排序清單**：此屬性用於顯示排序的選擇清單。
* **選擇**：使用此屬性來指定清單中的選項。
* **說明** ：使用此屬性為中繼資料元件新增簡短說明。
* **類別**：與屬性相關聯的物件類別。
* **刪除**：按一下 [!UICONTROL 刪除] 以從結構表單中刪除元件。

>[!NOTE]
>
>此 [!UICONTROL 隱藏欄位] 元件不包含這些屬性。 而是包含屬性，例如「名稱」、「值」、「欄位標籤」和「說明」。 每當儲存資產時，「隱藏欄位」元件的值都會以POST引數的形式傳送。 它不會儲存為資產的中繼資料。

如果您選取「必 **[!UICONTROL 要]** 」選項，可以搜尋遺失必要中繼資料的資產。從「篩 **[!UICONTROL 選器]** 」面板中，展開「中繼資料 **[!UICONTROL 驗證謂語]** 」並選取「 **[!UICONTROL 無效]** 」選項。搜尋結果會顯示遺失您透過結構表單設定之必要中繼資料的資產。

如果您將「關聯式中繼資料」元件新增至任何結構描述表單的任何索引標籤中，該元件會在套用特定結構描述的資產屬性頁面中顯示為清單。 此清單包含所有其他標籤，除了您套用內容中繼資料元件的標籤以外。 目前，此功能提供基本功能，可根據內容控制中繼資料的顯示。

除了顯示套用內容中繼資料元件的索引標籤之外，若要在屬性頁面中顯示任何索引標籤，請從清單中選取索引標籤。 標籤會新增至屬性頁面。

### 指定JSON檔案中的屬性 {#specify-properties-in-json-file}

您不必在「設定」標籤中指定選項的屬 **[!UICONTROL 性]** ，而是可以透過指定對應的索引鍵值配對，來定義JSON檔案中的選項。在「 **[!UICONTROL JSON路徑」欄位中指定JSON檔案的]** 路徑。

#### 在結構表單中新增或刪除索引標籤 {#add-delete-a-tab-in-the-schema-form}

架構編輯器可讓您新增或刪除標籤。預設結構表單包括 **[!UICONTROL 基本]**， **[!UICONTROL 進階]** ， **[!UICONTROL IPTC]**、和 **[!UICONTROL IPTC延伸]** 索引標籤。

![中繼資料結構表單中的預設標籤](assets/metadata-schema-form-tabs.png)

按一下 `+` 在結構表單上新增索引標籤。 依預設，新標籤具有名稱 `Unnamed-1`. 您可以修改名稱，從 **[!UICONTROL 設定]** 標籤。 按一下 `X` 以刪除標籤。

![使用中繼資料結構編輯器新增或刪除索引標籤](assets/metadata-schema-form-new-tab.png)

## 刪除中繼資料結構表單 {#deleting-metadata-schema-forms}

Experience Manager僅可讓您刪除自訂結構表單。 它不允許您刪除預設的結構表單/範本。 不過，您可以刪除這些表單中的任何自訂變更。

若要刪除表單，請選取表單並按一下刪除圖示。

>[!NOTE]
>
>刪除預設表單的自訂變更後，在「中繼資料結構」介面中，鎖定圖示會在該表單之前重新出現，表示該表單已恢復為預設狀態。

>[!NOTE]
>
>* 刪除預設表單的自訂變更後，鎖定 ![鎖定已關閉](assets/do-not-localize/lock_closed_icon.svg) 會在表單前重新出現。 這表示表單已恢復為預設狀態。
>* 您無法刪除中的預設中繼資料結構表單 [!DNL Assets].

## MIME型別的結構表單 {#schema-forms-for-mime-types}

[!DNL Experience Manager] 為各種現成的MIME型別提供預設表單。 不過，您可以為各種MIME型別的資產新增自訂表單。

### 為MIME型別新增表單 {#adding-new-forms-for-mime-types}

在適當的表單型別下建立表單。 例如，若要為 `image/png` 子型別，在「影像」表單下建立表單。 方案表單的標題是子類型名稱。在此範例中，標題為 `png`.

#### 針對各種MIME型別使用現有結構描述範本 {#use-an-existing-schema-template-for-various-mime-types}

您可以將現有的範本用於不同的MIME型別。 例如，使用 `image/jpeg` MIME型別資產的表單 `image/png`.

在此情況下，請在以下位置建立節點： `/etc/dam/metadataeditor/mimetypemappings` 在CRX存放庫中。 指定節點名稱並定義下列屬性：

| 名稱 | 說明 | 類型 | 值 |
|------|-------------|------|-------|
| `exposedmimetype` | 要對應的現有表單名稱 | `String` | `image/jpeg` |
| `mimetypes` | 使用中定義之表單的MIME型別清單 `exposedmimetype` 屬性 | `String` | `image/png` |

[!DNL Assets] 對應下列MIME型別和結構表單：

| 結構表單 | MIME型別 |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi， video/msvideo， video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## 授予存取中繼資料結構的許可權 {#grant-access-to-metadata-schemas}

「中繼資料結構」功能僅供管理員使用。 但是，管理員可以修改部分許可權，以向非管理員提供存取權。 為非管理員使用者提供建立、修改和刪除許可權。 `/conf` 資料夾。

## 套用資料夾特定的中繼資料 {#applying-folder-specific-metadata}

[!DNL Assets] 可讓您定義中繼資料結構的變體，並將其套用至特定資料夾。

例如，您可以定義預設中繼資料結構的變體，並將其套用至資料夾。 當您套用修改後的結構描述時，它會覆寫套用至資料夾內資產的原始預設中繼資料結構描述。

只有上傳到套用此結構的資料夾的資產才符合變體中繼資料結構中定義的修改後中繼資料。 [!DNL Assets] 在套用原始結構描述的其他資料夾中，會繼續遵守原始結構描述中定義的中繼資料。

資產的中繼資料繼承是根據套用至階層中頂層資料夾的結構描述。 子資料夾會套用或繼承相同的結構描述。 如果在子資料夾層級套用不同的結構描述，繼承就會停止。

1. 在 [!DNL Experience Manager] 介面，瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**. 此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 選取表單前面的核取方塊（例如預設的中繼資料表單），然後按一下 **[!UICONTROL 複製]** 並儲存為自訂表格。 指定表單的自訂名稱，例如 `my_default`. 或者，您也可以建立自訂表格。

1. 在 **[!UICONTROL 中繼資料結構Forms]** 頁面，選取 `my_default` 表單，然後按一下 **[!UICONTROL 編輯]**.
1. 在 **[!UICONTROL 中繼資料結構編輯器]** 頁面，新增文字欄位至結構表單。 例如，新增含有標籤的欄位 **[!UICONTROL 類別]**.
1. 按一下「**[!UICONTROL 儲存]**」。修改後的表單會列在 **[!UICONTROL 中繼資料結構Forms]** 頁面。
1. 選取 **[!UICONTROL 套用至資料夾]** 將自訂中繼資料套用至資料夾。
1. 選取要套用修改後之結構描述的資料夾，然後選取 **[!UICONTROL 套用]**.
1. 如果資料夾套用了其他中繼資料結構，系統會顯示一則訊息，警告您即將覆寫現有的中繼資料結構。 按一下 **覆寫**.
1. 按一下 **確定** 以關閉成功訊息。
1. 導覽至您套用修改後中繼資料結構的資料夾。

## 定義強制中繼資料 {#defining-mandatory-metadata}

您可以在檔案夾層級定義強制欄位，這會強制上傳至檔案夾的資產執行。 如果您上傳缺少先前定義之必要欄位中繼資料的資產，卡片檢視的資產會顯示缺少中繼資料的視覺指示。

>[!NOTE]
>
>中繼資料欄位可以根據其他欄位的值定義為必填欄位。 在「卡片」檢視中，Experience Manager不會針對此類必要中繼資料欄位，顯示有關遺失中繼資料的警告訊息。

1. 按一下Experience Manager標誌，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**. 此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 將預設中繼資料表單儲存為自訂表單。 例如，儲存為 `my_default`.
1. 編輯自訂表格。 新增必要欄位。 例如，新增 **[!UICONTROL 類別]** 欄位，並將欄位設為必填。
1. 按一下「**[!UICONTROL 儲存]**」。修改後的表單會列在 **[!UICONTROL 中繼資料結構Forms]** 頁面。 選取表單，然後選取 **[!UICONTROL 套用至資料夾]** 將自訂中繼資料套用至資料夾。
1. 導覽至資料夾，然後上傳部分資產，其中遺失您新增至自訂表單之必要欄位的中繼資料。 資產的「卡片」檢視中會顯示訊息，指出必填欄位缺少中繼資料。
1. （選擇性）存取 `https://[server]:[port]/system/console/components/`. 設定並啟用 `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` 預設為停用的元件。 設定Experience Manager檢查資產中繼資料有效性的頻率。

   此設定會新增屬性 `hasValidMetadata` 至 `jcr:content` 個資產。 使用此屬性，Experience Manager可以篩選搜尋的結果。

   >[!NOTE]
   >
   >如果資產在排程檢查後新增，該資產不會使用 `hasValidMetadata` 直到下一次排定的檢查。 資產未出現在中繼搜尋結果中。

   >[!CAUTION]
   >
   >中繼資料驗證檢查需要大量資源，可能會影響系統效能。 相應地排程檢查。 如果伺服器無法應付負載，請嘗試停用此工作

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)