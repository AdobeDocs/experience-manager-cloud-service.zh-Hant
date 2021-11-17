---
title: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
description: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: d75d9ac16f64b6770fcf35d58474c47c52b1585b
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# 安裝 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

具有管理員存取權的使用者 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 安裝增強型連接器。 安裝之前，請先檢閱平台支援和其他 [連接器的必要條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobe需要部署，並配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services],Adobe不支援。
>
>Adobe可發行 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 這使得該連接器冗餘；如果發生此情況，客戶可能需要從使用此連接器進行轉變。

安裝連接器之前，請遵循以下預安裝步驟：

1. [配置防火牆](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). 了解 [!DNL Workfront]，導覽至 [!UICONTROL 設定] > [!UICONTROL 系統] > [!UICONTROL 客戶資訊].

1. 在Dispatcher上，允許名為的HTTP標題 `authorization`, `username`，和 `apikey`. 允許 `GET`, `POST`，和 `PUT` 請求 `/bin/workfront-tools`.

1. 請確定中不存在下列路徑 [!DNL Experience Manager] 存放庫：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 此安裝需要有相關知識，才能在 [!DNL Experience Manager] as a [!DNL Cloud Service]. 使用下列資源來了解如何在您的Maven專案中包含協力廠商套件：

   * [在您的Maven專案中包含協力廠商套件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [使用部署 [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

若要在中安裝附加元件 [!DNL Experience Manager] as a [!DNL Cloud Service]，請遵循下列步驟：

1. 新增 `pom.xml` 相依性：

   1. 在父項中新增相依性 `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>1.7.4</version>
      </dependency>
      ```

   1. 在所有模組中新增相依性 [!DNL pom.xml].

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
         </dependency>
      ```

1. 新增 `pom.xml` 驗證。

   1. 在adobe-public設定檔的pom.xml中加入下列存放庫設定，以便在建置時（包括本機和Cloud Manager）解析連接器相依性（以上）。 購買授權時，將提供存放庫存取憑證。 需要將憑證新增至伺服器區段中的settings.xml檔案。

      ```XML
      <repository>
         <id>hoodoo-maven</id>
         <name>Hoodoo Repository</name>
         <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
      </repository>
      ```

   1. 建立名為 `./cloudmanager/maven/settings.xml` 在項目根目錄中。 若要支援受密碼保護的Maven存放庫，請參閱 [如何設定專案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md). 此外，還有一個範例 `settings.xml` 檔案供參考。 最後，更新您的本機 `settings.xml` 本地編譯。

      ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
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

1. 要建立系統用戶配置，請建立 `wf-workfront-users` in [!DNL Experience Manager] 使用者群組並指派權限 `jcr:all` to `/content/dam`. 系統用戶 `workfront-tools` 會自動建立，並自動管理所需的權限。 所有用戶來自 [!DNL Workfront] 使用enhanced連接器的使用者會自動新增為此群組的一部分。

## 配置之間的連接 [!DNL Experience Manager] as a [!DNL Cloud Service] 和 [!DNL Workfront] {#configure-connection}

建立連線的方式 [!DNL Workfront]，請遵循下列步驟：

1. 在 [!DNL Experience Manager]，選取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具設定]**.

1. 選擇 `workfront-tools` 在左側面板中，選取 **[!UICONTROL 建立]** 選項。

1. 在 **[!UICONTROL Workfront Connection]** 對話方塊，提供您 [!DNL Workfront] 部署，並選擇 **[!UICONTROL 連線至Workfront]** 選項。 成功連線後， [!DNL Workfront] 檔案自訂整合會自動建立於 [!DNL Workfront] 環境。

   ![Connect [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 導覽至 **[!UICONTROL 進階]** 標籤，然後選取選項 **[!UICONTROL 伺服器AEM是否as a Cloud Service]**.
