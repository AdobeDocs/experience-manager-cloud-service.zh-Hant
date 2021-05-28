---
title: '[!DNL Adobe Experience Manager] 作為Cloud Service發行前管道'
description: '[!DNL Adobe Experience Manager] 作為Cloud Service發行前管道'
source-git-commit: 4ee9a5744cdcec00dd497a00b0d8dbf288a5adcb
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 作為Cloud Service發行前管道  {#prerelease-channel}


## 簡介 {#introduction}

[!DNL Adobe Experience Manager] as aCloud Service會根據Experience Manager發行藍圖排程，以每月順序提 [供新功能](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service)。為了熟悉排定於下個月上線的功能，客戶可以訂閱發行前管道，在標準方案開發環境或任何沙箱方案環境中適當設定即可存取。 客戶可以預覽Sites主控台的變更，並根據任何新的發行前API建立程式碼。

特定月份的發行前功能清單會發佈在[每月發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)中。

>[！視頻](/help/release-notes/assets/prerelease-overview.mp4)

## 如何啟用發行前{#enable-prerelease}

搶鮮版功能的體驗方式不同：

* 雲端環境（標準方案開發環境或任何沙箱方案環境類型）
* 本機SDK

### 雲環境{#cloud-environments}

若要在雲端開發環境上查看Sites Console的新功能，以及任何專案自訂的結果：

* 使用[Cloud Manager API的環境變數端點](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables)，將&#x200B;**AEM_RELEASE_CHANNEL**&#x200B;環境變數設為值&#x200B;**prerelease**。

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

您也可以依照[https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)中的指示使用Cloud Manager CLI
```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


如果您想要將環境還原為一般（非發行前）管道的行為，可以刪除變數，或將其設回不同的值

### 本機SDK {#local-sdk}

您可以在本機Quickstart SDK的Sites主控台中看到新功能，並讓您的Maven專案參考位於Maven Central的預發行版本`API Jar`，以針對搶鮮版中的新API編碼。 您也可以在本機電腦上透過在發行前模式中啟動一般的Quickstart SDK來查看下列發行前功能：

* 從軟體發佈入口網站下載SDK，並依照[以Cloud ServiceSDK存取AEM](/help/implementing/developing/aem-as-a-cloud-service-sdk.md#accessing-the-aem-as-a-cloud-service-sdk.)所述進行安裝
* 啟動SDK快速入門時，請加入引數`-r prerelease`。
* 值為&#x200B;*sticky*，因此只能在第一次啟動時選取。 重新安裝SDK以更改命令行選項。

由於每月的功能發行之間可能有多個AEM維護髮行，因此您可以下載這些新SDK，並在Maven專案中參考新的SDK API Jar版本。 維護髮行不會新增其他發行前功能，但可能包含其他較小的變更，例如錯誤修正、安全性修正和效能增強。
Javadoc發佈到Maven Central。

若要根據發行前SDK建置：

1. 修改您maven專案的pom.xml，以參照發佈至Maven中央的不同發行前sdk api jar。 其中包含任何搶鮮版功能的新Java api，且與sdk api jar相依。 它使用相同版本。

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

   然後模組中的用法：

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   若要變更為發行前SDK，只需將相依性從`com.adobe.aem:aem-sdk-api`變更為`com.adobe.aem:aem-prerelease-sdk-api`，如下所述：

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

   如往常，個別專案可使用相依性。

1. 部署到本地伺服器
1. 如果滿足於在本機正常運作，請將程式碼提交至開發分支，並使用Cloud Manager非生產管道部署至訂閱發行前管道的環境

>[!CAUTION]
部署至Stage或Production時，絕不得使用`aem-prerelease-sdk-api` artifactId。 透過生產管道部署時，請一律使用aem-sdk-api。 同樣地，參考發行前API的程式碼也不應透過生產管道部署。

[AEM CS SDK組建Analyzer maven外掛程式v1.0和更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)會檢查相依性，以偵測專案中是否使用發行前api。 如果分析器找到，則會使用發行前sdk api來分析專案。

## 考量事項 {#considerations}

在發行前管道方面，請注意以下幾點：

* 發行前管道可能不包含將於下月發行的部分功能。
* 搶鮮版中的功能需經過嚴格的品質保證，且旨在完成功能，而非測試版品質。 如果您發現任何問題，請報告這些問題，就像在一般AEM版本中懷疑功能有錯誤時所做的一樣。
* 若要判斷環境是否已針對發行前通道進行設定，請前往AEM主控台的&#x200B;**關於**&#x200B;頁面，並檢查AEM版本編號是否包含&#x200B;*發行前*&#x200B;尾碼，例如```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```。

![關於](/help/release-notes/assets/about.png)
