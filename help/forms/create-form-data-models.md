---
title: 如何建立表單資料模型？
description: Experience Manager Forms資料整合提供了一個直觀的用戶介面，用於建立和使用表單資料模型。 瞭解如何使用或不使用配置的資料源建立表單資料模型。
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 1f3104d4a986018675f751afa04fe0ed3b7f5c26
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 0%

---

# 建立表單資料模型 {#create-form-data-model}

![資料整合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 資料整合提供了一個直觀的用戶介面，用於建立和使用表單資料模型。 表單資料模型依賴資料源來交換資料；但是，可以建立包含或不包含資料源的表單資料模型。 根據您是否配置了資料源，有兩種方法可以從資料模型建立：

* **使用預配置的資料源**:如中所述，如果已配置資料源 [配置資料源](configure-data-sources.md)，可在建立表單資料模型時選擇它們。 它將從選定資料源中提供的所有資料模型對象、屬性和服務都可用於表單資料模型中。

* **沒有資料源**:如果尚未為表單資料模型配置資料源，則仍然可以在沒有資料源的情況下建立它。 可以使用表單資料模型來建立自適應Forms <!--and interactive communication--> 用樣本資料test。 當資料源可用時，您可以將表單資料模型與資料源綁定，這些資料源會自動反映在關聯的自適應Forms中<!--and interactive communications-->。

>[!NOTE]
>
>您必須是兩者的成員 **fdm作者** 和 **表單用戶** 組以便能夠建立和使用表單資料模型。 聯繫您 [!DNL Experience Manager] 管理員成為組的成員。

## 建立表單資料模型 {#data-sources}

確保已配置了要在表單資料模型中使用的資料源，如中所述 [配置資料源](configure-data-sources.md)。 執行以下操作以基於已配置的資料源建立表單資料模型：

1. 在 [!DNL Experience Manager] 作者實例，導航 **[!UICONTROL Forms>資料整合]**。
1. 點擊 **[!UICONTROL 建立>表單資料模型]**。
1. 在「建立表單資料模型」對話框中：

   * 指定表單資料模型的名稱。
   * (**可選**)指定表單資料模型的標題、說明和標籤。
   * (**只有配置了資料源時才可選和適用**)按一下 **[!UICONTROL 資料源配置]** 欄位，並選擇要使用的資料源的雲服務所在的配置節點。 它將下一頁上可供選擇的資料源清單限制為所選配置節點中可用的資料源清單。 但是， [!DNL Experience Manager] 預設情況下會列出用戶配置檔案資料源。 如果未選擇配置節點，則會列出來自所有配置節點的資料源。

1. 點擊 **[!UICONTROL 下一個]**。

1. (**僅在配置資料源時適用**) **[!UICONTROL 選擇資料源]** 螢幕列出可用資料源（如果有）。 選擇要在表單資料模型中使用的資料源。
1. 點擊 **[!UICONTROL 建立]** 在確認對話框中，點擊 **[!UICONTROL 開啟]** 開啟「表單資料模型」編輯器。

   讓我們查看表單資料模型編輯器UI的不同元件。

   ![一個包含三個資料源的表單資料模型 — REST風格服務， [!DNL Experience Manager] 用戶配置檔案和RDBMS](assets/fdm-ui.png)

   答： **[!UICONTROL 資料源]** 在表單資料模型中列出資料源。 展開資料源以查看其資料模型對象和服務。

   B **[!UICONTROL 刷新資料源定義]** 從配置的資料源中讀取資料源定義中的任何更改，並在表單資料模型編輯器的「資料源」頁籤中更新這些更改。

   C. **[!UICONTROL 模型]** 顯示添加的資料模型對象的內容區域。

   D **[!UICONTROL 服務]** 顯示添加的資料源操作或服務的內容區域。

   E. **[!UICONTROL 工具欄]** 使用表單資料模型的工具。 工具欄顯示更多選項，具體取決於窗體資料模型中選定的對象。

   F. **[!UICONTROL 添加選定項]** 將所選資料模型對象和服務添加到表單資料模型。

有關表單資料模型編輯器以及如何使用它編輯和配置表單資料模型的詳細資訊，請參見 [使用表單資料模型](work-with-form-data-model.md)。

## 更新資料源 {#update}

執行以下操作可將資料源添加到現有表單資料模型或將其更新。

1. 轉到 **[!UICONTROL Forms>資料整合]**，選擇要添加或更新資料源的表單資料模型，然後點擊 **[!UICONTROL 屬性]**。
1. 在「表單資料模型」屬性中，轉到 **[!UICONTROL 更新源]** 頁籤。

   在 **[!UICONTROL 更新源]** 頁籤：

   * 按一下 **[!UICONTROL 上下文感知配置]** 欄位，並選擇要添加的資料源的雲配置所在的配置節點。 如果未選擇節點，則僅駐留在 `global` 點擊時列出節點 **[!UICONTROL 添加源]**。

   * 要添加新資料源，請點擊 **[!UICONTROL 添加源]** 並選擇要添加到表單資料模型的資料源。 配置的所有資料源 `global` 並顯示選定的配置節點（如果有）。

   * 要將現有資料源替換為同一類型的另一個資料源，請點擊 **[!UICONTROL 編輯]** 表徵圖，並從可用資料源清單中選擇。
   * 要刪除現有資料源，請點擊 **[!UICONTROL 刪除]** 表徵圖。 如果在表單資料模型中添加資料源中的資料模型對象，則「刪除」表徵圖將被禁用。

      ![fdm屬性](assets/fdm-properties.png)

1. 點擊 **[!UICONTROL 保存並關閉]** 來保存更新。

>[!NOTE]
>
>在表單資料模型中添加新資料源或更新現有資料源後，請確保在Adaptive Forms中更新綁定引用<!--and interactive communications--> 使用更新的表單資料模型。

## 特定運行模式的上下文感知配置 {#runmode-specific-context-aware-config}

[!UICONTROL 窗體資料模型] 利用 [吊帶上下文感知配置](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) 支援不同的資料源參數，以便與不同的資料源連接 [!DNL Experience Manager] 運行模式。

當 [!UICONTROL 窗體資料模型] 使用雲配置來儲存參數，當通過原始碼管理（Cloud-Manager GIT儲存庫）簽入和部署時，這些參數將為所有運行模式（開發、階段和生產）建立具有相同參數的雲配置。 但是，對於需要為test和生產環境提供不同資料集的使用情形，則我們使用不同資料源參數（例如資料源URL） [!DNL Experience Manager] 運行模式。

要實現此目標，您需要建立包含資料源參數 — 值對的OSGi配置。 這將覆蓋來自 [!UICONTROL 窗體資料模型] 運行時的雲配置。 由於OSGi配置預設支援這些運行模式，因此您可以根據運行模式將資料源參數覆蓋到不同的值。

在中啟用特定於部署的雲配置 [!UICONTROL 窗體資料模型]:

1. 在本地開發實例上建立雲配置。 有關詳細步驟，請參見 [如何配置資料源](/help/forms/configure-data-sources.md)。

1. 將雲配置儲存到檔案系統。
   1. 使用篩選器建立包 `/conf/{foldername}/settings/cloudconfigs/fdm`。 使用相同 `{foldername}` 按 替換 `fdm` 與 `azurestorage` 用於Azure儲存配置。
   1. 生成和下載包。 有關詳細資訊，請參閱 [包操作](/help/implementing/developing/tools/package-manager.md)。

1. 將雲配置整合到 [!DNL Experience Manager] 原型計畫。
   1. 解壓縮下載的包。
   1. 複製 `jcr_root` 資料夾 `ui.content` > `src` > `main` > `content`。
   1. 更新 `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` 包含篩選器 `/conf/{foldername}/settings/cloudconfigs/fdm`。 有關詳細資訊，請參閱 [項目原型的ui.AEMcontent模組](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html)。 當通過CM管道部署此原型項目時，所有環境（或運行模式）上都會安裝相同的雲配置。 要根據環境更改雲配置的欄位（如URL）的值，請使用以下步驟中討論的OSGi配置。

1. 建立Apache Sling上下文感知配置。 要建立OSGi配置：
   1. **在中設定OSGi配置檔案 [!DNL Experience Manager] 原型計畫。**
使用PID建立OSGi工廠配置檔案 
`org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`。 在每個運行模式資料夾下建立具有相同名稱的檔案，其中每個運行模式需要更改值。 有關詳細資訊，請參閱 [為配置OSGi [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations)。

   1. **設定OSGI配置json。** 要使用Apache Sling上下文感知配置覆蓋提供程式：
      1. 論地方發展實例 `/system/console/configMgr`，選擇具有名稱的工廠OSGi配置 **[!UICONTROL Apache Sling上下文感知配置覆蓋提供程式：OSGi配置]**。
      1. 提供說明。
      1. 選擇 **[!UICONTROL 啟用]**。
      1. 在覆蓋下，提供需要根據sling覆蓋語法中的環境更改的欄位。 有關詳細資訊，請參閱 [Apache Sling上下文感知配置 — 覆蓋](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax)。 比如說， `cloudconfigs/fdm/{configName}/url="newURL"`。
通過選擇 **[!UICONTROL +]**。
      1. 選擇 **[!UICONTROL 保存]**。
      1. 要獲取OSGi配置JSON，請按照中的步驟操作 [使用SDK快速啟動生成AEMOSGi配置](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)。
      1. 將JSON放在上一步中建立的OSGi工廠配置檔案中。
      1. 更改 `newURL` 基於環境（或運行模式）。
      1. 要根據運行模式更改機密值，可以使用 [雲管理器API](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) 以後可以在 [OSGi配置](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values)。
當此原型項目通過CM管道部署時，覆蓋將在不同的環境（或運行模式）上提供不同的值。

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] 用戶可以使用加密支援加密密鑰值(有關詳細資訊，請參閱 [配置屬性的加密支援](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) 並將加密文本放在 [上下文感知配置在service pack 6.5.13.0中提供](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config)。

1. 使用選項刷新中的資料源定義來刷新資料源定義 [表單資料模型編輯器](#data-sources) 通過FDM UI刷新FDM快取並獲取最新配置。

## 後續步驟 {#next-steps}

現在，您有一個表單資料模型，其中添加了資料源。 接下來，您可以編輯表單資料模型以添加和配置資料模型對象和服務、添加資料模型對象之間的關聯、編輯屬性、添加自定義資料模型對象和屬性、生成示例資料等。

有關詳細資訊，請參見 [使用表單資料模型](work-with-form-data-model.md)。
