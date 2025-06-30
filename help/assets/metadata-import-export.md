---
title: 大量匯入和匯出資產的中繼資料
description: 本文會說明如何大量匯入和匯出中繼資料。
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: fb70a068-3ba3-4459-952d-79155d286c42
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 10%

---

# 大量匯入和匯出資產的中繼資料 {#import-and-export-asset-metadata-in-bulk}

Adobe Experience Manager Assets可讓您使用CSV檔案大量匯入資產中繼資料。 您可以匯入CSV檔案，大量更新最近上傳的資產或現有資產。 您也可以以CSV格式從協力廠商系統大量擷取資產中繼資料。

## 匯入中繼資料 {#import-metadata}

中繼資料的匯入為非同步處理，不會阻礙系統效能。 因為使用資產微服務的中繼資料回寫活動，所以同時更新多個資產的中繼資料可能會耗費大量資源。 Adobe建議您在使用精簡伺服器期間計畫任何大量作業，以免影響其他使用者的效能。

>[!NOTE]
>
>若要在自訂名稱空間上匯入中繼資料，請先註冊名稱空間。

1. 導覽至[!DNL Assets]使用者介面，從工具列選取&#x200B;**[!UICONTROL 建立]**，然後從功能表選取&#x200B;**[!UICONTROL 中繼資料]**。
1. 在&#x200B;**[!UICONTROL 中繼資料匯入]**&#x200B;頁面中，按一下&#x200B;**[!UICONTROL 選取檔案]**。 選取包含中繼資料的CSV檔案。
1. 提供下列引數：

   | 參數 | 說明 |
   | ---------------------- | ------- |
   | 批次大小 | 批次中要匯入中繼資料的資產數量。 預設值為 50。最大值為100。 |
   | 欄位分隔符號 | 預設值為`,` （逗號）。 您可以指定任何其他字元。 |
   | 多值分隔符號 | 中繼資料值的分隔符號。 預設值為`|`。 |
   | 啟動工作流程 | 預設為False。 設為`true`時，預設設定對DAM中繼資料WriteBack工作流程(將中繼資料寫入二進位XMP資料)有效。 啟用工作流程會拖慢系統速度。 |
   | 資產路徑欄名稱 | 為含有資產的CSV檔案定義欄名稱。 |

1. 從工具列選取&#x200B;**[!UICONTROL 匯入]**。 匯入中繼資料後，系統會將通知傳送至您的「通知」收件匣。 導覽至資產屬性頁面，並確認是否正確匯入資產的中繼資料值。

1. 若要新增日期與時間戳記以匯入中繼資料，請使用`YYYY-MM-DDThh:mm:ss.fff-00:00`格式的日期與時間。 日期和時間以`T`分隔，`hh`是24小時格式的小時，`fff`是nanoseconds，而`-00:00`是時區位移。 例如，`2020-03-26T11:26:00.000-07:00`是2020年3月26日上午11:26:00:000 （太平洋標準時間）。

   * 日期格式取決於欄標題及其中的格式。 例如，如果日期為格式`yyyy-MM-dd'T'HH:mm:ssXXX`的投訴，則個別欄標題必須為`Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`。
   * 預設日期格式為`yyyy-MM-dd'T'HH:mm:ss.SSSXXX`。

<!-- Hidden via cqdoc-17869>

>[!CAUTION]
>
>If the date format does not match `YYYY-MM-DDThh:mm:ss.fff-00:00`, the date values are not set. The date formats of exported metadata CSV file is in the format `YYYY-MM-DDThh:mm:ss-00:00`. If you want to import it, convert it to the acceptable format by adding the nanoseconds value denoted by `fff`.
-->

## 匯出中繼資料 {#export-metadata}

您可以以CSV格式匯出多個資產的中繼資料。 中繼資料會以非同步方式匯出，不會影響系統效能。 若要匯出中繼資料，Experience Manager會周游資產節點`jcr:content/metadata`及其子節點的屬性，並將中繼資料屬性匯出為CSV檔案。

大量匯出中繼資料的一些使用案例包括：

* 移轉資產時，在第三方系統中匯入中繼資料。
* 與更廣大的專案團隊共用資產中繼資料。
* 測試或稽核中繼資料是否合規。
* 將中繼資料外部化，以利個別本地化。

>[!NOTE]
>
>中繼資料匯出限制在1,048,575 Assets，這對應於Microsoft Excel中的工作表大小上限。 如果匯出的階層包含超過此數量的Assets，則CSV檔案中只會包含前1,048,575個Assets的中繼資料。

1. 選取包含您要匯出中繼資料之資產的資產資料夾。 從工具列中選取&#x200B;**[!UICONTROL 匯出中繼資料]**。
1. 在「中繼資料匯出」對話方塊中，指定CSV檔案的名稱。 若要匯出子資料夾中資產的中繼資料，請選取&#x200B;**[!UICONTROL 包含子資料夾中的資產]**。

   ![匯出資料夾中所有資產中繼資料的介面和選項](assets/export_metadata_page.png "匯出資料夾中所有資產中繼資料的介面和選項")

1. 選取所需的選項。 提供檔案名稱，並視需要提供日期。

1. 在&#x200B;**[!UICONTROL 要匯出的屬性]**&#x200B;欄位中，指定您是要匯出所有屬性還是特定屬性。 如果您選擇要匯出的「選擇性」屬性，請新增所需的屬性。

1. 從工具列中選取&#x200B;**[!UICONTROL 匯出]**。 系統會顯示訊息，確認中繼資料已匯出。 關閉訊息。
1. 開啟導出作業的收件箱通知。選擇作業，然後從工具 **[!UICONTROL 欄中]** ，按一下「開啟」。若要下載含有中繼資料的CSV檔案，請從工具列選取&#x200B;**[!UICONTROL CSV下載]**。 按一下&#x200B;**[!UICONTROL 關閉]**。

   ![用於下載包含大量匯出之中繼資料的CSV檔案的對話方塊](assets/csv_download.png)

   *圖：用於下載包含大量匯出之中繼資料的CSV檔案的對話方塊。*

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
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* 大量匯入資產時[匯入中繼資料](/help/assets/add-assets.md#asset-bulk-ingestor)
