---
title: 提交 AEM 連接器
description: 瞭解如何在AEMas a Cloud Service中正確參考和部署聯結器。
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: 5482e94bc1a2e7524eb699f2ae766ba40c138e91
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 9%

---

提交 AEM 連接器
===========================

以下提供有用的AEM連接器提交資訊，並應與實作與維護連接器的相關文 [章一](implement.md) 起 [閱讀](maintain.md) 。

AEM聯結器列於 [Adobe交換](https://partners.adobe.com/exchangeprogram/experiencecloud).

在舊版AEM解決方案中， [封裝管理員](/help/implementing/developing/tools/package-manager.md) 可用來在各種AEM執行個體上安裝聯結器。 不過，透過AEMas a Cloud Service，聯結器是在Cloud Manager中的CI/CD流程期間部署。 為了部署聯結器，需要在maven專案的pom.xml中參考聯結器。

關於如何將套件包含在專案中，有多種選擇：

1. 合作夥伴的公共存放庫 — 合作夥伴將在可公開存取的maven存放庫中託管內容包
1. 合作夥伴的受密碼保護的存放庫 — 合作夥伴將在受密碼保護的maven存放庫中託管內容包。 另請參閱 [受密碼保護的maven存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=en#password-protected-maven-repositories) 以取得指示。
1. 套件式成品 — 在此情況下，聯結器套件會在本機包含在客戶的maven專案中。

無論套件位於何處，廠商都會在pom.xml中將套件當成相依性來參照。

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

如果ISV合作夥伴將聯結器託管在網際網路可存取（例如可存取的Cloud Manager）的maven存放庫中，則ISV應提供可放置pom.xml的存放庫設定，以便在建置時（本機或透過Cloud Manager）解析聯結器相依性（上述）。

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

如果ISV合作夥伴選擇將聯結器作為可下載檔案分發，則ISV應提供有關如何將檔案部署到本地檔案系統maven存放庫的指示，該存放庫需要作為AEM專案的一部分簽入Git，以便Cloud Manager能夠解析這些依賴項。
