---
title: Adobe Experience Manager as a Cloud Service 發行前通道
description: 了解如何使用發行前通道來取得即將推出的 AEM as a Cloud Service 功能預覽。
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
feature: Release Information
role: Admin
source-git-commit: e6567c965a026967e7a5baa67050eb5615979531
workflow-type: ht
source-wordcount: '893'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 發行前通道 {#prerelease-channel}

了解如何使用發行前通道來取得即將推出的 AEM as a Cloud Service 功能預覽。

## 簡介 {#introduction}

Adobe Experience Manager as a Cloud Service 定期提供新功能。特定功能發行中新增和即將推出的功能清單會發佈在[發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)中。

通常會透過以下兩種方式之一發行即將推出的功能：

* 作為 Alpha、Beta 或限量開放計畫的一部分
* 透過預發行通道使用

本文件說明如何啟用預發行通道。使用者可以透過預發行通道存取早期功能，而這些功能將成為 AEM 未來的功能版本。您可以藉此驗證新功能，並在未來發行前做好採用該功能的規劃。請參閱文件 [Adobe Experience Manager (AEM) as a Cloud Service 發行說明](/help/release-notes/home.md)，了解 AEM 發行排程的詳細資訊。

## 啟用預發行通道來存取及試用即將推出的功能 {#enable-prerelease}

在任何開發或沙箱環境中皆可啟用預發行通道。在中繼環境或生產環境中無法啟用預發行通道。

有兩種不同的方式可以存取預發行通道：

* [雲端環境](#cloud-environments)
* [本機 SDK](#local-sdk)

### 雲端環境 {#cloud-environments}

若要更新雲端環境以利使用預發行通道，您必須增加一個新的環境變數。您可以使用 Cloud Manager UI 或透過 CLI 執行此操作。

#### 使用 UI 新增環境變數 {#add-with-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 導覽至您要啟用預發行通道的計劃。

1. 選取您要啟用預發行通道的環境，並透過「**計劃** > **環境** > **環境設定**」存取其設定。

1. 新增一個新的[環境變數](/help/implementing/cloud-manager/environment-variables.md)

   | 名稱 | 值 | 套用的服務 | 類型 |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | 全部 | 變數 |

1. 儲存變更後，環境將重新整理並啟用預發行通道。

   ![新環境變數](assets/env-configuration-prerelease.png)

#### 使用 CLI 新增環境變數 {#add-with-cli}

您也可以使用 Cloud Manager API 和 CLI 來更新環境變數。

* 使用 [Cloud Manager API 的環境變數端點](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables)，將 `AEM_RELEASE_CHANNEL` 環境變數設定為值 `prerelease`。

  ```text
  PATCH /program/{programId}/environment/{environmentId}/variables
  [
          {
                  "name" : "AEM_RELEASE_CHANNEL",
                  "value" : "prerelease",
                  "type" : "string"
          }
  ]
  ```

* 也可以使用 [Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)

  ```shell
  aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL "prerelease
  ```

若要將環境還原成標準行為 (非預發行通道)，可刪除該變數。

### 本機 SDK {#local-sdk}

您可以在本機快速入門 SDK 的預發行通道中存取即將推出的功能，並將您的 Maven 專案設定為參照位於 Maven Central 中的預發行通道 `API Jar`，以便針對新 API 編寫程式碼。只要使用預發行模式啟動一般快速入門 SDK，您也可以在本機開發環境中查看和存取這些預發行通道。

#### 使用預發行模式啟動快速入門 SDK {#prerelease-mode}

1. 從軟體分發入口網站下載 SDK 並按照[存取 AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 中所述進行安裝。
1. 啟動 SDK 快速入門時，請包含引數 `-r prerelease`。

值為 sticky，因此只能在第一次啟動時選取它。重新安裝 SDK 以變更命令列選項。

由於每月功能發行之間可能會有多個 AEM 維護版本，因此您可以下載這些新的 SDK 並在 maven 專案中參照新的 SDK API Jar 版本。維護版本不會新增其他發行前功能，但可能包括其他較小幅的變更，例如錯誤修正、安全性修正和效能增強。
Javadoc 會發佈到 Maven Central。

#### 針對發行前 SDK 進行建置 {#build-sdk}

1. 修改您的 Maven 專案的 `pom.xml` 以參照獨特的發行前 SDK API jar，這個檔案已發佈到 Maven Central。它包含用於發行前功能的任何新 Java API，並且相依於 SDK API jar。它使用相同的版本。

   例如，這裡是參照一般 API jar 的父系 pom 的相依性管理區段中的片段：

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

   若要變更為發行前 SDK，只需將相依性從 `com.adobe.aem:aem-sdk-api` 變更為 `com.adobe.aem:aem-prerelease-sdk-api`，如下所述：

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

1. 部署到您的本機伺服器。

1. 如果其本機運作符合預期且您感到滿意，請將程式碼提交到開發分支，並使用 Cloud Manager 非生產管道部署到[啟用預發行通道的環境。](#cloud-environments)

>[!CAUTION]
> 
> 部署到中繼或生產環境時，絕不能使用 `aem-prerelease-sdk-api` artifactId。透過生產管道部署時，請一律使用 `aem-sdk-api`。同樣地，參照發行前 API 的程式碼不應該透過生產管道進行部署。

[AEM CS SDK Build Analyzer Maven 外掛程式 v1.0 及更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=zh-Hant#developing)將透過檢查相依性來偵測專案中是否使用了發行前 API。如果該分析器有找到，它將使用發行前 SDK API 來分析專案。

## 考量事項 {#considerations}

使用發行前通道時，需要注意幾個事項。

* 發行前通道不一定包含所有將在下一版中推出的新功能。
* 發行前版本中的功能經過嚴格的品質保證，旨在提供完整的功能而不是測試版品質。如果您發現任何問題，請提報，就像您在懷疑一般 AEM 版本中的功能存在錯誤時所做的。
* 若要判斷環境是否已經設定預發行通道，請前往 AEM 主控台的&#x200B;**關於**&#x200B;頁面，並檢查 AEM 版本號碼是否包含 `PRERELEASE` 字尾，例如 `Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE`。

![關於](/help/release-notes/assets/about.png)
