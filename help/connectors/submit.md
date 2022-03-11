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

連AEM接器列在 [AdobeExchange](https://partners.adobe.com/exchangeprogram/experiencecloud)。

在以前的AEM解決方案中， [包管理器](/help/implementing/developing/tools/package-manager.md) 用於在各種實例上安裝連AEM接器。 但是，在AEMas a Cloud Service的情況下，在Cloud Manager的CI/CD過程中部署連接器。 為了部署連接器，需要在maven項目的pom.xml中引用連接器。

在項目中如何包括軟體包有多種選項：

1. 合作夥伴的公共儲存庫 — 合作夥伴將將內容包托管在可公開訪問的主儲存庫中
1. 合作夥伴的受密碼保護的儲存庫 — 合作夥伴將將內容包托管在受密碼保護的主儲存庫中。 請參閱 [受密碼保護的maven主要儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=en#password-protected-maven-repositories) 的雙曲餘切值。
1. 捆綁的項目 — 在本例中，連接器軟體包包含在客戶的主項目中。

無論包的托管位置如何，都需要按照供應商提供的方法，在pom.xml中將包作為依賴項引用。

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

如果ISV合作夥伴將連接器托管在可訪問網際網路（如可訪問雲管理器）的主儲存庫上，則ISV應提供可放置pom.xml的儲存庫配置，以便在生成時（本地和雲管理器）解決連接器依賴項（以上）。

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

如果ISV合作夥伴選擇將Connector作為可下載檔案分發，則ISV應提供有關如何將檔案部署到本地檔案系統主儲存庫的說明AEM，該儲存庫需要作為項目的一部分簽入Git，以便Cloud Manager能夠解決這些依賴項。
