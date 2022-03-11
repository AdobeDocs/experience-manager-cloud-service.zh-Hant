---
title: 如何在Forms頁面上建立Experience Manager Sites門戶
description: 瞭解如何建立Forms門戶並在AEM Sites頁面上使用現成核心元件。
exl-id: 13cfe3ba-2e85-46bf-a029-2673de69c626
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1784'
ht-degree: 0%

---

# 在門戶上列出自適應Forms {#publish-forms-on-portal}

在典型的以表單為中心的門戶部署方案中，表單開發和門戶開發是兩個不相干的活動。 表單設計器在儲存庫中設計和儲存表單時，Web開發人員會建立一個Web應用程式來列出表單並處理表單提交。 Forms被複製到Web層，因為表單儲存庫和Web應用程式之間沒有通信。

這種情況往往導致管理問題和生產延遲。 例如，如果儲存庫中有一個較新版本的表單，則需要替換Web層上的表單，修改Web應用程式，然後在公共站點上重新部署該表單。 重新部署Web應用程式可能會導致伺服器停機。 通常，伺服器停機是計畫內活動，因此不能立即將更改推送到公共站點。

AEM Forms公司提供門戶元件，以減少管理費用和生產延遲。 這些元件使Web開發人員能夠在使用Adobe Experience Manager(AEM)創作的網站上建立和定制Forms門戶。

表單門戶元件允許您添加以下功能：

* 在自定義佈局中列出表單。 現成版本中提供「清單」視圖和「卡」視圖佈局。 您可以建立自己的自定義佈局。
* 允許您在列出自定義元資料和自定義操作時顯示它們。
* 列出由AEM FormsUI在使用Forms門戶元件的發佈實例上發佈的表單。
* 允許最終用戶以HTML和PDF格式呈現表單。
* 啟用基於標題和說明的表單搜索。
* 使用自定義CSS自定義門戶的外觀。
* 建立到表單的連結。
* 列出與最終用戶建立的自適應Forms相關的草稿和提交。

## Forms門戶頁的元件 {#forms-portal-components}

AEM Forms提供以下現成的門戶元件：

* 搜索和Lister:此元件允許您將表單從表單儲存庫列到門戶頁面，並提供了配置選項，以根據指定的條件列出表單。

* 草稿和提交：Search &amp; Lister元件顯示由Forms作者公開的表單，而Drafts &amp; Submissions元件則顯示保存為草稿的表單，以供日後完成和提交的表單。 此元件為任何登錄用戶提供個性化體驗。

* 連結：此元件允許您建立指向頁面上任意位置的表單的連結。

你可以 [導入開箱即用的Forms門戶元件](#import-forms-portal-components-aem-archetype) 原型AEM計畫。 導入後，請執行以下配置：
* [配置外部儲存](#configure-azure-storage-adaptive-forms)
* [啟用Forms門戶元件](#enable-forms-portal-components)
* [配置Forms門戶元件](#configure-forms-portal-components)

## 導入Forms門戶元件 {#import-forms-portal-components-aem-archetype}

要在AEM Formsas a Cloud Service上導入開箱即用的Forms門戶元件，請執行以下步驟：

1. **在本地開發實例上克隆Cloud Manager Git儲存庫：**  您的Cloud Manager Git儲存庫包含預設AEM項目。 它基於 [原AEM型](https://github.com/adobe/aem-project-archetype/)。 使用Cloud Manager UI中的自助Git帳戶管理來克隆Cloud Manager Git儲存庫，以將項目帶到本地開發環境。 有關訪問儲存庫的詳細資訊，請參見 [訪問儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html)。

1. **建立 [!DNL Experience Manager Forms] 作為 [Cloud Service] 項目：** 建立 [!DNL Experience Manager Forms] 作為 [Cloud Service] 基於 [原AEM型27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) 或稍後。 原型幫助開發人員輕鬆開始開發 [!DNL AEM Forms] as a Cloud Service。 它還包含一些示例主題和模板，幫助您快速啟動。

   建立 [!DNL Experience Manager Forms] as a Cloud Service項目，開啟命令提示符並運行以下命令。 要包括 [!DNL Forms] 特定配置、主題和模板，設定 `includeForms=y`。

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   另外，更改 `appTitle`。 `appId`, `groupId`，以反映您的環境。

1. **在預發行版中，執行以下步驟以使用Forms門戶元件：**
   * [啟用預發行渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en)。
   * 替換 `core-forms-components-*` 版本，其中包含您的 `Cloud Manager/AEM Archetype` 通過更新項目 `<core.forms.components.version>x.y.z</core.forms.components.version>` 頂層 `pom.xml` 原型工程。

1. **將項目部署到您的本地開發環境：** 可以使用以下命令部署到本地開發環境

   `mvn -PautoInstallPackage clean install`

   有關命令的完整清單，請參見 [構建和安裝](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [將代碼部署到 [!DNL AEM Forms] as a Cloud Service環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds)。


## 為AdaptiveForms配置Azure儲存 {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] 資料整合](data-integration.md) 提供 [!DNL Azure] 儲存配置與 [!DNL Azure] 儲存服務。 表單資料模型可用於建立與交互的自適應Forms [!DNL Azure] 伺服器以啟用業務工作流。

### 建立 Azure 儲存體設定 {#create-azure-storage-configuration}

在執行這些步驟之前，請確保您有Azure儲存帳戶和訪問密鑰以授權對 [!DNL Azure] 儲存帳戶。

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure儲存]**。
1. 選擇要建立配置的資料夾並點擊 **[!UICONTROL 建立]**。
1. 在中為配置指定標題 **[!UICONTROL 標題]** 的子菜單。
1. 指定 [!DNL Azure] 儲存帳戶 **[!UICONTROL Azure儲存帳戶]** 的子菜單。

### 為Forms門戶配置統一儲存連接器 {#configure-usc-forms-portal}

執行以下步驟以配置工作流的統一儲存連AEM接器：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 統一儲存連接器]**。
1. 在 **[!UICONTROL Forms門戶]** 選擇 **[!UICONTROL Azure]** 從 **[!UICONTROL 儲存]** 的子菜單。
1. 指定 [Azure儲存配置的配置路徑](#create-azure-storage-configuration) 的 **[!UICONTROL 儲存配置路徑]** 的子菜單。
1. 點擊 **[!UICONTROL 發佈]** 然後點擊 **[!UICONTROL 保存]** 的子菜單。

## 啟用Forms門戶元件 {#enable-forms-portal-components}

要在Adobe Experience Manager(AEM)站點中使用任何核心元件（包括現成門戶元件），必須建立代理元件並為您的站點啟用它。 有關建立代理元件和啟用門戶元件的資訊，請參見 [使用核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components)。

啟用門戶元件後，您可以在站點頁面的作者實例中使用它。

## 添加和配置Forms門戶元件 {#configure-forms-portal-components}

通過添加和配置門戶元件，可以在使用創AEM作的網站上建立和自定義Forms門戶。 確保 [元件已啟用](#enable-forms-portal-components) 在Forms門口使用。

要添加元件，請將元件從「元件」窗格拖放到頁面上的佈局容器中，或按一下佈局容器上的添加表徵圖，然後從 [!UICONTROL 插入新元件] 對話框。

### 配置草稿和提交元件 {#configure-drafts-submissions-component}

「草稿和提交」元件顯示保存為草稿的表單，以供以後完成和提交的表單。 要配置，請點擊元件，然後點擊 ![「配置」表徵圖](assets/configure_icon.png)。 在 [!UICONTROL 草稿和提交] 對話框，指定標題以指示表單清單為草稿或已提交表單。 還選擇元件應以卡片或清單格式列出草稿表單或已提交表單。

![草稿表徵圖](assets/drafts-component.png)

![提交表徵圖](assets/submission-listing.png)

### 配置Search &amp; Lister元件 {#configure-search-lister-component}

Search &amp; Lister元件用於在頁面上列出自適應表單並在列出的表單上實現搜索。

![「搜索和Lister」表徵圖](assets/search-and-lister-component.png)

要配置，請點擊元件，然後點擊 ![「配置」表徵圖](assets/configure_icon.png)。 的 [!UICONTROL 搜索和李斯特] 對話框。

1. 在 [!UICONTROL 顯示] 頁籤，配置以下內容：
   * 在 **[!UICONTROL 標題]**，指定Search &amp; Lister元件的標題。 指示性標題使用戶能夠跨表單清單執行快速搜索。
   * 從 **[!UICONTROL 佈局]** 清單中，選擇要以卡片或清單格式表示表單的佈局。
   * 選擇 **[!UICONTROL 隱藏搜索]** 和 **[!UICONTROL 隱藏排序]** 隱藏搜索並按功能排序。
   * 在 **[!UICONTROL 工具提示]**，提供懸停在元件上時顯示的工具提示。
1. 在 [!UICONTROL 資產資料夾] 頁籤，指定在頁面上提取和列出表單的位置。 可以配置多個資料夾位置。
1. 在 [!UICONTROL 結果] 頁籤，配置每頁要顯示的最大表單數。 預設為每頁8個表單。

### 配置連結元件 {#configure-link-component}

連結元件使您能夠提供指向頁面上自適應表單的連結。 要配置，請點擊元件，然後點擊 ![「配置」表徵圖](assets/configure_icon.png)。 的 [!UICONTROL 編輯連結元件] 對話框。

1. 在 [!UICONTROL 顯示] 頁籤，提供連結標題和工具提示，以便識別由連結表示的表單。
1. 在 [!UICONTROL 資產資訊] 頁籤，指定儲存資產的儲存庫路徑。
1. 在 [!UICONTROL 查詢參數] 頁籤中，以鍵值對格式指定其他參數。 按一下該連結時，這些附加參數會隨窗體一起傳遞。

## 使用Adobe Sign配置非同步表單提交 {#configure-asynchronous-form-submission-using-adobe-sign}

您可以配置為僅在所有收件人完成簽名儀式後提交自適應表單。 按照以下步驟使用Adobe Sign配置設定。

1. 在作者實例中，在編輯模式下開啟「自適應表單」。
1. 從左窗格中，按一下「Properties（屬性）」表徵圖，然後展開 **[!UICONTROL 電子簽名]** 的雙曲餘切值。
1. 選擇 **[!UICONTROL 啟用Adobe Sign]**。 顯示各種配置選項。
1. 在 [!UICONTROL 提交表單] 的 **[!UICONTROL 每個接受者都完成簽署儀式]** 的子菜單。 所有收件人簽名後，才提交表單。

## 將自適應Forms另存為草稿 {#save-adaptive-forms-as-drafts}

您可以將表單另存為「草稿」，以便以後完成表單。 表單保存為草稿有兩種方式：
* 在表單元件（例如按鈕）上建立「保存表單」規則。 按一下按鈕後，規則觸發器和表單將保存為草稿。
* 啟用自動保存功能，該功能按指定事件或在配置的時間間隔後保存表單。

### 建立規則以將自適應表單另存為草稿 {#rule-to-save-adaptive-form-as-draft}

要在表單元件（例如按鈕）上建立「保存表單」規則，請執行以下步驟：

1. 在作者實例中，在編輯模式下開啟「自適應表單」。
1. 從左窗格，點擊 ![元件表徵圖](assets/components_icon.png) 然後 [!UICONTROL 按鈕] 的子菜單。
1. 點擊 [!UICONTROL 按鈕] 然後點擊 ![「配置」表徵圖](assets/configure_icon.png)。
1. 點擊 [!UICONTROL 編輯規則] 表徵圖以開啟規則編輯器。
1. 點擊 **[!UICONTROL 建立]** 來配置和建立規則。
1. 在 [!UICONTROL 當] 中，選擇「已按一下」 [!UICONTROL 然後] 的子菜單。
1. 點擊 **[!UICONTROL 完成]** 來保存規則。

### 啟用自動保存 {#enable-auto-save}

可以按照如下方式為自適應表單配置自動保存功能：

1. 在作者實例中，在編輯模式下開啟「自適應表單」。
1. 從左窗格，點擊 ![「屬性」表徵圖](assets/configure_icon.png) 並擴展 [!UICONTROL 自動保存] 的雙曲餘切值。
1. 選擇 **[!UICONTROL 啟用]** 的子菜單。 您可以配置以下內容：
* 預設情況下， [!UICONTROL 自適應窗體事件] 設定為「true」，這意味著在每個事件後自動保存該窗體。
* 在 [!UICONTROL 觸發器]，配置為根據事件的發生或特定時間間隔後觸發自動保存。
