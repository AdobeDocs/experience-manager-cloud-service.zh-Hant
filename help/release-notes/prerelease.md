---
title: '"[!DNL Adobe Experience Manager] as a Cloud Service預發行渠道」'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service預發行渠道」'
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] as a Cloud Service預發行渠道 {#prerelease-channel}


## 簡介 {#introduction}

[!DNL Adobe Experience Manager] as a Cloud Service根據上面的時間表，在每月的節奏中提供新功能 [Experience Manager發佈路線圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service)。 為了熟悉計畫在下月上市的功能，客戶可以訂閱預發行渠道，該渠道可通過在標準程式開發環境或任何沙盒程式環境中適當配置來訪問。 客戶可以預覽對站點控制台的更改，並可以根據任何新的預發行API生成代碼。

給定月份的預發行功能清單將發佈在 [月發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

>[!VIDEO](/help/release-notes/assets/prerelease-overview.mp4)

## 如何啟用預發行 {#enable-prerelease}

預發行功能可以通過不同方式體驗：

* 雲環境（標準程式開發環境或任何沙盒程式環境類型）
* 本地SDK

### 雲環境 {#cloud-environments}

要查看雲開發環境的站點控制台中的新功能以及任何項目自定義的結果：

* 使用 [Cloud Manager API的環境變數終結點](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables)的子菜單。 **AEM_釋放_通道** 環境變數到值 **預釋放**。

```
PATCH /program/{programId}/environment/{environmentId}/variables
[
        {
                "name" : "AEM_RELEASE_CHANNEL",
                "value" : "prerelease",
                "type" : "string"
        }
]
```

也可以按照以下說明使用Cloud Manager CLI: [https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)
```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


如果希望將環境恢復為常規（非預發行）通道的行為，則可以刪除該變數或將其設定回其他值

* 或者，您也可以從 [雲管理器UI](/help/implementing/cloud-manager/environment-variables.md)。

### 本地SDK {#local-sdk}

您可以在本地Quickstart SDK的站點控制台中看到新功能，也可以通過讓您的主項目引用預發行版來針對預發行版中的新API執行代碼 `API Jar` 位於馬文中心。 在預發行模式下啟動常規Quickstart SDK，您也可以在本地電腦上看到以下預發行功能：

* 從軟體分發門戶下載SDK並安裝，如中所述 [訪問AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。
* 啟動SDK快速啟動時，請包括參數 `-r prerelease`。
* 值為 *黏* 因此，它只能在第一次啟動時被選中。 重新安裝SDK以更改命令行選項。

由於每月功能AEM版本之間可能有多個維護版本，因此您可以下載這些新SDK並引用多個項目中的新SDK API Jar版本。 維護版本不會添加其他預發行版功能，但可能包括其他較小的更改，如錯誤修復、安全修復和效能增強。
Javadoc將發佈到Maven Central。

要根據預發行SDK生成：

1. 修改maven項目的pom.xml以引用發佈到Maven中心的不同的預發行sdk api jar。 它包含任何用於預發行功能的新Java api，並且對sdk api jar具有依賴性。 它使用相同的版本。

   例如，父pom的依賴關係管理部分引用常規API Jar的代碼段如下：

   ```
   <dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
        </dependency>
   ```

   然後，在模組中使用：

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   為了更改為預發行SDK，只需更改從 `com.adobe.aem:aem-sdk-api` 至 `com.adobe.aem:aem-prerelease-sdk-api` 如下：

   ```
   <dependencyManagement>
    <dependencies>
      <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-prerelease-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
      </dependency>
   <dependencies>
      <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-prerelease-sdk-api</artifactId>
      </dependency>
   ```

   與通常一樣，單個項目可以使用依賴關係。

1. 部署到本地伺服器
1. 如果滿足本地預期，請將代碼提交到開發分支並使用Cloud Manager非生產管道部署到訂閱預發行通道的環境

>[!CAUTION]
> 
> 的 `aem-prerelease-sdk-api` 部署到Stage或Production時，決不能使用ArtifactId。 在通過生產管道部署時始終使用aem-sdk-api。 同樣，引用預發行API的代碼不應通過生產管道部署。

的 [AEMCS SDK生成Analyzer主插件v1.0及更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) 將通過檢查依賴關係來檢測預發行api是否在項目中使用。 如果分析器找到它，它將使用預發行sdk api來分析項目。

## 注意事項 {#considerations}

在預發行渠道方面，需要注意以下幾點：

* 預發行渠道中可能不包括將在下月發佈的某些功能。
* 預發行中的功能經過嚴格的質量保證，旨在使功能完整，而不是貝塔質量。 如果您發現任何問題，請報告它們，正如您懷疑常規版本中的功能存在缺陷時所AEM做的。
* 要確定是否為預發行通道配置了環境，請轉AEM到控制台 **關於** 頁並檢查版AEM本號是否包括 *預釋放* 尾碼，如 ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```。

![關於](/help/release-notes/assets/about.png)
