---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 更新[!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service]可讓您將[!DNL Workfront for Experience Manager enhanced connector]從舊版更新至最新版本。

>[!TIP]
>
>您正在搜尋AEM 6.5的[!DNL Workfront for Experience Manager enhanced connector]更新檔案嗎？ 按一下[這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=zh-Hant##update-enhanced-connector-for-workfront)。


若要將[!DNL Workfront for Experience Manager enhanced connector]更新至最新版本：

1. 從[Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip)下載最新版本的增強型聯結器。

1. [存取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=zh-Hant)並從Cloud Manager複製您的AEM as a Cloud Service存放庫。

1. 使用您選擇的IDE開啟複製的Experience Manager as a Cloud Service存放庫。

1. 將步驟1中所下載的增強型聯結器zip檔案放在下列路徑中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果`resources`資料夾不存在，請建立該資料夾。

1. 更新上層`pom.xml`中的增強型聯結器版本。

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

1. 更新`all module pom.xml`中的相依性。

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
   >請確定您在步驟5和步驟6中將`<scope>`和`<systemPath>`新增到相依性。

1. 更新`pom.xml`內嵌。 將[!DNL Workfront for Experience Manager enhanced connector]套件新增至您所有子專案之`pom.xml`的`embeddeds`區段。 在所有模組`pom.xml`中合併更新。

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

1. [移除Hoodoo散發點上的相依性](remove-external-dependencies.md) （如果有的話）。

1. 將變更推送至存放庫。

1. 執行管道以[將變更部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant)。
