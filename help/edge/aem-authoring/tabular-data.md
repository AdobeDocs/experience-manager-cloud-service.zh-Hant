---
title: 使用試算表管理表格資料
description: 了解如何使用試算表管理各種值的表格資料，例如使用「使用 Edge Delivery Services 的 AEM」網站的中繼資料和重新導向。
feature: Edge Delivery Services
exl-id: 26d4db90-3e4b-4957-bf21-343c76322cdc
source-git-commit: 61d65c37d263edef641db42589fc0f28a8eb9078
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 100%

---


# 使用試算表管理表格資料 {#tabular-data}

了解如何使用試算表管理各種值的表格資料，例如「使用 Edge Delivery Services 的 AEM」網站的中繼資料和重新導向。

## 使用案例 {#use-cases}

任何「使用 Edge Delivery Services 的 AEM」網站都需要維護表格資料清單，例如鍵值對應清單。這些可以是許多不同值的清單，例如中繼資料和重新導向。Edge Deliver Services 可讓您使用直覺式工具來維護此類表格清單：試算表。AEM 將這些試算表轉換為 JSON 檔案，您的網站或 Web 應用程式可以輕鬆使用這些檔案。

常見使用案例包含：

* [預留位置](/help/edge/docs/placeholders.md)
* [中繼資料](/help/edge/docs/bulk-metadata.md)
* [標頭](/help/edge/docs/custom-headers.md)
* [重新導向](/help/edge/docs/redirects.md)
* [設定](/help/edge/docs/setup-byo-cdn-push-invalidation.md) 例如 CND 設定

此外，您可以[建立任何結構的試算表](#own-spreadsheet)，用來儲存以自己的目為主的對應。

本文件使用重新導向範例來說明如何建立此類試算表。有關每個用例的詳細信息，請參閱 Edge Delivery Services 文件中先前連結的主題。

>[!TIP]
>
>若要了解試算表一般如何與 Edge Delivery Services 配合使用的資訊，請參閱文件「[試算表和 JSON](/help/edge/developer/spreadsheets.md)」。

>[!TIP]
>
>試算表只能用來維護表格資料。若要儲存結構化資料，請查看「[AEM 的 Headless 功能](/help/headless/introduction.md)」。

## 先決條件 {#prerequisites}

為了在「使用 Edge Delivery Services 的 AEM」專案中使用試算表來建立應對，您需要使用最新的網站範本建立網站。

請參閱文件「[使用 Edge Delivery Services 進行 AEM 製作的開發人員入門指南](/help/edge/aem-authoring/edge-dev-getting-started.md)」，了解更多資訊。

## 建立試算表 {#spreadsheet}

在此範例中，您將建立一個試算表來管理「使用 Edge Delivery Services 的 AEM」網站的重新導向。相同的步驟適用於您想要建立的[其他試算表類型](#other) 。

1. 登入您的 AEM as a Cloud Service 製作執行個體，前往 **Sites** 控制台，然後導覽至需要試算表的網站根目錄。點選或按一下「**建立** -> **頁面**」。

   ![建立頁面](assets/tabular-data/tabular-data-create-page.png)

1. 在建立頁面精靈的「**範本**」標籤上，點選或按一下「**重新導向**」範本並選取，然後點選或按一下「**下一步**」。

   ![選取範本](assets/tabular-data/tabular-data-create-page-teamplate-redirects.png)

1. 精靈的「**屬性**」標籤顯示重新導向試算表的預設值。點選或按一下「**建立**」。

   * **標題** - 保留此值不變。
   * **欄** - 需要預先填入重新導向的最少欄。
      * **來源** - 要重新導向的頁面
      * **目的地** - 重新導向前往的頁面

   ![試算表的屬性](assets/tabular-data/tabular-data-create-page-properties-redirects.png)

1. 在「**成功**」對話框中，點選或按一下「**開啟**」。

   ![成功對話框](assets/tabular-data/tabular-data-success.png)

1. 新標籤開啟且有試算表載入編輯器中，其中包含預先定義的&#x200B;**來源**&#x200B;和&#x200B;**目的地**&#x200B;欄。若要定義您的重新導向，請點選或按一下&#x200B;**來源**&#x200B;欄的空白列。當您編輯試算表時，變更會自動儲存。

   ![編輯試算表](assets/tabular-data/tabular-data-edit-redirects.png)

   *  **來源**&#x200B;與您網站的網域相關，因來源僅包含相對路徑。
   * 如果您重新導向至其他網站， **目的地**&#x200B;可以是完全符合條件的 URL；如果您在自己的網站內重新導向，則目的地可以是相對路徑。
   * 使用 Tab 鍵將焦點移至下一個儲存格。
   * 編輯器會依需要在試算表新增資料列。
   * 若要刪除或移動列，請分別使用每列末端的「**刪除**」圖示和每列開頭的拖曳控點。

## 發佈試算表 paths.json {#paths-json}

為了讓 AEM 可以發佈試算表中的資料，您還需要更新專案的 `paths.json` 檔案。

1. 在 GitHub 中開啟專案的根目錄。

1. 點選或按一下 `paths.json` 檔案以開啟其詳細資訊，然後按一下「**編輯**」圖示。

   ![paths.json 檔案](assets/tabular-data/tabular-data-paths-json.png)

1. 新增一行以將新試算表對應到 `redirects.json` 資源。

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/redirects:/redirects.json"
     ]
   }
   ```

1. 按一下「**提交變更...**」，將變更儲存到 `main`。

   * 根據您的流程提交 `main` 或建立提取請求。

1. 當您定義完重新導向並更新路徑對應，返回 **Sites** 控制台。

1. 點選或按一下以選取您在控制台建立的重新導向試算表，然後點選或按一下操作列中的「**快速發佈**」以發佈試算表。

   ![在 Sites 控制台中選取試算表](assets/tabular-data/tabular-data-select-publish.png)

1. 在「**快速發佈**」對話框中，點選或按一下「**發佈**」。

   ![確認發佈](assets/tabular-data/tabular-data-quick-publish.png)

1. 橫幅會確認發佈。

   ![橫幅確認發佈](assets/tabular-data/tabular-data-publish-banner.png)

重新導向試算表現已發佈並可供大家存取。

## 其他試算表類型 {#other}

現在您已經知道如何建立重新導向試算表，您可以建立任何其他標準試算表類型：

* 預留位置
* 中繼資料
* 標頭
* 設定

只需按照「[建立試算表](#spreadsheet)」和「[更新 paths.json](#paths-json)」等節中的相同步驟進行，並選擇適當範本及相關的 `paths.json` 檔案。

對於 [設定](https://www.aem.live/docs/configuration)、[標頭](https://www.aem.live/docs/custom-headers) 和 [中繼資料](https://www.aem.live/docs/bulk-metadata)，確保新增對應以將其發佈到預設位置：

* 設定：`/.helix/config.json`
* 標頭：`/.helix/headers.json`
* 中繼資料：`/metadata.json`

此外，您還可以[建立自己的試算表](#own-spreadsheet)，以及供您自己使用的任意資料欄。

>[!NOTE]
>
>您無需建立試算表來管理「使用 Edge Delivery Services 的 AEM as a Cloud Service」專案的索引。
>
>如果您想建立自己的索引， [請依照此文件](https://www.aem.live/developer/indexing#setting-up-more-index-configurations)建立你自己的 `helix-query.yaml` 檔案。

## 建立您自己的試算表 {#own-spreadsheet}

1. 請按照後節中的相同步驟進行：[建立試算表。](#spreadsheet)

1. 選取範本時，要選擇「**試算表**」。

1. 在精靈的「**屬性**」標籤中，您可以新增自己的欄。

   ![新增您自己的欄](assets/tabular-data/tabular-data-own-spreadsheet.png)

   * 在「**欄**」區段中，點選或按一下「**新增**」以新增一個欄。
   * 請提供欄的名稱。
   * 請分別使用「**刪除**」來移除或重新整理欄，並且拖曳控點。

1. 請依照重新導向試算表的說明，建立試算表並發佈。

1. 請依照重新導向試算表的說明，將對應新增至 `paths.json` 檔案。
