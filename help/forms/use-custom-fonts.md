---
title: 使用自訂字型
description: 使用自訂字型
exl-id: 88214d36-fb97-4d46-a9fe-71dbc7826eb1
source-git-commit: d60659f443d130a195fd81cfe4773cd87df28264
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# 使用自訂字型

**Cloud Service通訊檔案正在測試中**

您可以使用Formsas a Cloud Service通訊將XDP範本、XDP型PDF檔案或Acrobat表單(AcroForm)與XML資料結合，以產生PDF檔案。 您也可以使用「通訊」來組合、重新排列及增強PDF和XDP檔案，並取得PDF檔案的相關資訊。

除了前面提到的操作，您還可以使用Cloud Service中包含的字型或自定義字型（組織批准的字型）來呈現生成的PDF文檔。 您可以使用Cloud Service開發專案，將自訂字型新增至Cloud Service環境。

## PDF檔案的行為

您可以 [嵌入字型](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions) 到PDF文檔。 嵌入字型時，PDF文檔在所有平台上都顯示（外觀）相同。 它使用嵌入的字型來確保一致的外觀和感覺。 未內嵌字型時，字型呈現取決於Acrobat或Acrobat Reader等PDF檢視器用戶端的呈現設定。 如果該字型在客戶端電腦上可用，則PDF使用指定的字型，否則PDF將以預設的後援字型呈現。

## 將自訂字型新增至Formsas a Cloud Service環境 {#custom-fonts-cloud-service}

若要將自訂字型新增至您的Cloud Service環境：

1. 設定並開啟 [地方開發項目](setup-local-development-environment.md). 您可以使用您選擇的任何IDE。
1. 在項目的頂層資料夾結構中，建立一個資料夾（模組）以保存自定義字型，並將自定義字型添加到資料夾。 例如，字型/src/main/resources
   ![字型資料夾](assets/fonts.png)

1. 開啟開發專案字型模組的pom.xml檔案。
1. 將jar外掛程式新增至pom檔案：

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
           </archive>
       </configuration>
   </plugin>
   ```


1. 新增 `<Font-Archive-Version>` 資訊清單輸入.pom檔案，並將版本的值設為1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
               <manifestEntries>
                   <Font-Archive-Version>1</Font-Archive-Version>
                   <Font-Archive-Contents>/</Font-Archive-Contents>
               </manifestEntries> 
           </archive>
       </configuration>
   </plugin>
   ```

1. 將字型資料夾新增至 `<modules>` 列在pom檔案中。 例如：

   ```xml
   <modules>
       <module>all</module>
       <module>core</module>
       <module>ui.frontend</module>
       <module>ui.apps</module>
       <module>ui.apps.structure</module>
       <module>ui.config</module>
       <module>ui.content</module>
       <module>it.tests</module>
       <module>dispatcher</module>
       <module>dispatcher.ams</module>
       <module>dispatcher.cloud</module>
       <module>ui.tests</module>
       <module>fonts</module>
   </modules>
   ```

   字型資料夾包含所有自訂字型。

1. 檢入更新的程式碼，並 [運行管道](/help/implementing/cloud-manager/deploy-code.md) 將字型部署至您的Cloud Service環境。

1. （可選）開啟命令提示，導航到本地項目資料夾，然後運行以下命令。 命令會將字型封裝在.jar檔案中，並附上相關資訊。 您可以使用.jar檔案將自訂字型新增至FormsCloud Service本機開發環境。

   ```shell
   mvn clean install
   ```

## 將自訂字型新增至本機FormsCloud Service開發環境 {#custom-fonts-cloud-service-sdk}

1. 啟動您的本機開發環境。
1. 導覽至 `<aem install directory>/crx-quickstart/install` 檔案夾。
1. 放置 `<jar file contaning custom fonts and relevant deployment code>.jar` 至安裝資料夾。 如果您沒有.jar檔案，請執行 [將自訂字型新增至Formsas a Cloud Service環境](#custom-fonts-cloud-service) 區段來產生檔案。
1. 執行 [基於docker的SDK環境](setup-local-development-environment.md#docker-microservices)


   >[!NOTE]
   >
   >每當您將更新的自訂字型.jar檔案部署至本機開發環境時，都會重新啟動以Docker為基礎的SDK環境。
