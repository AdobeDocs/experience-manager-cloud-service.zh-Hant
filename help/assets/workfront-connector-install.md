---
title: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
description: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# 安裝 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

在[!DNL Adobe Experience Manager]中具有[!DNL Cloud Service]系統管理員存取許可權的使用者會安裝增強型聯結器。 安裝之前，請先檢閱平台支援和聯結器[&#128279;](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience)的其他必要條件。

>[!IMPORTANT]
>
>自2022年6月起，Adobe已發行新的原生整合，用於將Workfront與Adobe Experience Manager Assets as a Cloud Service連線。 此整合已成為連線這兩個解決方案的必要方法。 日後任何新實施的增強型聯結器（1.9.8及更新版本）都會遭到封鎖，以便將Workfront與AEM Assets as a Cloud Service連線。 如需如何設定此整合的詳細資訊，請參閱[設定Experience Manager Assets as a Cloud Service整合](workfront-connector-configure.md)。

>[!IMPORTANT]
>
>* Adobe僅需要透過認證合作夥伴或[!DNL Adobe Professional Services]來部署及設定[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未透過認證合作夥伴或[!DNL Adobe Professional Services]進行部署與設定，則Adobe不支援此功能。
>
>* Adobe可能會發行[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]的更新，使此聯結器成為多餘的；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
>
>* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請參閱[增強型聯結器安裝指示](workfront-connector-install.md)的步驟5(a)。
>
>* 請參閱Experience Manager Assets增強型聯結器的[Workfront合作夥伴認證測驗](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 如需有關考試的資訊，請參閱[考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。

在安裝聯結器之前，請遵循下列預先安裝步驟：

1. 如果您的AEM as a Cloud Service程式已設定進階網路並啟用IP允許清單，則您需要將Workfront IP新增至此允許清單，以允許事件訂閱和各種API呼叫傳遞到AEM。

   * [Workfront叢集IP](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=zh-Hant#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9)。 若要瞭解[!DNL Workfront]中的IP叢集，請瀏覽至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 系統]** > **[!UICONTROL 客戶資訊]**。

   * [Workfront事件訂閱API IP](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html?lang=zh-Hant)

   >[!IMPORTANT]
   >
   >* 如果您已為方案設定進階網路，且正在使用IP允許清單，則由於增強型Workfront聯結器架構的限制，您還需要將方案輸出IP新增到Cloud Manager中的允許清單。
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* 若要尋找程式的IP，請開啟終端機視窗並執行命令，例如：
   >
   >    ```
   >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
   >    
   >    ```

1. 確定[!DNL Experience Manager]存放庫中不存在下列覆蓋圖。 如果您在這些路徑上預先存在覆蓋圖，則需要移除覆蓋圖，或合併兩者之間的變更差異：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. 此安裝需要在[!DNL Experience Manager]中將Maven專案設定為[!DNL Cloud Service]的知識。 使用下列資源瞭解如何在您的Maven專案中包含協力廠商套件：

   * [在您的Maven專案中包含協力廠商套件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=zh-Hant#including-third-party)。
   * [使用 [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant)部署。

若要在[!DNL Experience Manager]中以[!DNL Cloud Service]的形式安裝附加元件，請遵循下列步驟：

1. 從[Adobe軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)下載增強型聯結器。

1. [存取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=zh-Hant)並從Cloud Manager複製您的AEM as a Cloud Service存放庫。

1. 使用您選擇的IDE開啟複製的AEM as a Cloud Service存放庫。

1. 將步驟1中所下載的增強型聯結器zip檔案放在下列路徑中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果`resources`資料夾不存在，請建立該資料夾。


1. 新增`pom.xml`相依性：

   1. 在父系`pom.xml`中新增相依性。

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
      ```

      >[!NOTE]
      >
      >在將相依性複製到父系`pom.xml`之前，請確定更新增強型聯結器版本號碼。

   1. 在`all module pom.xml`中新增相依性。

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. 新增`pom.xml`個內嵌。 將[!DNL Workfront for Experience Manager enhanced connector]套件新增至您所有子專案之`pom.xml`的`embeddeds`區段。 需要將它內嵌在所有模組`pom.xml`中。

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   內嵌區段的目標設定為`/apps/<path-to-project-install-folder>/install`。 此JCR路徑`/apps/<path-to-project-install-folder>`必須包含在`all/src/main/content/META-INF/vault/filter.xml`檔案的篩選規則中。 存放庫的篩選規則通常衍生自方案名稱。 使用資料夾名稱作為現有規則中的目標。

1. 將變更推送至存放庫。

1. 執行管道以[將變更部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant)。

1. 若要建立系統使用者組態，請在[!DNL Experience Manager]使用者群組中建立`wf-workfront-users`，並將許可權`jcr:all`指派給`/content/dam`。 系統使用者`workfront-tools`會自動建立，且必要的許可權會自動管理。 來自[!DNL Workfront]且使用增強型聯結器的所有使用者都會自動新增為此群組的一部分。

如需將[!DNL Workfront for Experience Manager enhanced connector]從舊版更新為最新版本的資訊，請按一下[這裡](update-workfront-enhanced-connector.md)。

## 將[!DNL Experience Manager]之間的連線設定為[!DNL Cloud Service]與[!DNL Workfront] {#configure-connection}

若要建立與[!DNL Workfront]的連線，請遵循下列步驟：

1. 在[!DNL Experience Manager]中，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Workfront工具組態]**。

1. 在左側面板中選取`workfront-tools`，然後在頁面的右上角區域選取&#x200B;**[!UICONTROL 建立]**&#x200B;選項。

1. 在&#x200B;**[!UICONTROL Workfront連線]**&#x200B;對話方塊中，提供您[!DNL Workfront]部署的必要詳細資料，並選取&#x200B;**[!UICONTROL 連線至Workfront]**&#x200B;選項。 成功連線後，[!DNL Workfront]檔案自訂整合會在[!DNL Workfront]環境中自動建立。

   ![連線[!DNL Experience Manager]和[!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 導覽至&#x200B;**[!UICONTROL 進階]**&#x200B;標籤，並選取選項&#x200B;**[!UICONTROL 為伺服器AEM as a Cloud Service]**。
