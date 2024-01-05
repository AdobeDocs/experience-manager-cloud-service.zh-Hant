---
title: 提交 AEM 連接器
description: 瞭解如何在Adobe Experience Manager (AEM)as a Cloud Service正確參照和部署聯結器。
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# 提交 AEM 連接器

以下提供有用的Adobe Experience Manager (AEM)聯結器提交資訊，並應連同相關文章一起閱讀 [實施](implement.md) 和  [維護](maintain.md) 聯結器。

AEM聯結器列於 [Adobe交換](https://partners.adobe.com/technologyprogram/experiencecloud.html).

在舊版AEM解決方案中， [封裝管理員](/help/implementing/developing/tools/package-manager.md) 可用來在各種AEM執行個體上安裝聯結器。 不過，透過AEMas a Cloud Service，聯結器是在Cloud Manager中的CI/CD流程期間部署。 對於要部署的聯結器，必須在maven專案的pom.xml中引用聯結器。

關於如何將套件包含在專案中，有多種選擇：

1. 合作夥伴的公共存放庫 — 合作夥伴將在可公開存取的maven存放庫中託管內容包
1. 合作夥伴的受密碼保護的存放庫 — 合作夥伴將在受密碼保護的maven存放庫中託管內容包。 另請參閱 [受密碼保護的maven存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/setting-up-project.html#password-protected-maven-repositories) 以取得指示。
1. 套件式成品 — 在此情況下，聯結器套件會在本機包含在客戶的maven專案中。

無論套件的託管位置為何，都必須將套件參照為pom.xml中的相依性（如廠商所提供）。

```xml
<!-- UberJAR Dependency to be added to the project's Reactor pom.xml -->
<dependency>
  <groupId>com.partnername</groupId>
  <artifactId>my-artifact</artifactId>
  <version>V123</version> <!-- use the latest! -->
  <scope>provided</scope>
  <classifier>my_classifier</classifier>
</dependency>
```

如果ISV合作夥伴將聯結器託管在網際網路可存取（例如可存取的Cloud Manager）的maven存放庫中，則ISV應提供存放庫設定，其中 `pom.xml` 可以放置。 原因是因為上述聯結器相依性可以在建置時由Cloud Manager在本機解決。

```xml
<repository>
    <id>the-repository</id>
    <name>The Repository Where the Connector is Hosted</name>
    <url>https://repo.partnername.com/repositories/aem_connector_repo</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

如果ISV合作夥伴選擇將聯結器作為可下載的檔案分發，則ISV應該提供指示。 此指示應說明如何將檔案部署到本機檔案系統Maven存放庫，該存放庫必須作為AEM專案的一部分簽入Git。 這可確保Cloud Manager能夠解析這些依賴項。
