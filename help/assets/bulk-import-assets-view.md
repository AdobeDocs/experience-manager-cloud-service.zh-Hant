---
title: 使用 Assets 檢視大量匯入資產
description: 了解如何使用新的 Assets UI (Assets 檢視) 大量匯入資產。此功能可讓管理員將大量資產從資料來源匯入到 AEM Assets。
exl-id: 10f9d679-7579-4650-9379-bc8287cb2ff1
source-git-commit: 88198e9333a7f706fc99e487d8cde84647fa111f
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 56%

---

# 使用 Assets 檢視大量匯入資產  {#bulk-import-assets-view}

AEM Assets 檢視中的大量匯入能讓管理員將大量資產從資料來源匯入到 AEM Assets。管理員不再需要將單個資產或資料夾上傳到 AEM Assets。

>[!NOTE]
>
>Assets 視圖大量匯入工具器使用的後端與管理員視圖大量匯入工具相同。 但是，它提供了更多可供匯入的資料來源和更簡化的使用者體驗。

您可以從以下資料來源匯入資產：

* Azure
* AWS
* Google 雲端
* Dropbox
* OneDrive

## 先決條件 {#prerequisites}

| 資料來源 | 先決條件 |
|-----|------|
| Azure | <ul> <li>Azure 儲存體帳戶 </li> <li> Azure Blob 容器 <li> 根據驗證模式的 Azure 存取金鑰或 SAS 權杖 </li></ul> |
| AWS | <ul> <li>AWS 區域 </li> <li> AWS 儲存貯體 <li> AWS 存取金鑰 </li><li> AWS 存取密碼 </li></ul> |
| Google 雲端 | <ul> <li>GCP 貯體 </li> <li> GCP 服務帳戶電子郵件 <li> GCP 服務帳戶私密金鑰</li></ul> |
| Dropbox | <ul> <li>Dropbox 用戶端 ID （應用程式鍵） </li> <li> Dropbox使用者端密碼（應用程式密碼）</li></ul> |
| OneDrive | <ul> <li>OneDrive租使用者ID  </li> <li> OneDrive使用者端ID</li><li> OneDrive使用者端密碼</li></ul> |

除了這些根據資料來源的先決條件之外，您也必須了解資料來源中可用的來源資料夾名稱，其中包含需要匯入到 AEM Assets 的所有資產。

## 設定Dropbox開發人員應用程式 {#dropbox-developer-application}

在將資產從您的Dropbox帳戶匯入至AEM Assets之前，請先建立和設定Dropbox開發人員應用程式。

執行以下步驟：

1. 登入您的 [Dropbox帳戶](https://www.dropbox.com/developers) 並按一下 **[!UICONTROL 建立應用程式]**.

1. 在 **[!UICONTROL 選擇API]** 區段中，選取唯一可用的選項按鈕。

1. 在 **[!UICONTROL 選擇您需要的存取型別]** 部分，選取下列其中一個選項：

   * 選取 **[!UICONTROL 應用程式資料夾]**，如果您需要存取在您Dropbox帳戶的應用程式中建立的單一資料夾。

   * 選取 **[!UICONTROL 完整Dropbox]**，以存取Dropbox帳戶內的所有檔案和資料夾。

1. 指定應用程式的名稱，然後按一下 **[!UICONTROL 建立應用程式]**.

1. 在 **[!UICONTROL 設定]** 標籤中，將以下專案新增至 **[!UICONTROL 重新導向URI]** 區段：

   * https://exc-unifiedcontent.experience.adobe.net

   * https://exc-unifiedcontent.experience-stage.adobe.net （僅適用於Stage環境）

1. 複製 **[!UICONTROL 應用程式金鑰]** 和 **[!UICONTROL 應用程式機密]** 欄位。 在AEM Assets中設定大量匯入工具時，需要這些值。

1. 在 **[!UICONTROL 許可權]** 索引標籤內，新增以下許可權 **[!UICONTROL 個別範圍]** 區段。

   * account_info.read

   * files.metadata.read

   * files.content.read

   * files.content.write

1. 按一下 **[!UICONTROL 提交]** 以儲存變更。

## 設定OneDrive開發人員應用程式 {#onedrive-developer-application}

從您的OneDrive帳戶匯入資產至AEM Assets之前，請先建立和設定OneDrive開發人員應用程式。

執行以下步驟：

1. 登入您的 [OneDrive帳戶](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) 並按一下 **[!UICONTROL 新註冊]**.

1. 指定應用程式的名稱，選取 **[!UICONTROL 僅此組織目錄中的帳戶(僅Adobe — 單一租使用者)]** 從 **[!UICONTROL 支援的帳戶型別]**，然後按一下 **[!UICONTROL 註冊]**. 已成功建立應用程式。

1. 複製應用程式使用者端ID和租使用者ID欄位的值。 在AEM Assets中設定大量匯入工具時，需要這些值。

1. 執行以下步驟以新增憑證：
   1. 在應用程式概觀頁面上，按一下 **[!UICONTROL 新增憑證或密碼]** 然後按一下 **[!UICONTROL 新使用者端密碼]**.
   1. 指定使用者端密碼描述和到期日，然後按一下 **[!UICONTROL 新增]**.
   1. 建立使用者端密碼後，複製 **[!UICONTROL 值]** 欄位（請勿複製密碼ID欄位）。 在AEM Assets中設定大量匯入時，這是必要作業。

1. 執行以下步驟以新增重新導向URI：
   1. 在應用程式概觀頁面上，按一下 **[!UICONTROL 新增重新導向URI]** > **[!UICONTROL 新增平台]** > **[!UICONTROL Web]**.
   1. 將下列專案新增至 **[!UICONTROL 重新導向URI]** 區段：

      * https://exc-unifiedcontent.experience.adobe.net

      * https://exc-unifiedcontent.experience-stage.adobe.net （僅適用於Stage環境）

      新增第一個URI並按一下 **[!UICONTROL 設定]** 以將其新增。 您可以按一下 **[!UICONTROL 新增URI]** 中可用的選項 **[!UICONTROL Web]** 區段於 **[!UICONTROL 驗證]** 頁面。

1. 執行以下步驟，為應用程式新增API許可權：
   1. 按一下 **[!UICONTROL API許可權]** 在左窗格中並按一下 **[!UICONTROL 新增許可權]**.
   1. 按一下 **[!UICONTROL Microsoft Graph]** > **[!UICONTROL 委派許可權]**. 此 **[!UICONTROL 選取許可權]** 區段會顯示可用的許可權。
   1. 選取 `offline_access` 許可權來自 `OpenId permissions` 和 `Files.ReadWrite.All` 許可權來自 `Files`.
   1. 按一下 **[!UICONTROL 新增許可權]** 以儲存更新。




## 建立大量匯入設定 {#create-bulk-import-configuration}

執行以下步驟以建立大量匯入設定：

1. 瀏覽到「**[!UICONTROL 設定]** > **[!UICONTROL 大量匯入]**」，並按一下「**[!UICONTROL 建立匯入]**」。
1. 選取資料來源。可用選項包括 Azure、AWS、Google 雲端和 Dropbox。
1. 在「**[!UICONTROL 名稱]**」欄位中為大量匯入設定指定名稱。
1. 指定資料來源特定的認證，如[先決條件](#prerequisites)中所述。
1. 提供資料夾的名稱，該資料夾包含資料來源中的資產。 **[!UICONTROL 來源資料夾]** 欄位。

   >[!NOTE]
   >
   >如果您使用Dropbox做為資料來源，請根據下列規則指定來源資料夾路徑：
   >* 如果您選取 **完整Dropbox** 建立Dropbox應用程式時，包含資產的資料夾位於 `https://www.dropbox.com/home/bulkimport-assets`，然後指定 `bulkimport-assets` 在 **[!UICONTROL 來源資料夾]** 欄位。
   >* 如果您選取 **應用程式資料夾** 建立Dropbox應用程式時，包含資產的資料夾位於 `https://www.dropbox.com/home/Apps/BulkImportAppFolderScope/bulkimport-assets`，然後指定 `bulkimport-assets` 在 **[!UICONTROL 來源資料夾]** 欄位，其中 `BulkImportAppFolderScope` 指應用程式的名稱。 `Apps` 之後自動新增 `home` 在此案例中。

1. (可選) 選取「**[!UICONTROL 匯入後刪除來源檔案]**」選項，在檔案匯入到 Experience Manager Assets 後，從來源資料存放區中刪除原始檔案。
1. 選取「**[!UICONTROL 匯入模式]**」。選取「**[!UICONTROL 跳過]**」、「**[!UICONTROL 取代]**」或「**[!UICONTROL 建立版本]**」。跳過模式是預設值，在此模式下，擷取工具會跳過匯入資產 (如果已存在)。
   ![匯入來源詳細資訊](/help/assets/assets/bulk-import-source-details.png)

1. (可選) 在中繼資料檔案欄位中指定要匯入的中繼資料檔案 (以 CSV 格式提供)，然後按一下「**[!UICONTROL 下一步]**」，瀏覽至「**[!UICONTROL 位置和篩選器]**」。
1. 要使用「**[!UICONTROL 資產目標資料夾]**」欄位在所要匯入資產的 DAM 中定義位置，請指定路徑。 例如，`/content/dam/imported_assets`。
1. (可選) 在「**[!UICONTROL 選擇篩選器]**」區段中，提供資產的檔案大小下限 (以 MB 為單位)，以便將它們包含在「**[!UICONTROL 按大小下限篩選]**」欄位中的擷取程序中。
1. (可選) 提供資產的檔案大小上限 (以 MB 為單位)，以納入「**[!UICONTROL 按大小上限篩選]**」欄位的擷取程序。
1. (可選) 使用「**[!UICONTROL 包含 MIME 類型]**」欄位選取要包含在擷取程序中的 MIME 類型。您可以在此欄位中選取多種 MIME 類型。如果您未定義值，則所有 MIME 類型都將包含在擷取程序中。

1. (可選) 使用「**[!UICONTROL 排除 MIME 類型]**」欄位選取要在擷取程序中排除的 MIME 類型。您可以在此欄位中選取多種 MIME 類型。如果您未定義值，則所有 MIME 類型都將包含在擷取程序中。

   ![大量匯入篩選器](assets/bulk-import-location.png)

1. 按一下「**[!UICONTROL 下一步]**」。選取「**[!UICONTROL 儲存並執行匯入]**」以儲存設定並執行大量匯入。選取「**[!UICONTROL 儲存匯入]**」暫時儲存設定，以便稍後執行。

   ![執行大量匯入](assets/bulk-import-run.png)

1. 按一下「**[!UICONTROL 儲存]**」執行所選選項。

### 大量匯入期間處理檔名 {#filename-handling-bulkimport-assets-view}

當您大量匯入資產或資料夾時，[!DNL Experience Manager Assets] 會匯入存在於匯入來源中的整個結構。 [!DNL Experience Manager] 會遵循資產和資料夾名稱中內建的特殊字元規則，因此這些檔名需要經過清理。 對於資料夾名稱和資產名稱，使用者定義的標題保持不變，並且儲存在 `jcr:title` 中。

在大量匯入期間，[!DNL Experience Manager] 會尋找現有資料夾以避免重複匯入資產和資料夾，並確認在發生匯入的父資料夾中已套用清理規則。 如果已在父資料夾中套用清理規則，則相同的規則也將套用於匯入來源。 對於新匯入，將套用以下清理規則來管理資產和資料夾的檔名。

如需大量匯入期間禁止的名稱、處理資產名稱和處理資料夾名稱的詳細資訊，請參閱[在管理員視圖中大量匯入期間處理檔名](add-assets.md##filename-handling-bulkimport)。

## 檢視現有的大量匯入設定 {#view-import-configuration}

如果您在建立設定後選擇儲存設定，則該設定會顯示在「**[!UICONTROL 已儲存的匯入]**」標籤中。

![儲存大量匯入設定](assets/bulk-import-save.png)

如果您選擇儲存並執行匯入，則匯入設定會顯示在「**[!UICONTROL 已執行的匯入]**」標籤中。

![儲存大量匯入設定](assets/bulk-import-executed.png)

如果您安排了匯入的排程，它會顯示在「**[!UICONTROL 已排定的匯入]**」標籤中。

## 編輯大量匯入設定 {#edit-import-configuration}

若要編輯組態詳細資訊，請按一下與組態名稱相對應的「更多選項(...)」，然後按一下 **[!UICONTROL 編輯]**. 執行編輯操作時無法編輯設定的標題和匯入資料來源。您可以使用「已執行」、「已排定」或「已儲存的匯入」標籤來編輯設定。

![編輯大量匯入設定](assets/bulk-import-edit.png)

## 安排單次或定期匯入的排程 {#schedule-imports}

要安排單次或定期大量匯入的排程，請執行以下步驟：

1. 按一下「更多選項(...)」(More Options (...))，其對應至 **[!UICONTROL 已執行的匯入]** 或 **[!UICONTROL 儲存的匯入]** 標籤並按一下 **[!UICONTROL 排程]**. 您也可以透過瀏覽到「**[!UICONTROL 已排定的匯入]**」標籤並按一下「**[!UICONTROL 排程]**」重新排程現有已排定的匯入。

1. 設定單次擷取或排定每小時、每天或每週排程。按一下「**[!UICONTROL 提交]**」。

   ![安排大量匯入設定的排程](assets/bulk-import-schedule.png)

## 執行匯入健康情況檢查 {#import-health-check}

若要驗證與資料來源的連線，請按一下與組態名稱相對應的[更多選項] (...)，然後按一下 **[!UICONTROL 檢查]**. 如果連線成功，Experience Manager Assets 會顯示以下訊息：

![大量匯入健全檢查](assets/bulk-import-health-check.png)

## 在執行匯入之前執行試執行 {#dry-run-bulk-import}

按一下與組態名稱相對應的「更多選項(...)」，然後按一下 **[!UICONTROL 練習]** 以叫用大量匯入工作的測試回合。 Experience Manager Assets 會顯示以下有關該大量匯入作業的詳細資訊：

![大量匯入健康情況檢查](assets/bulk-import-dry-run.png)

## 執行大量匯入 {#run-bulk-import}

如果您在建立組態時已儲存匯入，您可以瀏覽至「已儲存的匯入」標籤，按一下與組態相對應的「更多選項(...)」，然後按一下 **[!UICONTROL 執行]**.

同樣地，如果您需要執行已執行的匯入，請瀏覽至「已執行的匯入」標籤，按一下與組態名稱對應的「更多選項(...)」，然後按一下 **[!UICONTROL 執行]**.

## 停止或排程進行中的匯入 {#schedule-stop-ongoing-report}

您可以使用匯入期間，顯示在大量匯入首頁上的大量匯入狀態對話框進行排程或停止進行中的大量匯入。

![進行中的匯入](assets/bulk-import-progress.png)

您也可以透過按一下「**[!UICONTROL 檢視資產]**」檢視目標資料夾中已匯入的資產。


## 刪除大量匯入設定 {#delete-bulk-import-configuration}

按一下「更多選項(...)」(More Options (...))，這些選項與中現有的組態名稱相對應 **[!UICONTROL 已執行的匯入]**， **[!UICONTROL 已排程的匯入]**，或 **[!UICONTROL 儲存的匯入]** 標籤並按一下 **[!UICONTROL 刪除]** 刪除大量匯入組態。

## 執行大量匯入後瀏覽至資產 {#view-assets-after-bulk-import}

若要檢視執行「大量匯入」工作後匯入資產的「資產」目標位置，請按一下與組態名稱相對應的「更多選項(...)」，然後按一下 **[!UICONTROL 檢視資產]**.
