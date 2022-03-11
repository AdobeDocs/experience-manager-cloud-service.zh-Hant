---
title: 使用自定義字型
description: 使用自定義字型
exl-id: 88214d36-fb97-4d46-a9fe-71dbc7826eb1
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# 使用自定義字型

**Cloud Service通信文檔在測試版中**

可以使用Formsas a Cloud Service通信將XDP模板、基於XDP的PDF文檔或Acrobat表單(AcroForm)與XML資料組合起來，以生成PDF文檔。 您還可以使用「通信」來組合、重新排列和擴展PDF和XDP文檔，並獲取有關PDF文檔的資訊。

與前面提到的操作一起，您可以使用Cloud Service或自定義字型（組織批准的字型）中包含的字型來呈現生成的PDF文檔。 您可以使用Cloud Service開發項目將自定義字型添加到Cloud Service環境。

## PDF文檔的行為

你可以 [嵌入字型](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) 到PDF。 嵌入字型時，PDF文檔在所有平台上都顯示（看起來）相同。 它使用嵌入字型來確保外觀和感覺一致。 未嵌入字型時，字型呈現取決於PDF查看器客戶端(如Acrobat或Acrobat Reader)的呈現設定。 如果該字型在客戶端電腦上可用，則PDF使用指定的字型，否則PDF將使用預設回退字型呈現。

## 將自定義字型添加到您的Formsas a Cloud Service環境 {#custom-fonts-cloud-service}

要將自定義字型添加到Cloud Service環境：

1. 設定並開啟 [地方開發項目](setup-local-development-environment.md)。 可以使用您選擇的任何IDE。
1. 在項目的頂級資料夾結構中，建立一個資料夾（模組）以保存自定義字型，並將自定義字型添加到資料夾。 例如，字型/src/main/resources
   ![字型資料夾](assets/fonts.png)

1. 開啟開發項目字型模組的pom.xml檔案。
1. 將jar插件添加到pom檔案：

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


1. 添加 `<Font-Archive-Version>` manifest輸入.pom檔案並將版本值設定為1:

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

1. 將字型資料夾添加到 `<modules>` 在pom檔案中列出。 例如：

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

   字型資料夾包含所有自定義字型。

1. 簽入更新的代碼並 [運行管線](/help/implementing/cloud-manager/deploy-code.md) 將字型部署到Cloud Service環境。

1. （可選）開啟命令提示符，導航到本地項目資料夾，然後運行以下命令。 該命令將字型打包在.jar檔案中，並附帶相關資訊。 可以使用.jar檔案將自定義字型添加到FormsCloud Service本地開發環境。

   ```shell
   mvn clean install
   ```

## 將自定義字型添加到本地FormsCloud Service開發環境 {#custom-fonts-cloud-service-sdk}

1. 啟動本地開發環境。
1. 導航到 `<aem install directory>/crx-quickstart/install` 的子菜單。
1. 放置 `<jar file contaning custom fonts and relevant deployment code>.jar` 到安裝資料夾。 如果沒有.jar檔案，請執行中列出的步驟 [將自定義字型添加到您的Formsas a Cloud Service環境](#custom-fonts-cloud-service) 的子菜單。
1. 運行 [基於docker的SDK環境](setup-local-development-environment.md#docker-microservices)


   >[!NOTE]
   >
   >只要將更新的自定義字型.jar檔案部署到本地開發環境，請重新啟動基於Docker的SDK環境。
