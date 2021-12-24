---
title: '使用自訂字型 '
description: '使用自訂字型 '
source-git-commit: 7dd3785206b6d79caa500a155d3a6f3597303e65
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# 使用自訂字型

**Cloud Service通訊檔案正在測試中**

您可以使用Formsas a Cloud Service通訊，將XDP範本、XDP型PDF檔案或Acrobat Forms(AcroForm)與XML資料結合，以產生PDF檔案。 您可以使用系統字型(Cloud Service中包含的字型)或自定義字型（組織批准的字型）來渲染生成的PDF文檔。

系統字型已在Cloud Service中可用。 您可以使用Cloud Service開發專案，將自訂字型新增至Cloud Service環境。

## PDF檔案的行為

您可以 [嵌入字型](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) PDF文檔或僅指定字型的名稱。 嵌入字型時，PDF文檔在所有平台上都顯示（外觀）相同。 它使用內嵌字型來確保外觀和風格一致。 當字型未嵌入時，PDF呈現客戶端將在客戶端電腦上搜索字型。 如果該字型在客戶端電腦上可用，則PDF使用指定的字型，否則PDF將以後援字型呈現。

## 將自訂字型新增至Formsas a Cloud Service環境

若要將自訂字型新增至您的Cloud Service環境：

1. 設定並開啟本機開發專案。 您可以使用您選擇的任何IDE。
1. 在項目的頂層資料夾結構中，建立資料夾以保存自定義字型，並將自定義字型添加到資料夾。 例如，字型/src/main/resources
   ![字型資料夾](assets/fonts.png)

1. 開啟開發專案的頂層pom.xml檔案。
1. 新增 `<Font-Archive-Version>` 清單項目至.pom檔案，並將版本的值設為1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   </addDefaultEntries>
                   </addDefaultImplementationEntries>
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

1. 檢入更新的程式碼，並 [運行管道](/help/implementing/cloud-manager/deploy-code.md) 將字型部署至您的Cloud Service環境。
