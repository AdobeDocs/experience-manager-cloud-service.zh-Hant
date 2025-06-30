---
title: 適用於  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的資產選擇器
description: 在應用程式內使用資產選擇器進行搜尋、尋找和取得資產的中繼資料與轉譯。
role: Admin, User
exl-id: 62b0b857-068f-45b7-9018-9c59fde01dc3
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 100%

---

# 微前端資產選擇器 {#Overview}

微前端資產選擇器提供一個輕鬆整合 [!DNL Experience Manager Assets] 存放庫的使用者介面，讓您可以瀏覽或搜尋存放庫中的可用數位資產，並用於您的應用程式編寫體驗。

在您的應用程式體驗中可利用資產選擇器套件使用微前端使用者介面。套件的任何更新都會自動匯入，而最新部署的資產選擇器會自動載入到您的應用程式。

![概觀](assets/overview.png)

資產選擇器提供了許多優點，例如：

* 可使用 Vanilla JavaScript 資料庫輕鬆整合任何 [Adobe](/help/assets/integrate-asset-selector-adobe-app.md) 或[非 Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md) 應用程式。
* 容易維護，因為資產選擇器套件的更新會自動部署到您的應用程式可用的資產選擇器。您的應用程式無需更新即可載入最新的修改內容。
* 簡易的自訂功能，因為有可以控制應用程式中資產選擇器顯示的可用屬性。
* 全文搜尋、開箱即用和自訂篩選器，可快速找到要在編寫體驗中使用的資產。
* 能夠在 IMS 組織內切換存放庫以選擇資產。
* 能夠依照名稱、維度和大小對資產進行排序，並以清單、網格、圖庫或瀑布檢視檢視。

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## 先決條件{#prereqs}

您必須確保以下通訊方式：

* 該主機應用程式於 HTTPS 上執行。
* 您無法於 `localhost` 上執行該應用程式。如果您想在本機上整合資產選擇器，則必須建立一個自訂網域，例如 `[https://<your_campany>.localhost.com:<port_number>]`，並在 `redirectUrl list` 中新增此自訂網域。
* 您可以使用相應的 `imsClientId` 設定並新增 clientID 至 AEM Cloud Service 環境變數中。
<!--* You can configure and add `ADOBE_PROVIDED_CLIENT_ID` into the AEM Cloud Service environment variable with the respective `imsClientId`.
![Asset Selector IMS Client id environment](assets/asset-selector-ims-client-id-env.png)-->
* IMS 範圍清單需要在環境設定中進行定義。
* 應用程式的 URL 位於 IMS 用戶端的重新導向 URL 允許清單中。
* IMS 登入流程是使用網頁瀏覽器上的快顯視窗進行設定和轉譯。因此，應在目標瀏覽器上啟用或允許快顯視窗。

如果您需要資產選擇器的 IMS 驗證工作流程，應符合上述先決條件。或者，如果您已透過 IMS 工作流程進行驗證，則可以改為新增 IMS 資訊。

**了解更多**

* [整合資產選擇器與 Adobe 應用程式](/help/assets/integrate-asset-selector-adobe-app.md)
* [整合資產選擇器與非 Adobe 應用程式](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [整合資產選擇器 Dynamic Media Open API](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!IMPORTANT]
>
> 存放庫旨在作為補充文件，說明整合資產選擇器的可用 API 和使用範例。在嘗試安裝或使用資產選擇器之前，請確保您的組織已佈建對資產選擇器的存取權限，作為 Experience Manager Assets as a Cloud Service 設定檔的一部分。如果您尚未佈建，則無法整合或使用這些元件。若要要求佈建，您的程式管理員應從 Admin Console 提出標記為 P2 的支援服務單，並包含以下資訊：
>
>* 託管整合應用程式的網域名稱。
>* 佈建後，您的組織將獲得與所要求之環境相對應的 `imsClientId`、`imsScope` 和 `redirectUrl`，對於資產選擇器的設定至關重要。如果沒有這些有效屬性，您就無法執行安裝步驟。

## 安裝 {#installation}

ESM 內容傳遞網路 (例如 [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) 和 [UMD](https://github.com/umdjs/umd) 版本均可使用資產選擇器。

在使用 **UMD 版** 的瀏覽器中 (建議)：

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

在具備 `import maps` 支援並使用 **ESM CDN 版**&#x200B;的瀏覽器中：

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

在使用 **ESM CDN 版**&#x200B;的 Deno/Webpack Module Federation 中：

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

## 使用資產選擇器 {#using-asset-selector}

在資產選擇器設定完成後，且您以 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 應用程式使用資產選擇器完成身分驗證，則您可以選擇資產或執行各種其他操作，以便在存放庫中搜尋您的資產。

![using-asset-selector](assets/using-asset-selector.png)

* **A**：[隱藏/顯示面板](#hide-show-panel)
* **B**：[存放庫切換器](#repository-switcher)
* **C**：[資產](#repository)
* **D**：[篩選器](#filters)
* **E**：[搜尋列](#search-bar)
* **F**：[排序](#sorting)
* **G**：[按遞增或遞減順序排序](#sorting)
* **H**：[檢視](#types-of-view)

### 隱藏/顯示面板 {#hide-show-panel}

若要將資料夾隱藏在左側導覽中，請按一下&#x200B;**[!UICONTROL 隱藏資料夾]**&#x200B;圖示。要還原變更，請再按一下&#x200B;**[!UICONTROL 隱藏資料夾]**&#x200B;圖示。

### 存放庫切換器 {#repository-switcher}

資產選擇器也可讓您切換存放庫進行資產選擇。您可以從左側面板中的下拉清單中選擇您要的存放庫。下拉清單中可用的存放庫選項是根據`repositoryId``index.html`檔案中定義的屬性。它是以登入使用者所存取的選定 IMS org 環境為基礎。消費者可以傳遞一個偏好的`repositoryID`，而且在該情況下，資產選擇器將停止呈現 repo 切換器，並僅從指定的存放庫呈現資產。

### 資產存放庫

那是可用於執行操作的資產資料夾集合。

### 現成可用篩選器 {#filters}

資產選擇器也提供現成可用的篩選器選項，以調整您的搜尋結果。您可以使用以下篩選器：

* **[!UICONTROL 狀態]：**&#x200B;包含在 `all`、`approved`、`rejected` 和 `no status` 之間的資產現況。
* **[!UICONTROL 檔案類型]：**&#x200B;包含 `folder`、`file`、`images`、`documents` 或 `video`。
* **[!UICONTROL 過期狀態]：**&#x200B;依據資產的過期時間提及資產。您可以勾選 `[!UICONTROL Expired]` 核取方塊來篩選過期的資產；或設定資產的 `[!UICONTROL Expiration Duration]` 以根據其到期時間顯示資產。資產已過期或即將過期時，會出現一個徽章來描繪該狀態。此外，您可以控制是否允許使用 (或拖放) 過期資產。了解更多有關[自訂過期資產](/help/assets/asset-selector-customization.md#customize-expired-assets)的資訊。預設情況下，對於未來 30 天內到期的資產，會顯示&#x200B;**即將到期**&#x200B;徽章。不過，您可以使用 `expirationDate` 屬性來設定過期時間。

  >[!TIP]
  >
  > 如果您想根據未來的到期日檢視或篩選資產，請在 `[!UICONTROL Expiration Duration]` 欄位中提及未來的日期範圍。它會顯示附有&#x200B;**即將過期**&#x200B;徽章的資產。

* **[!UICONTROL MIME 類型]：**&#x200B;包含 `JPG`、`GIF`、`PPTX`、`PNG`、`MP4`、`DOCX`、`TIFF`、`PDF`、`XLSX`。
* **[!UICONTROL 影像尺寸]：**&#x200B;包含影像的最小/最大寬度、最小/最大高度。

  ![rail-view-example](assets/filters-asset-selector.png)

### 自訂搜尋

除了全文搜尋外，資產選擇器也可讓您使用自訂搜尋來搜尋檔案中的資產。您可以在模組檢視和邊欄檢視模式下，使用自訂搜尋篩選器。

![custom-search](assets/custom-search1.png)

您也可以建立一個預設的搜尋篩選器，以儲存您經常搜尋的欄位，並供後續使用。若要為資產建立自訂搜尋，您可以使用 `filterSchema` 屬性。

### 搜尋列 {#search-bar}

資產選擇器可讓您在選取的存放庫中執行資產的全文搜尋。例如，如果您在搜尋列中鍵入關鍵字 `wave`，就會顯示中繼資料屬性中提及 `wave` 關鍵字的所有資產。

### 排序 {#sorting}

您可以按資產的名稱、維度或大小對資產選擇器中的資產進行排序。您可以依照遞增或遞減順序排序資產。

### 檢視的類型 {#types-of-view}

資產選擇器可讓您在四種不同的檢視中檢視資產：

* ![清單檢視](assets/do-not-localize/list-view.png) [!UICONTROL **清單檢視**] 清單檢視會在單一欄中顯示可捲動的檔案和資料夾。
* ![網格檢視](assets/do-not-localize/grid-view.png) [!UICONTROL **網格檢視**] 網格檢視會在列與欄的網格中顯示可捲動的檔案和資料夾。
* ![圖庫檢視](assets/do-not-localize/gallery-view.png) [!UICONTROL **圖庫檢視**] 圖庫檢視會在居中鎖定的水平清單中顯示檔案或資料夾。
* ![瀑布檢視](assets/do-not-localize/waterfall-view.png) [!UICONTROL **瀑布**&#x200B;檢視] 瀑布檢視會以 Bridge 的形式顯示檔案或資料夾。

### 資產詳細資料和中繼資料 {#asset-details-and-metadata}

資產詳細資料頁面提供特定資產的全方位視圖，將所有關鍵資訊整合到一個地方。其中包含顯示名稱、檔案格式、狀態和簡要說明的概觀，以及方便視覺識別的預覽或縮圖。另外亦包括某項資產的中繼資料，例如建立日期、作者、大小、色彩配置等。這些屬性有助於提高資產搜尋、過濾和分類的效率。在資產選擇器的邊欄視圖和模態視圖中皆可看見資產詳細資料面板。在邊欄視圖中，必須啟用並設定 `onDrop` 屬性才能傳回資產。或者，在模態視圖中，`handleSelection` 屬性會傳回一項資產。請參閱[資產選擇器屬性](asset-selector-properties.md)。

要查看資產和中繼資料的詳細資料，請執行以下步驟：

1. 開啟資產選擇器 MFE 並導覽至一項資產。
1. 將滑鼠懸停在資產上方並點選![資訊圖示](/help/assets/assets/info-icon-solid-black.svg)。
1. 前往「**[!UICONTROL 資訊]**」索引標籤來查看資產的詳細資料。<!--Otherwise, go to the **[Renditions](#asset-renditions)** tab to see renditions of an asset.-->

若要自訂資產的詳細資料視圖面板，請參閱[在模態視圖中自訂資訊](asset-selector-customization.md#customize-info-in-modal-view)。

![資產詳細資料](assets/asset-details.png)

<!--

#### Asset renditions {#asset-renditions}

Renditions in Adobe Experience Manager (AEM) are customized versions of digital assets, such as images, designed for different devices and platforms to ensure optimal performance. See [Dynamic Media renditions](/help/assets/renditions.md#dynamic-media-renditions).

>[!NOTE]
>
>* Prerequisites to [Dynamic Media with OpenAPI Capabilities renditions](/help/assets/renditions.md##prereqs-dm-with-openapi-renditions).
>* Renditions tab in the details panel of an asset shows up if `featureSet`  props is set to `['detail-panel', 'dm-renditions']`.
>* An asset should be approved to see Dynamic Media with OpenAPI renditions and/or ensure processing/publishing of the asset to Dynamic Media is complete (for images only).

![Asset details dynamic media renditions](assets/asset-details-dm-renditions.png)

For assets that are approved and have renditions enabled, you see the **Dynamic Media with Open API** badge. 

![Dynamic Media Open API stamp](assets/dm-open-api-stamp.png)

Additionally, see [Asset Selector user interface for Dynamic Media with OpenAPI capabilities](integrate-asset-selector-dynamic-media-open-api.md##interface-dynamic-media-open-api).

##### Add modifiers {#modifiers-dm-media-renditions}

Beyond the common image settings available in the UI, Dynamic Media supports numerous advanced image modifications that you can specify in the Image Modifiers field. See [Defining image preset options with Image Modifiers](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/managing-image-presets#defining-image-preset-options-with-image-modifiers).

-->

## 深入了解重要功能 {#key-capabilities-asset-selector}

<table>
<tr>
    <td>
        <img src="assets/integrate-asset-selector.gif" width="70px" height="70px" alt="整合資產選擇器圖形"><br/>
        <a href="integrate-asset-selector.md">整合資產選擇器</a>
        <p>
        <em>了解將資產選擇器與多個應用程式整合的各種功能。
        </p>
     </td>
    <td>
        <img src="assets/with-adobe-app.gif" width="70px" height="70px" alt="整合資產選擇器與 Adobe 應用程式圖形"><br/>
        <a href="integrate-asset-selector-adobe-app.md">整合資產選擇器與 Adobe 應用程式</a>
        <p>
        <em>了解如何將資產選擇器與各種 Adobe 應用程式整合。</em>
        </p>
    </td>
    <td>
        <img src="assets/third-party-app.gif" width="70px" height="70px" alt="整合資產選擇器圖形"><br/>
        <a href="integrate-asset-selector-non-adobe-app.md">整合資產選擇器與第三方應用程式</a>
        <p>
        <em>挖掘將資產選擇器與非 Adobe 應用程式整合的功能。</em>
        </p>
    </td>
    <td>
        <img src="assets/with-dynamic-media-open-api.gif" width="70px" height="70px" alt="整合資產選擇器圖形"><br/>
        <a href="integrate-asset-selector-dynamic-media-open-api.md">整合資產選擇器與 Dynamic Media Open API</a>
        <p>
        <em>了解如何整合資產選擇器與 Dynamic Media Open API。</em>
        </p>
     </td>
     <td>
        <img src="assets/asset-selector-properties.gif" width="70px" height="70px" alt="資產選擇器範例圖形"><br/>
        <a href="asset-selector-properties.md">資產選擇器屬性</a>
        <p>
        <em>以實際的方式了解屬性的使用情形。</em>
        </p>
    </td>
</tr>
<tr>
    <td>
        <img src="assets/asset-selector-examples.gif" width="70px" height="70px" alt="資產選擇器屬性圖形"><br/>
        <a href="asset-selector-examples.md">資產選擇器範例</a>
        <p>
        <em>了解自訂資產選擇器各個元件的基礎知識，例如篩選器、資產選擇、過期資產等等。</em>
        </p>
    </td>
    <td>
        <img src="assets/customize-asset-selector.gif" width="70px" height="70px" alt="自訂資產選擇器圖形"><br/>
        <a href="asset-selector-customization.md">資產選擇器自訂</a>
        <p>
        <em>根據您的可用性設定和自訂資產選擇器的各種元件。</em>
        </p>
    </td>
    <td>
        <img src="assets/asset-selector-upload.gif" width="70px" height="70px" alt="資產選擇器上傳圖形"><br/>
        <a href="asset-selector-upload.md">資產選擇器上傳</a>
        <p>
        <em>了解如何從本機或第三方檔案系統，將檔案或資料夾上傳到資產選擇器。</em>
        </p>
    </td>
     <td>
        <img src="assets/asset-selector-collections.gif" width="70px" height="70px" alt="資產選擇器集合圖形"><br/>
        <a href="asset-selector-collections.md">資產選擇器集合</a>
        <p>
        <em>了解如何使用 Experience Manager 存放庫，在資產選擇器內使用集合。</em>
        </p>
    </td>
    <td>
    </td>
</tr>
</table>

>[!MORELIKETHIS]
>
>* [資產選擇器自訂](/help/assets/asset-selector-customization.md)
>* [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
>* [整合資產選擇器與具備 OpenAPI 功能的 Dynamic Media](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [由 Commerce 的 AEM Assets 整合提供支援的產品視覺化](https://experienceleague.adobe.com/zh-hant/docs/commerce/product-visuals/overview)
