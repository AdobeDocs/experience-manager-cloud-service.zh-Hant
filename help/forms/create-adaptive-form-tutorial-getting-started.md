---
title: 最適化Forms快速入門。
description: 請透過我們的逐步教學課程了解如何建立行動回應式最適化表單。這些表單可以在裝置之間無縫調適，確保流暢的體驗。
keywords: 最適化Forms、回應式Forms、HTML5 Forms
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
exl-id: b59cb56c-9629-48e4-b5c9-a861013a1360
source-git-commit: af58a784f24f212962ad73f11015fb788493d8b5
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 2%

---

# 建立最適化表單（核心元件） — 教學課程

在當今時代，使用者期望透過所有互動獲得適合行動裝置的體驗，表單也不例外。 調適型表單可協助您建立不僅適合行動裝置使用的表單，也有助於改善使用者參與，並降低完成表單所需的時間。

本教學課程提供建立最適化表單的逐步指南。 它分為使用案例和多個指南，每個指南都會教您如何將新功能新增至最適化表單。

在本教學課程結束時，您將能夠：

* 建立最適化表單及其資料模型
* 最適化表單的樣式
* 使用最適化表單規則編輯器建置商業規則
* 預填最適化表單欄位
* 新增電子簽章至您的表單
* 使用Google reCAPTCHA從機器人Protect您的表單
* 將不同語言的最適化表單當地語系化
* 設定您的表單以產生結構化資料
* 設定您的表單以提交資料至REST端點
* Publish您的最適化表單


## 為什麼要建立核心元件型表單？

AEM Forms提供基礎元件和核心元件，以建立表單體驗。 核心元件是建立任何新表單體驗的現代建議方法。 為何使用核心元件？ 這些元件輕量且開放原始碼（可在github上取得）、提供優異的Google Lighthouse和Web重要分數、相容於協助工具，並提供AEM Sites所有熟悉的功能（例如版本設定和本地化）。 此外，這些元件樣式更簡單，您可以根據組織的品牌指導方針輕鬆自訂其外觀。 這些元件沒有協力廠商相依性，任何瞭解JavaScript和CSS的開發人員都可以輕鬆自訂這些元件。

![為何要建立以最適化Forms為基礎的核心元件？ 這些元件輕量、更易於風格、提供Lighthouse高分數、支援協助工具標準、輕鬆自訂、開放原始碼、可在github上取得、不依賴第三方程式庫，並且幾乎對AEM開發人員和AEM作者沒有學習曲線。最上面，AEM Forms核心元件具有AEM WCM核心元件的所有功能。](/help/forms/assets/cc-core-components-benefits.png){width="50%"}

## 使用案例：透過最適化Forms簡化首頁貸款資格預審

在本教學課程中，您將為大型銀行建立最適化表單。 使用案例為：

潛在購房者請造訪銀行的網站或分行，以探索房屋貸款選項。 傳統的應用程式流程冗長且難以承受，通常需要事先提供說明檔案。 這會阻礙部分買家開始流程，進而影響銀行的銷售機會開發，以及買家自信地搜尋夢想家宅的能力。

您的任務是開發互動式住家貸款資格預審表單。 此表單會收集基本資訊、根據借款人的輸入預先確認其資格、提供預估貸款金額、潛在首期付款需求以及不同貸款型別的利率。 預先取得資格的使用者將能夠直接從預先取得資格表單中起始完整貸款申請。

表單將使用最適化表單建置。 這可提供個人化體驗，同時收集必要的財務資料，以取得精確的住家貸款預先資格。

完成教學課程後，您的表單外觀和運作方式將類似於以下表單：

![在此新增工作表單](/help/forms/assets/cc-tutorial-final-form.png)

## 設定開發環境

在將最適化表單部署至Cloud Service環境之前，您可以直接在本機電腦上建置和測試該表單。 Adobe為提供用於本機開發的AEM SDK，可讓您

* 在本機建立、自訂和測試表單。
* 在本機設計表單主題和建置設定，
* 輕鬆將完成的資產部署至雲端。

使用AEM SDK進行本機開發可節省您時間並簡化開發流程


**準備開始嗎？**

1. [設定AEM專案的開發工具](/help/forms/setup-local-development-environment.md#set-up-development-tools-for-aem-projects)：下載並安裝最新版本的[Java 11™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=zh-Hant#local-development-environment-set-up)、[Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=zh-Hant#install-git)、[Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=zh-Hant#node-js)和[Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=zh-Hant#install-maven)。 另外安裝純文字編輯器，本教學課程中的範例是以Visual Studio Code為基礎。

1. [安裝AEM SDK](/help/forms/setup-local-development-environment.md#set-up-local-experience-manager-environment-for-development)：下載並安裝最新版的AEM SDK。 這提供了AEM開發的基本工具。 記下AEM SDK的版本。

   ![軟體發佈](/help/forms/assets/software-distribution.png)

   ![安裝AEM SDK](/help/forms/assets/start-aem-sdk.png)

1. [新增AEM Forms附加元件](/help/forms/setup-local-development-environment.md#add-forms-archive-to-local-author-and-publish-instances-and-configure-forms-specific-users)：從[軟體發佈](https://experience.adobe.com/#/downloads)入口網站下載並安裝與AEM SDK版本相符的AEM Forms附加元件。
   ![install-aem-forms-add-on](/help/forms/assets/install-aem-forms-add-on.png)

   +++安裝AEM Forms附加元件：

   若要安裝AEM Forms附加元件：

   1. 停止AEM SDK。
   1. 將AEM Forms附加元件(.far)檔案新增至「`AEM SDK/crx-quickstart/install`」資料夾，
   1. 重新啟動AEM SDK。

   +++

1. [設定使用者許可權](/help/forms/setup-local-development-environment.md#configure-users-and-permissions)：建立具有開發、編寫和其他許可權的使用者，並將這些使用者新增至預先定義的表單群組。


1. [新增最適化Forms範本](/help/forms/setup-local-development-environment.md#set-up-a-development-project-for-forms-based-on-experience-manager-archetype)：使用AEM Archetypes 48或更新版本來建立新的AEM專案，並將其部署至您的AEM SDK。 專案會將最適化Forms範本新增至您的AEM SDK。

   ![最適化表單範本](/help/forms/assets/adaptive-forms-templates.png)

   +++將最適化Forms範本新增至您的AEM SDK：

   1. 執行以下命令以建立AEM專案。

      ```
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="48" -D appTitle=securbank -D appId=securbank -D groupId=com.securbank -D includeFormsenrollment="y" -D aemVersion="cloud"
      ```

      ![AEM-Archetyoe-Project](/help/forms/assets/aem-archetype-project.png)

   1. 將專案部署到您的本機開發環境。 您可以使用以下命令來部署到您的本機開發環境

      ```
      cd securbank
      
      mvn -PautoInstallPackage clean install
      ```

   部署AEM專案後，您可以在環境中檢視最適化Forms範本。

   +++


如需有關設定本機AEM Forms開發環境的詳細指示和逐步指南，請參閱[為AEM Forms設定本機開發環境](/help/forms/setup-local-development-environment.md)文章。



## 下一步

設定開發環境後，您就可以建立最適化表單了。 在下一篇文章中，您將學習

* 從空白範本建立最適化表單
* 顯示並輕鬆接受資訊的版面欄位。
* 預覽表單。

<!-- 

### Step 2: Create Form Data Model

A form data model lets you connect an adaptive form to disparate data sources. For example, AEM user profile, RESTful web services, SOAP-based web services, OData services, and relational databases. You can use the form data model with an adaptive form to retrieve, update, delete, and add data to connected data sources.

Goals of article:

* Create the form data model using Rest endpoint.
* Add data model objects so you can form the data model.
* Configure read and write services for the form data model.
* Test form data model and configured services with test data.

### Step 4: Apply rules to adaptive form fields

AEM Forms provide an editor to write rules on adaptive form objects. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps ensure accuracy and speeds up the form-filling experience.

Goals:

* Create and apply rules to adaptive form fields.
* Use rules to trigger form data model services to update the data to database.

### Step 5: Style your adaptive form

Adaptive forms provide OOTB themes and allows you to customize an existing theme to make a brand specific theme. 


A theme contains styling details for components and panels, and you can reuse a theme in different forms. Styles include properties such as background colors, state colors, transparency, alignment, and size. When you apply the theme to your form, the specified style reflects on corresponding components of your form.

Goals:

* Apply an out of the box theme to an adaptive form.
* Create your brand specific theme.


### Step 6: Publish your adaptive form

You can publish adaptive forms as a stand-alone form (single page application), include in AEM Sites page, or include in a non-AEM Sites page.

Goals:

* Publish the adaptive form as an AEM Page.
* Embed the adaptive form in an AEM Sites Page.
* Embed the adaptive form in an external webpage (a non-AEM webpage hosted outside AEM).

-->
