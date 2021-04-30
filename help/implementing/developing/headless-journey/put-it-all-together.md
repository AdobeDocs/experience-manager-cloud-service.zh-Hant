---
title: 如何將所有內容整合在一起——您的應用程式和內容以無頭AEM形式
description: 在「無頭開發人AEM員歷程」的這部分，瞭解如何讓您的專案（包括內容片段、GraphQL呼叫、REST API呼叫和應用程式）做好上線準備。
hide: true
hidefromtoc: true
index: false
exl-id: 254fb9dd-36c8-43ce-aaea-ceb4d079503d
translation-type: tm+mt
source-git-commit: dc4f1e916620127ebf068fdcc6359041b49891cf
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# 如何將所有內容整合在一起——您的應用程式和內AEM容無頭{#put-it-all-together}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[AEM Headless Developer Journey的這部分，](overview.md)瞭解如何讓您的專案（包括內容片段）、您的GraphQL呼叫、您的REST API呼叫和您的應用程式)做好上線準備。

## 到目前為止的故事{#story-so-far}

在上一份無頭歷程的AEM檔案中，[如何透過AEM AssetsAPI更新您的內容](update-your-content.md)您已學會如何透過API更新您現有的無頭內AEM容，您現在應：

* 瞭解AEM AssetsHTTP API。

本文以這些基礎為基礎，讓您瞭解如何準備您自己的無AEM頭專案上線。

## 目標 {#objective}

* 安裝AEMSDK以取得本端開發執行階段，您可用來在
* 瞭解您所需的開發工具
* 在上線前先在本機測試您的程式碼和內容

## 本機開發工作流程{#the-local-development-workflow}

本端開發專案是以Apache Maven為基礎，並使用Git進行來源控制。 為了更新專案，開發人員可使用他們偏好的整合開發環境，例如Eclipse、Visual Studio程式碼或IntelliJ等。

若要測試無頭應用程式所擷取的程式碼或內容更新，您必須將更新部署至本機執行階段，其中包含作者的本機AEM例項AEM和發佈例項。

請務必注意本端執行階段中每個元件之間的差異AEM，因為在最重要的地方測試更新非常重要——例如，測試作者的內容更新或在發佈執行個體上測試新程式碼。

在生產系統中，調度程式和http Apache伺服器將始終位於發佈實例AEM前面。 它們為系統提供快取和安全AEM服務，因此必須針對分派程式測試程式碼和內容更新。

一旦您確定所有項目都經過測試並正常運作後，就可將程式碼更新推送至Cloud Manager的集中式Git儲存庫。

將更新上傳到Cloud Manager後，即可使用Cloud Manager的CI/CD管道將AEM其部署為Cloud Service。


## AEMSDK {#the-aem-sdk}

SDKAEM可用來建立和部署自訂程式碼。 它包含下列對象：

* Quickstart jar —— 可執行的jar檔案，可用於設定作者和發佈實例
* Dispatcher tools - Dispatcher模組及其對基於Windows和UNIX的系統的依賴性
* Java API Jar - Java Jar/Maven Dependency，它公開所有允許的可用於開發的Java API AEM
* Javadocjar - Java APIjar的javadoc

## 本地開發環境設定{#local-development-environment}

為了讓您的無頭專AEM案準備啟動，您需要確保專案的所有組成部分都正常運作。

為此，您需要將程式碼、內容和設定等一切整合在一起，並在本機開發環境中進行測試，以便上線準備。

地方發展環境由三個主要領域組成：

1. 專AEM案——這將包含開發人員將要處理的所有自訂程AEM式碼、設定和內容
1. 本機執AEM行階段——作AEM者和發佈服務的本機版本，將用來從專案部署程AEM式碼
1. The Local Dispatcher Runtime - Apache httpd webserver的本地版本，其中包含Dispatcher模組

## 開發工具{#development-tools}

除了SDK之AEM外，您還需要其他工具，以協助在本端開發和測試您的程式碼和內容：

* Java
* Git
* 阿帕奇·馬文
* Node.js程式庫
* 您選擇的IDE

由AEM於是Java應用程式，您必須安裝Java和Java SDK，才能支援將AEM其開發為Cloud Service。

Git是您用來管理來源控制以及簽入Cloud Manager的變更，然後將其部署至生產實例的工具。

使AEM用Apache Maven來建立從Maven Project原型產生AEM的專案。 所有主要IDE都提供Maven的整合支援。

Node.js是JavaScript執行時期環境，用於處理專案的ui.frontendAEM子專案的前端資產。 Node.js與npm一起分發，實際上是Node.js包管理器，用於管理JavaScript依賴性。

## 下一個{#what-is-next}

您應繼AEM續無頭之旅，請先檢閱檔案[如何與無頭應用程式一起上線](go-live.md)，您將無頭專案實際上AEM線！

## 其他資源 {#additional-resources}

* [本機開發環境設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-dispatcher-runtime) -瞭解如何安裝開始開發所需的工具AEM
* [作AEM為Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) -深入瞭解AEMSDK