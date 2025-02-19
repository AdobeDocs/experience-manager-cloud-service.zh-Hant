---
title: 如何在AEM Forms中使用自訂字型？
description: 瞭解如何將自訂字型新增至Formsas a Cloud Service環境。
exl-id: 88214d36-fb97-4d46-a9fe-71dbc7826eb1
feature: Adaptive Forms
role: Admin, User
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 使用自訂字型

**Cloud Service通訊檔案為測試版**

您可以使用Formsas a Cloud Service通訊來組合XDP範本、XDP型PDF檔案或Acrobat表單(AcroForm)與XML資料，以產生PDF檔案。 您也可以使用通訊來組合、重新排列和增加PDF和XDP檔案，並取得有關PDF檔案的資訊。

除了前述操作之外，您可以使用Cloud Service中包含的字型或自訂字型（組織核准的字型）來轉譯產生的PDF檔案。 您可以使用Cloud Service開發專案來新增自訂字型到您的Cloud Service環境。

## PDF檔案的行為

您可以[將字型](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions)內嵌至PDF檔案。 內嵌字型時，在所有平台上都會出現（看起來）相同的PDF檔案。 它使用內嵌字型以確保一致的外觀和感覺。 如果未內嵌字型，則字型轉譯會依據Acrobat或Acrobat Reader等PDF檢視器使用者端的轉譯設定而定。 如果使用者端電腦上有該字型，則PDF會使用指定的字型，否則會以預設的遞補字型呈現PDF。

## 新增自訂字型至您的Formsas a Cloud Service環境 {#custom-fonts-cloud-service}

若要將自訂字型新增至您的Cloud Service環境：

1. 設定並開啟[本機開發專案](setup-local-development-environment.md)。 您可以使用您選擇的任何IDE。
1. 在專案的頂層資料夾結構上，建立資料夾（模組）以儲存自訂字型並將自訂字型新增至資料夾。 例如，fonts/src/main/resources
   ![字型資料夾](assets/fonts.png)

1. 開啟開發專案之字型模組的pom.xml檔案。
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

1. 將`<Font-Archive-Version>`資訊清單專案加入.pom檔案，並將版本值設為1：

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

1. 將您的字型資料夾新增至pom檔案中所列的`<modules>`。 例如：

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

1. 簽入更新的程式碼並[執行管道](/help/implementing/cloud-manager/deploy-code.md)以將字型部署至您的Cloud Service環境。

1. （可選）開啟命令提示字元，瀏覽至本機專案資料夾，然後執行下列命令。 該命令會將字型封裝在.jar檔案中，並附上相關資訊。 您可以使用.jar檔案將自訂字型新增到FormsCloud Service本機開發環境中。

   ```shell
   mvn clean install
   ```

## 新增自訂字型至本機FormsCloud Service開發環境 {#custom-fonts-cloud-service-sdk}

1. 啟動您的本機開發環境。
1. 導覽至`<aem install directory>/crx-quickstart/install`資料夾。
1. 將`<jar file contaning custom fonts and relevant deployment code>.jar`放置到安裝資料夾。 如果您沒有.jar檔案，請執行[新增自訂字型至您的Formsas a Cloud Service環境](#custom-fonts-cloud-service)區段中列出的步驟，以產生檔案。
1. 執行[docker型SDK環境](setup-local-development-environment.md#docker-microservices)


   >[!NOTE]
   >
   >每當您將更新的自訂字型.jar檔案部署到本機開發環境時，請重新啟動Docker型SDK環境。
