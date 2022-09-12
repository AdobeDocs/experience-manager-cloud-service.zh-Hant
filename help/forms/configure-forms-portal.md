---
title: 如何在Experience Manager Sites頁面上建立Forms Portal
description: 了解如何在Forms頁面上建立AEM Sites入口網站和使用現成可用的核心元件。
exl-id: 13cfe3ba-2e85-46bf-a029-2673de69c626
source-git-commit: 05bdc24974d2b82c1350bf6f75873cd7027f7d4a
workflow-type: tm+mt
source-wordcount: '1764'
ht-degree: 0%

---

# 在入口網站上列出適用性Forms {#publish-forms-on-portal}

在典型的以表單為中心的門戶部署情形中，表單開發和門戶開發是兩個不相關的活動。 表單設計人員在存放庫中設計和儲存表單時，網頁開發人員會建立網頁應用程式來列出表單並處理表單提交作業。 Forms會複製到Web層，因為表單存放庫與Web應用程式之間沒有通訊。

這種情況往往導致管理問題和生產延遲。 例如，如果儲存庫中有較新版本的表單，則您需要替換Web層上的表單、修改Web應用程式，然後在公共站點上重新部署該表單。 重新部署Web應用程式可能會造成伺服器停機。 通常，伺服器停機是計畫中的活動，因此無法即時將變更推送至公開網站。

AEM Forms提供入口元件，可減少管理開支和生產延遲。 這些元件讓網頁開發人員能在使用Adobe Experience Manager(AEM)製作的網站上建立和自訂Forms入口網站。

表單入口網站元件可讓您新增下列功能：

* 以自訂配置列出表單。 現成可用，提供清單視圖和卡片視圖佈局。 您可以建立自己的自訂配置。
* 可讓您在列出自訂中繼資料和自訂動作時顯示這些動作。
* 列出由AEM Forms UI發佈的表單，位於使用Forms Portal元件的發佈執行個體上。
* 允許使用者以HTML和PDF格式呈現表單。
* 根據標題和說明啟用表單搜尋。
* 使用自訂CSS來自訂入口網站的外觀和風格。
* 建立表單連結。
* 列出一般使用者建立之適用性Forms的草稿和提交。

## Forms入口網站頁面的元件 {#forms-portal-components}

AEM Forms可立即提供下列入口網站元件：

* Search &amp; Lister:此元件可讓您將表單從表單存放庫清單至入口網站頁面，並提供設定選項，讓您根據指定的條件列出表單。

* 草稿和提交：Search &amp; Lister元件顯示由Forms作者公開的表單，而Drafts &amp; Submissions元件則顯示儲存為草稿的表單，以供稍後完成已提交的表單。 此元件可為任何登入的使用者提供個人化體驗。

* 連結：此元件可讓您建立連結至頁面上任何位置的表單。

您可以 [匯入現成可用的Forms入口網站元件](#import-forms-portal-components-aem-archetype) 來自AEM專案原型。 匯入後，請執行下列設定：
* [配置外部儲存](#configure-azure-storage-adaptive-forms)
* [啟用Forms Portal元件](#enable-forms-portal-components)
* [設定Forms Portal元件](#configure-forms-portal-components)

## 匯入Forms入口網站元件 {#import-forms-portal-components-aem-archetype}

若要在AEM Formsas a Cloud Service上匯入現成可用的Forms Portal元件，請執行下列步驟：

1. **在本機開發執行個體上複製Cloud Manager Git存放庫：**  您的Cloud Manager Git存放庫包含預設的AEM專案。 其基礎為 [AEM原型](https://github.com/adobe/aem-project-archetype/). 使用Cloud Manager UI中的自助服務Git帳戶管理功能，原地複製您的Cloud Manager Git存放庫，將專案帶入本機開發環境。 有關訪問儲存庫的詳細資訊，請參閱 [存取儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

1. **建立 [!DNL Experience Manager Forms] as a [Cloud Service] 專案：** 建立 [!DNL Experience Manager Forms] as a [Cloud Service] 基於 [AEM原型27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) 或更新版本。 原型可協助開發人員輕鬆開始開發 [!DNL AEM Forms] as a Cloud Service。 此外也包含一些範例主題和範本，可協助您快速上手。

   若要建立 [!DNL Experience Manager Forms] as a Cloud Service於項目，請開啟命令提示符並運行以下命令。 要包括 [!DNL Forms] 特定配置、主題和模板，設定 `includeForms=y`.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   此外，變更 `appTitle`, `appId`，和 `groupId`，以反映您的環境。

   專案準備就緒後，請更新 `<core.forms.components.version>x.y.z</core.forms.components.version>` 頂層屬性 `pom.xml` 原型專案，以反映 [core-forms-components](https://github.com/adobe/aem-core-forms-components) 在 `AEM Archetype` 專案。

1. **將專案部署至本機開發環境：** 您可以使用下列命令來部署至本機開發環境

   `mvn -PautoInstallPackage clean install`

   有關命令的完整清單，請參見 [建置和安裝](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [將程式碼部署至 [!DNL AEM Forms] as a Cloud Service環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds).


## 為適用性Forms配置Azure儲存 {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] 資料整合](data-integration.md) proves [!DNL Azure] 儲存配置，將表單與 [!DNL Azure] 儲存服務。 表單資料模型可用來建立與互動的適用性Forms [!DNL Azure] 伺服器啟用業務工作流程。

### 建立 Azure 儲存體設定 {#create-azure-storage-configuration}

執行這些步驟之前，請確定您擁有Azure儲存帳戶和存取金鑰，以授權存取 [!DNL Azure] 儲存帳戶。

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure儲存]**.
1. 選取要建立設定的資料夾，然後點選 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 標題]** 欄位。
1. 指定 [!DNL Azure] 儲存帳戶 **[!UICONTROL Azure儲存帳戶]** 欄位。

### 為Forms Portal配置Unified Storage Connector {#configure-usc-forms-portal}

執行下列步驟為AEM工作流程配置Unified Storage Connector:

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 統一儲存連接器]**.
1. 在 **[!UICONTROL Forms入口網站]** 部分，選擇 **[!UICONTROL Azure]** 從 **[!UICONTROL 儲存]** 下拉式清單。
1. 指定 [Azure儲存配置的配置路徑](#create-azure-storage-configuration) 在 **[!UICONTROL 儲存配置路徑]** 欄位。
1. 點選 **[!UICONTROL 發佈]** 然後點選 **[!UICONTROL 儲存]** 以儲存設定。

## 啟用Forms Portal元件 {#enable-forms-portal-components}

若要在Adobe Experience Manager(AEM)網站中使用任何核心元件（包括現成可用的入口元件），您必須建立Proxy元件並為您的網站啟用它。 有關建立代理元件和啟用門戶元件的資訊，請參閱 [使用核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components).

啟用入口網站元件後，您就可以在網站頁面的製作例項中使用它。

## 新增及設定Forms Portal元件 {#configure-forms-portal-components}

您可以新增及設定入口網站元件，以在使用AEM製作的網站上建立和自訂Forms Portal。 確保 [元件已啟用](#enable-forms-portal-components) 在Forms入口網站中使用。

若要新增元件，請從「元件」窗格將元件拖放至頁面上的配置容器，或點選配置容器上的新增圖示，然後從「 」新增元件 [!UICONTROL 插入新元件] 對話框。

### 設定草稿和提交元件 {#configure-drafts-submissions-component}

「草稿與提交」元件會顯示儲存為草稿的表單，以供日後填寫及提交的表單。 若要設定，請點選元件，然後點選 ![配置表徵圖](assets/configure_icon.png). 在 [!UICONTROL 草稿和提交] 對話框，指定標題以指示表單清單為草稿或已提交的表單。 另請選取元件應以卡片或清單格式列出草稿表單或已提交表單。

![草稿圖示](assets/drafts-component.png)

![提交圖示](assets/submission-listing.png)

### 配置Search&amp;Lister元件 {#configure-search-lister-component}

Search &amp; Lister元件可用於列出頁面上的最適化表單，以及在列出的表單上實作搜尋。

![Search和Lister表徵圖](assets/search-and-lister-component.png)

若要設定，請點選元件，然後點選 ![配置表徵圖](assets/configure_icon.png). 此 [!UICONTROL 搜索和Lister] 對話框開啟。

1. 在 [!UICONTROL 顯示] 頁簽，配置以下內容：
   * 在 **[!UICONTROL 標題]**，指定Search &amp; Lister元件的標題。 指示性標題使用戶可以在表單清單中執行快速搜索。
   * 從 **[!UICONTROL 版面]** 清單中，選擇要以卡片或清單格式表示表單的版面。
   * 選擇 **[!UICONTROL 隱藏搜索]** 和 **[!UICONTROL 隱藏排序]** 隱藏搜索並按功能排序。
   * 在 **[!UICONTROL 工具提示]**，提供將游標暫留在元件上時顯示的工具提示。
1. 在 [!UICONTROL 資產資料夾] 頁簽，指定提取表單並列在頁面上的位置。 您可以配置多個資料夾位置。
1. 在 [!UICONTROL 結果] 索引標籤，設定每頁要顯示的表單數量上限。 預設為每頁8份表單。

### 設定連結元件 {#configure-link-component}

連結元件可讓您提供頁面上最適化表單的連結。 若要設定，請點選元件，然後點選 ![配置表徵圖](assets/configure_icon.png). 此 [!UICONTROL 編輯連結元件] 對話框開啟。

1. 在 [!UICONTROL 顯示] 頁簽，提供連結標題和工具提示，以便識別連結所代表的表單。
1. 在 [!UICONTROL 資產資訊] 索引標籤，指定儲存資產的存放庫路徑。
1. 在 [!UICONTROL 查詢參數] 索引標籤，以索引鍵值配對格式指定其他參數。 按一下連結時，會連同表單一併傳遞這些額外參數。

## 使用Adobe Sign設定非同步表單提交 {#configure-asynchronous-form-submission-using-adobe-sign}

您只有在所有收件者皆完成簽署儀式時，才能設定提交最適化表單。 請依照下列步驟，使用Adobe Sign設定。

1. 在製作例項中，在編輯模式中開啟最適化表單。
1. 從左窗格，點選「屬性」圖示並展開 **[!UICONTROL 電子簽名]** 選項。
1. 選擇 **[!UICONTROL 啟用Adobe Sign]**. 會顯示各種設定選項。
1. 在 [!UICONTROL 提交表單] 區段，選取 **[!UICONTROL 每位收件者都完成了簽署儀式]** 選項來設定「提交表單」動作，其中表單會先傳送給所有收件者以進行簽署。 所有收件者簽署表單後，表單才會提交。

## 將適用性Forms儲存為草稿 {#save-adaptive-forms-as-drafts}

您可以將表單儲存為草稿，以便稍後完成。 將表單另存為草稿的方式有兩種：
* 在表單元件上建立「儲存表單」規則，例如按鈕。 按一下按鈕時，規則觸發，表單會儲存草稿。
* 啟用自動儲存功能，可依照指定事件或設定的時間間隔後儲存表單。

### 建立規則以將最適化表單儲存為草稿 {#rule-to-save-adaptive-form-as-draft}

若要在表單元件（例如按鈕）上建立「儲存表單」規則，請遵循下列步驟：

1. 在製作例項中，以編輯模式開啟最適化表單。
1. 從左窗格，點選 ![元件圖示](assets/components_icon.png) 拖動 [!UICONTROL 按鈕] 元件。
1. 點選 [!UICONTROL 按鈕] 元件，然後點選 ![配置表徵圖](assets/configure_icon.png).
1. 點選 [!UICONTROL 編輯規則] 圖示以開啟規則編輯器。
1. 點選 **[!UICONTROL 建立]** 來設定和建立規則。
1. 在 [!UICONTROL 當] 區段中，選取「已點按」，並 [!UICONTROL 然後] 節，選擇「保存表單」選項。
1. 點選 **[!UICONTROL 完成]** 來儲存規則。

### 啟用自動儲存 {#enable-auto-save}

您可以依照下列方式設定最適化表單的自動儲存功能：

1. 在製作例項中，以編輯模式開啟最適化表單。
1. 從左窗格，點選 ![屬性圖示](assets/configure_icon.png) 並擴展 [!UICONTROL 自動儲存] 選項。
1. 選取 **[!UICONTROL 啟用]** 核取方塊以啟用表單的自動儲存。 您可以設定下列項目：
* 依預設， [!UICONTROL 適用性表單事件] 設為「true」，表示表單會在每個事件後自動儲存。
* 在 [!UICONTROL 觸發]，可設定為根據事件發生次數或特定時間間隔後觸發自動儲存。
