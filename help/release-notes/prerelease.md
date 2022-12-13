---
title: Adobe Experience Manager as a Cloud Service發行前管道
description: 了解如何使用發行前管道預覽即將推出的功能，讓AEMas a Cloud Service。
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: 9a76a1c2b5e3b7986654b0843842b015811679a2
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 23%

---


# Adobe Experience Manager as a Cloud Service發行前管道 {#prerelease-channel}

了解如何使用發行前管道預覽即將推出的功能，讓AEMas a Cloud Service。

## 簡介 {#introduction}

根據Adobe Experience Manager as a Cloud Service的資料， [Experience Manager發佈路線圖。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html#aem-as-cloud-service)

為了熟悉排定於下個月上線的功能，您可以訂閱發行前管道，此管道可透過設定開發環境或任何沙箱環境來存取。 您可以預覽可透過AEM UI存取的變更，並針對任何新的發行前API建置程式碼。

特定月份的發行前功能清單會發佈在 [每月發行說明。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## AEMas a Cloud Service版本 {#releases}

AEMas a Cloud Service有兩種版本。

* **每月發行** 新增功能至AEMas a Cloud Service
* **重要更新** 新增安全性更新、效能增強和錯誤修正，並會每天套用。

此模式可確保持續發行，不會中斷服務。

搶鮮版管道可讓您預覽排定在未來每月發行的功能，以評估即將推出的功能，並針對您自己的專案規劃可能的實作。 它可讓您提前規劃下一個月的發行。

例如，如果是5月，而您訂閱了發行前管道，則您可以在即將推出的6月版本中評估功能。

![發行前順序圖](assets/prerelease-cadence.png)

搶鮮版提供即將推出之AEMaCS功能的一個月滾動期，讓您有時間評估任何新功能對您專案和自訂項目的影響，並規劃這些功能的推出、測試和使用者訓練。

要有效利用搶鮮版管道，需要四個步驟。

1. [標籤日曆](#mark-calendars)
1. [檢閱發行說明](#release-notes)
1. [存取並試用新功能](#new-features)
1. [訓練您的使用者](#train-users)

## 標籤日曆 {#mark-calendars}

每月發行會事先排程，發行日期會發佈於 [Adobe Experience League。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html#aem-as-cloud-service)

請記下發行日期，以便規劃時間以檢閱及測試即將推出的功能。

## 檢閱發行說明 {#release-notes}

在日曆中標示發行日期後，請務必檢查 [Adobe Experience League](/help/release-notes/release-notes-cloud/release-notes-current.md) 網站以取得最新發行說明。

每次發行都會附上發行說明，其中不僅記錄該發行版本的新功能，也記錄可用於發行前評估的功能。 搶先了解，並規劃善用AEMaaCS的最新功能！

您也可以 [檢查已知問題](/help/release-notes/known-issues.md) 會隨每個版本一併發佈，因此您也可能會注意到任何技術問題，這些問題可能會對您的評估或最終採用任何新功能造成挑戰。

## 啟用發行前管道以存取並嘗試新功能 {#new-features}

可在任何開發或沙箱環境中啟用發行前管道。 測試或生產環境中無法啟用發行前版本。

可以透過不同方式體驗發行前功能：

* [雲端環境](#cloud-environments)
* [本機 SDK](#local-sdk)

### 雲端環境 {#cloud-environments}

若要更新雲端環境以使用發行前版本，您必須新增環境變數。 您可以使用Cloud Manager UI或透過CLI執行此操作。

#### 使用UI新增環境變數 {#add-with-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 導覽至您要啟用發行前版本的方案。

1. 選取您要啟用發行前版本的環境，並透過 **方案** > **環境** > **環境配置**.

1. 新增 [環境變數：](../implementing/cloud-manager/environment-variables.md)

   | 名稱 | 值 | 套用的服務 | 類型 |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | 全部 | 變數 |

1. 儲存變更，環境將重新整理並啟用發行前功能切換。

   ![新環境變數](assets/env-configuration-prerelease.png)

#### 使用CLI添加環境變數 {#add-with-cli}

您也可以使用Cloud Manager API和CLI來更新環境變數。

* 使用 [Cloud Manager API的環境變數端點，](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables) 設定 `AEM_RELEASE_CHANNEL` 環境變數至值 `prerelease`.

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

* [Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 也可供使用

   ```shell
   aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease
   ```

如果您希望環境還原為一般 (非發行前) 通道的行為，可以刪除該變數或將其設回不同的值。

### 本機 SDK {#local-sdk}

您可以在本機Quickstart SDK的Sites主控台中查看新功能，並將Maven專案設定為參考發行前版本，以針對發行前版本的新API編寫程式碼 `API Jar` 位於馬文中心。 您也可以在本機開發環境中，透過在發行前模式中啟動一般的Quickstart SDK來查看這些發行前功能。

#### 以發行前模式啟動Quickstart SDK {#prerelease-mode}

1. 從軟體發佈入口網站下載SDK，然後依照 [存取AEMas a Cloud ServiceSDK。](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
1. 啟動 SDK 快速入門時，包含引數 `-r prerelease`。

值為 sticky，因此只能在第一次啟動時選擇。 重新安裝SDK以更改命令行選項。

由於每月功能發行之間可能會有多個 AEM 維護版本，因此您可以下載這些新的 SDK 並在 maven 專案中參照新的 SDK API Jar 版本。 維護版本不會新增其他發行前功能，但可能包括其他較小幅的變更，例如錯誤修正、安全性修正和效能增強。
Javadoc 會發佈到 Maven Central。

#### 根據發行前SDK建置 {#build-sdk}

1. 修改您maven專案的 `pom.xml` 以參考發佈至Maven Central的不同發行前SDK API jar。 其中包含任何搶鮮版功能的新Java API，且與SDK API Jar相依。 它使用相同的版本。

   例如，上層pom的相依性管理區段中的程式碼片段會參考一般API Jar:

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

1. 部署到您的本機伺服器.

1. 如果滿意它在本機如預期般運作，將程式碼提交到開發分支並使用 Cloud Manager 非生產管道部署到訂閱發行前通道的環境.

>[!CAUTION]
> 
> 此 `aem-prerelease-sdk-api` 部署至預備或生產時，絕不得使用artifactId。 一律使用 `aem-sdk-api` 透過生產管道部署時。 同樣地，參考發行前API的程式碼也不應透過生產管道部署。

此 [AEM CS SDK組建Analyzer maven外掛程式v1.0及更新版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html#developing) 會檢查相依性，以偵測專案中是否使用發行前API。 如果分析器找到，則會使用發行前SDK API來分析專案。

## 訓練您的使用者 {#train-users}

在您測試發行前管道中的新功能並決定在您的專案中加以運用後，就需要訓練使用者。

Adobe Experience League提供許多學習AEMaCS的資源。

* [AEMaaCS檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)
* [教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-tutorials/overview.html)
* [每月發行概述影片](/help/release-notes/release-notes-cloud/release-notes-current.md#release-video) 在發行說明中

## 考量事項 {#considerations}

使用發行前管道時，需注意一些項目。

* 發行前管道不一定包含要在下列版本中推出的所有新功能。
* 發行前版本中的功能經過嚴格的品質保證，旨在提供完整的功能而不是測試版品質。如果您發現任何問題，請提報，就像您在懷疑一般 AEM 版本中的功能存在錯誤時所做的。
* 若要判斷環境是否已針對發行前管道設定，請前往AEM主控台的 **關於** 頁面，並檢查AEM版本號碼是否包含 *預發行* 尾碼，例如 ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![關於](/help/release-notes/assets/about.png)
