---
title: 'AEM 專案存放庫結構套件  '
description: Adobe Experience Manager as a Cloud ServiceMaven項目需要儲存庫結構子包定義，其唯一目的是定義項目的代碼子包部署到的JCR儲存庫根。
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 9%

---

# AEM 專案存放庫結構套件

Adobe Experience Manager as a Cloud Service的Maven項目需要儲存庫結構子包定義，其唯一目的是定義項目代碼子包部署到的JCR儲存庫根。 這確保在Experience Manageras a Cloud Service中安裝軟體包按JCR資源依賴項自動排序。 缺少依賴項可能導致子結構在其父結構之前安裝，因此意外地被刪除，從而中斷部署。

如果您的代碼包部署到代碼包 **未涵蓋的位置** ，則必須在儲存庫結構包中列舉任何上階資源 (靠近JCR根的JCR資源)，以建立這些依賴項。

![儲存庫結構包](./assets/repository-structure-packages.png)

儲存庫結構包定義的 `/apps` 包裝驗證器用於確定「不受潛在衝突影響」的區域，因為它們是標準根。

儲存庫結構包中包含的最典型路徑是：

+ `/apps` 是系統提供的節點
+ `/apps/cq/...`。 `/apps/dam/...`。 `/apps/wcm/...`, `/apps/sling/...` 提供共用的疊層 `/libs`。
+ `/apps/settings` 共用上下文感知配置根路徑

請注意，此子包 **沒有** 內容，且僅由 `pom.xml` 定義篩選器根。

## 建立儲存庫結構包

要為Maven項目建立儲存庫結構包，請建立一個新的空Maven子項目，具有以下內容 `pom.xml`，更新項目元資料以符合您的父Maven項目。

更新 `<filters>` 要包括您部署到的代碼包的所有JCR儲存庫路徑根目錄。

確保將此新Maven子項目添加到父項目 `<modules>` 清單框。

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

要使用儲存庫結構包，請通過所有代碼包（部署到的子包）引用它 `/apps`)通過FileVault內容包Maven插件進行項目管理 `<repositoryStructurePackage>` 配置。

在 `ui.apps/pom.xml`，以及任何其他代碼包 `pom.xml`s，將對項目的儲存庫結構包(#repository-structure-package)配置的引用添加到FileVault包Maven插件。

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

## 多代碼包使用案例

一個不太常見、也比較複雜的使用情形是支援部署安裝在JCR儲存庫相同區域的多個代碼包。

例如：

+ 代碼包A部署到 `/apps/a`
+ 代碼包B部署到 `/apps/a/b`

如果未從代碼包A上的代碼包B建立包級別依賴關係，則代碼包B可以首先部署到 `/apps/a`，後跟代碼包B，後面部署到 `/apps/a`，導致刪除以前安裝的 `/apps/a/b`。

在本例中：

+ 代碼包A應定義 `<repositoryStructurePackage>` 在項目的儲存庫結構包上(該包應具有 `/apps`)。
+ 代碼包B應定義 `<repositoryStructurePackage>` 在代碼包A上，因為代碼包B部署到由代碼包A共用的空間中。

## 錯誤和調試

如果儲存庫結構包未正確設定，則在Maven生成時將報告錯誤：

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

這表示分段代碼包沒有 `<repositoryStructurePackage>` 清單 `/apps/some/path` 的子菜單。

## 其他資源

+ [FileVault內容包主插件](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
