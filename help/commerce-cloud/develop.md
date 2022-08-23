---
title: 開AEM發商AEM業
description: 瞭解如何使用項目原型AEM生成啟AEM用商業的項目。 瞭解如何使用as a Cloud ServiceSDK構建項目並將其部署到本地AEM開發環境。
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

# 開AEM發商AEM業 {#develop}

基於商AEM務整合框架(CIF)為as a Cloud Service開發商業項AEM目也遵循與其他as a Cloud Service項目相同的規AEM則和最AEM佳做法。 請先查看以下內容：

- [AEM 專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service 開發方針](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## 使用AEMas a Cloud ServiceSDK進行本地開發 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建議採用當地發展環境與CIF項目合作。 為as a Cloud Service提供的CIF附加AEM程式也可供當地開發。 可以從 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。

CIF附加模組作為Sling功能歸檔檔案提供。 軟體分發門戶上可用的zip檔案包括兩個Sling功能存檔檔案，一個用於作AEM者，一個用於發AEM布實例。

**AEM as a Cloud Service 的新手嗎？** 簽出 [使用as a Cloud ServiceSDK設定本地開發環境的更詳細AEM指南](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)。

### 所需軟體

應在本地安裝以下內容：

- [AEMas a Cloud ServiceSDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [爪哇11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 或更新版本)
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [蠢貨](https://git-scm.com/)

### 訪問CIF載入項

CIF載入項可以作為zip檔案從 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。 zip檔案包含CIF載入項為 **Sling功能存檔**，它不是包AEM。 請注意，對SDK清單的訪問限於具有as a Cloud Service許可AEM證的清單。

>[!TIP]
>
>確保始終使用最新的CIF附加版本。

### 本地設定

對於使用as a Cloud ServiceSDK的本地CIF附AEM加開發，請執行以下步驟：

1. 獲取最新AEM的as a Cloud ServiceSDK
1. 解壓縮AEM.jar以建立 `crx-quickstart` 資料夾，運行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立 `crx-quickstart/install` 資料夾
1. 將CIF載入項的正確Sling Feature存檔檔案複製到 `crx-quickstart/install` 的子菜單。

   CIF附加ZIP檔案包含兩個Sling Feature存檔檔案 `.far` 的子菜單。 請確保為AEM作者或AEM發佈使用正確的SDK，具體取決於您計畫如何運行本地AEMas a Cloud ServiceSDK。

1. 建立名為的本地OS環境變數 `COMMERCE_ENDPOINT` 保持Adobe CommerceGraphQL終結點。

   MacOSX示例：

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   示例Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   此變數用於連AEM接到您的商業系統。 此外，CIF載入項包括本地反向代理，使Commerce GraphQL終結點在本地可用。 CIF創作工具（產品控制台和選取器）和執行直接GraphQL調用的CIF客戶端元件均使用此功能。

   還必須為as a Cloud Service環境設AEM置此變數。 有關變數的詳細資訊，請參見 [配置OSGiAEM以as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. （可選）要啟用分段目錄功能，必須為Adobe Commerce實例建立整合令牌。 請按照以下步驟執行 [入門](./getting-started.md#staging) 的子菜單。

   設定名為的OSGi密碼 `COMMERCE_AUTH_HEADER` 值：

   ```xml
   Authorization: Bearer <Access Token>
   ```

   有關機密的詳細資訊，請參見 [配置OSGiAEM以as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. 啟動AEMas a Cloud ServiceSDK

>[!NOTE]
>
>確保在步AEM驟5中設定了環境變數的同一終端窗口中啟動as a Cloud Service的SDK。 如果在單獨的終端窗口中啟動它，或按兩下.jar檔案，請確保環境變數可見。

通過OSGI控制台驗證安裝： `http://localhost:4502/system/console/osgi-installer`。 該清單應包括功能模型檔案中定義的CIF附加包、內容包和OSGI配置。

## 項目設定 {#project}

有兩種方法可以引導您的CIF項目以AEMas a Cloud Service。

### 使用項AEM目原型

的 [項AEM目原型](https://github.com/adobe/aem-project-archetype) 是引導預配置項目以開始使用CIF的主要工具。 CIF核心元件和所有必需的配置都可以包含在生成的項目中，並附加一個選項。

>[!TIP]
>
>始終使用 [項AEM目原型](https://github.com/adobe/aem-project-archetype/releases) 生成項目。

請參閱AEM項目原型 [用法說明](https://github.com/adobe/aem-project-archetype#usage) 如何生成項AEM目。 要將CIF包括到項目中，請使用 `includeCommerce` 的雙曲餘切值。

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

CIF核心元件可用於任何項目，包括提供的 `all` 或單獨使用CIF內容包和相關OSGI包。 要手動將CIF核心元件添加到項目，請使用以下相關項：

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

### 使用AEMVenia引用儲存

啟動CIF項目的第二個選項是克隆和使用 [韋尼AEM亞引用儲存](https://github.com/adobe/aem-cif-guides-venia)。 Venia參AEM考儲存是示例參考儲存應用程式，演示了CIF核心元件的使AEM用。 它旨在作為一組最佳實踐示例和開發您自己的功能的潛在起點。

要開始使用Venia Reference Store，只需克隆Git儲存庫，然後根據需要開始自定義項目。

>[!NOTE]
>
>Venia Reference Store項目包含兩個用於AEMas a Cloud Service和AEM6.5的生成配置檔案。檢查 [項目readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) 看看它們的用途。

## 其他資源

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [韋尼AEM亞引用儲存](https://github.com/adobe/aem-cif-guides-venia)
- [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
