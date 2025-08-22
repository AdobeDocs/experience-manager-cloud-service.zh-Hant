---
title: 如何在Forms as a Cloud Service和本機開發環境中啟用最適化AEM Forms核心元件？
description: 瞭解如何在AEM Forms as a Cloud Service上啟用最適化Forms核心元件。
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: 32a574e2-faa9-4724-a833-1e4c584582cf
hide: true
hidefromtoc: true
source-git-commit: 0845447c1c4f47b77debd179f24eac95a0d2c2db
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 75%

---

# 啟用最適化Forms核心元件 {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html) |
| AEM as a Cloud Service  | 本文章 |

在AEM Forms as a Cloud Service上啟用最適化Forms核心元件，可讓您開始建立、發佈及交付核心元件式的最適化Forms和Headless Forms ，並使用AEM Forms Cloud Service例項至多個管道。 您需要啟用調適型表單核心元件的環境才能使用 Headless 調適型表單。

## 考量事項

* 當您建立新的 AEM Forms as a Cloud Service 程序時，[系統已經為您的環境啟用調適型表單核心元件和 Headless 調適型表單](#are-adaptive-forms-core-components-enabled-for-my-environment)。

* 如果您有較舊版的 Forms as a Cloud Service 方案，且其中核心元件[未啟用](#enable-components)時，你可以[將調適型表單核心元件的相依性新增](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment)至您的 AEM as a Cloud Service 存放庫，並將該存放庫部署到您的 Cloud Service 環境以啟用 Headless 調適型表單。

* 如果您的現有Cloud Service環境提供[建立核心元件式最適化Forms](creating-adaptive-form-core-components.md)的選項，表示您的環境已啟用Adaptive Forms核心元件和Headless最適化Forms，而您可以將核心元件式最適化Forms當作Headless表單提供給需要最適化Forms的Headless呈現的管道。

## 啟用調適型表單核心元件和 Headless 調適型表單 {#enable-headless-forms}

依照所列順序執行以下步驟，為 AEM Forms as a Cloud Service 環境啟用調適型表單核心元件和 Headless 調適型表單


![啟用核心元件和Headless最適化表單](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## &#x200B;1. 原地複製您的 AEM Forms as a Cloud Service Git 存放庫 {#clone-git-repository}

1. 登入 [Cloud Manager](https://my.cloudmanager.adobe.com/)，並選取您的組織和計劃。

1. 從&#x200B;**計劃概觀**&#x200B;頁面瀏覽至&#x200B;**管道**&#x200B;卡，按一下「**存取存放庫資訊**」按鈕，以存取和管理您的 Git 存放庫。 此頁面包括以下資訊：

   * Cloud Manager Git 存放庫的 URL。
   * Git 存儲庫認證 (使用者名稱和密碼) Git 使用者名稱。

   按一下「**生成密碼**」，查看或生成密碼。

1. 在本機電腦上開啟終端或命令提示並執行以下命令：

   ```Shell
   git clone [Git Repository URL]
   ```

   出現提示時，提供認證。 原地複製 存放庫至本機電腦。


## &#x200B;2. 將調適型核心元件的相依性新增至您的 Git 存放庫 {#add-adaptive-forms-core-components-dependencies}

1. 在純文字程式碼編輯器中開啟 Git 存放庫資料夾。 例如 VS Code。
1. 閇啟 `[AEM Repository Folder]\pom.xml` 檔案進行編輯。
1. 以[核心元件文件](https://github.com/adobe/aem-core-forms-components)中指定的版本取代 `core.forms.components.version`、`core.forms.components.af.version` 和 `core.wcm.components.version` 等版本元件。如果該元件不存在，請新增這些元件。

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.wcm.components.version>2.22.10</core.wcm.components.version>
       <core.forms.components.version>2.0.18</core.forms.components.version>
       <core.forms.components.af.version>2.0.18</core.forms.components.af.version>
   </properties>
   ```

   ![提及最新版本的表單核心元件](/help/forms/assets/latest-forms-component-version.png)

1. 在 `[AEM Repository Folder]\pom.xml` 檔案的相依性部份中，新增以下相依性並儲存檔案。

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

1. 開啟 `[AEM Repository Folder]/all/pom.xml` 檔案進行編輯。 在 `<embeddeds>` 部份新增以下相依性並儲存檔案。

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
   >  以您的 appld 取代 `${appId}`。
   >
   >  若要尋找你的 `${appId}` (在 `[AEM Repository Folder]/all/pom.xml` 檔案內)，搜尋 `-packages/application/install` 一詞。在 `-packages/application/install` 一詞以前的文字是您的 `${appId}`。 例如，以下程式碼 `myheadlessform` 是 `${appId}`。
   >
   >   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. 在 `[AEM Repository Folder]/all/pom.xml` 檔案的 `<dependencies>` 部份中，新增以下相依性並儲存檔案：

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

1. 開啟 `[AEM Repository Folder]/ui.apps/pom.xml` 進行編輯。 新增 `af-core bundle` 相依性並儲存檔案。

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >確保您的專案中不包含以下調適型表單核心元件的成品。
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

## &#x200B;3. 建立並部署更新的程式碼

將更新後的程式碼部署到您的本機開發環境和 Cloud Service 環境，以在這兩個環境中啟用核心元件：

* [在本機開發環境中建立和部署更新的程式碼 (AEM as a Cloud Service SDK)](#core-components-on-aem-forms-local-sdk)

* [在 AEM Forms as a Cloud Service 環境中建立和部署更新的程式碼](#core-components-on-aem-forms-cs)

### 在本機開發環境中建立和部署更新的程式碼 {#core-components-on-aem-forms-local-sdk}

1. 開啟命令提示或終端機。

1. 瀏覽至 Git 存放庫專案的根目錄。

1. 執行以下命令為您的環境建立套件：

   ```Shell
       mvn clean install
   ```



   建立好套件後，你可以在 [Git 存放庫資料夾]\all\target\[appid].all-[version].zip 中找到套件

1. 使用[套件管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)，在本機開發環境中部署 [AEM Archetype 專案資料夾]\all\target\[appid].all-[version].zip 套件。


### 在 AEM Forms as a Cloud Service 環境中建立和部署更新的程式碼 {#core-components-on-aem-forms-cs}

1. 開啟終端機或命令提示。
1. 瀏覽至您的 `[AEM Repository Folder]`，並依所列順序執行以下命令

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. 將檔案提交到 Git 存放庫後，[執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)。

   執行好管道後，為對應環境啟用調適型表單核心元件。 此外，調適型表單 (核心元件) 範本和 Canvas 3.0 主題新增至您的 Forms as a Cloud Service 環境中，為您提供自訂和建以核心元件為主調適型表單的選項。


## 常見問答 {#faq}

### 核心元件有哪些？ {#core-components}

[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 是一組適用於 AEM 的標準化網站內容管理 (WCM) 元件，可加快開發時間並降低網站的維護成本。

### 啟用核心元件時新增哪些功能？ {#core-components-capabilities}

當為您的環境啟用調適型表單核心元件時，一個以核心元件為主的調適型表單空白範本和 Canvas 3.0 主題會新增至您的環境中。為您的環境啟用調適型表單核心元件後，您可以：

* [建立以核心元件為主的調適型表單](/help/forms/creating-adaptive-form-core-components.md)。
* [建立以核心元件為主的調適型表單範本](/help/forms/template-editor.md)。
* [為以核心元件為主的調適型表單範本建立自訂主題](/help/forms/using-themes-in-core-components.md)。
* [將以核心元件為主的調適型表單的代表提供給一些管道，例如行動、網頁、本機應用程式和需要表單以 Headless 呈現的服務。](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)。

### 系統是否已為我的環境啟用調適型表單核心元件？ {#enable-components}

若要查看系統是否已為您的環境啟用調適型表單核心元件：

1. [原地複製您的 AEM Forms as a Cloud Service 存放庫](#1-clone-your-aem-forms-as-a-cloud-service-git-repository)。

1. 開啟您 AEM Forms Cloud Service Git 存放庫的 `[AEM Repository Folder]/all/pom.xml` 檔案。

1. 搜尋以下相依性：

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![尋找 core-forms-components-af-core artifact in all/pom.xml](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   若相依性存在，表示系統已為您的環境啟用調適型表單核心元件。

### 核心元件型表單為何無法在專案中呈現？

由於Forms核心元件套件和專案原型中包含的版本不符，核心元件型表單可能無法呈現。 此問題通常發生在專案原型中指定的版本等於或高於Forms核心元件套件隨附的版本時。 若要解決此問題，請執行下列任一項作業：

* 在專案原型中使用較低版本的Forms核心元件套件。
* 從專案原型中移除Forms核心元件相依性，因為AEM as a Cloud Service已包含所需版本。 Forms核心元件套件自發行說20133開始與AEM as a Cloud SDK搭配，例如`AEM SDK v2025.3.20133.20250325T063357Z-250300`。

>[!MORELIKETHIS]
>
>* [建立最適化表單](/help/forms/creating-adaptive-form-core-components.md)
