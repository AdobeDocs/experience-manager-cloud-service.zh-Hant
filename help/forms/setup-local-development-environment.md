---
title: 如何設定AEM Forms的本機開發環境？
description: 設定Adobe Experience Manager Forms as a Cloud Service的本機開發環境
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 12877a77-094f-492a-af58-cffafecf79ae
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '2759'
ht-degree: 2%

---

# 設定AEM Forms的本機開發環境 {#overview}

當您將[!DNL &#x200B; Adobe Experience Manager Forms]設定為[!DNL &#x200B; Cloud Service]環境時，您會在雲端上設定開發、測試和生產環境。 此外，您也可以設定本機開發環境。

您可以使用本機開發環境執行以下動作，而無需登入雲端開發環境：

* [建立表單](creating-adaptive-form.md)和相關資產（主題、範本、自訂提交動作等）
* [將 PDF 表單轉換為最適化表單](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=zh-hant)
* 建立應用程式，依需求或以批次模式產生[客戶通訊](aem-forms-cloud-service-communications-introduction.md)。

當本機開發執行個體或應用程式上的最適化表單或相關資產準備就緒以產生[客戶通訊]後，您可以將最適化表單或客戶通訊應用程式從本機開發環境匯出至Cloud Service環境，以進行進一步測試或移至生產環境。

您也可以在本機開發環境中開發和測試自訂程式碼，例如自訂元件和預填服務。 當自訂程式碼測試並準備就緒時，您可以使用Cloud Service開發環境的Git存放庫來部署自訂程式碼。

若要設定新的本機開發環境並使用它來開發活動，請依下列順序執行下列動作：

* [設定開發工具](#setup-development-tools-for-AEM-projects)

* [設定本機作者和發佈執行個體](#set-up-local-experience-manager-environment-for-development)

* [將Forms封存新增至本機開發執行個體並設定使用者](#add-forms-archive-configure-users)

* [設定微服務的本機開發環境](#docker-microservices)

* [設定開發專案](#forms-cloud-service-local-development-environment)

* [設定本機Dispatcher工具](#setup-local-dispatcher-tools)

<!--
You can use the local development environment to create and test Adaptive Forms without connecting to the Cloud Service. [!DNL AEM Forms] provides an SDK to help test all the cloud-ready functionalities on the local development environment. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can also develop and test custom code like custom components and prefill service on the local development environment. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code. 

>[!NOTE]
>
> Pre-pilot release does not support using an [!DNL AEM Forms] as a Cloud Service development instance to create forms. You can create forms, related assets, and custom code only on a local development environment.-->

<!--
You configure two types of development environments:

* **[!DNL AEM Forms] as a Cloud Service development environment:** Use the [[!DNL AEM Forms] as a Cloud Service](setup-forms-cloud-service.md) environment to store, manage, and publish Adaptive Forms and related assets. Do not use an [!DNL AEM Forms] as a Cloud Service environment to create Adaptive Forms and related assets <!--, form-centric workflows, a form data model, or to generate a Document of Record. -->

<!--
* **Local development environment:** You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. 
Use a local development environment:
    
    * To create forms and related assets (themes, templates, custom Submit Actions, and more) and convert PDF forms to Adaptive Forms. After an Adaptive Form or related assets are ready on the local development instance, you can export the Adaptive Form and related assets from the local development environment to an [!DNL AEM Forms] as a Cloud Service development environment for publishing.  
    
    * To update configuration settings and develop and test custom code like custom components and prefill service. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code.  

You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can use the [development tools](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/dev-tools.html?lang=zh-Hant) to write custom code, customize or create new Adaptive Forms components, create a custom prefill service, or modify default configurations of an [!DNL AEM Forms] as a Cloud Service instance. 

-->

## 先決條件

您需要下列軟體來設定本機開發環境。 開始設定本機開發環境之前，請先下載這些專案：

| 軟體 | 說明 | 下載連結 |
|---|---|---|
| Adobe Experience Manager as a Cloud Service SDK | SDK包含[!DNL Adobe Experience Manager]個QuickStart和Dispatcher工具 | 從[Software Distribution](#software-distribution)下載最新的SDK |
| Adobe Experience Manager Forms功能封存(AEM Forms附加元件) | 建立、調整樣式及最佳化最適化Forms和其他Adobe Experience Manager Forms功能的工具 | 從[軟體發佈](#software-distribution)下載 |
| （選用） Adobe Experience Manager Forms參考內容 | 建立、調整樣式及最佳化最適化Forms和其他Adobe Experience Manager Forms功能的工具 | 從[軟體發佈](#software-distribution)下載 |
| （選用） Adobe Experience Manager Forms Designer | 建立、調整樣式及最佳化最適化Forms和其他Adobe Experience Manager Forms功能的工具 | 從[軟體發佈](#software-distribution)下載 |

### 從Software Distribution下載最新版本的軟體 {#software-distribution}

若要從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載最新版的Adobe Experience Manager as a Cloud Service SDK、Experience Manager Forms功能封存(AEM Forms附加元件)、表單參考資產或Forms Designer：

1. 使用您的Adobe ID登入<https://experience.adobe.com/#/downloads>

   >[!NOTE]
   >
   > 必須布建您的Adobe組織才能使用AEM as a Cloud Service下載AEM as a Cloud Service SDK。

1. 導覽至&#x200B;**[!UICONTROL AEM as a Cloud Service]**&#x200B;標籤。
1. 依發佈日期遞減排序。
1. 按一下最新的Adobe Experience Manager as a Cloud Service SDK、Experience Manager Forms功能封存(AEM Forms附加元件)、表單參考資產或Forms Designer。

   >[!NOTE]
   >
   > 建議您下載最新版Experience Manager Forms功能封存(AEM Forms附加元件)、表單參考資產或Forms Designer，以便與Adobe Experience Manager as a Cloud Service SDK緊密相容。

1. 檢閱並接受EULA。 選取&#x200B;**[!UICONTROL 下載]**&#x200B;按鈕。

## 設定AEM專案的開發工具 {#setup-development-tools-for-AEM-projects}

Adobe Experience Manager Forms專案是自訂程式碼基底。 它包含透過Cloud Manager部署至[!DNL Adobe Experience Manager] as a Cloud Service的程式碼、設定和內容。 [AEM專案Maven原型](https://github.com/adobe/aem-project-archetype)提供專案的基準結構。

設定下列開發工具，以用於您用於開發的[!DNL Adobe Experience Manager]專案：

* [Java™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=zh-Hant#local-development-environment-set-up)
* [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=zh-Hant#install-git)
* [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=zh-Hant#node-js)
* [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=zh-Hant#install-maven)

如需設定前述開發工具的詳細指示，請參閱[設定開發工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=zh-Hant)。

## 設定本機的Experience Manager環境以進行開發

Cloud Service SDK提供快速入門檔案。 這會執行Experience Manager的本機版本。 您可以在本機執行Author或Publish例項。

雖然QuickStart提供本機開發體驗，但並未提供[!DNL Adobe Experience Manager] as a Cloud Service中的所有功能。 因此，在將功能移至中繼或生產環境之前，請務必使用[!DNL Adobe Experience Manager] as a Cloud Service開發環境測試您的功能和程式碼。

若要安裝和設定本機Experience Manager環境，請執行以下步驟：

* [下載並解壓縮](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) [!DNL Adobe Experience Manager] as a Cloud Service SDK
* [設定作者執行個體](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=zh-Hant#set-up-local-aem-author-service)
* [設定發佈執行個體](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=zh-Hant#set-up-local-aem-publish-service)

## 將Forms封存新增至本機作者和發佈執行個體，並設定Forms專屬的使用者 {#add-forms-archive-configure-users}

以所列順序執行以下步驟，將Forms封存新增至Experience Manager執行個體，並設定表單特定使用者：

### 安裝最新的Forms附加功能封存 {#add-forms-archive}

Adobe Experience Manager Forms as a Cloud Service功能封存提供在本機開發環境中建立、樣式化和最佳化最適化Forms的工具。 安裝套件以建立最適化表單，並使用[!DNL AEM Forms]的各種其他功能。 若要安裝套件：

1. 從[!DNL AEM Forms]Software Distribution[下載並解壓縮作業系統的最新](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)封存。

1. 導覽至crx-quickstart/install目錄。 如果資料夾不存在，請建立它。

1. 停止您的AEM執行個體，將[!DNL AEM Forms]附加功能封存`aem-forms-addon-<version>.far`放入安裝資料夾中。
1. 移至使用中命令視窗並按`Ctrl + C`命令以重新啟動SDK。

   >[!NOTE]
   >
   > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式），可能會導致AEM開發環境不一致。

<!--**Q**: I've set up a Aem as a Cloud Service environment and added the Forms Add-On for a project. After the .far file addition, the bundles are not in the active state and are in installed state only due to the missing dependencies. How to make the bundles in the active state?
**A**: To resolve the issue:
1. Start the AEM and wait for it to start completely (all bundles up)
1. Stop aem (ctrl + c). Place the forms far in the install folder.
1. Restart AEM.-->


### 設定使用者和許可權 {#configure-users-and-permissions}

建立表單開發人員和表單從業人員等使用者，並[將這些使用者新增到預先定義的表單群組](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=zh-Hant#accessing)，以向他們提供所需的許可權。 下表列出所有型別的使用者以及每種型別表單使用者的預先定義群組：

| 使用者型別 | AEM群組 |
|---|---|
| 表單從業者/ | [!DNL forms-users] (AEM Forms使用者)、[!DNL template-authors]、[!DNL workflow-users]、[!DNL workflow-editors]和[!DNL fdm-authors] |
| 表單開發人員 | [!DNL forms-users] (AEM Forms使用者)、[!DNL template-authors]、[!DNL workflow-users]、[!DNL workflow-editors]和[!DNL fdm-authors] |
| Customer Experience Lead (UX Designer) | [!DNL forms-users]、[!DNL template-authors] |
| AEM 管理員 | [!DNL aem-administrators]、[!DNL fd-administrators] |
| 一般使用者 | 當使用者必須登入才能檢視並提交最適化表單時，請將這類使用者新增到[!DNL forms-users]群組。 </br>當存取最適化Forms不需要使用者驗證時，請勿將任何群組指派給這類使用者。 |

<!--  

## Set up a local AEM instance for development

Perform the following steps in the listed order to set up and configure your local development environment:

1. **Set up an AEM author instance:** You require an author instance to create Adaptive Forms. Download and extract the latest AEM SDK archive. Run the quick start file in author run mode to set up an author instance. For detailed instructions, see [default local instance](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=zh-Hant).  

1. **Install the latest [!DNL AEM Forms] add-on feature archive:** [!DNL AEM Forms] add-on feature archive provides tools to create, style, and optimize Adaptive Forms on the local development environment. Install the package to create an Adaptive Form and use various other features of [!DNL AEM Forms]. To install the package:

    1. Download and extract the latest [!DNL AEM Forms] archive for your operating system from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

    1. Navigate to the crx-quickstart/install directory. If the folder does not exist, create it.

    1. Stop your Cloud ready AEM instance, place the [!DNL AEM Forms] add-on feature archive, `aem-forms-addon-<version>.far`,  in the install folder, and restart the instance.

1. **Configure users and permissions:** Create users like Form Developer and Form Practitioner a nd add these users to pre-defined forms group to provide them required permissions. The table below lists all types of users and pre-defined groups for each type of forms users:
  
    | User Type | AEM Group |
    |---|---|
    | Form Practitioner  | forms-users (AEM Forms Users), template-authors  |
    | Form Developer | forms-users (AEM Forms Users), template-authors |
    | End-User| everyone* |

    `*` When a user should log in to access or submit Adaptive Forms, add such users to the everyone group.  -->

<!--    
### Set up an AEM project for the development tasks related to local AEM 6.5.5 Forms instance

Use this project to update configurations, create overlays, develop custom Adaptive Form components, and custom code using the local development environment. To set up the project:

1. **Install and configure Maven and set up an AEM project based on Apache Maven:** Apache Maven is an open-source tool for managing software projects. It helps automate builds and provides quality project information. It is the recommended build management tool for AEM projects. For detailed instructions to set up an AEM project based on Apache Maven, see [How to Build AEM Projects using Apache Maven](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/ht-projects-maven.html?lang=zh-Hant).

1. Configure the project to use [uber-jar](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=zh-Hant#install-aem-forms-jee-installer) version 6.5.5 or later and [[!DNL AEM Forms] Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/) version 6.0.160 or later.  

1. **Set Up an Integrated Development Environment:**  Set up an IDE of your choice for development, see [Set Up an Integrated Development Environment](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=zh-Hant#set-up-an-integrated-development-environment) for detailed instructions.
 -->

## 設定記錄檔案(DoR)的本機開發環境{#docker-microservices}

AEM Forms as a Cloud Services提供基於Docker的SDK環境，可更輕鬆地開發記錄檔案並使用其他微服務。 這可讓您不再手動設定平台特定的二進位檔和調整專案。 若要設定環境：

1. 安裝和配置Docker：

   * (適用於Microsoft® Windows)安裝[Docker案頭](https://www.docker.com/products/docker-desktop)。 它在您的電腦上設定`Docker Engine`和`docker-compose`。

   * (Apple macOS)安裝[適用於Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)的Docker Desktop。 它包括Docker引擎、Docker CLI客戶端、Docker撰寫、Docker內容信任、Kubernetes和Credential Helper。

   * (適用於Linux®)在您的電腦上安裝[Docker引擎](https://docs.docker.com/engine/install/#server)和[Docker構成](https://docs.docker.com/compose/install/)。

   >[!NOTE]
   >
   > * 對於Apple macOS，將包含本機AEM作者執行個體的資料夾加入允許清單。
   >
   > * 適用於Windows的Docker Desktop支援兩個後端，Hyper-V
   > （舊版）和WSL2 （新版）。 會自動共用檔案
   > 使用WSL2 （現代）時由Docker管理。 您必須
   > 使用Hyper-V （舊版）時明確設定檔案共用。

1. 建立與作者和發佈執行個體平行的資料夾（例如aem-sdk）。 例如， C:\aem-sdk。

1. 解壓縮`aem-forms-addon-<version>.zip\aem-forms-addon-native-<version>.zip`檔案。

   ![擷取的aem表單新增至原生](assets/microservice-docker.png)

1. 建立環境變數AEM_HOME，並指向本機AEM Author安裝。 例如， C:\aem\author\。

1. 開啟sdk.bat或sdk.sh進行編輯。 將AEM_HOME設定為指向本機AEM Author安裝。 例如， C:\aem\author\。

1. 開啟命令提示字元並瀏覽至`aem-forms-addon-native-<version>`資料夾。

1. 確保您的本機AEM作者執行個體已啟動且執行中。 執行以下命令以啟動SDK：

   * 在Microsoft® Windows上

     ```shell
     sdk.bat start
     ```


   * Linux®或Apple macOS

     ```Shell
     % export AEM_HOME=[local AEM Author installation]
     % ./sdk.sh start
     ```


   >[!NOTE]
   >
   > 如果您已在sdk.sh檔案中定義環境變數，則可在命令列指定該變數。 提供在命令列定義環境變數的選項，以在不更新shell指令碼的情況下執行命令。

   ![start-sdk-command](assets/start-sdk.png)

您現在可以使用本機開發環境來呈現記錄檔案。 若要測試，請上傳XDP檔案至您的環境並加以呈現。 例如，<http://localhost:4502/libs/xfaforms/profiles/default.print.pdf?template=crx:///content/dam/formsanddocuments/cheque-request.xdp>會將XDP檔案轉換為PDF檔案。

## 根據Experience Manager原型設定Forms的開發專案 {#forms-cloud-service-local-development-environment}

使用此專案在本機[!DNL Experience Manager Forms] SDK上建立最適化Forms、部署設定更新、覆蓋、建立自訂最適化表單元件、測試和自訂程式碼。 在本機測試之後，您可以將專案部署到[!DNL Experience Manager Forms]個as a Cloud Service生產和非生產環境。 部署專案時，也會部署下列AEM Forms資產：

| 主題 | 範本 | 表單資料模型(FDM) |
|---------|----------|---------|
| Canvas 3.0 | 基本 | Microsoft® Dynamics 365 |
| 寧靜 | 空白 | Salesforce |
| 城市化 |   |  |
| Ultraminary |  |  |
| 貝瑞爾 |  |  |

>[!NOTE]
>
> 設定AEM Archetype 30或更新版本專案，以取得並使用Microsoft®Dynamics 365和Salesforce表單資料模型(FDM)與AEM Forms as a Cloud Service。
> 設定AEM Archetype 32版或更新版本的專案，以透過AEM Forms as a Cloud Service取得和使用Tranquil、Urbane和Ultraminary主題。

若要設定專案：

1. **在本機開發執行個體上複製Cloud Manager Git存放庫：**&#x200B;您的Cloud Manager Git存放庫包含預設的AEM專案。 它以[AEM原型](https://github.com/adobe/aem-project-archetype/)為基礎。 從Cloud Manager UI使用自助Git帳戶管理功能來複製您的Cloud Manager Git存放庫，以將專案引進您的本機開發環境中。 如需存取存放庫的詳細資訊，請參閱[存取存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html?lang=zh-Hant)。

<!-- 1. 
After the repository is cloned, [integrate your Git repo with Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=zh-Hant)

**Make cloned AEM project compatible with [!DNL AEM Forms] as a Cloud Service:** Remove uber-jar and other non-cloud dependencies from the pom.xml files of the project. You can refer the pom.xml files of the [sample AEM project](assets/FaaCSample.zip) for the list of required dependencies and update your AEM project accordingly. You can also refer [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hant) to learn changes required to make an AEM project compatible with AEM as a Cloud Service.  -->

1. **將[!DNL Experience Manager Forms]建立為[Cloud Service]專案：**&#x200B;根據最新的[!DNL Experience Manager Forms]Cloud Service原型[或更新版本，將]建立為[AEM](https://github.com/adobe/aem-project-archetype)專案。 原型可協助開發人員輕鬆開始開發[!DNL AEM Forms] as a Cloud Service。 其中也包括一些範例主題和範本，可幫助您快速入門。

   開啟命令提示字元並執行以下命令以建立[!DNL Experience Manager Forms] as a Cloud Service專案。

   ```shell
   mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="41" -D appTitle=mysite -D appId=mysite -D groupId=com.mysite -D includeFormsenrollment="y" -D aemVersion="cloud"
   ```

   變更上述命令中的`appTitle`、`appId`和`groupId`以反映您的環境。 此外，根據您的授權和需求，將includeFormsenrollment、includeFormscommunications和includeFormsheadless的值設定為`y`或`n`。 includeFormsheadless是根據核心元件建立最適化Forms的必要元件。

   * 使用`includeFormsenrollment=y`選項來包含建立Adaptive Forms所需的Forms特定設定、主題、範本、核心元件和相依性。 如果您使用Forms入口網站，請設定`includeExamples=y`選項。 它也會將Forms Portal核心元件新增至專案。

   * 使用`includeFormscommunications=y`選項加入Forms核心元件和加入客戶通訊功能所需的相依性。

     >[!WARNING]
     >
     >* 使用版本45建立Archetype專案時，[AEM Archetype專案資料夾]/pom.xml一開始會將Forms核心元件版本設定為2.0.64。在建立或部署Archetype專案之前，請將Forms核心元件版本更新為2.0.62。

1. 將專案部署到您的本機開發環境。 您可以使用以下命令來部署到您的本機開發環境

   `mvn -PautoInstallPackage clean install`

   如需完整的命令清單，請參閱[建置和安裝](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=zh-Hant#building-and-installing)

1. [將程式碼部署到您的 [!DNL AEM Forms] as a Cloud Service環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=zh-Hant#customer-releases)。

## 設定本機Dispatcher工具 {#setup-local-dispatcher-tools}

Dispatcher是Apache HTTP Web伺服器模組，可在CDN和AEM發佈層級之間提供安全性與效能層。 Dispatcher是整體Experience Manager架構不可或缺的一部分，並應成為本機開發環境的一部分。

執行以下步驟來設定本機Dispatcher，然後新增Forms特定規則：

### 設定本機Dispatcher {#setup-local-dispatcher}

[!DNL Experience Manager] as a Cloud Service SDK包含建議的Dispatcher Tools版本，可協助本機設定、驗證和模擬Dispatcher。 Dispatcher工具以Docker為基礎，提供命令列工具，將Apache HTTP Web Server和Dispatcher設定檔案傳輸為相容格式，並將其部署到Docker容器中執行的Dispatcher。

Dispatcher上的快取可讓[!DNL AEM Forms]在使用者端預先填入最適化Forms。 這可改善預填表單的演算速度。

如需設定Dispatcher的詳細指示，請參閱[設定本機Dispatcher工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=zh-Hant#local-development-environment-set-up)

### 將Forms特定規則新增至Dispatcher {#forms-specific-rules-to-dispatcher}

執行以下步驟，為Experience Manager Forms as a Cloud Service設定Dispatcher快取：

1. 開啟您的AEM專案並導覽至`\src\conf.dispatcher.d\available_farms`
1. 建立`default.farm`檔案的復本。 例如，`forms.farm`。
1. 開啟已建立的`forms.farm`檔案進行編輯，並取代下列程式碼：

   ```json
   #/ignoreUrlParams {
   #/0001 { /glob "*" /type "deny" }
   #/0002 { /glob "q" /type "allow" }
   #}
   ```

   替換為

   ```json
   /ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   /0002 { /glob "dataRef" /type "allow" }
   }
   ```

1. 儲存並關閉檔案。
1. 移至`conf.d/enabled_farms`並建立指向`forms.farm`檔案的符號連結。
1. 編譯專案並將其部署至您的[!DNL AEM Forms] as a Cloud Service環境。

### 有關快取的考量事項 {#considerations-about-caching}

* Dispatcher快取可讓[!DNL AEM Forms]在使用者端預先填入最適化Forms。 這可改善預填表單的演算速度。
* 快取安全內容功能預設為停用。 若要啟用此功能，您可以執行[快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hant)文章中提供的指示
* Dispatcher可能無法讓某些最適化Forms和相關的最適化Forms失效。 若要解決這類問題，請參閱疑難排解一節中的[[!DNL AEM Forms] 快取](troubleshooting-caching-performance.md)。
* 快取本地化的最適化Forms：
   * 使用URL格式`http://host:port/content/forms/af/<afName>.<locale>.html`來要求最適化表單的本地化版本，而非`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * 瀏覽器地區設定選項預設為停用。 若要變更瀏覽器地區設定，
* 當您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`，且組態管理員中的「使用瀏覽器地區設定」已停用時，會提供非當地語系化版本的調適型表單。 非當地語系化語言是開發最適化表單時使用的語言。 系統不會考量為瀏覽器設定的地區設定（瀏覽器地區設定），而是提供非當地語系化版本的調適型表單。
* 當您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`，並且啟用Configuration Manager中的「使用瀏覽器地區設定」時，會提供當地語系化版本的適用性表單（如果有的話）。 當地語系化最適化表單的語言取決於瀏覽器設定的地區設定（瀏覽器地區設定）。 這會導致[只快取最適化表單]的第一個執行個體。 若要防止執行個體發生問題，請參閱疑難排解一節中的[僅快取Adaptive Form的第一個執行個體](troubleshooting-caching-performance.md)。

您的本機開發環境已準備就緒。

## 在 AEM Forms as a Cloud Service 和本機開發環境中啟用自適應表單核心元件

在AEM Forms as a Cloud Service上啟用最適化Forms核心元件，可讓您開始建立、發佈及交付核心元件式的最適化Forms和Headless Forms ，並使用AEM Forms Cloud Service例項至多個管道。 您需要啟用調適型表單核心元件的環境才能使用 Headless 調適型表單。

>[!NOTE]
>
> 安裝最新的Far，為AEM Cloud Service環境啟用最適化Forms核心元件。

## 升級您的本機開發環境 {#upgrade-your-local-development-environment}

將SDK升級至新版本需要取代整個本機開發環境，導致本機存放庫中的所有程式碼、設定和內容遺失。 確保任何不應銷毀的程式碼、設定或內容都會安全地提交至Git，或從本機Experience Manager執行個體匯出為CRX套件。

### 升級SDK時如何避免內容遺失 {#avoid-content-loss-when-upgrading--SDK}

升級SDK會有效地建立全新的製作和發佈執行個體，包括新的存放庫([設定AEM專案](#forms-cloud-service-local-development-environment))，這表示遺失對先前SDK存放庫所做的任何變更。 如需在SDK升級之間協助儲存內容的可行策略，請參閱[升級AEM SDK時如何避免內容遺失](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=zh-Hant#optional-local-aem-runtime-set-up-tasks)

<!--When you update any  Forms-specifc configuration, create overlays, develop custom Adaptive Form components, or develop and test any custom code in AEM project for the development tasks related to local development instance, use the AEM project cloned from the Cloud Manager Git repository to [deploy the custom code and other changes to your [!DNL AEM Forms] as a Cloud Service's production or non-production environment](https://video.tv.adobe.com/v/30191?quality=9).

## Upgrade your local development environment {#update-local-setup}

Update the local AEM setup (AEM SDK) to latest version at least monthly on, or shortly after, the last Thursday of each month, which is the release cadence for AEM as a Cloud Service "feature releases". You can download local AEM SDK from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

Updating the AEM SDK to a new version requires replacing the entire local development environment, resulting in a loss of all code, configuration and content in the local AEM repositories. Ensure that any code, config or content that should not be destroyed is safely committed to Git, or exported from the local AEM instance as AEM Packages.

### How to avoid content loss when upgrading the AEM SDK {#avoid-content-loss-when-upgrading--AEM-SDK}

Upgrading the AEM SDK is effectively creating a brand new AEM runtime ([Set up a local AEM instance](setup-forms-cloud-service.md)), including a new repository ([Set up AEM project](#forms-cloud-service-local-development-environment)), meaning any changes made to a prior AEM SDK's repository are lost. The following are viable strategies for aiding in persisting content between AEM SDK upgrades, and can be used discretely or in concert:

1. Create a content package dedicated to containing the sample content to aid in development and maintain it in Git. Any content that should be persisted through AEM SDK upgrades would be persisted into this package and re-deployed after upgrading the AEM SDK.
1. Use [oak-upgrade](https://jackrabbit.apache.org/oak/docs/migration.html) with the `includepaths` directive, to copy content from the prior AEM SDK repository to the new AEM SDK repository.
1. Back up any content using AEM Package Manager and content packages on the prior AEM SDK and re-install them on the new AEM SDK.

Remember, using the above approaches to maintain code between AEM SDK upgrades, indicates a development anti-pattern. Non-disposable code should originate in your Development IDE and flow into AEM SDK via deployments.

For information about troubleshooting, stopping local AEM environment, run modes, and deployment, see [Set up local AEM Runtime](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=zh-Hant#local-development-environment-set-up).-->

### 備份特定於Forms的內容，並將其匯入新的SDK環境 {#backup-and-import-Forms-specific-content-to-new-SDK-environment}

若要備份資產，並將資產從現有的SDK移至新的SDK環境：

* 建立現有內容的備份。

* 設定全新的SDK環境。

* 將備份匯入至您的新SDK環境。

### 建立現有內容的備份 {#create-backup-of-your-existing-content}

備份您的Adaptive Forms、範本、表單資料模型(FDM)、主題、設定和自訂程式碼。 您可以執行下列動作來建立備份：

1. [下載](import-export-forms-templates.md#manage-forms-and-related-assets)最適化Forms、主題和PDF forms。
1. 匯出自適應表單範本。

1. 下載表單資料模型

1. 匯出可編輯的範本、雲端設定和工作流程模型。 若要從您現有的SDK匯出所有先前提到的專案，請使用下列篩選器建立[CRX-Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=zh-Hant)：

   * /conf/ReferenceEditableTemplates
   * /conf/global/settings/cloudconfigs
   * /conf/global/settings/wcm
   * /var/workflow/model
   * /conf/global/settings/workflow
1. 從您的本機開發環境匯出電子郵件設定、提交和預填動作程式碼。 若要匯出這些設定和組態，請在您的本機開發環境中建立下列資料夾和檔案的復本：

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

### 將備份匯入至您的新SDK環境 {#import-the-backup-to-your-new-SDK-environment}

將最適化Forms、範本、表單資料模型、主題、設定和自訂程式碼匯入全新環境。 您可以執行下列動作來匯入備份：

1. [將](import-export-forms-templates.md#manage-forms-and-related-assets)最適化Forms、主題和PDF forms匯入新的SDK環境。
1. 將最適化表單範本匯入新的SDK環境。

1. 上傳表單資料模型至新的SDK環境。

1. 匯入可編輯的範本、雲端設定和工作流程模型。 若要匯入新SDK環境中所有先前提到的專案，請將包含這些專案的CRX套件匯入新SDK環境。

1. 從您的本機開發環境匯入電子郵件設定、提交和預填動作程式碼。 若要匯入這些設定和組態，請將下列檔案從舊的原型專案放入新的原型專案：

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

您的新環境現在有舊環境的表單和相關資產。
