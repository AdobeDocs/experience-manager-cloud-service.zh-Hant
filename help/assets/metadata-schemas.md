---
title: 中繼資料結構定義中繼資料屬性頁面的配置
description: 中繼資料結構定義屬性頁面的版面配置，以及為資產顯示的中繼資料屬性。 瞭解如何建立自訂中繼資料結構、編輯中繼資料結構，以及如何將中繼資料結構套用至資產。
contentOwner: AG
feature: 中繼資料
role: Business Practitioner,Administrator
exl-id: 9e94afeb-1c54-4653-bf52-b0910c0cb6c1
translation-type: tm+mt
source-git-commit: 855b8b1de11e5f986948d3144104d6b5226c2dd5
workflow-type: tm+mt
source-wordcount: '2567'
ht-degree: 9%

---

# 中繼資料結構{#metadata-schemas}

企業組織會提供中繼資料模型，以增強資產發現、使用、互操作性等。 正確的中繼資料應用程式是神聖不可侵犯的，可維持中繼資料導向的工作流程和程式。 為符合整個組織的中繼資料策略和標準，您可以使用中繼資料結構，協助DAM使用者對齊。 [!DNL Adobe Experience Manager] 可讓您以簡單而有彈性的方式建立、維護和套用中繼資料結構。

在[!DNL Adobe Experience Manager Assets]中，結構包含要填充的特定資訊的特定欄位。 它也包含版面資訊，以方便使用者的方式顯示中繼資料欄位。 中繼資料屬性包括標題、說明、MIME類型、標籤等。 您可以使用[!UICONTROL 中繼資料結構Forms]編輯器修改現有結構或新增自訂中繼資料結構。

若要檢視和編輯資產的屬性頁面，請依照下列步驟進行：

1. 在卡片檢視中，按一下資產圖格上的快速動作中的「檢視屬性」選項。 ****&#x200B;或者，選擇資產，然後從工具列按一下「屬性&#x200B;**** ![檢視屬性](assets/do-not-localize/info-circle-icon.png)」。

1. 您可以編輯可用標籤下的各種可編輯中繼資料屬性。 但是，您不能修改屬性頁面的[!UICONTROL Basic]標籤中的[!UICONTROL Type]資產。

   ![資產屬性的「基本」標籤，其中無法變更資產類型](assets/asset-properties-basic-tab.png)

   *圖：資產屬性上的「基 [!UICONTROL 本」標籤]。*

   若要修改資產的MIME類型，請使用自訂中繼資料結構表單或修改現有表單。 如需詳細資訊，請參閱[編輯中繼資料結構Forms](#edit-metadata-schema-forms)。 如果您修改MIME類型的中繼資料結構，資產和所有子類型的屬性頁面配置都會被修改。 例如，在`default/image`下修改jpeg架構只會修改MIME類型`image/jpeg`的資產的中繼資料配置（資產屬性）。 不過，如果您編輯預設結構，您的變更會修改所有類型資產的中繼資料配置。

## 中繼資料結構表單{#default-metadata-schema-forms}

若要檢視表單或範本清單，請在[!DNL Experience Manager]介面中導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**。

[!DNL Experience Manager] 提供了以下元資料架構表單模板。

| 範本 |  | 說明 |
|---|---|---|
| [!UICONTROL 預設] |  | 資產的基本中繼資料結構表單。 |
|  | 以下子表單繼承[!UICONTROL default]表單的屬性： |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Dynamic Media影片的架構表單。 |
|  | <ul><li>[!UICONTROL 影像]</li></ul> | 具有`image/jpeg`和`image/png`等MIME類型的映像的架構表單。 <br> 影像  表單包含下列子表單範本： <ul><li> [!UICONTROL jpeg]:子類型 [!UICONTROL jpeg資產的架構表單]。</li> <li>[!UICONTROL tiff]:子類型為TIFF的資產的架構表單。</li></ul> |
|  | <ul><li>[!UICONTROL 應用程式]</li></ul> | 具有`application/pdf`和`application/zip`等MIME類型的資產的架構表單。 <br>[!UICONTROL pdf]:子類型為PDF的資產的架構表單。 |
|  | <ul><li>[!UICONTROL 視訊]</li></ul> | 具有MIME類型（例如`video/avi`和`video/mp4`）的視訊資產的架構表單。 |
| [!UICONTROL 集合] |  | 系列的結構表單。 |
| [!UICONTROL contentfragment] |  | 內容片段的架構表單。 |
| [!UICONTROL 表單] |  | 此模式表單與[!DNL Adobe Experience Manager Forms]相關。 |
| [!UICONTROL ugc_contentfragment] |  | 使用者產生的內容片段與資產的架構表單，整合在來自社交媒體的Experience Manager中。 |

>[!NOTE]
>
>要查看方案表單的子表單，請按一下方案表單名稱。

## 添加元資料架構表單{#add-a-metadata-schema-form}

要添加元資料結構表單，請執行以下步驟：

1. 若要將自訂範本新增至清單，請從工具列按一下「建立&#x200B;**[!UICONTROL 」。]**

   >[!NOTE]
   >
   >鎖定符號與未編輯的模板一起顯示。 如果自定義模板，則不鎖定![lock closed](assets/do-not-localize/lock_closed_icon.svg)。

1. 在對話框中，提供模式表單的標題，然後按一下&#x200B;**[!UICONTROL 建立]**&#x200B;以完成表單建立過程。

## 編輯元資料架構表單{#edit-metadata-schema-forms}

您可以編輯新增或現有的中繼資料結構表單。 中繼資料結構表單包含標籤和標籤內的表單項目。 您可以將這些表單項目映射／配置到CRX儲存庫中元資料節點中的欄位。 您可以將標籤或表單項目新增至中繼資料結構表單。 衍生自父項的制表符和表單項處於鎖定狀態。 您無法在子級更改它們。

1. 在[!UICONTROL 中繼資料結構Forms]頁面上，選取表單，然後按一下工具列中的&#x200B;**[!UICONTROL 編輯]**。

1. 在&#x200B;**[!UICONTROL 中繼資料結構表單編輯器]**&#x200B;頁面上，自訂中繼資料表單。 將所需的元件從&#x200B;**[!UICONTROL Build Form]**&#x200B;頁籤拖到其中一個頁籤上。

   ![「元資料結構編輯器：自定義資產屬性」頁](assets/metadata-schema-editor.png)

   *圖：「元數 [!UICONTROL 據結構表單編] 輯器」頁，帶有可用頁籤。*

1. 要配置元件，請選擇該元件並在&#x200B;**[!UICONTROL Settings]**&#x200B;頁籤中修改其屬性。

### [!UICONTROL Build Form]標籤{#components-within-the-build-form-tab}中的元件

**[!UICONTROL 建置表單]**&#x200B;頁籤列出了在架構表單中使用的表單項。 **[!UICONTROL Settings]**&#x200B;標籤提供您在&#x200B;**[!UICONTROL Build Form]**&#x200B;標籤中選擇的每個項目的屬性。 下表列出了&#x200B;**[!UICONTROL Build Form]**&#x200B;頁籤中可用的表單項：

| 元件名稱 | 說明 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 區段標題] | 新增共用元件清單的區段標題。 |
| [!UICONTROL 單行文字] | 新增單行文字屬性。 它儲存為字串。 |
| [!UICONTROL 多值文字] | 新增多值文字屬性。 它儲存為字串陣列。 |
| [!UICONTROL 數量] | 添加數字元件。 |
| [!UICONTROL 日期] | 新增日期元件。 |
| [!UICONTROL 下拉式] | 新增下拉式清單。 |
| [!UICONTROL 標準標記] | 新增標記. |
| [!UICONTROL 智慧標記] | 自動新增中繼資料標籤，以增強搜尋功能。 |
| [!UICONTROL 隱藏欄位] | 新增隱藏欄位。 儲存資產時，會以POST參數傳送。 |
| [!UICONTROL 資產引用者] | 新增此元件以檢視資產參考的資產清單。 |
| [!UICONTROL 資產引用] | 新增以顯示參考資產的資產清單。 |
| [!UICONTROL 產品參考] | 新增以顯示與資產連結的產品清單。 |
| [!UICONTROL 資產評等] | 新增至顯示選項，以評分資產。 |
| [!UICONTROL 關聯式中繼資料] | 新增以控制資產屬性頁面中其他中繼資料標籤的顯示。 |

#### 編輯元資料元件{#edit-the-metadata-component}

要編輯表單上元資料元件的屬性，請按一下該元件以編輯&#x200B;**[!UICONTROL Settings]**&#x200B;頁籤中以下全部或子集的屬性。

**欄位標籤**:顯示在資產屬性頁面上的中繼資料屬性名稱。

**對應至屬性**:此屬性指定資產節點的相對路徑或名稱，該資產節點保存在CRX儲存庫中。它以`./`開頭，表示路徑位於資產節點下。

以下是此屬性的有效值：

* `./jcr:content/metadata/dc:title`:將值儲存在資產的中繼資料節點，做為屬性 `dc:title`。

* `./jcr:created`:儲存資產的建立日期和時間。它是受保護的屬性。 如果您設定這些屬性，Adobe建議您將它們標示為「停用編輯」。 否則，當您儲存資產的屬性時，會出現「資產無法修改」錯誤。

為確保元資料架構表單中的元件正確顯示，屬性路徑不應包含任何空格。

* **預留位置**:使用此屬性可指定與中繼資料屬性相關的預留位置文字。
* **必要**:使用此屬性可將中繼資料屬性標示為屬性頁面上的必要屬性。
* **停用編輯**:使用此屬性可禁止對屬性頁面上的屬性進行任何編輯。
* **在唯讀中顯示空白欄位**:標籤此屬性，即使其沒有值，也可在屬性頁面上顯示中繼資料屬性。預設情況下，當中繼資料屬性沒有值時，該屬性不會列在屬性頁面上。
* **顯示順序清單**:使用此屬性可顯示選擇的有序清單。
* **選擇**:使用此屬性可指定清單中的選擇。
* **說明** :使用此屬性可為中繼資料元件新增簡短說明。
* **類別**:屬性與關聯的對象類。
* **刪除**:按一下  刪除可從架構表單中刪除元件。

>[!NOTE]
>
>[!UICONTROL 隱藏欄位]元件不包含這些屬性。 而是包含屬性，例如屬性名稱、值、欄位標籤和說明。 每當儲存資產時，「隱藏欄位」元件的值都會以POST參數傳送。 它不會儲存為資產的中繼資料。

如果您選取「必 **[!UICONTROL 要]** 」選項，可以搜尋遺失必要中繼資料的資產。從「篩 **[!UICONTROL 選器]** 」面板中，展開「中繼資料 **[!UICONTROL 驗證謂語]** 」並選取「 **[!UICONTROL 無效]** 」選項。搜尋結果會顯示遺失您透過結構表單設定之必要中繼資料的資產。

如果將上下文元資料元件添加到任何方案表單的任何頁籤，則該元件將作為清單顯示在應用特定方案的資產的屬性頁中。 該清單包括除應用上下文元資料元件的頁籤之外的所有其他頁籤。 目前，此功能提供基本功能，可根據內容控制中繼資料的顯示。

要顯示屬性頁面中除了應用上下文元資料元件的頁籤之外的任何頁籤，請從清單中選擇該頁籤。 該頁籤將添加到屬性頁。

### 在JSON檔案{#specify-properties-in-json-file}中指定屬性

您不必在「設定」標籤中指定選項的屬 **[!UICONTROL 性]** ，而是可以透過指定對應的索引鍵值配對，來定義JSON檔案中的選項。在「 **[!UICONTROL JSON路徑」欄位中指定JSON檔案的]** 路徑。

#### 在架構表單{#add-delete-a-tab-in-the-schema-form}中添加或刪除頁籤

架構編輯器可讓您新增或刪除標籤。預設模式表單包括&#x200B;**[!UICONTROL Basic]**、**[!UICONTROL Advanced]**、**[!UICONTROL IPTC]**&#x200B;和&#x200B;**[!UICONTROL IPTC Extension]**&#x200B;標籤。

![中繼資料結構表單中的預設標籤](assets/metadata-schema-form-tabs.png)

按一下`+`在模式表單上添加頁籤。 預設情況下，新頁籤的名稱為`Unnamed-1`。 您可以從&#x200B;**[!UICONTROL Settings]**&#x200B;標籤中修改名稱。 按一下`X`刪除頁籤。

![使用中繼資料結構編輯器新增或刪除標籤](assets/metadata-schema-form-new-tab.png)

## 刪除元資料架構表單{#deleting-metadata-schema-forms}

可AEM讓您僅刪除自訂結構表單。 它不允許您刪除預設模式表單／模板。 不過，您可以刪除這些表單中的任何自訂變更。

要刪除表單，請選擇一個表單並按一下刪除表徵圖。

>[!NOTE]
>
>刪除對預設表單的自定義更改後，鎖定表徵圖會重新顯示在元資料架構介面的前面，以指示表單恢復為預設狀態。

>[!NOTE]
>
>* 刪除對預設表單的自定義更改後，在表單前會重新顯示鎖定![clock closed](assets/do-not-localize/lock_closed_icon.svg)。 它表示表單已回復為預設狀態。
>* 您無法刪除[!DNL Assets]中的預設元資料架構表單。


## MIME類型{#schema-forms-for-mime-types}的架構表單

[!DNL Experience Manager] 為各種現成可用的MIME類型提供預設表單。不過，您可以為各種MIME類型的資產新增自訂表格。

### 為MIME類型{#adding-new-forms-for-mime-types}添加新表單

在適當的表單類型下建立表單。 例如，要為`image/png`子類型添加模板，請在&quot;image&quot;表單下建立表單。 方案表單的標題是子類型名稱。在本例中，標題為`png`。

#### 對各種MIME類型{#use-an-existing-schema-template-for-various-mime-types}使用現有模式模板

您可以針對不同的MIME類型使用現有範本。 例如，對於MIME類型`image/png`的資產，請使用`image/jpeg`表格。

在這種情況下，請在CRX儲存庫的`/etc/dam/metadataeditor/mimetypemappings`處建立一個節點。 指定節點的名稱並定義以下屬性：

| 名稱 | 說明 | 類型 | 值 |
|------|-------------|------|-------|
| `exposedmimetype` | 要映射的現有表單的名稱 | `String` | `image/jpeg` |
| `mimetypes` | 使用`exposedmimetype`屬性中定義的表單的MIME類型清單 | `String` | `image/png` |

[!DNL Assets] 映射以下MIME類型和模式表單：

| 架構表單 | MIME類型 |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | 視訊/avi，視訊/msvideo，視訊/x-msvideo |
| video/wmv | video/x-ms-wmv |
| 視訊/flv | video/x-flv |

## 授予對元資料結構{#grant-access-to-metadata-schemas}的訪問權

「中繼資料結構」功能僅供管理員使用。 不過，管理員可修改某些權限，以提供非管理員的存取權。 為非管理員用戶提供對`/conf`資料夾的建立、修改和刪除權限。

## 套用資料夾特定的中繼資料{#applying-folder-specific-metadata}

[!DNL Assets] 可讓您定義中繼資料結構的變體，並將其套用至特定資料夾。

例如，您可以定義預設中繼資料結構的變體，並將其套用至資料夾。 當您套用已修改的架構時，它會覆寫套用至資料夾內資產的原始預設中繼資料架構。

只有上傳至套用此架構的資料夾的資產，才符合變型中繼資料架構中定義的已修改中繼資料。 [!DNL Assets] 在應用原始模式的其他資料夾中，繼續與原始模式中定義的元資料保持一致。

資產的中繼資料繼承是根據套用至階層中頂層檔案夾的架構。 子檔案夾會套用或繼承相同的架構。 如果在子資料夾級別應用了不同的方案，繼承將停止。

1. 在[!DNL Experience Manager]介面中，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**。 此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 選取表單前的核取方塊，例如預設中繼資料表單，然後按一下&#x200B;**[!UICONTROL Copy]**&#x200B;並儲存為自訂表單。 指定表單的自訂名稱，例如`my_default`。 或者，您也可以建立自訂表格。

1. 在&#x200B;**[!UICONTROL 中繼資料結構Forms]**&#x200B;頁面中，選擇`my_default`表單，然後按一下&#x200B;**[!UICONTROL 編輯]**。
1. 在&#x200B;**[!UICONTROL 中繼資料結構編輯器]**&#x200B;頁面中，將文字欄位新增至結構結構表單。 例如，新增標籤為&#x200B;**[!UICONTROL Category]**&#x200B;的欄位。
1. 按一下「**[!UICONTROL 儲存]**」。修改的表單列在&#x200B;**[!UICONTROL 中繼資料結構Forms]**&#x200B;頁面中。
1. 從工具列按一下／點選「套用至資料夾&#x200B;****」，將自訂中繼資料套用至資料夾。
1. 選擇要在其上應用已修改模式的資料夾，然後按一下／點選&#x200B;**[!UICONTROL Apply]**。
1. 如果資料夾已套用其他中繼資料結構，會出現警告訊息，指出您即將覆寫現有的中繼資料結構。 按一下&#x200B;**覆寫**。
1. 按一下&#x200B;**確定**&#x200B;關閉成功消息。
1. 導覽至您套用已修改中繼資料結構的資料夾。

## 定義強制元資料{#defining-mandatory-metadata}

您可以在資料夾層級定義必要欄位，並強制執行在上傳至資料夾的資產上。 如果您上傳資產時，先前定義之必填欄位的中繼資料遺失，則「卡片」檢視中的資產上會顯示遺失中繼資料的視覺指示。

>[!NOTE]
>
>中繼資料欄位可根據其他欄位的值，定義為必填欄位。 在「卡片」檢視中，不AEM會顯示此類強制中繼資料欄位遺失中繼資料的警告訊息。

1. 按一下 AEM 標誌，然後導覽至&#x200B;**[!UICONTROL 「工具」]**>**[!UICONTROL 「資產」]**>**[!UICONTROL 「中繼資料結構描述」]**。此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 將預設中繼資料表單儲存為自訂表單。 例如，將其另存為`my_default`。
1. 編輯自訂表格。 新增必填欄位。 例如，新增&#x200B;**[!UICONTROL Category]**&#x200B;欄位，並將欄位設為必填。
1. 按一下「**[!UICONTROL 儲存]**」。修改的表單列在&#x200B;**[!UICONTROL 中繼資料結構Forms]**&#x200B;頁面中。 選擇表單，然後從工具列按一下或點選「套用至資料夾&#x200B;****」，將自訂中繼資料套用至資料夾。
1. 導覽至資料夾，並上傳您新增至自訂表單之必填欄位中遺失中繼資料的部分資產。 資產的「卡片」檢視中會顯示必要欄位遺失中繼資料的訊息。
1. （可選）訪問`https://[server]:[port]/system/console/components/`。 配置並啟用預設禁用的`com.day.cq.dam.core.impl.MissingMetadataNotificationJob`元件。 設定檢查資AEM產中繼資料有效性的頻率。

   此配置將`hasValidMetadata`屬性添加到`jcr:content`資產中。 使用此屬性，AEM可以篩選搜尋結果。

   >[!NOTE]
   >
   >如果在排程檢查後新增資產，則資產在下次排程檢查前不會標幟為`hasValidMetadata`。 資產不會出現在中間搜尋結果中。

   >[!CAUTION]
   >
   >中繼資料驗證檢查需要耗費大量資源，而且可能會影響您系統的效能。 相應地安排檢查。 如果伺服器無法處理載入，請嘗試禁用此作業
