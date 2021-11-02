---
title: 提交 AEM 連接器
description: 提交 AEM 連接器
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: cf3273af030a8352044dcf4f88539121249b73e7
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 11%

---

提交 AEM 連接器
===========================

以下提供有用的AEM連接器提交資訊，並應與實作與維護連接器的相關文 [章一](implement.md) 起 [閱讀](maintain.md) 。

AEM連接器列於 [AdobeExchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

在先前的AEM解決方案中， [封裝管理員](/help/implementing/developing/tools/package-manager.md) 用來在各種AEM執行個體上安裝連接器。 不過，透過AEMas a Cloud Service，在Cloud Manager的CI/CD程式期間會部署連接器。 為了部署連接器，必須在maven專案的pom.xml中參考連接器。

有多種選項可讓您將套件納入專案中：

1. 合作夥伴的公用存放庫 — 合作夥伴會將內容套件托管於公開存取的Maven存放庫
1. 合作夥伴的受密碼保護的儲存庫 — 合作夥伴將將內容包托管在受密碼保護的Maven儲存庫中。 請參閱 [受密碼保護的maven儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=en#password-protected-maven-repositories) 的說明。
1. 套件 — 在此情況下，連接器封裝會包含在客戶的Maven專案本機中。

無論封裝托管於何處，都需如廠商所提供，在pom.xml中將封裝參照為相依性。

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

如果ISV合作夥伴將連接器托管在網際網路上可訪問（如可訪問的Cloud Manager）的主儲存庫上，則ISV應提供存放pom.xml的儲存庫配置，以便在構建時（本地和Cloud Manager）解決連接器依賴關係（如上）。

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

如果ISV合作夥伴選擇將Connector作為可下載的檔案分發，則ISV應提供有關如何將這些檔案部署到需要作為AEM項目一部分簽入Git的本地檔案系統主儲存庫的說明，以便Cloud Manager能夠解決這些依賴項。
