---
title: 'AEM 專案存放庫結構套件  '
description: Adobe Experience Manager as a Maven專案需要存放庫結構子套件定義，其唯一目的是定義JCR存放庫根，專案的程式碼子套件會部署到該根中。
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 9%

---

# AEM 專案存放庫結構套件

Adobe Experience Manager作為Cloud Service的Maven專案需要存放庫結構子套件定義，其唯一目的是定義專案的程式碼子套件部署所在的JCR存放庫根。 這可確保以Experience Manager形式安裝程式包，因為Cloud Service是按JCR資源依賴項自動排序的。 缺少依賴項可能會導致子結構在其父結構之前被安裝，因此意外地被刪除，從而中斷部署。

如果您的代碼包部署到代碼包 **未涵蓋的位置** ，則必須在儲存庫結構包中列舉任何上階資源 (靠近JCR根的JCR資源)，以建立這些依賴項。

![儲存庫結構包](./assets/repository-structure-packages.png)

儲存庫結構包定義了`/apps`的預期公共狀態，包驗證器使用該狀態來確定「不受潛在衝突影響」的區域，因為它們是標準根。

存放庫結構套件中最常包含的路徑為：

+ `/apps` 是系統提供的節點
+ `/apps/cq/...`、  `/apps/dam/...`、  `/apps/wcm/...`和， `/apps/sling/...` 為提供通用覆蓋 `/libs`。
+ `/apps/settings` 是共用的上下文感知配置根路徑

請注意，此子包&#x200B;**不包含**&#x200B;任何內容，且僅由定義篩選根的`pom.xml`組成。

## 建立儲存庫結構包

要為Maven項目建立儲存庫結構包，請建立新的空的Maven子項目，並使用以下`pom.xml`，更新項目元資料以符合父Maven項目。

更新`<filters>`以包含程式碼套件部署到的所有JCR存放庫路徑根。

請務必將此新的Maven子專案新增至父專案`<modules>`清單。

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

要使用儲存庫結構包，請通過`/apps`配置通過FileVault內容包Maven插件`<repositoryStructurePackage>`配置通過所有代碼包（部署到的子包）引用它。

在`ui.apps/pom.xml`和任何其他代碼包`pom.xml`中，將對項目的儲存庫結構包(#repository-structure-package)配置的引用添加到FileVault包Maven插件。

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

+ 代碼包A部署到`/apps/a`中
+ 代碼包B部署到`/apps/a/b`中

如果未從代碼包A上的代碼包B建立包級別依賴關係，則代碼包B可以先部署到`/apps/a`中，然後部署到`/apps/a`中的代碼包B，從而刪除先前安裝的`/apps/a/b`。

在此情況下：

+ 程式碼套件A應在專案的存放庫結構套件上定義`<repositoryStructurePackage>`（應包含`/apps`的篩選器）。
+ 代碼包B應在代碼包A上定義`<repositoryStructurePackage>`，因為代碼包B部署到代碼包A共用的空間中。

## 錯誤和除錯

如果未正確設定存放庫結構套件，在Maven建置時將會回報錯誤：

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

這表示中斷代碼包的篩選器清單中沒有列出`/apps/some/path`的`<repositoryStructurePackage>`。

## 其他資源

+ [FileVault Content Package Maven插件](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
