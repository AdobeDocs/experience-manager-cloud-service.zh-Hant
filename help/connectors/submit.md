---
title: 提交 AEM 連接器
description: 提交 AEM 連接器
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 12%

---


提交 AEM 連接器
===========================

以下提供有用的AEM連接器提交資訊，並應與實作與維護連接器的相關文 [章一](implement.md) 起 [閱讀](maintain.md) 。

「AEM連接器」會列在 [Adobe Exchange中](https://partners.adobe.com/exchangeprogram/experiencecloud)。

在先前的AEM解決方案中，Package Manager可用來在各種AEM例項上安裝連接器。 不過，以AEM為雲端服務，在Cloud Manager的CI/CD程式期間會部署連接器。 為了部署連接器，需要在maven專案的pom.xml中參考連接器。

項目中包含各種選項：

1. 合作夥伴的公共儲存庫——合作夥伴將將內容包托管在可公開訪問的主儲存庫中
1. 打包的對象——在本例中，連接器軟體包包括在客戶的主項目中的本地。

無論封裝在何處，都需要像供應商提供的那樣，在pom.xml中將封裝參照為相依性。

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

如果ISV合作夥伴將連接器托管在可訪問Internet（如可訪問Cloud Manager的）主儲存庫上，ISV應提供存放pom.xml的儲存庫配置，以便在構建時（本地和Cloud Manager）解決連接器依賴性（上述）。

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

如果ISV合作夥伴選擇將Connector分發為可下載的檔案，ISV應提供如何將檔案部署至本機檔案系統管理儲存庫（需要在AEM專案中籤入Git）的指示，讓Cloud Manager能夠解決這些相依性。
