---
title: '開發儲存庫結構包   '
description: Adobe Experience Manager作為雲端服務Maven專案需要「資料庫結構子套件」定義，其唯一目的是定義JCR資料庫根目錄，專案的程式碼子套件會部署在此目錄中。
translation-type: tm+mt
source-git-commit: 46d556fdf28267a08e5021f613fbbea75872ef21

---


# 開發儲存庫結構包

將Adobe Experience Manager專案當作雲端服務時，需要儲存庫結構子套件定義，其唯一目的是定義專案程式碼子套件所部署的JCR儲存庫根目錄。 這可確保在Experience manager中安裝包，因為Cloud Service是由JCR資源相依性自動排序的。 缺少相關性可能導致子結構安裝在其父結構之前，因此意外地被刪除，從而破壞部署。

如果您的代碼包部署到代碼包 **未涵蓋的位置** ，則必須在儲存庫結構包中列舉任何上階資源（靠近JCR根的JCR資源），以建立這些依賴項。

![儲存庫結構包](./assets/repository-structure-packages.png)

儲存庫結構軟體包定義軟體包驗證器用於確定「 `/apps` 不受潛在衝突影響」的區域的預期公共狀態，因為這些區域是標準根。

儲存庫結構包中最典型的路徑包括：

+ `/apps` 是系統提供的節點
+ `/apps/cq/...`、 `/apps/dam/...`、 `/apps/wcm/...`和 `/apps/sling/...` 提供共同覆蓋 `/libs`。
+ `/apps/settings` 即共用的上下文感知配置根路徑

請注意，此子包 **不含任何內容** ，僅由定義過濾 `pom.xml` 器根組成。

## 建立儲存庫結構包

要為Maven項目建立儲存庫結構包，請建立新的空Maven子項目，並使用以下內容更新項目元資料 `pom.xml`，以符合父Maven項目。

更新程 `<filters>` 序，以包含您的代碼包部署到的所有JCR儲存庫路徑根目錄。

請務必將此新的Maven子項目添加到父項目列 `<modules>` 表中。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
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
    <artifactId>my-app.repository-structure</artifactId>
    <packaging>content-package</packaging>
    <name>My App - Adobe Experience Manager Repository Structure Package</name>

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
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!-- Common overlay roots -->
                        <filter><root>/apps/sling</root></filter>
                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/dam</root></filter>
                        <filter><root>/apps/wcm</root></filter>

                        <!-- Immutable context-aware configurations -->
                        <filter><root>/apps/settings</root></filter>

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## 引用儲存庫結構包

要使用儲存庫結構包，請通過所有代碼包(部署到的子包 `/apps`)引用它，通過FileVault內容包Maven插件配置Maven項目 `<repositoryStructurePackage>` 。

在和其 `ui.apps/pom.xml``pom.xml`它任何代碼包中，將對項目的儲存庫結構包(#repository-structure-package)配置的引用添加到FileVault包Maven插件中。

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
              <artifactId>my-app.repository-structure</artifactId>
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
        <artifactId>my-app.repository-structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## 多程式碼套件使用案例

較不常見、更複雜的使用案例是支援部署多個代碼包，這些代碼包安裝在JCR儲存庫的相同區域。

例如：

+ 代碼包A部署到 `/apps/a`
+ 代碼包B部署到 `/apps/a/b`

如果未從代碼包A上的代碼包B建立包級別相關性，則代碼包B可以先部署到 `/apps/a`，接著將代碼包B部署到 `/apps/a`，從而刪除先前安裝的代碼包 `/apps/a/b`。

在本例中：

+ 代碼包A應在項目 `<repositoryStructurePackage>` 的儲存庫結構包上定義一個包(該包應具有篩選器 `/apps`)。
+ 代碼包B應在代碼包A `<repositoryStructurePackage>` 上定義一個代碼包，因為代碼包B部署到由代碼包A共用的空間中。

## 錯誤與除錯

如果儲存庫結構包未正確設定，則在Maven build上將報告錯誤：

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

這表示分段代碼套件的篩選清 `<repositoryStructurePackage>` 單中沒 `/apps/some/path` 有列出。

## 其他資源

+ [FileVault Content Package Maven Plug-in](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
