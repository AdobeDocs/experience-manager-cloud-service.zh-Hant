---
title: 為AEMas a Cloud Service開發AEM Commerce
description: 瞭解如何使用AEM專案原型產生啟用AEM的商務專案。 瞭解如何使用AEMas a Cloud ServiceSDK建置專案並將其部署至本機開發環境。
topics: Commerce, Development
feature: Commerce Integration Framework
version: Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 5%

---

# 為AEMas a Cloud Service開發AEM Commerce {#develop}

根據AEMas a Cloud Service適用的Commerce integration framework(CIF)開發AEM Commerce專案，會遵循與AEMas a Cloud Service上其他AEM專案相同的規則和最佳實務。 請先檢閱下列內容：

- [AEM 專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service 開發方針](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)

## 使用AEMas a Cloud ServiceSDK進行本機開發 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建議使用本機開發環境搭配CIF專案使用。 為CIFas a Cloud Service提供的AEM附加元件也可用於本機開發。 您可從以下網址下載： [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

CIF附加元件以Sling功能封存的形式提供。 軟體發佈入口網站上的zip檔案包含兩個Sling功能封存檔案，一個用於AEM作者，另一個用於AEM發佈執行個體。

**AEM as a Cloud Service 的新手嗎？** 簽出 [有關使用AEMas a Cloud ServiceSDK設定本機開發環境的更詳細指南](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html).

### 必要的軟體

下列專案應在本機安裝：

- [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 或更新版本)
- [Node.js v10+](https://nodejs.org/en)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 存取CIF附加元件

CIF附加元件可從 [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). zip檔案包含CIF附加元件，做為 **Sling功能封存**，它不是AEM套件。 可使用AEMas a Cloud Service授權存取SDK清單。

>[!TIP]
>
>請務必使用最新的CIF附加元件版本。

### 本機設定

對於使用CIFas a Cloud ServiceSDK的本機AEM附加元件開發，請執行以下步驟：

1. 取得最新的AEMas a Cloud ServiceSDK
1. 解壓縮AEM .jar，以便建立 `crx-quickstart` 資料夾，執行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立 `crx-quickstart/install` 資料夾
1. 將CIF附加元件的正確Sling功能封存檔案複製到中 `crx-quickstart/install` 資料夾。

   CIF附加元件zip檔案包含兩個Sling功能封存 `.far` 檔案。 請根據您計畫執行本機AEMas a Cloud ServiceSDK的方式，確定正確地使用AEM Author或AEM Publish的SDK。

1. 建立名為的本機作業系統環境變數 `COMMERCE_ENDPOINT` 保留Adobe Commerce GraphQL端點。

   macOS X範例：

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   範例Windows：

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   AEM使用此變數來連線至您的商務系統。 此外，CIF附加元件包含本機反向Proxy，可讓Commerce GraphQL端點在本機可用。 此Proxy由CIF編寫工具（產品主控台和選擇器）使用，並用於執行直接GraphQL呼叫的CIF使用者端元件。

   此外，此變數必須針對AEMas a Cloud Service環境進行設定。 如需變數的詳細資訊，請參閱 [設定AEM的OSGias a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. （選用）若要啟用分階段目錄功能，您必須為Adobe Commerce執行個體建立整合權杖。 請依照下列步驟操作： [快速入門](./getting-started.md#staging) 以建立Token。

   使用名稱設定OSGi密碼 `COMMERCE_AUTH_HEADER` 變更為下列值：

   ```xml
   Authorization: Bearer <Access Token>
   ```

   如需秘密的詳細資訊，請參閱 [設定AEM的OSGias a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. 啟動AEMas a Cloud ServiceSDK

>[!NOTE]
>
>請務必在步驟5中設定環境變數的相同終端機視窗中啟動AEMas a Cloud ServiceSDK。 如果您在單獨的終端機視窗中啟動它，或連按兩下.jar檔案，請確定環境變數是可見的。

透過OSGI主控台驗證設定： `http://localhost:4502/system/console/osgi-installer`. 此清單應包含功能模型檔案中定義的CIF附加元件相關組合、內容套件和OSGI設定。

## 專案設定 {#project}

針對AEMas a Cloud ServiceBootstrapCIF專案有兩種方式。

### 使用AEM專案原型

此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 是Bootstrap預先設定專案以開始使用CIF的主要工具。 CIF核心元件和所有的必要設定都可包含在產生專案中，並提供一個額外選項。

>[!TIP]
>
>一律使用最新版本的 [AEM專案原型](https://github.com/adobe/aem-project-archetype/releases) 以便您產生專案。

請參閱AEM專案原型 [使用指示](https://github.com/adobe/aem-project-archetype#usage) 產生一個AEM專案。 若要將CIF納入專案中，請使用 `includeCommerce` 選項。

例如：

```bash
mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
 -D archetypeGroupId=com.adobe.aem \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=35 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D includeCommerce=y
```

CIF核心元件可透過包含所提供的用於任何專案 `all` 套件或個別使用CIF內容套件和相關OSGI套件組合。 若要手動將CIF核心元件新增至專案，請使用下列相依性：

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

### 使用AEM Venia Reference Store

啟動CIF專案的第二個選項是複製並使用 [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store是範例參考店面應用程式，可示範AEM的CIF核心元件的使用情形。 其目的是作為一組最佳實務範例，以及開發您自己的功能的潛在起點。

若要開始使用Venia參考存放區，請複製Git存放庫，並開始根據您的需求自訂專案。

>[!NOTE]
>
>Venia Reference Store專案包含AEMas a Cloud Service和AEM 6.5的兩個組建設定檔。檢查 [專案readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) 以便您檢視其使用方式。

## 其他資源

- [AEM專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
- [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
