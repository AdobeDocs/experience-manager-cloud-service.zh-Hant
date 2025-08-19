---
title: 為AEM as a Cloud Service開發AEM Commerce
description: 瞭解如何使用AEM專案原型產生啟用AEM的商務專案。 瞭解如何使用AEM as a Cloud Service SDK建立專案並將其部署至本機開發環境。
topics: Commerce, Development
feature: Commerce Integration Framework
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
index: false
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 5%

---


# 為AEM as a Cloud Service開發AEM Commerce {#develop}

以AEM (CIF)為基礎，針對AEM as a Cloud Service開發Commerce integration framework Commerce專案，會遵循與AEM as a Cloud Service上其他AEM專案相同的規則和最佳作法。 請先檢閱下列內容：

* [AEM 專案結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md)
* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [AEM as a Cloud Service 開發指導方針](/help/implementing/developing/introduction/development-guidelines.md)

## 使用AEM as a Cloud Service SDK進行本機開發 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建議使用本機開發環境與CIF專案搭配使用。 為AEM as a Cloud Service提供的CIF附加元件也可用於本機開發。 可從[軟體發佈入口網站下載。](/help/implementing/developing/tools/package-manager.md#software-distribution)

CIF附加元件以Sling功能封存的形式提供。 軟體發佈入口網站上的zip檔案包含兩個Sling功能封存檔案，一個用於AEM作者，另一個用於AEM發佈執行個體。

>[!TIP]
>
>**剛開始使用AEM as a Cloud Service？**
>>檢視[使用AEM as a Cloud Service SDK設定本機開發環境的詳細指南。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)

### 必要的軟體 {#required-software}

下列專案應在本機安裝：

* [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
* [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 或更新版本)
* [Node.js v10+](https://nodejs.org/en)
* [npm 6+](https://www.npmjs.com/)
* [Git](https://git-scm.com/)

### 存取CIF附加元件 {#accessing-add-on}

可以從[軟體發佈入口網站下載CIF附加元件的ZIP檔案。](/help/implementing/developing/tools/package-manager.md) zip檔案包含CIF附加元件做為&#x200B;**Sling功能封存**，它不是AEM套件。 可使用SDK授權存取AEM as a Cloud Service清單。

>[!TIP]
>
>請務必使用最新的CIF附加元件版本。

### 本機設定 {#local-setup}

對於使用CIF SDK的本機AEM as a Cloud Service附加元件開發，請執行以下步驟：

1. 取得最新的AEM as a Cloud Service SDK。
1. 解壓縮AEM .jar，以便建立`crx-quickstart`資料夾。 執行以下命令：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立`crx-quickstart/install`資料夾。
1. 將CIF附加元件的正確Sling功能封存檔案複製到`crx-quickstart/install`資料夾。

   * CIF附加元件zip檔案包含兩個Sling功能封存`.far`檔案。
   * 請確保對AEM Author或AEM Publish使用正確的套裝，端視您計畫執行本機AEM as a Cloud Service SDK的方式而定。

1. 建立名為`COMMERCE_ENDPOINT`的本機OS環境變數，其中包含Adobe Commerce GraphQL端點。

   * AEM使用此變數來連線至您的商務系統。 CIF附加元件包含本機反向Proxy，可讓Commerce GraphQL端點在本機可用。 此Proxy可供CIF編寫工具（產品主控台和選擇器）以及進行直接GraphQL呼叫的CIF使用者端元件使用。

   * 此外，亦必須針對AEM as a Cloud Service環境設定此變數。 如需變數的詳細資訊，請參閱[為AEM as a Cloud Service設定OSGi。](/help/implementing/deploying/configuring-osgi.md#local-development)

   * macOS下的範例：

     ```bash
     export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

   * Windows下的範例：

     ```bash
     set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

1. （選用）若要啟用分階段目錄功能，您必須為Adobe Commerce執行個體建立整合權杖。 請依照[快速入門](/help/commerce-cloud/cif-storefront/getting-started.md#staging)中的步驟來建立權杖。

   * 將名稱為`COMMERCE_AUTH_HEADER`的OSGi密碼設定為下列值：

     ```xml
     Authorization: Bearer <Access Token>
     ```

   * 如需秘密的詳細資訊，請參閱[為AEM as a Cloud Service設定OSGi。](/help/implementing/deploying/configuring-osgi.md#local-development)

1. 啟動AEM as a Cloud Service SDK。

>[!NOTE]
>
>請務必在步驟5中設定環境變數的相同終端機視窗中啟動AEM as a Cloud Service SDK。 如果您在單獨的終端機視窗中啟動它，或連按兩下.jar檔案，請確定環境變數是可見的。

透過OSGi主控台驗證安裝： `http://localhost:4502/system/console/osgi-installer`。 此清單應包含功能模型檔案中定義的CIF附加元件相關組合、內容套件和OSGi設定。

## 專案設定 {#project}

有兩種方法可針對AEM as a Cloud ServiceBootstrap您的CIF專案。

### 使用AEM專案原型 {#project-archetype}

[AEM專案原型](https://github.com/adobe/aem-project-archetype)是Bootstrap預先設定專案以開始使用CIF的主要工具。 CIF核心元件和所有的必要設定都可以包含在產生的專案中，外加一個選項。

>[!TIP]
>
>請一律使用最新版的[AEM專案原型](https://github.com/adobe/aem-project-archetype/releases)，以便產生專案。

請參閱AEM專案原型[使用指示](https://github.com/adobe/aem-project-archetype#usage)，瞭解如何產生AEM專案。 若要將CIF納入專案中，請使用`includeCommerce`選項。

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

CIF核心元件可透過包含提供的`all`套件或單獨使用CIF內容套件和相關OSGi套件組合來用於任何專案。 若要手動將CIF核心元件新增至專案，請使用下列相依性：

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

### 使用AEM Venia Reference Store {#venia-reference}

啟動CIF專案的第二個選項是複製並使用[AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia Reference Store是參考店面應用程式範例，可示範AEM的CIF核心元件的使用情形。 其目的是作為一組最佳實務範例，以及開發您自己的功能的潛在起點。

若要開始使用Venia參考存放區，請複製Git存放庫，並開始根據您的需求自訂專案。

>[!NOTE]
>
>Venia Reference Store專案包含AEM as a Cloud Service和AEM 6.5的兩個組建設定檔。請檢查[專案readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)，以便瞭解其使用方式。

## 其他資源 {#additional-resources}

* [AEM專案原型](https://github.com/adobe/aem-project-archetype)
* [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
* [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
