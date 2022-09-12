---
title: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
description: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 6e1408abde71c5400adaeaea130e4b7f9287169a
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# 安裝 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

具有管理員存取權的使用者 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 安裝增強型連接器。 安裝之前，請先檢閱平台支援和其他 [連接器的必要條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe需要部署，並配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services],Adobe不支援。
>
>* Adobe可發行 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此連接器冗餘；如果發生此情況，客戶可能需要從使用此連接器進行轉變。
>
>* Adobe支援增強的連接器1.7.4版及更新版本。 不支援舊版和自訂版本。 要檢查增強的連接器版本，請參閱 [增強型連接器安裝指示](workfront-connector-install.md).
>
>* 請參閱 [Workfront for Experience Manager Assets enhanced connector的合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有關考試的資訊，請參見 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


安裝連接器之前，請遵循以下預安裝步驟：

1. [配置防火牆](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). 了解 [!DNL Workfront]，導覽至 [!UICONTROL 設定] > [!UICONTROL 系統] > [!UICONTROL 客戶資訊].

1. 在Dispatcher上，允許名為的HTTP標題 `authorization`, `username`，和 `apikey`. 允許 `GET`, `POST`，和 `PUT` 請求 `/bin/workfront-tools`.

1. 請確定中不存在下列路徑 [!DNL Experience Manager] 存放庫：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. 此安裝需要有相關知識，才能在 [!DNL Experience Manager] as a [!DNL Cloud Service]. 使用下列資源來了解如何在您的Maven專案中包含協力廠商套件：

   * [在您的Maven專案中包含協力廠商套件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [使用部署 [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

若要在中安裝附加元件 [!DNL Experience Manager] as a [!DNL Cloud Service]，請遵循下列步驟：

1. 從下載增強的連接器 [Adobe軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [存取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 並從Cloud Manager複製AEMas a Cloud Service存放庫。

1. 使用您選擇的IDE開啟複製的AEMas a Cloud Service存放庫。

1. 將在步驟1下載的增強連接器zip檔案置於下列路徑：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >若 `resources` 資料夾不存在，請建立資料夾。


1. 新增 `pom.xml` 相依性：

   1. 在父項中新增相依性 `pom.xml`.

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
      >將相依性複製到父項之前，請確定更新增強的連接器版本號 `pom.xml`.

   1. 在中新增相依性 `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. 新增 `pom.xml` 內嵌。 新增 [!DNL Workfront for Experience Manager enhanced connector] 封裝至 `embeddeds` 區段 `pom.xml` 所有子項目。 需要將它嵌入到所有模組中 `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   嵌入節的目標設定為 `/apps/<path-to-project-install-folder>/install`. 此JCR路徑 `/apps/<path-to-project-install-folder>` 的篩選規則中 `all/src/main/content/META-INF/vault/filter.xml` 檔案。 存放庫的篩選規則通常衍生自程式名稱。 在現有規則中使用資料夾的名稱作為目標。

1. 將變更推送至存放庫。

1. 將管線運行到 [部署對Cloud Manager的變更](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. 要建立系統用戶配置，請建立 `wf-workfront-users` in [!DNL Experience Manager] 使用者群組並指派權限 `jcr:all` to `/content/dam`. 系統用戶 `workfront-tools` 會自動建立，並自動管理所需的權限。 所有用戶來自 [!DNL Workfront] 使用enhanced連接器的使用者會自動新增為此群組的一部分。

如需更新 [!DNL Workfront for Experience Manager enhanced connector] 從上一版到最新版本，按一下 [此處](update-workfront-enhanced-connector.md).

## 配置之間的連接 [!DNL Experience Manager] as a [!DNL Cloud Service] 和 [!DNL Workfront] {#configure-connection}

建立連線的方式 [!DNL Workfront]，請遵循下列步驟：

1. 在 [!DNL Experience Manager]，選取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具設定]**.

1. 選擇 `workfront-tools` 在左側面板中，選取 **[!UICONTROL 建立]** 選項。

1. 在 **[!UICONTROL Workfront Connection]** 對話方塊，提供您 [!DNL Workfront] 部署，並選擇 **[!UICONTROL 連線至Workfront]** 選項。 成功連線後， [!DNL Workfront] 檔案自訂整合會自動建立於 [!DNL Workfront] 環境。

   ![Connect [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 導覽至 **[!UICONTROL 進階]** 標籤，然後選取選項 **[!UICONTROL 伺服器AEM是否as a Cloud Service]**.
