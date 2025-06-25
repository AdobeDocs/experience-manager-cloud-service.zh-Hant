---
title: ' [!DNL Workfront for Experience Manager enhanced connector] 版發行說明'
description: ' [!DNL Workfront for Experience Manager enhanced connector] 版發行說明'
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
feature: Release Information
role: Admin
source-git-commit: cb06380e4d3977f4f70a6444923cda2b0566d173
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 96%

---

# [!DNL Workfront for Experience Manager enhanced connector] 版發行說明 {#release-notes-enhanced-connector-workfront}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 與 Edge Delivery Services 整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

以下區段概述 [!DNL Workfront for Experience Manager enhanced connector] 的一般發行說明。

[!DNL Workfront for Experience Manager enhanced connector]的最新1.9.21版本的發行日期為2025年6月25日。

## 版本重點 {#release-highlights}

[!DNL Workfront for Experience Manager enhanced connector]的最新版本包含下列增強功能和錯誤修正：

* 改善API要求記錄，避免驗證失敗的誤判記錄。

* 修正Workfront API呼叫的連線洩漏問題。

* 支援適用於Java 17和Java 21版本的Workfront增強型聯結器與6.5 LTS。

>[!NOTE]
>
>AEM 6.4 的延伸支援已結束。請參閱我們的[技術支援期](https://helpx.adobe.com/tw/support/programs/eol-matrix.html)。請到[這裡](https://experienceleague.adobe.com/docs/?lang=zh-Hant)尋找支援的版本。

>[!IMPORTANT]
>
>Adobe 建議您[升級為 1.9.20 最新版本](/help/assets/workfront-connector-install.md)的 [!DNL Workfront for Experience Manager enhanced connector]。

## 已知問題 {#known-issues}

* 使用 AEM 6.4 設定專案連結的資料夾時，Experience Manager 並未儲存「**[!UICONTROL 子資料夾]**」和「**[!UICONTROL 在產品組合的專案中建立連結的資料夾]**」欄位的值。「**[!UICONTROL 子資料夾]**」欄位的值更新為&#x200B;**[!UICONTROL 未定義的]**，而「**[!UICONTROL 在產品組合的專案中建立連結的資料夾]**」欄位的值在儲存設定之後自動更新為&#x200B;**[!UICONTROL 預設產品組合]**。

* 在使用傳統 Workfront 體驗時，「**[!UICONTROL 更多]**」下拉式清單中的「**[!UICONTROL 傳送至]**」選項不允許您在 Experience Manager 之內選取目標目的地。使用「**[!UICONTROL 文件動作]**」下拉式清單時，「**[!UICONTROL 傳送至]**」選項正常運作。在使用新的 Workfront 體驗時，「**[!UICONTROL 更多]**」下拉式清單和「**[!UICONTROL 文件動作]**」下拉式清單的「**[!UICONTROL 傳送至]**」選項正常運作。

## 舊版本 {#previous-releases}

### 2024 年 9 月版 {#september-2024-release}

* 上傳和建立現有資產的新版本時，遺失 MIME 類型。

### 2024 年 4 月版 {#april-2024-release}

* 無法關閉 HTTP 用戶端會導致記憶體不足問題。


### 2024 年 3 月版 {#march-2024-release}

* 處理從 Workfront 上傳的多資產時遇到問題。
* 使用 Workfront 在 Experience Manager 搜尋資料夾時，不加入結束引號將會導致 `SERVER_ERROR`。

### 2024 年 2 月發行版本 {#february-2024-release}

* 啟用切換功能以允許 AEM Cloud 客戶配置和設定連接器。

* 在未明確關閉基礎工作階段的情況下關閉 `resourceResolver` 會導致 AEM 執行個體發生工作階段洩漏。明確關閉工作階段至關重要，因為自動關閉 Resource Resolver 不會隱含地關閉工作階段。

### 2024 年 1 月版 {#january-2024-release}

* [!DNL CRX DE] 中的 [!DNL Workfront] 設定目前不儲存 `project ID`，導致套用唯讀權限時發生錯誤。詳細了解如何[設定權限](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html#linked-folders)。

* 沒有關於如何將自訂屬性新增至開箱即用索引定義的公開文件。深入瞭解[新增自訂屬性](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html#metadata-schema-mapping)。

* 刪除增強型連接器上的連線設定會明顯影響事件訂閱和其他已儲存的設定，導致它們指向舊 URL。

* 安裝表單附加套件不會安裝&#x200B;**[!UICONTROL 切換路由器]**，導致 [!DNL WFEC AMS environment Toggle] 功能失敗。

* 在 EWC 設定上啟用事件訂閱會導致重複 API 呼叫失敗，並在第一次設定 [!DNL Workfront] 增強型連接器時出現 `HTTP 400` 錯誤。

* 在 Workfront 中刪除連結資料夾資源上的註釋無法在 AEM 上找到連結資料夾路徑。

* AEM 中對大檔案資源的支援不足會導致 4 位元組大小問題。

* 連結資料夾、文件更新和註釋更新中的關鍵流程無需請求時間處理。

### 2023 年 11 月版 {#nov-2023-release}

* 查看 AEM 檔案夾清單時，對話框需要超過一分鐘才能載入。
* 已獲授權的 [!DNL Workfront] 使用者正持續收到身份驗證失敗錯誤記錄。

### 2023 年 10 月版 {#october-2023-release}

* 當在「進階設定」下停用事件訂閱時，仍然可以選取以下選項：**訂閱文件更新事件以更新 AEM 資產中繼資料**、**在專案完成時將所有專案資產發佈到 Brand Portal**，以及&#x200B;**啟用註解同步**。

* 在 Workfront 中預覽時，無法正確轉譯 Experience Manager 所儲存的某些資產。

* 在重新設定 Experience Manager 與 Workfront 的連線時，未成功建立註解同步更新、刪除、文件更新等事件訂閱。

* 對於連結的資料夾建立、更新、啟用連結的資料夾、評論同步啟用和停用、進階設定保存於連接器上等主要 API 效能改善。

### 2023 年 9 月版 {#september-2023-release}

* Experience Manager 增強型連接器會從 Workfront 取得所有事件訂閱，同時刪除專案的事件訂閱，這會對應用程式的效能產生影響。

* 當資產從 Workfront 傳送到 Experience Manager 時，資產 MIME 類型未設定為 `dc:format`Experience Manager 中的屬性。

* Experience Manager 增強型連接器上儲存的 Workfront 專案 ID 包含重複項目。

### 2023 月 8 月版 {#august-2023-release}

* 無法在 Experience Manager 中建立連結的資料夾，因為沒有與所連結資料夾相關聯的使用者帳戶。

* Experience Manager 中資產的中繼資料更新期間的競爭狀況。

### 2023 年 6 月版 {#june-2023-release}

* 設定進階網路後，在將內容從 Adobe Workfront 傳送到 AEM as a Cloud Service 時會發生問題。


### 2023 年 5 月版 {#may-2023-release}

* Workfront 會根據從 Experience Manager 到 Workfront 的 REST 呼叫為重複事件訂閱傳回 409 HTTP 回覆，這會導致指標例外狀況。

### 2023 年 4 月版 {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector]2023 年 4 月 10 日發布的 1.9.9 版本包含以下更新：

* Experience Manager 在建立連結的資料夾期間從 Workfront 收到上次修改日期時顯示 DateTimeParseException  `DateTimeParseException`例外狀況。

* 在短時間內建立多個連結的專案資料夾時出現問題。

* 無法針對新的一組專案連結的資料夾數量設定臨界值限制。

### 2023 年 3 月版 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector]2023 年 3 月 3 日發布的 1.9.8 版本包含以下更新：

* Experience Manager 在 Workfront 中建立專案連結的資料夾時的效能得到改進。

* 在 Workfront 中刪除評論現在會反映在 Experience Manager 中。

* 能夠管理禁止 Experience Manager as a Cloud Service 的全新客戶設定連接器。

### 2023 年 1 月版 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]2023 年 2 月 2 日發布的 1.9.7 版本包含以下更新：

* 安裝 1.9.6 版本後，中繼資料編輯器不會列出 Workfront 自訂表單屬性。

* 在安裝 Workfront 增強型連接器並開啟資產首頁之後，開發控制台顯示`/content/dam/jcr:content/metadata/wfProjectURL not found`錯誤訊息。

### 2022 年 12 月版 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]12 月 9 日發布的 1.9.6 版本包含以下更新：

**增強功能**

<!--

* Workfront enhanced connector now lets you use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront 增強型連接器現在支援對資產和資料夾執行全文搜尋。

**錯誤修正**

* 文件版本中繼資料未在 Workfront 和 Experience Manager 之間適當第進行同步。
* 當資料夾使用的結構缺少在全域設定中的定義時，建立連結到 Workfront 之 Experience Manager 的資料夾時出現問題。
* 由於載入時間比預期還長，當您按一下任一欄位時，中繼資料結構編輯器表單會停止回應。為自訂表單已新增特定的 OSGi 設定以解決該問題。您新增到中繼資料結構編輯器的自訂表單的名稱可在紀錄中取得。

### 2022 年 11 月版 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]11 月 11 日發布的 1.9.5 版本包含以下更新：

* 在 Workfront 的多值欄位僅定義一個值時，該欄位值不會正確地對應到 Experience Manager。

* 在存取資產資料夾時，Experience Manager 顯示`SERVER_ERROR`於&#x200B;**[!UICONTROL 連結外部檔案和資料夾]**&#x200B;螢幕上 (因 `/content/dam/collections` 上的權限無效)。

* 在 Workfront 增強型連接器設定頁面上啟用「**[!UICONTROL 將資產發佈到 Brand Portal]**」的選項會建立不正確的事件。即使在停用該選項後，也不會刪除該事件。

  若要解決該問題：

   1. 升級到增強型連接器版本 1.9.5。

   1. 停用進階設定下的「**[!UICONTROL 將資產發佈到 Brand Portal]**」選項。

   1. 啟用「**[!UICONTROL 將資產發佈到 Brand Portal]**」選項。

   1. 刪除錯誤的事件訂閱。

      1. 執行 GET 呼叫 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         對每個頁碼執行一次 API 呼叫。

      1. 搜尋以下文字以尋找與以下 URL 相符但沒有 `objId` 的事件訂閱：

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         確保 `"objId": "",` 和 `"url"` 之間的內容符合 JSON 回應。建議的進行方法是從任何具有 `objId` 的事件訂閱進行複製，然後刪除該號碼。

      1. 記下該事件訂閱 ID。

      1. 刪除該錯誤的事件訂閱。進行刪除 API 呼叫 `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` 做為回應代碼表示成功刪除了錯誤的事件訂閱。
  >[!NOTE]
  >
  >如果您在執行此程序所述的步驟之前已經刪除了錯誤的事件訂閱，則可以跳過此程序的最後一步。

### 2022 年 10 月版 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]10 月 7 日發布的 1.9.4 版本包含以下更新：

* 由於許多事件，無法檢視增強型連接器設定頁面上的「事件訂閱」標籤。

* Workfront 無法擷取專案中現有資料夾的清單，這會導致建立重複的資料夾。

### 2022 年 9 月版 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]9 月 16 日發布的 1.9.3 版本包含以下更新：

* 無法上傳超過 8 GB 的檔案。
* 在自動發布從 Workfront 傳送到 AEM 的資產時出現問題。
* 在編輯預設中繼資料結構表單時，「根路徑」欄位無法用於「標籤」欄位。
* 在 Workfront 中使用 AEM 工作流程新增版本時出現問題。
* 當您對 Workfront 中可用的資產執行 AEM 搜尋時，AEM 顯示錯誤訊息。
* 在建立 AEM 工作流程以從資產建立任務且未定義父任務名稱時，該任務不會建立於 Workfront。

### 2022 年 8 月版 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]8 月 3 日發布的 1.9.2 版本包括以下更新：

* **[!UICONTROL 上傳文件]**&#x200B;工作流程步驟無法將文件附加到 Workfront。

* **[!UICONTROL 上傳文件]**&#x200B;工作流程步驟無法將文件附加到 Workfront 中的任務和問題。工作流程步驟已成功將文件附加到專案。

### 2022 年 7 月版 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]版本 1.9.1 包含以下更新：

* 對於遷移到 Adobe IMS 的執行個體，新增了使用 Workfront API 金鑰在 Experience Manager 和 Workfront 應用程式之間進行驗證的支援。

* 在連結外部檔案或資料夾時，Workfront 應用程式會顯示`SERVER_ERROR`錯誤訊息。該錯誤訊息指的是由於 API 密鑰不相符而導致未經授權的例外狀況。

* 在為資產執行建立任務工作流程時，日誌訊息中會顯示 Null 指標例外情況。

* 在啟用 Experience Manager 之「進階設定」下的 `Replace Spaces with DASH` 設定選項時，會造成在 Workfront 中建立重複的資料夾。

### 2022 年 6 月版 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包括以下更新：

* 在透過連結的資料夾上傳或使用 Workfront 中可用的 `Send To` 操作將資產上傳到 Experience Manager as a Cloud Service 時，資產會損壞且無法在 Adobe Photoshop 中開啟。

### 2022 年 3 月版 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包括以下更新：

* 現在，即使有多個專案連結的資料夾設定，您也可以在 Adobe Workfront 和 AEM Assets as a Cloud Service 之間建立連結的資料夾。

* 新增了對事件訂閱分頁的支援。

* 新增了對 AEM 6.4.x 的支援。

* 新增了對 Proxy 環境的支援。

* 根據合作夥伴和客戶意見回應進行的許多錯誤修正。

>[!MORELIKETHIS]
>
>* [整合  [!DNL Workfront for Experience Manager enhanced connector]  與 Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=zh-Hant)
