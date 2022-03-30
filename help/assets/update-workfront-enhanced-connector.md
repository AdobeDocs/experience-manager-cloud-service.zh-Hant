---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
source-git-commit: 34f3cf925a3ea58de176521be459a61f4317eec3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assetsas a Cloud Service] 允許您更新 [!DNL Workfront for Experience Manager enhanced connector] 從上一版本到最新版本。

>[!TIP]
>
>你在搜索 [!DNL Workfront for Experience Manager enhanced connector] 更新AEM6.5文檔？ 按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront)。


更新 [!DNL Workfront for Experience Manager enhanced connector] 至最新版本：

1. 從下載增強連接器的最新版本 [Adobe軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip)。

1. [訪問](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 並從雲管AEM理器克隆as a Cloud Service儲存庫。

1. 使用您選擇的IDE開啟克隆的Experience Manageras a Cloud Service儲存庫。

1. 將在步驟1中下載的增強連接器zip檔案置於以下路徑：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果 `resources` 資料夾不存在，請建立該資料夾。

1. 更新父級中增強的連接器版本 `pom.xml`。

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

1. 更新中的依賴關係 `all module pom.xml`。

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
   >確保添加 `<scope>` 和 `<systemPath>` 步驟5和步驟6中的從屬項。

1. 更新 `pom.xml` 床鋪。 添加 [!DNL Workfront for Experience Manager enhanced connector] 包 `embeddeds` 的下界 `pom.xml` 你的子項目。 將更新納入所有模組 `pom.xml`。

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

1. [刪除對Hoodoo分發點的依賴項](remove-external-dependencies.md)，如果有。

1. 將更改推送到儲存庫。

1. 將管線運行到 [將更改部署到雲管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。
