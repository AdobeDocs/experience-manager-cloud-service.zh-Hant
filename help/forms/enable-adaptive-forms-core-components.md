---
title: 在AEM Formsas a Cloud Service和本機開發環境中啟用最適化Forms核心元件
seo-title: Step-by-Step Guide for enabling Adaptive Forms Core Components on AEM Forms as a Cloud Service and local development environment
description: 瞭解如何使用我們的逐步指南在AEM Formsas a Cloud Service上啟用最適化Forms核心元件。 我們的教學課程會逐步引導您完成此程式，讓您輕鬆為AEM Forms環境啟用此強大功能。
seo-description: Learn how to enable Adaptive Forms Core Components on AEM Forms as a Cloud Service with our step-by-step guide. Our tutorial walks you through the process, making it easy to enable this powerful feature for your AEM Forms environment.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 2%

---


# 在AEM Formsas a Cloud Service和本機開發環境中啟用最適化Forms核心元件 {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

在AEM Formsas a Cloud Service上啟用最適化Forms核心元件，可讓您使用AEM FormsCloud Service例項在多個管道中開始建立、發佈和提供核心元件型最適化Forms和Headless Forms。 您需要啟用最適化Forms核心元件的環境才能使用Headless最適化Forms。

## 考量事項

* 當您建立全新的AEM Formsas a Cloud Service程式時， [已針對您的環境啟用最適化Forms核心元件和Headless最適化Forms](#are-adaptive-forms-core-components-enabled-for-my-environment).

* 如果您的核心元件位於舊版Formsas a Cloud Service程式中， [未啟用](#enable-components)，您可以 [新增Adaptive Forms核心元件相依性](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment) 至您的AEMas a Cloud Service存放庫，並將存放庫部署至您的Cloud Service環境，以啟用Headless最適化Forms。

* 如果您現有的Cloud Service環境提供 [建立以核心元件為基礎的最適化Forms](creating-adaptive-form-core-components.md)、最適化Forms核心元件和Headless最適化Forms已針對您的環境啟用，而您可以將核心元件型最適化Forms當作Headless表單提供給需要最適化Forms的Headless呈現的行動裝置、網路、原生應用程式和服務等頻道。


## 啟用Adaptive Forms核心元件和Headless Adaptive Forms {#enable-headless-forms}

按照所列順序，執行以下步驟，為AEM Formsas a Cloud Service環境啟用最適化Forms核心元件和Headless最適化Forms


![](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## 1.複製您的AEM Formsas a Cloud ServiceGit存放庫 {#clone-git-repository}

1. 登入 [Cloud Manager](https://my.cloudmanager.adobe.com/) 並選取您的組織和方案。

1. 導覽至 **管道** 卡片來自您的 **計畫總覽** 頁面，按一下 **存取存放庫資訊** 按鈕來存取和管理您的Git存放庫。 此頁面包含下列資訊：

   * Cloud Manager Git存放庫的URL。
   * Git存放庫的認證（使用者名稱和密碼） Git使用者名稱。

   按一下 **產生密碼** 以檢視或產生密碼。

1. 在本機電腦上開啟終端機或命令提示字元，然後執行下列命令：

   ```Shell
   git clone [Git Repository URL]
   ```

   出現提示時，請提供認證。 存放庫已複製到您的本機電腦。


## 2.將最適化Forms核心元件相依性新增至您的Git存放庫 {#add-adaptive-forms-core-components-dependencies}

1. 以純文字程式碼編輯器開啟Git存放庫資料夾。 例如，VS程式碼。
1. 開啟 `[AEM Repository Folder]\pom.xml` 檔案進行編輯。
1. 取代以下版本： `core.forms.components.version`， `core.forms.components.af.version` 和 `core.wcm.components.version` 具有中指定的版本的元件 [核心元件檔案](https://github.com/adobe/aem-core-forms-components). 如果元件不存在，請新增這些元件。

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.forms.components.version>2.0.14</core.formscomponents.version>
       <core.forms.components.af.version>2.0.14</core.forms.components.af.version>  
       <core.wcm.components.version>2.21.2</core.wcmcomponents.version>
   </properties>
   ```

   ![提及最新版Forms核心元件](/help/forms/assets/latest-forms-component-version.png)

1. 在的相依性區段中 `[AEM Repository Folder]\pom.xml` 檔案、新增下列相依性並儲存檔案。

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <version>${core.wcm.components.version}</version>
               <type>zip</type>
           </dependency>    
           <!-- End of WCM Core Component Examples Dependencies -->
           <!-- Forms Core Component Dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
   <!-- End of AEM Forms Core Component Dependencies -->
   ```

1. 開啟 `[AEM Repository Folder]/all/pom.xml` 檔案進行編輯。 將下列相依性新增至 `<embeddeds>` 區段並儲存檔案。

   ```XML
   <!-- WCM Core Component Examples Dependencies -->
   
   <!-- inside plugin config of filevault-package-maven-plugin -->  
   <!-- embed wcm core components examples artifacts -->
   
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.config</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <!-- embed forms core components artifacts -->
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   ```

   >[!NOTE]
   >
   >
   >  Replace `${appId}` 與您的appId搭配使用。
   >
   >  尋找您的 `${appId}`，在 `[AEM Repository Folder]/all/pom.xml` 檔案，搜尋 `-packages/application/install` 詞語。 在之前的文字 `-packages/application/install` 辭彙是您的 `${appId}`. 例如，下列程式碼： `myheadlessform` 是 `${appId}`.
   >
   >   
   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. 在 `<dependencies>` 部分 `[AEM Repository Folder]/all/pom.xml` 檔案、新增下列相依性並儲存檔案：

   ```XML
           <!-- Other existing dependencies -->
           <!-- wcm core components examples dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <type>zip</type>
               </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
           </dependency>
               <!-- forms core components dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
           </dependency>
               <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
           </dependency>
   ```

1. 開啟 `[AEM Repository Folder]/ui.apps/pom.xml` 進行編輯。 新增 `af-core bundle` 相依性，並儲存檔案。

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >確保您的專案中不包含下列最適化Forms核心元件成品。
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-apps</artifactId>`
   >
   > `</dependency>`
   >
   > 和
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-core</artifactId>`
   >
   > `</dependency>`


1. 儲存並關閉檔案。

## 3.建置和部署更新的程式碼

將更新後的程式碼部署到您的本機開發和Cloud Service環境，以在這兩個環境中啟用核心元件：

* [在本機開發環境(AEMas a Cloud ServiceSDK)上建置和部署更新的程式碼](#core-components-on-aem-forms-local-sdk)

* [在AEM Formsas a Cloud Service環境中建置和部署更新的程式碼](#core-components-on-aem-forms-cs)

### 在本機開發環境中建置和部署更新的程式碼 {#core-components-on-aem-forms-local-sdk}

1. 開啟命令提示字元或終端機。

1. 導覽至Git存放庫專案的根目錄。

1. 執行以下命令，為您的環境建置套件：

   ```Shell
       mvn clean install
   ```



   成功建立套件後，您可在以下網址找到它： [Git存放庫資料夾]\all\target\[appid].all-[版本].zip

1. 使用 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant) 以部署 [AEM原型專案資料夾]\all\target\[appid].all-[版本].zip套件（在本機開發環境中）。


### 在AEM Formsas a Cloud Service環境中建置和部署更新的程式碼 {#core-components-on-aem-forms-cs}

1. 開啟終端機或命令提示。
1. 導覽至 `[AEM Repository Folder]` 並按列出的順序執行下列命令

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. 檔案提交至Git存放庫後， [執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

   管道執行成功後，Adaptive Forms核心元件會針對對應的環境啟用。 此外，最適化Forms （核心元件）範本和畫布3.0主題已新增到您的Formsas a Cloud Service環境中，為您提供可自訂和建立以核心元件為基礎的最適化Forms的選項。


## 常見問答 {#faq}

### 核心元件有哪些？ {#core-components}

此 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 是適用於AEM的一組標準化網頁內容管理(WCM)元件，可加快開發時間並降低網站的維護成本。

### 啟用核心元件時新增了哪些功能？ {#core-components-capabilities}

為您的環境啟用最適化Forms核心元件後，會向您的環境新增一個空白的核心元件式最適化表單範本和畫布3.0主題。 為您的環境啟用最適化Forms核心元件後，您可以：

* [建立以核心元件為基礎的最適化Forms](/help/forms/creating-adaptive-form-core-components.md).
* [建立以Core Components為基礎的最適化表單範本](/help/forms/template-editor.md).
* [建立核心元件型最適化表單範本的自訂主題](/help/forms/using-themes-in-core-components.md).
* [為行動、網路、原生應用程式等管道，以及需要表單Headless呈現的服務提供核心元件型最適化表單的JSON呈現](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html).

### Adaptive Forms Core Components是否已針對我的環境啟用？ {#enable-components}

若要檢查您的環境是否已啟用Adaptive Forms核心元件：

1. [複製您的AEM Formsas a Cloud Service存放庫](#1-clone-your-aem-forms-as-a-cloud-service-git-repository).

1. 開啟 `[AEM Repository Folder]/all/pom.xml` AEM FormsCloud ServiceGit存放庫的檔案。

1. 搜尋下列相依性：

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-app
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![在all/pom.xml中找到core-forms-components-af-core成品](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   如果相依性存在，則會在您的環境中啟用Adaptive Forms核心元件。

