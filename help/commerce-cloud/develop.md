---
title: 發展AEM商業AEM做為Cloud Service
description: 瞭解如何使用專案原型產生AEM具商務功能AEM的專案。 瞭解如何使用Cloud ServiceSDK來建立專案並部署至本AEM機開發環境。
topics: Commerce, Development
feature: 商務整合框架
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
translation-type: tm+mt
source-git-commit: 97574c964e757ffa4d108340f6a4d1819050d79a
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 10%

---

# 開AEM發商AEM務作為Cloud Service{#develop}

以商AEM務整合框架(CIF)為Cloud Service開發商務專AEM案時，也會遵循與其他專案相AEM同的規AEM則和最佳實務。 請先閱讀以下內容：

- [AEM 專案結構](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service 開發方針](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## 以Cloud ServiceSDK AEM {#local}的身分進行本機開發

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建議在當地開發環境下與CIF項目合作。 作為Cloud Service提供的CIF附AEM加設備也可用於當地開發。 它可從[軟體分發入口](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載。

CIF Add-On是以Sling Feature封存檔的形式提供。 Software Distribution Portal上提供的zip檔案包含兩個Sling Feature封存檔，一個用於作AEM者，一個用於AEM發佈例項。

**AEM as a Cloud Service 的新手嗎？** 請參閱 [使用Cloud ServiceSDK來設定本機開發環境的更AEM詳細指南](https://docs.adobe.com/content/help/zh-Hant/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)。

### 所需軟體

本機應安裝下列程式碼：

- [AEM做為Cloud ServiceSDK](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 或更新版本)
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 訪問CIF附加模組

CIF附加元件可從[軟體散發入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載為zip檔案。 zip檔案包含CIF附加元件為&#x200B;**Sling Feature封存**，它不是AEM套件。 請注意，SDK清單的存取權限僅限於具AEM有Cloud Service授權的使用者。

>[!TIP]
>
>請務必使用最新的CIF附加元件版本。

### 本地設定

若要進行本機CIF附加元件開發，請使AEM用Cloud ServiceSDK:

1. 取得最新AEM版Cloud ServiceSDK
1. 解壓縮AEM.jar以建立`crx-quickstart`資料夾，請運行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立`crx-quickstart/install`資料夾
1. 將CIF附加元件的正確Sling Feature封存檔案檔案複製至`crx-quickstart/install`檔案夾。

   CIF附加郵遞區號檔案包含兩個Sling Feature封存檔`.far`檔案。 請務必針對AEM作者或AEM Publish使用正確的AEM Author或AEM Publish，視您打算如何以Cloud ServiceSDK的身分AEM執行本機。

1. 建立一個名為`COMMERCE_ENDPOINT`的本地OS環境變數，其中保存MagentoGraphQL端點。

   範例Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   示例Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   此變數可用AEM來連線至您的商務系統。 此外，CIF附加元件包含本機反向代理，讓Commerce GraphQL端點可在本機使用。 CIF製作工具（產品主控台和挑選器）和CIF用戶端元件直接呼叫GraphQL時，都會使用這個工具。

   此變數也必須設AEM定為Cloud Service環境。 有關變數的詳細資訊，請參見[將OSGi配置AEM為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. （可選）若要啟用分段目錄功能，您必須為Magento例項建立整合Token。 請依照[快速入門](./getting-started.md#staging)中的步驟建立Token。

   將名稱為`COMMERCE_AUTH_HEADER`的OSGi密碼設定為以下值：

   ```xml
   Authorization: Bearer <Access Token>
   ```

   有關機密的詳細資訊，請參見[將OSGi配置AEM為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. 開始AEM為Cloud ServiceSDK

>[!NOTE]
>
>請確定您在AEM步驟5中設定的Cloud Service變數，在相同的終端視窗中以SDK的身分開始。 如果您是在單獨的終端窗口中啟動它，或按兩下。jar檔案，請確保環境變數可見。

通過OSGI控制台驗證設定： `http://localhost:4502/system/console/osgi-installer`。 清單中應包含CIF附加元件相關的組合、內容封裝和OSGI組態，如特徵模型檔中所定義。

## 項目設定{#project}

有兩種方法可以引導您的CIF項目AEM作為Cloud Service。

### 使用AEM專案原型

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)是引導預配置項目以開始使用CIF的主要工具。 CIF核心元件和所有必需的配置都可以包含在生成的項目中，並附加一個選項。

>[!TIP]
>
>使用[AEM Project Archetype 24或更新版本](https://github.com/adobe/aem-project-archetype/releases)產生專案。

請參AEM閱項目原型[使用說明](https://github.com/adobe/aem-project-archetype#usage)，瞭解如何生成項AEM目。 要將CIF包括在項目中，請使用`includeCommerce`選項。

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

CIF核心元件可以通過包括提供的`all`包或單獨使用CIF內容包和相關OSGI包來用於任何項目。 要手動將CIF核心元件添加到項目，請使用以下相關性：

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
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

### 使用AEMVenia Reference Store

啟動CIF項目的第二個選擇是克隆並使用[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)。 Venia Reference StoreAEM是範例參考店面應用程式，示範CIF核心元件的使用AEM方式。 它是一組最佳實務範例，是開發您自己功能的潛在起點。

若要開始使用Venia Reference Store，只需仿製Git儲存庫，然後開始根據您的需求自訂專案。

>[!NOTE]
>
>Venia Reference Store專案包含兩個建置設定檔，AEM做為Cloud Service和AEM6.5。請查看[專案readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)以瞭解其使用方式。

## 其他資源

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [軟體散發入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
