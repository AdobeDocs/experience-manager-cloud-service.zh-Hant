---
title: "[!DNL Adobe Experience Manager] as a Cloud Service 發行前通道"
description: "[!DNL Adobe Experience Manager] as a Cloud Service 發行前通道"
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: c2f0b9c904374b5e59ce2b2f268fdd73dfdbfd21
workflow-type: ht
source-wordcount: '805'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 發行前通道 {#prerelease-channel}


## 簡介 {#introduction}

[!DNL Adobe Experience Manager] as a Cloud Service 會根據 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service)每月提供新功能。為了熟悉排定在下個月上線的功能，客戶可以訂閱發行前通道，而透過在標準程式開發環境或任何沙箱程式環境中進行適當設定即可存取該通道。 客戶可以預覽對 Sites 主控台的變更，並可針對任何新的發行前 API 建置程式碼。

特定月份的發行前功能清單發佈在[每月發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)中。

>[!VIDEO](/help/release-notes/assets/prerelease-overview.mp4)

## 如何啟用發行前版本 {#enable-prerelease}

可以透過不同方式體驗發行前功能：

* 雲端環境 (標準程式開發環境或任何沙箱程式環境類型)
* 本機 SDK

### 雲端環境 {#cloud-environments}

要更新雲環境以使用發行前版本，請使用 Cloud Manager 中的環境設定 UI，新增一個新的[環境變數](../implementing/cloud-manager/environment-variables.md)：

1. 瀏覽到您欲更新的「**程式**」>「**環境**」>「**環境設定**」。
1. 新增一個新的[環境變數](../implementing/cloud-manager/environment-variables.md)：

   | 名稱 | 值 | 套用的服務 | 類型 |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | 全部 | 變數 |

1. 儲存變更，環境將重新整理並啟用發行前功能切換。

   ![新環境變數](assets/env-configuration-prerelease.png)


**或者**&#x200B;您可以使用 Cloud Manager API 和 CLI 來更新環境變數：

* 使用 [Cloud Manager API 的環境變數端點](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables)，將 **AEM_RELEASE_CHANNEL**&#x200B;環境變數設定為值 **prerelease**。

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

* 也可以使用 Cloud Manager CLI，如 [https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 的指示

   ```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


如果您希望環境還原為一般 (非發行前) 通道的行為，可以刪除該變數或將其設回不同的值。

### 本機 SDK {#local-sdk}

您可以在本機快速入門 SDK 的 Sites 主控台中查看新功能，並透過讓您的 Maven 專案參照位於 Maven Central 中的發行前版本 `API Jar`，針對發行前版本中的新 API 進行編碼。 您還可以透過在發行前模式下啟動一般快速入門 SDK，在本機電腦上查看這些發行前功能：

* 從軟體散發入口網站下載 SDK 並按照[存取 AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 中所述進行安裝。
* 啟動 SDK 快速入門時，包含引數 `-r prerelease`。
* 值為 *sticky*，因此只能在第一次啟動時選擇。 重新安裝 SDK 以變更命令列選項。

由於每月功能發行之間可能會有多個 AEM 維護版本，因此您可以下載這些新的 SDK 並在 maven 專案中參照新的 SDK API Jar 版本。 維護版本不會新增其他發行前功能，但可能包括其他較小幅的變更，例如錯誤修正、安全性修正和效能增強。
Javadoc 會發佈到 Maven Central。

要對照發行前 SDK 進行建置：

1. 修改您的 Maven 專案的 pom.xml 以參照一個獨特的發行前 sdk api jar，這已發佈到 Maven Central。 它包含用於發行前功能的任何新 Java API，並且具備 sdk api jar 相依性。 它使用相同的版本。

   例如，這裡是參照一般 API Jar 的父系 pom 的相依性管理區段的片段：

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

   然後是模組中的用法：

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   為了變更為發行前 SDK，只需將相依性從 `com.adobe.aem:aem-sdk-api` 變更為 `com.adobe.aem:aem-prerelease-sdk-api`，如下所述：

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

   如同往常，個別專案可以使用相依性。

1. 部署到您的本機伺服器
1. 如果滿意它在本機如預期般運作，將程式碼提交到開發分支並使用 Cloud Manager 非生產管道部署到訂閱發行前通道的環境

>[!CAUTION]
> 
> 部署到階段或生產時絕不能使用 `aem-prerelease-sdk-api` artifactId。 透過生產管道部署時一律使用 aem-sdk-api。同樣，不應透過生產管道部署參照發行前 API 的程式碼。

[AEM CS SDK Build Analyzer Maven 外掛程式 v1.0 及更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)將透過檢查相依性來偵測專案中是否使用了發行前 API。如果分析器有找到，它將使用發行前 sdk api 來分析專案。

## 考量事項 {#considerations}

關於發行前通道，有幾點需要注意：

* 將在下個月發行的某些功能可能不包含在發行前通道中。
* 發行前版本中的功能經過嚴格的品質保證，旨在提供完整的功能而不是測試版品質。如果您發現任何問題，請提報，就像您在懷疑一般 AEM 版本中的功能存在錯誤時所做的。
* 要確定是否為發行前通道設定了環境，請前往 AEM 主控台的「**關於**」頁面並檢查 AEM 版本號碼是否包含&#x200B;*發行前*&#x200B;尾碼，如 ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![關於](/help/release-notes/assets/about.png)
