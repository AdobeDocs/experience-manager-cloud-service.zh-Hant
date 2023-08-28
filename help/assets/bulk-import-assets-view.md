---
title: 使用「資產」檢視大量匯入資產
description: 瞭解如何使用新的資產UI （資產檢視）大量匯入資產。 它讓管理員能夠將資料來源的大量資產匯入AEM Assets。
source-git-commit: 49d1e002f22427d8ffc6c5bdecd054c10eac47b9
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 3%

---

# 使用「資產」檢視大量匯入資產  {#bulk-import-assets-view}

在AEM Assets檢視中大量匯入可讓管理員從資料來源將大量資產匯入至AEM Assets。 管理員不再需要將個別資產或資料夾上傳到AEM Assets。

您可以從下列資料來源匯入資產：

* Azure
* AWS
* Google Cloud
* Dropbox

## 先決條件 {#prerequisites}

| 資料來源 | 先決條件 |
|-----|------|
| Azure | <ul> <li>Azure 儲存體帳戶 </li> <li> Azure Blob 容器 <li> 根據驗證模式的Azure存取金鑰或SAS權杖 </li></ul> |
| AWS | <ul> <li>AWS地區 </li> <li> AWS 儲存貯體 <li> AWS 存取金鑰 </li><li> AWS 存取密碼 </li></ul> |
| Google Cloud | <ul> <li>GCP 貯體 </li> <li> GCP 服務帳戶電子郵件 <li> GCP 服務帳戶私密金鑰</li></ul> |
| Dropbox | <ul> <li>Dropbox使用者端ID </li> <li> Dropbox使用者端密碼</li></ul> |

除了這些以資料來源為基礎的先決條件外，您還必須知道資料來源中可用的來源資料夾名稱，該名稱包含需要匯入至AEM Assets的所有資產。

## 建立大量匯入設定 {#create-bulk-import-configuration}

執行以下步驟來建立大量匯入設定：

1. 瀏覽至 **[!UICONTROL 設定]** > **[!UICONTROL 大量匯入]** 並按一下 **[!UICONTROL 建立匯入]**.
1. 選取資料來源。 可用的選項包括Azure、AWS、Google Cloud和Dropbox。
1. 在中指定大量匯入組態的名稱 **[!UICONTROL 名稱]** 欄位。
1. 如中所述，指定資料來源特定認證 [必要條件](#prerequisites).
1. 提供根資料夾的名稱，該資料夾包含資料來源中的資產，位於 **[!UICONTROL 來源資料夾]** 欄位。
1. （可選）選取 **[!UICONTROL 匯入後刪除來源檔案]** 將檔案匯入Experience Manager Assets後，可從來源資料存放區中刪除原始檔案的選項。
1. 選取 **[!UICONTROL 匯入模式]**. 選取 **[!UICONTROL 略過]**， **[!UICONTROL 取代]**，或 **[!UICONTROL 建立版本]**. 略過模式為預設模式，在此模式中，擷取程式會略過以匯入資產（若已存在）。
   ![匯入來源詳細資料](assets/bulk-import-source-details.png)

1. （選用）在「中繼資料檔案」欄位中指定要匯入的中繼資料檔案（以CSV格式提供），然後按一下 **[!UICONTROL 下一個]** 導覽至 **[!UICONTROL 位置和篩選器]**.
1. 若要在DAM中定義要使用匯入資產的位置 **[!UICONTROL 資產目標資料夾]** 欄位中，指定路徑。 例如，`/content/dam/imported_assets`。
1. （選用）在 **[!UICONTROL 選擇篩選器]** 區段，提供資產的最小檔案大小（以MB為單位），以將其納入的擷取程式中 **[!UICONTROL 按最小大小篩選]** 欄位。
1. （選用）提供資產檔案大小上限（以MB為單位），以將其納入的擷取程式中 **[!UICONTROL 按最大大小篩選]** 欄位。
1. （可選）使用選取要包含在擷取流程中的MIME型別 **[!UICONTROL 包括MIME型別]** 欄位。 您可以在此欄位中選取多個MIME型別。 如果您未定義值，則所有MIME型別都會納入擷取程式中。

1. （選用）選擇要在擷取程式中排除的MIME型別，請使用 **[!UICONTROL 排除MIME型別]** 欄位。 您可以在此欄位中選取多個MIME型別。 如果您未定義值，則所有MIME型別都會納入擷取程式中。

   ![大量匯入篩選器](assets/bulk-import-location.png)

1. 按一下「**[!UICONTROL 下一步]**」。選取 **[!UICONTROL 儲存並執行匯入]** 以儲存組態並執行大量匯入。 選取 **[!UICONTROL 儲存匯入]** 儲存設定，以便稍後執行。

   ![執行大量匯入](assets/bulk-import-run.png)

1. 按一下 **[!UICONTROL 儲存]** 執行選取的選項。

## 檢視現有的大量匯入設定 {#view-import-configuration}

如果您在建立組態後選取儲存組態，組態會顯示在 **[!UICONTROL 儲存的匯入]** 標籤。

![儲存大量匯入設定](assets/bulk-import-save.png)

如果您選取儲存並執行匯入，則匯入組態會顯示在 **[!UICONTROL 已執行的匯入]** 標籤。

![儲存大量匯入設定](assets/bulk-import-executed.png)

如果您排程匯入，則它會顯示在 **[!UICONTROL 已排程的匯入]** 標籤。

## 編輯大量匯入設定 {#edit-import-configuration}

若要編輯設定詳細資料，請按一下與設定名稱相對應的…… ，然後按一下 **[!UICONTROL 編輯]**. 執行編輯操作時，您無法編輯設定和匯入資料來源的標題。 您可以使用「已執行」、「已排程」或「已儲存的匯入」標籤來編輯組態。

![編輯大量匯入設定](assets/bulk-import-edit.png)

## 排程一次性或週期性匯入 {#schedule-imports}

若要排程一次性或循環的大量匯入，請執行下列步驟：

1. 按一下……對應至中可用的設定名稱 **[!UICONTROL 已執行的匯入]** 或 **[!UICONTROL 儲存的匯入]** 標籤並按一下 **[!UICONTROL 排程]**. 您也可以導覽至「 」，重新排程現有的排程匯入 **[!UICONTROL 已排程的匯入]** 標籤並按一下 **[!UICONTROL 排程]**.

1. 設定一次性擷取或排程每小時、每日或每週排程。 按一下 **[!UICONTROL 提交]**.

   ![排程大量匯入設定](assets/bulk-import-schedule.png)

## 執行匯入健康狀態檢查 {#import-health-check}

若要驗證與資料來源的連線，請按一下與設定名稱相對應的…… ，然後按一下 **[!UICONTROL 檢查]**. 如果連線成功，Experience Manager Assets會顯示下列訊息：

![大量匯入健康狀態檢查](assets/bulk-import-health-check.png)

## 執行匯入前先執行試運行 {#dry-run-bulk-import}

按一下與設定名稱相對應的…… ，然後按一下 **[!UICONTROL 練習]** 以叫用大量匯入工作的測試回合。 Experience Manager Assets會顯示下列有關大量匯入工作的詳細資訊：

![大量匯入健康狀態檢查](assets/bulk-import-dry-run.png)

## 執行大量匯入 {#run-bulk-import}

如果您在建立設定時儲存匯入，您可以導覽至儲存的匯入標籤，按一下與設定相對應的……並按一下 **[!UICONTROL 執行]**.

同樣地，如果您需要執行已執行的匯入，請導覽至已執行的匯入索引標籤，按一下與設定名稱對應的……並按一下 **[!UICONTROL 執行]**.

## 停止或排程進行中的匯入 {#schedule-stop-ongoing-report}

在匯入期間，您可以使用「大量匯入」首頁上顯示的大量匯入狀態對話方塊，來排程或停止進行中的大量匯入。

![正在匯入](assets/bulk-import-progress.png)

您也可以按一下「 」，檢視已匯入目標資料夾中的資產 **[!UICONTROL 檢視資產]**.


## 刪除大量匯入設定 {#delete-bulk-import-configuration}

按一下……對應至中現有的設定名稱 **[!UICONTROL 已執行的匯入]**， **[!UICONTROL 已排程的匯入]**，或 **[!UICONTROL 儲存的匯入]** 標籤並按一下 **[!UICONTROL 刪除]** 刪除大量匯入組態。

## 執行大量匯入後，導覽至資產 {#view-assets-after-bulk-import}

若要檢視在執行大量匯入工作後匯入資產的資產目標位置，請按一下與設定名稱對應的…… ，然後按一下 **[!UICONTROL 檢視資產]**.

