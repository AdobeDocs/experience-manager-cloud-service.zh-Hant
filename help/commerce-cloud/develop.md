---
title: 開發AEM Commerce for AEMas a Cloud Service
description: 了解如何使用AEM專案原型產生啟用商務的AEM專案。 了解如何使用AEM as a Cloud ServiceSDK建立專案並部署至本機開發環境。
topics: Commerce, Development
feature: Commerce Integration Framework
version: Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
source-git-commit: f5e465d90477f1b49e4ff1c5ca9dd47cc5d539bb
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 9%

---

# 開發AEM Commerce for AEMas a Cloud Service {#develop}

根據AEM Integration Framework(CIF)開發AEMas a Cloud Service的AEM商務專案，也會遵循與AEMas a Cloud Service上其他專案相同的規則和最佳實務。 請先查看以下內容：

- [AEM 專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service 開發方針](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## 使用AEM as a Cloud ServiceSDK進行本機開發 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

若要與CIF專案搭配使用，建議使用當地開發環境。 為AEMas a Cloud Service提供的CIF附加元件也適用於當地開發。 可從 [Software Distribution入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

CIF附加元件以Sling功能封存檔形式提供。 Software Distribution入口網站上提供的zip檔案包含兩個Sling Feature封存檔，一個用於AEM作者，另一個用於AEM發佈執行個體。

**AEM as a Cloud Service 的新手嗎？** 結帳 [使用AEM as a Cloud ServiceSDK設定本機開發環境的更詳細指南](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html).

### 所需軟體

應在本機安裝下列項目：

- [AEMas a Cloud ServiceSDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 或更新版本)
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 存取CIF附加元件

CIF附加元件可從 [Software Distribution入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). zip檔案包含CIF附加元件為 **Sling功能封存**，則不是AEM套件。 請注意，SDK清單的存取權限僅限於擁有AEMas a Cloud Service授權的使用者。

>[!TIP]
>
>請務必一律使用最新的CIF附加元件版本。

### 本機設定

使用AEMas a Cloud ServiceSDK進行本機CIF附加元件開發，請執行下列步驟：

1. 取得最新AEMas a Cloud ServiceSDK
1. 解壓縮AEM .jar以建立 `crx-quickstart` 資料夾，運行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立 `crx-quickstart/install` 資料夾
1. 將CIF附加元件的正確Sling Feature封存檔案複製到 `crx-quickstart/install` 檔案夾。

   CIF附加zip檔案包含兩個Sling功能封存 `.far` 檔案。 視您計畫如何執行本機AEMas a Cloud ServiceSDK而定，請務必為AEM製作或AEM發佈使用正確的AEM Publish。

1. 建立本機OS環境變數，名為 `COMMERCE_ENDPOINT` 保留Adobe Commerce GraphQL端點。

   範例Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   示例窗口：

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   此變數供AEM用來連線至您的商務系統。 此外，CIF附加元件包含本機反向代理，讓Commerce GraphQL端點可在本機使用。 CIF製作工具（產品主控台和選擇器）及執行直接GraphQL呼叫的CIF用戶端元件都會使用此功能。

   此變數也必須針對AEMas a Cloud Service環境進行設定。 如需變數的詳細資訊，請參閱 [為AEM as a Cloud Service配置OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. （選用）若要啟用分段目錄功能，您必須為Adobe Commerce例項建立整合代號。 請依照 [快速入門](./getting-started.md#staging) 來建立代號。

   以名稱設定OSGi密碼 `COMMERCE_AUTH_HEADER` 值：

   ```xml
   Authorization: Bearer <Access Token>
   ```

   有關機密的詳細資訊，請參閱 [為AEM as a Cloud Service配置OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. 啟動AEMas a Cloud ServiceSDK

>[!NOTE]
>
>請務必在步驟5中設定環境變數的相同終端機視窗中啟動AEMas a Cloud ServiceSDK。 如果您在個別的終端機視窗中啟動，或連按兩下.jar檔案，請確定環境變數可見。

透過OSGI主控台驗證設定： `http://localhost:4502/system/console/osgi-installer`. 清單中應包含CIF附加元件相關套件組合、內容套件和OSGI設定，如功能模型檔案中所定義。

## 專案設定 {#project}

有兩種方式可引導您進行AEMas a Cloud Service的CIF專案。

### 使用AEM專案原型

此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 是引導預先設定專案以開始使用CIF的主要工具。 CIF核心元件和所有必要設定皆可納入產生的專案中，並提供額外選項。

>[!TIP]
>
>請一律使用 [AEM專案原型](https://github.com/adobe/aem-project-archetype/releases) 來產生專案。

請參閱AEM專案原型 [使用說明](https://github.com/adobe/aem-project-archetype#usage) 關於如何產生AEM專案。 若要將CIF納入專案，請使用 `includeCommerce` 選項。

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

CIF核心元件可用於任何專案，方法是納入所提供的 `all` 封裝，或個別使用CIF內容套件和相關OSGI套件組合。 若要手動將CIF核心元件新增至專案，請使用下列相依性：

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

啟動CIF專案的第二個選項是複製並使用 [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store是範例參考店面應用程式，示範AEM的CIF核心元件使用方式。 這是一組最佳實務範例，也是開發您自己功能的潛在起點。

若要開始使用Venia Reference Store，只需複製Git存放庫，然後根據您的需求開始自訂專案即可。

>[!NOTE]
>
>Venia Reference Store專案包含AEM as a Cloud Service和AEM 6.5的兩個建置設定檔。請檢查 [project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) 以了解其使用方式。

## 其他資源

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Software Distribution入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
