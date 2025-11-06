---
title: AEM 專案存放庫結構套件
description: Adobe Experience Manager as a Cloud Service上的Maven專案需要存放庫結構子套件定義，其唯一用途是定義專案的程式碼子套件部署到的JCR存放庫根。
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 2%

---

# AEM 專案存放庫結構套件

Adobe Experience Manager as a Cloud Service的Maven專案需要存放庫結構子套件定義，其唯一用途是定義專案的程式碼子套件部署到的JCR存放庫根。 此方法可確保Experience Manager as a Cloud Service中套件的安裝會依JCR資源相依性自動排序。 缺少相依性可能會導致子結構安裝在其父結構之前，因此意外地被移除，中斷部署的情況。

如果您的程式碼套件部署到程式碼套件未涵蓋的位置&#x200B;**&#x200B;**，則必須在存放庫結構套件中列舉任何上階資源（靠近JCR根的JCR資源）。 建立這些相依性需要此程式。

![存放庫結構封裝](./assets/repository-structure-packages.png)

存放庫結構封裝定義了`/apps`的預期一般狀態，封裝驗證器會使用這些狀態來判斷區域「不會發生潛在衝突」，因為這些區域是標準根。

要包含在存放庫結構封裝中的最典型路徑是：

+ `/apps`是系統提供的節點
+ 為`/apps/cq/...`提供一般覆蓋的`/apps/dam/...`、`/apps/wcm/...`、`/apps/sling/...`和`/libs`。
+ `/apps/settings`是共用的內容感知設定根路徑

此子封裝&#x200B;**沒有**&#x200B;任何內容，且僅由定義篩選根目錄的`pom.xml`組成。

## 建立存放庫結構套件

若要為您的Maven專案建立存放庫結構套件，請使用以下`pom.xml`建立空的Maven子專案，更新專案中繼資料以符合您的父Maven專案。

更新`<filters>`以包含您部署程式碼套件的所有JCR存放庫路徑根。

請確定將此新的Maven子專案新增到父專案`<modules>`清單。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- ====================================================================== -->
    <!-- P A R E N T  P R O J E C T  D E S C R I P T I O N                      -->
    <!-- ====================================================================== -->
    <parent>
        <groupId>com.my-company</groupId>
        <artifactId>my-app</artifactId>
        <version>x.x.x</version>
        <relativePath>../pom.xml</relativePath>
    </parent>

    <!-- ====================================================================== -->
    <!-- P R O J E C T  D E S C R I P T I O N                                   -->
    <!-- ====================================================================== -->
    <artifactId>ui.apps.structure</artifactId>
    <packaging>content-package</packaging>
    <name>UI Apps Structure - Repository Structure Package for /apps</name>

    <description>
        Empty package that defines the structure of the Adobe Experience Manager repository the code packages in this project deploy into.
        Any roots in the code packages of this project should have their parent enumerated in the filters list below.
    </description>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.jackrabbit</groupId>
                <artifactId>filevault-package-maven-plugin</artifactId>
                <extensions>true</extensions>
                <properties>
                    <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlay structure, at each level here.

                        For example, adding a new section to the main AEM Tools navigation, necessitates the following rules:

                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/cq/core</root></filter>
                        <filter><root>/apps/cq/core/content</root></filter>
                        <filter><root>/apps/cq/core/content/nav/</root></filter>
                        <filter><root>/apps/cq/core/content/nav/tools</root></filter>


                        Any /apps level Context-aware configurations need to enumerated here. 
                        
                        For example, providing email templates under `/apps/settings/notification-templates/com.day.cq.replication` necessitates the following rules:

                        <filter><root>/apps/settings</root></filter>
                        <filter><root>/apps/settings/notification-templates</root></filter>
                        <filter><root>/apps/settings/notification-templates/com.day.cq.replication</root></filter>
                        -->

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## 參考存放庫結構套件

若要使用存放庫結構套件，請透過FileVault內容套件Maven外掛程式`/apps`設定透過所有程式碼套件（部署到`<repositoryStructurePackage>`的子套件）參考Maven專案。

在`ui.apps/pom.xml`和任何其他程式碼套件`pom.xml`中，將專案的存放庫結構套件(#repository-structure-package)組態的參考新增到FileVault套件Maven外掛程式。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
</build>
<dependencies>
    <!-- Add the dependency for the repository structure package so it resolves -->
    <dependency>
        <groupId>${project.groupId}</groupId>
        <artifactId>ui.apps.structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## 多程式碼套件使用案例

較不常見且較複雜的使用案例是支援部署多個程式碼套件，這些套件安裝在JCR存放庫的相同區域中。

例如：

+ 程式碼套件A部署至`/apps/a`
+ 程式碼套件B部署至`/apps/a/b`

如果未從程式碼套件A上的程式碼套件B建立套件層級相依性，程式碼套件B可能會先部署到`/apps/a`中。 如果接著是程式碼套件A （部署至`/apps/a`），結果會移除先前安裝的`/apps/a/b`。

在此案例中：

+ 程式碼套件A應在專案的存放庫結構套件（應該有`<repositoryStructurePackage>`的篩選器）上定義`/apps`。
+ 程式碼套件B應在程式碼套件A上定義`<repositoryStructurePackage>`，因為程式碼套件B會部署到程式碼套件A共用的空間。

## 錯誤與偵錯

如果存放庫結構套件未正確設定，在Maven構建會報告錯誤：

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

此錯誤表示中斷程式碼封裝的篩選清單中沒有列出`<repositoryStructurePackage>`的`/apps/some/path`。

## 其他資源

+ [FileVault Content Package Maven外掛程式](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
