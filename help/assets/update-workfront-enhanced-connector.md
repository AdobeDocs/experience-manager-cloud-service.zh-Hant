---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assetsas a Cloud Service] 可讓您更新 [!DNL Workfront for Experience Manager enhanced connector] 從舊版更新至最新版本。

>[!TIP]
>
>您是否在搜尋 [!DNL Workfront for Experience Manager enhanced connector] AEM 6.5的更新檔案？ 按一下 [此處](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


若要更新 [!DNL Workfront for Experience Manager enhanced connector] 至最新版本：

1. 從下載最新版本的增強型聯結器 [AdobeSoftware Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [存取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 並從Cloud Manager複製您的AEMas a Cloud Service存放庫。

1. 使用您選擇的IDE開啟複製的Experience Manageras a Cloud Service存放庫。

1. 將步驟1中所下載的增強型聯結器zip檔案放在下列路徑中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果 `resources` 資料夾不存在，請建立該資料夾。

1. 更新父項中的增強型聯結器版本 `pom.xml`.

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

1. 更新中的相依性 `all module pom.xml`.

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
   >確定您新增 `<scope>` 和 `<systemPath>` 至步驟5和步驟6中的相依性。

1. 更新 `pom.xml` 內嵌。 新增 [!DNL Workfront for Experience Manager enhanced connector] 封裝到 `embeddeds` 的區段 `pom.xml` 您的所有子專案的。 在所有模組中合併更新 `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   內嵌區段的目標設為 `/apps/<path-to-project-install-folder>/install`. 此JCR路徑 `/apps/<path-to-project-install-folder>` 必須包含在中的篩選規則 `all/src/main/content/META-INF/vault/filter.xml` 檔案。 存放庫的篩選規則通常衍生自方案名稱。 使用資料夾名稱作為現有規則中的目標。

1. [移除Hoodoo散發點上的相依性](remove-external-dependencies.md)，如果有的話。

1. 將變更推送至存放庫。

1. 執行管道至 [將變更部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
