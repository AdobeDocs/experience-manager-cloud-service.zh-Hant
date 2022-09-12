---
title: AEM 專案存放庫結構套件
description: Adobe Experience Manager as a Cloud Service Maven專案需要存放庫結構子套件定義，其唯一用途是定義專案的程式碼子套件部署所在的JCR存放庫根。
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 9%

---

# AEM 專案存放庫結構套件

適用於Adobe Experience Manager as a Cloud Service的Maven專案需要存放庫結構子套件定義，其唯一目的是定義專案的程式碼子套件部署所在的JCR存放庫根。 這可確保在Experience Manageras a Cloud Service安裝程式包時，按JCR資源依賴項自動排序。 缺少依賴項可能會導致子結構在其父結構之前被安裝，因此意外地被刪除，從而中斷部署。

如果您的代碼包部署到代碼包 **未涵蓋的位置** ，則必須在儲存庫結構包中列舉任何上階資源 (靠近JCR根的JCR資源)，以建立這些依賴項。

![儲存庫結構包](./assets/repository-structure-packages.png)

存放庫結構套件會定義 `/apps` 軟體包驗證器用於確定「不受潛在衝突影響」的區域，因為它們是標準根。

存放庫結構套件中最常包含的路徑為：

+ `/apps` 是系統提供的節點
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...`，和 `/apps/sling/...` 提供通用覆蓋 `/libs`.
+ `/apps/settings` 是共用的上下文感知配置根路徑

請注意，此子包 **沒有** 任何內容，並僅由 `pom.xml` 定義篩選根。

## 建立儲存庫結構包

要為Maven項目建立儲存庫結構包，請建立新的空Maven子項目，具有以下內容 `pom.xml`，更新專案中繼資料以符合您的父項Maven專案。

更新 `<filters>` 納入所有JCR存放庫路徑根，程式碼套件會部署至其中。

請務必將此新的Maven子專案新增至父專案 `<modules>` 清單。

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
                    <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlayed structure, at each level here.

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

## 引用儲存庫結構包

若要使用存放庫結構套件，請透過所有程式碼套件（部署至的子套件）來參照 `/apps`)透過FileVault內容套件Maven外掛程式Maven專案 `<repositoryStructurePackage>` 設定。

在 `ui.apps/pom.xml`，以及任何其他程式碼套件 `pom.xml`將對項目的儲存庫結構包(#repository-structure-package)配置的引用添加到FileVault包Maven插件中。

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

較不常見且更複雜的使用案例，是支援部署多個程式碼套件，這些套件會安裝在JCR存放庫的相同區域中。

例如：

+ 程式碼套件A部署至 `/apps/a`
+ 程式碼套件B部署至 `/apps/a/b`

如果未從程式碼套件A上的程式碼套件B建立程式套件層級相依性，程式碼套件B可先部署至 `/apps/a`，接著程式碼套件B，會部署至 `/apps/a`，導致移除先前安裝的 `/apps/a/b`.

在此情況下：

+ 程式碼套件A應定義 `<repositoryStructurePackage>` 的存放庫結構套件(應包含 `/apps`)。
+ 程式碼套件B應定義 `<repositoryStructurePackage>` 在程式碼套件A上，因為程式碼套件B部署至程式碼套件A共用的空間。

## 錯誤和除錯

如果未正確設定存放庫結構套件，在Maven建置時將會回報錯誤：

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

這表示中斷程式碼套件沒有 `<repositoryStructurePackage>` 清單 `/apps/some/path` 在其篩選清單中。

## 其他資源

+ [FileVault Content Package Maven插件](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
