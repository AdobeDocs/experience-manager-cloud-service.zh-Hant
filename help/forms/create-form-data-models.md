---
title: 如何建立表單資料模型？
description: Experience Manager Forms資料整合提供直覺式使用者介面，供您建立及使用表單資料模型。 了解如何使用或不使用已設定的資料來源建立表單資料模型。
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

[!DNL Experience Manager Forms] 資料整合提供直覺式使用者介面，供您建立及使用表單資料模型。 表單資料模型依賴資料來源來交換資料；不過，您可以建立表單資料模型時使用或不使用資料來源。 根據您是否已設定資料來源，有兩種從資料模型建立：

* **使用預配置的資料源**:如果您已依照 [設定資料來源](configure-data-sources.md)，您可以在建立表單資料模型時選取它們。 它提供來自選定資料源的所有資料模型對象、屬性和服務，這些資料源可用於表單資料模型中。

* **無資料來源**:如果您尚未為表單資料模型設定資料來源，仍可在沒有資料來源的情況下建立。 您可以使用表單資料模型來製作最適化Forms <!--and interactive communication--> 用樣本資料來測試。 有資料來源可用時，您可以將表單資料模型與資料來源系結，資料來源會自動反映在相關的適用性Forms中<!--and interactive communications-->.

>[!NOTE]
>
>您必須同時是 **fdm-author** 和 **forms-user** 群組，以便建立及使用表單資料模型。 請連絡您的 [!DNL Experience Manager] 管理員成為群組的成員。

## 建立表單資料模型 {#data-sources}

請確定您已設定要在表單資料模型中使用的資料來源，如 [設定資料來源](configure-data-sources.md). 請執行下列操作，根據已配置的資料源建立表單資料模型：

1. 在 [!DNL Experience Manager] 製作例項，導覽至 **[!UICONTROL Forms >資料整合]**.
1. 點選 **[!UICONTROL 建立>表單資料模型]**.
1. 在「建立表單資料模型」對話框中：

   * 指定表單資料模型的名稱。
   * (**可選**)指定表單資料模型的標題、說明和標籤。
   * (**只有在設定資料來源時才可選用且適用**)點選 **[!UICONTROL 資料來源設定]** 欄位，並選取您要使用之資料來源所在之雲端服務的設定節點。 這會將下一頁可供選取的資料來源清單，限制為所選設定節點中可用的資料來源清單。 不過， [!DNL Experience Manager] 預設會列出使用者設定檔資料來源。 如果未選擇配置節點，則會列出來自所有配置節點的資料源。

1. 點選 **[!UICONTROL 下一個]**.

1. (**僅在已設定資料來源時適用**) **[!UICONTROL 選擇資料源]** 畫面會列出可用的資料來源（如果有的話）。 選取您要在表單資料模型中使用的資料來源。
1. 點選 **[!UICONTROL 建立]** 在確認對話方塊上，點選 **[!UICONTROL 開啟]** 開啟「表單資料模型」編輯器。

   讓我們檢閱表單資料模型編輯器UI的不同元件。

   ![表單資料模型，包含三個資料來源 — RESTful服務， [!DNL Experience Manager] 使用者設定檔和RDBMS。](assets/fdm-ui.png)

   答： **[!UICONTROL 資料來源]** 列出表單資料模型中的資料來源。 展開資料源以查看其資料模型對象和服務。

   B. **[!UICONTROL 重新整理資料來源定義]** 從已設定的資料來源擷取資料來源定義中的任何變更，並在「表單資料模型」編輯器的「資料來源」標籤中更新。

   C. **[!UICONTROL 模型]** 顯示已添加資料模型對象的內容區域。

   D. **[!UICONTROL 服務]** 顯示新增資料來源作業或服務的內容區域。

   E. **[!UICONTROL 工具列]** 使用表單資料模型的工具。 工具列會根據表單資料模型中選取的物件顯示更多選項。

   F. **[!UICONTROL 添加選定內容]** 將所選資料模型對象和服務添加到表單資料模型。

如需表單資料模型編輯器以及如何使用表單資料模型來編輯和設定表單資料模型的詳細資訊，請參閱 [使用表單資料模型](work-with-form-data-model.md).

## 更新資料來源 {#update}

請執行下列操作，將資料來源新增或更新至現有的表單資料模型。

1. 前往 **[!UICONTROL Forms >資料整合]**，選擇要添加或更新資料源的「表單資料模型」，然後點選 **[!UICONTROL 屬性]**.
1. 在「表單資料模型」屬性中，前往 **[!UICONTROL 更新源]** 標籤。

   在 **[!UICONTROL 更新源]** 標籤：

   * 點選 **[!UICONTROL 內容感知配置]** 欄位，並選取要新增之資料來源雲端組態所在的設定節點。 若您未選取節點，則雲端設定僅會駐留在 `global` 點選時會列出節點 **[!UICONTROL 添加源]**.

   * 若要新增資料來源，請點選 **[!UICONTROL 添加源]** 並選取要新增至表單資料模型的資料來源。 在中設定的所有資料來源 `global` 並顯示所選配置節點（如果有）。

   * 若要將現有資料來源取代為其他相同類型的資料來源，請點選 **[!UICONTROL 編輯]** 圖示，並從可用資料來源清單中選取。
   * 若要刪除現有的資料來源，請點選 **[!UICONTROL 刪除]** 圖示。 如果在表單資料模型中新增資料來源中的資料模型物件，則會停用「刪除」圖示。

      ![fdm-properties](assets/fdm-properties.png)

1. 點選 **[!UICONTROL 儲存並關閉]** 以儲存更新。

>[!NOTE]
>
>在您新增資料來源或更新表單資料模型中的現有資料來源後，請務必在適用性Forms中更新系結參考<!--and interactive communications--> 使用更新後的表單資料模型。

## 特定執行模式的內容感知設定 {#runmode-specific-context-aware-config}

[!UICONTROL 表單資料模型] 利用 [Sling內容感知設定](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) 以支援不同的資料來源參數，以連線至不同的資料來源 [!DNL Experience Manager] 執行模式。

當 [!UICONTROL 表單資料模型] 使用雲配置來儲存參數，當通過原始碼控制項（Cloud-Manager GIT儲存庫）簽入並部署時，這些參數將為所有運行模式（開發、階段和生產）建立具有相同參數的雲配置。 但是，在測試和生產環境需要不同資料集的使用案例中，我們會針對不同的環境使用資料來源參數（例如資料來源URL） [!DNL Experience Manager] 執行模式。

若要達成此目標，您需建立包含資料來源參數 — 值組的OSGi設定。 這會覆寫同一組 [!UICONTROL 表單資料模型] 雲端設定。 由於OSGi設定預設支援這些執行模式，因此您可以根據執行模式將資料來源參數覆寫為不同的值。

若要啟用部署專屬雲端設定，請在 [!UICONTROL 表單資料模型]:

1. 在本機開發執行個體上建立雲端設定。 如需詳細步驟，請參閱 [如何設定資料來源](/help/forms/configure-data-sources.md).

1. 將雲配置儲存到檔案系統。
   1. 使用篩選器建立套件 `/conf/{foldername}/settings/cloudconfigs/fdm`. 使用相同 `{foldername}` 如步驟1。 和替換 `fdm` with `azurestorage` Azure儲存配置。
   1. 建置和下載套件。 如需詳細資訊，請參閱 [封裝動作](/help/implementing/developing/tools/package-manager.md).

1. 將雲配置整合到 [!DNL Experience Manager] 原型專案。
   1. 將下載的套件解壓縮。
   1. 複製 `jcr_root` 資料夾放入 `ui.content` > `src` > `main` > `content`.
   1. 更新 `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` 包含篩選器 `/conf/{foldername}/settings/cloudconfigs/fdm`. 如需詳細資訊，請參閱 [AEM專案原型的ui.content模組](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). 透過CM管道部署此原型專案時，所有環境（或執行模式）都會安裝相同的雲端設定。 若要根據環境變更雲端設定欄位（例如URL）的值，請使用下列步驟討論的OSGi設定。

1. 建立Apache Sling內容感知設定。 要建立OSGi配置：
   1. **在 [!DNL Experience Manager] 原型專案。**
使用PID建立OSGi工廠配置檔案 
`org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`. 在每個運行模式資料夾下建立具有相同名稱的檔案，其中每個運行模式需要更改值。 如需詳細資訊，請參閱 [為配置OSGi [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **設定OSGI設定json。** 若要使用Apache Sling內容感知設定覆寫提供者：
      1. 論地方開發實例 `/system/console/configMgr`，選擇名稱為的工廠OSGi配置 **[!UICONTROL Apache Sling內容感知設定覆寫提供者：OSGi配置]**.
      1. 提供說明。
      1. 選擇 **[!UICONTROL 已啟用]**.
      1. 在覆寫下方，提供根據sling覆寫語法中的環境需要變更的欄位。 如需詳細資訊，請參閱 [Apache Sling內容感知設定 — 覆寫](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). 例如， `cloudconfigs/fdm/{configName}/url="newURL"`.
可借由選取 **[!UICONTROL +]**.
      1. 選擇 **[!UICONTROL 儲存]**.
      1. 若要取得OSGi設定JSON，請依照 [使用AEM SDK快速入門產生OSGi設定](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. 將JSON放入上一步驟中建立的OSGi工廠組態檔中。
      1. 變更 `newURL` 根據環境（或執行模式）。
      1. 若要根據執行模式變更機密值，可使用 [cloud manager API](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) 之後可在 [OSGi配置](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
透過CM管道部署此原型專案時，覆寫會在不同環境（或執行模式）上提供不同的值。

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] 使用者可使用加密支援來加密機密值(如需詳細資訊，請參閱 [配置屬性的加密支援](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) 並將加密的文字放入 [service pack 6.5.13.0提供內容感知設定](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. 使用選項重新整理資料來源定義(在 [表單資料模型編輯器](#data-sources) 透過FDM UI重新整理FDM快取，並取得最新設定。

## 後續步驟 {#next-steps}

您現在有一個表單資料模型，其中新增了資料來源。 接下來，您可以編輯表單資料模型以添加和配置資料模型對象和服務、添加資料模型對象之間的關聯、編輯屬性、添加自定義資料模型對象和屬性、生成示例資料等。

如需詳細資訊，請參閱 [使用表單資料模型](work-with-form-data-model.md).
