---
title: 如何建立表單資料模型(FDM)？
description: 瞭解如何使用自適應表單或AEM工作流程建立表單資料模型(FDM)，並將資料傳送或擷取到資料來源。
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 1%

---

# 建立表單資料模型(FDM) {#create-form-data-model}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html) |
| AEM as a Cloud Service  | 本文章 |


![資料整合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms]資料整合提供直覺式使用者介面，用於建立和使用表單資料模型。 表單資料模型(FDM)依賴資料來源交換資料；但是，您可以建立具有或不具有資料來源的表單資料模型(FDM)。 根據您是否已設定資料來源，從資料模型建立有兩個方法：

* **使用預先設定的資料來源**：如果您已依照[設定資料來源](configure-data-sources.md)中的說明設定資料來源，則可以在建立表單資料模型(FDM)時選取它們。 它會從選定的資料來源帶入所有資料模型物件、屬性和服務，以供表單資料模型(FDM)使用。

* **沒有資料來源**：如果您尚未設定表單資料模型(FDM)的資料來源，仍可建立沒有資料來源的表單。 您可以使用表單資料模型(FDM)來撰寫最適化Forms <!--and interactive communication-->，並使用範例資料加以測試。 當資料來源可用時，您可以將表單資料模型(FDM)與資料來源繫結，這會自動反映在關聯的調適型Forms<!--and interactive communications-->中。

>[!NOTE]
>
>您必須是&#x200B;**fdm-author**&#x200B;和&#x200B;**forms-user**&#x200B;群組的成員才能建立和使用表單資料模型(FDM)。 請連絡您的[!DNL Experience Manager]管理員以成為群組的成員。

## 建立表單資料模型(FDM) {#data-sources}

請確定您已依照[設定資料來源](configure-data-sources.md)的說明，設定您要用於表單資料模型(FDM)的資料來源。 執行下列作業，根據已設定的資料來源建立表單資料模型(FDM)：

1. 在[!DNL Experience Manager]作者執行個體中，導覽至&#x200B;**[!UICONTROL Forms >資料整合]**。
1. 選取&#x200B;**[!UICONTROL 建立>表單資料模型]**。
1. 在建立表單資料模型對話方塊中：

   * 指定表單資料模型(FDM)的名稱。
   * （**選擇性**）指定表單資料模型(FDM)的標題、說明和標籤。
   * （**選擇性，並只在資料來源已設定時才適用**）選取&#x200B;**[!UICONTROL 資料Source設定]**&#x200B;欄位旁的勾選圖示，並選取您要使用之資料來源的雲端服務所在的設定節點。 它會將下一頁可供選取的資料來源清單，限制在所選設定節點中可供選取的資料來源。 不過，預設會列出任何[!DNL Experience Manager]使用者設定檔資料來源。 如果您未選取組態節點，則會列出所有組態節點的資料來源。

1. 選取&#x200B;**[!UICONTROL 「下一步」]**。

1. （**僅適用於已設定資料來源的情況**） **[!UICONTROL 選取資料來源]**&#x200B;畫面會列出可用的資料來源（如果有的話）。 選取您要在表單資料模型中使用的資料來源。
1. 選取&#x200B;**[!UICONTROL 建立]**，然後在確認對話方塊中選取&#x200B;**[!UICONTROL 開啟]**&#x200B;以開啟表單資料模型編輯器。

   讓我們檢閱表單資料模型編輯器UI的不同元件。

   ![具有三個資料來源的表單資料模型 — RESTful服務、[!DNL Experience Manager]使用者設定檔和RDBMS](assets/fdm-ui.png)

   A. **[!UICONTROL 資料來源]**&#x200B;列出表單資料模型中的資料來源。 展開資料來源以檢視其資料模型物件及服務。

   B. **[!UICONTROL 重新整理資料Source定義]**&#x200B;會從已設定的資料來源擷取資料來源定義的任何變更，並在表單資料模型編輯器的「資料來源」索引標籤中進行更新。

   C. **[!UICONTROL 模型]**&#x200B;顯示新增資料模型物件的內容區域。

   D. **[!UICONTROL 服務]**&#x200B;新增的資料來源作業或服務出現的內容區域。

   E. **[!UICONTROL 工具列]**&#x200B;使用表單資料模型(FDM)的工具。 工具列會根據表單資料模型(FDM)中選取的物件顯示更多選項。

   F. **[!UICONTROL 新增選取的專案]**&#x200B;將選取的資料模型物件和服務新增至表單資料模型。

如需有關表單資料模型編輯器以及如何使用它來編輯和設定表單資料模型(FDM)的詳細資訊，請參閱[使用表單資料模型](work-with-form-data-model.md)。

## 更新資料來源 {#update}

執行下列動作，將資料來源新增或更新至現有的表單資料模型(FDM)。

1. 移至&#x200B;**[!UICONTROL Forms >資料整合]**，選取您要新增或更新資料來源的表單資料模型(FDM)，然後選取&#x200B;**[!UICONTROL 屬性]**。
1. 在表單資料模型屬性中，移至&#x200B;**[!UICONTROL 更新Source]**&#x200B;標籤。

   在&#x200B;**[!UICONTROL 更新Source]**&#x200B;索引標籤中：

   * 在&#x200B;**[!UICONTROL 內容感知設定]**&#x200B;欄位中選取瀏覽圖示，並選取您要新增之資料來源的雲端設定所在的設定節點。 如果您未選取節點，當您選取`global`新增來源&#x200B;**[!UICONTROL 時，只會列出位於]**&#x200B;節點的雲端設定。

   * 若要新增資料來源，請選取&#x200B;**[!UICONTROL 新增來源]**，然後選取要新增至表單資料模型(FDM)的資料來源。 會顯示在`global`中設定的所有資料來源及選取的設定節點（若有的話）。

   * 若要以相同型別的另一個資料來源取代現有的資料來源，請選取資料來源的&#x200B;**[!UICONTROL 編輯]**&#x200B;圖示，然後從可用資料來源清單中選取。
   * 若要刪除現有的資料來源，請選取資料來源的&#x200B;**[!UICONTROL 刪除]**&#x200B;圖示。 如果將資料來源中的資料模型物件加入表單資料模型(FDM)，則「刪除」圖示會停用。

     ![fdm-properties](assets/fdm-properties.png)

1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存更新。

>[!NOTE]
>
>您在表單資料模型(FDM)中新增資料來源或更新現有資料來源後，請務必視情況在使用更新後的表單資料模型(FDM)的最適化Forms<!--and interactive communications-->中更新繫結參考。

## 特定執行模式的內容感知設定 {#runmode-specific-context-aware-config}

[!UICONTROL 表單資料模型(FDM)]利用[Sling內容感知設定](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html)支援不同的資料來源引數，以連線不同[!DNL Experience Manager]執行模式的資料來源。

當[!UICONTROL 表單資料模型(FDM)]使用雲端設定來儲存引數時，這些引數在簽入時透過原始檔控制（Cloud-Manager GIT存放庫）部署，會為所有執行模式（開發、暫存和生產）使用相同的引數來建立雲端設定。 不過，在測試和生產環境需要不同資料集的使用案例中，我們會針對不同的[!DNL Experience Manager]執行模式使用資料來源引數（例如資料來源URL）。

為此，您需要建立包含資料來源引數 — 值組的OSGi設定。 這會在執行階段覆寫來自[!UICONTROL 表單資料模型(FDM)]雲端組態的相同組。 由於OSGi設定預設支援這些執行模式，因此您可以根據執行模式將資料來源引數覆寫為不同的值。

若要在[!UICONTROL 表單資料模型(FDM)]中啟用部署特定的雲端設定：

1. 在本機開發執行個體上建立雲端設定。 如需詳細步驟，請參閱[如何設定資料來源](/help/forms/configure-data-sources.md)。

1. 將您的雲端設定儲存至檔案系統。
   1. 使用篩選器`/conf/{foldername}/settings/cloudconfigs/fdm`建立封裝。 使用與步驟1相同的`{foldername}`。 並以Azure儲存體設定的`fdm`取代`azurestorage`。
   1. 建置並下載套件。 如需詳細資訊，請參閱[封裝動作](/help/implementing/developing/tools/package-manager.md)。

1. 整合[!DNL Experience Manager]原型專案中的雲端設定。
   1. 將下載的套件解壓縮。
   1. 複製「`jcr_root`」資料夾並放置您的「`ui.content` > `src` > `main` > `content`」。
   1. 更新`ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml`以包含篩選器`/conf/{foldername}/settings/cloudconfigs/fdm`。 如需詳細資訊，請參閱AEM專案原型的[ui.content模組](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html)。 透過CM管道部署此原型專案時，相同的雲端設定會安裝在所有環境（或runmodes）上。 若要根據環境變更雲端設定的欄位值（例如URL），請使用以下步驟中討論的OSGi設定。

1. 建立Apache Sling內容感知設定。 若要建立OSGi設定：
   1. **在[!DNL Experience Manager] Archetype專案中設定OSGi設定檔。**
建立PID為`org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`的OSGi Factory組態檔。 在每個執行模式資料夾下建立名稱相同的檔案，其中每個執行模式的值都需要變更。 如需詳細資訊，請參閱[為 [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations)設定OSGi。

   1. **設定OSGI設定json。**&#x200B;若要使用Apache Sling內容感知設定覆寫提供者：
      1. 在本機開發執行個體`/system/console/configMgr`上，選取名稱為&#x200B;**[!UICONTROL Apache Sling內容感知設定覆寫提供者： OSGi設定]**&#x200B;的工廠OSGi設定。
      1. 提供說明。
      1. 選取&#x200B;**[!UICONTROL 已啟用]**。
      1. 在覆寫下，根據sling覆寫語法中的環境，提供需要變更的欄位。 如需詳細資訊，請參閱[Apache Sling內容感知設定 — 覆寫](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax)。 例如，`cloudconfigs/fdm/{configName}/url="newURL"`。
選取**[!UICONTROL +]**&#x200B;可新增多個覆寫。
      1. 選取「**[!UICONTROL 儲存]**」。
      1. 若要取得OSGi設定JSON，請依照[使用AEM SDK快速入門產生OSGi設定](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)中的步驟操作。
      1. 將JSON放在上一步建立的OSGi Factory設定檔案中。
      1. 根據環境（或執行模式）變更`newURL`的值。
      1. 若要根據執行模式變更密碼值，可使用[Cloud Manager API](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties)建立密碼變數，以後可在[OSGi設定](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values)中參照。
透過CM管道部署此原型專案時，覆寫將在不同的環境（或執行模式）上提供不同的值。

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service]使用者可以使用加密支援來加密密碼值，以取得詳細資料，請參閱[設定屬性的encryption支援](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support)，並在[Service Pack 6.5.13.0](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config)中有內容感知設定之後，將加密文字置於值中。

1. 使用在[表單資料模型編輯器](#data-sources)中重新整理資料來源定義的選項來重新整理資料來源定義，透過FDM UI重新整理FDM快取並取得最新組態。

## 後續步驟 {#next-steps}

您現在擁有已新增資料來源的表單資料模型(FDM)。 接下來，您可以編輯表單資料模型(FDM)，以新增及設定資料模型物件與服務、新增資料模型物件之間的關聯、編輯屬性、新增自訂資料模型物件與屬性、產生範例資料等。

如需詳細資訊，請參閱[使用表單資料模型](work-with-form-data-model.md)。


