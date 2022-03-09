---
title: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
description: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: a5776453b261e6f4e6c891763934b236bade8f7f
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# 安裝 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

具有管理員訪問權限的用戶 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 安裝增強的連接器。 安裝前，請查看平台支援和其他 [連接器的先決條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)。

>[!IMPORTANT]
>
>Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅通過認證合作夥伴或 [!DNL Adobe Professional Services]。 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services]，它不受Adobe支援。
>
>Adobe可以發佈更新 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使這個連接器冗餘；如果發生這種情況，可能需要客戶從使用此連接器進行過渡。

在安裝連接器之前，請遵循以下預安裝步驟：

1. [配置防火牆](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html)。 瞭解中的IP群集 [!DNL Workfront]，導航 [!UICONTROL 設定] > [!UICONTROL 系統] > [!UICONTROL 客戶資訊]。

1. 在調度程式上，允許HTTP標頭命名 `authorization`。 `username`, `apikey`。 允許 `GET`。 `POST`, `PUT` 請求 `/bin/workfront-tools`。

1. 確保中不存在以下路徑 [!DNL Experience Manager] 儲存庫：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 此安裝需要知識才能在 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。 使用以下資源瞭解如何在Maven項目中包括第三方包：

   * [在Maven項目中包括第三方包](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party)。
   * [部署 [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)。

在中安裝載入項 [!DNL Experience Manager] 作為 [!DNL Cloud Service]，請執行以下步驟：

1. 從下載增強的連接器 [Adobe軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)。

1. [訪問](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 並從雲管AEM理器克隆as a Cloud Service儲存庫。

1. 使用您選AEM擇的IDE開啟克隆的as a Cloud Service儲存庫。

1. 將在步驟1中下載的增強連接器zip檔案置於以下路徑：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果 `resources` 資料夾不存在，請建立該資料夾。


1. 添加 `pom.xml` 依賴項：

   1. 在父項中添加依賴項 `pom.xml`。

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
      >確保在將依賴關係複製到父級之前更新增強的連接器版本號 `pom.xml`。

   1. 在中添加依賴項 `all module pom.xml`。

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. 添加 `pom.xml` 床鋪。 添加 [!DNL Workfront for Experience Manager enhanced connector] 包 `embeddeds` 的下界 `pom.xml` 你的子項目。 需要將它嵌入到所有模組中 `pom.xml`。

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   嵌入節的目標設定為 `/apps/<path-to-project-install-folder>/install`。 此JCR路徑 `/apps/<path-to-project-install-folder>` 必須包含在 `all/src/main/content/META-INF/vault/filter.xml` 的子菜單。 儲存庫的篩選器規則通常從程式名派生。 在現有規則中將資料夾的名稱用作目標。

1. 將更改推送到儲存庫。

1. 將管線運行到 [將更改部署到雲管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。

1. 要建立系統用戶配置，請建立 `wf-workfront-users` 在 [!DNL Experience Manager] 用戶組並分配權限 `jcr:all` 至 `/content/dam`。 系統用戶 `workfront-tools` 自動建立，並自動管理所需權限。 所有用戶 [!DNL Workfront] 使用增強連接器的用戶將自動添加為此組的一部分。

## 配置之間的連接 [!DNL Experience Manager] 作為 [!DNL Cloud Service] 和 [!DNL Workfront] {#configure-connection}

建立與 [!DNL Workfront]，請執行以下步驟：

1. 在 [!DNL Experience Manager]選中 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**。

1. 選擇 `workfront-tools` 在左面板中，然後選擇 **[!UICONTROL 建立]** 的上界。

1. 在 **[!UICONTROL Workfront]** 對話框，提供所需的詳細資訊 [!DNL Workfront] 部署，然後選擇 **[!UICONTROL 連接到Workfront]** 的雙曲餘切值。 成功連接後， [!DNL Workfront] 文檔自定義整合在 [!DNL Workfront] 環境。

   ![連接 [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 導航到 **[!UICONTROL 高級]** 選項 **[!UICONTROL 伺服器AEMas a Cloud Service]**。
