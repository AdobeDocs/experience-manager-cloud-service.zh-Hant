---
title: 為Adobe Experience Manager Forms as a Cloud Service設定本機開發環境
description: 為Adobe Experience Manager Forms as a Cloud Service設定本機開發環境
exl-id: 12877a77-094f-492a-af58-cffafecf79ae
source-git-commit: 131b17f53b364138d2cea7648d4c23a8480740bf
workflow-type: tm+mt
source-wordcount: '2647'
ht-degree: 1%

---

# 建立本地開發環境和初始開發項目 {#overview}

當您設定並設定 [!DNL  Adobe Experience Manager Forms] as a [!DNL  Cloud Service] 環境中，您可以在雲端上設定開發、測試和生產環境。 此外，您也可以設定和設定本機開發環境。

您可以使用本機開發環境來建立表單和相關資產（主題、範本、自訂提交動作等），以及 [將PDF forms轉換為最適化Forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) 而不需登入雲端開發環境。 在本機開發執行個體上準備好適用性表單或相關資產後，您可以將適用性表單和相關資產從本機開發環境匯出至Cloud Service環境，以進一步測試和發佈。

您也可以在本機開發環境上開發及測試自訂程式碼，例如自訂元件和預填服務。 當自訂程式碼經過測試並準備就緒時，您就可以使用Cloud Service開發環境的Git存放庫來部署自訂程式碼。

若要設定新的本機開發環境，並使用它來開發活動，請依列出順序執行下列動作：

* [設定開發工具](#setup-development-tools-for-AEM-projects)

* [設定本機製作和發佈執行個體](#set-up-local-experience-manager-environment-for-development)

* [將Forms封存新增至本機開發執行個體並設定使用者](#add-forms-archive-configure-users)

* [為微服務設定本地開發環境](#docker-microservices)

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

You can use the [development tools](https://docs.adobe.com/content/help/en/experience-manager-65/developing/devtools/dev-tools.html) to write custom code, customize or create new Adaptive Forms components, create a custom prefill service, or modify default configurations of an [!DNL AEM Forms] as a Cloud Service instance. 

-->

## 必備條件

您需要下列軟體來設定本機開發環境。 請先下載這些檔案，再開始設定本機開發環境：

| 軟體 | 說明 | 下載連結 |
|---|---|---|
| Adobe Experience Manager as a Cloud Service SDK | SDK包含 [!DNL Adobe Experience Manager] QuickStart和Dispatcher工具 | 從下載最新SDK [Software Distribution](#software-distribution) |  |
| Adobe Experience Manager Forms功能封存(AEM Forms附加元件) | 建立、設定樣式和最佳化適用性Forms和其他Adobe Experience Manager表單功能的工具 | 從下載 [Software Distribution](#software-distribution) |
| （選用）Adobe Experience Manager Forms參考內容 | 建立、設定樣式和最佳化適用性Forms和其他Adobe Experience Manager表單功能的工具 | 從下載 [Software Distribution](#software-distribution) |
| （選用）Adobe Experience Manager Forms Designer | 建立、設定樣式和最佳化適用性Forms和其他Adobe Experience Manager表單功能的工具 | 從下載 [Software Distribution](#software-distribution) |

### 從Software Distribution下載最新版軟體 {#software-distribution}

若要從以下網址下載最新版本的Adobe Experience Manager as a Cloud Service SDK、Experience Manager Forms功能封存(AEM Forms附加元件)、表單參考資產或Forms Designer，請前往 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html):

1. 使用您的Adobe ID登入https://experience.adobe.com/#/downloads

   >[!NOTE]
   >
   > 必須布建您的Adobe組織，AEMas a Cloud Service才能下載AEMas a Cloud ServiceSDK。

1. 導覽至 **[!UICONTROL AEMas a Cloud Service]** 標籤。
1. 依發佈日期以降序排序。
1. 按一下最新的Adobe Experience Manager as a Cloud Service SDK、Experience Manager Forms功能封存(AEM Forms附加元件)、表單參考資產或Forms Designer。
1. 檢閱並接受EULA。 點選 **[!UICONTROL 下載]** 按鈕。

## 設定AEM專案的開發工具 {#setup-development-tools-for-AEM-projects}

Adobe Experience Manager Forms專案是自訂程式碼基底。 其中包含透過Cloud Manager部署至 [!DNL Adobe Experience Manager] as a Cloud Service。 此 [AEM專案Maven原型](https://github.com/adobe/aem-project-archetype) 提供專案的基線結構。

設定下列開發工具以用於您的 [!DNL Adobe Experience Manager] 開發項目：

* [Java™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up)
* [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git)
* [Node.js(npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js)
* [馬文](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven)

如需設定前述開發工具的詳細指示，請參閱 [設定開發工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html).

## 設定本機Experience Manager環境以進行開發

Cloud ServiceSDK提供QuickStart檔案。 它會執行本機版本的Experience Manager。 您可以在本機執行「製作」或「發佈」執行個體。

雖然QuickStart提供了本地開發體驗，但它並沒有 [!DNL Adobe Experience Manager] as a Cloud Service。 因此，請一律使用測試您的功能和程式碼 [!DNL Adobe Experience Manager] as a Cloud Service開發環境，再將功能移至預備或生產環境。

要安裝和配置本地Experience Manager環境，請執行以下步驟：

* [下載和解壓縮](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) the [!DNL Adobe Experience Manager] as a Cloud ServiceSDK
* [設定Author例項](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-author-service)
* [設定發佈例項](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-publish-service)

## 將Forms封存新增至本機製作和發佈執行個體，並設定Forms專用的使用者 {#add-forms-archive-configure-users}

在所列順序中執行下列步驟，將Forms封存新增至Experience Manager執行個體並設定表單專用使用者：

### 安裝最新的Forms附加元件功能封存 {#add-forms-archive}

Adobe Experience Manager Formsas a Cloud Service功能封存提供工具，可在本機開發環境中建立、設定樣式和最佳化最適化Forms。 安裝套件以建立最適化表單，並使用 [!DNL AEM Forms]. 要安裝包：

1. 下載並解壓縮最新 [!DNL AEM Forms] 從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

1. 導覽至crx-quickstart/install目錄。 如果資料夾不存在，請建立它。

1. 停止AEM執行個體，將 [!DNL AEM Forms] 附加功能歸檔， `aem-forms-addon-<version>.far`，並重新啟動執行個體。

### 設定使用者和權限 {#configure-users-and-permissions}

建立表單開發人員和表單從業人員等使用者，並 [將這些使用者新增至預先定義的表單群組](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=en#accessing) 提供必要的權限。 下表列出每種表單使用者類型的所有使用者類型和預先定義的群組：

| 使用者類型 | AEM群組 |
|---|---|
| 表單從業人員/ | [!DNL forms-users] (AEM Forms使用者)、 [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors]，和 [!DNL fdm-authors] |
| 表單開發人員 | [!DNL forms-users] (AEM Forms使用者)、 [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors]，和 [!DNL fdm-authors] |
| 客戶體驗銷售機會或UX設計工具 | [!DNL forms-users], [!DNL template-authors] |
| AEM 管理員 | [!DNL aem-administrators], [!DNL fd-administrators] |
| 一般使用者 | 當使用者必須登入才能檢視和提交適用性表單時，請將這類使用者新增至 [!DNL forms-users] 群組。 </br> 當存取適用性Forms不需要使用者驗證時，請勿將任何群組指派給這類使用者。 |

<!--  

## Set up a local AEM instance for development

Perform the following steps in the listed order to set up and configure your local development environment:

1. **Set up an AEM author instance:** You require an author instance to create Adaptive Forms. Download and extract the latest AEM SDK archive. Run the quick start file in author run mode to set up an author instance. For detailed instructions, see [default local instance](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html).  

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

1. **Install and configure Maven and set up an AEM project based on Apache Maven:** Apache Maven is an open-source tool for managing software projects. It helps automate builds and provides quality project information. It is the recommended build management tool for AEM projects. For detailed instructions to set up an AEM project based on Apache Maven, see [How to Build AEM Projects using Apache Maven](https://docs.adobe.com/content/help/en/experience-manager-65/developing/devtools/ht-projects-maven.html).

1. Configure the project to use [uber-jar](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html#install-aem-forms-jee-installer) version 6.5.5 or later and [[!DNL AEM Forms] Client SDK](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aemfd/aemfd-client-sdk/) version 6.0.160 or later.  

1. **Set Up an Integrated Development Environment:**  Set up an IDE of your choice for development, see [Set Up an Integrated Development Environment](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) for detailed instructions.
 -->

## 為記錄文檔(DoR)設定本地開發環境{#docker-microservices}

AEM Forms as aCloud Services提供以Docker為基礎的SDK環境，以更輕鬆開發記錄檔案和使用其他微服務。 如此一來，您就不必再手動設定平台特定的二進位檔和調整功能。 若要設定環境：

1. 安裝和配置Docker:

   * (適用於Microsoft Windows)安裝 [Docker Desktop](https://www.docker.com/products/docker-desktop). 它會在您的電腦上配置Docker引擎和Docker合成。

   * (Apple macOS)安裝 [適用於Mac的Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac). 它包括Docker引擎、Docker CLI客戶端、Docker撰寫、Docker內容信任、Kubernetes和憑據幫助程式。

   * （Linux適用）安裝 [Docker引擎](https://docs.docker.com/engine/install/#server) 和 [Docker Compose](https://docs.docker.com/compose/install/) 在你的機器上。
   >[!NOTE]
   >
   > * 若為Apple macOS，則會將包含本機AEM Author例項的白名單資料夾列入其中。
   >
   > * Docker Desktop for Windows支援兩個後端，Hyper-V
      > （舊版）和WSL2（現代版）。 檔案共用會自動
      > 使用WSL2時由Docker管理（現代）。 你必須
      > 使用Hyper-V（舊版）時顯式配置檔案共用。


1. 與製作和發佈例項平行建立資料夾，例如aem-sdk。 例如C:\aem-sdk。

1. 擷取 `aem-forms-addon-<version>.zip\aem-forms-addon-native-<version>.zip` 檔案。

   ![原生檔案中擷取的aem forms附加元件](assets/microservice-docker.png)

1. 建立環境變數AEM_HOME並指向本機AEM Author安裝。 例如C:\aem\author\。

1. 開啟sdk.bat或sdk.sh進行編輯。 設定AEM_HOME ，以指向本機AEM Author安裝。 例如C:\aem\author\。

1. 開啟命令提示字元並導覽至 `aem-forms-addon-native-<version>` 檔案夾。

1. 請確定您本機的AEM Author例項已啟動並執行。 執行下列命令以啟動SDK:

   * (在Microsoft Windows上) `sdk.bat start`
   * (在Linux或Apple Mac OS上) `AEM_HOME=[local AEM Author installation] ./sdk.sh start`

   >[!NOTE]
   >
   > 如果您已在sdk.sh檔案中定義環境變數，請在命令列中指定它為選用。 在命令行處定義環境變數的選項被提供來執行該命令，而不更新shell指令碼。

   ![start-sdk-command](assets/start-sdk.png)

您現在可以使用本機開發環境來轉譯記錄檔案。 若要測試，請上傳XDP檔案至您的環境並加以呈現。 例如， http://localhost:4502/libs/xfaforms/profiles/default.print.pdf?template=crx:///content/dam/formsanddocuments/check-request.xdp會將XDP檔案轉換為PDF檔案。

## 根據Experience Manager原型設定Forms的開發專案 {#forms-cloud-service-local-development-environment}

本專案可讓您在本機上建立適用性Forms、部署設定更新、覆蓋、建立自訂適用性表單元件、測試和自訂程式碼 [!DNL Experience Manager Forms] SDK. 在本機測試後，您可以將專案部署至  [!DNL Experience Manager Forms] as a Cloud Service的生產和非生產環境。 部署專案時，也會部署下列AEM Forms資產：

| 主題 | 範本 | 表單資料模型 |
---------|----------|---------
| 畫布3.0 | 基本 | Microsoft Dynamics 365 |
| 寧靜 | 空白 | Salesforce |
| 厄巴內 |  |  |
| 超海洋 |  |  |
| 柏利 |  |  |

>[!NOTE]
>
> 設定AEM Archetype 30版或更新版本型專案，以取得和使用Microsoft Dynamics 365和Salesforce表單資料模型，並搭配AEM Formsas a Cloud Service。
> 設定AEM Archetype 32版或更新版本型專案，以取得和使用具有AEM Formsas a Cloud Service的Tranquil、Urbane和Ultramarine主題。

若要設定專案：

1. **在本機開發執行個體上複製Cloud Manager Git存放庫：**  您的Cloud Manager Git存放庫包含預設的AEM專案。 其基礎為 [AEM原型](https://github.com/adobe/aem-project-archetype/). 使用Cloud Manager UI中的自助服務Git帳戶管理功能，原地複製您的Cloud Manager Git存放庫，將專案帶入本機開發環境。 有關訪問儲存庫的詳細資訊，請參閱 [存取儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

<!-- 1. 
After the repository is cloned, [integrate your Git repo with Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)

**Make cloned AEM project compatible with [!DNL AEM Forms] as a Cloud Service:** Remove uber-jar and other non-cloud dependencies from the pom.xml files of the project. You can refer the pom.xml files of the [sample AEM project](assets/FaaCSample.zip) for the list of required dependencies and update your AEM project accordingly. You can also refer [AEM Project Structure](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) to learn changes required to make an AEM project compatible with AEM as a Cloud Service.  -->

1. **建立 [!DNL Experience Manager Forms] as a [Cloud Service] 專案：** 建立 [!DNL Experience Manager Forms] as a [Cloud Service] 基於 [AEM原型32](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-32) 或更新版本。 原型可協助開發人員輕鬆開始開發 [!DNL AEM Forms] as a Cloud Service。 此外也包含一些範例主題和範本，可協助您快速上手。

   開啟命令提示字元，然後執行以下命令以建立 [!DNL Experience Manager Forms] as a Cloud Service專案。 要包括 [!DNL Forms] 特定配置、主題和模板，設定 `includeFormsenrollment=y`.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=32 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeFormsenrollment="y"
   ```

   此外，變更 `appTitle`, `appId`，和 `groupId`，以反映您的環境。

1. 將專案部署至本機開發環境。 您可以使用下列命令來部署至本機開發環境

   `mvn -PautoInstallPackage clean install`

   有關命令的完整清單，請參見 [建置和安裝](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [將程式碼部署至 [!DNL AEM Forms] as a Cloud Service環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).



## 設定本機Dispatcher工具 {#setup-local-dispatcher-tools}

Dispatcher是Apache HTTP Web伺服器模組，可在CDN和AEM Publish層級之間提供安全性和效能層。 Dispatcher是整體Experience Manager架構的必要部分，且應是本機開發環境的一部分。

執行下列步驟來設定本機Dispatcher，然後新增Forms專用規則至：

### 設定本機Dispatcher {#setup-local-dispatcher}

此 [!DNL Experience Manager] as a Cloud Service的SDK包含建議的Dispatcher工具版本，有助於在本機設定、驗證和模擬Dispatcher。 Dispatcher工具以Docker為基礎，並提供命令列工具，將Apache HTTP Web Server和Dispatcher組態檔傳輸成相容格式，並部署至在Docker容器中執行的Dispatcher。

Dispatcher上的快取允許 [!DNL AEM Forms] 在用戶端預填適用性Forms。 它可改善預填表單的轉譯速度。

如需設定Dispatcher的詳細指示，請參閱 [設定本機Dispatcher工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#local-development-environment-set-up)

### 將Forms特定規則新增至Dispatcher {#forms-specific-rules-to-dispatcher}

執行下列步驟來設定Experience Manager Formsas a Cloud Service的Dispatcher快取：

1. 開啟AEM專案並導覽至 `\src\conf.dispatcher.d\available_farms`
1. 建立 `default.farm` 檔案。 例如， `forms.farm`.
1. 開啟新建立的 `forms.farm` 檔案進行編輯並取代下列程式碼：

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

1. 儲存並關閉您的檔案。
1. 前往 `conf.d/enabled_farms` 並建立指向的符號連結 `forms.farm` 檔案。
1. 編譯專案並部署至您的 [!DNL AEM Forms] as a Cloud Service環境。

### 快取的考量事項 {#considerations-about-caching}

* Dispatcher快取允許 [!DNL AEM Forms] 在用戶端預填適用性Forms。 它可改善預填表單的轉譯速度。
* 預設會停用快取安全內容功能。 若要啟用功能，您可以執行 [快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=en) 文章
* Dispatcher無法使某些適用性Forms和相關的適用性Forms失效。 若要解決此類問題，請參閱 [[!DNL AEM Forms] 快取](troubleshooting-caching-performance.md) 疑難排解一節。
* 快取本地化適用性Forms:
   * 使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求本地化版本的最適化表單，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * 預設情況下禁用「瀏覽器區域設定」選項。 要更改瀏覽器區域設定，
* 使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`，且設定管理員中的「使用瀏覽器地區設定」已停用，則會提供非本地化版本的適用性表單。 非本地化語言是開發最適化表單時使用的語言。 未考慮為瀏覽器配置的地區設定（瀏覽器地區設定），並提供非本地化版本的適用性表單。
* 使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`，並啟用設定管理器中的「使用瀏覽器地區設定」 ，則會提供適用性表單的本地化版本（如果可用）。 本地化「適用性表單」的語言是根據為瀏覽器設定的地區（瀏覽器地區）。 這會導致 [僅快取適用性表單的第一個例項]. 若要防止問題在您的執行個體上發生，請參閱 [系統只會快取最適化表單的第一個例項](troubleshooting-caching-performance.md) 疑難排解一節。

您的本地開發環境已就緒。

## 升級您的本機開發環境 {#upgrade-your-local-development-environment}

將SDK升級至新版本需要取代整個本機開發環境，導致本機存放庫中的所有程式碼、設定和內容都遺失。 確保任何不應銷毀的程式碼、設定或內容都能安全提交至Git，或從本機Experience Manager執行個體匯出為CRX-Packages。

### 如何避免升級SDK時發生內容遺失 {#avoid-content-loss-when-upgrading--SDK}

升級SDK能有效建立全新的製作和發佈例項，包括新的存放庫([設定AEM專案](#forms-cloud-service-local-development-environment))，表示對先前SDK存放庫所做的任何變更都會遺失。 如需協助在SDK升級後持續保存內容的可行策略，請參閱 [升級AEM SDK時如何避免內容遺失](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#optional-local-aem-runtime-set-up-tasks)

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

For information about troubleshooting, stopping local AEM environment, run modes, and deployment, see [Set up local AEM Runtime](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#local-development-environment-set-up).-->

### 備份Forms特定內容並匯入新SDK環境 {#backup-and-import-Forms-specific-content-to-new-SDK-environment}

若要備份資產並將資產從現有SDK移至新的SDK環境：

* 建立現有內容的備份。

* 設定全新的SDK環境。

* 將備份匯入新SDK環境。

### 建立現有內容的備份 {#create-backup-of-your-existing-content}

備份最適化Forms、範本、表單資料模型、主題、設定和自訂程式碼。 您可以執行以下操作來建立備份：

1. [下載](import-export-forms-templates.md#manage-forms-and-related-assets) 最適化Forms、主題和PDF forms。
1. 匯出最適化表單範本。

1. 下載表單資料模型

1. 匯出可編輯的範本、雲端設定和工作流程模型。 若要從您現有的SDK匯出所有先前提及的項目，請建立 [CRX-Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html) ，並搭配下列篩選器：

   * /conf/ReferenceEditableTemplates
   * /conf/global/settings/cloudconfigs
   * /conf/global/settings/wcm
   * /var/workflow/models
   * /conf/global/settings/workflow
1. 從您的本機開發環境中，匯出電子郵件設定、提交和預填動作程式碼。 若要匯出這些設定和設定，請在本機開發環境中建立下列資料夾和檔案的復本：

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

### 將備份匯入新SDK環境 {#import-the-backup-to-your-new-SDK-environment}

將適用性Forms、範本、表單資料模型、主題、設定和自訂程式碼匯入全新環境。 您可以執行下列操作以導入備份：

1. [匯入](import-export-forms-templates.md#manage-forms-and-related-assets) 適用性Forms、主題和PDF forms，以適應新的SDK環境。
1. 將最適化表單範本匯入新SDK環境。

1. 將表單資料模型上傳至新的SDK環境。

1. 匯入可編輯的範本、雲端設定和工作流程模型。 若要匯入您新SDK環境中所有先前提及的項目，請將包含這些項目的CRX套件匯入至您的新SDK環境。

1. 從您的本機開發環境匯入電子郵件設定、提交和預填動作程式碼。 若要匯入這些設定和設定，請將下列檔案從您的舊原型專案放入您的新原型專案：

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

您的新環境現在擁有舊環境的表單和相關資產。
