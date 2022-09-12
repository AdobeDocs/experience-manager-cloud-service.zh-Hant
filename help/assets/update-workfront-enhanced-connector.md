---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
source-git-commit: 77aceab8db82082185c931202fc6ea8eee79c11e
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assetsas a Cloud Service] 可讓您更新 [!DNL Workfront for Experience Manager enhanced connector] 從舊版轉換為最新版本。

>[!TIP]
>
>您在搜尋 [!DNL Workfront for Experience Manager enhanced connector] 更新AEM 6.5的檔案？ 按一下 [此處](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


若要更新 [!DNL Workfront for Experience Manager enhanced connector] 至最新版本：

1. 從下載最新版的Enhanced Connector [Adobe軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [存取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 並從Cloud Manager複製AEMas a Cloud Service存放庫。

1. 使用您選擇的IDE開啟複製的Experience Manageras a Cloud Service存放庫。

1. 將在步驟1下載的增強連接器zip檔案置於下列路徑：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >若 `resources` 資料夾不存在，請建立資料夾。

1. 更新父項中的增強連接器版本 `pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version> updated enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

1. 在中更新相依性 `all module pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <scope>system</scope>
         <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

   >[!NOTE]
   >
   >確定您新增 `<scope>` 和 `<systemPath>` 步驟5和步驟6中的相依性。

1. 更新 `pom.xml` 內嵌。 新增 [!DNL Workfront for Experience Manager enhanced connector] 封裝至 `embeddeds` 區段 `pom.xml` 所有子項目。 將更新併入所有模組 `pom.xml`.

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

1. [刪除對Hoodo分佈點的依賴項](remove-external-dependencies.md)，如果有。

1. 將變更推送至存放庫。

1. 將管線運行到 [部署對Cloud Manager的變更](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
