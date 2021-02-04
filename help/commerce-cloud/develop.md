---
title: 將AEM的AEM Commerce開發為雲端服務
description: 瞭解如何使用AEM專案原型產生具商務功能的AEM專案。 瞭解如何使用AEM做為雲端服務SDK，將專案建立並部署至本機開發環境。
topics: Commerce, Development
feature: Commerce Integration Framework
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: 9d8d7c3c8c1ac3cb843ce74b3ccdb6904bbfaa05
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 7%

---


# 將AEM的AEM Commerce開發為雲端服務{#develop}

以「AEM雲端服務」適用的「商務整合架構」(CIF)為基礎，開發AEM Commerce專案時，也會遵循與AEM上其他AEM專案（如雲端服務）相同的規則和最佳實務。 請先閱讀以下內容：

- [AEM 專案結構](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service 開發方針](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## 將AEM當做雲端服務SDK的本機開發{#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建議在當地開發環境下與CIF項目合作。 針對AEM（雲端服務）環境提供的CIF附加元件也適用於本機開發。 它可從[軟體分發入口](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載。

CIF Add-On是以Sling Feature封存檔的形式提供。 Software Distribution Portal上提供的zip檔案包含兩個Sling Feature封存檔，一個用於AEM作者，一個用於AEM發佈例項。

**您是AEM的新手嗎？** 請參閱更 [詳細的指南，以使用AEM做為雲端服務SDK來設定本機開發環境](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)。

### 所需軟體

本機應安裝下列程式碼：

- [AEM as a Cloud Service SDK](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) （3.3.9或更新版本）
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 訪問CIF附加模組

CIF附加元件可從[軟體散發入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載為zip檔案。 zip檔案包含CIF附加元件為&#x200B;**Sling Feature封存**，不是AEM套件。 請注意，SDK清單的存取權限僅限AEM為雲端服務授權的使用者。

>[!TIP]
>
>請務必使用最新的CIF附加元件版本。

### 本機設定

若是使用AEM做為雲端服務SDK進行本機CIF附加元件開發，請執行下列步驟：

1. 取得最新的AEM作為雲端服務SDK
1. 解壓縮AEM .jar以建立`crx-quickstart`資料夾，執行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立`crx-quickstart/install`資料夾
1. 將CIF附加元件的正確Sling Feature封存檔案檔案複製至`crx-quickstart/install`檔案夾。

   CIF附加郵遞區號檔案包含兩個Sling Feature封存檔`.far`檔案。 請務必針對AEM作者或AEM Publish使用正確的AEM，視您計畫如何以雲端服務SDK的形式執行本機AEM而定。

1. 建立一個名為`COMMERCE_ENDPOINT`的本地OS環境變數，其中保存Magento GraphQL端點。

   範例Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   示例Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   AEM會使用此變數來連線至您的商務系統。 此外，CIF附加元件還包括本地反向代理，使Magento GraphQL端點在本地可用。 CIF製作工具（產品主控台和挑選器）和CIF用戶端元件直接呼叫GraphQL時，都會使用這個工具。

   此變數也必須設定為AEM的雲端服務環境。 如需變數的詳細資訊，請參閱[將AEM的OSGi設定為雲端服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. （可選）若要啟用分段目錄功能，您必須為Magento例項建立整合Token。 請依照[快速入門](./getting-started.md#staging)中的步驟建立Token。

   將名稱為`COMMERCE_AUTH_HEADER`的OSGi密碼設定為以下值：

   ```xml
   Authorization: Bearer <Access Token>
   ```

   如需有關機密的詳細資訊，請參閱[將AEM的OSGi設定為雲端服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. 以雲端服務SDK形式啟動AEM

通過OSGI控制台驗證設定： `http://localhost:4502/system/console/osgi-installer`。 清單中應包含CIF附加元件相關的組合、內容封裝和OSGI組態，如特徵模型檔中所定義。

## 項目設定{#project}

有兩種方式可引導您的CIF專案，以AEM做為雲端服務。

### 使用AEM Project原型

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)是引導預先設定專案以開始使用CIF的主要工具。 CIF核心元件和所有必需的配置都可以包含在生成的項目中，並附加一個選項。

>[!TIP]
>
>使用[AEM Project Archetype 24或更新版本](https://github.com/adobe/aem-project-archetype/releases)產生專案。

請參閱「AEM專案原型[使用指示](https://github.com/adobe/aem-project-archetype#usage)」，瞭解如何產生AEM專案。 要將CIF包括在項目中，請使用`includeCommerce`選項。

例如：

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=24 \
 -D aemVersion=cloud \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF核心元件可通過包括提供的`all`包或單獨使用CIF內容包和相關OSGI包來用於任何項目。 要手動將CIF核心元件添加到項目，請使用以下相關性：

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### 使用AEM Venia Reference Store

啟動CIF專案的第二個選擇是克隆並使用[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia Reference Store是範例參考店面應用程式，示範CIF核心元件對AEM的使用方式。 它旨在做為一組最佳範例，以及開發您自己功能的潛在起點。

若要開始使用Venia Reference Store，只需仿製Git儲存庫，然後開始根據您的需求自訂專案。

>[!NOTE]
>
>Venia Reference Store專案包含兩個AEM的Cloud Service和AEM 6.5建置設定檔。請查看[專案readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)以瞭解其使用方式。

## 其他資源

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [軟體散發入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
