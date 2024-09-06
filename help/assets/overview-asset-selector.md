---
title: 適用於  [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service] 的資產選擇器
description: 使用Asset Selector搜尋、尋找和擷取應用程式內的資產中繼資料和轉譯。
role: Admin, User
source-git-commit: fb1350c91468f9c448e34b66dc938fa3b5a3e9a9
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 35%

---

# 微前端資產選擇器 {#Overview}

微前端資產選擇器提供一個輕鬆整合 [!DNL Experience Manager Assets] 存放庫的使用者介面，讓您可以瀏覽或搜尋存放庫中的可用數位資產，並用於您的應用程式編寫體驗。

在您的應用程式體驗中可利用資產選擇器套件使用微前端使用者介面。套件的任何更新都會自動匯入，而最新部署的資產選擇器會自動載入到您的應用程式。

![概觀](assets/overview.png)

資產選擇器提供了許多優點，例如：

* 使用Vanilla JavaScript程式庫輕鬆與任何[Adobe](#integrate-asset-selector-adobe-app.md)或[非Adobe](#integrate-asset-selector.md)應用程式整合。
* 容易維護，因為資產選擇器套件的更新會自動部署到您的應用程式可用的資產選擇器。您的應用程式無需更新即可載入最新的修改內容。
* 簡易的自訂功能，因為有可以控制應用程式中資產選擇器顯示的可用屬性。
* 全文搜尋、開箱即用和自訂篩選器，可快速找到要在編寫體驗中使用的資產。
* 能夠在 IMS 組織內切換存放庫以選擇資產。
* 可依名稱、維度和大小排序資產，並在「清單」、「格線」、「收藏館」或「瀑布」檢視中檢視資產。

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

您必須確定下列通訊方法：

* 應用程式正在HTTPS上執行。
* 應用程式的URL位於IMS使用者端的允許重新導向URL清單中。
* IMS登入流程已設定完畢，並使用網頁瀏覽器上的快顯視窗呈現。 因此，目標瀏覽器上應該啟用或允許快顯視窗。

如果您需要Asset Selector的IMS驗證工作流程，請使用上述先決條件。 或者，如果您已通過IMS工作流程驗證，您可以改為新增IMS資訊。

**檢視更多**

* [整合Asset Selector與Adobe應用程式](#integrate-asset-selector-adobe-app.md)
* [將資產選擇器與非Adobe應用程式整合](#integrate-asset-selector-non-adobe-app.md)
* [整合Asset Selector dynamic media open API](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!IMPORTANT]
>
> 此存放庫旨在作為補充檔案，說明整合資產選擇器的可用API和使用範例。 在嘗試安裝或使用「資產選擇器」之前，請確保貴組織已布建對「資產選擇器」的存取權，作為Experience Manager Assetsas a Cloud Service設定檔的一部分。 如果您尚未布建，則無法整合或使用這些元件。 若要請求布建，您的程式管理員應從Admin Console提出標示為P2的支援票證，並包含下列資訊：
>
>* 託管整合應用程式的網域名稱。
>* 布建後，您的組織將會收到`imsClientId`、`imsScope`以及對應到設定資產選擇器所需必要環境的`redirectUrl`。 如果沒有這些有效的屬性，您就無法執行安裝步驟。

## 安裝 {#installation}

資產選擇器可透過ESM CDN （例如[esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)）和[UMD](https://github.com/umdjs/umd)版本使用。

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
* **H**：[視圖](#types-of-view)

### 隱藏/顯示面板 {#hide-show-panel}

若要隱藏左側導覽中的資料夾，請按一下&#x200B;**[!UICONTROL 隱藏資料夾]**&#x200B;圖示。 要還原變更，請再按一下&#x200B;**[!UICONTROL 隱藏資料夾]**&#x200B;圖示。

### 存放庫切換器 {#repository-switcher}

Asset Selector也可讓您切換資產選取的存放庫。 您可以從左側面板中的下拉清單中選擇您要的存放庫。下拉清單中可用的存放庫選項是根據`repositoryId``index.html`檔案中定義的屬性。其基礎是登入使用者存取之所選IMS組織的環境。 消費者可以傳遞一個偏好的`repositoryID`，而且在該情況下，資產選擇器將停止呈現 repo 切換器，並僅從指定的存放庫呈現資產。

### 資產存放庫

那是可用於執行操作的資產資料夾集合。

### 現成可用篩選器 {#filters}

資產選擇器也提供現成可用的篩選器選項，以調整您的搜尋結果。您可以使用以下篩選器：

* **[!UICONTROL 狀態]：**&#x200B;包含`all`、`approved`、`rejected`或`no status`之間的資產目前狀態。
* **[!UICONTROL 檔案型別]：**&#x200B;包含`folder`、`file`、`images`、`documents`或`video`。
* **[!UICONTROL 到期狀態]：**&#x200B;根據資產的到期持續時間提及該資產。 您可以勾選「`[!UICONTROL Expired]`」核取方塊以篩選過期的資產；或設定資產的`[!UICONTROL Expiration Duration]`以根據資產的到期持續時間顯示資產。 當資產已過期或即將過期時，畫面會顯示相同的徽章。 此外，您可以控制是否允許使用（或拖放）過期的資產。 深入瞭解[自訂過期的資產](#asset-selector-customization.md#customize-expired-assets)。 依預設，會針對未來30天內到期的資產顯示&#x200B;**即將到期**&#x200B;徽章。 不過，您可以使用`expirationDate`屬性來設定到期日。

  >[!TIP]
  >
  > 若要根據資產的未來到期日檢視或篩選資產，請在「`[!UICONTROL Expiration Duration]`」欄位中提及未來日期範圍。 它會顯示具有&#x200B;**即將到期**&#x200B;徽章的資產。

* **[!UICONTROL MIME型別]：**&#x200B;包含`JPG`、`GIF`、`PPTX`、`PNG`、`MP4`、`DOCX`、`TIFF`、`PDF`、`XLSX`。
* **[!UICONTROL 影像大小]：**&#x200B;包含影像的最小/最大寬度、最小/最大高度。

  ![rail-view-example](assets/filters-asset-selector.png)

### 自訂搜尋

除了全文檢索搜尋之外，「資產選擇器」可讓您使用自訂搜尋功能來搜尋檔案中的資產。 您可以在模組視圖和邊欄視圖模式下，使用自訂搜尋篩選器。

![custom-search](assets/custom-search1.png)

您也可以建立預設搜尋篩選器，以儲存您經常搜尋的欄位並在稍後使用。 若要為資產建立自訂搜尋，您可以使用 `filterSchema` 屬性。

### 搜尋列 {#search-bar}

「資產選擇器」可讓您在選取的存放庫中執行資產的全文搜尋。 例如，如果您在搜尋列中鍵入關鍵字 `wave`，就會顯示中繼資料屬性中提及 `wave` 關鍵字的所有資產。

### 排序 {#sorting}

您可以按資產的名稱、維度或大小對資產選擇器中的資產進行排序。您可以依照遞增或遞減順序排序資產。

### 視圖的類型 {#types-of-view}

「資產選取器」可讓您以四種不同的檢視檢視檢視資產：

* **![清單檢視](assets/do-not-localize/list-view.png) [!UICONTROL 清單檢視]**&#x200B;清單檢視在單一欄中顯示可捲動檔案和資料夾。
* **![格線檢視](assets/do-not-localize/grid-view.png) [!UICONTROL 格線檢視]**&#x200B;格線檢視在列與欄的格線中顯示可捲動檔案與資料夾。
* **![相簿檢視](assets/do-not-localize/gallery-view.png) [!UICONTROL 相簿檢視]**&#x200B;相簿檢視會在置中鎖定的水準清單中顯示檔案或資料夾。
* **![瀑布檢視](assets/do-not-localize/waterfall-view.png) [!UICONTROL 瀑布檢視]**&#x200B;瀑布檢視以Bridge的形式顯示檔案或資料夾。

**概觀圖形**


## 進一步瞭解主要功能 {#key-capabilities-asset-selector}

<table>
<tr>
    <td>
        <img src="assets/integrate-asset-selector.gif" width="70px" height="70px" alt="整合資產選擇器圖形"><br/>
        <a href="integrate-asset-selector.md">整合資產選擇器</a>
        <p>
        <em>瞭解各種功能，以便將Asset Selector與多個應用程式整合。
        </p>
     </td>
    <td>
        <img src="assets/with-adobe-app.gif" width="70px" height="70px" alt="整合Asset Selector與Adobe應用程式圖形"><br/>
        <a href="integrate-asset-selector.md">整合Asset Selector與Adobe應用程式</a>
        <p>
        <em>瞭解如何整合資產選擇器與各種Adobe應用程式。</em>
        </p>
    </td>
    <td>
        <img src="assets/third-party-app.gif" width="70px" height="70px" alt="整合資產選擇器圖形"><br/>
        <a href="integrate-asset-selector.md">整合Asset Selector與協力廠商應用程式</a>
        <p>
        <em>瞭解如何將「資產選擇器」與非Adobe應用程式整合。</em>
        </p>
    </td>
    <td>
        <img src="assets/with-dynamic-media-open-api.gif" width="70px" height="70px" alt="整合資產選擇器圖形"><br/>
        <a href="integrate-asset-selector.md">整合Asset Selector與Dynamic Media Open API</a>
        <p>
        <em>瞭解如何整合Asset Selector與Dynamic Media Open API。</em>
        </p>
     </td>
</tr>
<tr>
    <td>
        <img src="assets/asset-selector-examples.gif" width="70px" height="70px" alt="Asset Selector屬性圖形"><br/>
        <a href="asset-selector-customization.md">資產選擇器屬性</a>
        <p>
        <em>瞭解自訂Asset Selector各種元件的基本知識，例如篩選器、資產選擇、過期資產等等。</em>
        </p>
    </td>
    <td>
        <img src="assets/asset-selector-properties.gif" width="70px" height="70px" alt="資產選擇器範例圖形"><br/>
        <a href="asset-selector-customization.md">資產選擇器範例</a>
        <p>
        <em>瞭解如何以實際方式使用屬性。</em>
        </p>
    </td>
    <td>
        <img src="assets/customize-asset-selector.gif" width="70px" height="70px" alt="自訂資產選擇器圖形"><br/>
        <a href="asset-selector-customization.md">資產選擇器自訂</a>
        <p>
        <em>根據您的使用狀態，設定和自訂各種資產選擇器元件。</em>
        </p>
    </td>
    <td></td>
</tr>
</table>

>[!MORELIKETHIS]
>
>* [資產選擇器自訂](/help/assets/asset-selector-customization.md)
>* [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
>* [整合資產選擇器Dynamic Media開啟API](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
